.. _component_filter_expression-rule:

|svg_filt_expression_rule_22| |img_filter_expression| Règle d'expression
============================================================================

La règle de filtre « Règle d'expression » (à partir de MM 2.4) permet de
soumettre l'exécution d'autres règles de filtre à une condition. Un nœud est
créé dans la liste des règles ; il peut accueillir une ou au maximum deux
autres règles de filtre comme nœuds enfants. Si la condition est remplie, la
première sous-règle est exécutée ; si elle ne l'est pas, la seconde sous-règle
(si elle existe) est exécutée (principe du si/sinon).

Cette règle de filtre n'a pas de sortie de widget frontend propre. L'option
« Uniquement les valeurs restantes » influence les options affichées dans
d'autres widgets de filtre.

.. seealso:: Des exemples pratiques sur la règle d'expression figurent dans le
   livre de recettes : :ref:`rst_cookbook_filter_expression-rule`


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
     - Sélection du type de règle de filtre – ici : « Règle d'expression ».
   * - Activé
     - Active ou désactive cette règle de filtre.
   * - Commentaire
     - Champ de texte libre pour décrire l'objectif de cette règle de filtre.
   * - Règle d'expression
     - La condition à évaluer, sous forme d'expression. Elle est évaluée à
       l'exécution ; si l'expression renvoie ``true``, la première sous-règle
       est exécutée, sinon la seconde (si elle existe).
   * - Uniquement les valeurs restantes
     - N'affiche dans les autres widgets de filtre que les valeurs pour
       lesquelles des résultats subsistent après application de cette règle
       d'expression.


Attributs compatibles
----------------------

La règle d'expression n'est pas directement liée à un attribut. Les règles de
filtre utilisées dans les sous-règles peuvent porter sur n'importe quel
attribut.


.. |svg_filt_expression_rule_22| image:: /_img/icons_svg/filter_expression.svg
   :width: 22px
.. |img_filter_expression| image:: /_img/icons/filter_expression.png

.. |br| raw:: html

   <br />
