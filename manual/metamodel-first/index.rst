.. _mm_first_index:

Le premier MetaModel
=====================

La création du premier MetaModel a pour but de permettre une prise en main facile
de la mise en œuvre. La tâche pour cette première réalisation est une simple liste
d'employés avec seulement quelques informations. La liste doit pouvoir être remplie
dans le backend et peut être affichée dans le frontend sous forme de tableau.
Certains aspects comme les tris, les filtrages etc. ont volontairement été laissés
de côté.

La mise en œuvre s'appuie sur les :ref:`component_index` - vous y trouverez également
plus d'indications sur les templates utilisés et les relations possibles. Si vous
n'êtes pas sûr de la meilleure façon de démarrer, consultez
:ref:`l'article sur le déroulement du travail <component_workflow>`.

Pour avoir une meilleure vue d'ensemble de ce qui se trouve où, il existe le
:download:`« plan MM » </_download/MM_Lageplan_e-spin-Berlin.pdf>` à télécharger.

**Énoncé de la tâche :**

* Création d'une liste d'employés modifiable dans le backend
* Enregistrement des valeurs : nom, prénom, e-mail, département
* Champ supplémentaire pour la publication d'un enregistrement
* Sortie de la liste sous forme de tableau dans le frontend

**Prérequis :**

* Une version actuelle de Contao (LTS) - voir :ref:`manual_install`
* Une version actuelle de MetaModels compatible avec la version de Contao - voir
  :ref:`manual_install` et :ref:`rst_cookbook_checklists_mm-start`
* Une bonne maîtrise de Contao
* Compréhension des :ref:`component_index`

.. toctree::
    :hidden:
    :maxdepth: 1

    new-mm
    attribute
    rendersettings
    dca
    searchable-pages
    filter
    dca-combine
    contentelements
    conclusion
