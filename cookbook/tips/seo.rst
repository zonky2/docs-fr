.. _rst_cookbook_tips_seo:

Optimisation pour les moteurs de recherche (SEO)
======================================================

Pour que les contenus issus de MM soient bien trouvés et indexés sur le site, on peut aider les « bots » avec
différents réglages.

Recherche Contao
--------------------

Pour la `recherche Contao <https://docs.contao.org/manual/de/layout/modulverwaltung/website-suche>`_, les contenus
sont indexés de différentes manières. Cela peut se faire lors de la visite d'une page par un utilisateur, ou via le
`crawler Contao <https://docs.contao.org/manual/de/cli/crawl/>`_, qui suit les liens présents sur le site et analyse
les indications de la ``sitemap.xml``.

Pour une indexation, les autorisations habituelles doivent être accordées dans les réglages de la page, ou la
recherche ne doit pas être exclue.

Si l'on souhaite favoriser l'indexation des pages de détail via la ``sitemap.xml``, cela peut être obtenu dans MM en
créant sa propre indexation - voir :ref:`component_searchable-pages`.

Pour les pages avec filtre FE contenant des listes de liens, il convient de tenir compte de la manière
:ref:`d'exclure ces liens du crawling <rst_cookbook_filter_exclude-url-from-search-index>`.


SEO pour Google & Cie
--------------------------

.. _rst_cookbook_tips_seo_url:
URL « parlantes »
....................

Dans la plupart des cas, il s'agit ici du lien vers la page de détail, par ex. depuis une page de liste.
Habituellement, l'alias de l'item est utilisé pour le filtrage sur la page de détail. Dans les réglages de
l'attribut :ref:`Alias <component_attribute_alias>` ou :ref:`Alias traduit <component_attribute_translatedalias>`,
la combinaison souhaitée d'autres valeurs d'attributs peut être définie.


.. _rst_cookbook_tips_seo_metadata-title:
Métadonnées Title et Description
........................................

Ces réglages concernent à nouveau principalement les réglages d'une page de détail. Dans l'élément de contenu ou le
module FE MM-Liste, il existe respectivement une liste de sélection avec les attributs disponibles pour Title et
Description.

La Description devrait décrire le contenu de la page de manière concise. Google, par exemple,
`n'impose pas de nombre maximal de caractères <https://developers.google.com/search/docs/appearance/snippet?hl=de#meta-descriptions>`_,
mais de nombreux sites SEO indiquent un nombre de caractères maximal de 150 à 160 - Contao lui-même limite cela à
320 caractères dans la fe_page.

Si l'on souhaite des possibilités de réglage plus individuelles, on peut créer des attributs texte dédiés pour Title
et Description. Le rédacteur peut ainsi optimiser ces indications indépendamment des autres attributs.

Comme autre possibilité de transmission des données, on peut effectuer la création de Title et Description dans le
template de rendu - voir :ref:`component_templates`. La sortie peut par ex. se faire avec l'extrait de code suivant
dans le template :

.. code-block:: php
   :linenos:

   <?php
   // templates/metamodels_prerendered_details.html5
   use Contao\CoreBundle\Routing\ResponseContext\HtmlHeadBag\HtmlHeadBag;
   use Contao\StringUtil;
   use Contao\System;

   $container       = System::getContainer();
   $htmlDecoder     = $container->get('contao.string.html_decoder');
   $responseContext = $container->get('contao.routing.response_context_accessor')->getResponseContext();
   $htmlHeadBag     = $responseContext->get(HtmlHeadBag::class);
   ?>
   ...
   <?php
   $htmlHeadBag->setTitle($htmlDecoder->inputEncodedToPlainText($arrItem['text']['title'] . ' - ' $arrItem['text']['art_no']));
   $htmlHeadBag->setMetaDescription(StringUtil::substr($htmlDecoder->inputEncodedToPlainText($arrItem['text']['title'] . ' - ' $arrItem['text']['description']), 160));
   ?>

Le ``$htmlHeadBag`` pourrait également être mis à disposition via une classe helper, en injectant les services
intégrés.


.. _rst_cookbook_tips_seo_breadcrumb:
Fil d'Ariane (Breadcrumb)
.................................

Le dernier point de navigation du fil d'Ariane est généré automatiquement à partir du titre de la page. Si, pour une
page de détail, le :ref:`titre de page a été généré dynamiquement à partir d'un attribut MM <rst_cookbook_tips_seo_metadata-title>`,
celui-ci n'est pas affiché dans le fil d'Ariane. Cela s'explique par le fait que le module FE pour le fil d'Ariane
est généralement placé avant la MM-Liste et reçoit donc cette information trop tard, voire pas du tout.

