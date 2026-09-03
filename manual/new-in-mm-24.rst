.. _new_in_mm240:

Modifications et fonctionnalités de MM 2.4
==========================================

Vous trouverez ci-dessous un aperçu des modifications et fonctionnalités de MetaModels 2.4, rendues possibles grâce
au « programme early adopter » - pour en savoir plus sur le financement, voir la rubrique Fundraising sur le
`site web de MM <https://now.metamodel.me/de/unterstuetzer/fundraising#metamodels_2-4>`_.

Pour une vérification après une mise à niveau vers MM 2.4, voir :ref:`plus d'indications ci-dessous
<check_upgrade_mm240>`.

.. note:: Pour créer les tables mm_* et les colonnes des attributs, une migration de base de données doit être
   exécutée - voir :ref:`Gestionnaire de schéma <component_schema-manager>`. |br|
   Après avoir créé ou modifié les libellés des MetaModels, des Attributs ou des légendes, veuillez vider le cache
   (de traduction) - voir :ref:`component_translations`.


Généralités et Core
-------------------

Avec Contao 5 entre en jeu une nouvelle version de Symfony et nous avons relevé la version minimale de PHP à 8.2.
Dans Contao 5, le changement le plus visible est le backend légèrement modifié, avec toute sa largeur et de
nouvelles icônes. Les nouvelles `indications de largeur d'un widget
<https://docs.contao.org/dev/reference/dca/palettes/#arranging-fields>`_ dans le masque de saisie, comme « w25 » ou
« w66 », peuvent bien sûr aussi être utilisées dans MM. MetaModels prend en charge le « design sombre » (mode
sombre) du backend, y compris des variantes d'icônes avec le suffixe « --dark ».

Pour vos propres adaptations ou développements, plusieurs points doivent être pris en compte, qui ont changé dans
Contao, comme par exemple les dépréciations (Deprecations) de `C 4.13
<https://github.com/contao/contao/blob/4.13/DEPRECATED.md>`_ et de `C 5
<https://github.com/contao/contao/blob/5.x/DEPRECATED.md>`_, les chemins absolus pour les fichiers comme les icônes
ou les CSS/JS, ou encore les indications complètes lors de l'appel de méthodes, par exemple
``\Contao\Input::get('myvariable')``.

Pour les tailles d'image, certains préréglages standards comme « Centre-centre » n'existent plus - définissez à la
place vos propres tailles d'image et adaptez-les par exemple au niveau des réglages de rendu.

Les liens dans le CE et le module vers MetaModel, Filter, etc. s'ouvrent désormais dans un onglet séparé du
navigateur.

Le noyau MM (MM-Core) prend désormais en charge un
"`route_prefix <https://docs.contao.org/5.x/manual/de/system/einstellungen/#zus%C3%A4tzliche-backend-einstellungen>`_"
individuel, permettant d'appeler le backend avec par exemple ``admin/`` au lieu de ``contao/``.

Pour les sorties frontend, la prise en charge de la Content Security Policy (CSP) a été intégrée afin de sécuriser
les scripts JavaScript et les styles en ligne (inline styles) - `plus d'informations dans la newsletter de
novembre 2025 <https://now.metamodel.me/de/mm-eap-newsletter-2-4/details/eap-info-mm-2-4-november-i-2025>`_

Pour TinyMCE, il est possible de configurer un sélecteur de lien (Link-Picker) sur les pages de détail - voir
:ref:`rst_cookbook_specials_picker-for-tinymce`.

Pour la recherche des fichiers utilisés, l'extension « Contao File Usage » est prise en charge - voir
:ref:`rst_extended_file-usage`.


Multilinguisme
--------------

Avec MM 2.4, certains principes de conception liés au multilinguisme ont été appliqués de façon plus cohérente,
voire corrigés - :ref:`plus d'informations ici sur la structure du multilinguisme dans MetaModels
<component_multi-language>`

Parmi les adaptations figure la sortie stricte des contenus de la langue de repli, lorsque la langue à traduire ne
possède pas de contenu propre - cela s'applique par exemple aussi aux attributs Fichier et Contenu d'un article.

Ce comportement peut être désactivé via l'option « Désactiver le mode de repli » - cette option est par exemple
disponible pour l'attribut :ref:`Case à cocher traduite <component_attribute_translatedcheckbox>`. Cela signifie
qu'une valeur est enregistrée pour une langue même si elle est identique à la valeur de repli.

Lorsque des enregistrements multilingues sont copiés, toutes les autres langues sont désormais copiées en plus de
la langue de repli.

L'affichage dans le backend indiquant quelle langue est la langue de repli a été amélioré. Lorsqu'on passe, dans le
masque de saisie, de la langue de repli à la langue à traduire, il est désormais indiqué au niveau des attributs
quel contenu est affiché - à savoir |img_fallback| ou |img_translated|.

