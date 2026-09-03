.. _component_attribute_translatedtags:

|svg_attr_translatedtags_22| |img_tags| Sélection multiple traduite [tags]
==============================================================================

L'attribut « Sélection multiple traduite » est une extension de l'attribut
:ref:`Sélection multiple <component_attribute_tags>`. Il est utilisé lorsque
la table source référencée possède sa propre colonne de langue — par exemple
une table externe avec un champ ``language``. Les associations sont stockées
comme pour l'attribut monolingue dans la table de relation
``tl_metamodel_tag_relation``, de sorte qu'aucune colonne propre n'est créée
dans la table du MetaModel.

Domaines d'application typiques :

* Sélection multiple dans une table externe dépendante de la langue (par ex.
  des mots-clés issus d'une table avec colonne de langue)
* Association avec des tables multilingues propres à Contao
* Scénarios dans lesquels la table source elle-même fournit des entrées
  dépendantes de la langue et où MetaModels doit filtrer selon la langue
  active

.. note:: Pour les relations entre deux tables MetaModels multilingues,
   l'attribut Sélection multiple monolingue suffit généralement — MetaModels
   reconnaît la langue automatiquement et bascule en conséquence.

.. seealso:: La variante monolingue de cet attribut est décrite dans
   :ref:`component_attribute_tags`.

.. seealso:: Des indications sur le multilinguisme dans MetaModels se
   trouvent sur la page :ref:`component_multi-language`.


Installation
------------

L'attribut s'installe via le **Contao Manager** ou **Composer** :

.. code-block:: bash

   composer require metamodels/attribute_translatedtags


Réglages à la création de l'attribut
-------------------------------------

Outre les réglages généraux de l'attribut et les options de l'attribut
Sélection multiple monolingue, l'attribut traduit propose les options
supplémentaires suivantes :

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Option
     - Description
   * - Table de base de données
     - La table à partir de laquelle les valeurs de sélection sont
       récupérées.
   * - Colonne de table pour libellé/nom
     - La colonne de la table source dont le contenu est affiché comme
       libellé.
   * - ID de la sélection multiple
     - La colonne servant d'identifiant unique (par défaut : ``id``).
   * - Alias de la sélection multiple
     - La colonne utilisée comme identifiant lisible dans les widgets de
       filtre.
   * - Tri de la sélection multiple
     - Colonne selon laquelle la liste de sélection est triée.
   * - Sens du tri
     - Croissant (A → Z) ou décroissant (Z → A).
   * - SQL (condition WHERE)
     - Condition SQL WHERE optionnelle pour restreindre la liste de
       sélection. L'alias ``t`` désigne la table source.
   * - Filtre
     - Choix d'un jeu de filtres MetaModels pour restreindre dynamiquement
       les options.
   * - Paramètres de filtre
     - Valeurs par défaut pour les paramètres du jeu de filtres sélectionné.
   * - Colonne de langue
     - Colonne de la table source contenant le code de langue de l'entrée
       (par ex. ``language``). MetaModels filtre automatiquement la liste
       de sélection selon la langue active.
   * - Table source (traduction)
     - Table source alternative pour les données de référence indépendantes
       de la langue, à partir de laquelle les valeurs de repli sont
       récupérées en l'absence de traduction.
   * - Tri (table source)
     - Colonne de tri dans la table source pour la vue traduite.


Réglages dans les réglages de rendu
--------------------------------------

L'attribut ne possède pas de réglages de rendu qui lui soient propres. Dans
la liste des attributs d'un réglage de rendu, les options habituelles sont
disponibles :

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Option
     - Description
   * - Template
     - Choix d'un template personnalisé pour l'affichage des valeurs
       associées.
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
   * - Choisir le type d'affichage
     - Mode de présentation de la sélection multiple :

       * **Menu de cases à cocher** – liste classique de cases à cocher
       * **Assistant de cases à cocher** – liste de cases à cocher avec
         tri Haut/Bas
       * **Sélecteur en popup** – sélection via un sélecteur arborescent
         (pour les tables source hiérarchiques telles que ``tl_page`` ou
         ``tl_files``)
       * **Liste de tags** – menu déroulant consultable avec chosen.js
   * - Niveau le plus bas (arbre)
     - Pour le sélecteur arborescent : les enregistrements en dessous de ce
       niveau ne sont pas sélectionnables.
   * - Niveau le plus haut (arbre)
     - Pour le sélecteur arborescent : les enregistrements au-dessus de ce
       niveau ne sont pas sélectionnables.

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
     - L'attribut est disponible dans le backend comme critère de filtrage.
   * - Utilisable pour la recherche
     - L'attribut est disponible dans le backend comme champ de recherche.


Règles de filtre
-------------------

.. list-table::
   :header-rows: 1
   :widths: 30 70

   * - Règle de filtre
     - Remarque
   * - Sélection multiple
     - Filtre selon une ou plusieurs valeurs sélectionnées dans la table
       source ; la liste de filtrage est automatiquement restreinte à la
       langue active.
   * - Filtre sur un attribut du modèle avec une relation
     - Filtre les items MetaModel selon la valeur d'un attribut du
       MetaModel associé.


Fonctions spéciales
---------------------

**Stockage**

Les relations sont stockées dans la table intermédiaire
``tl_metamodel_tag_relation`` (colonnes : ``att_id``, ``item_id``,
``value_id``, ``value_sorting``). Aucune colonne propre dans la table du
MetaModel. La traduction ne concerne que les valeurs d'affichage de la liste
de sélection, pas les relations stockées.

**Liste de sélection dépendante de la langue**

MetaModels filtre automatiquement la liste de sélection dans le backend
selon la colonne de langue configurée, en fonction de la langue backend
active.

**Condition SQL WHERE**

Dans la condition WHERE, l'alias ``t`` désigne la table source. Exemple de
filtrage sur les entrées publiées :

.. code-block:: sql

   t.published = '1'


.. |svg_attr_translatedtags_22| image:: /_img/icons_svg/tags.svg
   :width: 22px
.. |img_tags| image:: /_img/icons/tags.png
.. |br| raw:: html

   <br />
