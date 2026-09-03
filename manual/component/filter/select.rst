.. _component_filter_select:

|svg_filt_select_22| |img_filter_select| Sélection unique
==============================================================

La règle de filtre « Sélection unique » (paquet ``filter_select``) affiche un
widget frontend permettant aux visiteurs de choisir une seule valeur dans une
liste de sélection. Les éléments sont filtrés selon la valeur choisie d'un
attribut. Cette règle de filtre est typiquement combinée avec le type
d'attribut :ref:`Sélection unique (select) <component_attribute_select>` afin
de rendre une relation (1:n) filtrable dans le frontend.

Les templates ``mm_filteritem_radiobutton.html5`` (boutons radio) et
``mm_filteritem_linklist.html5`` (liste de liens) sont également disponibles en
alternative.


Installation
------------

La règle de filtre s'installe via le **Contao Manager** ou **Composer** :

.. code-block:: bash

   composer require metamodels/filter_select


Réglages lors de la création de la règle de filtre
----------------------------------------------------

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Réglage
     - Description
   * - Type
     - Sélection du type de règle de filtre – ici : « Sélection unique ».
   * - Activé
     - Active ou désactive cette règle de filtre.
   * - Commentaire
     - Champ de texte libre pour décrire l'objectif de cette règle de filtre.
   * - Attribut
     - L'attribut selon la valeur duquel le filtrage doit être effectué.
   * - Attribut pour le texte du libellé
     - Second attribut facultatif dont la valeur est utilisée comme texte
       d'affichage des options dans le widget (par ex. un attribut nom ou
       titre) – à partir de MM 2.4.12.

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
   * - Utiliser le libellé comme option vide
     - Le libellé est utilisé comme première option vide (au lieu d'une ligne
       vide).
   * - Template
     - Template pour l'affichage du widget. Par défaut :
       ``mm_filteritem_default`` ; alternativement : ``mm_filteritem_radiobutton``
       ou ``mm_filteritem_linklist``.
   * - Tri
     - Tri des options de sélection dans le widget (croissant ou décroissant).
   * - Par défaut
     - Valeur présélectionnée dans le widget frontend.
   * - Permettre une sélection vide
     - Ajoute une option vide (« Tous ») dans la liste de sélection.
   * - Uniquement les valeurs assignées
     - N'affiche dans le widget que les valeurs effectivement attribuées à au
       moins un élément du MetaModel.
   * - Uniquement les valeurs restantes
     - N'affiche que les valeurs pour lesquelles des résultats subsistent
       après application des autres filtres actifs (options de filtre
       dynamiques).
   * - Ignorer ce filtre pour les valeurs restantes
     - Lors du calcul des valeurs restantes, ce filtre ne renvoie pas ses
       propres options comme restriction.
   * - ID/Classe CSS
     - Définit un ID ou une classe CSS sur l'élément du widget.


Attributs compatibles
----------------------

La règle de filtre « Sélection unique » convient particulièrement pour :

* :ref:`Sélection unique [select] <component_attribute_select>`
* :ref:`Sélection unique traduite [select] <component_attribute_translatedselect>`
* :ref:`Texte <component_attribute_text>`
* :ref:`Alias <component_attribute_alias>`
* :ref:`Entrées combinées <component_attribute_combinedvalues>`
* :ref:`Token <component_attribute_token>`


Fonctions particulières
-------------------------

**Boutons radio et listes de liens**

Via la sélection de template, le widget peut être affiché sous forme de liste
de boutons radio (``mm_filteritem_radiobutton``) ou de liste de liens
(``mm_filteritem_linklist``). Les listes de liens conviennent particulièrement
pour une navigation optimisée pour le SEO, sans soumission de formulaire.


.. |svg_filt_select_22| image:: /_img/icons_svg/filter_select.svg
   :width: 22px
.. |img_filter_select| image:: /_img/icons/filter_select.png

.. |br| raw:: html

   <br />