Pour les traductions, un :ref:`outil de traduction pour DeepL & Co.
<rst_extended_translator-bridge>` est venu s'ajouter à l' :ref:`export/import XLIFF <rst_extended_xliff_ex-import>`.


Attributs
---------

* Case à cocher
    * Prise en charge du mode sombre pour les icônes - pour cela, créer un fichier d'icône supplémentaire avec le
      suffixe « --dark »
    * Template ``mm_attr_checkbox_icon.html5`` pour l'affichage dans le backend sous forme de ☑ ou ☐ dans la vue en
      liste
* Marqueur Cowegis (NOUVEAU)
    * Sélection de marqueurs dans Cowegis pour l'affichage sur une carte -
      :ref:`voir « Intégration de la couche Cowegis pour les marqueurs » <extended_cowegis-layer-marker>`
* Fichier
    * Adaptation des templates pour la sortie de `title`, `alt`, `caption` à partir du nœud `metafile`
    * deux nouveaux templates : ``mm_attr_file_contao_image.html5`` pour la sortie standard comme dans Contao, ce
      qui inclut également la sortie des données JSON-LD, ainsi que ``mm_attr_file_contao_image_ofpage.html5`` pour
      la sortie standard comme dans Contao, où la première image est en plus fournie comme ``primaryImageOfPage`` ;
      voir aussi :ref:`Adaptations SEO <rst_cookbook_tips_seo_structured-data>`
* Sélection simple [select]
    * Prise en charge de l'utilisation avec un widget popup dans une table enfant
* Contenu d'un article
    * Prise en charge de l'utilisation dans une table enfant
    * Modification des templates - transmission d'un tableau d'objets Content
* Valeurs combinées
    * Option « Toujours enregistrer » (alwaysSave) activée - enregistre même sans modification de valeur
* Pays
    * Passage des codes pays en majuscules
* Texte long
    * Migration pour `basicEntities` - `voir le manuel Contao
      <https://docs.contao.org/manual/de/artikelverwaltung/insert-tags/#basic-entities>`_
* Sélection multiple [tags]
    * Prise en charge de l'utilisation dans une table enfant
* Tableau multiple (MCW)
    * Prise en charge de ``'inputType' => 'fileTree'`` avec ``'multiple' => 'true'``, y compris le déplacement de
      fichiers
* Texte
    * Migration pour `basicEntities` - `voir le manuel Contao
      <https://docs.contao.org/manual/de/artikelverwaltung/insert-tags/#basic-entities>`_
* Token (NOUVEAU)
    * génère, lors du premier enregistrement d'un enregistrement, une chaîne de caractères aléatoire d'un point de
      vue cryptographique et immuable (Token) - voir :ref:`component_attribute_token`
* Alias traduit
    * Colonne ``langcode`` en ``varchar(64)``
* Case à cocher traduite
    * Prise en charge du mode sombre pour les icônes - pour cela, créer un fichier d'icône supplémentaire avec le
      suffixe « --dark »
    * Template ``mm_attr_translatedcheckbox_icon.html5`` pour l'affichage dans le backend sous forme de ☑ ou ☐ dans
      la vue en liste
    * Colonne ``langcode`` en ``varchar(64)``
    * Option « Désactiver le mode de repli » pour enregistrer une valeur pour une langue, même si elle est identique
      à la valeur de repli
* Fichier traduit
    * Adaptation des templates pour la sortie de `title`, `alt`, `caption` à partir du nœud `metafile`
    * deux nouveaux templates : ``mm_attr_file_contao_image.html5`` pour la sortie standard comme dans Contao, ce
      qui inclut également la sortie des données JSON-LD, ainsi que ``mm_attr_file_contao_image_ofpage.html5`` pour
      la sortie standard comme dans Contao, où la première image est en plus fournie comme ``primaryImageOfPage`` ;
      voir aussi :ref:`Adaptations SEO <rst_cookbook_tips_seo_structured-data>`
    * Colonne ``langcode`` en ``varchar(64)``
* Contenu d'un article traduit
    * Prise en charge de l'utilisation dans une table enfant
    * Colonne ``mm_lang`` en ``varchar(64)``
    * Modification des templates - transmission d'un tableau d'objets Content
* Valeurs combinées traduites
    * Option « Toujours enregistrer » (alwaysSave) activée - enregistre même sans modification de valeur
* Texte long traduit
    * Migration pour `basicEntities` - `voir le manuel Contao
      <https://docs.contao.org/manual/de/artikelverwaltung/insert-tags/#basic-entities>`_
    * Colonne ``langcode`` en ``varchar(64)``
