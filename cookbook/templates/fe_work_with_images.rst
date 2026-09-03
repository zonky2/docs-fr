.. _rst_cookbook_templates_fe_work_with_images:

Travailler avec des images dans les templates
==================================================

Pour la sortie d'une ou plusieurs images dans MetaModels, l'attribut Fichier est disponible. Pour sélectionner un ou
plusieurs fichiers, un bouton dans le masque de saisie ouvre une fenêtre pop-up donnant accès à la gestion des
fichiers.

Dans les réglages de base de l'attribut, on peut définir différentes options telles que le chemin de base, une ou
plusieurs sélections, les types de fichiers, etc.

Dans la plupart des cas, on souhaite également afficher les fichiers images en tant qu'image. Les réglages
correspondants se trouvent, pour l'attribut, dans les réglages de rendu. Il faut alors cocher la case « Utiliser
comme champ image avec aperçu » et choisir une taille d'image (cela s'applique également à l'affichage dans le BE
dans la vue en liste). Il est en outre possible de choisir une image de remplacement ainsi qu'un affichage dans une
lightbox.

Ce réglage s'applique à l'affichage aussi bien pour le FE que pour le BE (si les images y sont affichées).

Dans un template FE personnalisé, l'affichage en tant qu'image nécessite la sortie du nœud html5 - |br|
par ex. ``<?= $arrItem['html5']['my_image'] ?>``.

Via la sélection ou l'adaptation du :ref:`template de l'attribut <component_templates>`, d'autres exigences pour la
sortie peuvent être définies, telles qu'une liste sous forme de ``ul`` ou ``div``, un balisage pour des galeries ou
des sliders, etc.

Ces possibilités de sortie et de personnalisation suffisent pour la grande majorité des besoins d'affichage. Mais si
des images doivent être affichées alors qu'elles sont intégrées par exemple via une :ref:`relation <component_relations>`
- via le nœud ``raw`` -, elles ne sont alors disponibles que comme image d'origine, via le chemin ou l'UUID.

Pour pouvoir également manipuler ces images dans son propre template, les extraits de code suivants doivent servir
d'aide.

Plus d'informations sur ces méthodes se trouvent dans le manuel Contao, à la section
`Image processing <https://docs.contao.org/dev/framework/image-processing/index.html>`_.

Sur le thème des `images responsives`, il existe une
`conférence (toujours d'actualité) de Peter Müller à la CK2016 <https://www.youtube.com/watch?v=ub8yROSQyQ4>`_.


Affichage d'une image intégrée via une sélection simple
------------------------------------------------------------

Insert-tags
...........

voir `Insert-Tags <https://docs.contao.org/manual/de/artikelverwaltung/insert-tags/#verschiedenes>`_

.. code-block:: php
   :linenos:

   <?php if (!empty($arrItem['raw']['speaker']['biography_image']): ?>
       {{image::<?= $arrItem['raw']['speaker']['biography_image'] ?>?width=180&height=180&mode=crop&class=img--circle}}
       <!-- ODER -->
       {{picture::<?= $arrItem['raw']['speaker']['biography_image'] ?>?size=_image_circle}}
       <!-- ODER -->
       {{figure::<?= $arrItem['raw']['speaker']['biography_image'] ?>?size=_image_circle&metadata[title]=<?= $arrItem['raw']['speaker']['full_name'] ?>}}
   <?php endif; ?>

Exemple pour ``$size`` (`voir <https://docs.contao.org/dev/framework/image-processing/image-sizes/index.html>`_) :

.. code-block:: yaml
   :linenos:

   # config/config.yml
   contao:
       image:
           sizes:
               _defaults:
                   formats:
                       jpg: [webp, jpg]
                       webp: [webp, jpg]
                       png: [webp, png]
                   densities: 0.5x, 2x, 3x
                   lazy_loading: true
                   resize_mode: proportional
               image_circle:
                   width: 180
                   height: 180
                   resize_mode: crop
                   zoom: 100
                   css_class: img--circle


Image-Studio FigureRenderer
...........................

* ``$from`` : chemin vers le fichier
* ``$size`` : voir ci-dessus
* ``$configuration`` : indications de configuration, par ex. métadonnées
* ``$template`` : template de sortie

.. code-block:: php
   :linenos:

   <?php
   if (!empty($arrItem['raw']['speaker']['biography_image'])) {
      $from          = $arrItem['raw']['speaker']['biography_image'];
      $size          = '_image_circle';
      $configuration = [];
      $template      = 'image';
      echo $container->get('contao.image.studio.figure_renderer')->render($from, $size, $configuration, $template);
   }
   ?>


Image-Studio FigureBuilder
..........................

voir `FigureBuilder <https://docs.contao.org/dev/framework/image-processing/image-studio/index.html#using-the-figurebuilder>`_

* ``fromPath`` : chemin vers le fichier
* ``setSize`` : voir ci-dessus
* ``$configuration`` : indications de configuration, par ex. métadonnées
* ``$template`` : template de sortie

.. code-block:: php
   :linenos:

   <?php
   if (!empty($arrItem['raw']['speaker']['biography_image'])) {
       $figure = $container
         ->get('contao.image.studio')
         ->createFigureBuilder()
         ->fromPath($arrItem['raw']['speaker']['biography_image'])
         ->setSize('_image_circle')
         ->build();

       $template = new FrontendTemplate('image');

       $figure->applyLegacyTemplateData($template);
       //$template->setData($figure->getLegacyTemplateData()); // Alternative
       echo $template->parse();
   }
   ?>


Image-Studio PictureFactory
...........................

voir `PictureFactory <https://docs.contao.org/dev/framework/image-processing/image-picture-factory/index.html#picture-factory>`_

* ``setSize`` : voir ci-dessus
* ``$data`` : données image + métadonnées
* ``$pictureTemplate`` : template de sortie

.. code-block:: php
   :linenos:

   <?php
   // würde man in Helper auslagern
   use Contao\FrontendTemplate;
   use Contao\StringUtil;
   use Contao\System;

   $container      = System::getContainer();
   $rootDir        = $container->getParameter('kernel.project_dir');
   $pictureFactory = $container->get('contao.image.picture_factory');

   // ...
   if (!empty($arrItem['raw']['speaker']['biography_image'])) {
      $staticUrl = $container->get('contao.assets.files_context')->getStaticUrl();
      $picture   = $pictureFactory->create($rootDir . '/' . $arrItem['raw']['speaker']['biography_image'], '_image_circle');

      $data = [
         'img'     => $picture->getImg($rootDir, $staticUrl),
         'sources' => $picture->getSources($rootDir, $staticUrl),
         'alt'     => StringUtil::specialcharsAttribute(''),
         'class'   => StringUtil::specialcharsAttribute(''),
      ];

      $pictureTemplate = new FrontendTemplate('picture_default');
      $pictureTemplate->setData($data);

      echo $pictureTemplate->parse();
   }
   ?>

.. note:: Cette page peut volontiers être complétée par d'autres extraits de code - dès que MM fonctionnera
   également avec des templates Twig, la page sera adaptée.


.. |br| raw:: html

   <br />
