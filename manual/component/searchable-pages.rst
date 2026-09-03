.. _component_searchable-pages:

|svg_searchable_pages_32| |img_searchable_pages_32| Réglages de recherche
=============================================================================

.. note:: intégrer les pages de détail d'un MetaModel dans le sitemap.xml de Contao

Introduction
------------

Les réglages de recherche permettent d'intégrer les pages de détail d'un rendering (liste)
MetaModel dans la génération du sitemap.xml.

Ce « traitement spécial » des pages de détail par rapport aux affichages de liste normaux résulte
de la manière dont ces pages sont appelées. Les pages de détail créées dans l'arborescence des
pages de Contao doivent toujours être appelées avec des paramètres GET ou de routage d'URL
spécifiques pour afficher une page de détail (utile) avec des valeurs. La fonction Contao de
génération du sitemap.xml ne peut pas accéder à ces paramètres provenant de MetaModels et a donc
besoin d'un support correspondant.

Les « affichages en liste normaux » n'ont pas besoin de ce traitement spécial et les pages sont
automatiquement intégrées correctement dans la recherche ou le sitemap via les fonctions Contao.

La « page de base » telle que créée par Contao est retirée du sitemap.xml, c'est-à-dire que la page
``domain.tld/mein-projekt/detail.html`` n'apparaît pas dans le sitemap.xml, mais seulement les URL
avec le paramètre de filtre, donc par ex. ``domain.tld/mein-projekt/detail/alias-1.html``,
``.../alias-2.html``, etc.

Les pages de détail ne sont pas intégrées dans le module FE « Sitemap ».

Il faut noter que les URL comportant certains mots-clés utilisés comme « Keys » par Contao, comme
`id`, `file`, `year`, etc., ne sont pas indexées ; par ex. pour une URL
details/id/meine-details-123.html - les mots-clés sont listés dans le tableau
`$GLOBALS['TL_NOINDEX_KEYS'] <https://github.com/contao/core/blob/master/system/modules/core/config/config.php#L419>`_.

Les pages de détail sont plus facilement intégrées dans la recherche (normale) de Contao grâce aux
liens présents dans le sitemap.xml - voir `contao:crawl <https://docs.contao.org/manual/de/cli/crawl/>`_

Options
-------

* **Nom** : |br|
  désignation pour le backend
* **Réglages de rendu** : |br|
  sélection du réglage de rendu pour la vue en liste, qui mène également à la vue détaillée
* **Ensemble de filtres** : |br|
  sélection d'un ensemble de filtres pour restreindre les pages de détail - par ex. pour ne
  sortir/intégrer dans le sitemap.xml que les enregistrements publiés

Déroulement
-----------

Un nouveau réglage de recherche est créé via l'icône « |img_new| Nouveau réglage de recherche »,
puis, après la saisie du nom, le réglage de rendu est sélectionné. Le réglage de rendu est
généralement le même que celui choisi pour le CE/module liste MetaModel de la sortie frontend de la
« liste d'aperçu » - mais un réglage de rendu propre peut également être créé.

Un filtre doit être sélectionné si certaines URL de pages de détail ne doivent pas apparaître dans
le sitemap.xml - par ex. pour n'intégrer que les enregistrements publiés.

Depuis Contao 4.11, la génération du sitemap.xml se fait dynamiquement lors de l'appel et n'est
plus déposée dans le dossier `share`.

Conseils
--------

* :ref:`rst_cookbook_filter_exclude-url-from-search-index`
* :ref:`rst_cookbook_tips_seo_structured-data` ou
* :ref:`rst_cookbook_templates_fe_template_schema_org`
* :ref:`rst_cookbook_specials_add_items_at_navigation`


.. |svg_searchable_pages_32| image:: /_img/icons_svg/searchable_pages.svg
   :width: 32px
.. |img_searchable_pages_32| image:: /_img/icons/searchable_pages_32.png
.. |img_searchable_pages| image:: /_img/icons/searchable_pages.png
.. |img_new| image:: /_img/icons/new.gif


.. |br| raw:: html

   <br />
