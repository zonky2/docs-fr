.. _rst_cookbook_filter_custom-sql:

SQL personnalisé
================

Une description détaillée de la règle de filtre « SQL personnalisé » se trouve sur la :ref:`page détaillée des
règles de filtre <component_filter_customsql>` - une information rapide est disponible via l'aide |img_help| dans
les réglages.

Petit rappel : même avec la règle de filtre « SQL personnalisé », seules les ID sont transmises à la règle de
filtrage suivante ou au jeu de filtres. Il n'est pas possible d'ajouter ou de calculer des « valeurs d'attribut »,
même si cela serait techniquement possible en SQL, par ex. via des JOINs ou des instructions mathématiques.

Voici quelques requêtes SQL comme « ingrédients » pour son propre « menu SQL » :


Requête « LIKE » avec valeur par défaut
****************************************

« Recherche les items dont l'attribut 'name' correspond, si le paramètre GET 'name'
est défini, sinon retourne tous les items (pas de filtrage). »

.. code-block:: sql
   :linenos:

   SELECT `id`
   FROM {{table}}
   WHERE `name` LIKE (CONCAT('%',{{param::get?name=name&default=%%}},'%'))


Filtrage par date
******************

« Recherche les items dont l'attribut 'date_start' est supérieur ou égal à la
date du jour - donc dans le futur »

.. code-block:: sql
   :linenos:

   SELECT `id`
   FROM {{table}}
   WHERE FROM_UNIXTIME(`date_start`) >= CURDATE()

ou

.. code-block:: sql
   :linenos:

   SELECT `id`
   FROM {{table}}
   WHERE DATE(FROM_UNIXTIME(`date_start`)) >= DATE(now())


Filtrage par date (début ou « en cours »)
********************************************

« Recherche les items dont l'attribut 'date_start' est supérieur ou égal à la
date du jour - donc dans le futur - ou les items pour lesquels la date actuelle
se situe entre 'date_start' et 'date_end' (en cours) »

.. code-block:: sql
   :linenos:

   SELECT `id`
   FROM {{table}}
   WHERE
   ( DATE(FROM_UNIXTIME(`date_start`)) >= DATE(NOW()) )
   OR
   ( DATE(FROM_UNIXTIME(`date_start`)) <= DATE(NOW())
     AND
     DATE(FROM_UNIXTIME(`date_end`)) >= DATE(NOW())
   )


Filtrage par date (début/fin)
*******************************

« Recherche les items pour lesquels l'attribut 'start' est supérieur à
l'horodatage Unix actuel et pour lesquels l'attribut 'stop' n'est pas
encore atteint. Les valeurs d'attribut vides sont considérées comme non
pertinentes (alors seul 'start' ou 'stop' est pertinent). » [de « Cyberlussi »]

.. code-block:: sql
   :linenos:

   SELECT `id`
   FROM {{table}}
   WHERE (`date_start` IS NULL OR `date_start` = '' OR `date_start` < UNIX_TIMESTAMP())
   AND (`date_stop` IS NULL OR `date_stop` = '' OR `date_stop` > UNIX_TIMESTAMP())

Alternative

.. code-block:: sql
   :linenos:

   SELECT `id` FROM {{table}}
   WHERE (`date_start` IS NULL OR DATE(FROM_UNIXTIME(`date_start`)) <= DATE(now()))
   AND (`date_stop` IS NULL OR DATE(FROM_UNIXTIME(`date_stop`)) >= DATE(now()))


Filtrage par date (début) et date de publication avec vérification par GET
*******************************************************************************

Par exemple pour des événements qui doivent être masqués une fois la date de début
atteinte, mais qui ne doivent être affichés qu'à partir d'une certaine date - si celle-ci
est définie.

Pour la vérification, on peut ajouter un paramètre GET à l'URL en FE - le format de date
est « YYYY-MM-DD », par ex. « domain.tld/meine-liste.html?now=2023-07-10 ».

.. code-block:: sql
   :linenos:

   SELECT id FROM {{table}}
   WHERE DATE(FROM_UNIXTIME(`date_start`)) >= DATE(now())
   AND (`date_published` IS NULL
   	OR DATE(FROM_UNIXTIME(`date_published`)) <= DATE(now())
   	OR DATE(FROM_UNIXTIME(`date_published`)) <= {{param::get?name=now}}
   )

Filtrage par date (début) des 12 derniers mois
*************************************************
Filtre d'archive pour les items passés des 12 derniers mois :

