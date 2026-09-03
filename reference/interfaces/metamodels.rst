.. _ref_api_interf_mm:

Interfaces MetaModels
======================

Les interfaces MetaModels constituent la base des interfaces et
permettent l'accès à un MetaModel jusqu'à l'item individuel.

De nombreux travaux liés à l'utilisation des interfaces se concentrent
sur l'interrogation des données existantes d'un MetaModel. La structure suit
ici la logique d'une requête ou d'un listage via l'élément de contenu
ou le module frontend avec


* Connexion à MetaModels ; par exemple pour établir une connexion en dehors
  d'un template MetaModel - voir :ref:`ref_api_interf_mm_metamodelsservicecontainer`
* Connexion au MetaModel - voir :ref:`ref_api_interf_mm_factory`
* Interrogation d'un MetaModel en tenant compte des règles de filtre
  - voir :ref:`ref_api_interf_mm_metamodel`
* Interrogation et définition de la langue active pour les MetaModels traduits - voir
  :ref:`ref_api_interf_mm_translatedmetamodel`
* Accès à tous les items ; éventuellement analyse (parsing) des items avec indication du format de sortie
  (texte, HTML5) et du paramètre de rendu) - voir :ref:`ref_api_inteface_items`
* Accès à un item ou sortie (brute, texte, HTML5) - voir :ref:`ref_api_interf_mm_item`

En outre, les interfaces d'un MetaModel permettent également de créer différents objets (MetaModel,
attribut, item), de modifier leurs valeurs ou d'interroger leurs propriétés telles que
le nombre ou la langue.


.. _ref_api_interf_mm_metamodelsservicecontainer:

Interface MetaModelsServiceContainer :
.......................................

L'interface MetaModelsServiceContainer permet d'établir une connexion à
MetaModels. Ceci est par exemple nécessaire lorsqu'un accès au MetaModel
en dehors d'un template MetaModel est requis.

Pour accéder à cette interface, il faut disposer d'un « Service Container », que l'on peut
par exemple récupérer dans la portée globale (scope)

``$container = $this->getContainer();``

On peut ensuite y accéder via une interface - par exemple :

``$factory = $container->getFactory();`` |br|
ou bien |br|
``$factory = $this->getContainer()->get('metamodels.factory');``

L'accès via $GLOBALS permet d'accéder facilement au conteneur de services depuis
ses propres templates et programmations. D'autres possibilités
seraient les événements comme par exemple « \MetaModelsEvents::SUBSYSTEM_BOOT ».

Informations actuelles sur : `IMetaModelsServiceContainer <https://github.com/MetaModels/core/blob/master/src/IMetaModelsServiceContainer.php>`_

**Interfaces :**

``getFactory()`` |br|
renvoie l'accès à MetaModels

``getAttributeFactory()`` |br|
renvoie l'accès aux attributs

``getFilterFactory()`` |br|
renvoie l'accès aux filtres

``getRenderSettingFactory()`` |br|
renvoie l'accès aux paramètres de rendu

``getEventDispatcher()`` |br|
renvoie l'accès au dispatcher d'événements

``getDatabase()`` |br|
renvoie l'accès à la base de données

``getCache()`` |br|
renvoie l'accès au cache

``setService($service, $serviceName = null)`` |br|
ajoute un service personnalisé au conteneur

``getService($serviceName)`` |br|
renvoie l'accès à un service portant le nom transmis


.. _ref_api_interf_mm_servicecontaineraware:

Interface ServiceContainerAware :
...................................

L'interface ServiceContainerAware permet d'obtenir un accès au
conteneur de services ou d'en attribuer un nouveau.

Informations actuelles sur : `IServiceContainerAware <https://github.com/MetaModels/core/blob/master/src/IServiceContainerAware.php>`_

**Interfaces :**

``setServiceContainer(IMetaModelsServiceContainer $serviceContainer)`` |br|
définit le conteneur de services à utiliser

