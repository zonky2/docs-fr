.. _component_attribute_geodistance:

|svg_attr_geodistance_22| |img_geodistance| Distance géographique
===================================================================

L'attribut « Distance géographique » calcule, lors d'une recherche par rayon, la
distance géographique entre le couple de coordonnées enregistré d'un item et un
point de recherche. Le résultat permet de trier des listes par distance. Cas
d'utilisation typiques :

* Recherche de revendeurs ou de points de vente (« Trouver tous les revendeurs
  dans un rayon de 50 km »)
* Recherche d'événements par proximité géographique
* Tri des résultats par distance par rapport à la position de l'utilisateur

L'attribut lui-même n'enregistre aucune valeur de données propre, mais lit les
coordonnées d'autres attributs du MetaModel (latitude et longitude) et calcule la
distance à la demande.

.. seealso:: Dans le livre de recettes :

   * :ref:`rst_cookbook_specials_generate-geocoordinates`
   * :ref:`rst_cookbook_specials_marker-for-gmap`


Installation
------------

L'attribut s'installe via le **Contao Manager** ou **Composer** :

.. code-block:: bash

   composer require metamodels/attribute_geodistance


Réglages lors de la création de l'attribut
-------------------------------------------

L'attribut propose les réglages spécifiques suivants, répartis en deux groupes :

**Paramètres**

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Option
     - Description
   * - Paramètre GET pour l'adresse
     - Nom du paramètre GET d'URL par lequel l'adresse de recherche est
       transmise (par ex. ``address``). Champ obligatoire.
   * - Valeur par défaut du pays
     - Détermine comment le pays est déterminé pour la résolution d'adresse :

       * **Aucun** – aucun pays n'est prédéfini
       * **Valeur par défaut** – un pays fixe est défini par défaut (saisie du
         code pays dans le sous-champ « Valeur par défaut pour le pays »)
       * **Utiliser un paramètre GET** – le pays est transmis via un paramètre
         d'URL (saisie du nom du paramètre dans le sous-champ « Paramètre GET
         pour le pays »)

**Données**

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Option
     - Description
   * - Mode de données
     - Détermine comment les coordonnées géographiques sont enregistrées dans
       les attributs MetaModels :

       * **Mode simple** – la latitude et la longitude sont enregistrées
         combinées dans un seul attribut. Seul un attribut de type
         :ref:`LatLong <component_attribute_latlong>` peut être sélectionné.
         Sous-champ : sélection de l'attribut.
       * **Mode multiple** – la latitude et la longitude sont enregistrées
         dans deux attributs séparés. Sous-champs : attribut pour la latitude
         (Lat) et attribut pour la longitude (Lng).
   * - Pas d'arrondi (km)
     - La distance calculée est arrondie à un multiple de cette valeur (en
       kilomètres) - par ex. ``0.001`` arrondit au mètre près, ``1`` aux
       kilomètres entiers, ``5`` par pas de 5 kilomètres. N'affecte que la
       valeur affichée, pas l'ordre de tri - celui-ci reste toujours exact.
   * - Services de résolution
     - Assistant à plusieurs colonnes pour configurer les services qui
       convertissent une adresse en coordonnées géographiques. Services
       disponibles (selon l'installation) :

       * **Coordonnées** – saisie directe des coordonnées
       * **Google Maps** – résolution d'adresse via l'API Google Maps
       * **OpenStreetMap** – résolution d'adresse via l'API Nominatim

       Pour les services nécessitant un jeton API, celui-ci peut être saisi
       dans le champ « Jeton API ».

       Les services de résolution sont traités dans l'ordre de haut en bas et
       s'arrêtent au premier résultat trouvé. Si, en plus de la saisie d'une
       adresse, les coordonnées doivent également être autorisées en
       frontend, ce service doit figurer en première position.


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
     - Sélection d'un template propre pour l'affichage de la valeur de
       distance.
   * - Classe CSS
     - Classe CSS optionnelle ajoutée à l'élément de sortie.


Réglages dans le masque de saisie
-----------------------------------

L'attribut Distance géographique n'apparaît pas comme champ de saisie modifiable
dans le masque de saisie — la valeur de distance est calculée dynamiquement et est
en lecture seule.


Règles de filtre
-------------------

L'attribut est typiquement utilisé conjointement avec la règle de filtre
« Recherche par rayon » (du paquet ``filter_perimetersearch``) :

.. list-table::
   :header-rows: 1
   :widths: 30 70

   * - Règle de filtre
     - Remarque
   * - Recherche par rayon
     - Filtre les items selon un rayon géographique autour d'une adresse
       saisie. L'attribut Distance géographique met à disposition les
       valeurs de distance calculées, qui permettent ensuite un tri.


Fonctions particulières
-------------------------

**Calcul**

La distance entre le point de recherche et le couple de coordonnées enregistré
est calculée via la fonction spatiale native ``ST_Distance_Sphere()`` de
MySQL/MariaDB (distance sphérique, tenant compte de la courbure terrestre). En
mode simple, la colonne ``POINT`` de l'attribut
:ref:`LatLong <component_attribute_latlong>` est utilisée directement - si un
index spatial y est défini, seule la
:ref:`recherche par rayon <component_filter_perimeter-search>` elle-même en
profite, pas le tri effectué ici (celui-ci s'effectue sur l'ensemble de résultats
déjà restreint par la recherche par rayon).

**Mise en cache**

Les coordonnées résolues (adresse → latitude/longitude) sont mises en cache dans
la table ``tl_metamodel_perimetersearch``, afin d'éviter des requêtes API
répétées.

**Stockage**

L'attribut ne crée pas de colonne propre dans la table du MetaModel. Il lit les
coordonnées dans les attributs source configurés et calcule la distance à
l'exécution.

**Tri par distance**

Les valeurs de distance calculées peuvent être utilisées comme critère de tri
dans la vue en liste de MetaModels, de sorte que les résultats les plus proches
apparaissent en premier.


.. |svg_attr_geodistance_22| image:: /_img/icons_svg/geodistance.svg
   :width: 22px
.. |img_geodistance| image:: /_img/icons/geodistance.png
.. |br| raw:: html

   <br />
