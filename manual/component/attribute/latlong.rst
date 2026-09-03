.. _component_attribute_latlong:

|svg_attr_latlong_22| LatLong (à partir de MM 2.5)
=======================================================

L'attribut « LatLong » enregistre un couple de coordonnées (latitude et longitude)
dans une seule colonne du type de donnée natif MySQL/MariaDB ``POINT``. Contrairement
à deux attributs Décimal séparés ou à un attribut Texte avec des valeurs séparées par
une virgule, un véritable type de colonne spatial est ainsi disponible, sur lequel la
base de données peut créer un index spatial si besoin.

Cas d'utilisation typiques :

* Enregistrement de la position d'un jeu de données (point de vente, lieu
  d'événement, marqueur sur une carte)
* Base pour une :ref:`recherche par rayon <component_filter_perimeter-search>` ou
  l'attribut :ref:`Distance géographique <component_attribute_geodistance>`
* Position du marqueur pour l'intégration
  :ref:`Cowegis-Layer <extended_cowegis-layer-marker>`

.. seealso::

   * :ref:`component_filter_perimeter-search`
   * :ref:`component_attribute_geodistance`
   * :ref:`extended_cowegis-layer-marker`


Installation
------------

L'attribut s'installe via le **Contao Manager** ou **Composer** :

.. code-block:: bash

   composer require metamodels/attribute_latlong


Réglages lors de la création de l'attribut
-------------------------------------------

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Option
     - Description
   * - Créer un index spatial
     - Crée un ``SPATIAL INDEX`` sur la colonne, afin que les requêtes (par ex. la
       :ref:`recherche par rayon <component_filter_perimeter-search>`) puissent
       l'utiliser pour une recherche par rayon nettement plus rapide - voir
       :ref:`Fonctions particulières <component_attribute_latlong_special>`
       ci-dessous. Requiert que la colonne soit ``NOT NULL`` - l'attribut devient
       donc automatiquement obligatoire, aussi bien à l'enregistrement d'un jeu de
       données que visiblement dans le masque de saisie (voir ci-dessous). Si un
       attribut contient déjà des valeurs vides, l'activation échoue tant que
       celles-ci ne sont pas renseignées.


Réglages dans les réglages de rendu
-------------------------------------

L'attribut ne possède pas de réglages de rendu spécifiques. Dans la liste des
attributs d'un réglage de rendu, les options habituelles sont disponibles :

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Option
     - Description
   * - Template
     - Sélection d'un template propre pour l'affichage du couple de coordonnées.
   * - Classe CSS
     - Classe CSS optionnelle ajoutée à l'élément de sortie.


Réglages dans le masque de saisie
-----------------------------------

Dans le masque de saisie, deux champs apparaissent par défaut côte à côte
(latitude, longitude). Si « Créer un index spatial » est activé sur l'attribut, le
champ est en plus marqué comme obligatoire - ceci n'est pas modifiable tant que
l'index est actif.

**Détermination de l'adresse via le widget Geocode**

Si le paquet `cowegis/cowegis-contao-geocode-widget-bundle
<https://github.com/cowegis/cowegis-contao-geocode-widget-bundle>`_ est installé,
une légende supplémentaire est disponible dans le masque de saisie, permettant de
remplacer ou compléter la saisie manuelle des coordonnées par une recherche
d'adresse avec sélection sur une carte :

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Option
     - Description
   * - Disposition des champs
     - Détermine, indépendamment de la détermination d'adresse, si les
       coordonnées sont affichées dans deux champs séparés (latitude, longitude -
       par défaut) ou dans un seul champ sous forme de valeur séparée par une
       virgule (``latitude,longitude``).
   * - Déterminer les coordonnées à partir d'une adresse |br| (`widget Cowegis Geocode <https://github.com/cowegis/cowegis-contao-geocode-widget-bundle>`_ nécessaire)
     - Ajoute une fenêtre popup avec recherche d'adresse et carte, permettant de
       déterminer les coordonnées à partir d'une adresse saisie et de les ajuster
       sur la carte (``submitOnChange`` - affiche immédiatement les options
       suivantes).
   * - Attribut rue / numéro / |br| code postal / ville / pays
     - Sélection des attributs du même MetaModel dont les valeurs composent la
       requête de recherche pour la détermination de l'adresse. Les cinq champs
       sont optionnels et sélectionnables indépendamment les uns des autres - au
       moins un doit être renseigné pour que la fenêtre popup apparaisse.
   * - URL du serveur de tuiles (optionnel) |br| Mention de la source de la carte (optionnel)
     - Les deux champs peuvent rester vides - le widget utilise alors son propre
       serveur de tuiles par défaut avec la mention de source correspondante. À
       renseigner uniquement si un autre fournisseur de cartes doit être utilisé
       (par ex. en raison de ses conditions d'utilisation pour le trafic de
       données propre).

