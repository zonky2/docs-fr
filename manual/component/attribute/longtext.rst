.. _component_attribute_longtext:

|svg_attr_longtext_22| |img_longtext| Texte long
================================================

L'attribut « Texte long » est destiné aux saisies de texte plus longues. Il est
affiché comme widget de type zone de texte (textarea) dans le backend et peut
optionnellement être équipé d'un éditeur de texte enrichi (RTE tel que TinyMCE).
Cas d'utilisation typiques :

* Textes de description, descriptions de produits, textes d'articles
* Champs de texte libre pour des saisies multilignes
* Contenus HTML (lorsque le RTE est activé)

La longueur maximale est de 65 535 caractères (type MySQL ``TEXT``).

.. seealso:: Pour les MetaModels multilingues, l'attribut
   :ref:`component_attribute_translatedlongtext` est disponible.

.. seealso:: Cet attribut est pris en charge par l'intégration
   :ref:`File-Usage <rst_extended_file-usage>`. Elle permet d'afficher dans la
   gestion des fichiers de Contao si et où un fichier est utilisé.


Installation
------------

L'attribut s'installe via le **Contao Manager** ou **Composer** :

.. code-block:: bash

   composer require metamodels/attribute_longtext


Réglages lors de la création de l'attribut
-------------------------------------------

L'attribut Texte long ne possède pas de réglages spécifiques lors de sa création.
Seuls les réglages généraux de l'attribut sont utilisés :

* Nom, nom de colonne, description
* Autoriser le remplacement dans les variantes


Réglages dans les réglages de rendu
-------------------------------------

L'attribut Texte long ne possède pas de réglages de rendu spécifiques. Dans la
liste des attributs d'un réglage de rendu, les options habituelles sont
disponibles :

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Option
     - Description
   * - Template
     - Sélection d'un template propre pour l'affichage du texte long. Si aucun
       template n'est indiqué, l'affichage se fait sous forme de texte simple
       ou de HTML.
   * - Classe CSS
     - Classe CSS optionnelle ajoutée à l'élément de sortie.


Réglages dans le masque de saisie
-----------------------------------

Lorsque l'attribut Texte long est ajouté à un masque de saisie, les options
suivantes sont disponibles :

**Présentation**

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Option
     - Description
   * - Classe backend
     - Classes CSS pour l'affichage du champ dans le formulaire du backend (par
       ex. ``long clr`` pour la pleine largeur avec saut de ligne).
   * - Template pour le backend
     - Sélection d'un template de widget propre pour le formulaire du backend.
   * - Template pour le frontend
     - Sélection d'un template de widget propre pour l'édition en frontend
       (disponible uniquement si l'extension « Frontend Editing » est installée).
   * - Éditeur de texte enrichi (RTE)
     - Activation et sélection d'un éditeur de texte enrichi (par ex.
       ``tinyMCE`` ou ``ace``). Si aucun RTE n'est sélectionné, un simple champ
       de type zone de texte apparaît.
   * - Mode de coloration syntaxique
     - Sélection de la coloration syntaxique pour l'éditeur de code source
       ``ace``.
   * - Lignes
     - Nombre de lignes visibles du champ de type zone de texte (hauteur) -
       généralement écrasé par le CSS de Contao. Lorsque le template
       ``be_tinyMCE_mm`` ou ``be_ace_mm`` est sélectionné, les indications de
       hauteur sont transmises au widget comme option - en pixels pour
       ``tinyMCE`` et en lignes pour ``ace``.
   * - Colonnes
     - Nombre de caractères visibles par ligne du champ de type zone de texte
       (largeur) - généralement écrasé par le CSS de Contao.

**Fonctions**

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Option
     - Description
   * - Champ obligatoire
     - Rend le champ obligatoire.
   * - Autoriser la saisie HTML
     - Autorise la saisie de balises HTML dans le champ de texte (sans RTE).
   * - Conserver les balises
     - Les balises HTML ne sont ni filtrées ni encodées à l'enregistrement.
   * - Décoder les entités
     - Les entités HTML sont décodées à l'enregistrement.

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

L'attribut Texte long peut être utilisé avec les règles de filtre suivantes :

.. list-table::
   :header-rows: 1
   :widths: 30 70

   * - Règle de filtre
     - Remarque
   * - Recherche textuelle
     - Saisie de texte libre pour la recherche plein texte dans le champ Texte
       long.
   * - Recherche assistée par Levenshtein
     - Recherche par similarité avec tolérance aux fautes de frappe ; nécessite
       le paquet ``attribute_levenshtein``.
   * - Loupe
     - Recherche par index plein texte ; nécessite le paquet ``filter_loupe``
       (à partir de MM 2.4).


Fonctions particulières
-------------------------

**Éditeur de texte enrichi (RTE)**

Un RTE tel que TinyMCE peut être activé via le masque de saisie. Il convient de
noter que le RTE formate les contenus HTML saisis et encode les entités à
l'enregistrement. L'option « Autoriser la saisie HTML » devrait alors également
être activée dans les fonctions.

Le widget de saisie TinyMCE peut être équipé d'un
:ref:`sélecteur jumpTo propre vers la page de détail
<rst_cookbook_specials_picker-for-tinymce>`.

**Stockage en base de données**

Le texte est enregistré sous la forme ``text NULL`` (jusqu'à 65 535 caractères).
Une valeur vide est enregistrée comme ``NULL`` (compatible avec le mode strict
de MySQL). Pour des contenus plus longs, une migration vers ``mediumtext`` ou
``longtext`` directement au niveau de la base de données peut être nécessaire —
cela est décrit dans le livre de recettes sous
:ref:`rst_cookbook_inputmask_manipulate-select-values`.


.. |svg_attr_longtext_22| image:: /_img/icons_svg/longtext.svg
   :width: 22px
.. |img_longtext| image:: /_img/icons/longtext.png
.. |br| raw:: html

   <br />
