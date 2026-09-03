.. _extended_cowegis-layer-marker:

Intégration Cowegis-Layer pour les marqueurs
=============================================

`Cowegis-Layer` permet l'affichage de marqueurs issus de MetaModels dans l'extension Contao
`Cowegis <https://github.com/cowegis>`_. Avec Cowegis, différentes cartes, marqueurs, polygones etc.
peuvent être configurés et restitués via `Leaflet <https://leafletjs.com/>`_. L'extension fonctionne
aussi bien avec des MetaModels monolingues qu'avec des MetaModels multilingues.

.. note:: Cette extension est disponible à partir de MM 2.4 avec Contao 5.3 - pour une activation, merci
   d'envoyer un e-mail à mail@metamodel.me. Financement actuellement encore ouvert : 3 181,25 €


Installation
------------

L'installation de `Cowegis-Layer` installe automatiquement les paquets de base nécessaires de Cowegis. Si l'on
souhaite utiliser Cowegis également indépendamment de MetaModels, il est recommandé d'installer l'un des deux
paquets suivants :

* `Cowegis Contao Monolingual Pack <https://github.com/cowegis/cowegis-contao-monolingual-pack>`_
* `Cowegis Contao Multilingual Pack <https://github.com/cowegis/cowegis-contao-multilingual-pack>`_

