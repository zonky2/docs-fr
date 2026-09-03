.. _component_index:

Composants d'un MetaModel
===========================

Les chapitres suivants présentent la structure des MetaModels afin de comprendre la « logique »
de la construction de l'extension.

Tout d'abord, une distinction entre deux notions : par **MetaModel** (singulier), on désignera
dans la suite une table de données avec ses attributs, ses possibilités d'entrée/sortie, ses
filtres, etc. Un MetaModel est écrit sans « s » dans les textes qui suivent, même lorsque cela
serait par exemple requis par un pluriel.

Le terme **MetaModels** (pluriel) désigne uniquement le paquet d'extension pour Contao.

Pour les nouveaux utilisateurs ou ceux qui reprennent MetaModels après une pause, il peut être
un peu difficile de trouver un déroulement de travail adapté à la création. Pour ce public, il
existe un :ref:`déroulement de travail simple pour l'utilisation de MetaModels
<component_workflow>`. On y trouve également quelques :ref:`conseils pour démarrer
<component_workflow_tips>` ainsi qu'un :ref:`aperçu des attributs permettant de stocker
quel type de donnée <component_data-in-attributes>`.

Avant de se lancer dans la création de structures de données plus complexes dans MetaModels, il
est indispensable de réfléchir à une construction « élégante » - en particulier aux relations
entre les Models. Une page d'aperçu y est consacrée : ":ref:`component_relations`".

.. note:: Attention : dans MM 2.5, de nouvelles icônes SVG ont été introduites dans MetaModels.
   Pendant une période de transition, les deux variantes sont affichées dans le manuel - d'abord
   la nouvelle, puis l'ancienne - un aperçu se trouve ici : :ref:`manual_new_icons-25`

Après la création d'un MetaModel, les composants principaux suivants sont disponibles pour l'édition :

 |svg_fields_22| |img_fields|  :ref:`component_attribute` |br|
 |svg_rendersettings_22| |img_rendersettings|  :ref:`component_rendersettings` |br|
 |svg_dca_22| |img_dca|  :ref:`component_dca` |br|
 |svg_searchable_pages_22| |img_searchable_pages|  :ref:`component_searchable-pages` |br|
 |svg_filter_22| |img_filter|  :ref:`component_filter` |br|
 |svg_dca_combine_22| |img_dca_combine|  :ref:`component_dca-combine`

Lors de la création d'un MetaModel (simple), les composants peuvent être traités dans l'ordre
indiqué. Avec la complexité croissante du MetaModel - c'est-à-dire lorsque plusieurs MetaModels
interagissent entre eux - il devient inévitable de compléter ou de modifier ultérieurement
certaines saisies dans un MetaModel existant.

Outre les composants principaux, il existe d'autres possibilités de réglage comme la création
de groupements/tris des Items dans une liste du back-end ou les :ref:`conditions d'affichage
des widgets de saisie d'un masque de saisie <component_dca_visibility-conditions>`.

.. _rst_component_index_mm_lageplan:
Pour une vue d'ensemble facilitant la recherche des informations, un
:download:`« plan du site MM » </_download/MM_Lageplan_e-spin-Berlin.pdf>` est disponible au
téléchargement.

Avec l'extension MetaModels, Contao dispose de deux nouveaux éléments de contenu et modules
pour l'affichage en frontend. Avec l'élément de contenu/module « Liste MetaModel », des
enregistrements peuvent être affichés individuellement ou sous forme de liste sur le site web,
et avec l'élément de contenu/module « Filtre frontend MetaModel », un filtre est disponible pour
le frontend - pour en savoir plus, voir :ref:`component_contentelements`.

La manière dont les différents templates interagissent est décrite sur la page consacrée aux
:ref:`component_templates`.

MetaModels est très bien adapté au travail avec des contenus multilingues -
:ref:`en savoir plus sur le multilinguisme dans MM. <component_multi-language>`

Pour afficher des valeurs individuelles d'un enregistrement (Item) ou le nombre total
d'enregistrements dans le contexte de Contao, différents :ref:`Insert-Tags <component_inserttags>`
sont disponibles.


.. toctree::
    :hidden:
    :maxdepth: 1

    workflow
    new-mm
    attribute
    rendersettings
    dca
    dca-visibility-conditions
    searchable-pages
    filter
    dca-combine
    contentelements
    relations
    schema-manager
    translations
    templates
    data-in-attributes
    multi-language
    inserttags

.. |br| raw:: html

   <br />

.. |nbsp| unicode:: 0xA0
   :trim:

.. |img_fields| image:: /_img/icons/fields.png
.. |svg_fields_22| image:: /_img/icons_svg/fields.svg
   :width: 22px
.. |img_rendersettings| image:: /_img/icons/rendersettings.png
.. |svg_rendersettings_22| image:: /_img/icons_svg/rendersettings.svg
   :width: 22px
.. |img_dca| image:: /_img/icons/dca.png
.. |svg_dca_22| image:: /_img/icons_svg/dca.svg
   :width: 22px
.. |img_searchable_pages| image:: /_img/icons/searchable_pages.png
.. |svg_searchable_pages_22| image:: /_img/icons_svg/searchable_pages.svg
   :width: 22px
.. |img_filter| image:: /_img/icons/filter.png
.. |svg_filter_22| image:: /_img/icons_svg/filter.svg
   :width: 22px
.. |img_dca_combine| image:: /_img/icons/dca_combine.png
.. |svg_dca_combine_22| image:: /_img/icons_svg/dca_combine.svg
   :width: 22px
