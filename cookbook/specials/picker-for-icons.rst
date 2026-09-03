.. _rst_cookbook_specials_picker-for-icons:

Sélecteur d'icônes (Icon-Picker)
==================================

Si l'on souhaite doter des enregistrements d'une icône, on peut utiliser l'attribut Fichier ou, si les icônes sont
intégrées via une police, les classes CSS correspondantes. La sélection des icônes n'est alors cependant pas très
conviviale.

Pour Contao, il existe différentes extensions qui proposent un sélecteur d'icônes dédié.

Pour mettre également cette fonctionnalité à disposition dans MM, on pourrait créer un attribut personnalisé. La
plupart des sélecteurs d'icônes ne stockent que des chaînes de caractères ou des tableaux sérialisés, de sorte que,
avec de petites adaptations du DCA et des templates, on peut aussi utiliser l'attribut Texte.

Les adaptations pour les extensions de sélection courantes sont présentées ci-après :

- :ref:`RockSolid Icon Picker <picker_rst>`
- :ref:`Marco Cupic Font Awesome Icon Picker <picker_mcfa>`
- :ref:`NetGroup IconToolkit <picker_ng>`
- :ref:`Lukas Bableck SVG Icon-Picker <picker_lbsvg>`

Veuillez respecter les conditions de licence respectives des icônes ou des polices !


Prérequis
---------

Il faut d'abord créer un **attribut Texte**, y compris la migration et l'intégration dans le masque de saisie et
dans les réglages de rendu.

Pour les adaptations du DCA, un fichier PHP ``contao/dca/mm_employees.php`` doit être créé. Si le libellé
« LABEL NOT SET » apparaît au lieu du libellé attendu, :ref:`veuillez corriger cela selon le guide <component_translations_lns>`.

L'adaptation du DCA peut être reprise des exemples respectifs - il faut adapter le nom du MetaModel
(``mm_employees``) et le nom de colonne de l'attribut ``*_icon`` (par ex. ``rst_icon``).

Pour la sortie, des templates dédiés - dérivés de ``mm_attr_text`` - doivent être créés et sélectionnés dans les
réglages de rendu de l'attribut. On peut également y renseigner des indications CSS supplémentaires pour la taille ou
la couleur.


.. _picker_rst:
RockSolid Icon Picker
------------------------

`Extension sur Github <https://github.com/madeyourday/contao-rocksolid-icon-picker>`_.

L'extension fonctionne avec sa propre `police d'icônes <https://github.com/madeyourday/RockSolid-Icon-Font>`_ - les
fichiers SVG peuvent être convertis avec le `générateur de police SVG <https://github.com/madeyourday/SVG-Icon-Font-Generator>`_
et, le cas échéant, on peut également ajouter ses propres icônes SVG. Ceux qui utilisent un
`thème RST <https://rocksolidthemes.com/de/contao-themes>`_ trouveront les fichiers de police déjà prêts dans le
paquet du thème correspondant.

Adaptation du DCA :

.. code-block:: php
   :linenos:

   <?php
   // contao/dca/mm_employees.php
   $GLOBALS['TL_DCA']['mm_employees']['fields']['rst_icon']['inputType']        = 'rocksolid_icon_picker';
   $GLOBALS['TL_DCA']['mm_employees']['fields']['rst_icon']['eval']['iconFont'] = '/files/themes/iconfont/rocksolid-icons.svg';

Template :

.. code-block:: php
   :linenos:

   <?php
   // templates/mm_attr_text_rst_icon.html5
   <span class="<?= $this->additional_class ?>" data-icon="&#x<?= $this->raw ?>;"></span>

CSS :

.. code-block:: css
   :linenos:

   /* files/themes/css/icons.css */
   /* Icon font */
   @font-face {
     font-family: "RockSolid Icons";
     src: url("../iconfont/rocksolid-icons.woff2") format("woff2"), url("../iconfont/rocksolid-icons.svg") format("svg");
     font-weight: normal;
     font-style: normal;
   }

   /* Icon attribute */
   *[data-icon]:before,
   *[class^="icon-"]:before,
   *[class*=" icon-"]:before {
     font: 100%/1 "RockSolid Icons";
     -webkit-font-smoothing: antialiased;
     font-smoothing: antialiased;
     text-rendering: geometricPrecision;
     text-indent: 0;
     display: inline-block;
     position: relative;
     margin-right: 0.26667em;
   }
   *[data-icon]:before {
     content: attr(data-icon);
   }
   *[data-icon].after:before {
     content: none;
   }
   *[data-icon].after:after {
     font: 100%/1 "RockSolid Icons";
     content: attr(data-icon);
     -webkit-font-smoothing: antialiased;
     font-smoothing: antialiased;
     text-rendering: geometricPrecision;
     text-indent: 0;
     display: inline-block;
     position: relative;
     margin-left: 0.26667em;
   }