``getServiceContainer()`` |br|
renvoie le conteneur de services


.. _ref_api_interf_mm_factory:

Interface Factory :
.....................

L'interface Factory permet de créer des instances d'un MetaModel et d'interroger
certaines propriétés.

La création d'un nouveau MetaModel n'est pas prévue - bien que possible - car
sa création nécessiterait de transmettre des paramètres très complexes, et la
création est plutôt conçue pour être réalisée depuis le backend.

Informations actuelles sur : `IFactory <https://github.com/MetaModels/core/blob/master/src/IFactory.php>`_

**Interfaces :**

``getMetaModel($modelName);`` |br|
crée une instance de MetaModel avec le nom transmis

``translateIdToMetaModelName($modelId);`` |br|
renvoie le nom correspondant à un ID de MetaModel

``collectNames();`` |br|
renvoie tous les noms de MetaModel sous forme de tableau

``getServiceContainer();`` |br|
renvoie le conteneur de services

.. warning:: Les méthodes `byTableName`, `byId` et `getAllTables`
   ont été supprimées dans la version 2.0

``byTableName($strTableName);`` |br|
utiliser la méthode ``getMetaModel($modelName);``

``byId($intMetaModelId);`` |br|
utiliser la méthode ``getMetaModel($modelName);`` avec
``translateIdToMetaModelName($modelId);``

``getAllTables();`` |br|
utiliser la méthode ``collectNames();``



.. _ref_api_interf_mm_metamodel:

Interface MetaModel :
.......................

L'interface MetaModel permet d'interroger ou d'influencer les propriétés
d'une instance de MetaModel.

Il faut d'abord créer une instance de MetaModel via l'ID ou le nom d'un MetaModel
(voir :ref:`ref_api_interf_mm_factory`)

``$model = \MetaModels\IFactory::getMetaModel($modelName);``

ou bien, en incluant le conteneur de services :

.. code-block:: php
   :linenos:

   <?php
   $modelId = 42;

   /** @var $container */
   $factory   = $this->getContainer()->get('metamodels.factory');
   $modelName = $factory->translateIdToMetaModelName($modelId);
   $model     = $factory->getMetaModel($modelName);


On peut ensuite interroger ou définir une propriété - par exemple l'interrogation
de tous les attributs existants :

``$attributes = $metaModel->getAttributes();``

Informations actuelles sur : `IMetaModel <https://github.com/MetaModels/core/blob/master/src/IMetaModel.php>`_

**Interfaces :**

.. warning:: La méthode `getServiceContainer` est dépréciée - merci
   de l'intégrer comme service

``getServiceContainer()`` |br|
renvoie le conteneur de services

``get($strKey)``  |br|
renvoie les paramètres de configuration

``getTableName()``  |br|
renvoie le nom de la table du MetaModel instancié

``getName()``  |br|
renvoie le nom du MetaModel instancié

.. warning:: La méthode `isTranslated` est dépréciée - merci
   d'utiliser ITranslatedMetaModel

``isTranslated()``  |br|
vérifie si le MetaModel instancié peut créer des traductions

``hasVariants()``  |br|
vérifie si le MetaModel instancié peut créer des variantes

.. warning:: La méthode `getAvailableLanguages` est dépréciée - merci
   d'utiliser ITranslatedMetaModel

``getAvailableLanguages()``  |br|
renvoie tous les codes de langue du MetaModel instancié sous forme de tableau

.. warning:: La méthode `getFallbackLanguage` est dépréciée - merci
   d'utiliser ITranslatedMetaModel

``getFallbackLanguage()``  |br|
renvoie le code de la langue de repli (fallback) du MetaModel instancié

.. warning:: La méthode `getActiveLanguage` est dépréciée - merci
   d'utiliser ITranslatedMetaModel

``getActiveLanguage()``  |br|
renvoie le code de la langue active du MetaModel instancié

``addAttribute(IAttribute $attribute)``  |br|
ajoute un attribut à la liste interne des attributs