.. note:: Le widget Geocode est un paquet autonome, indépendant de MetaModels -
   voir sa `documentation <https://github.com/cowegis/cowegis-contao-geocode-widget-bundle>`_
   pour plus de détails sur l'utilisation de la fenêtre popup.


Règles de filtre
-------------------

.. list-table::
   :header-rows: 1
   :widths: 30 70

   * - Règle de filtre
     - Remarque
   * - :ref:`Recherche par rayon <component_filter_perimeter-search>`
     - Dans le « mode de données » de la règle de filtre, l'option « Attribut
       unique » est disponible - seul un attribut de type LatLong peut y être
       choisi. Si un index spatial est créé sur l'attribut, celui-ci est
       automatiquement utilisé pour la recherche par rayon.


.. _component_attribute_latlong_special:

Fonctions particulières
-------------------------

**Format de stockage**

Les coordonnées sont enregistrées sous forme de ``POINT`` natif (format binaire
WKB, SRID inclus), et non sous forme de deux valeurs décimales ou de texte. Toutes
les fonctions spatiales de MySQL/MariaDB (par ex. ``ST_Distance_Sphere()``,
``ST_X()``, ``ST_Y()``) sont ainsi directement disponibles sur la colonne.

Les données existantes peuvent être facilement reprises dans le nouvel attribut -
par exemple :

.. code-block:: mysql
   :linenos:

   -- copie de geo_lat/geo_long vers le nouveau champ geo_latlong_single
   UPDATE mm_map
   SET geo_latlong_single = POINT(geo_long, geo_lat)
   WHERE geo_lat IS NOT NULL
     AND geo_long IS NOT NULL
     AND geo_latlong_single IS NULL;


**Performance avec index spatial**

Un simple ``WHERE ST_Distance_Sphere(...) <= x`` ne peut par principe **pas**
utiliser d'index spatial - c'est pourquoi la recherche par rayon combine, lorsque
l'index est activé, un pré-filtre grossier de type boîte englobante utilisable par
l'index (``MBRContains``) avec le calcul exact de ``ST_Distance_Sphere()``. Mesuré
sur une table de 500 000 jeux de données avec une recherche par rayon de 50 km
(médiane de 5 exécutions) :

.. list-table::
   :header-rows: 1
   :widths: 50 25 25

   * - Variante
     - Temps
     - Facteur
   * - Ancien : approximation de Haversine, deux attributs Décimal séparés, sans
       index
     - 0,402 s
     - Référence
   * - Nouveau : ``ST_Distance_Sphere()``, attribut LatLong sans index
     - 0,181 s
     - ~2,2× plus rapide
   * - Nouveau : ``ST_Distance_Sphere()`` + pré-filtre boîte englobante + index
       spatial
     - 0,014 s
     - ~28× plus rapide

Le seul changement de formule apporte déjà environ le double de rapidité, et
l'index spatial avec pré-filtre boîte englobante ajoute encore environ 13 fois
plus.


.. |svg_attr_latlong_22| image:: /_img/icons_svg/latlong.svg
   :width: 22px

.. |br| raw:: html

   <br />