Un « BreadcrumbController », qui n'ajoute le fil d'Ariane qu'ultérieurement au rendu de la page, permet d'y
remédier. On peut actuellement trouver `un exemple de code ici <https://gist.github.com/fritzmg/e7df2804365fe676b1d88f053a234707?permalink_comment_id=5698503#gistcomment-5698503>`_
- `ce problème sera corrigé dans Contao 5.7 <https://youtu.be/nvIPd3OzXhs?t=1787>`_.


.. _rst_cookbook_tips_seo_metadata-hreflang:
Métadonnées hreflang
.........................

Si, pour une structure de page multilingue, la sortie existe également dans une ou plusieurs autres langues, cela
peut être indiqué au moteur de recherche via un lien dans ``hreflang``. Pour permettre au visiteur de changer de
langue dans le frontend, il existe différentes extensions - c'est souvent
« `ChangeLanguage <https://github.com/terminal42/contao-changelanguage>`_ » qui est utilisée.

Cette extension génère automatiquement les métadonnées pour ``hreflang``, à condition que les relations
correspondantes aient été sélectionnées dans les propriétés de la page.

Les liens affichés dans le code source fonctionnent sans adaptation supplémentaire, mais uniquement vers l'alias de
page respectif des autres pages, sans transmission des paramètres de filtre, par ex. pour la page de détail.

L'extension « ChangeLanguage » propose, dans les réglages de page, l'option « Conserver les paramètres de requête »,
à renseigner avec des clés. Les paires clé-valeur correspondantes sont alors également ajoutées aux autres liens de
langue. La clé ``auto_item`` n'est cependant pas prise en charge en tant que telle.

Pour un changement de langue d'une page de détail, on peut utiliser la configuration suivante :

* Filtre « Détails » avec la règle de filtre « Requête simple » pour l'attribut « Alias » - laisser le
  « paramètre URL » sur ``alias`` et ne pas le régler sur ``auto_item``
* dans les propriétés de page, saisir « alias » dans « Conserver les paramètres de requête » sur toutes les pages
  de détail

Le résultat se présente alors, en résumé, comme suit :

.. code-block:: html
   :linenos:

   <link rel="alternate" hreflang="de" href="http://my-domain.tld/de/details/alias/mayer-herbert">
   <link rel="alternate" hreflang="x-default" href="http://my-domain.tld/de/details/alias/mayer-herbert">
   <link rel="alternate" hreflang="en" href="http://my-domain.tld/en/details/alias/mayer-herbert">

Si l'on souhaite créer des liens avec ``auto_item`` ou intégrer dans l'URL les clés et valeurs traduites
d'attributs multilingues, cela doit être réalisé avec une adaptation personnalisée, par ex. via le hook
« `changelanguageNavigation <https://extensions.terminal42.ch/docs/changelanguage/en/developers/>`_ ».

:ref:`Plus d'informations sur le multilinguisme dans MM. <component_multi-language>`


.. _rst_cookbook_tips_seo_filter-url:
Paramètres Slug vs GET dans les URL de filtre
....................................................

À partir de MM 2.4, on peut choisir, dans chaque règle de filtre via le réglage « Type d'URL pour le paramètre »,
si un paramètre de filtre est transmis comme partie du chemin d'URL (slug) ou comme paramètre GET classique - voir
:ref:`paramètres de réglage de la règle de filtre <component_filter>`.