Rendu BE & FE :

|img_rst_01.png|

|img_rst_02.png|


.. _picker_mcfa:
Marco Cupic Font Awesome Icon Picker
----------------------------------------

`Extension sur Github <https://github.com/markocupic/fontawesome-icon-picker-bundle>`_.

À partir de la version 7, aucune indication dans le ``config.yaml`` n'est nécessaire pour le widget - toutefois, les
données des icônes sont récupérées directement depuis le serveur Fontawesome. Ceux qui ne le souhaitent pas peuvent
aussi intégrer les fichiers directement sur le serveur web. Pour cela, on peut télécharger le paquet d'icônes depuis
le `site web <https://fontawesome.com/download>`_ et le décompresser. Les dossiers ``js/``, ``metadata/`` et
``webfonts/`` doivent être placés sur le serveur web dans un dossier correspondant sous ``files/``.

La configuration se présente alors par exemple comme suit :

.. code-block:: php
   :linenos:

   # config/config.yaml
   markocupic_fontawesome_icon_picker:
     fontawesome_source_path: 'files/themes/fa7_icons/js/all.min.js'
     fontawesome_allowed_styles:
       - fa-regular
       - fa-solid
       - fa-brands
     fontawesome_meta_file_path: 'files/themes/fa7_icons/metadata/icons.yml'

Pour les icônes, selon la configuration de ``fontawesome_allowed_styles`` et les icônes disponibles, les libellés R
Regular, S Solid, B Brands, etc. sont disponibles comme boutons de sélection - l'ordre détermine le style d'icône
affiché dans le widget.

Les utilisateurs d'une variante FA-Pro se réfèrent à la description du
`Readme <https://github.com/markocupic/fontawesome-icon-picker-bundle?tab=readme-ov-file#configuration>`_.

Il faut noter que, pour les deux variantes, il faut soi-même intégrer les polices d'icônes pour le FE via CSS.

Adaptation du DCA :

.. code-block:: php
   :linenos:

   <?php
   // contao/dca/mm_employees.php
   $GLOBALS['TL_DCA']['mm_employees']['fields']['mcfa_icon']['inputType'] = 'fontawesomeIconPicker';

Template :

Comme le stockage se fait sous forme de tableau sérialisé, il faut créer le template aussi bien pour ``html5`` que
pour ``text``.

.. code-block:: php
   :linenos:

   <?php
   // templates/mm_attr_text_mcfa_icon.html5
   /** Nach Deserialisierung steht ein Array mit drei Angaben zur Verfügung z. B.
   * Array
   * (
   *     [0] => circle-check
   *     [1] => fa-regular
   *     [2] => f058
   * )
   */

   $mcfaData = \Contao\StringUtil::deserialize($this->raw, true);
   ?>
   <i class="<?= $mcfaData[1] ?? '' ?> fa-<?= $mcfaData[0] ?? '' ?><?= $this->additional_class ?>"></i>


.. code-block:: php
   :linenos:

   <?php
   // templates/mm_attr_text_mcfa_icon.text
   <?php
   $mcfaData = \Contao\StringUtil::deserialize($this->raw, true);
   ?>
   <?= $mcfaData[1] ?? '' ?> fa-<?= $mcfaData[0] ?? '' ?>

Rendu BE & FE :

|img_mcfa_01.png|

|img_mcfa_02.png|


.. _picker_ng:
NetGroup IconToolkit
------------------------

`Extension sur Github <https://github.com/netgroupgmbh/contao-icontoolkit>`_.

L'extension est conçue pour `Font Awesome <https://fontawesome.com/>`_ et le fournit en version 7.1. Il est
cependant aussi possible de charger ses propres polices d'icônes ou un jeu d'icônes plus récent. Un module FE est
disponible pour l'intégration de la police.

