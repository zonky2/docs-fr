.. _cookbook_install_mm2.1-alpha:

Installer MetaModels 2.1 pour le test alpha
===========================================

Pour l'installation de MM 2.1, les conditions indiquées dans :ref:`manual_install` s'appliquent.

Il existe actuellement encore des problèmes avec le ``strict mode``, qui est activé par défaut dans les
installations MariaDB plus récentes. Actuellement, il faut soit désactiver le `strict mode`, soit retirer
manuellement, dans la base de données, le ``NOT NULL`` des champs de ses propres tables MM qui ont une valeur
par défaut.

Pendant le test alpha, les bundles `bundle_start` ou `bundle_all` ne sont pas encore disponibles pour
l'installation. Outre le noyau, les paquets nécessaires pour les attributs et les filtres doivent être
installés séparément.

Le choix se fait soit via le Contao-Manager, soit en mettant à jour directement le fichier `composer.json`.

Comme implémentation de base, tant pour le composer.json directement que pour le Contao-Manager, les paquets
suivants doivent être installés, avec les indications de version suivantes :

* MM-Core ``^2.1.0@dev``
* DC_General avec ``dev-feature/contao4-release as 2.1.0``
* MultiColumnWizard (MCW) avec ``^3.4.0@beta``

Comme modèle pour le `composer.json`, les indications suivantes peuvent être reprises dans « require » :

.. code-block:: json
   :linenos:

   "require": {
     "php": "^7.1",
     "contao-community-alliance/dc-general": "^2.1",
     "contao/manager-bundle": "<4.5",
     "contao/installation-bundle": "<4.5",
     "menatwork/contao-multicolumnwizard-bundle": "^3.4",
     "metamodels/core": "^2.1.0@dev",
     "metamodels/attribute_alias": "^2.1.0@dev",
     "metamodels/attribute_checkbox": "^2.1.0@dev",
     "metamodels/attribute_color": "^2.1.0@dev",
     "metamodels/attribute_combinedvalues": "^2.1.0@dev",
     "metamodels/attribute_country": "^2.1.0@dev",
     "metamodels/attribute_decimal": "^2.1.0@dev",
     "metamodels/attribute_file": "^2.1.0@dev",
     "metamodels/attribute_langcode": "^2.1.0@dev",
     "metamodels/attribute_levensthein": "^2.1.0@dev",
     "metamodels/attribute_longtext": "^2.1.0@dev",
     "metamodels/attribute_numeric": "^2.1.0@dev",
     "metamodels/attribute_rating": "^2.1.0@dev",
     "metamodels/attribute_select": "^2.1.0@dev",
     "metamodels/attribute_tabletext": "^2.1.0@dev",
     "metamodels/attribute_tags": "^2.1.0@dev",
     "metamodels/attribute_text": "^2.1.0@dev",
     "metamodels/attribute_timestamp": "^2.1.0@dev",
     "metamodels/attribute_url": "^2.1.0@dev",
     "metamodels/attribute_translatedalias": "^2.1.0@dev",
     "metamodels/attribute_translatedcheckbox": "^2.1.0@dev",
     "metamodels/attribute_translatedcombinedvalues": "^2.1.0@dev",
     "metamodels/attribute_translatedfile": "^2.1.0@dev",
     "metamodels/attribute_translatedlongtext": "^2.1.0@dev",
     "metamodels/attribute_translatedselect": "^2.1.0@dev",
     "metamodels/attribute_translatedtabletext": "^2.1.0@dev",
     "metamodels/attribute_translatedtags": "^2.1.0@dev",
     "metamodels/attribute_translatedtext": "^2.1.0@dev",
     "metamodels/attribute_translatedurl": "^2.1.0@dev",
     "metamodels/filter_checkbox": "^2.1.0@dev",
     "metamodels/filter_fromto": "^2.1.0@dev",
     "metamodels/filter_range": "^2.1.0@dev",
     "metamodels/filter_select": "^2.1.0@dev",
     "metamodels/filter_tags": "^2.1.0@dev",
     "metamodels/filter_text": "^2.1.0@dev",
     "metamodels/filter_register": "^2.1.0@dev"
   },

Il convient de noter que seuls les paquets réellement utilisés doivent être installés - en particulier si vous
avez travaillé auparavant avec `bundle_all`.

Une requête dans la base de données permet de déterminer rapidement les attributs et filtres utilisés :

.. code-block:: sql
   :linenos:

   -- Attribute
   SELECT type FROM `tl_metamodel_attribute` GROUP BY type ORDER BY type

   -- Filter
   SELECT type FROM `tl_metamodel_filtersetting` GROUP BY type ORDER BY type
