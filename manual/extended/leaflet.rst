.. _rst_extended_leaflet:

Intégration Leaflet-Maps
#########################

.. note:: L'extension `Contao-Leaflet <https://github.com/netzmacht/contao-leaflet-metamodels>`_ n'a pas été
   poursuivie pour Contao 5 - il existe désormais une alternative avec :ref:`Cowegis-Layer <extended_cowegis-layer-marker>`.

Avec l'`intégration Leaflet-Maps <https://github.com/netzmacht/contao-leaflet-metamodels>`_, l'affichage de
MetaModels dans l'extension `netzmacht/contao-leaflet-maps`_ devient possible.

.. note:: Cette documentation se réfère exclusivement à Contao 4, même si l'extension est également mise à
   disposition pour Contao 3.5.


Fonctions
---------

 * Rendu d'un item MetaModels comme marqueur sur une carte
 * Référencer un layer dans l'item MetaModels et l'afficher sur la carte
 * Lier des fichiers GeoJson dans l'item MetaModels et les afficher sur la carte
 * Attribut carte Leaflet : rendre directement une carte dans l'item MetaModels


Prérequis
---------

Contao 4
~~~~~~~~

 - Contao 4.4 min.
 - MetaModels 2.1 min.
 - PHP 7.1 min.
 - Symfony 3.4 min.

Contao 3.5
~~~~~~~~~~

*(support de correctifs se terminant en mai 2019)*

 - MetaModels 2.0
 - `netzmacht/contao-leaflet-maps`_ 2.0
 - PHP 5.4 min.

Installation
------------

`netzmacht/contao-leaflet-metamodels`_ peut être installé via Composer/Contao Manager.


Intégrer un MetaModel sur une carte
------------------------------------

Ce guide montre comment un MetaModel disposant de géocoordonnées peut être
affiché sur une carte de Leaflet pour Contao.


Attributs de coordonnées
~~~~~~~~~~~~~~~~~~~~~~~~~

Les géocoordonnées peuvent être définies dans le MetaModel sous forme d'attributs
séparés ou dans un seul attribut (Latitude et Longitude séparées par une virgule).
Un simple attribut texte convient par exemple comme type d'attribut.

.. figure:: /_img/screenshots/extended/leaflet/mm_attribute.png
   :alt: Attributs dans le MetaModel

   Attributs Latitude et Longitude dans le MetaModel

.. _netzmacht/contao-leaflet-maps: https://github.com/netzmacht/contao-leaflet-maps
.. _netzmacht/contao-leaflet-metamodels: https://github.com/netzmacht/contao-leaflet-metamodels


Créer un layer MetaModels
~~~~~~~~~~~~~~~~~~~~~~~~~~

Comme étape suivante, un nouveau layer de type "MetaModels" est créé sous
Layers de carte. Les réglages suivants doivent être effectués ici :

 * **Type** : sélectionner MetaModel
 * **MetaModel** : le MetaModel souhaité
 * **Relation des limites** : définit quelles dépendances doivent exister entre les éléments du layer
   et les limites de la carte - sélection de *extend*. Les limites de la carte sont étendues par les
   marqueurs définis.
 * **Réglage de filtre à appliquer** : ici, comme d'habitude avec MetaModels, un réglage de filtre est
   sélectionné, qui influence les items à afficher.

.. figure:: /_img/screenshots/extended/leaflet/leaflet_layer.png
   :alt: Configuration du layer MetaModels

   Configuration du layer MetaModels


Créer le renderer du layer MetaModels
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

L'étape suivante consiste à définir comment l'item MetaModels doit être
affiché sur la carte. Dans cet exemple, ils doivent être affichés comme marqueurs.
Pour cela, les *renderers* correspondants peuvent être créés via l'icône d'édition du layer de carte.

.. figure:: /_img/screenshots/extended/leaflet/leaflet_layer_2.png
   :alt: Aperçu des layers de carte

   Aperçu des layers de carte

Dans le masque de saisie, il est possible de définir de nouveaux renderers. Les réglages suivants
doivent être effectués ici :

 * **Type** : sélection de *marker*, puisque les items MetaModel doivent être affichés comme marqueurs
 * **Coordonnées** : sélection de *separate* si les valeurs pour Latitude et Longitude se trouvent dans
   des attributs séparés
 * **Attribut Largeur** : sélectionner l'attribut pour *Latitude*
 * **Attribut Longueur** : sélectionner l'attribut pour *Longitude*
 * **Activer le réglage de rendu** : activer le réglage de rendu
 * **Chargement différé** : pour les listes plus importantes, il est recommandé de recharger dynamiquement
   les données de carte via une API. Elles ne sont alors pas directement rendues en Javascript.

En plus de la configuration de base, le MetaModel peut également être ajouté comme popup au marqueur.
Deux modes sont pris en charge ici :

 * **render** : un réglage de rendu est sélectionné et rendu
 * **attribute** : un attribut est rendu. Un réglage de rendu doit également être sélectionné pour cela

Il est également possible d'influencer l'affichage sous forme d'icône. Il est possible de sélectionner
l'une des icônes prédéfinies ou, alternativement, de la déterminer via un attribut MetaModels.

.. figure:: /_img/screenshots/extended/leaflet/layer_renderer.png
   :alt: Réglage du renderer

   Réglage du renderer


Activer le layer dans la carte
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Comme dernière étape, une carte doit encore être assignée au layer pour l'affichage. Cela
peut se faire via les layers standard d'une carte.

Il est en outre recommandé d'activer, pour la fonction *définir les limites*, les options *à l'initialisation
de la carte* et *après le chargement de la fonctionnalité différée*. La carte s'étend alors dynamiquement à
la zone dans laquelle les marqueurs existent.

.. figure:: /_img/screenshots/extended/leaflet/leaflet_map.png
   :alt: Réglages de la carte

   Réglages de la carte

Si un filtre alimentant le réglage de filtre sélectionné ci-dessus est intégré à la page,
la vue de la carte est filtrée en conséquence.