Pour la restitution multilingue de données issues de MetaModels - par ex. pour les textes dans les popups - le
Monolingual Pack suffit. Le Multilingual Pack est destiné aux traductions propres au niveau des cartes (il
utilise l'extension `DC_Multilingual <https://github.com/terminal42/contao-DC_Multilingual>`_).

Après l'installation et la migration de la base de données, une nouvelle section « COWEGIS » apparaît dans la
navigation du backend. Les cartes et les marqueurs peuvent être créés via les points de navigation correspondants.


Démarche générale
------------------

Dans Cowegis, une carte se compose de plusieurs calques (Layers) qui combinent différents contenus dans la vue
d'ensemble de la carte. Un calque avec les données cartographiques est bien entendu la base. Comme ces données
cartographiques sont composées de tuiles (Tiles) individuelles, on parle fréquemment de « tuiles » ou « tiles ».
Sur ce calque « carte », différents éléments comme des marqueurs, des polygones etc. peuvent à leur tour être
affichés via leurs propres calques.

Le déroulement pour la création d'une carte avec des marqueurs issus de données MetaModels est le suivant :

**Préparation :**

* créer un calque pour les données cartographiques
* créer une carte et y intégrer le calque
* afficher la carte

**Affichage des données MetaModels**

* créer les données MetaModels
* créer le calque de marqueurs
* intégrer le calque de marqueurs dans la carte

**Réglages optionnels**

* configurer les icônes
* configurer le popup
* créer des éléments de contrôle
* créer d'autres calques

La plupart des valeurs de saisie ont leur équivalent dans le projet `Leaflet <https://leafletjs.com/>`_, qui fournit
la bibliothèque JavaScript pour l'affichage des cartes. En cas de paramètre peu clair, il est conseillé d'y jeter un
œil dans les exemples et la documentation.


Préparation
-----------

Créer un calque
................

Dans la section Calques, un nouveau calque pour l'affichage de la carte est créé. Les types disponibles sont
« Calque de tuiles » ou « Carte préconfigurée ».

Pour le type « Calque de tuiles », il faut renseigner un modèle d'URL adapté. On le trouve par ex. chez les
fournisseurs de cartes correspondants ou on peut le récupérer depuis les
`fournisseurs Leaflet <https://github.com/leaflet-extras/leaflet-providers/blob/master/leaflet-providers.js>`_.
L'URL typique pour OSM est ``https://tile.openstreetmap.org/{z}/{x}/{y}.png``. Pour ce type de calque, les
paramètres de configuration possibles sont disponibles pour des réglages individuels.

Une variante plus simple est le type « Carte préconfigurée ». Ici, les fournisseurs de cartes habituels comme OSM,
MapBox, etc. peuvent être sélectionnés dans une liste - les paramètres spécifiques du fournisseur concerné sont
alors automatiquement intégrés.

Créer une carte et intégrer le calque
.......................................

À l'étape suivante, une nouvelle carte est créée dans la rubrique `Cartes` via « Créer une carte ». Seul le titre
est ici un champ obligatoire.

On peut saisir des coordonnées pour un centrage initial ainsi qu'un facteur de zoom. Les coordonnées pour le
centrage peuvent être déterminées à partir d'une adresse. Pour cela, ouvrir le popup de la carte via l'icône carte
|img_map|, saisir une adresse en haut à droite dans le champ de recherche et valider avec Entrée. En cliquant sur
le bouton « Appliquer », les coordonnées sont reprises. Les autres paramètres pourront être réglés ou ajustés
ultérieurement.

Si aucun centrage initial n'est indiqué, il convient de s'assurer que la carte se positionne correctement grâce
à d'autres réglages. Cela peut par exemple se faire en activant, pour les calques activés (marqueurs) d'une carte,
l'option « Définir les limites » (voir plus bas).

Après l'enregistrement et la fermeture, une nouvelle entrée apparaît dans la liste avec la nouvelle carte.

|img_screenshot_16|

Via l'icône de la vue des calques |img_layers|, on accède à la liste des calques créés.

|img_screenshot_17|

Avec l'icône verte plus |img_copy|, le calque de carte créé est ajouté, respectivement activé. L'icône verte plus
se transforme alors en icône rouge X |img_delete| et les icônes crayon |img_edit| et carte |img_map| apparaissent.
Le crayon ouvre le masque d'édition habituel et via l'icône carte, on peut définir si le calque de carte doit être
affiché par défaut ou non.

Si les limites de la carte doivent réagir à un calque comme par ex. un calque de marqueurs, il faut activer
l'option « Définir les limites » (voir ci-dessus).

Même si un calque de carte n'est pas défini comme calque par défaut - l'icône est désactivée |img_map_1| - les
données cartographiques sont bien restituées en frontend. Mais leur affichage est empêché et peut être activé ou
désactivé via un élément de contrôle de calques (voir plus bas). Cela permet de donner au visiteur du site la
possibilité d'activer ou de désactiver lui-même différents calques, comme des types de cartes par ex. avec/sans
transports en commun ou avec/sans marqueurs ou polygones.

L'icône carte n'est donc pas l'habituelle « icône œil » de désactivation d'un enregistrement. Pour désactiver un
calque, il faut au contraire ouvrir le masque d'édition via le crayon et le désactiver via la case à cocher
« Actif », ou cliquer sur l'icône rouge X |img_delete| dans la vue liste.

|img_screenshot_15|

Afficher la carte
..................

À l'étape suivante, on peut créer la carte comme élément de contenu ou module frontend. Pour cela, on se rend
dans le masque d'édition correspondant et on sélectionne « Carte Cowegis » comme type. Après avoir sélectionné
la carte Cowegis, saisi une largeur et une hauteur de carte et enregistré, la carte est visible sur la sortie
frontend correspondante.

Pour les paramètres « Centrer » avec ``52.510885,13.3989367`` et « Facteur de zoom » ``14``, le rendu de la carte
ressemble à peu près à ceci :

|img_screenshot_13|

Affichage des données MetaModels
---------------------------------

Créer les données MetaModels
..............................

Pour afficher des enregistrements comme marqueurs sur une carte, différentes données doivent être renseignées
dans MetaModels. Pour les indications suivantes, des attributs correspondants devraient/doivent être disponibles
dans MM (avec indication des attributs pris en charge) :

* Coordonnées (Latitude et Longitude obligatoires, Altitude optionnelle) - :ref:`LatLong
  <component_attribute_latlong>` (recommandé), Décimal en cas de saisie individuelle par coordonnée ou Texte pour
  une saisie séparée par des virgules
* Attribut Title (optionnel) - Texte, Valeurs combinées, Texte traduit, Valeurs combinées traduites
* Attribut Alt (optionnel) - Texte, Valeurs combinées, Texte traduit, Valeurs combinées traduites
* Popup (optionnel) - Texte, Texte long, Valeurs combinées, Texte traduit, Texte long traduit, Valeurs combinées
  traduites

Les coordonnées du marqueur peuvent être enregistrées de trois façons :

* **Attribut LatLong** (à partir de MM 2.5, recommandé) - un seul attribut enregistre la paire de coordonnées
  sous forme de ``POINT`` natif. Cette variante prend en charge en option un index spatial et peut également
  être filtrée avec une :ref:`recherche par rayon depuis MetaModels <extended_perimetersearch>` - entre-temps
  même nettement plus rapide que la variante avec des attributs décimaux individuels, à condition que l'index
  soit activé.
* **Texte séparé par des virgules** - un attribut Texte reçoit le tuple (``52.510885,13.3989367``) ou le triplet
  (``52.510885,13.3989367,36``). Non filtrable avec une recherche par rayon.
* **Valeurs individuelles** - deux ou trois attributs « Décimal » pour la Latitude, la Longitude et
  éventuellement l'Altitude. Prend également en charge une recherche par rayon depuis MetaModels.

Un texte peut optionnellement être transmis à l'icône du marqueur pour l'attribut Title ou Alt. Pour cela, un
attribut « Texte » correspondant est nécessaire. Le texte ne doit contenir aucun formatage HTML, ce qui
perturberait la sortie HTML.

Pour le marqueur, il est possible d'afficher une boîte d'information sous forme de popup au clic. Le contenu
peut provenir d'un attribut, par ex. « Texte » ou « Texte long », et peut également contenir des formatages HTML
comme des liens etc. Le rendu de l'attribut est déterminé par le choix du réglage de rendu - l'attribut devrait
figurer comme élément dans le réglage de rendu.

En alternative à un attribut unique, un :ref:`réglage de rendu <component_rendersettings>` propre peut également
être créé pour le popup. Avec un réglage de rendu séparé, il est possible de combiner la sortie de plusieurs
attributs et de la restituer avec un template propre. De plus, la sortie simple de liens de détail (jumpTo) est
possible.

Pour les trois sorties de texte (popup ainsi que attributs Title et Alt), aussi bien des attributs MetaModels
monolingues que traduits peuvent être utilisés - une sortie multilingue est prise en charge.

Une fois tous les attributs créés et remplis de données, l'étape suivante consiste en l'intégration, respectivement
la création automatique, des marqueurs dans Cowegis.

Créer le calque de marqueurs
..............................

Une fois toutes les préparations effectuées dans MM, un calque correspondant pour la sortie des marqueurs peut
être créé.

Pour cela, dans Cowegis sous Calques, créer un nouveau calque de type « Marqueur MetaModels » avec « Créer un
calque ». Le choix du type affiche les widgets de saisie adaptés dans le masque. Dans la section « MetaModel »,
le modèle souhaité doit être sélectionné. Dans la section Coordonnées, le choix entre un ou plusieurs attributs
pour les coordonnées est possible. Selon le choix, un ou trois champs de sélection sont disponibles.

Les réglages dans la section Icône sont optionnels. Les réglages de l'icône sont abordés plus bas. Le choix d'un
attribut MetaModel pour l'attribut Title ou Alt de l'icône peut désormais être effectué.

Dans la section optionnelle Popup, on peut déterminer avec « Ajouter un popup » si un popup doit apparaître et,
le cas échéant, si le contenu doit provenir d'un attribut MetaModel ou d'un réglage de rendu séparé.

Voici un exemple des réglages de configuration :

|img_screenshot_14|

Intégrer le calque de marqueurs dans la carte
................................................

Une fois toutes les saisies effectuées et enregistrées, on revient à la carte créée pour afficher les calques
|img_layers|.

Le calque de marqueurs créé y apparaît avec l'icône |img_metamodels_marker.svg| et est intégré avec |img_copy|.
Le calque devrait ainsi également être défini comme calque par défaut visible - le cas échéant, l'activer via
l'édition ou l'icône carte. La liste des calques pourrait ressembler à ceci :

|img_screenshot_01|

Voici un exemple de l'aspect que pourraient avoir les marqueurs sur une carte :

|img_screenshot_02|

Si le centrage de la carte et le zoom doivent réagir aux marqueurs, l'option « Ajuster les limites » doit être
activée - sinon, les valeurs par défaut de centrage et de zoom de la carte sont utilisées.

|img_screenshot_20|


Réglages optionnels
--------------------

La sortie peut être adaptée à ses propres souhaits et exigences à de très nombreux endroits. Par exemple, pour le
calque avec les marqueurs MetaModels, la transparence peut être réglée dans la section Configuration, ou si les
icônes doivent être accessibles au tabulateur.

Configurer les icônes
.......................

L'adaptation de l'affichage des icônes de marqueurs est possible de multiples façons. Par défaut, l'icône
suivante de `Leaflet <https://leafletjs.com/>`_ est restituée à la taille 25x41px :

|img_marker-icon|

Ses propres icônes peuvent être créées dans les Modèles avec « Créer une icône ». Les types suivants sont
actuellement disponibles au choix :

* Fichier
* DIV
* SVG
* Font-Awesome

**Fichier** |br|
Pour le `type « Fichier » <https://leafletjs.com/reference.html#icon>`_, on peut sélectionner un fichier dans la
gestion des fichiers. Qui ne dispose pas de son propre fichier peut par ex. récupérer une icône chez certaines
polices d'icônes comme `Lucide <https://lucide.dev/icons/?search=map>`_. Le type Fichier prend en charge, outre
le PNG, également le SVG. La taille de l'icône affichée est déterminée par le fichier d'origine ou peut être
ajustée via `iconSize en indiquant « largeur,hauteur » en pixels <https://leafletjs.com/reference.html#icon>`_ ;
par ex. ``42,42``.

|img_screenshot_03|

**DIV** |br|
Pour le `type « DIV » <https://leafletjs.com/reference.html#divicon>`_, n'importe quel contenu HTML peut être
saisi dans le champ « HTML » - cela peut également être un code source SVG. Voici un exemple sous forme de
conteneur Div et de CSS (iconSize ``80,40``) ;

|img_screenshot_12|

.. code-block:: html
   :linenos:

   <style>
   /* http://projects.verou.me/bubbly/ */
   .marker-bubble {
       position: relative;
       background: #00aabb;
       border-radius: .4em;
       text-align: center;
       padding: .6rem;
       color: #FFFFFF;
   }

   .marker-bubble:after {
       content: '';
       position: absolute;
       bottom: 0;
       left: 50%;
       width: 0;
       height: 0;
       border: 1.719em solid transparent;
       border-top-color: #00aabb;
       border-bottom: 0;
       border-left: 0;
       margin-left: -0.859em;
       margin-bottom: -1.7em;
   }
   </style>
   <div class="marker-bubble">
       Moin!
   </div>

**SVG** |br|
Pour le type « SVG », un marqueur standard est restitué, dont la taille (iconSize) et la couleur peuvent être
ajustées ; le contenu du champ « Content » est affiché dans l'icône, par ex. ``#42``.

|img_screenshot_04|

**Font-Awesome** |br|
Pour le `type « Font-Awesome » <https://github.com/lennardv2/Leaflet.awesome-markers>`_, un marqueur standard
incluant une icône de Font-Awesome est restitué. Le marqueur peut, outre la taille (iconSize), également être
ajusté en couleur. Les icônes de Font-Awesome sont déjà fournies avec l'extension Cowegis - le choix se fait via
la saisie correspondante du nom de l'icône, respectivement de la classe CSS.

Dans le marqueur, les icônes de la
`Font-Awesome Free Version 6 sont actuellement disponibles <https://fontawesome.com/v6/search?ic=free>`_
par ex. « `fa-envelope <https://fontawesome.com/icons/envelope?f=classic&s=solid>`_ ».

|img_screenshot_18|

Il faut noter que le nom de l'icône dans « Classe CSS de l'icône » doit être saisi sans le préfixe, par ex.
« fa- » - donc ``envelope``. De plus, le jeu correspondant parmi « Regular, Solid, Brands » de l'icône souhaitée
doit être sélectionné.

La taille du marqueur est ajustée via l'indication « Taille de l'icône » et se rapporte au conteneur Div complet,
qui englobe aussi bien le SVG de la « goutte » que le SVG de Font-Awesome. Le conteneur Div a par défaut une
taille de ``26,40`` en pixels - pour un agrandissement de 50 %, il faudrait saisir ``39,60``.

**Sélectionner un modèle d'icône dans MetaModels**
Dans MetaModels, un nouvel attribut « Marqueur Cowegis » est disponible, avec lequel un modèle d'icône de
Cowegis peut être enregistré dans MM. Pour cela, l'attribut correspondant est créé comme d'habitude et activé
dans le masque de saisie. Lorsqu'un enregistrement est édité, un modèle d'icône peut être sélectionné via un
champ de sélection ; c'est l'ID du modèle qui est enregistré. Dans la sortie liste du réglage de rendu, le nom
du modèle est affiché par défaut - si le template de l'attribut est modifié en ``mm_attr_marker_icon_image``, un
aperçu de l'icône est également affiché en plus du nom (actuellement uniquement pour le type « Fichier »).

|img_screenshot_05|

Ensuite, dans les réglages du calque de type « Marqueur MetaModels », l'affichage des icônes individuelles peut
être ajusté. Dans la section Icône, il existe le choix « Attribut Icône » avec lequel on peut sélectionner
l'attribut créé « Marqueur Cowegis ». Comme repli pour ce réglage, une icône par défaut propre peut être
définie - ici, dans le champ de sélection, le choix d'un modèle d'icône créé est possible. Si ce réglage ne
s'applique pas non plus, l'icône par défaut de Leaflet est restituée.

|img_screenshot_06|

Sur la carte, cela ressemble alors à ceci :

|img_screenshot_07|

Configurer le popup
.....................

L'affichage des popups peut également être configuré sous Modèles. Pour cela, se rendre dans la vue « Gérer les
popups » et exécuter « Créer un popup » - puis procéder aux réglages souhaités.

Ensuite, dans les réglages du calque de type « Marqueur MetaModels », l'affichage des popups individuels est
possible. Dans la section Popup, sous « Préréglage de popup », activer le modèle souhaité. Voici un affichage
avec popup et infobulle ouverts.

|img_screenshot_08|

Créer des éléments de contrôle
.................................

Sous les cartes, sur la ligne de chaque carte, l'icône |img_control| pour créer des éléments de contrôle est
disponible. Via « Créer un élément de contrôle », différents éléments de contrôle peuvent être créés, comme par
ex. :

* Barre de copyright : L'`élément de contrôle de mention d'auteur
  <https://leafletjs.com/reference.html#control-attribution>`_ permet d'afficher les ayants droit dans une petite
  boîte de texte sur la carte.
* Élément de contrôle plein écran : Ce réglage ajoute un bouton qui bascule le
  `mode plein écran <https://github.com/brunob/leaflet.fullscreen>`_.
* Élément de contrôle des calques : L'`élément de contrôle des calques
  <https://leafletjs.com/reference.html#control-layers>`_ donne aux visiteurs du frontend la possibilité de
  basculer entre différents calques et d'activer ou de désactiver des overlays.
* Indicateur de chargement : `Leaflet.loading <https://github.com/ebrelsford/Leaflet.loading>`_ est un simple
  indicateur de chargement sous forme d'élément de contrôle.
* Élément de contrôle d'échelle : `élément de contrôle d'échelle
  <https://leafletjs.com/reference.html#control-scale>`_ simple, qui affiche l'échelle actuelle du centre de la
  carte.
* Élément de contrôle de zoom : Ce composant permet un `contrôle du comportement de zoom
  <https://leafletjs.com/reference.html#control-zoom>`_.


Créer d'autres calques
........................

Pour finir, d'autres calques peuvent être créés, affichant par ex. des marqueurs fixes dont les données ne
proviennent pas de MetaModels, ou d'autres types de cartes. Si l'élément de contrôle des calques est configuré,
les visiteurs du frontend peuvent y activer ou désactiver les calques.

Un type de calque est le `« Marker Cluster » <https://github.com/Leaflet/Leaflet.markercluster>`_, avec lequel
plusieurs marqueurs sont regroupés à un niveau de zoom faible en une icône ronde indiquant leur nombre. Après la
création du Marker Cluster, un ou plusieurs calques de marqueurs sont insérés comme sous-niveau du Marker
Cluster - les calques de marqueurs déjà existants y sont déplacés.

|img_screenshot_09|

Le nouveau calque Marker-Cluster doit également être activé dans la carte sous Calques.

|img_screenshot_10|

Selon le niveau de zoom, les marqueurs proches les uns des autres sont regroupés. La couleur de l'icône du
cluster dépend du `nombre d'éléments contenus
<https://github.com/Leaflet/Leaflet.markercluster/blob/c0f055bd5dcd1d6a733090d0cf024d7362d77bc8/src/MarkerClusterGroup.js#L824-L831>`_
et `peut être ajustée par CSS
<https://github.com/Leaflet/Leaflet.markercluster/blob/c0f055bd5dcd1d6a733090d0cf024d7362d77bc8/dist/MarkerCluster.Default.css#L1-L20>`_.
En cliquant sur un cluster, le zoom est modifié de manière à ce que le contenu soit visible.

|img_screenshot_11|


Reprendre les filtrages de MM dans la carte
---------------------------------------------

Souvent, une carte est intégrée en combinaison avec une liste MM filtrée - on souhaite alors naturellement que le
filtrage se répercute également sur les marqueurs affichés.

Cowegis ne récupère pas ses données pour la génération de la carte et de tous les autres éléments directement via
l'élément de contenu ; c'est l'élément carte qui récupère les données via son propre chemin. Cet appel ne reçoit
en revanche rien des données de filtre présentes dans l'URL.

.. note:: **À partir de MM 2.5 :** Cowegis-Layer fournit pour cela son propre template, qui reprend
   automatiquement les paramètres de filtre - voir plus bas. La surcharge de template manuelle jusqu'ici
   nécessaire n'est ainsi plus nécessaire dans le cas standard.

**Template fourni** ``ce_cowegis_map_mm-filter``

Cowegis-Layer fournit un second template pour l'élément de contenu carte. Il détermine automatiquement, via la
carte sélectionnée dans l'élément de contenu, quels paramètres d'URL les calques « Marqueur MetaModels » qui y
sont intégrés attendent pour leur réglage de filtre, et ajoute lui-même leurs valeurs actuelles à l'appel de la
carte - sans aucune adaptation propre.

Pour l'utiliser, sélectionner dans l'élément de contenu carte, sous « Réglages de template », le template
``ce_cowegis_map_mm-filter`` à la place du template standard. Il faut pour cela qu'au moins un
:ref:`réglage de filtre <component_filter>` soit renseigné au niveau du calque de marqueurs, sous « MetaModel »,
à « Réglages de filtre à appliquer » - les noms de paramètres d'URL correspondants sont déterminés
automatiquement.

Pour les cas particuliers - par ex. des paramètres d'URL propres qui ne proviennent pas d'un réglage de filtre
MM - il est toujours possible de créer un template propre avec des noms de paramètres fixes, selon le même
modèle qu'auparavant :

.. code-block:: html
   :linenos:

   <!-- templates/ce_cowegis_map_eigene-parameter.html5 -->
   <?php $this->extend('ce_cowegis_map'); ?>

   <?php $this->block('content') ?>
   <?php
   $params  = [];
   $keyList = ['address', 'address_range'];
   foreach ($keyList as $key) {
     $params[$key] = \Contao\Input::get($key);
   }
   $paramString = http_build_query($params);
   ?>
   <cowegis-map id="<?= $this->mapId ?>" style="<?= $this->mapStyle ?>"
                map-uri="<?= $this->mapUri . '&' . $paramString ?>">
   </cowegis-map>

   <?php $this->endblock() ?>

Si la carte doit s'adapter au nombre modifié de marqueurs, l'option « Ajuster les limites » doit être activée
pour la carte MM (voir ci-dessus).


Adaptations individuelles par JavaScript
-------------------------------------------

La carte peut être manipulée par JavaScript, par ex. pour afficher d'autres marqueurs ou polygones. Il faut alors
noter que certains appels peuvent le cas échéant être « écrasés » par le JavaScript de Cowegis. C'est par ex. le
cas lorsque, dans les réglages de la carte, l'option « Définir les limites » est activée : la méthode
``fitBounds()`` n'a alors aucun effet.

L'option doit alors être désactivée dans les réglages et gérée via son propre script. Avec l'extrait suivant, on
peut démarrer ses propres adaptations.

.. code-block:: html
   :linenos:

   <script>
       const element = document.getElementById("<?= $this->mapId ?>");

       const initializeMarker = function () {
           const map     = element.map;
           const leaflet = element.leaflet;

           // Own code...
       }

       if (element.map) {
           initializeMarker();
       } else {
           element.addEventListener('cowegis:ready', initializeMarker);
       }
   </script>

Un exemple serait un affichage adapté après une recherche par rayon, avec affichage du point de recherche et du
rayon.

|img_screenshot_19|


Débogage
--------

Pendant le développement, respectivement la mise en place du calque, il peut arriver que la carte ne s'affiche
plus. Souvent, l'erreur consiste en ce que le tableau JSON transmis ne peut pas être analysé. Dans les outils de
développement du navigateur, on trouve alors fréquemment le message
``SyntaxError: JSON.parse: unexpected character at line 1 column 1 of the JSON data``.

Dans l'analyse réseau, l'appel à l'API Cowegis devrait être trouvable - il ressemble à peu près à
``https://domain.tld/cowegis/api/map/3?_locale=de&es5=1&=``, le nombre étant l'ID de la carte. Cet appel peut
être ouvert dans un onglet propre du navigateur et analysé.


Migration depuis Leaflet-Maps Integration
--------------------------------------------

Qui passe de :ref:`Leaflet-Maps Integration <rst_extended_leaflet>` à Cowegis-Layer devrait tenir compte des
points suivants :

* pour les valeurs Lat/Long, seul le type d'attribut Décimal est désormais autorisé en cas de saisie individuelle
  (voir ci-dessus « Créer les données MetaModels ») - qui avait auparavant enregistré les valeurs dans un
  attribut de type Texte doit
  :ref:`adapter ce type <rst_cookbook_tips_change_table_column_name>`


Dons
----

Un grand merci pour les dons* pour l'extension à :

* `AntwortInternet <https://www.antwortinternet.com/>`_ : 200 €
* `P-Kreativ <https://p-kreativ.at/>`_ : 200 €
* `Biades <https://biades.de/>`_ : 200 €
* `AntwortInternet <https://www.antwortinternet.com/>`_ : 200 €
* `External IT Solutions <https://external.at/>`_ : 200 €
* `Klarika <https://www.klarika.de/>`_ : 200 €
* `AntwortInternet <https://www.antwortinternet.com/>`_ : 600 €

(*Dons en net)


.. |br| raw:: html

   <br />

.. |img_control| image:: /_img/screenshots/extended/cowegis_layer/control.png
.. |img_copy| image:: /_img/screenshots/extended/cowegis_layer/copy.svg
.. |img_delete| image:: /_img/screenshots/extended/cowegis_layer/delete.svg
.. |img_edit| image:: /_img/screenshots/extended/cowegis_layer/edit.svg
.. |img_layers| image:: /_img/screenshots/extended/cowegis_layer/layers.png
.. |img_marker-icon| image:: /_img/screenshots/extended/cowegis_layer/marker-icon.png
.. |img_map| image:: /_img/screenshots/extended/cowegis_layer/map.png
.. |img_map_1| image:: /_img/screenshots/extended/cowegis_layer/map_1.png
.. |img_metamodels_marker.svg| image:: /_img/screenshots/extended/cowegis_layer/metamodels_marker.svg
.. |img_screenshot_01| image:: /_img/screenshots/extended/cowegis_layer/screenshot_01.png
.. |img_screenshot_02| image:: /_img/screenshots/extended/cowegis_layer/screenshot_02.png
.. |img_screenshot_03| image:: /_img/screenshots/extended/cowegis_layer/screenshot_03.png
.. |img_screenshot_04| image:: /_img/screenshots/extended/cowegis_layer/screenshot_04.png
.. |img_screenshot_05| image:: /_img/screenshots/extended/cowegis_layer/screenshot_05.png
.. |img_screenshot_06| image:: /_img/screenshots/extended/cowegis_layer/screenshot_06.png
.. |img_screenshot_07| image:: /_img/screenshots/extended/cowegis_layer/screenshot_07.png
.. |img_screenshot_08| image:: /_img/screenshots/extended/cowegis_layer/screenshot_08.png
.. |img_screenshot_09| image:: /_img/screenshots/extended/cowegis_layer/screenshot_09.png
.. |img_screenshot_10| image:: /_img/screenshots/extended/cowegis_layer/screenshot_10.png
.. |img_screenshot_11| image:: /_img/screenshots/extended/cowegis_layer/screenshot_11.png
.. |img_screenshot_12| image:: /_img/screenshots/extended/cowegis_layer/screenshot_12.png
.. |img_screenshot_13| image:: /_img/screenshots/extended/cowegis_layer/screenshot_13.png
.. |img_screenshot_14| image:: /_img/screenshots/extended/cowegis_layer/screenshot_14.png
.. |img_screenshot_15| image:: /_img/screenshots/extended/cowegis_layer/screenshot_15.png
.. |img_screenshot_16| image:: /_img/screenshots/extended/cowegis_layer/screenshot_16.png
.. |img_screenshot_17| image:: /_img/screenshots/extended/cowegis_layer/screenshot_17.png
.. |img_screenshot_18| image:: /_img/screenshots/extended/cowegis_layer/screenshot_18.png
.. |img_screenshot_19| image:: /_img/screenshots/extended/cowegis_layer/screenshot_19.png
.. |img_screenshot_20| image:: /_img/screenshots/extended/cowegis_layer/screenshot_20.png
