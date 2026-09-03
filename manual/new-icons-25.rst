.. _manual_new_icons-25:

Nouvelles icônes SVG pour MetaModels
====================================

Toutes les icônes du backend sont passées du **PNG au SVG**. Elles restent ainsi nettes dans
toutes les tailles - même en cas d'affichage agrandi dans le navigateur ou sur des écrans à
haute résolution.

.. seealso:: Si les icônes du backend vous semblent globalement trop petites, vous pouvez les
   agrandir dans votre propre profil utilisateur grâce à l'extension
   `contao-backend-size-bundle <https://github.com/e-spin/contao-backend-size-bundle>`_ - le
   réglage s'applique par utilisateur, pas pour toute l'installation. Cette extension **ne
   fait pas** partie de MetaModels et peut être utilisée indépendamment ; grâce au passage au
   SVG, les icônes de MetaModels restent toutefois nettes.


Ce qui a également changé
-------------------------

**Couleur selon le domaine.** Les symboles du niveau de structure sont colorés, de sorte que
les domaines du backend se distinguent en un coup d'œil : le MetaModel et ses masques de saisie
en ocre, les attributs en bleu, les filtres en rouge, les vues en vert. Les icônes des
différents types d'attribut, de filtre et de condition restent volontairement d'un gris foncé
neutre - elles représentent le contenu, pas le domaine.

Les couleurs choisies le sont de manière à s'intégrer au schéma de couleurs de Contao, à être
distinguables entre elles, à fonctionner autant que possible aussi bien en mode clair qu'en mode
sombre, et à rester distinguables même en cas de daltonisme rouge-vert.

**Variante propre pour le mode sombre.** Chaque icône dispose d'un fichier portant le suffixe
``--dark``. Contao le sélectionne lui-même lorsque le backend fonctionne avec le schéma de
couleurs sombre ; aucun réglage n'est donc nécessaire.

**Variante estompée pour « désactivé ».** Le fichier portant le suffixe ``_1`` est la version
grisée. MetaModels l'utilise partout où quelque chose est certes configuré mais pas actif -
une règle de filtre désactivée, une condition désactivée, un MetaModel non traduit.

Les tableaux suivants comparent, pour chaque type, l'ancienne icône à la nouvelle. Un « - »
dans la colonne *Avant* signifie qu'il n'existait auparavant pas d'icône propre pour ce type.

.. note:: Contao intègre les icônes à 16 pixels. Dans les tableaux, elles sont affichées à
   22 pixels - c'est-à-dire telles qu'elles apparaissent avec l'extension mentionnée ci-dessus
   dans un backend agrandi. Cela illustre d'ailleurs précisément la raison de ce changement :
   les anciens PNG sont des images matricielles qui deviennent floues en cas d'agrandissement,
   tandis que les nouveaux SVG restent nets.


Core et structure
-----------------

Les symboles de l'arborescence et des menus - tout ce qui caractérise un MetaModel lui-même,
ses masques de saisie, ses ensembles de filtres et ses vues.

.. list-table::
   :header-rows: 1
   :widths: 44 9 9 38

   * - Signification
     - Avant
     - Nouveau
     - Remarque
   * - MetaModels dans le fil d'Ariane
     - |alt_logo_png|
     - |neu_mm_logo_small_svg|
     -
   * - Attributs
     - |alt_fields_png|
     - |neu_fields_svg|
     -
   * - Paramètres de rendu
     - |alt_rendersettings_png|
     - |neu_rendersettings_svg|
     -
   * - Champs d'un paramètre de rendu
     - |alt_rendersetting_png|
     - |neu_rendersetting_svg|
     -
   * - « Tout ajouter » dans le paramètre de rendu
     - |alt_rendersettings_add_png|
     - |neu_rendersettings_add_svg|
     -
   * - Masques de saisie
     - |alt_dca_png|
     - |neu_dca_svg|
     -
   * - Champs d'un masque de saisie
     - |alt_dca_setting_png|
     - |neu_dca_setting_svg|
     -
   * - Condition d'affichage d'un champ
     - |alt_dca_condition_png|
     - |neu_dca_condition_svg|
     -
   * - Groupement et tri
     - |alt_dca_groupsortsettings_png|
     - |neu_dca_groupsortsettings_svg|
     -
   * - « Tout ajouter » dans le masque de saisie
     - |alt_dca_add_png|
     - |neu_dca_add_svg|
     -
   * - Paramètres de recherche
     - |alt_searchable_pages_png|
     - |neu_searchable_pages_svg|
     -
   * - Ensemble de filtres
     - |alt_filter_png|
     - |neu_filter_svg|
     -
   * - Règles de filtre
     - |alt_filter_setting_png|
     - |neu_filter_setting_svg|
     -
   * - Attribution des droits
     - |alt_dca_combine_png|
     - |neu_dca_combine_svg|
     -
   * - Variantes
     - |alt_variants_png|
     - |neu_variants_svg|
     -
   * - MetaModel traduit
     - |alt_locale_png|
     - |neu_locale_svg|
     -
   * - Table enfant sans icône propre
     - |alt_metamodels_png|
     - |neu_child_table_svg|
     - auparavant l'icône par défaut d'un MetaModel, qui ne signifiait rien ici
   * - Icône par défaut d'un MetaModel
     - |alt_metamodels_png|
     - |neu_metamodels_svg|
     - solution de repli, lorsqu'un MetaModel n'a pas défini sa propre icône
   * - Groupe de menu « MetaModels » dans le menu du backend
     - |alt_mm_group_icon_contour_svg|
     - |neu_mm_group_icon_svg|
     - auparavant seulement le contour, désormais rempli