* Tableau multiple traduit (MCW)
    * Prise en charge de ``'inputType' => 'fileTree'`` avec ``'multiple' => 'true'``, y compris le déplacement de
      fichiers
    * Colonne ``langcode`` en ``varchar(64)``
* Tableau-texte traduit
    * Colonne ``langcode`` en ``varchar(64)``
* Texte traduit
    * Migration pour `basicEntities` - `voir le manuel Contao
      <https://docs.contao.org/manual/de/artikelverwaltung/insert-tags/#basic-entities>`_
    * Colonne ``langcode`` en ``varchar(64)``
* URL traduite
    * Nom de colonne changé de ``language`` à ``langcode`` - migration disponible
    * Colonne ``langcode`` en ``varchar(64)``


Filtres
-------

Toutes les règles de filtre qui génèrent une URL disposent désormais d'un nouveau réglage (« Type d'URL pour le
paramètre ») déterminant si les paramètres doivent apparaître dans l'URL sous forme de slug ou de paramètre GET.
Pour des raisons de rétrocompatibilité, ce réglage est positionné sur « Slug ou GET » après une mise à niveau - ce
réglage est déprécié et devrait être défini, pour chaque règle de filtre concernée, soit sur Slug, SOIT sur GET.
Plus d'informations dans les :ref:`conseils SEO <rst_cookbook_tips_seo_filter-url>`

* Requête simple
    * si l'option « Paramètre statique » est activée, une valeur peut être sélectionnée comme préréglage pour la
      règle de filtre, aussi bien dans le CE/module « Liste MM » que dans « Filtre MM » - voir
      `Ticket #345 <https://github.com/MetaModels/core/issues/345>`_
* Règle Expression (Nouveau)
    * Avec la règle de filtre « Expression », l'exécution d'autres règles de filtre peut être liée à des conditions
      - voir :rel:`rst_cookbook_filter_expression-rule`
* Filter-by-related
    * :ref:`remplace le filtre « Filter-Parent » <rst_extended_filter_by_related>`
    * cette règle de filtre permet de filtrer les éléments (Items) selon les propriétés d'un MetaModel lié
      (relation). Comme relation, une sélection simple (Select) ou une table enfant sont possibles.
* Recherche par périmètre (Perimeterseach)
    * les fournisseurs de cartes ``GoogleMaps`` et ``OpenStreetMaps`` nécessitent, lors de l'appel, un
      ``HttpClientInterface`` comme paramètre
* Valeur de/à pour un attribut (from-to)
    * les valeurs min. et max. sont disponibles dans le template sous ``optionsMin`` et ``optionsMax``
    * nouveau template pour le type ``date`` : ``mm_filteritem_datepicker.html5``
* Valeur de/à pour deux attributs (range)
    * les valeurs min. et max. sont disponibles dans le template sous ``optionsMin`` et ``optionsMax``
    * nouveau template pour le type ``date`` : ``mm_filteritem_datepicker.html5``
* Recherche en texte intégral avec « Loupe »
    * Cette nouvelle règle de filtre crée un index sur les attributs sélectionnés, dans lequel il est ensuite
      possible de faire des recherches - voir :ref:`Loupe <rst_extended_loupe>`
* Règle Expression** (Nouveau)
    * elle permet de lier l'exécution d'autres règles de filtre à des conditions ; plus d'informations à ce sujet
      dans la :ref:`règle de filtre Expression <rst_cookbook_filter_expression-rule>`


Édition frontend (FEE)
----------------------

* Renommage du template `form_textfield_multiple` en `form_text_multiple` dans « FormTextFieldMultipleBundle »
  (alignement avec Contao 5)
* dans les réglages du masque de saisie pour un upload de fichier, selon que l'option « Édition multiple » est
  activée ou non, seuls les réglages adaptés à l'upload simple ou multiple sont désormais affichés dans les modes de
  widget - en cas de changement au niveau de l'attribut, l'upload doit toutefois être adapté en conséquence
* l'adaptation du répertoire cible ou du nom de fichier via l'insert-tag ``{{post::<attribute-spaltenname>}}`` n'est
  plus possible, ce tag n'existant plus dans Contao 5 - un Simple-Token peut désormais être utilisé à la place, sous
  la forme ``##post::<attribute-spaltenname>##`` - :ref:`voir FEE <extended_frontend_editing_upload>`
* prise en charge des MetaModels multilingues - le masque FE dispose désormais d'un sélecteur de langue comme dans
  le BE ; voir :ref:`FEE <extended_frontend_editing_multilanguage>`
* possibilité de choisir les templates de formulaire pour le masque de saisie (FEE) pour tous les attributs traduits
* prise en charge de la Content Security Policy (CSP)


Problèmes connus
----------------

