.. _component_attribute_tags:

|svg_attr_tags_22| |img_tags| Sélection multiple [tags]
========================================================

L'attribut « Sélection multiple [tags] » crée une
:ref:`relation m:n <component_relations_standard-relation-mton>` vers une autre
table — soit une table MetaModels, soit n'importe quelle table Contao (par ex.
``tl_member``, ``tl_page``). La liaison est enregistrée dans une table de
relation propre (``tl_metamodel_tag_relation``), de sorte qu'**aucune colonne
propre** n'est créée pour l'attribut dans la table du MetaModel. Cas
d'utilisation typiques :

* Association de plusieurs mots-clés (tags) à un produit
* Liaison d'un article avec plusieurs catégories ou auteurs
* Sélection de plusieurs régions, langues ou groupes cibles

La sélection peut être affichée dans le backend sous forme de liste de cases à
cocher, d'assistant à cases à cocher, de sélecteur arborescent ou de liste
déroulante consultable.

.. note:: Pour les relations entre deux MetaModels multilingues, la variante
   monolingue « Sélection multiple » devrait être utilisée — MetaModels détecte
   automatiquement la langue et change en conséquence.

.. seealso:: Pour les cas particuliers avec une colonne de langue propre dans la
   table référencée, l'attribut :ref:`component_attribute_translatedtags` est
   disponible.


Installation
------------

L'attribut s'installe via le **Contao Manager** ou **Composer** :

.. code-block:: bash

   composer require metamodels/attribute_tags


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
   * - Table de la base de données
     - La table à partir de laquelle les valeurs de sélection sont obtenues.
       Sont disponibles les tables MetaModels ainsi que toutes les tables de la
       base de données Contao.
   * - Colonne de table pour libellé/nom
     - La colonne de la table source dont le contenu est affiché comme
       libellé dans la liste de sélection.
   * - ID de la sélection multiple
     - La colonne servant d'identifiant unique (valeur enregistrée). Par
       défaut : ``id``.
   * - Alias de la sélection multiple
     - La colonne utilisée comme identifiant lisible dans les widgets de
       filtrage.
   * - Tri de la sélection multiple
     - Colonne selon laquelle la liste de sélection est triée.
   * - Sens du tri
     - Croissant (A → Z) ou décroissant (Z → A).
   * - SQL (condition WHERE)
     - Condition SQL WHERE optionnelle pour restreindre la liste de
       sélection. L'alias ``t`` représente la table source (par ex.
       ``t.published = '1'``). La condition ne filtre pas si le type de widget
       « Sélecteur popup » est sélectionné.
   * - Filtre
     - Sélection d'un jeu de filtres MetaModels pour restreindre
       dynamiquement les options.
   * - Paramètres de filtre
     - Valeurs par défaut pour les paramètres du jeu de filtres sélectionné.


Réglages dans les réglages de rendu
-------------------------------------

L'attribut Sélection multiple ne possède pas de réglages de rendu spécifiques.
Dans la liste des attributs d'un réglage de rendu, les options habituelles sont
disponibles :

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Option
     - Description
   * - Template
     - Sélection d'un template propre pour l'affichage des valeurs liées.
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
   * - Choisir le type d'affichage
     - Mode de présentation de la sélection multiple :

       * **Menu de cases à cocher** – liste de cases à cocher classique
       * **Assistant de cases à cocher** – liste de cases à cocher avec tri
         haut/bas
       * **Sélecteur popup** – sélection via un sélecteur arborescent (pour
         les tables source hiérarchiques comme ``tl_page`` ou ``tl_files``)
       * **Liste de tags** – liste déroulante consultable avec chosen.js
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

L'attribut Sélection multiple peut être utilisé avec les règles de filtre
suivantes :

.. list-table::
   :header-rows: 1
   :widths: 30 70

   * - Règle de filtre
     - Remarque
   * - Sélection multiple
     - Filtre selon une ou plusieurs valeurs sélectionnées de la table source ;
       par ex. tous les produits portant un tag déterminé.
   * - Filtre sur un attribut du modèle avec une relation
     - Filtre les items MetaModel selon la valeur d'un attribut du MetaModel
       lié ; par ex. tous les produits dont les tags possèdent une
       caractéristique déterminée.


Fonctions particulières
-------------------------

**Stockage en base de données**

Les relations ne sont **pas** enregistrées dans la table du MetaModel, mais
dans une table intermédiaire propre ``tl_metamodel_tag_relation`` avec les
colonnes ``att_id`` (ID de l'attribut), ``item_id`` (ID de l'item),
``value_id`` (ID du jeu de données lié) et ``value_sorting`` (ordre de tri).
Aucune colonne n'est ainsi nécessaire dans la table MM, et aucune migration de
base de données n'est requise.

**Condition SQL WHERE**

Dans la condition WHERE, l'alias ``t`` représente la table source. Exemple de
filtrage sur les entrées publiées :

.. code-block:: sql

   t.published = '1'


.. |svg_attr_tags_22| image:: /_img/icons_svg/tags.svg
   :width: 22px
.. |img_tags| image:: /_img/icons/tags.png
.. |br| raw:: html

   <br />