**Les paramètres slug (chemins d'URL parlants)** génèrent des URL propres et bien lisibles - par ex.
``/produkte/kategorie/mit-akku`` au lieu de ``/produkte?kategorie=mit-akku``. Ils constituent en général la
variante privilégiée pour les contenus indexables, car les moteurs de recherche traitent cette forme comme une page
autonome. Cette forme convient particulièrement lorsque des combinaisons de filtres doivent servir de landing pages
autonomes et indexables. Cela peut cependant rapidement conduire à un grand nombre de variantes d'URL potentielles,
qu'il convient de contrôler soigneusement via des balises canoniques ou des règles d'indexation. Avec les
paramètres slug, en indiquant ``auto_item`` comme paramètre d'URL, la clé peut être masquée, par ex. pour la
catégorie ``/produkte/mit-akku`` - mais ``auto_item`` ne fonctionne que pour un seul paramètre d'URL.

**Les paramètres GET** (par ex. ``?farbe=rot``) sont certes également traités par les moteurs de recherche, mais
sont considérés comme moins « parlants » et souvent interprétés comme des variantes techniques de la même page. Ils
conviennent donc particulièrement aux filtres purement fonctionnels, qui ne doivent pas avoir de pertinence SEO
propre et qui, typiquement, n'ont pas besoin d'être indexés. En combinaison avec des URL canoniques appropriées,
cela permet d'éviter la création d'un trop grand nombre de variantes de contenu dupliqué. Il est en outre possible,
pour les outils de suivi comme Google Analytics, d'exclure certains paramètres GET du tracking.

**Recommandation :** |br|
Les paramètres slug devraient être utilisés pour les combinaisons filtrables et pertinentes pour les moteurs de
recherche, tandis que les paramètres GET conviennent mieux aux filtres purement interactifs ou non indexables. La
décision dépend en définitive de la question de savoir si une combinaison de filtres doit fonctionner comme une
landing page autonome ou ne sert qu'à la navigation interne.

Remarque : si un paramètre existe à la fois en slug et en GET, Contao renvoie une erreur 404.


Pagination de la sortie de liste
.......................................

Les listes de sortie longues devraient être paginées - d'une part parce que la page est plus facile à appréhender
pour l'utilisateur et se charge plus vite, et d'autre part pour un meilleur classement lors de l'évaluation des
performances par les moteurs de recherche.

La page de sortie devrait comporter, dans les métadonnées, une indication de l'
`URL canonique <https://developers.google.com/search/docs/crawling-indexing/consolidate-duplicate-urls>`_ - cela
peut être activé dans les propriétés de la page. Google impose la restriction que la première page (page de base) ne
doit pas être désignée comme page canonique, mais seulement toutes les pages de pagination suivantes -
`voir Google « Bien utiliser les URL » <https://developers.google.com/search/docs/specialty/ecommerce/pagination-and-incremental-page-loading?hl=de#use-urls-correctly>`_

L'indication de ``rel="next"`` et ``rel="prev"``
`n'est plus prise en compte par Google <https://developers.google.com/search/docs/specialty/ecommerce/pagination-and-incremental-page-loading?hl=de#use-urls-correctly>`_
- d'autres moteurs de recherche comme Bing semblent encore l'exploiter, et certains navigateurs utilisent les liens
dans les métadonnées pour précharger la page.

Ceux qui souhaitent afficher ces indications dans le ``head`` de la page peuvent créer un template dédié
``mm_pagination.html5`` et y compléter les indications méta - par ex. avec

.. code-block:: php
   :linenos:

   <?php
   // templates/mm_pagination.html5
   ...
   <?php if ($this->hasPrevious): ?>
      <?php $GLOBALS['TL_HEAD'][] = '<link rel="prev" href="' . $this->previous['href'] . '" />' ?>
   ...
   <?php if ($this->hasNext): ?>
      <?php $GLOBALS['TL_HEAD'][] = '<link rel="next" href="' . $this->next['href'] . '" />' ?>
   ...

.. _rst_cookbook_tips_seo_structured-data:
Données structurées
..........................

Pour l'association sémantique des contenus affichés, on peut en outre afficher dans le code source ce que l'on
appelle des « `données structurées
<https://developers.google.com/search/docs/appearance/structured-data/intro-structured-data>`_ ».

Avec ces « données auxiliaires », un moteur de recherche peut associer les contenus, par ex. d'une FAQ, d'un
événement, d'une recherche d'emploi, d'une annonce de logement, d'une recette de cuisine, etc.

La manière d'intégrer ces données est décrite dans l'article « :ref:`rst_cookbook_templates_fe_template_schema_org` ».

Si l'on souhaite également que les images issues de l'attribut Fichier - comme c'est courant chez Contao - figurent
dans les données JSON-LD, un template dédié ``mm_attr_file_contao_image.html5`` est disponible - il doit être
sélectionné dans les réglages de rendu de l'attribut ou repris dans son propre template.

Il existe en outre un template ``mm_attr_file_contao_image_ofpage.html5``, qui intègre en plus la première image
comme ``primaryImageOfPage`` dans les données JSON-LD. Si cette indication d'image est présente, cette image est
également affichée, par ex. dans les résultats de la recherche Contao. Cela fonctionne de manière analogue aux vues
de détail des News et Events de Contao.

.. |br| raw:: html

   <br />
