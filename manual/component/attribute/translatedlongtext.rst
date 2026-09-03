.. _component_attribute_translatedlongtext:

|svg_attr_translatedlongtext_22| |img_longtext| Texte long traduit
=====================================================================

L'attribut « Texte long traduit » est la variante multilingue de l'attribut
:ref:`Texte long <component_attribute_longtext>`. Il stocke pour chaque
langue sa propre valeur de texte long (jusqu'à 65 535 caractères). Les
valeurs ne sont pas stockées dans la table du MetaModel, mais dans la table
de traduction ``tl_metamodel_translatedlongtext``.

Domaines d'application typiques :

* Descriptions de produits multilingues
* Textes d'articles ou d'actualités dépendants de la langue
* Contenus HTML traduits (avec éditeur de texte enrichi activé)

.. seealso:: La variante monolingue de cet attribut est décrite dans
   :ref:`component_attribute_longtext`.

.. seealso:: Des indications sur le multilinguisme dans MetaModels se
   trouvent sur la page :ref:`component_multi-language`.

.. seealso:: Cet attribut est pris en charge par l'intégration
   :ref:`File-Usage <rst_extended_file-usage>`. Elle permet d'afficher dans
   la gestion des fichiers de Contao si et où un fichier est utilisé.


Installation
------------

L'attribut s'installe via le **Contao Manager** ou **Composer** :

.. code-block:: bash

   composer require metamodels/attribute_translatedlongtext


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
     - Choix d'un template personnalisé pour l'affichage du texte long.
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
     - Classes CSS pour la présentation du champ dans le formulaire backend
       (par ex. ``long clr`` pour la pleine largeur avec saut de ligne).
   * - Template pour le backend
     - Choix d'un template de widget personnalisé pour le formulaire backend.
   * - Template pour le frontend
     - Choix d'un template de widget personnalisé pour l'édition en frontend
       (uniquement si « Frontend Editing » est installé).
   * - Éditeur de texte enrichi (RTE)
     - Activation et choix d'un éditeur de texte enrichi (par ex.
       ``tinyMCE`` ou ``ace``). Si aucun RTE n'est sélectionné, un simple
       champ de zone de texte apparaît.
   * - Mode de coloration syntaxique
     - Choix de la coloration syntaxique pour l'éditeur de code source
       ``ace``.
   * - Lignes
     - Nombre de lignes visibles du champ de zone de texte (hauteur) —
       généralement écrasé par le CSS de Contao. Si le template
       ``be_tinyMCE_mm`` ou ``be_ace_mm`` est sélectionné, les valeurs de
       hauteur sont transmises au widget en tant qu'option — en pixels pour
       ``tinyMCE`` et en lignes pour ``ace``.
   * - Colonnes
     - Nombre de caractères visibles par ligne du champ de zone de texte
       (largeur) — généralement écrasé par le CSS de Contao.

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
     - Les balises HTML ne sont ni filtrées ni encodées lors de
       l'enregistrement.
   * - Décoder les entités
     - Les entités HTML sont décodées lors de l'enregistrement.

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
   * - Recherche textuelle
     - Saisie libre pour la recherche en texte intégral dans le champ de
       texte long de la langue active.
   * - Recherche par Levenshtein
     - Recherche par similarité avec tolérance aux fautes de frappe ;
       nécessite le paquet ``attribute_levenshtein``.
   * - Loupe
     - Recherche par index plein texte ; nécessite le paquet ``filter_loupe``
       (à partir de MM 2.4).


Fonctions spéciales
---------------------

**Stockage**

Les valeurs de texte sont stockées de façon spécifique à la langue dans
``tl_metamodel_translatedlongtext`` (champs : ``att_id``, ``item_id``,
``langcode``, ``value`` en ``text``). La table du MetaModel ne reçoit pas de
colonne propre.

**Éditeur de texte enrichi (RTE)**

Un RTE tel que TinyMCE peut être activé via le masque de saisie. Le RTE
formate les contenus HTML et encode les entités lors de l'enregistrement.
L'option « Autoriser la saisie HTML » doit alors également être activée.

**Langue de repli**

S'il manque une valeur pour une langue, MetaModels se rabat sur la langue de
repli.


.. |svg_attr_translatedlongtext_22| image:: /_img/icons_svg/longtext.svg
   :width: 22px
.. |img_longtext| image:: /_img/icons/longtext.png
.. |br| raw:: html

   <br />
