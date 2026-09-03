.. _component_attribute_translatedtablemulti:

|svg_attr_translatedtablemulti_22| |img_translatedtablemulti| Table multiple traduite (MCW)
================================================================================================

L'attribut « Table multiple traduite (MCW) » est la variante multilingue de
l'attribut :ref:`Table multiple <component_attribute_tablemulti>`. Il permet
d'avoir des valeurs de tableau propres à chaque langue avec la même
structure de colonnes. Les données sont stockées dans une table de
traduction dédiée, de sorte qu'**aucune colonne propre** n'est créée pour
l'attribut dans la table du MetaModel.

Domaines d'application typiques :

* Spécifications techniques multilingues avec types de saisie mixtes
* Horaires d'ouverture ou tableaux de caractéristiques traduits

.. warning:: La structure des colonnes n'est **pas** configurée dans le
   backend de MetaModels, mais dans un fichier de configuration PHP. Cela
   nécessite des connaissances en développement.

.. seealso:: La variante monolingue de cet attribut est décrite dans
   :ref:`component_attribute_tablemulti`.

.. seealso:: Des indications sur le multilinguisme dans MetaModels se
   trouvent sur la page :ref:`component_multi-language`.

.. seealso:: Cet attribut est pris en charge par l'intégration
   :ref:`File-Usage <rst_extended_file-usage>`. Elle permet d'afficher dans
   la gestion des fichiers de Contao si et où un fichier est utilisé.


Installation
------------

L'attribut s'installe via le **Contao Manager** ou **Composer** :

.. code-block:: bash

   composer require metamodels/attribute_translatedtablemulti


Réglages à la création de l'attribut
-------------------------------------

L'attribut ne possède pas de réglages propres dans le backend de
MetaModels. La configuration de la structure de tableau s'effectue dans le
fichier de configuration PHP via
``$GLOBALS['TL_CONFIG']['metamodelsattribute_multi']`` — identique à la
variante monolingue :

.. code-block:: php

   $GLOBALS['TL_CONFIG']['metamodelsattribute_multi']['mm_beispiel']['mein_feld'] = [
       'minCount'     => 0,
       'maxCount'     => 0,
       'columnFields' => [
           'col_name' => [
               'label'     => 'Bezeichnung',
               'inputType' => 'text',
               'eval'      => ['style' => 'width:200px'],
           ],
       ],
   ];


Réglages dans les réglages de rendu
--------------------------------------

L'attribut possède son propre réglage de rendu :

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Option
     - Description
   * - Masquer l'en-tête de tableau
     - Masque les en-têtes de colonnes dans l'affichage frontend.
   * - Template
     - Choix d'un template personnalisé pour l'affichage.
   * - Classe CSS
     - Classe CSS optionnelle ajoutée à l'élément de sortie.


Réglages dans le masque de saisie
------------------------------------

Lorsque l'attribut est ajouté à un masque de saisie, les options suivantes
sont disponibles :

**Présentation**

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Option
     - Description
   * - Classe backend
     - Classes CSS pour la présentation du champ dans le formulaire backend.
   * - Template pour le backend
     - Choix d'un template de widget personnalisé pour le formulaire backend.
   * - Template pour le frontend
     - Choix d'un template de widget personnalisé pour l'édition en frontend
       (uniquement si « Frontend Editing » est installé).


Règles de filtre
-------------------

L'attribut Table multiple traduite ne prend en charge aucune règle de
filtrage — ``getFilterOptions()`` retourne un tableau vide.


Fonctions spéciales
---------------------

**Stockage**

Les valeurs du tableau sont stockées de façon spécifique à la langue dans
``tl_metamodel_translatedtablemulti`` (champs : ``att_id``, ``item_id``,
``langcode``, ``row``, ``col``, ``value``). La table du MetaModel ne reçoit
pas de colonne propre.

**Langue de repli**

S'il manque une valeur pour une langue, MetaModels se rabat automatiquement
sur la langue de repli.

**Différence avec la variante monolingue**

La seule différence structurelle avec la table multiple monolingue est la
colonne ``langcode`` supplémentaire dans la table de valeurs et l'utilisation
des méthodes ``getTranslatedDataFor()`` et ``setTranslatedDataFor()``, qui
tiennent compte de la langue.


.. |svg_attr_translatedtablemulti_22| image:: /_img/icons_svg/translatedtablemulti.svg
   :width: 22px
.. |img_translatedtablemulti| image:: /_img/icons/translatedtablemulti.png
.. |br| raw:: html

   <br />
