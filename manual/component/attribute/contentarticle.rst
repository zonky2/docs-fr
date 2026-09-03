.. _component_attribute_contentarticle:

|svg_attr_contentarticle_22| |img_article| Contenu d'un article
================================================================

L'attribut « Contenu d'un article » permet d'associer à un jeu de données MetaModels
des éléments de contenu Contao (Content Elements) — à l'instar des éléments de
contenu d'un article Contao. Les contenus sont enregistrés dans la table Contao
``tl_content`` et gérés via un widget de backend dédié.

Cas d'utilisation typiques :

* Descriptions de produits avec une mise en page de contenu complexe (texte, images,
  tableaux)
* Pages de détail avec un contenu rédactionnel élaboré par item
* Plusieurs zones de contenu par jeu de données (par ex. contenu principal + barre
  latérale)

Dans le backend apparaît un widget affichant une liste des éléments de contenu
associés et proposant un lien direct vers la gestion des contenus.

.. seealso:: Pour les MetaModels multilingues, l'attribut
   :ref:`component_attribute_translatedcontentarticle` est disponible.

.. seealso:: Cet attribut est pris en charge par l'intégration
   :ref:`File-Usage <rst_extended_file-usage>`. Elle permet d'afficher dans la
   gestion des fichiers de Contao si et où un fichier est utilisé.

.. seealso:: L'affichage des listes et filtres MetaModels en frontend est décrit sur
   la page :ref:`component_contentelements`.


Installation
------------

L'attribut s'installe via le **Contao Manager** ou **Composer** :

.. code-block:: bash

   composer require metamodels/attribute_contentarticle


Réglages lors de la création de l'attribut
-------------------------------------------

L'attribut ne possède pas de réglages spécifiques lors de sa création. Seuls les
réglages généraux de l'attribut sont utilisés :

* Nom, nom de colonne, description
* Autoriser le remplacement dans les variantes


Réglages dans les réglages de rendu
-------------------------------------

L'attribut ne possède pas de réglages de rendu spécifiques. Dans la liste des
attributs d'un réglage de rendu, les options habituelles sont disponibles :

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Option
     - Description
   * - Template
     - Sélection d'un template propre pour l'affichage des éléments de contenu.
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

.. note:: L'attribut ne peut être rempli avec des éléments de contenu qu'après le
   premier enregistrement du jeu de données. Tant que le jeu de données n'a pas
   encore été enregistré, un message d'information correspondant s'affiche.


Règles de filtre
-------------------

L'attribut « Contenu d'un article » ne prend en charge aucune règle de filtre
propre — les éléments de contenu ne peuvent pas être utilisés comme critère de
filtrage en frontend.


Fonctions particulières
-------------------------

**Stockage**

Les éléments de contenu ne sont **pas** enregistrés dans la table du MetaModel, mais
en tant qu'éléments de contenu Contao classiques dans ``tl_content``, avec les
champs de liaison suivants :

* ``pid`` – ID du jeu de données MetaModels
* ``ptable`` – nom de la table du MetaModel (par ex. ``mm_produits``)
* ``mm_slot`` – nom de colonne de l'attribut (permet plusieurs attributs de type
  article par MM)

Les éléments de contenu sont récupérés via ``ContentModel::findPublishedByPidAndTable()``
et rendus avec ``Controller::getContentElement()``.

**Widget de backend**

Dans le formulaire du backend, le widget affiche une liste des éléments de contenu
existants avec leur type et leur statut de visibilité. Un lien mène directement à
l'interface de gestion des éléments de contenu. Les requêtes AJAX sont actualisées
directement dans le conteneur du widget.

**Duplication de jeux de données**

Lorsqu'un jeu de données MetaModels est dupliqué ou collé (Paste), les éléments de
contenu associés sont automatiquement copiés. MetaModels détecte à cette occasion
tous les attributs ``contentarticle`` et crée des copies des entrées ``tl_content``
avec la nouvelle valeur ``pid``.

**Protection contre la récursion**

L'extension comporte une protection contre la récursion afin d'éviter les boucles
infinies au cas où des éléments de contenu référenceraient eux-mêmes des contenus
MetaModels.


.. |svg_attr_contentarticle_22| image:: /_img/icons_svg/article.svg
   :width: 22px
.. |img_article| image:: /_img/icons/article.png
.. |br| raw:: html

   <br />
