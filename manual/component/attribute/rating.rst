.. _component_attribute_rating:

|svg_attr_rating_22| |img_star_full| Évaluation
===============================================

L'attribut « Évaluation » met à disposition un système de notation par étoiles.
Les visiteurs peuvent évaluer les items via un widget AJAX en frontend. Dans le
backend, le nombre d'évaluations et la valeur moyenne sont affichés. Cas
d'utilisation typiques :

* Évaluations de produits dans des boutiques
* Notation d'articles, de recettes ou d'événements
* Enquêtes auprès des utilisateurs avec échelle d'étoiles

L'évaluation proprement dite s'effectue exclusivement via AJAX depuis le frontend
— le champ est en lecture seule dans le backend. Un blocage basé sur la session est
appliqué par visiteur et par item, afin d'empêcher les évaluations multiples.


Installation
------------

L'attribut s'installe via le **Contao Manager** ou **Composer** :

.. code-block:: bash

   composer require metamodels/attribute_rating


Réglages lors de la création de l'attribut
-------------------------------------------

Outre les réglages généraux de l'attribut, l'attribut propose les options
spécifiques suivantes :

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Option
     - Description
   * - Valeur maximale
     - Détermine le nombre maximal d'étoiles pouvant être attribuées (par ex.
       ``5`` pour une évaluation à cinq étoiles).
   * - Notations à moitié
     - Active des pas de 0,5 au lieu de nombres entiers, de sorte que par ex.
       3,5 sur 5 étoiles soit possible.
   * - Image pour « étoile vide »
     - Image propre affichée comme étoile non remplie. Si aucune image n'est
       choisie, l'icône par défaut de l'extension est utilisée.
   * - Image pour « étoile pleine »
     - Image propre affichée comme étoile remplie.
   * - Image pour l'effet de survol
     - Image propre affichée lors du survol avec la souris.


Réglages dans les réglages de rendu
-------------------------------------

L'attribut possède un réglage de rendu propre :

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Option
     - Description
   * - Désactiver le vote
     - Désactive la possibilité de voter en frontend pour ce réglage de
       sortie. Le résultat est alors uniquement affiché, sans qu'une nouvelle
       évaluation puisse être soumise.
   * - Template
     - Sélection d'un template propre pour l'affichage de l'évaluation.
   * - Classe CSS
     - Classe CSS optionnelle ajoutée à l'élément de sortie.


Réglages dans le masque de saisie
-----------------------------------

L'attribut est en lecture seule dans le backend — les évaluations ne peuvent être
soumises que via le widget AJAX en frontend. S'il est ajouté à un masque de
saisie, la moyenne d'évaluation actuelle ainsi que le nombre de votes sont
affichés.

**Présentation**

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Option
     - Description
   * - Classe backend
     - Classes CSS pour l'affichage dans le formulaire du backend.
   * - Template pour le backend
     - Sélection d'un template de widget propre pour le formulaire du backend.


Règles de filtre
-------------------

L'attribut Évaluation ne prend en charge aucune règle de filtre propre — les
données d'évaluation ne peuvent pas être utilisées directement comme critère de
filtrage en frontend. Un tri selon l'évaluation (valeur moyenne, puis nombre de
votes) est toutefois possible.


Fonctions particulières
-------------------------

**Stockage**

Les données d'évaluation ne sont **pas** enregistrées dans la table du MetaModel,
mais dans une table propre ``tl_metamodel_rating`` avec les colonnes suivantes :

* ``mid`` – ID du MetaModel
* ``aid`` – ID de l'attribut
* ``iid`` – ID de l'item
* ``votecount`` – nombre de votes soumis
* ``meanvalue`` – valeur moyenne calculée sous forme de pourcentage (``double``)

**Logique de vote**

Chaque vote soumis est traité via AJAX. MetaModels vérifie, à l'aide de la
session du visiteur, si un vote a déjà été soumis pour cet item. Le calcul de la
valeur moyenne s'effectue selon la formule suivante :

``(1 / (rating_max × votecount)) × (valeur totale précédente + nouveau vote)``

La valeur est enregistrée sous forme de pourcentage (0–1).

**Icônes par défaut**

Si aucune image propre n'est choisie pour les symboles d'étoile, l'extension
utilise les images par défaut du bundle : ``star-empty.png``, ``star-full.png``,
``star-hover.png``.

**Tri**

Les items sont triés par valeur moyenne décroissante ; en cas d'égalité, le
nombre de votes est déterminant. Les items sans évaluation sont classés en fin
de liste.


.. |svg_attr_rating_22| image:: /_img/icons_svg/star.svg
   :width: 22px
.. |img_star_full| image:: /_img/icons/star-full.png
.. |br| raw:: html

   <br />