``hasAttribute($attributeName)``  |br|
vérifie si un attribut portant le nom donné existe dans la liste interne des
attributs

``getAttributes()``  |br|
renvoie un tableau contenant tous les attributs du MetaModel instancié

``getInVariantAttributes()``  |br|
renvoie un tableau contenant les attributs du MetaModel instancié
qui ne sont pas définis comme variantes

``getAttribute($attributeName)``  |br|
renvoie l'instance de l'attribut portant le nom d'attribut donné

``getAttributeById($id)``  |br|
renvoie l'instance de l'attribut portant l'ID d'attribut donné

``findById($id, $attrOnly = [])``  |br|
renvoie l'item portant l'ID donné ; un tableau contenant des noms d'attributs
dont les valeurs doivent être renvoyées peut être indiqué en option

``getEmptyFilter()``  |br|
crée un objet de filtre « vide » sans règle de filtre

.. warning:: La méthode `prepareFilter` est dépréciée - merci
   d'utiliser la Filter-Setting-Factory

``prepareFilter($filterSettings, $filterUrl)``  |br|
crée un objet de filtre à partir d'un ID de filtre donné et d'un tableau
optionnel de paramètres de filtre, par exemple pour reprendre des valeurs GET
depuis une URL

``findByFilter(
$filter,
$sortBy = '',
$offset = 0,
$limit = 0,
$sortOrder = 'ASC',
$attrOnly = []
)``  |br|
renvoie les items déterminés selon un filtre donné dans le MetaModel
instancié - outre les paramètres de tri, d'offset, de limite
et de sens du tri, un tableau de noms d'attributs peut être indiqué pour
préciser les valeurs à renvoyer

``getIdsFromFilter(
$filter,
$sortBy = '',
$offset = 0,
$limit = 0,
$sortOrder = 'ASC'
)``  |br|
renvoie les ID des items déterminés selon un filtre donné dans le MetaModel
instancié - les paramètres de tri, d'offset, de limite
et de sens du tri peuvent être indiqués

``getCount($filter)``  |br|
renvoie le nombre d'items déterminés selon un filtre donné

``findVariantBase($filter)``  |br|
renvoie tous les items d'une base de variantes déterminés selon un filtre donné

``findVariants($ids, $filter)``  |br|
renvoie tous les items de variantes d'un tableau d'ID et d'un filtre donné

``findVariantsWithBase($ids, $filter)``  |br|
renvoie tous les items de variantes d'un tableau d'ID et d'un filtre donné ;
la requête ne fait pas de distinction entre les items d'une base de variantes et les items eux-mêmes

``getAttributeOptions($attribute, $filter = null)``  |br|
renvoie toutes les options d'un attribut donné ; un filtre peut être
indiqué en option

``saveItem($item, $timestamp = null)``  |br|
enregistre un item donné ; un nouvel item est créé si aucun ID n'a été
transmis

``delete($item)``  |br|
supprime un item donné

.. warning:: La méthode `getView` est dépréciée - merci
   d'utiliser la Render-Setting-Factory

``getView($viewId = 0)``  |br|
renvoie l'instance des paramètres de rendu du MetaModel instancié


.. _ref_api_interf_mm_translatedmetamodel:

Interface Translated MetaModel :
..................................

.. note:: Cette fonctionnalité est disponible à partir de MM 2.2.

L'interface Translated MetaModel permet d'interroger ou de définir les paramètres
de langue d'un MetaModel traduit.

Jusqu'à la version MM 2.1, la langue active d'un MetaModel traduit ne pouvait être
obtenue qu'en définissant (temporairement) ``$GLOBALS['TL_LANGUAGE']``. Avec cette interface,
il est possible de définir la langue du MetaModel indépendamment de la langue du backend de
Contao.

Si, par exemple, pour un MetaModel traduit, un item doit être enregistré dans une langue
donnée, la langue peut être définie via le code de langue (de, en, fr, ...) comme suit :

