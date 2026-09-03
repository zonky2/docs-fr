.. _component_attribute_translatedcontentarticle:

|svg_attr_translatedcontentarticle_22| |img_article| Contenu d'article traduit
=================================================================================

L'attribut « Contenu d'article traduit » est la variante multilingue de
l'attribut :ref:`Contenu d'article <component_attribute_contentarticle>`. Il
permet d'associer des éléments de contenu Contao propres à chaque langue pour
un enregistrement MetaModels. Les contenus sont stockés dans la table Contao
``tl_content`` avec un champ de langue supplémentaire.

Domaines d'application typiques :

* Descriptions de produits multilingues avec mise en page de contenu complexe
* Contenus de pages de détail dépendants de la langue avec une structure
  différente selon la langue
* Contenu rédactionnel traduit par item

.. seealso:: La variante monolingue de cet attribut est décrite dans
   :ref:`component_attribute_contentarticle`.

.. seealso:: Des indications sur le multilinguisme dans MetaModels se
   trouvent sur la page :ref:`component_multi-language`.

.. seealso:: Cet attribut est pris en charge par l'intégration
   :ref:`File-Usage <rst_extended_file-usage>`. Elle permet d'afficher dans
   la gestion des fichiers de Contao si et où un fichier est utilisé.


Installation
------------

L'attribut s'installe via le **Contao Manager** ou **Composer** :

.. code-block:: bash

   composer require metamodels/attribute_translatedcontentarticle


Réglages à la création de l'attribut
-------------------------------------

L'attribut ne possède pas de réglages spécifiques propres à sa création.
Seuls les réglages généraux de l'attribut sont utilisés :

* Nom, nom de colonne, description
* Autoriser la surcharge de variante


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
     - Choix d'un template personnalisé pour l'affichage des éléments de
       contenu.
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

.. note:: L'attribut ne peut être rempli d'éléments de contenu qu'après le
   premier enregistrement de l'enregistrement.


Règles de filtre
-------------------

L'attribut ne prend en charge aucune règle de filtre propre.


Fonctions spéciales
---------------------

**Stockage**

Les éléments de contenu sont stockés dans ``tl_content`` — de façon
identique à la variante monolingue, mais avec un champ supplémentaire :

* ``pid`` – ID de l'enregistrement MetaModels
* ``ptable`` – nom de la table du MetaModel
* ``mm_slot`` – nom de colonne de l'attribut
* ``mm_lang`` – code de langue de l'élément de contenu (par ex. ``de``, ``en``)

La récupération des éléments de contenu s'effectue de façon spécifique à la
langue. S'il manque un élément de contenu pour une langue, MetaModels se
rabat automatiquement sur la langue de repli.

**Widget backend**

Le widget backend affiche les éléments de contenu de la langue backend
actuellement active. Le choix de la langue est transmis automatiquement au
widget via l'écouteur d'événement ``setWidgetLanguage``.

**Duplication d'enregistrements**

Lorsqu'un enregistrement MetaModels est dupliqué, les éléments de contenu
associés de toutes les langues sont copiés également. Lors d'une copie
d'une langue vers une autre langue, une copie vers la même langue n'est pas
possible (message d'erreur).

**Langue de repli**

S'il manque un ensemble d'éléments de contenu pour une langue, les contenus
de la langue de repli sont automatiquement affichés.


.. |svg_attr_translatedcontentarticle_22| image:: /_img/icons_svg/article.svg
   :width: 22px
.. |img_article| image:: /_img/icons/article.png
.. |br| raw:: html

   <br />