.. code-block:: sql
   :linenos:

   SELECT id FROM {{table}}
   WHERE DATE(FROM_UNIXTIME(`date_start`)) < DATE(now())
   AND DATE(FROM_UNIXTIME(`date_start`)) >= DATE(now() - INTERVAL 12 month)

Filtrage des éléments enfants d'un élément parent
****************************************************

« Recherche tous les éléments enfants pour un élément parent donné via le paramètre alias
- par ex. pour afficher sur une page de détail tous les 'éléments enfants' associés. »

.. code-block:: sql
   :linenos:

   SELECT `id`
   FROM mm_child
   WHERE `pid` = (
     SELECT `id`
     FROM mm_parent
     WHERE
     `parent_alias` = {{param::get?name=auto_item}}
     LIMIT 1
   )


Filtrage de l'élément parent d'un élément enfant
****************************************************

« Recherche l'élément parent pour un élément enfant donné via le paramètre alias
- par ex. pour afficher sur une page de détail l''élément parent' associé. »

.. code-block:: sql
   :linenos:

   SELECT `id`
   FROM mm_parent
   WHERE `id` = (
     SELECT `pid`
     FROM mm_child
     WHERE
     `child_alias` = {{param::get?name=auto_item}}
     LIMIT 1
   )

ou plus court

.. code-block:: sql
   :linenos:

   SELECT `pid` as id
   FROM mm_child
   WHERE `child_alias` = {{param::get?name=auto_item}}


.. _rst_cookbook_filter_custom-sql_sortierung-der-ausgabe-nach-mehr-als-einem-attribut-fest:
Tri de la sortie selon plusieurs attributs (fixe)
****************************************************

« Trier les 'équipes' par points décroissants + matchs croissants +
priorité décroissante. »
voir aussi le `forum <https://community.contao.org/de/showthread.php?62625-Zweite-Sortierung>`_

Il faut noter que cette règle SQL doit être placée dans le filtre en tant que *première règle*. C'est la première
règle - dans la mesure où elle retourne bien une liste d'items - qui définit l'« ensemble de base » et l'ordre des
items ; les règles suivantes ne font ensuite que réduire cet ensemble. Le sens de tri est toujours ASC sous MySQL -
pour obtenir un autre sens, il faut le préciser pour chaque colonne de tri indiquée.

.. code-block:: sql
   :linenos:

   SELECT `id`
   FROM mm_mannschaft
   ORDER BY `punkte` DESC, `spiele` ASC, `prio` DESC


Tri de la sortie selon un numéro et les valeurs NULL, ou de façon aléatoire
********************************************************************************

Il faut noter que cette règle SQL doit être placée dans le filtre en tant que *première règle*.
Afficher les items selon un numéro d'ordre propre, mais tous les items sans numéro (NULL) à la fin :

.. code-block:: sql
   :linenos:

   SELECT `id`
   FROM mm_sv_categories
   ORDER BY ISNULL(`sort_number`), `sort_number` ASC

On peut aussi faire apparaître certains items en premier (attribut « Curseur de priorité » = 1) et
le reste de façon aléatoire :

.. code-block:: sql
   :linenos:

   SELECT `id`
   FROM mm_sv_trainings
   ORDER BY `prio_slider` DESC, rand()


Tri de la sortie d'un MM référencé et d'un nom
*************************************************

Si l'on a par ex. un MM Produits, dans lequel un partenaire est référencé via une sélection simple
[select], et que l'on souhaite afficher les produits triés d'abord selon le tri manuel (sorting)
des partenaires puis selon le nom du produit lui-même, on peut y parvenir avec le code suivant :

.. code-block:: sql
   :linenos:

   SELECT pro.id FROM mm_products AS pro
   LEFT JOIN mm_partners AS part ON pro.partner = part.id
   WHERE pro.published = 1
   ORDER BY part.sorting, pro.product_code

Dans la liste de sortie, on pourrait ainsi afficher par ex. un sous-titre à chaque nouveau partenaire.
Pour cela, il suffit de stocker l'ID du partenaire actuel dans une variable temporaire et de vérifier
à chaque tour de boucle s'il y a égalité - si ce n'est pas le cas, afficher le « nom du partenaire ».


Valeur par défaut dynamique
*******************************

