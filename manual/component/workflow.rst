.. _component_workflow:

Déroulement de travail avec MetaModels
=======================================

Le déroulement de travail permettant de transposer sa propre structure de données dans MetaModels
se divise en plusieurs étapes qui doivent être réalisées les unes après les autres pour chaque
MetaModel. La description suivante s'adresse aux débutants dans MetaModels et a été rédigée sur
la base d'une « bonne pratique » - les utilisateurs expérimentés regrouperont certaines étapes et
les compléteront directement.

Les différentes étapes sont détaillées plus précisément dans les autres articles de la section
:ref:`component_index`.

.. note:: Attention : dans MM 2.5, de nouvelles icônes SVG ont été introduites dans MetaModels.
   Pendant une période de transition, les deux variantes sont affichées dans le manuel - d'abord
   la nouvelle, puis l'ancienne - un aperçu se trouve ici : :ref:`manual_new_icons-25`

Étape 0 : concept de la structure de données
---------------------------------------------

L'ensemble des MetaModels et leurs liaisons forment une structure de base de données permettant
de stocker, d'afficher et de filtrer les données de la manière souhaitée. En particulier pour les
tâches complexes, une bonne planification aide à éviter des modifications ultérieures.

Il est recommandé de représenter graphiquement la structure des MetaModels et leurs liaisons.
Cela aide aussi bien à la création qu'à la documentation.

Dans MetaModels, outre les relations classiques comme la liaison simple (1:n) ou multiple (m:n),
d'autres options sont également disponibles - pour en savoir plus, voir l'article
:ref:`component_relations`.

Dans le cas le plus simple, on peut esquisser le schéma avec papier et crayon - mais il existe
aussi divers outils comme `yEd <https://www.yworks.com/products/yed>`_ ou la variante en ligne
`yEd live <https://www.yworks.com/yed-live/>`_.

Exemple de structure pour des collaborateurs, avec liaisons vers un département et des projets
ainsi qu'une auto-référence pour un remplacement de congés :

|img_db-schema_01|

Pour le stockage des données et les relations, MetaModels a besoin des attributs correspondants -
ceux qui sont disponibles à cet effet se trouvent sur :ref:`component_data-in-attributes`.

Cela permet également de choisir quels paquets de MM installer en plus du Core.

Étape 1 : réglages de base pour un MetaModel
----------------------------------------------

Pour les réglages de base, les paramètres les plus importants sont présélectionnés, de sorte
que seules les indications et sélections les plus nécessaires doivent être effectuées. Pour une
vue d'ensemble facilitant la recherche des informations, un
:download:`« plan du site MM » </_download/MM_Lageplan_e-spin-Berlin.pdf>` est disponible au
téléchargement.

* 1 : |img_new| :ref:`Créer un nouveau MetaModel <mm_first_new-mm>`
    * régler le :ref:`multilinguisme <component_multi-language>` si nécessaire
    * après l'enregistrement, les icônes peuvent être utilisées de gauche à droite comme suit
      |svg_workflow_01| |img_workflow_01|
* 2 : |svg_fields_22| |img_fields| :ref:`Créer les attributs <mm_first_attribute>`
    * après avoir créé tous les attributs, exécuter impérativement la
      :ref:`migration de la base de données <component_schema-manager>` (Contao-Manager ou console)
      et vider le cache
* 3.a : |svg_rendersettings_22| |img_rendersettings| :ref:`Créer un réglage de rendu <component_rendersettings>`
    * réglage de base pour la vue en liste
* 3.b : |svg_rendersetting_22| |img_rendersetting| :ref:`Ajouter des attributs dans le réglage de rendu <component_rendersettings>`
    * détermine quels attributs sont disponibles dans la vue de liste concernée
* 4.a : |svg_dca_22| |img_dca| :ref:`Créer un masque de saisie <component_dca>`
    * réglage de base pour le masque de saisie
* 4.b : |svg_dca_setting_22| |img_dca_setting| :ref:`Créer les attributs pour le masque de saisie <component_dca>`
    * détermine quels attributs sont disponibles dans la vue du masque de saisie concerné
* 5 : |svg_dca_combine_22| |img_dca_combine| :ref:`Créer les affectations saisie/rendu <component_dca-combine>`
    * sélectionner et enregistrer le réglage de rendu et le masque de saisie créés

Une fois le point 5 terminé, le nouveau MetaModel devrait apparaître à gauche dans la navigation
de Contao, dans la section « METAMODELS ».

**On peut, voire on devrait maintenant saisir les premiers enregistrements de test.**

Étape 2 : sortie de base
-------------------------