``$model->selectLanguage('fr');``

Une vérification de type peut être implémentée comme suit :

.. code-block:: php
   :linenos:

   <?php

   use MetaModels\ITranslatedMetaModel;

   if ($model instanceof ITranslatedMetaModel) {
       // faire quelque chose...
   }

À partir de MetaModels 2.2, les interfaces suivantes doivent être utilisées :

**Interfaces :**

``getLanguages()``  |br|
détermine tous les codes de langue marqués comme disponibles pour la traduction dans ce MetaModel

``getMainLanguage()``  |br|
détermine le code de langue marqué comme langue de repli (fallback) dans ce MetaModel

``getLanguage()``  |br|
détermine le code de langue actuel

``selectLanguage($activeLanguage)``  |br|
définit la nouvelle langue active et renvoie le code de la langue précédente


.. _ref_api_inteface_items:

Interface Items :
...................

L'interface Items permet d'interroger les propriétés des items.

Il faut d'abord créer une instance de MetaModel via l'ID ou le nom d'un MetaModel,
puis déterminer une liste d'items, par exemple via un filtre.

``$items = $model->findByFilter($filter);``

On peut ensuite interroger une propriété - par exemple l'interrogation
du nombre total d'items existants :

``$amountItems = $items->getCount();``

Informations actuelles sur : `IItems <https://github.com/MetaModels/core/blob/master/src/IItems.php>`_

**Interfaces :**

``getItem()``  |br|
renvoie l'item actuel

``getCount()``  |br|
renvoie le nombre d'items

``first()``  |br|
place le pointeur sur le premier élément des items

``prev()``  |br|
place le pointeur sur l'élément suivant des items

``last()``  |br|
place le pointeur sur le dernier élément des items

``reset()``  |br|
réinitialise le résultat actuel

``getClass()``  |br|
renvoie la classe CSS de l'item actuel (first, last, even, odd)

``parseValue($outputFormat = 'text', $settings = null)``  |br|
analyse (parse) l'item actuel et renvoie le résultat sous forme de tableau des attributs ;
pour les sorties en HTML5, les paramètres de rendu doivent être transmis
en tant que $objSettings, par exemple $metaModel->getView(3)

``parseAll($outputFormat = 'text', $settings = null)``  |br|
analyse (parse) tous les items et renvoie le résultat sous forme de tableau des items avec leurs attributs ;
pour les sorties en HTML5, les paramètres de rendu doivent être transmis
en tant que $objSettings, par exemple $metaModel->getView(3)


.. _ref_api_interf_mm_item:

Interface Item :
..................

L'interface Item permet d'interroger les propriétés d'un item.

Il faut d'abord créer une instance de MetaModel via l'ID ou le nom d'un MetaModel,
puis déterminer une liste d'items, par exemple via un filtre (éventuellement
également un filtre vide).

``$items = $model->findByFilter($filter);``  |br|

On peut ensuite interroger une propriété - par exemple l'interrogation
de la valeur d'un attribut :

``$attribute = $items->getItem()->get($attributeName);``  |br|

Un nouvel item est créé comme suit :

``$item = new \MetaModels\Item($model, []);``

Dans le tableau transmis, des « paires clé-valeur » peuvent être passées - mais cela
n'a de sens que pour des types d'items simples comme le texte.

Informations actuelles sur : `IItem <https://github.com/MetaModels/core/blob/master/src/IItem.php>`_

**Interfaces :**

``get($attributeName)``  |br|
renvoie la valeur d'un attribut pour le nom d'attribut donné

``set($attributeName, $value)``  |br|
définit la valeur d'un attribut pour le nom d'attribut donné

``getMetaModel()``  |br|
renvoie l'instance du MetaModel de l'item

``getAttribute($attributeName)``  |br|
renvoie l'instance d'un attribut pour le nom d'attribut donné

``isVariant()``  |br|
détermine si l'item est une variante d'un autre item

``isVariantBase()``  |br|
détermine si l'item est une base de variantes

