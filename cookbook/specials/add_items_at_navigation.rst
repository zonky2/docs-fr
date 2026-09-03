.. _rst_cookbook_specials_add_items_at_navigation:

Afficher des pages de détail dans la navigation Contao
==========================================================

Dans le module FE de navigation Contao, seules les pages présentes dans l'arborescence des pages sont affichées comme
point de navigation, par ex. ``/produkte/uebersicht``. Si l'on souhaite afficher, en plus des pages Contao, des pages
de détail telles que ``/produkt/detail/artikelnummer/1364``, alors qu'il n'existe que la page ``/produkt/detail`` dans
l'arborescence, plusieurs approches sont possibles.


Pages dédiées dans l'arborescence avec alias pour la redirection
--------------------------------------------------------------------

S'il existe une page Contao ``/produkt/detail`` où l'article souhaité est affiché via le paramètre de slug
``artikelnummer/1364``, on peut ajouter une nouvelle page dans l'arborescence, à l'endroit voulu pour la navigation,
par ex. avec le titre « Artikel 1364 ». L'alias de la page est cependant réglé manuellement sur l'alias de la vue de
détail ``/produkt/detail/artikelnummer/1364``. Pour que le contenu souhaité s'affiche bien lors de l'appel du lien de
navigation « Artikel 1364 », la page ``/produkt/detail`` doit recevoir une priorité de route plus élevée (10) que la
page ``artikelnummer/1364`` (0).

:ref:`Plus de conseils sur la priorité des routes <rst_cookbook_tips_set-route-priority>`.


ParseTemplateListener pour adapter la navigation
----------------------------------------------------

Avec le `ParseTemplateListener <https://docs.contao.org/5.x/dev/reference/hooks/parseTemplate/>`_, le template
``nav_default`` (ou ses propres variantes) peut encore être manipulé avant sa « livraison ». Cela permet d'insérer, à
l'endroit souhaité, ses propres liens de navigation (voir ``getSublinks()``). Voici un exemple de code :

.. code-block:: php
   :linenos:

   <?php
   // src/EventListener/ParseTemplateListener.php

   namespace App\EventListener;

   use Contao\CoreBundle\DependencyInjection\Attribute\AsHook;
   use Contao\Template;
   use MetaModels\Filter\Setting\IFilterSettingFactory;
   use MetaModels\IFactory;
   use MetaModels\IMetaModel;
   use MetaModels\Render\Setting\IRenderSettingFactory;
   use Symfony\Component\HttpFoundation\RequestStack;

   use function sprintf;
   use function str_replace;
   use function trim;

   #[AsHook('parseTemplate')]
   class ParseTemplateListener
   {
       public function __construct(
           private readonly IFactory $factory,
           private readonly IFilterSettingFactory $filterFactory,
           private readonly IRenderSettingFactory $renderFactory,
           private readonly RequestStack $requestStack,
       ) {
       }

       public function __invoke(Template $template): void
       {
           if ('nav_default' === $template->getName()) {
               $levelData = $template->getData();

               // Check only level 1.
               if ('level_1' !== $levelData['level']) {
                   return;
               }

               $items = $levelData['items'];
               foreach ($items as &$item) {
                   // Check only page id 7.
                   if (7 !== ($item['id'] ?? null)) {
                       continue;
                   }

                   // Add subitems as level 2 at page id 7 and mark parent as trail.
                   if ([] !== ($subLinks = $this->getSublinks())) {
                       $item['subitems'] = $subLinks['subitems'];
                       $item['class']    =
                           trim(
                               'submenu ' . ($subLinks['trail'] ? str_replace('sibling', 'trail', $item['class']) : '')
                           );
                   }
               }
               unset($item);
               $levelData['items'] = $items;

               $template->setData($levelData);
           }
       }

       private function getSublinks(): array
       {
           // Begin configuration.
           $modelName = 'mm_employees';
           $renderId  = 4;
           $filterId  = 3;
           // End configuration.

           if (!(($model = $this->factory->getMetaModel($modelName)) instanceof IMetaModel)) {
               return [];
           }

           $filter           = $model->getEmptyFilter();
           $filterCollection = $this->filterFactory->createCollection($filterId);
           $filterCollection->addRules($filter, []);
           $items = $model->findByFilter($filter);

           if (!$items->getCount()) {
               return [];
           }

           $parsed = $items->parseAll('text', $this->renderFactory->createCollection($model, $renderId));
           unset($items, $filterCollection, $filter, $model);

           $request = $this->requestStack->getCurrentRequest();
           if (null === $request) {
               return [];
           }
           $path        = $request->getRequestUri();
           $isTrail     = false;
           $subLinkList = '<ul class="level_2">';
           foreach ($parsed as $item) {
               $href = $item['actions']['jumpTo']['href'];
               // Possibly clean up the path+href from GET parameters or anchor links.
               if ($path !== $href) {
                   $subLinkList .= sprintf(
                       '<li><a href="%1$s" title="%2$s">%2$s</a></li>',
                       $href,
                       $item['text']['name']
                   );
               } else {
                   $isTrail     = true;
                   $subLinkList .= sprintf(
                       '<li class="active"><strong class="active" aria-current="page">%s</strong></li>',
                       $item['text']['name']
                   );
               }
           }
           $subLinkList .= '</ul>';

           return ['trail' => $isTrail, 'subitems' => $subLinkList];
       }
   }

Pour en savoir plus sur l'enregistrement de services, voir :ref:`l'article associé <rst_cookbook_specials_register-services>`.


Extension « hofff/contao-navigation » et « TreeEvent »
-----------------------------------------------------------

L'extension « `Contao-Navigation <https://github.com/hofff/contao-navigation>`_ » propose son propre module FE pour
la navigation. Elle dispose en outre de différents événements permettant de manipuler la sortie de manière plus
élégante qu'avec le ``ParseTemplateListener``. Voici un exemple de code pour ajouter un lien supplémentaire dans la
navigation - il peut également être adapté pour afficher des pages de détail MM.

.. code-block:: php
   :linenos:

   <?php
   // src/EventListener/NavigationMenuListener.php

   namespace App\EventListener;

   use Hofff\Contao\Navigation\Event\TreeEvent;
   use Symfony\Component\EventDispatcher\Attribute\AsEventListener;

   use function array_keys;

   #[AsEventListener('Hofff\Contao\Navigation\Event\TreeEvent')]
   class NavigationMenuListener
   {
       public function __invoke(TreeEvent $treeEvent): void
       {
           $moduleId  = $treeEvent->moduleModel()->id; // Id du module pour vérifier qu'il s'agit du bon module.
           $pageId    = $treeEvent->items()->currentPage->id; // Id de la page pour vérifier qu'il s'agit de la bonne page.
           $pageItems = $treeEvent->items(); // Récupérer les éléments de page pour l'arbre de navigation.
           $rootIds   = $pageItems->roots;

           // Ajouter un nouvel élément à la première racine, en dernière position.
           $pageItems->subItems[array_keys($rootIds)[0]][] = 9999;

           // Données de l'élément.
           $pageItems->items[9999] = [
               'class'     => 'mm-page',
               'isInTrail' => false,
               'isActive'  => false,
               'pageTitle' => 'MetaModels',
               'accesskey' => '',
               'target'    => 'target="_blank"',
               'link'      => 'MetaModels',
               'href'      => 'https://now.metamodel.me',
           ];
       }
   }

Pour en savoir plus sur l'enregistrement de services, voir :ref:`l'article associé <rst_cookbook_specials_register-services>`.