Pour le SQL personnalisé, des valeurs par défaut sont possibles via 'default=<valeur>',
utilisées lorsque le paramètre de filtre n'est pas défini. Dans le tag param, il n'est
actuellement pas encore possible d'imbriquer des insert-tags ni d'utiliser des
fonctions MySQL, de sorte que pour des valeurs par défaut dynamiques, il faut recourir
à un contournement via un « SQL-IF ».
voir aussi `Github #880 <https://github.com/MetaModels/core/issues/880>`_

.. code-block:: sql
   :linenos:

   SELECT `id` FROM mm_monate
   WHERE FROM_UNIXTIME(`von_datum`) <= IF(
      {{param::get?name=von_datum}},
      {{param::get?name=von_datum}},
      CURDATE()
   )
   ORDER BY `von_datum` DESC

Valeur par défaut ''
**********************

Pour le SQL personnalisé, des valeurs par défaut sont possibles via 'default=<valeur>',
utilisées lorsque le paramètre de filtre n'est pas défini. Dans le tag param, la saisie
de `''` ou `""` est actuellement transtypée, de sorte que le filtrage ne s'effectue pas
correctement ; ceci s'applique par ex. pour des valeurs de case à cocher.

.. code-block:: sql
   :linenos:

   SELECT `id` FROM mm_mitarbeiter
   WHERE `driver_licence` = IF(
      {{param::get?name=driver_licence}},
      {{param::get?name=driver_licence}},
      ''
   )

Transmission de plusieurs valeurs pour `IN()`
*************************************************

Plusieurs valeurs peuvent être transmises à la requête sous forme de liste séparée par des virgules ou de tableau -
selon le type de transmission, le paramètre `aggregate` prend la valeur `list` ou `set`.

.. code-block:: sql
   :linenos:

   -- en tant que liste
   -- domain.tld/de/liste?id=13,15,19
   SELECT id FROM {{table}}
   WHERE id IN ({{param::get?name=id&aggregate=list}})

   -- en tant que tableau
   -- domain.tld/de/liste?id[]=13&id[]=15&id[]=19
   SELECT id FROM {{table}}
   WHERE id IN ({{param::get?name=id&aggregate=set}})

Filtrer les tags d'un item
*******************************

Les employés ont une sélection multiple [tags] vers le MetaModel « Softskills ».
Pour la vue de détail d'un employé, ceux-ci doivent être déterminés - la vue de
détail est filtrée via « auto_item » par l'alias.

Les softskills sont affichés comme une liste propre sur la page de détail, mais
doivent être filtrés en conséquence. Pour déterminer les données, il faut passer
par la table de relation « tl_metamodel_tag_relation ». Il est important de
déterminer l'ID d'attribut pour « rel.att_id », c.-à-d. que dans les attributs
d'« Employés », la sélection multiple a par ex. l'ID 5 (à déterminer via le bouton i).

.. code-block:: sql
   :linenos:

   SELECT DISTINCT(rel.value_id) as id FROM mm_mitarbeiter as ma
   LEFT JOIN tl_metamodel_tag_relation rel ON (ma.id = rel.item_id AND rel.att_id=5)
   WHERE
   ma.alias = {{param::get?name=auto_item}}

Filtrer les items selon une propriété de sélection simple
****************************************************************

Les employés ont une sélection simple vers le MetaModel « Département ».
Pour une vue en liste des employés, seuls ceux qui travaillent dans un
département dont le « score » est supérieur à 99 doivent être affichés.


.. code-block:: sql
   :linenos:

   SELECT `id` FROM mm_mitarbeiter
   WHERE `abteilung` IN (
      SELECT `id` FROM mm_abteilung
      WHERE `score` > 99
   )

ou

.. code-block:: sql
   :linenos:

   SELECT ma.id FROM mm_mitarbeiter ma
   LEFT JOIN mm_abteilung rel ON (ma.abteilung = rel.id)
   WHERE rel.score > 99


Filtrer les employés pour une page associée via une sélection multiple [tags]
***********************************************************************************

Les employés ont un attribut de sélection multiple vers la table `tl_page`,
pour désigner sur des pages individuelles un employé comme responsable. Sur les
pages correspondantes, un élément de liste MM peut être inséré, qui affiche les
employés associés. Pour le filtrage, la requête suivante peut être utilisée :

.. code-block:: sql
   :linenos:

   SELECT ma.id FROM mm_mitarbeiter ma
   LEFT JOIN tl_metamodel_tag_relation rel ON (ma.id = rel.item_id)
   WHERE
   rel.att_id = 79 AND             -- 79 ID de l'attribut [tags]
   rel.value_id = {{page::id}} AND -- ID de page variable
   ma.published = 1
   ORDER BY ma.name


