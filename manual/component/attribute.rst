.. _component_attribute:

|svg_fields_32| |img_fields_32| Attributs
============================================

.. note:: créer ses propres colonnes de la table de base de données sous forme d'attributs et les
   configurer |br|
   Pour créer les colonnes d'attribut dans la table mm_*, effectuer une migration de base de
   données - :ref:`voir Gestionnaire de schéma <component_schema-manager>`


Introduction
------------

Le composant « Attributs » est l'un des réglages les plus fondamentaux d'un MetaModel. Les
attributs permettent de définir les champs de données propres et spécifiques et de les créer sous
forme de colonnes dans la table de base de données. La page :ref:`component_data-in-attributes`
indique quel attribut peut être utilisé pour quel type de donnée de la base de données. Outre les
types de données habituels comme ``varchar``, ``int``, ``text``, etc., il existe également des
attributs pour des stockages spéciaux - pour en savoir plus, voir la liste suivante.

Lors de la création d'un attribut « |img_new| Nouvel attribut », les champs obligatoires sont le
choix du type d'attribut ainsi que la saisie du nom de colonne - le nom de colonne définit, comme
son nom l'indique, la désignation de la colonne dans la table de base de données. En saisies
supplémentaires, un nom et une description peuvent être renseignés, qui apparaîtront également
comme désignation et description dans le masque de saisie.

.. warning:: Lors de la modification du type d'attribut, tout comme lors de la suppression de
  l'attribut, les valeurs saisies jusque-là sont supprimées de la base de données ! Si un type
  d'attribut doit néanmoins être modifié en conservant les valeurs, cela devrait être accompagné
  directement au niveau de la base de données, par ex. via un export/import de la colonne
  d'attribut au format CSV. Un attribut modifié devrait ensuite être à nouveau ajouté dans les
  réglages de rendu et les masques de saisie.

.. seealso:: Liste de contrôle pour la modification d'un type d'attribut :
  :ref:`rst_cookbook_checklists_attribut_change`

Selon le type d'attribut, d'autres possibilités de saisie ou options sont disponibles après un
rechargement de la page. Voici une liste des types d'attribut avec des indications sur les options
spécifiques :

