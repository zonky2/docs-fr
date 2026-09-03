.. _component_attribute_alias:

|svg_attr_alias_22| |img_alias| Alias
=====================================

L'attribut « Alias » génère un identifiant court, unique et compatible avec les URL, à
partir d'un ou plusieurs attributs existants. Les cas d'utilisation typiques sont :

* Paramètres d'URL pour le filtrage en frontend (par ex. ``/produits/mon-produit``)
* Identifiants lisibles et stables pour les liens profonds ou les :ref:`URL SEO <rst_cookbook_tips_seo_url>`
* Abréviations uniques générées automatiquement à partir de noms ou de titres

L'alias est composé automatiquement à l'enregistrement d'un jeu de données à partir des
attributs source configurés. Un jeu de caractères et une langue de conversion peuvent être
définis afin que les caractères spéciaux (par ex. les trémas) soient correctement convertis.

.. note:: Un alias n'est pas automatiquement unique. Pour garantir son unicité, l'option
   « Valeurs uniques » doit être activée dans les réglages généraux de l'attribut.

.. warning:: Si l'option « Forcer la régénération de l'alias » est activée, les valeurs
   d'alias existantes sont régénérées à chaque modification des attributs source.
   Les URL déjà publiées peuvent ainsi devenir invalides.


Installation
------------

L'attribut s'installe via le **Contao Manager** ou **Composer** :

.. code-block:: bash

   composer require metamodels/attribute_alias


Réglages lors de la création de l'attribut
-------------------------------------------

Outre les réglages généraux de l'attribut (nom, nom de colonne, description, valeurs
uniques, autoriser le remplacement dans les variantes), l'attribut Alias propose les
options spécifiques suivantes :

**Champs de l'alias**

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Option
     - Description
   * - Champs de l'alias
     - Sélection d'un ou plusieurs attributs à partir desquels l'alias est composé.
       Outre les attributs propres au MetaModel, les méta-champs système comme ID,
       PID, tri ou horodatage sont également disponibles. Si plusieurs champs sont
       sélectionnés, leurs valeurs sont reliées par un trait d'union.

**Génération et jeu de caractères**

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Option
     - Description
   * - Forcer la régénération de l'alias
     - Si la case est cochée, l'alias est automatiquement régénéré à chaque
       modification de l'un des attributs source. Le champ alias est alors affiché
       en lecture seule dans le backend. Sans cette option, un alias déjà généré
       reste inchangé.
   * - Caractères valides pour l'alias
     - Détermine le jeu de caractères utilisé pour la génération automatique.
       Valeurs possibles : *chiffres et minuscules Unicode* (par défaut),
       *chiffres et lettres Unicode*, *chiffres et minuscules ASCII*,
       *chiffres et lettres ASCII*.
   * - Langue de conversion
     - Code de langue ISO 639-1 (par ex. ``fr`` ou ``fr-FR``) selon lequel les
       caractères spéciaux sont convertis lors de la génération. Si le champ est
       laissé vide, la conversion par défaut s'applique.
   * - Préfixe de l'alias
     - Texte optionnel placé devant l'alias généré (seuls les caractères
       alphanumériques sont autorisés).
   * - Suffixe de l'alias
     - Texte optionnel placé après l'alias généré.
   * - Pas de préfixe entier
     - Si la case est cochée (par défaut), aucun préfixe ``id-`` n'est ajouté
       lorsque l'alias résultant est purement numérique.


Réglages dans les réglages de rendu
-------------------------------------

L'attribut Alias ne possède pas de réglages de rendu spécifiques. Dans la liste des
attributs d'un réglage de rendu, les options habituelles sont disponibles :

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Option
     - Description
   * - Template
     - Sélection d'un template propre pour l'affichage de la valeur de l'alias. Si
       aucun template n'est indiqué, l'affichage se fait sous forme de texte simple.
   * - Classe CSS
     - Classe CSS optionnelle ajoutée à l'élément de sortie.


