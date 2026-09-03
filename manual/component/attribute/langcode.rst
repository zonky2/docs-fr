.. _component_attribute_langcode:

|svg_attr_langcode_22| |img_langcode| Code de langue
=====================================================

L'attribut « Code de langue » met à disposition une liste de sélection de codes de
langue ISO (locales). Les noms de langues sont affichés dans la langue active du
backend. Le code de langue est enregistré (par ex. ``de``, ``en``, ``fr`` ou aussi
``de_DE``, ``en_US``). Cas d'utilisation typiques :

* Langue d'un document, d'un article ou d'un produit
* Langue cible pour des commandes de traduction
* Préférence linguistique dans les données d'utilisateurs ou de membres

Les codes de langue disponibles peuvent être restreints lorsque seule une sélection
déterminée de langues est pertinente. La saisie s'effectue via des cases à cocher.


Installation
------------

L'attribut s'installe via le **Contao Manager** ou **Composer** :

.. code-block:: bash

   composer require metamodels/attribute_langcode


Réglages lors de la création de l'attribut
-------------------------------------------

Outre les réglages généraux de l'attribut (nom, nom de colonne, description,
autoriser le remplacement dans les variantes), l'attribut Code de langue propose
l'option spécifique suivante :

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Option
     - Description
   * - Codes de langue
     - Restriction de la sélection de langues à des codes de langue déterminés.
       Les langues disponibles sont affichées sous forme de liste de cases à
       cocher. Si aucune sélection n'est faite, toutes les langues disponibles
       dans Contao peuvent être choisies.


Réglages dans les réglages de rendu
-------------------------------------

L'attribut Code de langue ne possède pas de réglages de rendu spécifiques. Dans la
liste des attributs d'un réglage de rendu, les options habituelles sont
disponibles :

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Option
     - Description
   * - Template
     - Sélection d'un template propre pour l'affichage. Si aucun template n'est
       indiqué, le nom de langue localisé dans la langue active est affiché.
   * - Classe CSS
     - Classe CSS optionnelle ajoutée à l'élément de sortie.


Réglages dans le masque de saisie
-----------------------------------

Lorsque l'attribut Code de langue est ajouté à un masque de saisie, les options
suivantes sont disponibles :

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
     - Affiche une option de sélection vide, afin qu'aucun code de langue ne
       soit présélectionné.

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

Aucune règle de filtre propre n'est actuellement disponible pour l'attribut Code
de langue. Pour filtrer selon un code de langue, la règle de filtre « Requête
simple » peut être utilisée avec le code de langue (par ex. ``fr``) comme
paramètre.


Fonctions particulières
-------------------------

**Sortie localisée**

Le code de langue enregistré (par ex. ``fr``) est automatiquement converti à
l'affichage en nom de langue localisé dans la langue active. L'attribut utilise
pour cela le service Contao ``contao.intl.locales`` et met le résultat en cache
par langue.

**Langues de repli**

Si un nom de langue n'est pas disponible pour la langue active, l'attribut recourt
automatiquement à des langues de repli afin d'afficher malgré tout un nom lisible.

**Stockage en base de données**

Le code de langue est enregistré sous la forme ``varchar(5) NULL`` (jusqu'à 5
caractères, par ex. ``de_DE``). Une valeur vide est enregistrée comme ``NULL``
(compatible avec le mode strict de MySQL).


.. |svg_attr_langcode_22| image:: /_img/icons_svg/langcode.svg
   :width: 22px
.. |img_langcode| image:: /_img/icons/langcode.png
.. |br| raw:: html

   <br />