- 1 : créer une page et un article dans Contao
- 2.a : créer dans l'article un :ref:`élément de contenu « Liste MetaModel » <component_contentelements>`
- 2.b : dans la liste MetaModel, sélectionner le MetaModel créé ainsi que le réglage de rendu, puis
  enregistrer

**Sur la page créée, le frontend devrait maintenant afficher une liste avec les enregistrements
de test saisis à l'étape 1.**

Étape 3 : adapter les réglages de l'étape 1
----------------------------------------------

* 1 : |img_new| :ref:`Adapter le MetaModel <mm_first_new-mm>`
    * activer les :ref:`variantes <component_relations_variants>` si nécessaire pour la structure
      de données
* 3.a : |svg_rendersettings_22| |img_rendersettings| :ref:`Adapter le réglage de rendu <component_rendersettings>`
    * créer un réglage de rendu spécifique, par ex. pour la sortie en liste dans le FE
    * sélectionner une :ref:`variante du template « metamodels_prerendered » <component_templates>`
      pour une sortie individuelle
    * réglage de la page « jumpTo » pour la :ref:`vue détaillée <component_contentelements>`
* 3.b : |svg_rendersetting_22| |img_rendersetting| :ref:`Adapter les attributs dans le réglage de rendu <component_rendersettings>`
    * effectuer des réglages spécifiques sur les attributs - par ex. :ref:`la sortie d'images avec
      leur taille <rst_cookbook_templates_fe_work_with_images>`
    * sélectionner une :ref:`variante du template « mm_attr_<type> » <component_templates>` pour
      une sortie individuelle
* 4.a : |svg_dca_22| |img_dca| :ref:`Adapter le masque de saisie <component_dca>`
    * indiquer les clés pour la sortie du filtre, de la recherche, du tri, de la limite
    * choisir la zone du backend où le MetaModel doit apparaître, par ex. Contenus ou une zone
      propre
    * affichage sous forme de tableau dans le backend
    * droits pour l'édition
* 4.b : |svg_dca_setting_22| |img_dca_setting| :ref:`Adapter les attributs pour le masque de saisie <component_dca>`
    * classe CSS comme w50
    * champ obligatoire, lecture seule (Readonly)
    * option indiquant si l'attribut doit être filtrable et/ou consultable dans la liste du BE
    * ajouter des légendes pour subdiviser logiquement les masques de saisie plus grands
* 4.c : |svg_dca_groupsortsettings_22| |img_dca_groupsortsettings| :ref:`Créer un tri/groupement <component_dca>`
    * créer un tri standard ou d'autres tris pour la sélection dans la liste
* 4.d : |svg_dca_condition_22| |img_dca_condition| :ref:`Créer des conditions d'affichage <component_dca_visibility-conditions>`
    * les widgets de saisie peuvent être affichés ou masqués en fonction des valeurs d'autres
      widgets
* 5 : |svg_dca_combine_22| |img_dca_combine| :ref:`Créer les affectations saisie/rendu <component_dca-combine>`
    * attribuer une sélection de réglages de rendu et de masques de saisie aux groupes
      d'utilisateurs (BE) ou aux groupes de membres (FE)
* 6.a : |svg_filter_22| |img_filter| :ref:`Créer un filtre <component_filter>`
    * donner un nom au filtre
* 6.b : |svg_filter_setting_22| |img_filter_setting| :ref:`Créer des règles de filtre <component_filter>`
    * insérer les règles de filtre
    * des imbrications avec AND ou OR sont possibles
    * sans autre indication, toutes les règles de filtre sont automatiquement combinées avec AND

**Avec les adaptations effectuées, l'affichage dans le backend et le frontend devrait correspondre
aux souhaits individuels.**

Outre les options mentionnées, il existe d'autres possibilités décrites sur les pages liées.

Étape 4 : autres options pour la sortie de l'étape 2
------------------------------------------------------

- 2.c : élément de contenu « Liste MetaModel » de l'étape 2
    - sélectionner un filtre
    - définir un tri selon un attribut - :ref:`voir aussi le tri personnalisé <rst_cookbook_filter_custom-sql_sortierung-der-ausgabe-nach-mehr-als-einem-attribut-fest>`
      ou les :ref:`liens de tri <rst_cookbook_templates_fe_list_sorting>`
    - régler la limite et la pagination
- 3.a : créer dans l'article un :ref:`élément de contenu « Filtre MetaModel » <component_contentelements>`
- 3.b : sélectionner le MetaModel ainsi que le filtre (généralement identique à celui de la liste
  MM) avec les règles de filtre souhaitées

**Sur la page, le frontend devrait afficher un filtre avec les widgets de filtre correspondants
et la liste devrait réagir au filtrage.**

La sortie en frontend peut être adaptée avec différents réglages pour un :ref:`rst_cookbook_tips_seo`.