``getVariants($filter)``  |br|
renvoie un tableau avec les variantes de l'item, ou null si l'item ne
gère pas les variantes

``getVariantBase()``  |br|
renvoie l'item de la base de variantes ; pour un item sans variantes,
la base de variantes est l'item lui-même

``parseValue($outputFormat = 'text', $settings = null)``  |br|
rend l'item dans le format indiqué ; les données brutes [raw]
sont toujours renvoyées, y compris les attributs des MetaModels référencés

``parseAttribute($attributeName, $outputFormat = 'text', $settings = null)``  |br|
rend un attribut individuel de l'item dans le format indiqué ; les données brutes [raw]
sont toujours renvoyées, y compris les attributs des MetaModels référencés

``copy()``  |br|
crée un nouvel item en tant que copie d'un item existant

``varCopy()``  |br|
crée un nouvel item en tant que copie d'un item existant, sous forme de variante

``save()``  |br|
enregistre la ou les valeurs actuelles de l'item


Exemple :
..........

L'exemple suivant vise à fournir une petite introduction au travail avec les interfaces. Pour tester le travail
avec l'API, vous pouvez vous inspirer de la
`présentation d'Ingolf Steinhardt à la CK23 <https://www.e-spin.de/contao-metamodels/metamodels-vortrag-contao-konferenz-2023.html>`_.

Des exemples d'utilisation des filtres se trouvent ici : :ref:`ref_api_interf_filter`

L'exemple se base sur l'extension de ":ref:`mm_first_index`".

.. code-block:: php
   :linenos:

   <?php
   // Exemple d'implémentation dans un fichier de template à des fins de test.
   // Dans un environnement de production, il est conseillé d'utiliser une « classe d'assistance » et d'y injecter les services.


   // Nom de la table MetaModel (voir « Premier MetaModel »)
   $modelName = 'mm_mitarbeiterliste';
   // ID des paramètres de rendu « FE-Liste »
   $renderId = 2;
   // ID du filtre
   $filterId = 1;

   // Factories MM
   $factory       = \Contao\System::getContainer()->get('metamodels.factory');
   $renderFactory = \Contao\System::getContainer()->get('metamodels.render_setting_factory');

   // Créer le MetaModel si le nom de la table/du MetaModel est connu.
   $model = $factory->getMetaModel($modelName);
   // Créer le MetaModel si seul l'ID est connu ($metaModelId == tl_metamodel.id du MetaModel).
   //$model = $factory->getMetaModel($factory->translateIdToMetaModelName($metaModelId));

   // filtre vide - voir aussi « Interfaces de filtre »
   $filter = $model->getEmptyFilter();
   // filtre prédéfini via l'ID de filtre ; en second paramètre, un tableau de valeurs peut être transmis au filtre
   //$filter = $model->prepareFilter($filterId, []);

   // récupérer tous les items avec le filtre
   $items = $model->findByFilter($filter);

   // nombre d'items
   echo 'Nombre : '.$items->getCount()."<br>\n";
   // ou vérification
   if (!$items->getCount()) {
       return;
   }

   // Sortie : variante 1 - objet Items
   /*
   foreach ($items as $item)
   {
       echo $item->get('name')."<br>\n";
   }
   */

   // Sortie : variante 2 - tableau Items
   // tous les items analysés (parsed) sous forme de tableau avec des nœuds HTML5
   $arrItems = $items->parseAll('html5', $renderFactory->createCollection($model, $renderId));
   // alternativement, seulement les nœuds raw et text
   //$arrItems = $items->parseAll('text');
   foreach ($arrItems as $arrItem)
   {
       echo $arrItem['html5']['name']."<br>\n";
   }

   // Sortie : variante 3 - traiter uniquement l'item actuel
   $item = $items->getItem()->parseValue('text', $renderFactory->createCollection($model, $renderId));
   echo $item['text']['name']."<br>\n";


.. |br| raw:: html

   <br />