Réglages dans le masque de saisie
-----------------------------------

Lorsque l'attribut Alias est ajouté à un masque de saisie (réglage DCA), les options
suivantes sont disponibles :

**Présentation**

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Option
     - Description
   * - Classe backend
     - Classes CSS pour l'affichage du champ dans le formulaire du backend (par ex.
       ``w50`` pour une demi-largeur, ``clr`` pour un saut de ligne, ``long`` pour
       la pleine largeur).
   * - Template pour le backend
     - Sélection d'un template de widget propre pour le formulaire du backend.
   * - Template pour le frontend
     - Sélection d'un template de widget propre pour l'édition en frontend
       (disponible uniquement si l'extension « Frontend Editing » est installée).

**Fonctions**

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Option
     - Description
   * - Champ obligatoire
     - Rend le champ obligatoire. Si l'option « Valeurs uniques » est activée dans
       les réglages de l'attribut, cette option est automatiquement définie.
   * - Toujours enregistrer
     - Le champ est enregistré même si sa valeur n'a pas changé. Si « Forcer la
       régénération de l'alias » est activé, cette option est également définie
       automatiquement.

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

L'attribut Alias peut être utilisé avec les règles de filtre suivantes :

.. list-table::
   :header-rows: 1
   :widths: 30 70

   * - Règle de filtre
     - Remarque
   * - Requête simple
     - Filtre les jeux de données selon une valeur d'alias exacte ou partielle ; le
       nom de la colonne alias est utilisé par défaut comme paramètre d'URL (par ex.
       ``?alias=mon-produit`` ou, avec ``auto_item``, ``/mon-produit``) - voir par
       ex. la :ref:`page de détail <mm_first_contentelements_detailpage>`.
   * - Recherche textuelle
     - Saisie de texte libre en frontend pour rechercher dans le champ alias.
   * - Recherche assistée par Levenshtein
     - Recherche par similarité incluant la tolérance aux fautes de frappe ;
       nécessite le paquet ``attribute_levenshtein``.
   * - Loupe
     - Recherche par index plein texte basée sur une base de données SQLite ;
       nécessite le paquet ``filter_loupe`` (à partir de MM 2.4).


Fonctions particulières
-------------------------

**Insert-tags dans les attributs source**

Si un attribut source contient des insert-tags (par ex. ``{{env::page}}``), ceux-ci
sont résolus avant la génération du slug. Cela permet d'intégrer des éléments d'alias
dynamiques.

**Comportement lors de la copie d'un jeu de données**

Si « Forcer la régénération de l'alias » est activé, une valeur d'alias existante n'est
pas reprise lors de la duplication d'un jeu de données dans le backend. Un nouvel alias
est au contraire automatiquement généré après l'enregistrement (comportement
``doNotCopy``).

**Unicité avec attribution automatique de suffixe**

Si « Valeurs uniques » est activé, le générateur de slug vérifie après la génération si
l'alias existe déjà. En cas de doublon, Contao ajoute automatiquement un suffixe
numérique (par ex. ``mon-produit-2``, ``mon-produit-3``, etc.) jusqu'à obtenir une
valeur unique.

**Stockage en base de données**

L'alias est stocké sous forme de ``varchar(255) NULL`` dans la table du MetaModel. Une
valeur vide est enregistrée comme ``NULL`` (compatible avec le mode strict de MySQL).

**Caractères spéciaux du beautifier**

Les séquences ``[-]``, ``[zwsp]``, ``&shy;`` et ``&ZeroWidthSpace;`` (séparateurs
conditionnels utilisés par Contao pour la mise en forme du texte) sont automatiquement
supprimées avant la génération du slug, afin qu'elles n'apparaissent pas dans l'alias.


.. |svg_attr_alias_22| image:: /_img/icons_svg/alias.svg
   :width: 22px
.. |img_alias| image:: /_img/icons/alias.png

.. |br| raw:: html

   <br />