* lors du basculement vers/depuis le mode débogage dans le BE via le bouton, la page de référence n'est plus
  correcte et il faut y accéder à nouveau - par exemple avec « retour » dans le navigateur et rechargement de la
  page |br|
  Contao n'offre actuellement aucun moyen d'influencer le referer à cet endroit


.. _check_upgrade_mm240:
Vérifications pour la mise à niveau vers MM 2.4
-----------------------------------------------

En principe, une mise à niveau au sein de la branche MM 2.x est possible sans problème, et les adaptations
nécessaires aux libellés ainsi qu'aux modifications de base de données sont prises en charge par les migrations.
Il y a toutefois quelques éléments qui ne peuvent pas être pris en charge de cette manière, ou seulement très
difficilement. C'est pourquoi, lors du passage à MM 2.4, les points suivants doivent être gardés à l'esprit :

* veuillez suivre toutes les indications de :ref:`MM 2.3 <check_upgrade_mm230>` et :ref:`MM 2.2
  <check_upgrade_mm220>`
* modification des templates du DC_General
* renommage du template `form_textfield_multiple` en `form_text_multiple` dans « FormTextFieldMultipleBundle » (FEE)
* modification des templates pour Fichier et Fichier traduit pour la sortie des métadonnées
* vérifier ses propres développements par rapport à Contao 5 (voir ci-dessus)
* pour le FEE avec upload de fichier, vérifier le mode de widget dans les réglages de l'attribut dans le masque de
  saisie (voir ci-dessus)
* pour le FEE et l'upload de fichier : vérifier si l'insert-tag ``{{post::*}}`` a été utilisé et l'adapter (voir
  ci-dessus)
* pour le FEE et le lien de suppression d'un item, tenir compte des changements dus à la prise en charge du CSP et
  adapter le CSS si nécessaire (voir ci-dessus)
* pour le mode sombre, créer le cas échéant d'autres variantes de ses propres icônes avec le suffixe « --dark » -
  par exemple, à partir de `flag_enabled.svg` et `flag_disabled.svg`, créer `flag_enabled--dark.svg` et
  `flag_disabled--dark.svg` - voir
  `EAP-News octobre II 2024 <https://now.metamodel.me/de/mm-eap-newsletter-2-4/details/eap-info-mm-2-4-oktober-ii-2024>`_
* pour l'attribut Pays, l'écriture des codes pays a été changée en majuscules comme dans Contao - les données
  existantes sont adaptées via une migration ; adapter le cas échéant ses propres vérifications ou enregistrements
* pour l'attribut URL traduite, le nom de la colonne pour le code de langue a été changé en ``langcode`` - adapter
  le cas échéant ses propres requêtes SQL ou sorties de template
* vérifier la sélection des tailles d'image - certains préréglages standards comme « Centre-centre » n'existent plus
* si l'option « Paramètre statique » est définie dans une règle de filtre, vérifier alors dans « Liste MM » la
  valeur par défaut de « Valeur de filtre pour l'attribut » - si aucun item n'est affiché dans la liste, la mettre
  sur « sans valeur de donnée [null] »
* pour ses propres requêtes de recherche par périmètre ou de détermination des coordonnées géographiques, transmettre
  un ``HttpClientInterface`` comme paramètre au fournisseur de cartes
* pour les règles de filtre, vérifier le réglage « Type d'URL pour le paramètre » et le régler sur Slug OU GET
* nouveaux templates pour Contenu d'un article (également multilingue) avec transmission d'un tableau d'objets
  Content
* sortie des contenus de la langue de repli lorsqu'aucun contenu traduit n'est disponible
* pour Case à cocher traduite, définir l'option « Désactiver le mode de repli » (réglages de l'attribut) pour
  conserver les filtrages existants - pour déterminer les attributs concernés :

.. code-block:: sql
   :linenos:

   SELECT mm.name AS metamodel, a.colname
   FROM `tl_metamodel_attribute` AS a
   JOIN `tl_metamodel` AS mm ON mm.id = a.pid
   WHERE a.type = 'translatedcheckbox'
   ORDER BY mm.name, a.colname;



Refinancement
-------------
.. seealso:: Pour un refinancement des travaux importants réalisés, l'équipe MM sollicite un soutien financier.
   Comme ordre de grandeur, il convient de se baser sur l'ampleur du projet à réaliser et de prévoir environ 10 %
   de son montant - d'après l'expérience des derniers soutiens reçus, il s'agit de montants compris entre 100 € et
   500 € (net) - une facture incluant la TVA est bien entendu toujours établie. `En savoir plus...
   <https://now.metamodel.me/de/unterstuetzer/spenden>`_


.. |img_fallback| image:: /_img/icons/fallback.png
.. |img_translated| image:: /_img/icons/translated.png

.. |br| raw:: html

   <br />