Attributs
---------

Les icônes de type des attributs, telles qu'elles apparaissent dans la liste des attributs et
dans la sélection du type d'attribut.

.. list-table::
   :header-rows: 1
   :widths: 22 30 9 9 30

   * - Type
     - Libellé dans le backend
     - Avant
     - Nouveau
     - Remarque
   * - ``alias``
     - Alias
     - |alt_alias_png|
     - |neu_alias_svg|
     -
   * - ``checkbox``
     - Case à cocher
     - |alt_checkbox_png|
     - |neu_checkbox_svg|
     -
   * - ``color``
     - Sélecteur de couleur
     - |alt_color_png|
     - |neu_color_svg|
     -
   * - ``combinedvalues``
     - Entrées combinées
     - |alt_combinedvalues_png|
     - |neu_combinedvalues_svg|
     -
   * - ``contentarticle``
     - Contenu d'un article
     - |alt_article_png|
     - |neu_article_svg|
     -
   * - ``country``
     - Pays
     - |alt_country_png|
     - |neu_country_svg|
     -
   * - ``decimal``
     - Décimal
     - |alt_decimal_png|
     - |neu_decimal_svg|
     -
   * - ``file``
     - Fichier
     - |alt_file_png|
     - |neu_file_svg|
     -
   * - ``geodistance``
     - Distance géographique
     - |alt_geodistance_png|
     - |neu_geodistance_svg|
     -
   * - ``langcode``
     - Code de langue
     - |alt_langcode_png|
     - |neu_langcode_svg|
     -
   * - ``levenshtein``
     - Recherche assistée par Levenshtein
     - |alt_levenshtein_png|
     - |neu_levenshtein_svg|
     -
   * - ``longtext``
     - Texte long
     - |alt_longtext_png|
     - |neu_longtext_svg|
     -
   * - ``marker_icon``
     - Marqueur Cowegis
     - |alt_marker_png|
     - |neu_marker_svg|
     -
   * - ``numeric``
     - Numérique
     - |alt_numeric_png|
     - |neu_numeric_svg|
     -
   * - ``rating``
     - Évaluation
     - |alt_star_full_png|
     - |neu_star_svg|
     - jusqu'à MM 2.4, la même icône que l'étoile pleine du frontend (``star-full``) ; obtient
       avec 2.5 son propre fichier
   * - ``select``
     - Sélection simple [select]
     - |alt_select_png|
     - |neu_select_svg|
     -
   * - ``tablemulti``
     - Tableau multi (MCW)
     - |alt_tablemulti_png|
     - |neu_tablemulti_svg|
     -
   * - ``tabletext``
     - Tableau de texte
     - |alt_tabletext_png|
     - |neu_tabletext_svg|
     -
   * - ``tags``
     - Sélection multiple [tags]
     - |alt_tags_png|
     - |neu_tags_svg|
     -
   * - ``text``
     - Texte
     - |alt_text_png|
     - |neu_text_svg|
     -
   * - ``timestamp``
     - Date/Heure
     - |alt_timestamp_png|
     - |neu_timestamp_svg|
     -
   * - ``token``
     - Token
     - |alt_token_png|
     - |neu_token_svg|
     -
   * - ``url``
     - URL
     - |alt_url_png|
     - |neu_url_svg|
     -


