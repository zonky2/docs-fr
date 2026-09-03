.. _rst_cookbook_inputmask_manipulate-schema:

Adaptation du schéma pour les attributs
=======================================

.. note:: Le gestionnaire de schéma est implémenté depuis la version 2.3.

Les propriétés de la base de données pour les attributs sont manipulées via le gestionnaire de schéma - voir
:ref:`component_schema-manager` - et non par une adaptation du DCA. Les modifications sont vérifiées et exécutées
lors du déroulement de la migration de la base de données - celle-ci peut être déclenchée via le Contao-Manager ou
via la console.

Dans l'exemple suivant, le champ de l'attribut texte long `vita` du modèle `mm_employees` est modifié de `TEXT`
(65535) à `MEDIUMTEXT` (16777215) - voir
`Doctrine <https://www.doctrine-project.org/projects/doctrine-dbal/en/latest/reference/types.html#mapping-matrix>`_ et
`Github <https://github.com/doctrine/dbal/blob/369ab24fc865939ff451c5214742cebac052f2f1/src/Platforms/AbstractMySQLPlatform.php#L40-L46>`_.

.. code-block:: php
   :linenos:

   <?php
   // src/SchemaManager/SchemaManager.php
   namespace App\SchemaManager;

   use Doctrine\DBAL\Platforms\AbstractMySQLPlatform;
   use MetaModels\Information\MetaModelCollectionInterface;
   use MetaModels\Schema\Doctrine\DoctrineSchemaGeneratorInterface;
   use MetaModels\Schema\Doctrine\DoctrineSchemaInformation;

   #[DoctrineSchemaProvider(-20)]
   final class SchemaManager implements DoctrineSchemaGeneratorInterface
   {
       public function generate(DoctrineSchemaInformation $schema, MetaModelCollectionInterface $collection): void
       {
           if (!$schema->getSchema()->hasTable('mm_employees')) {
               return;
           }

           $table = $schema->getSchema()->getTable('mm_employees');

           $table->getColumn('vita')->setLength(AbstractMySQLPlatform::LENGTH_LIMIT_MEDIUMTEXT);
       }
   }

Si l'on ne peut pas ou ne souhaite pas travailler avec l'enregistrement via l'attribut « DoctrineSchemaProvider »,
l'enregistrement peut alternativement se faire via ``services.yml``.

.. code-block:: yml
   :linenos:

   # config/services.yml
   services:
     App\SchemaManager\SchemaManager:
       tags:
         - { name: 'metamodels.schema-generator.doctrine', priority: -20 }

Pour vérifier si son propre gestionnaire de schéma a été enregistré et chargé, on peut le contrôler en console avec

``php vendor/bin/contao-console debug:container``

Plus d'informations à ce sujet : ":ref:`rst_cookbook_specials_register-services`".

.. |br| raw:: html

   <br />
