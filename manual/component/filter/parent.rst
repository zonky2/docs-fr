.. _component_filter_parent:

|svg_filt_parent_22| |img_filter_default| Filtre parent
===========================================================

.. note:: Cette règle de filtre n'est plus développée - son successeur est la
   règle de filtre :ref:`component_filter_by-related`, qui couvre également
   cette fonctionnalité.

La règle de filtre « Filtre parent » (paquet ``filter_parent``, à partir de MM
2.3) permet de filtrer les éléments selon une relation parent-enfant avec un
autre MetaModel. Un élément du MetaModel cible est alors lié, via un attribut,
à un élément du MetaModel « parent ». La règle de filtre filtre ensuite les
éléments liés à un élément parent déterminé.

Il est possible d'afficher en option un widget frontend permettant aux
visiteurs de choisir eux-mêmes l'élément parent.

Avec l'option « Paramètre statique », il est possible, dans l'élément de contenu/module
MetaModels Liste et Filtre, de définir une sélection modifiable comme réglage de
filtre - voir :ref:`rst_cookbook_filter_filter-with-static-parameter`.

Installation
------------

La règle de filtre s'installe via le **Contao Manager** ou **Composer** :

.. code-block:: bash

   composer require metamodels/filter_parent


Réglages lors de la création de la règle de filtre
----------------------------------------------------

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Réglage
     - Description
   * - Type
     - Sélection du type de règle de filtre – ici : « Filtre parent ».
   * - Activé
     - Active ou désactive cette règle de filtre.
   * - Commentaire
     - Champ de texte libre pour décrire l'objectif de cette règle de filtre.
   * - MetaModel parent
     - Le MetaModel qui sert de niveau parent (le MetaModel « parent »).
   * - Attribut parent
     - L'attribut du MetaModel actuel qui établit la relation avec l'élément
       parent (par ex. un attribut à sélection unique pointant vers le
       MetaModel parent).


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
   * - Autoriser une valeur vide
     - Si cette option est active et que le paramètre d'URL est vide, aucun
       filtre n'est actif.
   * - Libellé
     - Intitulé du widget de filtre.
   * - Template
     - Template pour l'affichage du widget.
   * - Par défaut
     - Enregistrement parent présélectionné dans le widget frontend.
   * - Permettre une sélection vide
     - Ajoute une option vide (« Tous »).
   * - Uniquement les valeurs assignées
     - N'affiche dans le widget que les éléments parents effectivement liés à
       au moins un élément.
   * - Uniquement les valeurs restantes
     - N'affiche que les éléments parents pour lesquels des résultats
       subsistent après application des autres filtres.
   * - Ignorer ce filtre pour les valeurs restantes
     - Lors du calcul des valeurs restantes, ce filtre ne renvoie pas ses
       propres options comme restriction.


Attributs compatibles
----------------------

La règle de filtre « Filtre parent » travaille avec un attribut du MetaModel
actuel qui établit la relation avec le MetaModel parent :

* :ref:`Sélection unique [select] <component_attribute_select>`


.. |svg_filt_parent_22| image:: /_img/icons_svg/filter_default.svg
   :width: 22px
.. |img_filter_default| image:: /_img/icons/filter_default.png

.. |br| raw:: html

   <br />
