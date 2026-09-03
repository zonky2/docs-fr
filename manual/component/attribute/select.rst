.. _component_attribute_select:

|svg_attr_select_22| |img_select| Sélection unique [select]
===========================================================

L'attribut « Sélection unique [select] » crée une
:ref:`relation 1:n <component_relations_standard-relation-1ton>` vers une autre
table — soit une table MetaModels, soit n'importe quelle table Contao (par ex.
``tl_member``, ``tl_page``). L'ID du jeu de données sélectionné est enregistré
dans la base de données. Cas d'utilisation typiques :

* Association d'un produit à une catégorie
* Liaison d'un article avec un auteur
* Sélection d'une page Contao comme page cible

La sélection peut être affichée dans le backend sous forme de liste déroulante,
de liste de boutons radio ou de sélecteur arborescent.

.. note:: Pour les relations entre deux MetaModels multilingues, la variante
   monolingue « Sélection unique » devrait être utilisée — MetaModels détecte
   automatiquement la langue et change en conséquence.

.. seealso:: Pour les cas particuliers avec une colonne de langue propre dans la
   table référencée, l'attribut :ref:`component_attribute_translatedselect` est
   disponible.


Installation
------------

L'attribut s'installe via le **Contao Manager** ou **Composer** :

.. code-block:: bash

   composer require metamodels/attribute_select


Réglages lors de la création de l'attribut
-------------------------------------------

Outre les réglages généraux de l'attribut (nom, nom de colonne, description,
autoriser le remplacement dans les variantes), l'attribut propose les options
spécifiques suivantes :

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Option
     - Description
   * - Table source
     - La table à partir de laquelle les valeurs de sélection sont obtenues.
       Sont disponibles les tables MetaModels ainsi que toutes les tables de la
       base de données Contao.
   * - Colonne de valeur
     - La colonne de la table source dont le contenu est affiché comme
       libellé dans la liste de sélection.
   * - Colonne d'ID
     - La colonne servant d'identifiant unique (valeur enregistrée). Par
       défaut : ``id``.
   * - Colonne d'alias
     - La colonne utilisée comme identifiant lisible dans les widgets de
       filtrage. En cas de doute, choisir la même colonne que pour la colonne
       d'ID.
   * - Tri de la sélection
     - Colonne selon laquelle la liste de sélection est triée.
   * - Sens du tri
     - Croissant (A → Z) ou décroissant (Z → A).
   * - SQL (condition WHERE)
     - Condition SQL WHERE optionnelle pour restreindre la liste de
       sélection. L'alias ``sourceTable`` représente la table source (par ex.
       ``sourceTable.published = '1'``). La condition ne filtre pas si le
       type de widget « Sélecteur popup » est sélectionné.
   * - Filtre
     - Sélection d'un jeu de filtres MetaModels pour restreindre
       dynamiquement les options.
   * - Paramètres de filtre
     - Valeurs par défaut pour les paramètres du jeu de filtres sélectionné.


Réglages dans les réglages de rendu
-------------------------------------

L'attribut Sélection unique ne possède pas de réglages de rendu spécifiques.
Dans la liste des attributs d'un réglage de rendu, les options habituelles sont
disponibles :

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Option
     - Description
   * - Template
     - Sélection d'un template propre pour l'affichage de la valeur liée.
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
   * - Template pour le frontend
     - Sélection d'un template de widget propre pour l'édition en frontend
       (disponible uniquement si l'extension « Frontend Editing » est installée).
   * - Type d'affichage
     - Mode de présentation de la sélection :

       * **Menu de sélection (Select)** – menu déroulant classique
       * **Liste de boutons radio** – toutes les options sous forme de
         boutons radio
       * **Sélecteur popup** – sélection via un sélecteur arborescent (pour
         les tables source hiérarchiques comme ``tl_page`` ou ``tl_files``)
   * - Niveau le plus bas (arbre)
     - Pour le sélecteur arborescent : les jeux de données en dessous de ce
       niveau ne sont pas sélectionnables (0 = aucune restriction).
   * - Niveau le plus haut (arbre)
     - Pour le sélecteur arborescent : les jeux de données au-dessus de ce
       niveau ne sont pas sélectionnables (0 = aucune restriction).

**Fonctions**

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Option
     - Description
   * - Champ obligatoire
     - Rend le champ obligatoire.
   * - Afficher une option vide
     - Affiche une option de sélection vide, afin qu'aucune présélection ne
       soit faite.

**Aperçu (filtre et recherche backend)**

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Option
     - Description
   * - Filtrable
     - L'attribut est disponible comme critère de filtrage dans le backend.
   * - Cherchable
     - L'attribut est disponible comme champ de recherche dans le backend.


Règles de filtre
-------------------

L'attribut Sélection unique peut être utilisé avec les règles de filtre
suivantes :

.. list-table::
   :header-rows: 1
   :widths: 30 70

   * - Règle de filtre
     - Remarque
   * - Sélection unique
     - Filtre selon une valeur sélectionnée de la table source ; par ex. tous
       les produits d'une catégorie déterminée.
   * - Filtre sur un attribut du modèle avec une relation
     - Filtre les items MetaModel selon la valeur d'un attribut du MetaModel
       lié ; par ex. tous les produits dont la catégorie possède une
       caractéristique déterminée.


Fonctions particulières
-------------------------

**Stockage en base de données**

L'ID du jeu de données sélectionné est enregistré sous la forme ``int(11) NULL``
dans la table du MetaModel.

**Types de table source**

Peuvent être choisies comme table source :

* **Tables MetaModels** – avec accès complet à tous les attributs
* **Tables Contao non traduites** – toute table de la base de données Contao
* **Tables SQL** – sélection directe de table via un alias SQL

**Condition SQL WHERE**

Dans la condition WHERE, l'alias ``sourceTable`` représente la table source.
Exemple de filtrage sur les entrées publiées :

.. code-block:: sql

   sourceTable.published = '1'


.. |svg_attr_select_22| image:: /_img/icons_svg/select.svg
   :width: 22px
.. |img_select| image:: /_img/icons/select.png
.. |br| raw:: html

   <br />
