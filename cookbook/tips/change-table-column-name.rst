.. _rst_cookbook_tips_change_table_column_name:

Modifier le nom d'une table ou d'une colonne
================================================

.. note:: Le gestionnaire de schéma est implémenté à partir de la version 2.3 - :ref:`voir le gestionnaire de schéma <component_schema-manager>`

Les noms de tables et de colonnes doivent être bien réfléchis, car une adaptation ultérieure est une opération
plutôt critique et devrait être évitée.

Une modification du nom d'une table ou d'une colonne reste néanmoins tout à fait possible. Avec le gestionnaire de
schéma, la tâche d'adaptation de la base de données est confiée à Doctrine, qui l'exécute dans le cadre d'une
migration de base de données. Chez Doctrine, il est prévu que, lors d'une modification du nom d'une table ou d'une
colonne, il n'y ait pas de simple renommage, mais que le nouvel élément soit créé et l'ancien supprimé.

Si aucune donnée utile n'est encore présente dans la table ou la colonne, l'adaptation peut se faire sans problème.

Si des données utiles existent déjà et doivent être conservées, il faut intervenir lors de l'adaptation et
sauvegarder les données. L'avantage du gestionnaire de schéma est que les deux actions (création/Create et
suppression/Drop) se déroulent l'une après l'autre, ce qui laisse l'occasion de transférer les données de
« l'ancien vers le nouveau » entre les deux.

Pour les colonnes, cela ne concerne que les attributs qui créent leur propre colonne dans la table mm_*, comme par
ex. Texte ou Alias (attribut simple).

Ce transfert peut s'effectuer dans l'un des outils de base de données habituels comme phpMyAdmin, ou directement en
console. Une fois la nouvelle table ou colonne créée, les données peuvent être copiées avec les commandes
suivantes :

Table : |br|
``php vendor/bin/contao-console doctrine:query:sql 'INSERT mm_test_neu SELECT * FROM mm_test_alt'``

Colonne : |br|
``php vendor/bin/contao-console doctrine:query:sql 'UPDATE mm_test SET col_neu=col_alt'``

Remarque : démarrer la migration : |br|
``php vendor/bin/contao-console contao:migrate``

Ensuite, la suppression/Drop peut être effectuée.

.. note:: Sous Windows, MySQL traite les noms de tables et de colonnes de manière insensible à la casse -
   c'est pourquoi une modification de la casse via MM n'est en principe pas possible.

.. |br| raw:: html

   <br />
