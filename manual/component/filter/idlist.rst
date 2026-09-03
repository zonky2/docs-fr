.. _component_filter_idlist:

|svg_filt_idlist_22| |img_filter_default| Ensemble d'éléments prédéfini
============================================================================

La règle de filtre « Ensemble d'éléments prédéfini » permet d'indiquer une
liste fixe d'ID d'éléments comme base de filtrage. Le jeu de filtres ne renvoie
que les éléments dont l'ID figure dans la liste indiquée. Cette règle de filtre
convient pour des sélections statiques où les enregistrements à afficher sont
connus à l'avance, par ex. pour des « entrées recommandées » ou des « temps
forts ».

Cette règle de filtre n'a pas de sortie de widget frontend et se configure
exclusivement dans le backend.


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
     - Sélection du type de règle de filtre – ici : « Ensemble d'éléments
       prédéfini ».
   * - Activé
     - Active ou désactive cette règle de filtre.
   * - Commentaire
     - Champ de texte libre pour décrire l'objectif de cette règle de filtre.
   * - Éléments
     - Liste d'ID d'éléments séparés par des virgules, selon lesquels le
       filtrage doit être effectué. Seuls les éléments possédant ces ID sont
       pris en compte dans la sortie.


Attributs compatibles
----------------------

La règle de filtre « Ensemble d'éléments prédéfini » ne travaille pas par
attribut, mais directement avec les ID d'éléments de la table MetaModels.
Aucune sélection d'attribut n'est donc nécessaire.


Fonctions particulières
-------------------------

Cette règle de filtre peut être combinée avec d'autres règles de filtre. Comme
elle renvoie toujours un ensemble fixe d'ID, elle convient particulièrement
comme condition ET en combinaison avec des règles de filtre dynamiques, afin de
restreindre à l'avance l'ensemble des éléments consultables.


.. |svg_filt_idlist_22| image:: /_img/icons_svg/filter_idlist.svg
   :width: 22px
.. |img_filter_default| image:: /_img/icons/filter_default.png

.. |br| raw:: html

   <br />
