.. _component_attribute_timestamp:

|svg_attr_timestamp_22| |img_timestamp| Date
=============================================

L'attribut « Date » stocke une date, une heure ou les deux sous forme
d'horodatage Unix (``bigint``). Dans le backend, un sélecteur de date s'affiche
avec le format de date configuré dans Contao. Domaines d'application typiques :

* Date de parution, date d'événement, date d'expiration
* Horaires d'ouverture (heure seule)
* Période de réservation avec date de début et de fin (deux attributs Date)
* Horodatage d'événements

.. note:: Les valeurs de date sont stockées sous forme d'horodatage Unix. Pour
   des filtrages ou requêtes SQL personnalisés, des conversions peuvent
   s'avérer nécessaires (par ex. ``FROM_UNIXTIME()`` en MySQL).

.. seealso:: Pour un sélecteur de date moderne en frontend :
   :ref:`rst_cookbook_templates_flatpickr-integration`


Installation
------------

L'attribut s'installe via le **Contao Manager** ou **Composer** :

.. code-block:: bash

   composer require metamodels/attribute_timestamp


Réglages à la création de l'attribut
-------------------------------------

Outre les réglages généraux de l'attribut (nom, nom de colonne, description,
autoriser la surcharge de variante), l'attribut Date propose l'option
spécifique suivante :

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Option
     - Description
   * - Schéma
     - Détermine le type de saisie utilisé dans le backend :

       * **Date** – date uniquement (sans heure)
       * **Date et heure** – date accompagnée de l'heure
       * **Heure** – heure uniquement (sans date)


Réglages dans les réglages de rendu
--------------------------------------

L'attribut Date possède ses propres réglages de rendu :

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Option
     - Description
   * - Format
     - Format de date personnalisé pour l'affichage, formaté avec la fonction
       PHP ``date()`` (par ex. ``d.m.Y``, ``H:i``, ``d.m.Y H:i``). Si le champ
       est laissé vide, le format standard configuré dans le système Contao
       est utilisé.
   * - Template
     - Choix d'un template personnalisé pour l'affichage de la valeur de date.
   * - Classe CSS
     - Classe CSS optionnelle ajoutée à l'élément de sortie.


Réglages dans le masque de saisie
------------------------------------

Lorsque l'attribut Date est ajouté à un masque de saisie, les options
suivantes sont disponibles :

**Présentation**

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Option
     - Description
   * - Classe backend
     - Classes CSS pour la présentation du champ dans le formulaire backend
       (par ex. ``w50`` pour une demi-largeur).
   * - Template pour le backend
     - Choix d'un template de widget personnalisé pour le formulaire backend.
   * - Template pour le frontend
     - Choix d'un template de widget personnalisé pour l'édition en frontend
       (disponible uniquement si l'extension « Frontend Editing » est installée).

**Fonctions**

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Option
     - Description
   * - Champ obligatoire
     - Rend le champ obligatoire.
   * - Gestion de la date et de l'heure
     - Détermine quelle partie de l'horodatage est remise à 0 lors de
       l'enregistrement. Important pour un filtrage correct :

       * **Enregistrer uniquement la date sans l'heure** – l'heure est
         réinitialisée à ``00:00:00``. Utile pour les filtres purement
         basés sur la date.
       * **Enregistrer uniquement l'heure sans la date** – la date est
         réinitialisée au jour de départ de l'époque Unix (01.01.1970).

**Aperçu (filtre et recherche backend)**

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Option
     - Description
   * - Filtrable
     - L'attribut est disponible dans le backend comme critère de filtrage.
   * - Utilisable pour la recherche
     - L'attribut est disponible dans le backend comme champ de recherche.


Règles de filtre
-------------------

L'attribut Date peut être utilisé avec les règles de filtre suivantes :

.. list-table::
   :header-rows: 1
   :widths: 30 70

   * - Règle de filtre
     - Remarque
   * - Valeur de/à pour une date
     - Filtre par plage de/à pour un seul attribut Date ; par ex. tous les
       événements dans une période donnée. Template propre :
       ``mm_filteritem_datepicker.html5`` pour un sélecteur de date HTML5
       (format ``AAAA-MM-JJ``).
   * - Valeur de/à pour deux dates
     - Filtre par plage sur deux attributs Date ; par ex. lorsque la date de
       début et de fin sont stockées comme attributs distincts.


Fonctions spéciales
---------------------

**Stockage en base de données**

Les valeurs de date et d'heure sont stockées sous forme d'horodatage Unix
dans un champ ``bigint(10) NULL``. Une valeur vide est enregistrée comme
``NULL``.

**Formatage**

L'affichage est contrôlé par l'événement Contao ``ParseDateEvent``. Le format
défini dans les réglages de rendu prévaut sur le format système général de
Contao. Dans les templates, la valeur formatée est directement disponible
sous ``$arrData['html5']`` ou ``$arrData['text']``.


.. |svg_attr_timestamp_22| image:: /_img/icons_svg/timestamp.svg
   :width: 22px
.. |img_timestamp| image:: /_img/icons/timestamp.png
.. |br| raw:: html

   <br />
