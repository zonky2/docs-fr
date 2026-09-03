.. _rst_cookbook_filter_expression-rule:

Règle de filtre « Expression »
===================================

.. note:: Disponible à partir de la version 2.4 - actuellement encore une fonctionnalité expérimentale !

Avec la règle de filtre « Expression », l'exécution d'autres règles de filtre peut être soumise à des
conditions. Un nœud est créé dans la liste des règles, pouvant accueillir un ou au maximum deux autres règles de
filtrage comme nœuds enfants.

La condition est définie dans la règle de filtre sous forme d'une
`expression Symfony <https://symfony.com/doc/current/reference/formats/expression_language.html>`_ - si la
condition est remplie, la première règle de filtre des nœuds enfants est exécutée, et si la condition n'est pas
remplie, c'est la deuxième règle de filtre des nœuds enfants qui s'exécute.

La deuxième règle de filtre des nœuds enfants est optionnelle - si elle n'existe pas, aucune ID d'item n'est
transmise à la liste, c.-à-d. qu'aucune donnée n'est affichée dans la liste.

La structure pourrait ressembler à ceci :

|img_expression_01|

S'il existe un ensemble de règles de filtre devant s'appliquer dans le premier nœud enfant, celles-ci peuvent être
regroupées dans une condition ET.

|img_expression_02|

Dans la syntaxe d'expression, les paramètres suivants sont actuellement disponibles pour les vérifications :

* ``filterUrl``: tableau avec les paramètres de filtre de l'URL
* ``request``: la pile de requêtes (request stack) actuelle

.. note:: L'affichage des widgets de filtre en frontend n'est pas influencé par cette règle de filtre - cette
   fonctionnalité pourrait éventuellement être ajoutée ultérieurement.


Exemples de construction :
******************************

**Tâche :** N'afficher la liste que lorsqu'une valeur de filtre est définie. |br|
**Expression :** ``filterUrl != []`` |br|
**Construction :**

* Règle de filtre Expression

  * Règle de filtre pour le filtrage, par ex. sélection multiple ou sélection simple

Ici, il n'est pas nécessaire de créer une deuxième règle de filtre comme nœud enfant - cela reste toutefois
possible en option.

**Tâche :** N'afficher la liste filtrée que lorsqu'une valeur de filtre est définie - si aucun filtre n'est défini,
afficher un jeu de données fixe. |br|
**Expression :** ``filterUrl != []`` |br|
**Construction :**

* Règle de filtre Expression

  * Règle de filtre pour le filtrage, par ex. sélection multiple ou sélection simple
  * Règle de filtre « Ensemble prédéfini d'items » avec l'ID souhaitée du jeu de données, respectivement les ID
    des jeux de données


Exemples d'expressions :
****************************

* aucun paramètre de filtre n'est défini : ``filterUrl != []``
* le paramètre de filtre avec le paramètre d'URL ``kategorien`` doit contenir une valeur :
  ``(filterUrl['kategorien'] ?? '') != ''``
* le paramètre GET ``foo`` ne doit pas être ``1`` : ``(!request.query.has('foo') || request.query.get('foo') !== '1')``

Les opérateurs possibles sont listés dans le
`manuel de Symfony <https://symfony.com/doc/current/reference/formats/expression_language.html#supported-operators>`_.


.. |img_expression_01| image:: /_img/screenshots/cookbook/filter/expression_01.png
.. |img_expression_02| image:: /_img/screenshots/cookbook/filter/expression_02.png

.. |br| raw:: html

   <br />
