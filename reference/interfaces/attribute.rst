.. _ref_api_interf_attribute:

Interfaces des attributs
=========================

.. warning:: Encore en construction !

Les interfaces d'attributs permettent d'accéder aux
attributs - c'est-à-dire aux colonnes de la table MetaModel -
pour définir et lire des valeurs ou interroger des
informations.


.. _ref_api_interf_attribute_iattributefactory:

Interface IAttributeFactory
............................

L'interface IAttributeFactory est la « Factory Interface » pour l'interrogation
d'un attribut.

Informations actuelles sur : `IAttributeFactory <https://github.com/MetaModels/core/blob/master/src/Attribute/IAttributeFactory.php>`_

**Interfaces :**

``createAttribute($arrInformation, $objMetaModel)`` |br|
renvoie l'instance d'attribut pour un MetaModel donné et un tableau de
paramètres d'attribut

``addTypeFactory(IAttributeTypeFactory $typeFactory)`` |br|
ajoute une « type factory » à la « factory » donnée

``getTypeFactory($typeFactory)`` |br|
renvoie la « type factory » pour la « factory » donnée

``attributeTypeMatchesFlags($factory, $intFlags)`` |br|
vérifie l'attribut selon les flags à comparer

``getTypeNames($varFlags = false)`` |br|
renvoie les noms de types enregistrés de la factory

``collectAttributeInformation(IMetaModel $objMetaModel)`` |br|
renvoie toutes les informations d'attributs d'un MetaModel

``createAttributesForMetaModel($objMetaModel)`` |br|
renvoie toutes les instances d'attributs d'un MetaModel

``getIconForType($strType)`` |br|
renvoie l'icône pour un nom de type donné


.. _ref_api_interf_attribute_iattribute:

Interface IAttribute
......................

L'interface IAttribute est l'interface de base pour les attributs.

Informations actuelles sur : `IAttributeFactory <https://github.com/MetaModels/core/blob/master/src/Attribute/IAttribute.php>`_

**Interfaces :**

``getName()`` |br|
renvoie le nom (lisible) ou le titre d'un attribut

``getColName()`` |br|
renvoie le nom de colonne d'un attribut

``getMetaModel()`` |br|
renvoie l'instance de MetaModel d'un attribut

``get($strKey)`` |br|
renvoie les méta-informations d'un attribut pour la clé donnée

``set($strKey, $varValue)`` |br|
définit les méta-informations d'un attribut pour la clé donnée

``handleMetaChange($strMetaName, $varNewValue)`` |br|
remplace les méta-informations d'un attribut pour la clé donnée

``initializeAUX()`` |br|
crée toutes les données auxiliaires d'un attribut dans d'autres tables

``destroyAUX()`` |br|
supprime toutes les données auxiliaires d'un attribut dans d'autres tables

``getAttributeSettingNames()`` |br|
renvoie tous les noms de paramètres autorisés

``getFieldDefinition($arrOverrides = array())`` |br|
renvoie un DCA du type "$GLOBALS['TL_DCA']['tablename']['fields']['attribute-name]"
avec un tableau optionnel de paramètres à écraser

``valueToWidget($varValue)`` |br|
renvoie une valeur compatible avec le widget à partir d'une valeur d'attribut native

``widgetToValue($varValue, $intItemId)`` |br|
renvoie une valeur compatible avec l'attribut à partir d'une valeur de widget native

``setDataFor($arrValues)`` |br|
enregistre les valeurs selon le schéma « id => value » dans la base de données

``getDefaultRenderSettings()`` |br|
renvoie l'instance des paramètres de rendu par défaut de l'attribut

``parseValue($arrRowData, $strOutputFormat = 'text', $objSettings = null)`` |br|
renvoie les données converties selon le format de sortie donné

``getFilterUrlValue($varValue)`` |br|
renvoie les valeurs d'attribut après utilisation d'une URL de filtre

``sortIds($strListIds, $strDirection)`` |br|
renvoie un tableau d'ID triés selon le sens de tri ("ASC|DESC")

``getFilterOptions($strListIds, $usedOnly, &$arrCount = null)`` |br|
renvoie les attributs selon le schéma « id => value »

``searchFor($strPattern)`` |br|
renvoie tous les items correspondant à un motif de recherche (par exemple joker * ou ? pour une lettre)

``filterGreaterThan($varValue, $blnInclusive = false)`` |br|
renvoie une liste d'ID d'items supérieurs à la valeur donnée ;
si l'option « Inclusive » est définie, l'item est inclus dans la
liste en cas d'égalité

``filterLessThan($varValue, $blnInclusive = false)`` |br|
renvoie une liste d'ID d'items inférieurs à la valeur donnée ;
si l'option « Inclusive » est définie, l'item est inclus dans la
liste en cas d'égalité

``filterNotEqual($varValue)`` |br|
renvoie une liste d'ID d'items égaux à la valeur donnée

``modelSaved($objItem)`` |br|
est appelé lorsqu'un item donné est enregistré


.. _ref_api_interf_attribute_isimple:

Interface ISimple
...................

L'interface ISimple est destinée à tous les attributs « simples »
pouvant être déterminés via la méthode simple « SELECT colName FROM mm_table ».

Informations actuelles sur : `ISimple <https://github.com/MetaModels/core/blob/master/src/Attribute/ISimple.php>`_

**Interfaces :**

``getSQLDataType`` |br|
renvoie la déclaration de type SQL, par exemple "text NULL"

``createColumn()`` |br|
crée la structure de base de données de base pour un attribut donné

``deleteColumn()`` |br|
supprime la structure de base de données de base pour un attribut donné

``renameColumn($strNewColumnName)`` |br|
renomme la structure de base de données de base pour un attribut donné ;
attention : les données existantes dans la base de données sont alors supprimées

``unserializeData($strValue)`` |br|
renvoie les données brutes de la base de données désérialisées

``serializeData($strValue)`` |br|
renvoie les données sérialisées pour la base de données


.. _ref_api_interf_attribute_icomplex:

Interface IComplex
....................

L'interface IComplex est destinée à tous les attributs « complexes »
qui ne peuvent pas être déterminés via la méthode simple « SELECT colName FROM mm_table ».

Informations actuelles sur : `IComplex <https://github.com/MetaModels/core/blob/master/src/Attribute/IComplex.php>`_

**Interfaces :**

``getDataFor($arrIds)`` |br|
renvoie, pour les ID transmis, les valeurs sous forme de « id => 'native data' »,
où les « données natives » dépendent du type d'attribut respectif

``unsetDataFor($arrIds)`` |br|
supprime les valeurs des attributs pour le tableau d'ID transmis


.. _ref_api_interf_attribute_itranslated:

Interface ITranslated
.......................

L'interface ITranslated est destinée à tous les attributs traduits.

Informations actuelles sur : `ITranslated <https://github.com/MetaModels/core/blob/master/src/Attribute/ITranslated.php>`_

**Interfaces :**

``searchForInLanguages($strPattern, $arrLanguages = array())`` |br|
renvoie les ID des items trouvés selon le motif de recherche indiqué (jokers inclus)
et le tableau optionnel de langues

``setTranslatedDataFor($arrValues, $strLangCode)`` |br|
définit la valeur d'un item dans la langue correspondante

``getTranslatedDataFor($arrIds, $strLangCode)`` |br|
renvoie un tableau des valeurs pour les items du tableau d'ID dans la langue
correspondante

``unsetValueFor($arrIds, $strLangCode)`` |br|
supprime les valeurs du tableau d'ID d'items dans la langue correspondante

.. |br| raw:: html

   <br />
