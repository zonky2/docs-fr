.. _component_attribute_tabletext:

|svg_attr_tabletext_22| |img_tabletext| Table de texte
=======================================================

L'attribut « Table de texte » permet la saisie de données texte dans une
structure tabulaire avec des colonnes configurées et un nombre de lignes
quelconque. Les données sont enregistrées dans une table de valeurs propre, de
sorte qu'**aucune colonne propre** n'est créée pour l'attribut dans la table du
MetaModel. Cas d'utilisation typiques :

* Plusieurs URL ou numéros de téléphone par jeu de données (par ex. « URL +
  libellé »)
* Spécifications techniques sur plusieurs lignes (par ex. « Propriété +
  Valeur »)
* Horaires d'ouverture (par ex. « Jour de la semaine + De + À »)
* Listes de prix avec plusieurs colonnes

Le nombre et la désignation des colonnes sont définis lors de la création de
l'attribut. Dans le masque de saisie, un nombre quelconque de lignes peut alors
être ajouté.

.. seealso:: Pour les MetaModels multilingues, l'attribut
   :ref:`component_attribute_translatedtabletext` est disponible.


Installation
------------

L'attribut s'installe via le **Contao Manager** ou **Composer** :

.. code-block:: bash

   composer require metamodels/attribute_tabletext


Réglages lors de la création de l'attribut
-------------------------------------------

Outre les réglages généraux de l'attribut (nom, nom de colonne, description,
autoriser le remplacement dans les variantes), l'attribut Table de texte propose
les options spécifiques suivantes :

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Option
     - Description
   * - Réglage des colonnes
     - Définition des colonnes du tableau. Pour chaque colonne, les éléments
       suivants sont indiqués :

       * **Libellé** – désignation de la colonne (apparaît comme en-tête de
         colonne dans le masque de saisie et dans le template frontend)
       * **Largeur** – largeur de la colonne dans le masque de saisie (par ex.
         ``200px``, ``50%``) ; n'a aucune influence sur l'affichage en
         frontend.

       Le nombre de lignes dans le réglage des colonnes détermine le nombre
       de colonnes du tableau.
   * - Nombre minimal de lignes
     - Nombre minimal de lignes de données affichées dans le masque de saisie
       (0 = aucune valeur minimale imposée).
   * - Nombre maximal de lignes
     - Nombre maximal de lignes de données pouvant être saisies (0 = aucune
       limite).
   * - Désactiver le tri
     - Masque les boutons haut/bas permettant le tri manuel des lignes dans le
       masque de saisie.


Réglages dans les réglages de rendu
-------------------------------------

L'attribut Table de texte possède un réglage de rendu propre :

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Option
     - Description
   * - Masquer l'en-tête du tableau
     - Masque les en-têtes de colonne (libellés) dans l'affichage en frontend.
   * - Template
     - Sélection d'un template propre pour l'affichage. Si aucun template
       n'est indiqué, l'affichage se fait sous forme de tableau HTML.
   * - Classe CSS
     - Classe CSS optionnelle ajoutée à l'élément de sortie.


Réglages dans le masque de saisie
-----------------------------------

Lorsque l'attribut Table de texte est ajouté à un masque de saisie, les options
suivantes sont disponibles :

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
   * - Template pour le frontend
     - Sélection d'un template de widget propre pour l'édition en frontend
       (disponible uniquement si l'extension « Frontend Editing » est installée).


Règles de filtre
-------------------

L'attribut Table de texte peut être utilisé avec les règles de filtre
suivantes :

.. list-table::
   :header-rows: 1
   :widths: 30 70

   * - Règle de filtre
     - Remarque
   * - Recherche assistée par Levenshtein
     - Recherche par similarité avec tolérance aux fautes de frappe sur toutes
       les valeurs de cellule ; nécessite le paquet ``attribute_levenshtein``.
   * - Loupe
     - Recherche par index plein texte sur toutes les valeurs de cellule ;
       nécessite le paquet ``filter_loupe`` (à partir de MM 2.4).


Fonctions particulières
-------------------------

**Stockage en base de données**

Les valeurs du tableau ne sont **pas** enregistrées dans la table du MetaModel,
mais dans une table de valeurs propre ``tl_metamodel_tabletext`` avec les
colonnes ``item_id``, ``att_id``, ``row`` (index de ligne), ``col`` (index de
colonne) et ``value``. Aucune colonne n'est ainsi créée dans la table MM et
aucune migration de base de données n'est nécessaire.

**Structure des colonnes dans le template**

Dans le template frontend, les valeurs sont disponibles sous forme de tableau
imbriqué : ``$arrData['raw']`` contient des lignes (row) avec des colonnes
(col_0, col_1, …), les noms de colonnes étant générés automatiquement à partir
du réglage des colonnes.


.. |svg_attr_tabletext_22| image:: /_img/icons_svg/tabletext.svg
   :width: 22px
.. |img_tabletext| image:: /_img/icons/tabletext.png
.. |br| raw:: html

   <br />
