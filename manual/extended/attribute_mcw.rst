.. _rst_extended_attribute_mcw:

Attribut pour Multi-Column-Wizard
==================================

Le Multi-Column-Wizard (MCW) permet de définir un tableau de saisie variable
avec différents types de saisie comme texte, cases à cocher, sélection dans les
colonnes - pour en savoir plus sur les possibilités du MCW, voir
`Github <https://github.com/MetaModels/attribute_tablemulti>`_ ou le
`Wiki Contao <http://de.contaowiki.org/MultiColumnWizard>`_.

Avec l'extension `attribute_tablemulti <https://github.com/MetaModels/attribute_tablemulti>`_
le MCW peut être utilisé comme attribut dans MetaModels. Il faut cependant noter
que le MCW ne peut pas être configuré entièrement depuis le backend, mais nécessite
un fichier de configuration DCA correspondant. De plus, il n'est pas possible de
rechercher ou de filtrer sur les valeurs enregistrées de l'attribut MCW.
Les valeurs du MCW sont enregistrées dans la base de données sous forme de tableau sérialisé.

Outre la version mentionnée, il existe également le pendant pour une utilisation
multilingue sous la forme de l'extension
`attribute_translatedtablemulti <https://github.com/MetaModels/attribute_translatedtablemulti>`_

L'attribut MCW peut par exemple être utilisé pour saisir, dans un masque de saisie,
un nombre variable d'entrées comportant différents types de saisie. Un exemple simple
serait la saisie de plusieurs liens avec un champ de texte pour l'URL, un champ de
texte pour le texte du lien et une case à cocher pour la cible du lien.

L'installation et l'utilisation se composent des points suivants

* Installation de l'attribut via Composer depuis Github ou via le Contao Manager
* Adaptation du fichier de configuration DCA


Adaptation du fichier de configuration DCA
--------------------------------------------

Le fichier de configuration DCA ``<nom-de-la-table-mm>.php`` ou ``config.php`` doit être
placé à un endroit approprié de l'installation Contao, ou un fichier existant doit être
complété avec les indications correspondantes. Cela peut se faire par exemple sous la forme

* contao/dca/<nom-de-la-table-mm>.php
* contao/config/config.php

ou dans son propre bundle sous

* src/AppBundle/Resources/contao/dca/<nom-de-la-table-mm>.php
* src/AppBundle/Resources/contao/config/config.php

Ce fichier doit être adapté avec un éditeur en fonction de vos propres paramètres de
MetaModel et des champs souhaités - voir le `Wiki Contao <http://de.contaowiki.org/MultiColumnWizard>`_.

Une configuration pour le MetaModel "mm_my_table" avec l'attribut MCW "my_mcw"
pourrait se présenter comme suit :

.. code-block:: php
   :linenos:

   <?php
   // /contao/dca/mm_my_table.php

   $GLOBALS['TL_CONFIG']['metamodelsattribute_multi']['mm_my_table']['my_mcw'] = array(
      'minCount'     => 2,
      'maxCount'     => 4,
      'tl_class'     => 'clr w50',
      'columnFields' => array(
         'ts_client_os'     => array(
            'label'     => 'Meine Optionen',
            'exclude'   => true,
            'inputType' => 'select',
            'options'   => array(
               'option1' => 'Option 1',
               'option2' => 'Option 2',
            ),
            'eval'      => array('style' => 'width:250px', 'includeBlankOption' => true, 'chosen' => true)
         ),
         'ts_client_mobile' => array(
            'label'     => 'Meine Checkbox',
            'exclude'   => true,
            'inputType' => 'checkbox',
            'eval'      => array('style' => 'width:40px')

         ),
         'ts_extension'     => array(
            'label'     => 'Das Textfeld',
            'inputType' => 'text',
            'eval'      => array('mandatory' => true, 'style' => 'width:115px')
         ),
      ),

   );

Remarque : les intitulés dans "label" peuvent également être intégrés sous forme de tableau de langue.

Après avoir adapté la configuration, videz le cache !

Aperçu dans le masque de saisie :

|img_input_mask|

.. note:: à partir de MM 2.4, les deux "attributs MM-MCW" prennent également en charge le type de saisie ``fileTree``,
   avec sélection multiple, affichage en galerie et possibilité de tri.

La configuration d'une sélection d'images avec tri individuel se présente comme suit :

.. code-block:: php
   :linenos:

   <?php
   // /contao/dca/mm_my_table.php

   $GLOBALS['TL_CONFIG']['metamodelsattribute_multi']['mm_my_table']['my_mcw'] = [
       'tl_class'     => 'clr',
       'minCount'     => 0,
       'columnFields' => [
           'col_title'     => [
               'label'     => 'Title',
               'exclude'   => true,
               'inputType' => 'text',
               'eval'      => [
                   'style'         => 'width:100%',
                   'tl_class'      => 'my_class',
                   'wrapper_style' => 'width:50%',
               ]
           ],
           'col_images' => [
               'label'     => 'Dateiauswahl',
               'exclude'   => true,
               'inputType' => 'fileTree',
               'eval'      => [
                   'filesOnly'     => true,
                   'multiple'      => true,
                   'fieldType'     => 'checkbox',
                   'isGallery'     => true,
                   'orderField'    => 'col_images',
                   'extensions'    => \Contao\Config::get('validImageTypes'),
                   'isSortable'    => true,
                   'style'         => 'width:100%',
                   'tl_class'      => 'my_class',
                   'wrapper_style' => 'width:50%',
               ]
           ],
       ],
   ];

.. |img_input_mask| image:: /_img/screenshots/extended/attribute_mcw/input_mask.jpg
