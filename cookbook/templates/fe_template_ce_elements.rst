.. _rst_cookbook_templates_fe_template_ce_elements:

Créer des templates FE via des éléments de contenu
=======================================================

.. _rst_cookbook_templates_fe_template_ce_elements_youtube:
CE YouTube
----------

Pour des sorties plus complexes, comme par ex. avec le CE YouTube, il existe, outre l'ID YT, différents autres
paramètres qui peuvent être réglés ou affichés. On peut intégrer ces CE via le template MM et les utiliser pour la
sortie. L'intégration des CE peut se faire aussi bien dans le template des réglages de rendu
(``metamodels_prerendered.html5``) que dans les templates des attributs (``mm_attr_*.html5``).

La démarche est illustrée ci-après à l'aide du CE Youtube. On crée un attribut Texte dans lequel l'ID YT est
stockée. On crée en outre un nouveau template ``mm_attr_text_video_yt.html5``, qui est sélectionné dans les réglages
de rendu au niveau des réglages de l'attribut.

Saisir le code suivant dans le template :

.. code-block:: php
   :linenos:

   <?php

   use Contao\ContentModel;
   use Contao\ContentYouTube;

   $contentData['type']           = 'youtube';
   $contentData['youtube']        = $this->raw . '?rel=0';
   $contentData['youtubeOptions'] = serialize(['youtube_nocookie']);
   $contentData['playerSize']     = serialize(['560', '315']);
   $contentData['playerAspect']   = '16:9';

   $model = new ContentModel();
   $model->setRow($contentData);

   $content = new ContentYouTube($model);

   echo $content->generate();


La structure de base est ainsi déjà terminée et peut être étendue selon les besoins. Les paramètres possibles
peuvent être déterminés à partir des classes d'éléments de Contao -
par ex. `ContentYouTube <https://github.com/contao/contao/blob/6cfb659affeb526539d776b430bcafa4b0324849/core-bundle/src/Resources/contao/elements/ContentYouTube.php>`_.

Les paramètres peuvent être saisis en dur comme dans l'exemple - il serait cependant également possible d'intégrer
des valeurs issues d'autres attributs via ``$this->row['yt_aspect']`` dans le template de l'attribut, ou
``$arrItem['text']['yt_aspect']`` dans le template des réglages de rendu.

Dans les réglages de rendu, une saisie via les paramètres du module CE/FE serait également possible -
voir :ref:`rst_cookbook_templates_fe_list_parameters`.

Pour une présentation compacte et une saisie dans le masque de saisie, on pourrait également créer, avec l'attribut
MCW, une « saisie multiple » sur une seule ligne - voir :ref:`rst_extended_attribute_mcw`.


.. _rst_cookbook_templates_fe_template_ce_elements_rstslider:
Module FE RockSolid Slider
------------------------------

Si l'on souhaite afficher des sliders prêts à l'emploi, comme le
`RockSolid Slider <https://rocksolidthemes.com/de/contao/plugins/responsive-slider>`_, en tant que contenu dans MM,
il existe, comme toujours, différentes approches - en voici une à titre d'exemple :

On crée d'abord un slider, par ex. un slider d'images, via le point de navigation correspondant dans le BE et on y
sélectionne les images souhaitées. Pour simplifier les réglages de configuration, on crée en outre un module FE de
type « RockSolid Slider » et on y effectue les réglages souhaités pour la taille, l'animation, la navigation, etc.
- l'ID du module FE, par ex. ``55``, sera nécessaire plus tard dans le template.

Dans MM, on crée un attribut de type Sélection simple [Select] avec les réglages suivants :

* Table source : tl_rocksolid_slider
* Colonne ID : id
* Colonne valeur : name
* Colonne alias : id
* Tri de la sélection : name

Cela permet ensuite de sélectionner un slider dans le masque de saisie - l'attribut est bien entendu également
intégré dans le masque de saisie.

On crée en outre un template dédié, par ex. ``mm_attr_select_rst_slider.html5``, avec le contenu suivant :

.. code-block:: php
   :linenos:

   <?php
   $moduleData['type']                      = 'rocksolid_slider';
   $moduleData['rsts_id']                   = $this->raw['id'];
   $moduleData['rsts_import_settings']      = 1;
   $moduleData['rsts_import_settings_from'] = 55;

   $model = new \Contao\ModuleModel();
   $model->setRow($moduleData);

   $module = new MadeYourDay\RockSolidSlider\Module\Slider($model);

   echo $module->generate();

Le type doit impérativement être indiqué pour que les classes CSS appropriées pour le slider soient intégrées dans
le code source ; ``55`` est l'ID de module des réglages.

Dans les réglages de rendu pour la sortie, l'attribut est également intégré, et le template
``mm_attr_select_rst_slider`` est sélectionné dans les réglages de l'attribut.

La manière d'obtenir les paramètres de façon dynamique dans le template est décrite dans la section précédente et
peut se faire de manière analogue ici.