Filtrage d'une sélection dans le BE pour une table non-MM
****************************************************************

Si, pour l'attribut de sélection simple [select], une table qui n'est pas une table MM a été
sélectionnée, il est possible, en tant que filtre, de saisir une « restriction WHERE ».
Si l'on souhaite par ex. avoir dans son jeu de données une connexion vers la table des membres
« tl_member », mais avec la restriction qu'un membre ne puisse être sélectionné qu'une seule fois,
il faut insérer la chaîne suivante :

.. code-block:: sql
   :linenos:

   (SELECT tl_member.id FROM tl_member
    LEFT JOIN mm_member
           ON mm_member.memberId=tl_member.id
      WHERE
            mm_member.memberId IS NULL
      AND
            tl_member.id=sourceTable.id)


Séparer l'ID du paramètre GET après '::'
********************************************

Pour les filtrages en backend ou pour l'édition en frontend, il faut parfois accéder
à l'ID à partir du paramètre GET de l'URL. Celui-ci est cependant couplé à un nom de
table via '::' et doit être séparé pour être utilisé dans une requête SQL personnalisée.
Cela se fait par ex. via la commande `SUBSTRING_INDEX` dans la requête, comme le montre
l'exemple suivant :

.. code-block:: sql
   :linenos:

   -- URL : ....&id=mm_mitarbeiter::51&...
   SELECT * FROM mm_mitarbeiter
   WHERE `id` = SUBSTRING_INDEX({{param::get?name=id}},'::',-1)


Filtre pour une sélection/des tags dans le masque de saisie
****************************************************************

Les attributs Sélection simple et Sélection multiple (Select et Tags) peuvent être dotés
d'un filtre pour le masque de saisie. Si ce filtre doit réagir dynamiquement à un autre
attribut du masque de saisie, on peut utiliser la règle de filtre « SQL personnalisé »
et employer les paramètres dynamiques.

Comme paramètre dynamique, on peut par ex. exploiter l'URL avec les paramètres GET ou, en
cas de `submitonchange` d'un attribut du masque de saisie, les paramètres POST. En GET, on
part de l'ID du jeu de données, et en POST, de la ou des valeurs de l'attribut déclencheur.

Par exemple, on souhaite que, sur la sélection du département, la liste des employés
sélectionnables soit restreinte à ceux appartenant au même département. On « écoute » le
paramètre POST du département, puis on peut restreindre la liste des employés avec QUERY-P
(POST) ou QUERY-G (GET).

.. code-block:: sql
   :linenos:

   SELECT `id` FROM  mm_mitarbeiter
   WHERE IF (
         {{param::post?name=abteilung}} != 'NULL', (QUERY-P), (QUERY-G)
    )

On peut ainsi également rendre deux sélections dépendantes l'une de l'autre. Si l'on a une
table pour les catégories ``mm_markt_kategorie`` et une table enfant avec des sous-catégories
``mm_markt_unterkategorie`` ainsi qu'une table ``mm_markt_maschine`` dans laquelle les deux
tables sont intégrées en sélection simple. Si, dans le masque de saisie des machines, une
catégorie est sélectionnée, seuls les éléments correspondants doivent apparaître dans le
select des sous-catégories. Pour cela, il faudrait intégrer la règle de filtre SQL suivante
dans le modèle des sous-catégories :

.. code-block:: sql
   :linenos:

   SELECT unterkategorie.id FROM mm_markt_unterkategorie AS unterkategorie
   WHERE IF (
       {{param::post?name=category}} != 'NULL',
       unterkategorie.pid = (
           SELECT kategorie.id FROM mm_markt_kategorie AS kategorie
           WHERE kategorie.alias = {{param::post?name=category}}
           LIMIT 1
       ),
       unterkategorie.pid = (
           SELECT markt.category
           FROM mm_markt_maschine AS markt
           WHERE markt.id = SUBSTRING_INDEX({{param::get?name=id}},'::',-1)
           LIMIT 1
       )
   )

Pour la restriction d'une sélection multiple, il faut ruser un peu, car la condition avec
IF dans les sous-requêtes ne permet pas de retourner plusieurs valeurs. Il est cependant
possible, avec GROUP_CONCAT, de générer une chaîne unique avec les ID, qui peut être évaluée
par IN.