.. _component_workflow_tips:
Conseils :
----------

* pour les « débutants MM », il est recommandé de construire l'exemple
  :ref:`« Le premier MetaModel » <mm_first_index>`
* imprimer le cas échéant le :download:`« plan du site MM » </_download/MM_Lageplan_e-spin-Berlin.pdf>`
  et le garder à portée de main
* représenter graphiquement la structure de données - il n'est pas nécessaire d'indiquer tous les
  attributs - cela aide à la construction et à la communication avec les clients ainsi que pour les
  demandes de support
* lors de la création des Models, procéder « de l'extérieur vers l'intérieur » - dans l'exemple
  ci-dessus, d'abord le département et les projets, puis les collaborateurs - ainsi, les Models
  sont déjà disponibles dans la sélection lors de la création des attributs pour les références
  (ici la sélection simple)
* pour les structures de données plus importantes, les Models qui vont ensemble peuvent recevoir
  un « préfixe » propre comme « events », de sorte que les tables s'appellent par ex.
  « mm_events_categories », « mm_events_contacts », etc. - la liste des tables peut alors être
  filtrée sur « mm_events_ » et devient plus claire lors de l'édition
* créer les attributs de même type les uns à la suite des autres - avec « Enregistrer et créer un
  nouveau », le type d'attribut précédent est conservé, ce qui évite d'avoir à le sélectionner à
  nouveau
* pour les « indications auxiliaires » comme la civilité, les unités de mesure ou autres, il n'est
  pas nécessaire de créer à chaque fois un MetaModel comme référence - on peut par ex. résoudre
  cela avec :ref:`une construction de Model auxiliaire <rst_cookbook_specials_helper-models>`
* après avoir créé un Model ou un attribut, effectuer la migration de la base de données et vider
  le cache
* avant de commencer, vérifier si le Model ou les attributs doivent être multilingues - un
  changement ultérieur n'est pas facile à réaliser
* la création des attributs dans le réglage de rendu et le masque de saisie est simplifiée par le
  bouton « Tout ajouter »
* il existe une série de :ref:`listes de contrôle <rst_cookbook_checklists_index>` qui aident dans
  le travail
* de l'aide est disponible sur le `forum <https://community.contao.org/de/forumdisplay.php?149-MetaModels>`_
  et sur `Slack (#metamodels) <https://contao.slack.com/archives/CKGEBDV60>`_ - il est également
  possible de se faire accompagner par l'équipe MM sur des projets
  (`mail@metamodels.me <mailto:mail@metamodels.me>`_)


.. |br| raw:: html

   <br />

.. |img_db-schema_01| image:: /_img/screenshots/metamodel_first/db-schema_01.png
   :width: 400px

.. |img_new| image:: /_img/icons/new.gif
.. |img_fields| image:: /_img/icons/fields.png
.. |svg_fields_22| image:: /_img/icons_svg/fields.svg
   :width: 22px
.. |img_workflow_01| image:: /_img/screenshots/workflow/workflow_01.png
.. |svg_workflow_01| image:: /_img/screenshots/workflow/svg_workflow_01.png
.. |img_rendersettings| image:: /_img/icons/rendersettings.png
.. |svg_rendersettings_22| image:: /_img/icons_svg/rendersettings.svg
   :width: 22px
.. |img_rendersetting| image:: /_img/icons/rendersetting.png
.. |svg_rendersetting_22| image:: /_img/icons_svg/rendersetting.svg
   :width: 22px
.. |img_dca| image:: /_img/icons/dca.png
.. |svg_dca_22| image:: /_img/icons_svg/dca.svg
   :width: 22px
.. |img_dca_setting| image:: /_img/icons/dca_setting.png
.. |svg_dca_setting_22| image:: /_img/icons_svg/dca_setting.svg
   :width: 22px
.. |img_dca_groupsortsettings| image:: /_img/icons/dca_groupsortsettings.png
.. |svg_dca_groupsortsettings_22| image:: /_img/icons_svg/dca_groupsortsettings.svg
   :width: 22px
.. |img_dca_condition| image:: /_img/icons/dca_condition.png
.. |svg_dca_condition_22| image:: /_img/icons_svg/dca_condition.svg
   :width: 22px
.. |img_dca_combine| image:: /_img/icons/dca_combine.png
.. |svg_dca_combine_22| image:: /_img/icons_svg/dca_combine.svg
   :width: 22px
.. |img_filter| image:: /_img/icons/filter.png
.. |svg_filter_22| image:: /_img/icons_svg/filter.svg
   :width: 22px
.. |img_filter_setting| image:: /_img/icons/filter_setting.png
.. |svg_filter_setting_22| image:: /_img/icons_svg/filter_setting.svg
   :width: 22px
