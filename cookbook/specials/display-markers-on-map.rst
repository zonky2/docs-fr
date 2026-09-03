.. _rst_cookbook_specials_marker-for-gmap:

Afficher des emplacements sous forme de marqueurs sur une carte Google
========================================================================

.. note:: Comme alternative à la sortie via un template, l'extension
   :ref:`Cowegis-Layer <extended_cowegis-layer-marker>` est disponible.


Objectif
--------
Sur une page, les entrées (éventuellement filtrées) d'un MetaModel doivent être affichées sous forme de marqueurs sur
une carte Google.


Prérequis
---------

* Contao 5.3 avec MetaModels 2.4, également testé avec succès avec Contao 4.13 et MetaModels 2.3
* Clé API Google Maps pour l'affichage de la carte → ``API_KEY_WEBSITE`` (application : sites web ; API : Maps
  JavaScript API)
* Template MetaModels avec accès à ``latitude``, ``longitude`` et éventuellement des champs individuels comme
  ``name`` dans cet exemple

La sortie s'effectue dans le template MetaModels des réglages de rendu. Il s'agit du template avec lequel la liste
MetaModels est affichée dans le frontend - voir :ref:`Templates <component_templates>`. On peut créer une variante du
template ``metamodel_prerendered.html5``, par ex. sous le nom ``metamodel_pre_gmap-with-marker.html5``, et la
sélectionner en conséquence dans les réglages de rendu.

Préparer les marqueurs
-----------------------

Dans le template, on crée d'abord un tableau contenant toutes les coordonnées :

.. code-block:: php

  <?php $markers = []; ?>
  <?php foreach ($this->data as $arrItem): ?>
    <?php
      if (!empty($arrItem['text']['latitude']) && !empty($arrItem['text']['longitude'])) {
          $markers[] = [
              'lat'   => (float) $arrItem['text']['latitude'],
              'lng'   => (float) $arrItem['text']['longitude'],
              'title' => htmlspecialchars($arrItem['text']['name'], ENT_QUOTES, 'UTF-8'),
          ];
      }
    ?>
    <?php //Autres sorties de la liste … ?>
  <?php endforeach; ?>


Intégrer la carte
-------------------

La carte est également affichée dans le template créé, après la boucle « foreach ». Attention : ``API_KEY_WEBSITE``
doit être remplacé par la clé API correspondante. Le tableau PHP issu de la boucle est converti en une chaîne JSON
correspondante pour l'utilisation en JavaScript.

.. code-block:: html

      <div class="map_wrapper">
      <script async src="https://maps.googleapis.com/maps/api/js?key=API_KEY_WEBSITE&callback=initMap&language=de&region=DE"></script>

      <div id="map" style="height: 400px; width: 100%;"></div>

      <script>
        function initMap() {
          const mapOptions = {
            center: { lat: 52.553807, lng: 13.405007 }, // Valeur par défaut pour Berlin
            zoom: 10,
            zoomControl: true,
            streetViewControl: true,
            mapTypeControl: true,
            mapTypeId: google.maps.MapTypeId.ROADMAP,
            styles: [
              {
                "featureType": "poi.business",
                "stylers": [
                  { "visibility": "off" }
                ]
              },
              {
                "featureType": "poi.park",
                "elementType": "labels.text",
                "stylers": [
                  { "visibility": "off" }
                ]
              }
            ]
          };

          // Initialiser la carte
          const map = new google.maps.Map(document.getElementById("map"), mapOptions);
          // Tableau de marqueurs au format JSON
          var markers = <?= json_encode($markers, JSON_HEX_TAG | JSON_HEX_APOS | JSON_HEX_QUOT | JSON_HEX_AMP) ?>;

          var bounds = new google.maps.LatLngBounds();
          var infowindow = new google.maps.InfoWindow();
          var minZoom = 11;

          if (markers.length === 0) {
            map.setCenter({ lat: 52.553807, lng: 13.405007 });
            map.setZoom(minZoom);
            return;
          }

          // Création des marqueurs à partir des données JSON
          markers.forEach(function(markerData) {
            let marker = new google.maps.Marker({
              position: { lat: markerData.lat, lng: markerData.lng },
              map: map,
              title: markerData.title,
              clickable: true
            });

            // Création de l'info-bulle, par ex. avec titre et URL
            marker.addListener("click", function() {
              let content = "<strong>" + markerData.title + "</strong>";
              if (markerData.website) {
                content += "<br>" + markerData.website;
              }
              infowindow.setContent(content);
              infowindow.open(map, marker);
            });

            bounds.extend(marker.position);
          });

          map.fitBounds(bounds);

          google.maps.event.addListenerOnce(map, 'zoom_changed', function() {
            if (map.getZoom() > minZoom) {
              map.setZoom(minZoom);
            }
          });
        }
      </script>
    </div>


Remarques
---------

* Pour une utilisation conforme à la protection des données, la carte devrait être activée via un outil de gestion
  du consentement.
* La sortie lors du rendu peut être accélérée si, dans les réglages de l'élément de contenu MM-Liste, l'option
  « Ne pas sortir d'items analysés via "$data" » est activée - un rendu des données n'est alors pas nécessaire.
* La manière dont les coordonnées d'une adresse sont automatiquement récupérées et enregistrées lors de la sauvegarde
  est décrite sous « :ref:`rst_cookbook_specials_generate-geocoordinates` ».


**Remerciements**

Merci à `Nicole Weiß - Webstylisten.de <https://webstylisten.de>`_ pour cet article.
