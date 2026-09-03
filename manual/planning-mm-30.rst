.. _planning_mm30:

Planification de MM 3.0
=======================

.. seealso:: Cette liste est complétée en continu

Voici quelques points prévus pour la planification de MM 3.0. Avec cette nouvelle version majeure, nous pourrons
effectuer des adaptations plus fondamentales sur MM et moderniser encore davantage l'infrastructure sous-jacente.

Les propositions à ce sujet sont les bienvenues sous forme de ticket sur `Github <https://github.com/MetaModels/core/issues>`_
- de préférence avec le préfixe de titre "[MM 3.0]"

* Passage aux UUID (par ex. pour le support de l'export/import)
* les différents MM devraient pouvoir être regroupés dans un "projet" - le niveau projet se situerait donc
  "au-dessus" des MM (actuellement, je fais cela avec un "sous-préfixe de projet" comme "mm__proj1*", "mm__proj2*").
  Les "niveaux de projet" devraient alors se retrouver dans toutes les tables des attributs ; dans l'idéal, on
  devrait ensuite pouvoir exporter et importer séparément toutes les tables du projet A et du projet B.
* Configuration via YAML/XML - à l'image des CustomElements de RST (https://app.intco.it/rsce-visual-editor/index.html)
  - la "GUI" actuelle dans le backend (via DCG ?) resterait conservée...

  * nécessaire pour l'export/import
  * enregistrement/suivi des adaptations (par ex. Git)
* Attributs répartis en classes :

  * refonte de la MM-API
  * attributs virtuels (pour des choses comme la Geodistance)
  * séparation stricte des attributs et suppression des dépendances (notamment pour les clés de langue etc.)
  * Alias aware interface https://github.com/MetaModels/core/issues/904, https://github.com/MetaModels/core/tree/feature-aliasaware
  * Templates en Twig
* Adaptations de la base de données :

  * moins de requêtes
  * ACL au niveau de la base de données
  * hiérarchie/arborescence => éventuellement Nested Set
  * journalisation/piste d'audit
  * versionnement/annulation
  * traductions
  * par ex. => http://symfony.com/doc/master/bundles/StofDoctrineExtensionsBundle/index.html
* Gestion de schéma (extraction des manipulations de schéma de base de données des attributs dans des classes
  autonomes, ... + gestionnaires de mise à jour etc.)

  * fonctionnalité de gestion de schéma : https://github.com/MetaModels/core/pull/1267
  * répartition de la table de relations en tables séparées (important également pour l'export/import)
* Symfony-Forms (DCG 3.0)
* approche API de MM pour communiquer par ex. via REST, Hydra-LD, GraphQL
* ASC/DESC etc. sous forme de constantes
* refonte des filtres :

  * meilleure mise en cache,
  * tri multiple,
  * tri des listes de sélection/cases à cocher/boutons radio,
  * filtrage hiérarchique,
  * transmission d'un objet liste d'ID plutôt qu'un tableau
  * optique/ergonomie backend : (y compris DCG)
  * CSS/templates
* nettoyage/réorganisation des réglages
* financement :

  * EAP

.. |br| raw:: html

   <br />
