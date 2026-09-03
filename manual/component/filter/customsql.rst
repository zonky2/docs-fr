.. _component_filter_customsql:

|svg_filt_customsql_22| |img_filter_customsql| SQL personnalisé
===================================================================

La règle de filtre « SQL personnalisé » permet d'utiliser une requête SQL écrite
soi-même pour filtrer les éléments. La requête doit retourner une liste d'ID
d'éléments. Cette règle de filtre s'adresse aux utilisateurs avancés ayant
besoin de conditions de filtrage complexes qui ne peuvent pas être représentées
avec les types de règles de filtre existants – par ex. des comparaisons sur
plusieurs colonnes, des sous-requêtes ou des calculs liés à des dates.

Cette règle de filtre n'a pas de sortie de widget frontend.

Les noms de colonnes doivent toujours être placés entre backticks `` ` `` comme
par ex. \`nom\`, ou préfixés par le nom de la table ou son alias (voir
`Identifiants MySQL <https://dev.mysql.com/doc/refman/8.0/en/identifiers.html>`_).
Cela permet également l'utilisation de
`mots réservés <https://dev.mysql.com/doc/refman/8.0/en/keywords.html>`_ en (My)SQL.

Pour les requêtes plus complexes, il est conseillé de les tester au préalable
avec des outils SQL adaptés comme phpMyAdmin, PHPStorm ou similaires, ou, en cas
d'imbrications, de les construire étape par étape en travaillant d'abord avec
des valeurs fixes. Les données correspondantes doivent bien entendu être
présentes en tant qu'éléments dans la base de données. En dernière étape, on
ajoute si nécessaire les paramètres dynamiques à l'aide des insert-tags
disponibles. Les insert-tags SQL de MM ne sont résolus que pendant le traitement
de la requête et ne sont donc pas disponibles de manière générale dans le
frontend.

Même avec la règle de filtre « SQL personnalisé », seuls des ID sont transmis à
la règle de filtre suivante ou au jeu de filtres. Il n'est pas possible
d'ajouter ou de calculer des « valeurs d'attribut », même si cela serait
techniquement possible en SQL, par ex. via des JOIN ou des instructions
mathématiques.

.. seealso:: Des exemples pratiques et des indications d'utilisation figurent
   dans le livre de recettes : :ref:`rst_cookbook_filter_custom-sql` |br|
   Astuces SQL générales : :ref:`rst_cookbook_sql-tips`


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
     - Sélection du type de règle de filtre – ici : « SQL personnalisé ».
   * - Activé
     - Active ou désactive cette règle de filtre.
   * - Commentaire
     - Champ de texte libre pour décrire l'objectif de cette règle de filtre.
   * - Requête SQL personnalisée
     - Saisie de la requête SQL. La requête doit retourner au moins une colonne
       ``id``. Les noms de colonnes doivent être préfixés par l'alias de la
       table (par ex. ``t.id``). Les insert-tags et les sources de paramètres
       sont pris en charge. |br|
       Modèle par défaut : ``SELECT id FROM {{table}} WHERE 1 = 1``
   * - Utiliser uniquement dans l'environnement
     - Restriction facultative de l'environnement Contao (par ex. backend ou
       frontend) dans lequel la règle de filtre doit être exécutée.


Attributs compatibles
----------------------

La règle de filtre « SQL personnalisé » n'est pas liée à un attribut. La
logique de filtrage est entièrement définie dans la requête SQL. Le nom de la
table du MetaModel est inséré via le paramètre ``{{table}}``.


Fonctions particulières
-------------------------

Paramètre ``{{table}}``
~~~~~~~~~~~~~~~~~~~~~~~~~

Le paramètre ``{{table}}`` est remplacé à l'exécution par le nom de table réel
du MetaModel, par ex. ``mm_monmodele``.

.. code-block:: sql

   SELECT t.id FROM {{table}} AS t WHERE t.page_id = 1

équivaut à :

.. code-block:: sql

   SELECT t.id FROM mm_mymetamodel AS t WHERE t.page_id = 1


Insert-tags
~~~~~~~~~~~

Des insert-tags Contao peuvent être utilisés dans la requête SQL. Il faut noter
que tous les tags ne sont pas disponibles dans toutes les sorties. Un tag comme
``{{page::id}}`` ne fonctionne par ex. que lors des accès aux pages en
frontend, pas pour les flux RSS.

Exemples :

* ``{{user::id}}`` – ID du membre frontend connecté
* ``{{page::id}}`` – ID de la page actuelle
* ``{{env::request}}`` – URI de la requête actuelle


Insert-tags sécurisés
~~~~~~~~~~~~~~~~~~~~~~

Les insert-tags sécurisés fonctionnent comme les insert-tags normaux, mais les
valeurs sont automatiquement échappées dans la requête. Une utilisation
irréfléchie peut donc conduire à des résultats inattendus.

Notation :

.. code-block:: text

   {{secure::page::id}}


Sources de paramètres ``{{param::...}}``
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Les sources de paramètres permettent d'accéder à différentes valeurs externes
directement dans la requête SQL. Le format est le suivant :

.. code-block:: text

   {{param::[source]?[chaîne de requête]}}

**Sources disponibles :**

.. list-table::
   :header-rows: 1
   :widths: 20 80

   * - Source
     - Description
   * - ``get``
     - Chaîne de requête HTTP GET
   * - ``post``
     - Champs HTTP POST
   * - ``session``
     - N'importe quel champ de la session Contao
   * - ``filter``
     - Paramètre de filtre exécuté (pour partager des valeurs de filtre entre
       règles de filtre)

**Mots-clés facultatifs dans la chaîne de requête :**

.. list-table::
   :header-rows: 1
   :widths: 20 80

   * - Mot-clé
     - Description
   * - ``name``
     - Nom du paramètre (champ obligatoire)
   * - ``default``
     - Valeur par défaut, si aucune autre valeur n'est disponible
   * - ``aggregate``
     - ``list`` ou ``set`` – pour les valeurs de type tableau
   * - ``key``
     - À placer à ``1`` pour lire la clé d'un tableau (nécessite ``aggregate``)
   * - ``recursive``
     - À placer à ``1`` pour lire les tableaux de manière récursive (nécessite
       ``aggregate``)


Exemples
--------

**Exemple 1 – Requête simple**

.. code-block:: sql

   SELECT t.id FROM mm_mymetamodel AS t WHERE t.page_id = 1

Sélectionne tous les ID de la table ``mm_mymetamodel`` pour lesquels
``page_id = 1``.

**Exemple 2 – Insertion du nom de la table**

.. code-block:: sql

   SELECT t.id FROM {{table}} AS t WHERE t.page_id = 1

Comme l'exemple 1, mais le nom de la table du MetaModel actuel est inséré
automatiquement.

**Exemple 3 – Paramètre GET et valeur par défaut**

.. code-block:: sql

   SELECT t.id
   FROM {{table}} AS t
   WHERE t.catname = {{param::get?name=category&default=defaultcat}}

Pour l'URL ``https://example.org/list/category/demo.html``, on obtient : |br|
``SELECT t.id FROM mm_demo AS t WHERE t.catname = 'demo'``

Pour l'URL ``https://example.org/list.html`` (sans paramètre) : |br|
``SELECT t.id FROM mm_demo AS t WHERE t.catname = 'defaultcat'``


.. |svg_filt_customsql_22| image:: /_img/icons_svg/filter_customsql.svg
   :width: 22px
.. |img_filter_customsql| image:: /_img/icons/filter_customsql.png

.. |br| raw:: html

   <br />