Attributs traduits
..................

Les attributs traduits utilisent la même icône que leur équivalent non traduit ; seuls
``translatedtablemulti`` et ``translatedtabletext`` ont une icône propre.

.. list-table::
   :header-rows: 1
   :widths: 22 30 9 9 30

   * - Type
     - Libellé dans le backend
     - Avant
     - Nouveau
     - Remarque
   * - ``translatedalias``
     - Alias traduit
     - |alt_alias_png|
     - |neu_alias_svg|
     -
   * - ``translatedcheckbox``
     - Case à cocher traduite
     - |alt_checkbox_png|
     - |neu_checkbox_svg|
     -
   * - ``translatedcombinedvalues``
     - Valeurs combinées traduites
     - |alt_combinedvalues_png|
     - |neu_combinedvalues_svg|
     -
   * - ``translatedcontentarticle``
     - Contenu traduit d'un article
     - |alt_article_png|
     - |neu_article_svg|
     -
   * - ``translatedfile``
     - Fichier traduit
     - |alt_file_png|
     - |neu_file_svg|
     -
   * - ``translatedlongtext``
     - Texte long traduit
     - |alt_longtext_png|
     - |neu_longtext_svg|
     -
   * - ``translatedselect``
     - Sélection simple traduite [select]
     - |alt_select_png|
     - |neu_select_svg|
     -
   * - ``translatedtablemulti``
     - Tableau multi traduit (MCW)
     - |alt_translatedtablemulti_png|
     - |neu_translatedtablemulti_svg|
     - icône propre
   * - ``translatedtabletext``
     - Tableau de texte traduit
     - |alt_translatedtabletext_png|
     - |neu_translatedtabletext_svg|
     - icône propre
   * - ``translatedtags``
     - Sélection multiple traduite [tags]
     - |alt_tags_png|
     - |neu_tags_svg|
     -
   * - ``translatedtext``
     - Texte traduit
     - |alt_text_png|
     - |neu_text_svg|
     -
   * - ``translatedurl``
     - URL traduite
     - |alt_url_png|
     - |neu_url_svg|
     -


Règles de filtre
----------------

Toutes les règles de filtre sélectionnables dans le backend, classées par ordre alphabétique
selon leur type - indépendamment du paquet dont elles proviennent.

.. list-table::
   :header-rows: 1
   :widths: 22 30 9 9 30

   * - Type
     - Libellé dans le backend
     - Avant
     - Nouveau
     - Remarque
   * - ``checkbox``
     - Oui / Non
     - |alt_filter_checkbox_png|
     - |neu_filter_yes_no_svg|
     - le fichier s'appelle désormais ``filter_yes-no``
   * - ``checkbox_published``
     - Statut de case à cocher
     - |alt_visible_png|
     - |neu_filter_checkbox_svg|
     - auparavant l'œil (``visible.png``)
   * - ``conditionand``
     - Condition ET
     - |alt_filter_and_png|
     - |neu_filter_and_svg|
     - du Core
   * - ``conditionor``
     - Condition OU
     - |alt_filter_or_png|
     - |neu_filter_or_svg|
     - du Core
   * - ``customsql``
     - SQL personnalisé
     - |alt_filter_customsql_png|
     - |neu_filter_customsql_svg|
     - du Core
   * - ``expression_rule``
     - Règle d'expression
     - |alt_filter_expression_png|
     - |neu_filter_expression_svg|
     - du Core
   * - ``fromto``
     - Valeur de/à pour un attribut
     - |alt_filter_fromto_png|
     - |neu_filter_fromto_svg|
     -
   * - ``fromtodate``
     - Valeur de/à pour un attribut de date
     - |alt_filter_fromto_png|
     - |neu_filter_fromto_date_svg|
     - icône propre, auparavant identique à ``fromto``
   * - ``idlist``
     - Ensemble prédéfini d'éléments
     - |alt_filter_default_png|
     - |neu_filter_idlist_svg|
     - icône propre, auparavant l'icône de repli
   * - ``levenshtein``
     - Recherche assistée par Levenshtein
     - |alt_filter_levenshtein_png|
     - |neu_filter_levenshtein_svg|
     -
   * - ``loupe``
     - Recherche assistée par Loupe
     - —
     - |neu_loupe_emblem_svg|
     - était déjà en SVG auparavant, inchangé
   * - ``member_filter``
     - Autorisation pour les membres du frontend
     - |alt_filter_member_png|
     - |neu_filter_member_svg|
     - de contao-frontend-editing
   * - ``perimetersearch``
     - Recherche par périmètre
     - |alt_filter_perimetersearch_png|
     - |neu_filter_perimetersearch_svg|
     -
   * - ``range``
     - Valeur de/à pour deux attributs
     - |alt_filter_range_png|
     - |neu_filter_range_svg|
     -
   * - ``rangedate``
     - Valeur de/à pour deux attributs de date
     - |alt_filter_range_png|
     - |neu_filter_rangedate_svg|
     - icône propre, auparavant identique à ``range``
   * - ``register``
     - Registre
     - |alt_filter_register_png|
     - |neu_filter_register_svg|
     -
   * - ``related``
     - Filtre sur un attribut du modèle lié par une relation
     - |alt_filter_by_related_png|
     - |neu_filter_by_related_svg|
     -
   * - ``select``
     - Sélection simple
     - |alt_filter_select_png|
     - |neu_filter_select_svg|
     -
   * - ``simplelookup``
     - Requête simple
     - |alt_filter_default_png|
     - |neu_filter_simplelookup_svg|
     - icône propre, auparavant l'icône de repli
   * - ``tags``
     - Sélection multiple
     - |alt_filter_tags_png|
     - |neu_filter_tags_svg|
     -
   * - ``text``
     - Filtre de texte
     - |alt_filter_text_png|
     - |neu_filter_text_svg|
     -
   * - ``translatedcheckbox_published``
     - Statut de case à cocher traduit
     - |alt_visible_png|
     - |neu_filter_checkbox_svg|
     - partage l'icône avec ``checkbox_published``
   * - —
     - Règle de filtre sans icône propre
     - |alt_filter_default_png|
     - |neu_filter_default_svg|
     - valeur de repli ; les types ``idlist`` et ``simplelookup`` ont désormais leurs propres
       icônes


