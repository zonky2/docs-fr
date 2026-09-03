.. _component_filter_perimeter-search:

|svg_filt_perimeter_search_22| |img_filter_perimetersearch| Recherche par périmètre
========================================================================================

La règle de filtre « Recherche par périmètre » (paquet
``filter_perimetersearch``) filtre les éléments selon leur position
géographique. Les visiteurs saisissent une adresse ou des coordonnées et
choisissent un rayon de recherche ; la règle de filtre détermine tous les
éléments dont les géocoordonnées (latitude/longitude) se situent dans le
périmètre indiqué.

Il est nécessaire que les éléments disposent de leurs géocoordonnées, soit dans
un seul :ref:`attribut LatLong <component_attribute_latlong>`, soit dans deux
attributs distincts de type décimal ou texte (latitude et longitude). Pour la
géocodification des adresses en coordonnées, des services de recherche externes
sont utilisés (par ex. OpenStreetMap/Nominatim, API Google Maps).

.. seealso:: Documentation détaillée sur la recherche par périmètre :
   :ref:`extended_perimetersearch`

.. note:: **À partir de MM 2.5 :** si le champ d'adresse est vidé, la sélection
   de périmètre précédemment choisie disparaît également du widget - auparavant,
   elle restait visible bien qu'elle n'ait plus aucun effet sans adresse
   (`Issue #31 <https://github.com/MetaModels/filter_perimetersearch/issues/31>`_).
   Dans MM 2.4, le comportement précédent est conservé.

.. note:: **À partir de MM 2.5 :** si un :ref:`attribut LatLong
   <component_attribute_latlong>` avec index spatial activé est utilisé
   (attribut unique), la recherche par périmètre utilise automatiquement un
   préfiltre par boîte englobante (bounding box) assisté par index - plusieurs
   fois plus rapide que sans index, selon le volume de données. Détails et
   chiffres de référence : :ref:`Fonctions particulières de l'attribut LatLong
   <component_attribute_latlong_special>`.


Installation
------------

La règle de filtre s'installe via le **Contao Manager** ou **Composer** :

.. code-block:: bash

   composer require metamodels/filter_perimetersearch


Réglages lors de la création de la règle de filtre
----------------------------------------------------

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Réglage
     - Description
   * - Type
     - Sélection du type de règle de filtre – ici : « Recherche par
       périmètre ».
   * - Activé
     - Active ou désactive cette règle de filtre.
   * - Commentaire
     - Champ de texte libre pour décrire l'objectif de cette règle de filtre.
   * - Mode de données
     - Détermine comment les géocoordonnées des éléments sont stockées :

       * **Attribut unique** – Les coordonnées sont stockées dans un seul
         :ref:`attribut LatLong <component_attribute_latlong>`. Option
         supplémentaire : **Attribut (unique)** – sélection de l'attribut
         (seuls les attributs LatLong sont sélectionnables).
       * **Deux attributs** – Latitude et longitude sont stockées dans deux
         attributs distincts (:ref:`décimal <component_attribute_decimal>` ou
         :ref:`texte <component_attribute_text>`). Options supplémentaires :
         **Premier attribut (Lat)** et **Second attribut (Long)**.
   * - Paramètre d'URL
     - La clé du paramètre d'URL pour la saisie de l'adresse/des coordonnées.


Réglages du widget frontend
----------------------------

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Réglage
     - Description
   * - Paramètre d'URL
     - La clé du paramètre d'URL utilisée pour transmettre la valeur du filtre.
       Si elle n'est pas précisée, le nom de colonne de l'attribut est utilisé.
       Avec ``auto_item``, seule la valeur – sans clé – est intégrée dans l'URL.
   * - Type d'URL pour le paramètre
     - Détermine si le paramètre est transmis sous forme de slug (URL explicite)
       ou de paramètre GET (à partir de MM 2.4) - :ref:`voir SEO
       <rst_cookbook_tips_seo_filter-url>`
   * - Libellé
     - Intitulé du champ de saisie de l'adresse.
   * - Texte indicatif
     - Texte indicatif dans le champ de saisie de l'adresse.
   * - Template (champ d'adresse)
     - Template pour l'affichage du champ de saisie de l'adresse.
   * - Libellé (périmètre)
     - Intitulé du widget de sélection du périmètre.
   * - Template (périmètre)
     - Template pour l'affichage du widget de périmètre. Par défaut :
       ``mm_filteritem_default``.
   * - Mode de périmètre
     - Détermine comment le rayon de recherche est déterminé :

       * **Libre** – Le visiteur saisit le rayon sous forme de valeur
         numérique. Option supplémentaire : **Texte indicatif (périmètre)**.
       * **Prédéfini** – Un rayon fixe est utilisé. Option supplémentaire :
         **Rayon prédéfini** (valeur en kilomètres).
       * **Sélection** – Le visiteur choisit parmi une liste prédéfinie de
         rayons. Option supplémentaire : **Sélection de rayons** (tableau MCW
         avec valeur et indicateur par défaut).
   * - Mode de pays
     - Détermine si et comment un pays est prédéfini pour la géocodification :

       * **Aucun pays** – Pas de filtre de pays.
       * **Prédéfini** – Pays fixe (code ISO). Option supplémentaire :
         **Pays prédéfini**.
       * **Paramètre GET** – Le pays est transmis via un paramètre d'URL.
         Option supplémentaire : **Paramètre GET du pays**.
   * - Services de recherche
     - Assistant multicolonne pour configurer les services qui convertissent
       une adresse en géocoordonnées. Services disponibles (selon
       l'installation) :

       * **Coordonnées** – Saisie directe des coordonnées
       * **Google Maps** – Résolution d'adresse via l'API Google Maps
       * **OpenStreetMap** – Résolution d'adresse via l'API Nominatim

       Pour les services nécessitant un jeton API, celui-ci peut être saisi
       dans le champ « Jeton API ».

       Les services de recherche sont traités dans l'ordre, de haut en bas, et
       s'arrêtent au premier résultat. Si, en plus de la saisie d'une adresse,
       la saisie de coordonnées doit également être possible dans le frontend,
       ce service doit figurer en premier. Sur les appareils mobiles, les
       valeurs latitude/longitude peuvent être lues directement depuis
       l'appareil via JavaScript.


Attributs compatibles
----------------------

Selon le mode de données choisi, la règle de filtre « Recherche par périmètre »
nécessite l'un des attributs suivants :

* :ref:`LatLong <component_attribute_latlong>` (attribut unique – recommandé,
  prend en charge un index spatial pour une recherche par périmètre nettement
  plus rapide)
* :ref:`Décimal <component_attribute_decimal>` ou :ref:`Texte
  <component_attribute_text>` (deux attributs – pour la latitude et la
  longitude séparément)

En complément, l'attribut :ref:`Distance géographique
<component_attribute_geodistance>` peut être utilisé pour l'affichage et le tri
selon la distance.


.. |svg_filt_perimeter_search_22| image:: /_img/icons_svg/filter_perimetersearch.svg
   :width: 22px
.. |img_filter_perimetersearch| image:: /_img/icons/filter_default.png

.. |br| raw:: html

   <br />
