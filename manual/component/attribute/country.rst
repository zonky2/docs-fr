.. _component_attribute_country:

|svg_attr_country_22| |img_country| Pays
========================================

L'attribut « Pays » met à disposition une liste de sélection de tous les pays du
monde. Les noms de pays sont affichés dans la langue active du backend et triés par
ordre alphabétique. Le code ISO 3166-1 alpha-2 à deux lettres est enregistré (par ex.
``FR`` pour la France, ``BE`` pour la Belgique). Cas d'utilisation typiques :

* Champ pays dans les formulaires d'adresse
* Pays d'origine ou de destination pour des produits ou des options d'expédition
* Indication de nationalité dans des données personnelles

Les pays disponibles peuvent être restreints lorsque seule une sélection de pays
déterminés est pertinente.


Installation
------------

L'attribut s'installe via le **Contao Manager** ou **Composer** :

.. code-block:: bash

   composer require metamodels/attribute_country


Réglages lors de la création de l'attribut
-------------------------------------------

Outre les réglages généraux de l'attribut (nom, nom de colonne, description,
autoriser le remplacement dans les variantes), l'attribut Pays propose l'option
spécifique suivante :

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Option
     - Description
   * - Filtrer les pays disponibles
     - Restriction de la sélection de pays à des pays déterminés. Sélection
       multiple possible via une liste déroulante consultable. Si aucune
       sélection n'est faite, tous les pays sont disponibles.


Réglages dans les réglages de rendu
-------------------------------------

L'attribut Pays ne possède pas de réglages de rendu spécifiques. Dans la liste des
attributs d'un réglage de rendu, les options habituelles sont disponibles :

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Option
     - Description
   * - Template
     - Sélection d'un template propre pour l'affichage. Si aucun template n'est
       indiqué, le nom de pays localisé dans la langue active est affiché.
   * - Classe CSS
     - Classe CSS optionnelle ajoutée à l'élément de sortie.


Réglages dans le masque de saisie
-----------------------------------

Lorsque l'attribut Pays est ajouté à un masque de saisie, les options suivantes
sont disponibles :

**Présentation**

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Option
     - Description
   * - Classe backend
     - Classes CSS pour l'affichage du champ dans le formulaire du backend (par
       ex. ``w50`` pour une demi-largeur).
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
     - Rend le champ obligatoire.
   * - Afficher une option vide
     - Affiche une option de sélection vide en début de liste des pays, afin
       qu'aucun pays ne soit présélectionné.

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

Aucune règle de filtre propre n'est actuellement disponible pour l'attribut Pays.
Pour filtrer selon un pays, la règle de filtre « Requête simple » peut être
utilisée avec le code pays (par ex. ``FR``) comme paramètre.


Fonctions particulières
-------------------------

**Sortie localisée**

Le code ISO enregistré (par ex. ``FR``) est automatiquement converti à l'affichage
en nom de pays localisé dans la langue active. L'attribut résout le code en interne
via le service Contao ``contao.intl.countries`` et met le résultat en cache par
langue.

**Tri par nom de pays**

Le tri des jeux de données selon l'attribut Pays s'effectue selon le nom de pays
localisé (et non selon le code ISO enregistré), de sorte que le tri alphabétique
soit correct selon la langue.

**Stockage en base de données**

La valeur du pays est enregistrée sous la forme ``varchar(2) NULL`` (code ISO à
deux lettres). Une valeur vide est enregistrée comme ``NULL`` (compatible avec le
mode strict de MySQL).


.. |svg_attr_country_22| image:: /_img/icons_svg/country.svg
   :width: 22px
.. |img_country| image:: /_img/icons/country.png

.. |br| raw:: html

   <br />
