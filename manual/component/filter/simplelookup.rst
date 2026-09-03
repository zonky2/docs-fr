.. _component_filter_simplelookup:

|svg_filt_simplelookup_22| |img_filter_default| Requête simple
===================================================================

La règle de filtre « Requête simple » filtre les éléments selon la valeur d'un
seul attribut. La valeur du filtre peut soit être transmise dynamiquement via
un paramètre d'URL (GET/slug), soit être configurée de manière fixe via
« Paramètre statique » dans l'élément de contenu ou le module. Cette règle de
filtre convient pour des sélections simples comme « Afficher tous les éléments
de la catégorie X » ou « Filtrer selon un tag déterminé ».

Cette règle de filtre est typiquement utilisée pour :ref:`afficher un
enregistrement en tant que page de détail
<mm_first_contentelements_detailpage>`.

Il est possible d'afficher en option un widget frontend permettant aux
visiteurs de choisir eux-mêmes une valeur - cette règle de filtre fonctionne
alors comme :ref:`component_filter_select`.

Avec l'option « Paramètre statique », il est possible, dans l'élément de contenu/module
MetaModels Liste et Filtre, de définir une sélection modifiable comme réglage de
filtre - voir :ref:`rst_cookbook_filter_filter-with-static-parameter`.


Installation
------------

Cette règle de filtre fait partie de ``metamodels/core`` et est disponible sans
paquet supplémentaire après l'installation de base de MetaModels.


Réglages lors de la création de la règle de filtre
----------------------------------------------------

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Réglage
     - Description
   * - Type
     - Sélection du type de règle de filtre – ici : « Requête simple ».
   * - Activé
     - Active ou désactive cette règle de filtre.
   * - Commentaire
     - Champ de texte libre pour décrire l'objectif de cette règle de filtre.
   * - Attribut
     - L'attribut selon la valeur duquel le filtrage doit être effectué.
   * - Attribut pour le texte du libellé
     - Second attribut facultatif dont la valeur est utilisée comme texte
       d'affichage dans le widget frontend (par ex. un attribut titre à la
       place de l'alias interne) – à partir de MM 2.4.12.

       Ce réglage n'apparaît que si l'attribut filtré ne fournit pas lui-même
       le texte d'affichage – c'est-à-dire pour les attributs sans relation.
       Pour la sélection unique (MetaModel), les tags et les tags traduits, il
       est absent, car le texte d'affichage y est déjà déterminé par la
       colonne de valeurs de l'attribut ; la colonne alias fournit la clé pour
       l'URL.
   * - Rechercher dans toutes les langues
     - Pour les MetaModels multilingues, détermine si toutes les langues ou
       uniquement la langue active doivent être prises en compte pour la
       comparaison.


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
     - Affiche un widget de filtre dans le frontend, permettant aux visiteurs
       de choisir une valeur.
   * - Autoriser une valeur vide
     - Si cette option est active et que le paramètre d'URL est vide, la règle
       de filtre se comporte comme si elle n'était pas définie (aucun filtre
       actif).
   * - Libellé
     - Intitulé du widget de filtre dans le frontend. Si aucun libellé n'est
       indiqué, le nom de l'attribut est utilisé.
   * - Masquer le libellé du widget de filtre
     - Supprime l'affichage du libellé dans le frontend.
   * - Utiliser le libellé comme option vide
     - Le libellé est affiché comme première option vide dans la liste de
       sélection.
   * - Template
     - Template pour l'affichage du widget de filtre. Par défaut :
       ``mm_filteritem_default``.
   * - Par défaut
     - Valeur présélectionnée dans le widget frontend.
   * - Tri
     - Tri des valeurs de sélection dans le widget (croissant ou décroissant).
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
     - Définit un ID ou une classe CSS sur l'élément du widget de filtre.


Attributs compatibles
----------------------

La règle de filtre « Requête simple » prend en charge les attributs stockant
une valeur unique et comparable :

* Texte, alias, entrées combinées, token
* Numérique, décimal
* Case à cocher
* Sélection unique (select)
* Sélection multiple (tags)


Fonctions particulières
-------------------------

**Attributs multilingues**

Pour les attributs traduits (par ex. « Texte traduit »), l'option « Rechercher
dans toutes les langues » permet de configurer si seule la langue active ou
toutes les variantes linguistiques doivent être utilisées pour la comparaison.

**Paramètre statique dans l'élément de contenu**

Si « Paramètre statique » est activé, une liste de sélection apparaît dans
l'élément de contenu/module, permettant de définir une valeur de filtre fixe.
Ce réglage convient pour des pages devant toujours afficher une catégorie
déterminée, sans qu'un paramètre d'URL soit nécessaire - voir
:ref:`rst_cookbook_filter_filter-with-static-parameter`.


.. |svg_filt_simplelookup_22| image:: /_img/icons_svg/filter_simplelookup.svg
   :width: 22px
.. |img_filter_default| image:: /_img/icons/filter_default.png

.. |br| raw:: html

   <br />
