.. _component_filter_tags:

|svg_filt_tags_22| |img_filter_tags| Sélection multiple
============================================================

La règle de filtre « Sélection multiple » (paquet ``filter_tags``) affiche un
widget frontend permettant aux visiteurs de choisir simultanément plusieurs
valeurs dans une liste. Les éléments sont filtrés selon les valeurs choisies
d'un attribut. Cette règle de filtre est typiquement combinée avec le type
d'attribut :ref:`Sélection multiple (tags) <component_attribute_tags>` afin de
rendre des relations (m:n) filtrables dans le frontend.

Le template ``mm_filteritem_linklist.html5`` (liste de liens) est disponible en
alternative. L'option « Liaison OU » permet de configurer si les éléments
doivent satisfaire toutes les valeurs choisies ou seulement l'une d'entre
elles.


Installation
------------

La règle de filtre s'installe via le **Contao Manager** ou **Composer** :

.. code-block:: bash

   composer require metamodels/filter_tags


Réglages lors de la création de la règle de filtre
----------------------------------------------------

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Réglage
     - Description
   * - Type
     - Sélection du type de règle de filtre – ici : « Sélection multiple ».
   * - Activé
     - Active ou désactive cette règle de filtre.
   * - Commentaire
     - Champ de texte libre pour décrire l'objectif de cette règle de filtre.
   * - Attribut
     - L'attribut de type tags selon les valeurs duquel le filtrage doit être
       effectué.
   * - Attribut pour le texte du libellé
     - Second attribut facultatif dont la valeur est utilisée comme texte
       d'affichage des options dans le widget – à partir de MM 2.4.12.

       Ce réglage n'apparaît que si l'attribut filtré ne fournit pas lui-même
       le texte d'affichage – c'est-à-dire pour les attributs sans relation.
       Pour la sélection unique (MetaModel), les tags et les tags traduits, il
       est absent, car le texte d'affichage y est déjà déterminé par la
       colonne de valeurs de l'attribut ; la colonne alias fournit la clé pour
       l'URL.


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
   * - Libellé
     - Intitulé du widget de filtre.
   * - Masquer le libellé du widget de filtre
     - Supprime l'affichage du libellé.
   * - Template
     - Template pour l'affichage du widget. Par défaut :
       ``mm_filteritem_default`` ; alternativement : ``mm_filteritem_linklist``.
   * - Tri
     - Tri des options de sélection dans le widget (croissant ou décroissant).
   * - Permettre une sélection vide
     - Ajoute une option vide (« Tous »).
   * - Afficher le bouton « Tout sélectionner »
     - Ajoute un bouton permettant de sélectionner toutes les options en une
       fois.
   * - Liaison OU
     - Si cette option est active, un élément est affiché dès lors qu'il
       contient au moins l'une des valeurs choisies (OU). Si l'option est
       inactive, toutes les valeurs choisies doivent être présentes (ET).
   * - Uniquement les valeurs assignées
     - N'affiche dans le widget que les valeurs effectivement attribuées à au
       moins un élément.
   * - Uniquement les valeurs restantes
     - N'affiche que les valeurs pour lesquelles des résultats subsistent
       après application des autres filtres actifs.
   * - Ignorer ce filtre pour les valeurs restantes
     - Lors du calcul des valeurs restantes, ce filtre ne renvoie pas ses
       propres options comme restriction.
   * - ID/Classe CSS
     - Définit un ID ou une classe CSS sur l'élément du widget.


Attributs compatibles
----------------------

La règle de filtre « Sélection multiple » convient particulièrement pour :

* :ref:`Sélection multiple [tags] <component_attribute_tags>`
* :ref:`Sélection multiple traduite [tags] <component_attribute_translatedtags>`


Fonctions particulières
-------------------------

**Listes de liens**

Le template ``mm_filteritem_linklist`` affiche les options de filtre sous forme
de liens. Chaque clic sur un lien transmet la valeur en tant que paramètre
d'URL, sans nécessiter de formulaire. Cela convient particulièrement pour des
navigations de filtrage favorables au SEO.

**Liaison ET vs. OU**

Lorsque l'option OU est désactivée (par défaut), tous les tags choisis doivent
être présents dans un élément (filtrage ET). Lorsque l'option OU est activée,
un seul tag correspondant suffit (filtrage OU). Cela influence de manière
significative l'ensemble de résultats en cas de sélection multiple.


.. |svg_filt_tags_22| image:: /_img/icons_svg/filter_tags.svg
   :width: 22px
.. |img_filter_tags| image:: /_img/icons/filter_tags.png

.. |br| raw:: html

   <br />
