.. _mm_first_conclusion:

Résumé et perspectives
========================

La création du premier MetaModel a permis de mettre en place un tableau simple
et de parcourir les étapes de travail fondamentales pour un MetaModel.

Avec le MetaModel « Liste des employés », la saisie dans le backend et
l'affichage dans le frontend sont réalisés. Cela ne représente naturellement
qu'une petite partie des possibilités de MetaModels, et même cet exemple simple
peut encore être développé.

Voici une petite liste de possibilités :

* modifier la structure de données - transformer le département en MetaModel
  distinct et le relier (relation) à la liste des employés
* dans le backend, des filtrages, tris et fonctions de recherche peuvent être
  ajoutés
* dans le frontend également, une extension avec filtrages, tris et fonctions
  de recherche serait possible

À titre d'illustration, les deux copies d'écran suivantes - d'une part le
backend avec un MetaModel séparé pour les départements (modification de
l'attribut « Département » de « Text » à « Sélection »)

|img_conclusion_01|

ainsi qu'une vue du frontend avec filtres et recherche (employés du
département « GF » dont le prénom commence par « F »)

|img_conclusion_02|

Le chapitre :ref:`mm_second_index` met en œuvre une structure de données plus
complexe, et le chapitre :ref:`mm_special_index` aborde certains aspects
particuliers comme le multilinguisme, les variantes, les tables enfants, etc.

.. |img_conclusion_01| image:: /_img/screenshots/metamodel_first/conclusion_01.png
.. |img_conclusion_02| image:: /_img/screenshots/metamodel_first/conclusion_02.png
