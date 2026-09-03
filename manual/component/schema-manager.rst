.. _component_schema-manager:

Gestionnaire de schéma
=======================

.. note:: Le gestionnaire de schéma est implémenté à partir de la version 2.3.

Bref aperçu
-----------

Avec le gestionnaire de schéma, les tables mm_* des Models et les colonnes des attributs ne sont
plus créées immédiatement lors de l'enregistrement. Il est nécessaire d'effectuer une migration de
base de données via la console, le Manager ou l'outil d'installation - de manière analogue à la
procédure lorsque des modifications de la base de données sont dues via le DCA. Des indications
correspondantes sont fournies dans le masque de saisie du Model et des attributs.


Contexte
--------

Dans MetaModels 2.3, un nouveau gestionnaire de schéma a été mis en place, établissant la
communication avec Doctrine. Doctrine est la couche d'abstraction de base de données de Symfony,
sur laquelle Contao s'appuie également. L'utilisation du nouveau gestionnaire de schéma résulte de
nécessités telles que le fait que Contao ne considère pas les tables mm_* comme « étrangères » et
souhaiterait les supprimer. Son utilisation apporte des avantages, comme une construction de table
propre et sûre, celle-ci étant surveillée par Doctrine. La modification, la suppression ou la
copie d'attributs ne doivent plus être prises en charge par MM, mais sont désormais effectuées par
Doctrine.

Ce changement entraîne également une modification fondamentale du travail avec MM : lors de la
création d'un Model et d'attributs, une migration de base de données doit désormais toujours être
effectuée par les moyens habituels (console, Manager ou outil d'installation) - comme cela a
toujours été nécessaire et l'est encore pour Contao et les modifications du DCA.

Pour les colonnes, cela n'est pertinent que pour les attributs qui créent leur propre colonne dans
la table mm_*, comme par ex. Texte ou Alias (attribut simple).

Ce changement anticipe quelque peu ce qui aurait de toute façon eu lieu au plus tard avec MM 3.0.
Il devrait également être possible de définir le schéma de base de données de MM via des fichiers.
Cela permettrait le versionnement, la réutilisabilité ainsi que l'export/import. Avec cette
fonctionnalité, une adaptation du schéma ne sera possible que par l'exécution d'une migration de
base de données.

L'adaptation de son propre « workflow MM » nécessitera certainement un certain temps
d'accoutumance, mais avec le gestionnaire de schéma, une base technique plus évolutive pour la
gestion de la base de données a été créée.

Étant donné que Doctrine divise les modifications de tables ou de colonnes existantes en deux
actions, il est possible de « sauver » les données existantes - voir les :ref:`conseils
<rst_cookbook_tips_change_table_column_name>`.

Le gestionnaire de schéma permet d'adapter durablement les types de colonnes - les modifications
sont également prises en compte par la migration de base de données - voir
:ref:`rst_cookbook_inputmask_manipulate-schema`.
