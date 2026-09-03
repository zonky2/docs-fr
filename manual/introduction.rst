Introduction à MetaModels
=========================

.. _introdution_was-ist-metamodels:

Qu'est-ce que MetaModels ?
--------------------------

MetaModels est une extension pour le CMS Contao qui permet de gérer toutes sortes de contenus structurés sans
programmation. Que ce soit un catalogue de produits, un calendrier d'événements, une liste d'employés, des biens en
location ou un plan de menus — quiconque a besoin dans Contao d'une gestion de données personnalisée avec des
champs individuels, du filtrage, du tri et une sortie multilingue trouve dans MetaModels une solution clé en main.

L'avantage décisif : plutôt que de faire développer une extension spécifique pour chaque nouveau besoin, les
administrateurs peuvent créer de nouvelles structures de données entièrement depuis le backend de Contao — sans
programmation et sans développeur externe. Les adaptations individuelles peuvent ainsi être mises en œuvre
rapidement et de manière autonome, même lorsque les besoins évoluent en cours d'exploitation.

MetaModels prend en charge de nombreux types de champs — textes, listes de sélection, dates, fichiers, champs
oui/non, et bien d'autres encore — et les restitue en frontend sous forme de listes, de vues détaillées ou de
sorties filtrées. Les rédacteurs saisissent leurs contenus dans des masques de saisie clairs, exactement comme ils
en ont l'habitude dans les autres parties de Contao.

Vous trouverez plus de détails sur les fonctions dans :ref:`rst_features`.

Ce qui a été réalisé avec MetaModels en pratique est présenté dans la
`vitrine MetaModels <https://now.metamodel.me/en/showcase>`_ ou dans la
`présentation donnée à la CK17 <https://www.e-spin.de/metamodels-vortrag-contao-konferenz-2017.html>`_.

Une `équipe active autour de MetaModels <https://now.metamodel.me/de/ueber-uns/team>`_ vous accompagne dans sa mise
en œuvre à l'aide de ce manuel, ainsi que via le
`forum Contao <https://community.contao.org/en/forumdisplay.php?184-MetaModels>`_ et le
`canal Slack <https://contao.slack.com/archives/CKGEBDV60>`_.


MetaModels comparé à d'autres outils
------------------------------------

MetaModels est particulièrement le bon choix lorsqu'un site a besoin de zones de données personnalisées qui vont
au-delà des simples éléments de contenu — et lorsque cette solution doit rester maintenable, extensible et
utilisable par les rédacteurs de manière habituelle.

Sa vraie force réside dans la répartition du travail : un administrateur configure une fois pour toutes le modèle
de données — champs, masques de saisie, filtres et sortie. Les rédacteurs entretiennent ensuite les contenus de
manière autonome, sans avoir besoin de connaissances techniques particulières.

Comparé à une extension sur mesure, MetaModels offre un avantage décisif : les modifications de la structure et de
la sortie sont possibles à tout moment depuis le backend, sans connaissances en programmation et sans déploiement.
Pour un produit destiné à être distribué et empaqueté (par exemple une extension commerciale), une extension propre
reste en revanche plus pertinente.

Pour exploiter pleinement les possibilités de MetaModels — par exemple ses propres templates, des filtres SQL
complexes ou des hooks — des connaissances de base en HTML, SQL, dans le système de templates de Contao et en PHP
sont un plus. Pour les cas d'usage standard, le backend suffit à lui seul.


Comment démarrer ?
------------------

Pour qui découvre MetaModels, voici le moyen le plus simple de démarrer :

**1. Installation** |br|
MetaModels s'installe via le Contao Manager ou Composer. Vous trouverez un guide à ce sujet dans la section
:ref:`manual_install`.

**2. Créer son premier MetaModel** |br|
La section ":ref:`mm_first_index`" présente les concepts essentiels à l'aide d'un exemple concret :

- créer un modèle de données
- définir les attributs (champs)
- configurer un masque de saisie
- configurer la sortie en frontend
- créer et intégrer des filtres

**3. Checklist pour bien démarrer** |br|
La page :ref:`component_workflow` résume de façon compacte les étapes habituelles pour créer un nouveau MetaModel —
utile comme aide-mémoire pour vos premiers projets.

**Conseil pour démarrer :** |br|
Un :ref:`exemple simple <mm_first_index>` — par exemple une liste d'employés avec nom, fonction et photo — est idéal
pour s'exercer. Il contient les briques essentielles (attributs, masque de saisie, sortie, filtrage) tout en restant
suffisamment simple pour bien comprendre les liens entre elles. Pour vous repérer, gardez à portée de main le
:download:`"MM-Lageplan" </_download/MM_Lageplan_e-spin-Berlin.pdf>`.

En cas de questions, le `forum Contao <https://community.contao.org/en/forumdisplay.php?184-MetaModels>`_ et le
`canal Slack #metamodels <https://contao.slack.com/archives/CKGEBDV60>`_ peuvent vous aider - pour des tâches plus
complexes, une personne de l'équipe MM peut vous conseiller ou intervenir comme « MM-Coach » ; contact via
`mail@metamodels.me <mailto:mail@metamodels.me>`_.


Histoire de MetaModels
----------------------

MetaModels a démarré en 2012 comme la « next generation » de la célèbre et très appréciée extension 'Catalog' - la
version 1.0 a été publiée en mai 2013.

Au fil du temps, 'Catalog' est devenue une extension complexe offrant de nombreuses possibilités à Contao. Mais il
devenait malheureusement de plus en plus difficile de la maintenir et d'ajouter de nouvelles fonctions.

Les expériences acquises lors du développement de Catalog 1 et Catalog 2 ont rendu évident qu'un « Catalog 3 »
nécessiterait un nouveau départ complet.

C'est sur cette base que nous avons développé, sous le nom "MetaModels", une extension entièrement nouvelle
intégrant de nombreux paradigmes de programmation modernes. Notre but était de développer une extension reposant
sur un code de base flexible et extensible.

Avec la version 2.0 de MetaModels pour Contao 3.x, le résultat de nombreuses heures de discussion sur la « meilleure
solution » et d'un travail de programmation considérable a vu le jour.

Le développement s'est poursuivi avec la version 2.1, migration de la 2.0 vers Contao 4.4. Ces changements ont
permis d'adapter beaucoup de choses dans l'« infrastructure » sous-jacente, de couper les « vieilles habitudes »,
de corriger de nombreux petits bugs et de passer les requêtes en base de données à un style Symfony. Une synthèse
pour MM 2.2 est :ref:`disponible ici <new_in_mm220>`.

Le chemin s'est poursuivi via :ref:`MM 2.3 pour Contao 4.13 <new_in_mm230>` jusqu'à
:ref:`MM 2.4 pour Contao 5.3 <new_in_mm240>` avec davantage de composants standards issus de Symfony - un MM 2.5
pour Contao 5.7 est en cours de développement.

Des travaux de planification sont également déjà en cours pour MM 3.0 - :ref:`voir ici <planning_mm30>`.


Ressources
----------

* `Site du projet MetaModels <https://now.metamodel.me>`_
* `MetaModels chez Github <https://github.com/MetaModels>`_
* `Manuel MetaModels chez Github <https://github.com/MetaModels/docs-fr>`_
* `Sous-forum MetaModels de la communauté Contao <https://community.contao.org/en/forumdisplay.php?184-MetaModels>`_
* `MetaModels sur Slack Contao #metamodels <https://contao.slack.com/archives/CKGEBDV60>`_
* :download:`"MM-Lageplan" </_download/MM_Lageplan_e-spin-Berlin.pdf>`


.. |br| raw:: html

   <br />
