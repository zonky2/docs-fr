.. _rst_cookbook_specials_generate-geocoordinates:

Génération et enregistrement automatiques de coordonnées
============================================================

Introduction
------------

Ce guide décrit comment, dans une installation MetaModels, des coordonnées peuvent être automatiquement générées et
enregistrées à partir de données d'adresse.


Prérequis
---------

* Contao 5.3 avec MetaModels 2.4, également testé avec succès avec Contao 4.13 et MetaModels 2.3
* Clé API Google Maps pour la génération de coordonnées → ``API_KEY_SERVER`` (application : adresses IP ; API :
  Geocoding API)
* Champs dans le MetaModel : ``strasse``, ``plz``, ``ort``, ``latitude``, ``longitude``
* Les champs ``latitude`` et ``longitude`` sont du type « Décimal » (metamodels/attribute_decimal)


Étape 1 : création de l'EventListener
----------------------------------------

Pour déterminer et enregistrer automatiquement les coordonnées à partir des données d'adresse, un listener est créé
pour le PrePersistModelEvent. Cet événement est déclenché avant que le modèle ne soit écrit dans la base de données.

Pour cela, on crée un fichier ``src/EventListener/PrePersistModelEventListener.php`` avec le contenu suivant.
Attention : ``API_KEY_SERVER`` doit être remplacé par la clé API correspondante.

.. code-block:: php

  <?php
  // src/EventListener/PrePersistModelEventListener.php
  namespace App\EventListener;

  use ContaoCommunityAlliance\DcGeneral\Event\PrePersistModelEvent;
  use App\Service\GoogleMaps;

  class PrePersistModelEventListener
  {
    public function __invoke(PrePersistModelEvent $event) {
      $model = $event->getModel();
      if (!$model->getProperty('latitude') || !$model->getProperty('longitude')) {
        $strasse     = $model->getProperty('strasse');
        $plz         = $model->getProperty('plz');
        $ort         = $model->getProperty('ort');
        $address     = $strasse . ', ' . $plz . ' ' . $ort;
        $googleMaps  = new GoogleMaps();
        $apiToken    = ‚API_KEY_SERVER‘;
        $coordinates = $googleMaps->getCoordinates($address, $apiToken);

        if (null !== $coordinates) {
          $model->setProperty('latitude', $coordinates->getLatitude());
          $model->setProperty('longitude', $coordinates->getLongitude());
        }
      }
    }
  }


Étape 2 : création de la classe GoogleMaps
---------------------------------------------

Créer le fichier ``src/Service/GoogleMaps.php`` avec le contenu suivant :

.. code-block:: php

  <?php
  // src/Service/GoogleMaps.php
  namespace App\Service;

  use App\Service\Coordinates;

  class GoogleMaps
  {
    public function getCoordinates($address, $apiKey) {
      $url      = \sprintf('https://maps.googleapis.com/maps/api/geocode/json?address=%s&key=%s', urlencode($address), $apiKey);
      $response = file_get_contents($url);
      $data     = json_decode($response);

      if ($data->status === 'OK') {
        $loc = $data->results[0]->geometry->location;

        return new Coordinates($loc->lat, $loc->lng);
      }

      return null;
    }
  }


Étape 3 : création de la classe Coordinates
-----------------------------------------------

Créer le fichier ``src/Service/Coordinates.php`` avec le contenu suivant :

.. code-block:: php

  <?php
  // src/Service/Coordinates.php
  namespace App\Service;

  class Coordinates
  {
    private $lat;
    private $lng;

    public function __construct($lat, $lng) {
      $this->lat = $lat;
      $this->lng = $lng;
    }

    public function getLatitude() {
      return $this->lat;
    }

    public function getLongitude() {
      return $this->lng;
    }
  }


Étape 4 : enregistrement de l'EventListener
------------------------------------------------

Créer ou modifier le fichier ``src/Resources/config/service.yml`` :

.. code-block:: yaml

  # src/Resources/config/service.yml
  services:
    App\EventListener\PrePersistModelEventListener:
      public: true
      tags:
        - { name: kernel.event_listener, event: dc-general.model.pre-persist }

S'assurer que ce fichier est bien inclus dans la configuration principale, par ex. dans ``config/services.yaml`` :

.. code-block:: yaml

  # config/services.yaml
  imports:
    - { resource: '../src/Resources/config/service.yml' }


Test
----

Modifier un enregistrement existant dans le back-end, remplir les champs ``strasse``, ``plz`` et ``ort`` et laisser
les champs ``latitude`` et ``longitude`` vides. Lors de l'enregistrement, la génération automatique des coordonnées
s'effectue.


Remarques
---------

* Le ``PrePersistModelEvent`` n'est déclenché que pour les enregistrements modifiés.
* La façon dont les coordonnées enregistrées peuvent être affichées sous forme de marqueurs sur une carte est décrite
  sous « :ref:`rst_cookbook_specials_marker-for-gmap` ».
* Si le :ref:`filtre Recherche par périmètre (metamodels/filter_perimetersearch) <extended_perimetersearch>` est
  implémenté, l'un des services qui y sont implémentés peut également être utilisé pour déterminer les coordonnées.
* L'EventListener peut également être enregistré via une annotation ou un attribut PHP - voir
  :ref:`rst_cookbook_specials_register-services`


**Remerciements**

Merci à `Nicole Weiß - Webstylisten.de <https://webstylisten.de>`_ pour cet article.
