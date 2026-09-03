.. _component_filter_by-related:

|svg_filt_by_related_22| |img_filter_default| Filter-by-related
===============================================================

La règle de filtre « Filter-by-related » (paquet ``filter_by_related``, à partir de MM 2.4)
permet de filtrer les éléments en fonction des propriétés d'un MetaModel lié (en
relation). La relation entre le MetaModel principal et le MetaModel lié peut être
établie soit via une table enfant (relation pid), soit via un attribut à
sélection unique (relation select).

Par exemple, dans une structure « Fabricant → Produits », il est possible de filtrer
selon les propriétés du fabricant (par ex. « Afficher tous les produits des
fabricants originaires d'Allemagne »).

Il est possible d'afficher en option un widget frontend permettant aux visiteurs
de choisir eux-mêmes une valeur.

Avec l'option « Paramètre statique », il est possible, dans l'élément de contenu/module
MetaModels Liste et Filtre, de définir une sélection modifiable comme réglage de
filtre - voir :ref:`rst_cookbook_filter_filter-with-static-parameter`.

.. seealso:: Documentation détaillée sur Filter-by-related :
   :ref:`rst_extended_filter_by_related`


Installation
------------

La règle de filtre s'installe via le **Contao Manager** ou **Composer** :

.. code-block:: bash

   composer require metamodels/filter_by_related


Réglages lors de la création de la règle de filtre
----------------------------------------------------

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Réglage
     - Description
   * - Type
     - Sélection du type de règle de filtre – ici : « Filter-by-related ».
   * - Activé
     - Active ou désactive cette règle de filtre.
   * - Commentaire
     - Champ de texte libre pour décrire l'objectif de cette règle de filtre.
   * - MetaModel lié
     - Le MetaModel via lequel la relation est établie (le « MetaModel parent »).
   * - Colonne de relation
     - Détermine comment la relation avec le MetaModel principal est établie :

       * **PID** – via la relation de table enfant (champ pid)
       * **Méta-attribut** – via un méta-attribut
       * **Attribut** – via un attribut à sélection unique dans le MetaModel principal
   * - Attribut lié
     - L'attribut du MetaModel lié dont la valeur sert de critère de filtrage.
   * - Attribut de libellé
     - L'attribut du MetaModel lié dont la valeur est utilisée comme texte
       d'affichage dans le widget frontend.


Réglages du widget frontend
----------------------------

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Réglage
     - Description
   * - Paramètre d'URL
     - La clé du paramètre d'URL utilisée pour transmettre la valeur du filtre.
       Si elle n'est pas précisée, le nom de colonne de l'attribut est utilisé.
       Avec ``auto_item``, seule la valeur – sans clé – est intégrée dans l'URL.
   * - Type d'URL pour le paramètre
     - Détermine si le paramètre est transmis sous forme de slug (URL explicite)
       ou de paramètre GET (à partir de MM 2.4) - :ref:`voir SEO
       <rst_cookbook_tips_seo_filter-url>`
   * - Paramètre statique
     - Si cette option est active, la valeur du filtre peut être prédéfinie de
       façon modifiable à partir d'une liste de sélection dans l'élément de
       contenu/module.
   * - Fournir un widget frontend
     - Affiche un widget de filtre dans le frontend.
   * - Type de widget
     - Mode d'affichage du widget frontend :

       * **Select** – Liste de sélection (par défaut)
       * **Text** – Champ de saisie de texte
       * **Radio** – Boutons radio
       * **Checkbox** – Cases à cocher
   * - Type de recherche
     - Uniquement pour le type de widget **Text** : détermine comment le terme de
       recherche est comparé à la valeur de l'attribut lié :

       * **Contient le terme de recherche** – La valeur de l'attribut doit
         contenir le terme de recherche (par défaut).
       * **Recherche exacte** – Le terme de recherche doit correspondre
         exactement à la valeur de l'attribut.
       * **Commence par le terme de recherche** – La valeur de l'attribut doit
         commencer par le terme de recherche.
       * **Se termine par le terme de recherche** – La valeur de l'attribut doit
         se terminer par le terme de recherche.

       Un astérisque (``*``) saisi par le visiteur agit comme un joker et
       prévaut sur le type de recherche configuré.
   * - Autoriser une valeur vide
     - Si cette option est active et que le paramètre d'URL est vide, aucun
       filtre n'est actif.
   * - Libellé
     - Intitulé du widget de filtre.
   * - Masquer le libellé du widget de filtre
     - Supprime l'affichage du libellé.
   * - Template
     - Template pour l'affichage du widget.
   * - Par défaut
     - Valeur présélectionnée dans le widget frontend.
   * - Permettre une sélection vide
     - Ajoute une option vide (« Tous »).
   * - Uniquement les valeurs assignées
     - N'affiche que les valeurs effectivement présentes dans une relation.
   * - Uniquement les valeurs restantes
     - N'affiche que les valeurs pour lesquelles des résultats subsistent après
       application des autres filtres.
   * - Ignorer ce filtre pour les valeurs restantes
     - Lors du calcul des valeurs restantes, ce filtre ne renvoie pas ses
       propres options comme restriction.


Attributs compatibles
----------------------

La règle de filtre « Filter-by-related » ne travaille pas avec un attribut du
MetaModel principal, mais avec des attributs du MetaModel lié. N'importe quel
type d'attribut peut y être filtré.

La relation avec le MetaModel principal peut être établie via les types
d'attributs suivants :

* :ref:`Sélection unique [select] <component_attribute_select>`
* Relation de table enfant (pid/ptable)


.. |svg_filt_by_related_22| image:: /_img/icons_svg/filter_by_related.svg
   :width: 22px
.. |img_filter_default| image:: /_img/icons/filter_default.png

.. |br| raw:: html

   <br />
