.. _rst_cookbook_inputmask_manipulate-select-values:

Masque de saisie : compléter la sélection simple avec d'autres valeurs
======================================================================

Par défaut, la colonne de valeurs de l'attribut Sélection simple est limitée au choix
d'un attribut d'une table Contao quelconque. Si l'on souhaite afficher, dans le masque
de saisie de l'attribut Sélection simple, un ou plusieurs attributs/valeurs de la table
référencée, cela peut se faire de différentes façons :

**1. Attribut « Valeurs combinées »**

On crée dans le modèle référencé un attribut supplémentaire dans lequel les valeurs
sont combinées pour l'affichage.

**2. Événement « GetPropertyOptionsEvent »** (recommandé)

.. code-block:: php
   :linenos:

   <?php
   // src/EventListener/GetPropertyOptionsListener.php

   namespace App\EventListener;

   use Contao\MemberModel;
   use ContaoCommunityAlliance\DcGeneral\Contao\View\Contao2BackendView\Event\GetPropertyOptionsEvent;
   use MetaModels\AttributeSelectBundle\Attribute\AbstractSelect;
   use MetaModels\DcGeneral\Data\Model;
   use Terminal42\ServiceAnnotationBundle\Annotation\ServiceTag;

   /**
    * @ServiceTag("kernel.event_listener", event="dc-general.view.contao2backend.get-property-options", priority="100")
    */
   class GetPropertyOptionsListener
   {
       public function __invoke(GetPropertyOptionsEvent $event)
       {
           // Check if options set.
           if ($event->getOptions() !== null) {
               return;
           }

           // Check if right model table and type.
           if ('mm_my_model' !== $event->getEnvironment()->getDataDefinition()->getName()) {
               return;
           }

           $model = $event->getModel();
           if (!($model instanceof Model)) {
               return;
           }

           // Check if right attribute and type.
           if ('member' !== $event->getPropertyName()) {
               return;
           }

           $attribute = $model->getItem()->getAttribute($event->getPropertyName());
           if (!($attribute instanceof AbstractSelect)) {
               return;
           }

           // Generate own options list.
           $members     = MemberModel::findAll(['order' => 'lastname ASC']); // add e.g. filter for not disabled...
           $aliasColumn = $attribute->get('select_alias');

           $options = [];

           foreach ($members as $member) {
               $options[$member->{$aliasColumn}] =
                   \sprintf('%s, %s [%s]', $member->lastname, $member->firstname, $member->email);
           }

           $event->setOptions($options);
       }
   }

Résultat : |br|
|img_manipulate-select-values_01|

Référence : |br|
`GetPropertyOptionsListener <https://github.com/MetaModels/attribute_select/blob/master/src/EventListener/GetPropertyOptionsListener.php>`_

**3. Callback DCA « options_callback »**

.. code-block:: php
   :linenos:

   <?php
   // contao/dca/<Nom-Table-MM>.php
   $GLOBALS['TL_DCA']['<Nom-Table-MM>']['fields']['<Nom-Colonne-MM-Select>'] = [
    'options_callback' => function () {
        $modelName = '<Nom-Table-MM-Select>';
        $factory   = $this->getContainer()->get('metamodels.factory');
        $model     = $factory->getMetaModel($modelName);
        $filter    = $model->getEmptyFilter();
        $items     = $model->findByFilter($filter);
        $arrItems  = $items->parseAll('text');

        $options = [];
        foreach ($arrItems as $arrItem) {
            $options[$arrItem['text']['<Nom-Colonne-MM-Select-Alias>']] = \sprintf(
            '%s [%s]',
            $arrItem['text']['<Nom-Colonne-MM-Select-1>'],
            $arrItem['text']['<Nom-Colonne-MM-Select-2>']
            );
        }

        return $options;
       },
   ];

Les clés du tableau ``$options`` doivent correspondre au réglage « Alias » des
réglages de l'attribut.

Les filtres définis dans l'attribut « Select » pour le backend sont ainsi
contournés.


.. |img_manipulate-select-values_01| image:: /_img/screenshots/cookbook/inputmask/manipulate-select-values_01.jpg

.. |br| raw:: html

   <br />