Par exemple, pour l'attribut « Modules de voyage », les sélections possibles doivent être
restreintes à la sélection de l'attribut « Destinations ». Le modèle suivant se veut une
suggestion - il existe éventuellement des solutions plus élégantes.

.. code-block:: sql
   :linenos:

   SELECT rb.id FROM mm_reisebausteine AS rb
   WHERE rb.region IN (
       SELECT IF(
           {{param::post?name=reiseziele}} != 'NULL',
           (SELECT GROUP_CONCAT(rz.id) FROM mm_reiseziele AS rz
               WHERE rz.alias IN ({{param::post?name=reiseziele}}) GROUP BY rz.pid),
           (SELECT GROUP_CONCAT(rel.value_id) AS id FROM tl_metamodel_tag_relation AS rel
               WHERE rel.att_id = '42'
               AND rel.item_id = SUBSTRING_INDEX({{param::get?name=id}},'::',-1) GROUP BY rel.att_id)
       ) as id
   )

Filtre pour une sélection multiple dans le masque de saisie : uniquement les items non sélectionnés
***********************************************************************************************************

Si l'on a par ex. une table Régions avec une sélection multiple vers des pays et que l'on
souhaite restreindre la sélection aux pays qui n'ont pas encore été affectés, on peut activer
un filtre sur l'attribut Sélection multiple (ID : 42) pour les pays. Dans le filtre, on peut
créer une règle de filtre « SQL personnalisé » comme suit :

.. code-block:: sql
   :linenos:

   SELECT `id`
   FROM mm_countries
   WHERE `id` NOT IN (
       SELECT `value_id` as id
       FROM tl_metamodel_tag_relation
       WHERE `att_id` = '42'
   ) OR id IN (
       SELECT `value_id` as id
       FROM tl_metamodel_tag_relation
       WHERE `att_id` = '42'
       AND `item_id` = SUBSTRING_INDEX({{param::get?name=id}},'::',-1)
   )

Distinction du filtrage entre frontend et backend
*******************************************************

.. note:: Depuis MM 2.3, une option a été ajoutée à la règle de filtre, permettant de déterminer
   l'environnement d'exécution, par ex. « Backend uniquement ». Cela permet de simplifier les
   requêtes SQL.

Pour les filtrages avec SQL personnalisé, il peut être nécessaire d'établir une distinction
entre frontend et backend. Depuis MM 2.2, les filtres configurés pour les attributs Select et
Tags sont également appliqués en frontend, ce qui peut poser des problèmes avec les règles de
filtrage qui ne doivent s'appliquer que dans le masque de saisie.

On peut effectuer une requête sur la chaîne de requête actuelle et y rechercher son propre nom
de modèle comme premier mot, par ex. « mm_employees ».

.. code-block:: sql
   :linenos:

   SELECT artd.id FROM mm_article_details artd
   LEFT JOIN tl_metamodel_tag_relation rel ON (artd.id = rel.item_id)
   WHERE
   IF (SUBSTRING_INDEX(SUBSTRING_INDEX('{{env::request}}', '/', -1), '?', 1) = 'mm_employees',
      rel.att_id = 43 AND                                             -- 43 ID de l'attribut [tags]
      rel.value_id = SUBSTRING_INDEX({{param::get?name=id}},'::',-1), -- ID variable de l'URL pour l'article/produit
      1=1
   )

.. note:: Depuis la version MM 2.3-beta1, le routage dans le BE a changé - au lieu de
   ``domain.de/contao?do=metamodel_mm_employees&act=edit...``, on a désormais
   ``domain.de/contao/metamodel/mm_employees?act=edit``, c.-à-d. qu'avant ce changement, la
   requête ``SUBSTRING_INDEX(SUBSTRING_INDEX('{{env::request}}', '/', -1), '?', 1)`` retournait
   la valeur « contao ».


Commentaires dans la requête SQL
*************************************

Les requêtes SQL peuvent devenir assez complexes et contenir certaines valeurs
fixes comme des ID d'attributs, etc. Pour ne pas perdre le fil ultérieurement
ou lors du travail en équipe, on peut également y insérer des commentaires -
plus d'informations dans le `manuel de référence MySQL <https://dev.mysql.com/doc/refman/5.6/en/comments.html>`_.

Exemple :
|img_sql-comment|


.. |img_about| image:: /_img/icons/about.png
.. |img_help| image:: /_img/icons/help.svg
.. |img_sql-comment| image:: /_img/screenshots/cookbook/filter/sql-comment.jpg

