.. _rst_cookbook_filter_search-text-at-two-fields:

Recherche textuelle sur deux champs
======================================

Si l'on souhaite mettre en place une recherche textuelle sur deux champs (ou plus), il est possible d'utiliser des
filtres spécifiques tels que `metamodelsfilter_textcombine
<https://github.com/cogizz/metamodelsfilter_textcombine>`_,
ou de résoudre cela avec les « moyens du bord ».

Pour la solution avec les « moyens du bord », les étapes suivantes doivent être mises en place comme règles de
filtrage :

* règle de filtre « OU » pour combiner les champs texte, respectivement les règles de filtre
* dans les règles de filtre des champs texte, le même paramètre d'URL doit être configuré

Comme exemple, un jeu de filtres pour une recherche simultanée dans les attributs « Nom » et « Prénom » - une
remarque concernant le libellé : ici, pour la sortie en frontend, c'est le libellé de la dernière règle de filtre
qui est affiché.

Jeu de filtres :

|img_multi-textfilter_01|

Réglage du deuxième filtre texte :

|img_multi-textfilter_02|

Filtrage en frontend :

|img_multi-textfilter_03|

|img_multi-textfilter_04|



.. |img_multi-textfilter_01| image:: /_img/screenshots/cookbook/filter/multi-textfilter_01.jpg
.. |img_multi-textfilter_02| image:: /_img/screenshots/cookbook/filter/multi-textfilter_02.jpg
.. |img_multi-textfilter_03| image:: /_img/screenshots/cookbook/filter/multi-textfilter_03.jpg
.. |img_multi-textfilter_04| image:: /_img/screenshots/cookbook/filter/multi-textfilter_04.jpg

