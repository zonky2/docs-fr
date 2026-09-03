.. _component_attribute_tablemulti:

|svg_attr_tablemulti_22| |img_tablemulti| Table multiple (MCW)
==============================================================

L'attribut « Table multiple (MCW) » est une variante étendue de l'attribut
:ref:`Table de texte <component_attribute_tabletext>`. Au lieu de simples
saisies de texte, un type de widget propre peut être configuré dans chaque
cellule du tableau — par ex. liste déroulante, boutons radio, cases à cocher,
sélecteur de date ou champs de texte. Les données sont enregistrées dans une
table de valeurs propre, de sorte qu'**aucune colonne propre** n'est créée pour
l'attribut dans la table du MetaModel.

Cas d'utilisation typiques :

* Spécifications techniques avec des types de saisie mixtes (texte + sélection +
  date)
* Horaires d'ouverture avec sélection du jour de la semaine et champs horaires
* Listes de caractéristiques configurables avec saisie validée

.. warning:: La structure des colonnes (nombre et type des colonnes) n'est
   **pas** configurée dans le backend de MetaModels, mais dans un fichier de
   configuration PHP (``contao/config/config.php``). Cela requiert des
   connaissances de développeur.

.. seealso:: Pour les MetaModels multilingues, l'attribut
   :ref:`component_attribute_translatedtablemulti` est disponible.

.. seealso:: Cet attribut est pris en charge par l'intégration
   :ref:`File-Usage <rst_extended_file-usage>`. Elle permet d'afficher dans la
   gestion des fichiers de Contao si et où un fichier est utilisé.


Installation
------------

L'attribut s'installe via le **Contao Manager** ou **Composer** :

.. code-block:: bash

   composer require metamodels/attribute_tablemulti


Réglages lors de la création de l'attribut
-------------------------------------------

L'attribut ne possède pas de réglages propres dans le backend de MetaModels lors
de sa création. Seuls les réglages généraux de l'attribut sont utilisés :

* Nom, nom de colonne, description
* Autoriser le remplacement dans les variantes

La configuration proprement dite de la structure du tableau s'effectue dans le
fichier de configuration PHP via
``$GLOBALS['TL_CONFIG']['metamodelsattribute_multi']`` :

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
           'col_type' => [
               'label'     => 'Typ',
               'inputType' => 'select',
               'options'   => ['a' => 'Option A', 'b' => 'Option B'],
               'eval'      => ['style' => 'width:150px'],
           ],
       ],
   ];

Ici, ``mm_beispiel`` représente le nom de la table du MetaModel et ``mein_feld``
le nom de colonne de l'attribut.


Réglages dans les réglages de rendu
-------------------------------------

L'attribut possède un réglage de rendu propre :

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Option
     - Description
   * - Masquer l'en-tête du tableau
     - Masque les en-têtes de colonne dans l'affichage en frontend.
   * - Template
     - Sélection d'un template propre pour l'affichage.
   * - Classe CSS
     - Classe CSS optionnelle ajoutée à l'élément de sortie.


Réglages dans le masque de saisie
-----------------------------------

Lorsque l'attribut est ajouté à un masque de saisie, les options suivantes sont
disponibles :

**Présentation**

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Option
     - Description
   * - Classe backend
     - Classes CSS pour l'affichage du champ dans le formulaire du backend.
   * - Template pour le backend
     - Sélection d'un template de widget propre pour le formulaire du backend.


Règles de filtre
-------------------

L'attribut Table multiple peut être utilisé avec les règles de filtre
suivantes :

.. list-table::
   :header-rows: 1
   :widths: 30 70

   * - Règle de filtre
     - Remarque
   * - Sélection unique / Sélection multiple
     - Filtre selon les valeurs de cellule existantes (valeurs distinctes de la
       table de valeurs).


Fonctions particulières
-------------------------

**Stockage en base de données**

Les valeurs du tableau ne sont **pas** enregistrées dans la table du MetaModel,
mais dans une table de valeurs propre ``tl_metamodel_tablemulti`` avec les
colonnes ``att_id``, ``item_id``, ``row`` (index de ligne), ``col`` (identifiant
de colonne) et ``value``. Aucune colonne n'est ainsi créée dans la table MM et
aucune migration de base de données n'est nécessaire.

**Types de widget par colonne**

Contrairement à l'attribut Table de texte, chaque colonne peut être associée à
n'importe quel type de widget Contao : ``text``, ``select``, ``checkbox``,
``radio``, ``datePicker``, ``colorPicker``, etc.

**Format de stockage**

Les UUID binaires sont convertis en UUID lisibles avant l'enregistrement. Les
valeurs de type tableau sont enregistrées sérialisées et automatiquement
désérialisées à la lecture.


.. |svg_attr_tablemulti_22| image:: /_img/icons_svg/tablemulti.svg
   :width: 22px
.. |img_tablemulti| image:: /_img/icons/tablemulti.png
.. |br| raw:: html

   <br />
