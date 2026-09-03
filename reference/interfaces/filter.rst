.. _ref_api_interf_filter:

Interfaces de filtre
======================

Les interfaces de filtre permettent d'accéder aux filtres ou
règles de filtre définis dans le backend d'un MetaModel.

De plus, la programmation permet de créer d'autres filtres
ou de définir des paramètres de filtre.


.. _ref_api_interf_filter_filterrule:

Interface IFilterRule
.......................

Informations actuelles sur : `IFilterRule <https://github.com/MetaModels/core/blob/master/src/Filter/IFilterRule.php>`_

**Interfaces :**

``getMatchingIds()`` |br|
renvoie tous les ID correspondant à la règle de filtre donnée


.. _ref_api_interf_filter_filter:

Interface IFilter
...................

Informations actuelles sur : `IFilter <https://github.com/MetaModels/core/blob/master/src/Filter/IFilter.php>`_

**Interfaces :**

``addFilterRule(IFilterRule $objFilterRule)`` |br|
ajoute une règle de filtre à la chaîne de filtres

``getMatchingIds()`` |br|
renvoie tous les ID correspondant à la règle de filtre donnée

``createCopy()`` |br|
crée une copie du filtre


Exemples
.........

Les blocs « Filtrage » entre « Début » et « Fin » doivent être considérés comme des alternatives l'un à l'autre. Les
classes appelées doivent être importées de manière qualifiée via « use ».

.. code-block:: php
   :linenos:

   <?php
   // Début
   $modelName = 'mm_employees';
   $factory   = \Contao\System::getContainer()->get('metamodels.factory');
   // alternativement
   //$factory = $this->getContainer()->get('metamodels.factory');
   $model  = $factory->getMetaModel($modelName);
   $filter = $model->getEmptyFilter();

   // Filtrage selon une liste d'ID fixe :
   $idList = [1,2,3];
   $filter->addFilterRule(new \MetaModels\Filter\Rules\StaticIdList($idList));

   // Filtrage selon la valeur d'un attribut :
   $value      = 'marketing';
   $languages  = $model->getAvailableLanguages();
   $attribute  = $model->getAttribute('division');
   $filter->addFilterRule(new \MetaModels\Filter\Rules\SearchAttribute($attribute, $value, $languages));

   // SQL personnalisé *1 :
   $query = \sprintf('SELECT * FROM %s WHERE published = 1', $modelName);
   $filter->addFilterRule(new \MetaModels\Filter\Rules\SimpleQuery($query));
   // Alternativement, voir https://www.doctrine-project.org/projects/doctrine-dbal/en/4.2/reference/data-retrieval-and-manipulation.html
   $query = \sprintf('SELECT * FROM %s WHERE published = ?', $modelName);
   $filter->addFilterRule(new \MetaModels\Filter\Rules\SimpleQuery($query, [1]));

   // Filtrage avec plusieurs règles :
   // Combinaison avec ConditionAnd() ou ConditionOr()
   // Comparaison possible avec GreaterThan, LessThan, NotEqual
   $attribute        = $model->getAttribute('price');
   $compareInclusive = true;
   $andRule          = new \MetaModels\Filter\Rules\Condition\ConditionAnd();
   $andRule
       ->addRule(new \MetaModels\Filter\Rules\Comparing\GreaterThan($attribute, 10, $compareInclusive)) // >= 10
       ->addRule(new \MetaModels\Filter\Rules\Comparing\LessThan($attribute, 20));                      // < 20
   $filter->addFilterRule($andRule);

   // Fin
   $items    = $model->findByFilter($filter);
   $arrItems = $items->parseAll('text');
   //dump($arrItems);

*1 : Le SQL personnalisé peut également être construit via le
`queryBuilder Doctrine DBAL <https://www.doctrine-project.org/projects/doctrine-dbal/en/4.4/reference/query-builder.html>`_
et transmis à SimpleQuery. Le queryBuilder permet de construire élégamment une requête, par exemple lorsque
différentes dépendances doivent être prises en compte. Voici un exemple :

.. code-block:: php
   :linenos:

   <?php

   use Doctrine\DBAL\Connection;
   use MetaModels\Filter\Rules\SimpleQuery;

   // ...

   $modelName = 'mm_employees';
   $model     = $factory->getMetaModel($modelName);
   $filter    = $model->getEmptyFilter();

   $builder = $this->connection->createQueryBuilder()
               ->select('t.id')
               ->from($metaModel->getTableName(), 't');

   if ($checkUpload) {
       $builder->andWhere('t.upload_allowed = 1');
   }

   $filter = $metaModel->getEmptyFilter();
   $filter->addFilterRule(SimpleQuery::createFromQueryBuilder($builder));
   $items = $metaModel->findByFilter($filter, 'name');


.. |br| raw:: html

   <br />