Adaptation du DCA :

.. code-block:: php
   :linenos:

   <?php
   // contao/dca/mm_employees.php
   use NetGroup\IconToolkit\Classes\Contao\Widgets\IconPickerWidget;

   $GLOBALS['TL_DCA']['mm_employees']['fields']['ng_icon']['inputType'] = IconPickerWidget::TYPE;

Template :

.. code-block:: php
   :linenos:

   <?php
   // templates/mm_attr_text_ng_icon.html5
   <i class="<?= $this->raw ?><?= $this->additional_class ?>"></i>

CSS :

.. code-block:: css
   :linenos:

   // /* Klassen 'fa-2x fa-green' in Rendersettings */
   .fa-green {
     color: #6bb710;
   }

Rendu BE & FE :

|img_ng_01.png|

|img_ng_02.png|


.. _picker_lbsvg:
Lukas Bableck SVG Icon-Picker
---------------------------------

`Extension sur Github <https://github.com/lukasbableck/contao-svg-icon-picker-bundle>`_.

L'extension est conçue pour `Font Awesome <https://fontawesome.com/>`_ - il est cependant aussi possible de charger
ses propres icônes SVG, comme par ex. `Lucide <https://lucide.dev/icons/>`_ ou `Bootstrap <https://icons.getbootstrap.com>`_.

Les icônes sont diffusées comme de « vrais » SVG, ce qui permet des adaptations de la couleur, etc.

Adaptation du DCA :

.. code-block:: php
   :linenos:

   <?php
   // contao/dca/mm_employees.php
   $GLOBALS['TL_DCA']['mm_employees']['fields']['lbsvg_icon']['inputType']                 = 'svgIconPicker';
   $GLOBALS['TL_DCA']['mm_employees']['fields']['lbsvg_icon']['eval']['sourceDirectory']   = '/files/themes/svg-icons/svgs-full/regular';
   $GLOBALS['TL_DCA']['mm_employees']['fields']['lbsvg_icon']['eval']['metadataDirectory'] = '/files/themes/svg-icons/metadata';

Template :

.. code-block:: php
   :linenos:

   <?php
   // templates/mm_attr_text_lbsvg_icon.html5
   use Contao\System;
   use Lukasbableck\ContaoSVGIconPickerBundle\Twig\Extension;

   $rootDir = System::getContainer()->getParameter('kernel.project_dir');
   $svgTool = new Extension($rootDir);

   $svg = \str_replace('class="', 'class="' . \trim($this->additional_class) . ' ', $svgTool->renderSVG($this->raw));
   ?>

   <?= $svg ?>

CSS :

.. code-block:: css
   :linenos:

   /* Klassen 'lbsvg_icon lbsvg_green' in Rendersettings */
   svg.lbsvg_icon {
     width: 33px;
     height: 33px;
   }

   svg.lbsvg_green {
     color: #6bb710;
   }


Rendu BE & FE :

|img_lbsvg_01.png|

|img_lbsvg_02.png|


Remarques sur Fontawesome
----------------------------

Le paquet d'icônes Fontawesome peut être téléchargé depuis le `site web <https://fontawesome.com/download>`_. La
« variante gratuite » contient les styles Regular, Solid et Brands. Si l'on souhaite utiliser les icônes SVG, il est
recommandé d'intégrer le dossier ``svg-full/`` - toutes les icônes y sont carrées avec une marge correspondante.

Si le CSS de Fontawesome est également diffusé dans le FE, comme par ex. avec NG IconToolkit, les classes de style
correspondantes, telles que ``fa-2x`` pour une taille double, peuvent être indiquées dans les réglages de rendu. Un
aperçu de ces indications se trouve dans la `documentation FA <https://docs.fontawesome.com/web/style/style-cheatsheet>`_.


Remarques sur les icônes Lucide
-----------------------------------

À partir de la version 5.5, Contao utilise dans le backend des icônes du paquet `Lucide <https://lucide.dev/icons/>`_.
Pour les utiliser également dans le FE, le plus simple est d'utiliser l'extension :ref:`SVG Icon-Picker <picker_lbsvg>`.

Le paquet complet peut être téléchargé et décompressé depuis Github via
`« Code > Download ZIP » <https://github.com/lucide-icons/lucide/archive/refs/heads/main.zip>`_.
Le dossier ``icons/`` contient toutes les icônes SVG et doit être placé sur le serveur web dans un dossier approprié
sous ``files``.

