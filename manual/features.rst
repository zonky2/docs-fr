.. _rst_features:

Aperçu des fonctions
====================

Modèles de données
------------------

MetaModels vous permet de concevoir des modèles de données facilement et de manière (presque) illimitée depuis le
backend de Contao, sans aucune compétence en programmation. Pour construire des modèles de données complexes,
différentes :ref:`relations <component_relations>` sont disponibles afin de stocker les données dans des tables
séparées et de les relier entre elles - voir la `normalisation <https://de.wikipedia.org/wiki/Normalisierung_(Datenbank)>`_.

Dans les modèles de données, différents types de données sont disponibles pour les champs (attributs) comme, par
exemple, le texte, les images, les nombres, les dates et les fichiers - :ref:`voici un aperçu des types de données par
attribut <component_data-in-attributes>` ainsi qu'une :ref:`liste de tous les attributs <component_attribute_index>`.
Si vous atteignez une limite parce que le type de donnée souhaité n'est pas disponible, il est aussi possible de
l'implémenter soi-même avec l':ref:`API MM <ref_api>`.

Il est aussi possible de connecter les tables aux autres tables du Contao Core, d'établir des :ref:`« connexions
parent-enfant » <component_relations_child-tables>` ou de mettre en œuvre des :ref:`saisies de variantes
<component_relations_variants>`.


Masques de saisie
-----------------

Vous pouvez concevoir des masques de saisie complexes pour le backend, permettant aux « rédacteurs » de conserver le
« look-and-feel » habituel de Contao. Au sein d'un masque de saisie, il est possible de réagir à la saisie de valeurs
ou de cases à cocher pour afficher, au choix, différentes sous-palettes - voir :ref:`component_dca_visibility-conditions`.

Pour une meilleure orientation dans les données, l'affichage peut être complété par différents filtres, fonctions de
recherche et de regroupement.

Le système de droits flexible développé pour MetaModels permet de définir des vues backend différentes pour les
groupes d'utilisateurs rédacteurs et administrateurs.

Le backend peut en outre être personnalisé de manière à ce que seuls certains groupes aient accès à certains champs
de saisie, et l'ordre de ces champs peut également être adapté individuellement par groupe d'utilisateurs.


Multilinguisme
--------------

Dès le départ, MetaModels a été conçu avec l'exigence du multilinguisme. Les attributs peuvent donc prendre en charge
la traduction des données qu'ils stockent dans plusieurs langues. Il suffit, dans le backend, de changer de langue à
l'aide du sélecteur de langue pour pouvoir modifier immédiatement l'enregistrement dans la langue choisie.

Le meilleur dans tout cela : les attributs qui ne sont pas traduisibles ne sont pas traduits non plus. Cela permet
par exemple de ne rendre traduisibles que le nom et la description d'un produit, mais pas la référence produit ni les
dimensions. Cette manière de procéder réduit la redondance des données à saisir.

:ref:`En savoir plus sur les réglages et la gestion du multilinguisme au niveau des composants d'un MetaModel.
<component_multi-language>`


Filtres
-------

MetaModels dispose d'un système de filtres puissant, qui permet également de réaliser des tâches complexes.
L'administrateur du site peut adapter entièrement les interactions des filtres à ses besoins. Ceci se fait en
configurant et en combinant les réglages de filtres et leurs paramètres.

MetaModels est fourni avec différents réglages de filtres permettant de générer des champs de saisie de filtrage en
frontend, comme par exemple des menus de sélection, des filtres par plage, la recherche en texte libre, etc. -
:ref:`un aperçu est disponible ici <component_filter_list>` ainsi que :ref:`ici, pour savoir quels attributs peuvent
être filtrés et comment <component_data-in-attributes>`.

En combinant ces filtres avec des réglages de filtres tels que des conditions ET/OU ou des requêtes SQL
personnalisées, on obtient des filtres complexes et interactifs.

MetaModels n'impose aucune limite à la combinaison des filtres et maîtrise même des scénarios de filtrage extrêmement
complexes. Grâce à la structure ouverte de l':ref:`API MM <ref_api>`, vous pouvez également programmer vos propres
règles de filtre avec un minimum d'effort.


Vues dynamiques
---------------

Grâce aux réglages de rendu, MetaModels a repris le concept de template « partiel » de Contao sous une forme
enrichie. L'utilisateur peut personnaliser chaque aspect des vues, au niveau des attributs comme des enregistrements.

De nombreux réglages généraux peuvent être définis dans la configuration du backend. Ils peuvent toutefois être
écrasés, adaptés finement ou même totalement ignorés en définissant un template propre au niveau des attributs ou des
enregistrements. Ces réglages de rendu offrent la manière la plus flexible de définir des « vues de données ».

Le concepteur peut définir une vue totalement différente pour chaque usage, qu'il s'agisse d'une simple sortie en
liste, d'une accroche pour la page d'accueil ou d'une vue de détail d'un enregistrement, ainsi que le moment et
l'endroit où elle doit être utilisée.

La page « :ref:`component_templates` » explique la hiérarchie et la structure des templates.


Extensions
----------

Pour des tâches spécifiques, il existe des paquets supplémentaires qui complètent ou étendent les fonctionnalités de
MetaModels, comme par exemple une recherche par périmètre géographique, une liste de favoris, l'édition en frontend
ou une interface avec la boutique `Isotope`.

Un aperçu est disponible ici : :ref:`extended_index`


Perspectives
------------

Nous travaillons continuellement à enrichir l'éventail des fonctions de MetaModels. Une mise en œuvre rapide de
nouvelles fonctions n'est possible qu'avec un soutien financier ou la mise à disposition de développements sur
commande - informations à ce sujet sur le `site du projet MetaModels <https://now.metamodel.me>`_ ou en contactant
directement l'équipe MM : `mail@metamodels.me <mailto:mail@metamodels.me>`_.