Conditions d'affichage
----------------------

Les conditions qui permettent d'afficher ou de masquer certains champs du masque de saisie
(*Gérer les conditions* au niveau d'un paramètre de masque de saisie) n'avaient jusqu'ici
aucune icône - la liste affichait le même symbole pour chaque condition. Chaque type de
condition reçoit désormais sa propre icône, de sorte que les combinaisons ET, OU et NON
puissent aussi être distinguées dans une liste imbriquée.

.. note:: Si un type de condition provenant d'un paquet tiers n'apporte pas sa propre icône,
   ``condition_default.svg`` est affiché. Un nouveau type n'a donc besoin que d'un fichier
   ``condition_<name>.svg`` dans le Core - aucun enregistrement n'est nécessaire.

.. list-table::
   :header-rows: 1
   :widths: 22 30 9 9 30

   * - Type
     - Libellé dans le backend
     - Avant
     - Nouveau
     - Remarque
   * - ``conditionand``
     - ET
     - —
     - |neu_condition_and_svg|
     - combine plusieurs conditions, toutes doivent être remplies
   * - ``conditionor``
     - OU
     - —
     - |neu_condition_or_svg|
     - combine plusieurs conditions, une seule suffit
   * - ``conditionnot``
     - NON
     - —
     - |neu_condition_not_svg|
     - inverse la condition qu'elle contient
   * - ``conditionpropertyvalueis``
     - La valeur de la propriété est …
     - —
     - |neu_condition_propertyvalueis_svg|
     - vérifie une valeur déterminée
   * - ``conditionpropertycontainanyof``
     - La valeur de la propriété peut contenir …
     - —
     - |neu_condition_propertycontainanyof_svg|
     - vérifie l'une de plusieurs valeurs
   * - ``conditionpropertyvisible``
     - La propriété est visible …
     - —
     - |neu_condition_propertyvisible_svg|
     - se rattache à la visibilité d'une autre propriété
   * - —
     - Icône de repli
     - —
     - |neu_condition_default_svg|
     - pour les types de condition issus de paquets tiers qui n'apportent pas leur propre icône


Autres symboles
---------------

Symboles d'état et de frontend qui ne représentent pas un type.

.. list-table::
   :header-rows: 1
   :widths: 44 9 9 38

   * - Signification
     - Avant
     - Nouveau
     - Remarque
   * - Case à cocher active (vue en liste)
     - |alt_visible_svg|
     - |neu_checkbox_active_svg|
     - auparavant le ``visible.svg`` propre à Contao, désormais une icône propre
   * - Case à cocher inactive (vue en liste)
     - |alt_invisible_svg|
     - |neu_checkbox_inactive_svg|
     - auparavant le ``invisible.svg`` propre à Contao, désormais une icône propre
   * - Évaluation – étoile vide
     - |alt_star_empty_png|
     - |neu_star_empty_svg|
     - affichage frontend
   * - Évaluation – étoile pleine
     - |alt_star_full_png|
     - |neu_star_full_svg|
     - affichage frontend
   * - Évaluation – étoile au survol
     - |alt_star_hover_png|
     - |neu_star_hover_svg|
     - affichage frontend
   * - Levenshtein – index
     - |alt_levenshtein_index_png|
     - |neu_levenshtein_index_svg|
     -


Extensions
----------

Deux extensions apportent leurs propres symboles. Elles suivent la même règle que le Core :
ce qui désigne une entité est coloré ; ce qui représente un type reste d'un gris neutre. Pour
la liste de favoris (Merkliste), les deux se voient - la liste de favoris elle-même en jaune,
sa règle de filtre en gris.

L'attribut ``marker_icon`` figure en outre plus haut dans les attributs, car il partage son
icône avec l'extension.

.. list-table::
   :header-rows: 1
   :widths: 44 9 9 38

   * - Signification
     - Avant
     - Nouveau
     - Remarque
   * - Liste de favoris
     - |alt_notelist_png|
     - |neu_notelist_svg|
     - la liste de favoris elle-même - jaune, car l'icône représente l'entité
   * - Liste de favoris – entrée contenue
     - |alt_notelist_png|
     - |neu_notelist_filled_svg|
     - auparavant la même icône que la liste de favoris elle-même - l'état rempli est nouveau
   * - Règle de filtre « liste de favoris »
     - |alt_notelist_png|
     - |neu_filter_notelist_svg|
     - icône de type grise propre
   * - Cowegis – couche MetaModels
     - |alt_metamodels_marker_svg|
     - |neu_metamodels_marker_svg|
     - type de couche dans la carte Cowegis ; était déjà en SVG auparavant
   * - Cowegis – marqueur
     - |alt_marker_png|
     - |neu_marker_svg|
     - également l'icône de type de l'attribut ``marker_icon``


.. Bild-Ersetzungen

.. |alt_alias_png| image:: /_img/icons/alias.png
   :width: 22px
.. |alt_article_png| image:: /_img/icons/article.png
   :width: 22px
.. |alt_checkbox_png| image:: /_img/icons/checkbox.png
   :width: 22px
.. |alt_color_png| image:: /_img/icons/color.png
   :width: 22px
.. |alt_combinedvalues_png| image:: /_img/icons/combinedvalues.png
   :width: 22px
.. |alt_country_png| image:: /_img/icons/country.png
   :width: 22px
.. |alt_dca_add_png| image:: /_img/icons/dca_add.png
   :width: 22px
.. |alt_dca_combine_png| image:: /_img/icons/dca_combine.png
   :width: 22px
.. |alt_dca_condition_png| image:: /_img/icons/dca_condition.png
   :width: 22px
.. |alt_dca_groupsortsettings_png| image:: /_img/icons/dca_groupsortsettings.png
   :width: 22px
.. |alt_dca_png| image:: /_img/icons/dca.png
   :width: 22px
.. |alt_dca_setting_png| image:: /_img/icons/dca_setting.png
   :width: 22px
.. |alt_decimal_png| image:: /_img/icons/decimal.png
   :width: 22px
.. |alt_fields_png| image:: /_img/icons/fields.png
   :width: 22px
.. |alt_file_png| image:: /_img/icons/file.png
   :width: 22px
.. |alt_filter_and_png| image:: /_img/icons/filter_and.png
   :width: 22px
.. |alt_filter_by_related_png| image:: /_img/icons/filter_by_related.png
   :width: 22px
.. |alt_filter_checkbox_png| image:: /_img/icons/filter_checkbox.png
   :width: 22px
.. |alt_filter_customsql_png| image:: /_img/icons/filter_customsql.png
   :width: 22px
.. |alt_filter_default_png| image:: /_img/icons/filter_default.png
   :width: 22px
.. |alt_filter_expression_png| image:: /_img/icons/filter_expression.png
   :width: 22px
.. |alt_filter_fromto_png| image:: /_img/icons/filter_fromto.png
   :width: 22px
.. |alt_filter_levenshtein_png| image:: /_img/icons/filter_levenshtein.png
   :width: 22px
.. |alt_filter_member_png| image:: /_img/icons/filter_member.png
   :width: 22px
.. |alt_filter_or_png| image:: /_img/icons/filter_or.png
   :width: 22px
.. |alt_filter_perimetersearch_png| image:: /_img/icons/filter_perimetersearch.png
   :width: 22px
.. |alt_filter_png| image:: /_img/icons/filter.png
   :width: 22px
.. |alt_filter_range_png| image:: /_img/icons/filter_range.png
   :width: 22px
.. |alt_filter_register_png| image:: /_img/icons/filter_register.png
   :width: 22px
.. |alt_filter_select_png| image:: /_img/icons/filter_select.png
   :width: 22px
.. |alt_filter_setting_png| image:: /_img/icons/filter_setting.png
   :width: 22px
.. |alt_filter_tags_png| image:: /_img/icons/filter_tags.png
   :width: 22px
.. |alt_filter_text_png| image:: /_img/icons/filter_text.png
   :width: 22px
.. |alt_geodistance_png| image:: /_img/icons/geodistance.png
   :width: 22px
.. |alt_invisible_svg| image:: /_img/icons/invisible.svg
   :width: 22px
.. |alt_langcode_png| image:: /_img/icons/langcode.png
   :width: 22px
.. |alt_levenshtein_index_png| image:: /_img/icons/levenshtein_index.png
   :width: 22px
.. |alt_levenshtein_png| image:: /_img/icons/levenshtein.png
   :width: 22px
.. |alt_locale_png| image:: /_img/icons/locale.png
   :width: 22px
.. |alt_logo_png| image:: /_img/icons/logo.png
   :width: 22px
.. |alt_longtext_png| image:: /_img/icons/longtext.png
   :width: 22px
.. |alt_marker_png| image:: /_img/icons/marker.png
   :width: 22px
.. |alt_metamodels_marker_svg| image:: /_img/icons/metamodels_marker.svg
   :width: 22px
.. |alt_metamodels_png| image:: /_img/icons/metamodels.png
   :width: 22px
.. |alt_mm_group_icon_contour_svg| image:: /_img/icons/mm_group_icon_contour.svg
   :width: 22px
.. |alt_notelist_png| image:: /_img/icons/notelist.png
   :width: 22px
.. |alt_numeric_png| image:: /_img/icons/numeric.png
   :width: 22px
.. |alt_rendersetting_png| image:: /_img/icons/rendersetting.png
   :width: 22px
.. |alt_rendersettings_add_png| image:: /_img/icons/rendersettings_add.png
   :width: 22px
.. |alt_rendersettings_png| image:: /_img/icons/rendersettings.png
   :width: 22px
.. |alt_searchable_pages_png| image:: /_img/icons/searchable_pages.png
   :width: 22px
.. |alt_select_png| image:: /_img/icons/select.png
   :width: 22px
.. |alt_star_empty_png| image:: /_img/icons/star-empty.png
   :width: 22px
.. |alt_star_full_png| image:: /_img/icons/star-full.png
   :width: 22px
.. |alt_star_hover_png| image:: /_img/icons/star-hover.png
   :width: 22px
.. |alt_tablemulti_png| image:: /_img/icons/tablemulti.png
   :width: 22px
.. |alt_tabletext_png| image:: /_img/icons/tabletext.png
   :width: 22px
.. |alt_tags_png| image:: /_img/icons/tags.png
   :width: 22px
.. |alt_text_png| image:: /_img/icons/text.png
   :width: 22px
.. |alt_timestamp_png| image:: /_img/icons/timestamp.png
   :width: 22px
.. |alt_token_png| image:: /_img/icons/token.png
   :width: 22px
.. |alt_translatedtablemulti_png| image:: /_img/icons/translatedtablemulti.png
   :width: 22px
.. |alt_translatedtabletext_png| image:: /_img/icons/translatedtabletext.png
   :width: 22px
.. |alt_url_png| image:: /_img/icons/url.png
   :width: 22px
.. |alt_variants_png| image:: /_img/icons/variants.png
   :width: 22px
.. |alt_visible_png| image:: /_img/icons/visible.png
   :width: 22px
.. |alt_visible_svg| image:: /_img/icons/visible.svg
   :width: 22px
.. |neu_alias_svg| image:: /_img/icons_svg/alias.svg
   :width: 22px
.. |neu_article_svg| image:: /_img/icons_svg/article.svg
   :width: 22px
.. |neu_checkbox_active_svg| image:: /_img/icons_svg/checkbox_active.svg
   :width: 22px
.. |neu_checkbox_inactive_svg| image:: /_img/icons_svg/checkbox_inactive.svg
   :width: 22px
.. |neu_checkbox_svg| image:: /_img/icons_svg/checkbox.svg
   :width: 22px
.. |neu_child_table_svg| image:: /_img/icons_svg/child_table.svg
   :width: 22px
.. |neu_color_svg| image:: /_img/icons_svg/color.svg
   :width: 22px
.. |neu_combinedvalues_svg| image:: /_img/icons_svg/combinedvalues.svg
   :width: 22px
.. |neu_condition_and_svg| image:: /_img/icons_svg/condition_and.svg
   :width: 22px
.. |neu_condition_default_svg| image:: /_img/icons_svg/condition_default.svg
   :width: 22px
.. |neu_condition_not_svg| image:: /_img/icons_svg/condition_not.svg
   :width: 22px
.. |neu_condition_or_svg| image:: /_img/icons_svg/condition_or.svg
   :width: 22px
.. |neu_condition_propertycontainanyof_svg| image:: /_img/icons_svg/condition_propertycontainanyof.svg
   :width: 22px
.. |neu_condition_propertyvalueis_svg| image:: /_img/icons_svg/condition_propertyvalueis.svg
   :width: 22px
.. |neu_condition_propertyvisible_svg| image:: /_img/icons_svg/condition_propertyvisible.svg
   :width: 22px
.. |neu_country_svg| image:: /_img/icons_svg/country.svg
   :width: 22px
.. |neu_dca_add_svg| image:: /_img/icons_svg/dca_add.svg
   :width: 22px
.. |neu_dca_combine_svg| image:: /_img/icons_svg/dca_combine.svg
   :width: 22px
.. |neu_dca_condition_svg| image:: /_img/icons_svg/dca_condition.svg
   :width: 22px
.. |neu_dca_groupsortsettings_svg| image:: /_img/icons_svg/dca_groupsortsettings.svg
   :width: 22px
.. |neu_dca_setting_svg| image:: /_img/icons_svg/dca_setting.svg
   :width: 22px
.. |neu_dca_svg| image:: /_img/icons_svg/dca.svg
   :width: 22px
.. |neu_decimal_svg| image:: /_img/icons_svg/decimal.svg
   :width: 22px
.. |neu_fields_svg| image:: /_img/icons_svg/fields.svg
   :width: 22px
.. |neu_file_svg| image:: /_img/icons_svg/file.svg
   :width: 22px
.. |neu_filter_and_svg| image:: /_img/icons_svg/filter_and.svg
   :width: 22px
.. |neu_filter_by_related_svg| image:: /_img/icons_svg/filter_by_related.svg
   :width: 22px
.. |neu_filter_checkbox_svg| image:: /_img/icons_svg/filter_checkbox.svg
   :width: 22px
.. |neu_filter_customsql_svg| image:: /_img/icons_svg/filter_customsql.svg
   :width: 22px
.. |neu_filter_default_svg| image:: /_img/icons_svg/filter_default.svg
   :width: 22px
.. |neu_filter_expression_svg| image:: /_img/icons_svg/filter_expression.svg
   :width: 22px
.. |neu_filter_fromto_date_svg| image:: /_img/icons_svg/filter_fromto_date.svg
   :width: 22px
.. |neu_filter_fromto_svg| image:: /_img/icons_svg/filter_fromto.svg
   :width: 22px
.. |neu_filter_idlist_svg| image:: /_img/icons_svg/filter_idlist.svg
   :width: 22px
.. |neu_filter_levenshtein_svg| image:: /_img/icons_svg/filter_levenshtein.svg
   :width: 22px
.. |neu_filter_member_svg| image:: /_img/icons_svg/filter_member.svg
   :width: 22px
.. |neu_filter_notelist_svg| image:: /_img/icons_svg/filter_notelist.svg
   :width: 22px
.. |neu_filter_or_svg| image:: /_img/icons_svg/filter_or.svg
   :width: 22px
.. |neu_filter_perimetersearch_svg| image:: /_img/icons_svg/filter_perimetersearch.svg
   :width: 22px
.. |neu_filter_range_svg| image:: /_img/icons_svg/filter_range.svg
   :width: 22px
.. |neu_filter_rangedate_svg| image:: /_img/icons_svg/filter_rangedate.svg
   :width: 22px
.. |neu_filter_register_svg| image:: /_img/icons_svg/filter_register.svg
   :width: 22px
.. |neu_filter_select_svg| image:: /_img/icons_svg/filter_select.svg
   :width: 22px
.. |neu_filter_setting_svg| image:: /_img/icons_svg/filter_setting.svg
   :width: 22px
.. |neu_filter_simplelookup_svg| image:: /_img/icons_svg/filter_simplelookup.svg
   :width: 22px
.. |neu_filter_svg| image:: /_img/icons_svg/filter.svg
   :width: 22px
.. |neu_filter_tags_svg| image:: /_img/icons_svg/filter_tags.svg
   :width: 22px
.. |neu_filter_text_svg| image:: /_img/icons_svg/filter_text.svg
   :width: 22px
.. |neu_filter_yes_no_svg| image:: /_img/icons_svg/filter_yes-no.svg
   :width: 22px
.. |neu_geodistance_svg| image:: /_img/icons_svg/geodistance.svg
   :width: 22px
.. |neu_langcode_svg| image:: /_img/icons_svg/langcode.svg
   :width: 22px
.. |neu_levenshtein_index_svg| image:: /_img/icons_svg/levenshtein_index.svg
   :width: 22px
.. |neu_levenshtein_svg| image:: /_img/icons_svg/levenshtein.svg
   :width: 22px
.. |neu_locale_svg| image:: /_img/icons_svg/locale.svg
   :width: 22px
.. |neu_longtext_svg| image:: /_img/icons_svg/longtext.svg
   :width: 22px
.. |neu_loupe_emblem_svg| image:: /_img/icons_svg/loupe-emblem.svg
   :width: 22px
.. |neu_marker_svg| image:: /_img/icons_svg/marker.svg
   :width: 22px
.. |neu_metamodels_marker_svg| image:: /_img/icons_svg/metamodels_marker.svg
   :width: 22px
.. |neu_metamodels_svg| image:: /_img/icons_svg/metamodels.svg
   :width: 22px
.. |neu_mm_group_icon_svg| image:: /_img/icons_svg/mm_group_icon.svg
   :width: 22px
.. |neu_mm_logo_small_svg| image:: /_img/icons_svg/mm_logo_small.svg
   :width: 22px
.. |neu_notelist_filled_svg| image:: /_img/icons_svg/notelist_filled.svg
   :width: 22px
.. |neu_notelist_svg| image:: /_img/icons_svg/notelist.svg
   :width: 22px
.. |neu_numeric_svg| image:: /_img/icons_svg/numeric.svg
   :width: 22px
.. |neu_rendersetting_svg| image:: /_img/icons_svg/rendersetting.svg
   :width: 22px
.. |neu_rendersettings_add_svg| image:: /_img/icons_svg/rendersettings_add.svg
   :width: 22px
.. |neu_rendersettings_svg| image:: /_img/icons_svg/rendersettings.svg
   :width: 22px
.. |neu_searchable_pages_svg| image:: /_img/icons_svg/searchable_pages.svg
   :width: 22px
.. |neu_select_svg| image:: /_img/icons_svg/select.svg
   :width: 22px
.. |neu_star_empty_svg| image:: /_img/icons_svg/star-empty.svg
   :width: 22px
.. |neu_star_full_svg| image:: /_img/icons_svg/star-full.svg
   :width: 22px
.. |neu_star_hover_svg| image:: /_img/icons_svg/star-hover.svg
   :width: 22px
.. |neu_star_svg| image:: /_img/icons_svg/star.svg
   :width: 22px
.. |neu_tablemulti_svg| image:: /_img/icons_svg/tablemulti.svg
   :width: 22px
.. |neu_tabletext_svg| image:: /_img/icons_svg/tabletext.svg
   :width: 22px
.. |neu_tags_svg| image:: /_img/icons_svg/tags.svg
   :width: 22px
.. |neu_text_svg| image:: /_img/icons_svg/text.svg
   :width: 22px
.. |neu_timestamp_svg| image:: /_img/icons_svg/timestamp.svg
   :width: 22px
.. |neu_token_svg| image:: /_img/icons_svg/token.svg
   :width: 22px
.. |neu_translatedtablemulti_svg| image:: /_img/icons_svg/translatedtablemulti.svg
   :width: 22px
.. |neu_translatedtabletext_svg| image:: /_img/icons_svg/translatedtabletext.svg
   :width: 22px
.. |neu_url_svg| image:: /_img/icons_svg/url.svg
   :width: 22px
.. |neu_variants_svg| image:: /_img/icons_svg/variants.svg
   :width: 22px
