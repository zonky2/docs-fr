.. _rst_cookbook_tips_backend-section:

Section personnalisée dans la navigation du backend
========================================================

On souhaite souvent regrouper l'accès à la saisie des données MetaModel dans une section dédiée de la navigation du
backend. Pour cela, il faut créer un groupe correspondant, auquel on peut assigner le ou les modèles souhaités dans
les propriétés du masque de saisie, sous « Zone du backend ».

|img_be-section|


Par configuration (à partir de MM 2.5, recommandé)
--------------------------------------------------------

Depuis MetaModels 2.5, un tel groupe peut être créé directement via le ``config.yaml`` - sans aucun code
personnalisé :

.. code-block:: yaml

   meta_models_core:
       be_sections:
           products:
               name:
                   de: 'Produkte'
                   en: 'Products'
               tooltip:
                   de: 'Produkte erstellen'
                   en: 'Create products'
               icon: 'files/theme/mm/products.svg'
               add:
                   before: design

``products`` est ici l'alias unique de la zone - il sera ensuite sélectionné dans le masque de saisie, sous
« Zone du backend ».

* ``name`` (obligatoire) - table de langues pour le libellé. C'est la langue de backend actuelle qui est affichée,
  sinon l'anglais, sinon la première entrée disponible.
* ``tooltip`` (optionnel) - table de langues pour l'infobulle, résolue de la même manière que ``name``. Sans
  indication, c'est ``name`` qui est utilisé.
* ``icon`` (optionnel) - chemin web vers une icône, généralement sous la gestion des fichiers Contao ``files/…``.
  Sans indication - ou si le fichier indiqué n'est pas trouvé - l'icône grise standard de MetaModels est affichée.
* ``add`` (obligatoire) - définit la position par rapport à une entrée de navigation existante, via exactement l'une
  des deux indications ``before`` ou ``after``.
* ``collapsed`` (optionnel, valeur par défaut ``false``) - fait démarrer la zone repliée lors du premier affichage.

.. note:: L'alias cible sous ``add`` est le nom de groupe **interne** de Contao, et non le libellé affiché - la
   zone « Layout » s'appelle en interne ``design`` depuis Contao 4/5, et non ``layout``. Les cibles courantes sont
   ``content``, ``design``, ``accounts``, ``system`` ou l'alias d'une autre zone créée elle aussi par
   configuration. Si l'alias indiqué ne se trouve pas dans la navigation, la zone personnalisée est ajoutée à la
   fin à la place.

Cette configuration crée exclusivement le **groupe vide**. Il se remplit comme d'habitude : dans les propriétés du
masque de saisie d'un MetaModel, saisir sous « Zone du backend » l'alias choisi (ici ``products``).

.. seealso:: `core#1519 <https://github.com/MetaModels/core/issues/1519>`_, ainsi que la section
   « Zones de backend personnalisées par configuration » dans :ref:`new_in_mm250`.


Manuellement via un Event-Listener (pour les cas particuliers)
---------------------------------------------------------------------

Si la configuration ci-dessus ne suffit pas - par exemple parce que la visibilité ou le libellé de la zone doit
dépendre de conditions à l'exécution (utilisateur connecté, contenu de la base de données, etc.) - le même type de
zone peut toujours être construit via un listener ``MenuEvent`` personnalisé, comme c'était le seul moyen avant MM
2.5.

Pour cela, il faut une icône SVG ainsi qu'une assignation via le MenuEvent de Contao.

On peut par exemple télécharger des icônes SVG sur `material.io <https://material.io/tools/icons/>`_ - la largeur
(width), la hauteur (height) et la couleur (fill) doivent être adaptées dans un éditeur de texte, comme dans
l'exemple :

.. code-block:: svg
   :linenos:

    <svg xmlns="http://www.w3.org/2000/svg" fill="#91979c" width="15" height="15" viewBox="0 0 24 24">
        <path d="...."/>
    </svg>

Le fichier peut par exemple être enregistré sous ``files/backend/group_icon_mm-test.svg`` (rendre le dossier
public).

Il faut en outre un Event-Listener qui crée l'entrée - les paramètres suivants permettent de configurer le groupe
(lignes 30 à 34) :

* $nodeName - alias de l'entrée
* $nodeTitle - titre
* $nodeIcon - chemin vers l'icône
* $targetNode - recherche d'une entrée existante, comme « content » pour Contenus
* $targetType - indication si l'entrée doit apparaître avant (``before``) ou après (``after``) le « targetNode »

Placer le listener dans le chemin ``src/EventListener/BackendMenuListener.php`` et exécuter ``composer install``.

.. code-block:: php
   :linenos:

   <?php

   namespace App\EventListener;

   use Contao\CoreBundle\Event\MenuEvent;
   use Knp\Menu\Util\MenuManipulator;
   use Symfony\Component\EventDispatcher\Attribute\AsEventListener;
   use Symfony\Component\HttpFoundation\RequestStack;
   use Symfony\Component\HttpFoundation\Session\Attribute\AttributeBagInterface;

   #[AsEventListener(priority: -1)]
   class BackendMenuListener
   {
       private array $targetTypes = ['before' => 0, 'after' => 1];

       public function __construct(
           private readonly RequestStack $requestStack,
       ) {
       }

       public function __invoke(MenuEvent $event): void
       {
           $factory = $event->getFactory();
           $tree    = $event->getTree();

           if ('mainMenu' !== $tree->getName()) {
               return;
           }

           $nodeName   = 'mm-test';
           $nodeTitle  = 'Meine MM Kategorie';
           $nodeIcon   = '/files/backend/group_icon_mm-test.svg';
           $targetNode = 'content';
           $targetType = 'after';

           $categoryNode = $tree->getChild($nodeName);
           if (!$categoryNode) {
               $sessionBag  = $this->requestStack->getSession()->getBag('contao_backend');
               $status      = ($sessionBag instanceof AttributeBagInterface) ? $sessionBag->get('backend_modules') : [];
               $isCollapsed = ($status[$nodeName] ?? 1) < 1;

               $categoryNode = $factory
                   ->createItem($nodeName)
                   ->setLabel($nodeTitle)
                   ->setUri('/contao?mtg=' . $nodeName)
                   ->setLinkAttribute('class', 'group-' . $nodeName)
                   ->setLinkAttribute('title', $nodeTitle)
                   ->setLinkAttribute('data-action', 'contao--toggle-navigation#toggle:prevent')
                   ->setLinkAttribute('data-contao--toggle-navigation-category-param', $nodeName)
                   ->setLinkAttribute('aria-controls', $nodeName)
                   ->setLinkAttribute('aria-expanded', $isCollapsed ? 'false' : 'true')
                   ->setChildrenAttribute('id', $nodeName)
                   ->setLinkAttribute('style', \sprintf('background: url(%s) 3px 2px no-repeat;', $nodeIcon))
                   ->setExtra('translation_domain', false);

               if ($isCollapsed) {
                   $categoryNode->setAttribute('class', 'collapsed');
               }

               $tree->addChild($categoryNode);

               $targetPosition = \array_search($targetNode, \array_keys($tree->getChildren()), true);
               $targetPosition = false === $targetPosition ? 0 : $targetPosition + $this->targetTypes[$targetType];
               $manipulator    = new MenuManipulator();
               $manipulator->moveToPosition($categoryNode, $targetPosition);
           }
       }
   }
   ?>

Le listener ainsi qu'un fichier SVG factice sont disponibles :download:`ici en téléchargement </_download/BE-section.zip>`.


.. |img_be-section| image:: /_img/screenshots/cookbook/tips/be-section_01.png
