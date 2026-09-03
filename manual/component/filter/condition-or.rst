.. _component_filter_condition-or:

|svg_filt_condition_or_22| |img_filter_or| Condition OU (OR)
================================================================

La règle de filtre « Condition OU » est un conteneur pouvant accueillir
plusieurs sous-règles de filtre. Les règles de filtre qu'il contient sont
combinées par un opérateur OU : un élément doit satisfaire au moins l'une des
sous-conditions pour apparaître dans l'ensemble de résultats.

Cette règle de filtre permet de représenter des alternatives de filtrage, par
ex. « Afficher tous les éléments de la catégorie A ou de la catégorie B ». En
l'imbriquant avec des conditions ET, il est possible de réaliser des
combinaisons complexes comme ``(A ET B) OU (C ET D)``.

L'option « Arrêter après le premier résultat » permet une optimisation des
performances : dès qu'une sous-règle fournit des éléments, les sous-règles
suivantes ne sont plus exécutées.

Cette règle de filtre n'a pas de sortie de widget frontend.


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
     - Sélection du type de règle de filtre – ici : « Condition OU (OR) ».
   * - Activé
     - Active ou désactive cette règle de filtre.
   * - Commentaire
     - Champ de texte libre pour décrire l'objectif de cette règle de filtre.
   * - Arrêter après le premier résultat
     - Si cette option est active, les sous-règles suivantes ne sont plus
       exécutées dès qu'une sous-règle a trouvé au moins un élément. Cela peut
       réduire le nombre de requêtes en base de données et améliorer les
       performances.


Attributs compatibles
----------------------

La condition OU n'est pas un filtre lié à un attribut, mais un conteneur
structurel. Les sous-règles de filtre qu'elle contient peuvent utiliser
n'importe quel attribut.


Fonctions particulières
-------------------------

**Imbrication avec des conditions ET**

En combinant des conditions OU et ET, il est possible de construire des
expressions logiques reproduisant des clauses SQL WHERE natives avec ET/OU.

Exemple d'une combinaison OU à trois branches avec deux conditions ET chacune :

.. code-block:: text

   Condition OU
   ├── Condition ET
   │   ├── Règle de filtre A (par ex. Catégorie = « Sport »)
   │   └── Règle de filtre B (par ex. Statut = publié)
   └── Condition ET
       ├── Règle de filtre C (par ex. Catégorie = « Culture »)
       └── Règle de filtre D (par ex. Statut = publié)


.. |svg_filt_condition_or_22| image:: /_img/icons_svg/filter_or.svg
   :width: 22px
.. |img_filter_or| image:: /_img/icons/filter_or.png

.. |br| raw:: html

   <br />