Ensuite, le dossier doit être indiqué dans la configuration - par ex.

.. code-block:: php
   :linenos:

   <?php
   // contao/dca/mm_employees.php
   $GLOBALS['TL_DCA']['mm_employees']['fields']['lbsvg_icon']['inputType']                 = 'svgIconPicker';
   $GLOBALS['TL_DCA']['mm_employees']['fields']['lbsvg_icon']['eval']['sourceDirectory']   = '/files/themes/lucide-icons';
   //$GLOBALS['TL_DCA']['mm_employees']['fields']['lbsvg_icon']['eval']['metadataDirectory'] = '/files/themes/svg-icons/metadata';

Lucide ne fournit pas automatiquement les icônes sous forme de police. Les fichiers peuvent cependant être convertis
en police. Les fichiers SVG doivent au préalable être convertis de traits en remplissages - par ex. à l'aide de
l'outil Iconly « `Convert SVG Strokes to Fills <https://iconly.io/tools/svg-convert-stroke-to-fill>`_ » ou du paquet
npm `« svg-outline-stroke » <https://www.npmjs.com/package/svg-outline-stroke>`_. La police d'icônes Lucide peut
ensuite être générée avec `IcoMoon <https://icomoon.io/>`_ ou le paquet npm
`« fantasticon » <https://github.com/tancredi/fantasticon>`_.


Remarques sur les icônes Bootstrap
--------------------------------------

Bootstrap 5 comprend son propre paquet d'icônes avec des fichiers SVG et une police au format woff et woff2.

On peut télécharger le paquet depuis le `site web de Bootstrap <https://icons.getbootstrap.com/#download>`_, le
décompresser et le placer dans un dossier approprié sous ``files``.

Pour utiliser les fichiers SVG, on peut employer l'extension :ref:`SVG Icon-Picker <picker_lbsvg>` - il faut adapter
en conséquence le chemin de ``sourceDirectory`` dans la configuration du DCA.

Si l'on préfère la `sortie sous forme de police <https://icons.getbootstrap.com/#icon-font>`_ dans le FE, on peut,
en utilisant l'extension :ref:`SVG Icon-Picker <picker_lbsvg>`, utiliser les icônes SVG pour la sélection dans le
backend et adapter le template pour le FE - par ex.

.. code-block:: php
   :linenos:

   // templates/mm_attr_text_lbsvg_bs5_icon.html5
   <i class="bi bi-<?= basename($this->raw, '.svg') ?><?= $this->additional_class ?>"></i>

Il faut en outre intégrer le CSS BS ``bootstrap-icons.min.css`` pour le FE en conséquence - le fichier est inclus
dans le paquet de téléchargement.

Une adaptation du style des icônes est possible par exemple avec les
`classes « text-* » <https://getbootstrap.com/docs/5.3/utilities/colors/#colors>`_ ou les
`classes « fs-* » <https://getbootstrap.com/docs/5.3/utilities/text/#font-size>`_ ; ces classes peuvent être
renseignées dans les réglages de rendu de l'attribut. Pour cela, le CSS Bootstrap « normal » doit également être
intégré `Bootstrap-CSS <https://getbootstrap.com/docs/5.3/getting-started/download/>`_.





.. |img_lbsvg_01.png| image:: /_img/screenshots/cookbook/specials/icon_picker/lbsvg_01.png
.. |img_lbsvg_02.png| image:: /_img/screenshots/cookbook/specials/icon_picker/lbsvg_02.png
.. |img_mcfa_01.png| image:: /_img/screenshots/cookbook/specials/icon_picker/mcfa_01.png
.. |img_mcfa_02.png| image:: /_img/screenshots/cookbook/specials/icon_picker/mcfa_02.png
.. |img_ng_01.png| image:: /_img/screenshots/cookbook/specials/icon_picker/ng_01.png
.. |img_ng_02.png| image:: /_img/screenshots/cookbook/specials/icon_picker/ng_02.png
.. |img_rst_01.png| image:: /_img/screenshots/cookbook/specials/icon_picker/rst_01.png
.. |img_rst_02.png| image:: /_img/screenshots/cookbook/specials/icon_picker/rst_02.png

.. |br| raw:: html

   <br />
