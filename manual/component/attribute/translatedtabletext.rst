.. _component_attribute_translatedtabletext:

|svg_attr_translatedtabletext_22| |img_translatedtabletext| Table de texte traduite
========================================================================================

L'attribut « Table de texte traduite » est la variante multilingue de
l'attribut :ref:`Table de texte <component_attribute_tabletext>`. Il permet
la saisie de données textuelles dans une structure tabulaire avec des
colonnes configurées — avec des libellés de colonnes et des valeurs de
données propres à chaque langue. Les données sont stockées dans une table de
traduction dédiée, de sorte qu'**aucune colonne propre** n'est créée pour
l'attribut dans la table du MetaModel.

Domaines d'application typiques :

* Tableaux de spécifications multilingues (par ex. « Propriété + valeur » en
  FR et EN)
* Horaires d'ouverture traduits avec des noms de jours de la semaine
  dépendants de la langue
* Listes de prix ou tableaux de caractéristiques spécifiques à la langue

.. seealso:: La variante monolingue de cet attribut est décrite dans
   :ref:`component_attribute_tabletext`.

.. seealso:: Des indications sur le multilinguisme dans MetaModels se
   trouvent sur la page :ref:`component_multi-language`.


Installation
------------

L'attribut s'installe via le **Contao Manager** ou **Composer** :

.. code-block:: bash

   composer require metamodels/attribute_translatedtabletext


Réglages à la création de l'attribut
-------------------------------------

Outre les réglages généraux de l'attribut, l'attribut propose les options
spécifiques suivantes :

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Option
     - Description
   * - Nombre de colonnes
     - Détermine le nombre de colonnes du tableau. Cette valeur détermine
       combien de colonnes peuvent être configurées dans l'assistant de
       colonnes multilingue.
   * - Réglage des colonnes (traduit)
     - Assistant multi-colonnes pour définir les libellés de colonnes par
       langue. Pour chaque langue et chaque colonne, il est possible
       d'indiquer :

       * **Langue** – code de langue (par ex. ``fr``, ``en``)
       * **Libellé** – désignation de la colonne dans cette langue
       * **Largeur** – largeur de la colonne dans le masque de saisie
         (par ex. ``200px``)

       Les libellés de colonnes sont affichés de façon spécifique à la
       langue dans le backend et dans le template frontend.
   * - Nombre minimal de lignes
     - Nombre minimal de lignes de données affichées dans le masque de
       saisie (0 = pas de minimum imposé).
   * - Nombre maximal de lignes
     - Nombre maximal de lignes de données pouvant être saisies (0 = pas de
       limite).
   * - Désactiver le tri
     - Masque les boutons Haut/Bas pour le tri manuel des lignes dans le
       masque de saisie.


Réglages dans les réglages de rendu
--------------------------------------

L'attribut possède son propre réglage de rendu :

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Option
     - Description
   * - Masquer l'en-tête de tableau
     - Masque les en-têtes de colonnes (libellés) dans l'affichage frontend.
   * - Template
     - Choix d'un template personnalisé pour l'affichage. Si aucun template
       n'est indiqué, l'affichage se fait sous forme de tableau HTML.
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

.. list-table::
   :header-rows: 1
   :widths: 30 70

   * - Règle de filtre
     - Remarque
   * - Recherche par Levenshtein
     - Recherche par similarité avec tolérance aux fautes de frappe, sur
       toutes les valeurs de cellule de la langue active ; nécessite le
       paquet ``attribute_levenshtein``.
   * - Loupe
     - Recherche par index plein texte sur toutes les valeurs de cellule ;
       nécessite le paquet ``filter_loupe`` (à partir de MM 2.4).


Fonctions spéciales
---------------------

**Stockage**

Les valeurs du tableau sont stockées de façon spécifique à la langue dans
``tl_metamodel_translatedtabletext`` (champs : ``att_id``, ``item_id``,
``langcode``, ``row`` (index de ligne), ``col`` (index de colonne),
``value``). La table du MetaModel ne reçoit pas de colonne propre.

**Libellés de colonnes dépendants de la langue**

Contrairement à la table de texte monolingue, les en-têtes de colonnes
peuvent être définis différemment selon la langue. Dans le template
frontend, les libellés de colonnes de la langue active sont affichés.

**Langue de repli**

S'il manque une valeur pour une langue, MetaModels se rabat sur la langue de
repli.

**Structure des colonnes dans le template**

Dans le template frontend, les valeurs sont disponibles sous forme de
tableau imbriqué : ``$arrData['raw']`` contient des lignes (row) avec des
colonnes (col_0, col_1, …), les noms de colonnes étant générés
automatiquement à partir du nombre de colonnes. Les libellés de colonnes
traduits sont disponibles sous ``$arrData['cols']``.


.. |svg_attr_translatedtabletext_22| image:: /_img/icons_svg/translatedtabletext.svg
   :width: 22px
.. |img_translatedtabletext| image:: /_img/icons/translatedtabletext.png
.. |br| raw:: html

   <br />
