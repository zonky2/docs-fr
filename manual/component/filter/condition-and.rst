.. _component_filter_condition-and:

|svg_filt_condition_and_22| |img_filter_and| Condition ET (AND)
=================================================================

La règle de filtre « Condition ET » est un conteneur pouvant accueillir
plusieurs sous-règles de filtre. Toutes les règles de filtre qu'il contient sont
combinées par un opérateur ET : un élément doit satisfaire toutes les
sous-conditions pour apparaître dans l'ensemble de résultats.

Comme les règles de filtre situées au même niveau au sein d'un jeu de filtres
sont de toute façon automatiquement combinées par ET, la condition ET est
principalement nécessaire pour structurer les règles à l'intérieur d'une
condition OU. Elle permet ainsi de construire des combinaisons de filtres
complexes comme ``(A ET B) OU (C ET D)``.

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
     - Sélection du type de règle de filtre – ici : « Condition ET (AND) ».
   * - Activé
     - Active ou désactive cette règle de filtre.
   * - Commentaire
     - Champ de texte libre pour décrire l'objectif de cette règle de filtre.


Attributs compatibles
----------------------

La condition ET n'est pas un filtre lié à un attribut, mais un conteneur
structurel. Les sous-règles de filtre qu'elle contient peuvent utiliser
n'importe quel attribut.


Fonctions particulières
-------------------------

**Structure de filtre hiérarchique**

Les icônes en forme de classeur dans la liste des règles de filtre permettent
d'insérer une règle de filtre dans une condition ET (ou une condition OU). On
obtient ainsi une structure de filtre imbriquée capable de représenter des
expressions logiques presque aussi complexes que souhaité.


.. |svg_filt_condition_and_22| image:: /_img/icons_svg/filter_and.svg
   :width: 22px
.. |img_filter_and| image:: /_img/icons/filter_and.png

.. |br| raw:: html

   <br />