* **Alias** : champ alias, par ex. pour les paramètres URL lors du filtrage |br|
  l'alias peut être créé comme combinaison de différents attributs (existants) ; en option, la
  régénération de l'alias peut être forcée lors de modifications des attributs d'origine (forcer la
  régénération de l'alias) ; un alias n'est pas automatiquement créé comme valeur unique - cela
  nécessite l'activation de la case « Valeurs uniques » - :ref:`plus... <component_attribute_alias>`
* **Case à cocher (Checkbox)** : case à cocher unique pour les valeurs booléennes |br|
  la case à cocher permet de définir des valeurs booléennes (0|1) ; une variante spéciale est la
  « Publication » - avec elle, une icône « œil » apparaît dans le backend, le filtrage pour la
  publication elle-même devant être créé séparément ; le nom de colonne généralement utilisé pour
  la valeur de publication est « published » ; via l'option « Case à cocher en vue liste », une
  icône personnalisée peut être utilisée dans le backend pour afficher le statut -
  :ref:`plus... <component_attribute_checkbox>`
* **Entrées combinées** : combinaison de différents attributs |br|
  tous les attributs existants ainsi que les « attributs système » comme ID, PID, etc. peuvent être
  combinés en un nouvel attribut ; la combinaison s'effectue via un formatage sprintf ; par ex., les
  deux attributs « Nom » et « Prénom » peuvent être combinés via l'instruction « %s, %s » en
  « Nom, Prénom » ; l'option « Forcer l'actualisation » impose la régénération lors de modifications
  des valeurs - :ref:`plus... <component_attribute_combinedvalues>`
* **Pays** : sélection de pays |br|
  cet attribut propose une sélection de pays ; la sélection des pays peut être restreinte avec
  l'option « Filtrer les pays disponibles » - :ref:`plus... <component_attribute_country>`
* **Décimal** : nombres décimaux |br|
  cet attribut est destiné au stockage de nombres décimaux comme des montants monétaires ; il y a
  deux décimales - :ref:`plus... <component_attribute_decimal>`
* **Fichier** : sélecteur de fichier |br|
  l'attribut « Fichier » propose un sélecteur de fichier pour choisir un fichier, ou plusieurs
  fichiers si l'option « Sélection multiple » est activée ; l'option « Personnaliser l'arborescence
  de fichiers » permet de définir d'autres options de fichier pendant la sélection ; pour une
  utilisation avec des images, il faut noter que, pour un affichage (direct) de vignettes dans le
  backend ou le frontend, l'option « Utiliser comme champ image avec vignette » doit être activée
  dans les réglages de rendu de l'attribut fichier - :ref:`plus... <component_attribute_file>`
* **Texte long** : saisie de texte |br|
  attribut pour des saisies de texte plus longues - :ref:`plus... <component_attribute_longtext>`
* **Numérique** : saisie de valeurs entières (Integer) - :ref:`plus... <component_attribute_numeric>`
* **Sélection simple [select]** : relation (1:n) vers une autre table de MetaModels ou de Contao |br|
  l'attribut « Sélection » crée une relation 1:n vers une autre table ; il peut s'agir aussi bien
  d'une table MetaModels que de toute autre table de Contao, par ex. tl_member -
  :ref:`plus... <component_attribute_select>`
* **Tableau de texte** : saisie de valeurs sous forme de tableau |br|
  l'attribut « Tableau de texte » définit un nombre de colonnes, y compris leur désignation et leur
  largeur ; dans le masque de saisie, un nombre quelconque de lignes peut ensuite être créé, par ex.
  pour enregistrer plusieurs URL ou numéros de téléphone - :ref:`plus... <component_attribute_tabletext>`
* **Sélection multiple [tags]** : relation (m:n) vers une autre table de MetaModels ou de Contao |br|
  l'attribut « Sélection » crée une relation m:n vers une autre table ; il peut s'agir aussi bien
  d'une table MetaModels que de toute autre table de Contao, par ex. tl_page ; la résolution de la
  relation s'effectue dans une table spéciale de MetaModels, de sorte qu'aucune colonne n'est créée
  dans la table MetaModel pour cet attribut - :ref:`plus... <component_attribute_tags>`
* **Texte** : champ de texte simple - :ref:`plus... <component_attribute_text>`
* **Date** : date, ou date et heure |br|
  les données sont stockées sous forme d'horodatage Unix ; pour des filtrages SQL personnalisés,
  des conversions peuvent le cas échéant être nécessaires - :ref:`plus... <component_attribute_timestamp>`
* **URL** : texte de lien et URL |br|
  saisie de liens externes (y compris en saisissant « \http:// ») ou de liens internes via le
  sélecteur de page ; en option, « Supprimer le titre » permet de n'afficher que l'URL -
  :ref:`plus... <component_attribute_url>`

Si l'option « Traduction » est activée dans le MetaModel, les attributs suivants sont en outre
disponibles pour un usage multilingue :

* Case à cocher traduite - :ref:`plus... <component_attribute_translatedcheckbox>`
* Entrées combinées traduites - :ref:`plus... <component_attribute_translatedcombinedvalues>`
* Fichier traduit - :ref:`plus... <component_attribute_translatedfile>`
* Texte long traduit - :ref:`plus... <component_attribute_translatedlongtext>`
* Sélection simple traduite - :ref:`plus... <component_attribute_translatedselect>`
* Tableau de texte traduit - :ref:`plus... <component_attribute_translatedtabletext>`
* Sélection multiple traduite - :ref:`plus... <component_attribute_translatedtags>`
* Texte traduit - :ref:`plus... <component_attribute_translatedtext>`

Ces attributs se distinguent de leurs équivalents monolingues essentiellement par la saisie des
indications multilingues pour le nom et la description. Pour les attributs traduits, des tables
spéciales de l'extension sont utilisées, et non la table générée lors de la création du MetaModel.

Il faut noter que, pour des relations via « Sélection simple » ou « Sélection multiple » entre deux
MetaModels avec traductions, il ne faut généralement *pas* choisir les options « Sélection simple
traduite [select] » et « Sélection multiple traduite [tags] ». La détection ou le basculement de la
langue est effectué automatiquement par MetaModels avec les attributs « Sélection simple » et
« Sélection multiple ».

Les deux « variantes traduites » sont principalement destinées à la connexion de tables qui
n'appartiennent pas à MetaModels et possèdent leur propre champ pour la variante linguistique - ou
pour le cas particulier où, dans le MetaModel référencé, des Items différents doivent être
sélectionnés selon la langue. Pour en savoir plus, voir une page spéciale sur le multilinguisme -
sponsors recherchés pour cela !

Outre les attributs listés, d'autres types d'attribut peuvent être proposés via des extensions
supplémentaires de MetaModels. Les attributs sont installés via Composer ou, comme des extensions
Contao classiques, par copie dans le dossier « modules » (selon la mise à disposition par le
développeur).

Voici des exemples d'attributs supplémentaires :

* **Évaluation** : module d'évaluation avec des étoiles |br|
  ce module d'attribut sert à afficher une « évaluation par étoiles » en frontend ; dans le
  backend, différentes options comme le nombre d'étoiles peuvent être réglées -
  :ref:`plus... <component_attribute_rating>`
* **Sélecteur de couleur** : sélection de couleurs web et de transparence -
  :ref:`plus... <component_attribute_color>`
* **Levenshtein** : recherche de mots selon Levenshtein |br|
  cet attribut détermine une similarité de mots pour une recherche flexible -
  :ref:`plus... <component_attribute_levenshtein>`
* **Sélection de pays** : liste de sélection avec des pays - :ref:`plus... <component_attribute_country>`
* **Clé de langue** : sélection de codes de langue ISO |br|
  cet attribut propose une sélection de codes de langue ; les codes de langue peuvent être
  sélectionnés via une case à cocher - :ref:`plus... <component_attribute_langcode>`
* **ContentArticle** : possibilité de créer des éléments de contenu Contao, comme dans un |br|
  article, dans un widget - :ref:`plus... <component_attribute_contentarticle>` |br|
  existe également en variante traduite - :ref:`plus... <component_attribute_translatedcontentarticle>`
* **Tableau multi** : similaire à l'attribut « Tableau de texte », à ceci près que dans chaque |br|
  « cellule » un type de widget propre comme Select, boutons radio, cases à cocher, etc. peut être
  intégré - :ref:`plus... <component_attribute_tablemulti>` |br|
  existe également en variante traduite - :ref:`plus... <component_attribute_translatedtablemulti>`
* **Distance géographique** : calcule, lors d'une recherche par périmètre, la distance |br|
  géographique par rapport au point de recherche ; cette valeur permet de trier les listes selon la
  distance - :ref:`plus... <component_attribute_geodistance>`
* **LatLong** (à partir de MM 2.5) : paire de coordonnées (latitude/longitude) sous forme de |br|
  ``POINT`` natif dans une colonne, en option avec un index spatial pour une recherche par périmètre
  plus rapide ; saisie au choix via une recherche d'adresse avec carte -
  :ref:`plus... <component_attribute_latlong>`
* **Token** (à partir de MM 2.4) : chaîne de caractères unique |br|
  création de chaînes de caractères uniques qui ne changent plus ensuite -
  :ref:`plus... <component_attribute_token>`

L'ordre dans lequel les attributs sont créés est libre - seuls les attributs qui se réfèrent à
d'autres attributs, comme par ex. « Alias » ou « Entrées combinées », gagnent à être créés après
coup.

Pour les attributs « Sélection simple » et « Sélection multiple », les MetaModels référencés
doivent en outre déjà être créés.


Options
-------

Deux options sont disponibles pour tous les attributs : « Écraser les variantes » et « Valeurs
uniques ».

Avec « Écraser les variantes », l'attribut est également disponible dans les masques de saisie de
la saisie de variantes. Cela suppose que l'option « Variantes » soit activée pour le MetaModel -
sinon la case est inactive.

Avec l'option « Valeurs uniques », les saisies de l'attribut sont vérifiées pour leur unicité
(unique).


Déroulement
-----------

Un nouvel attribut s'ouvre via « |img_new| Nouvel attribut ». Une fois toutes les options
nécessaires renseignées ou sélectionnées, le réglage est enregistré et apparaît dans la liste des
attributs des MetaModels existants. L'ordre dans la liste n'a pas d'autre influence.
Effectuer la migration de base de données !

.. seealso:: Dans le livre de recettes :

   * :ref:`rst_cookbook_checklists_attribut_new`
   * :ref:`rst_cookbook_tips_speedup_backend`


Détails de tous les attributs
--------------------------------

.. toctree::
   :maxdepth: 1

   attribute/alias
   attribute/checkbox
   attribute/combinedvalues
   attribute/decimal
   attribute/file
   attribute/longtext
   attribute/numeric
   attribute/select
   attribute/tabletext
   attribute/tags
   attribute/text
   attribute/timestamp
   attribute/url
   attribute/translatedalias
   attribute/translatedcheckbox
   attribute/translatedcombinedvalues
   attribute/translatedfile
   attribute/translatedlongtext
   attribute/translatedselect
   attribute/translatedtabletext
   attribute/translatedtags
   attribute/translatedtext
   attribute/translatedurl
   attribute/rating
   attribute/color
   attribute/levenshtein
   attribute/country
   attribute/langcode
   attribute/contentarticle
   attribute/translatedcontentarticle
   attribute/tablemulti
   attribute/translatedtablemulti
   attribute/geodistance
   attribute/latlong
   attribute/token


.. |svg_fields_32| image:: /_img/icons_svg/fields.svg
   :width: 32px
.. |img_fields_32| image:: /_img/icons/fields_32.png
.. |img_fields| image:: /_img/icons/fields.png
.. |img_new| image:: /_img/icons/new.gif

.. |br| raw:: html

   <br />

.. |nbsp| unicode:: 0xA0
   :trim:
