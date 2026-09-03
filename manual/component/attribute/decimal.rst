.. _component_attribute_decimal:

|svg_attr_decimal_22| |img_decimal| Décimal
===========================================

L'attribut « Décimal » enregistre des nombres décimaux (nombres à virgule flottante
en double précision). Cas d'utilisation typiques :

* Montants et prix (par ex. ``19.99``)
* Mesures et poids (par ex. ``1.75``, ``0.5``)
* Coordonnées géographiques (latitude/longitude)
* Valeurs en pourcentage ou valeurs de notation

.. note:: Pour les codes postaux ou les numéros de téléphone, l'attribut « Texte »
   doit être utilisé, car il ne s'agit pas de véritables valeurs numériques et les
   zéros initiaux seraient perdus. Pour la recherche par rayon, un attribut Décimal
   distinct doit être créé pour la latitude et pour la longitude.

.. note:: La saisie s'effectue avec un **point** comme séparateur décimal
   (et non une virgule).


Installation
------------

L'attribut s'installe via le **Contao Manager** ou **Composer** :

.. code-block:: bash

   composer require metamodels/attribute_decimal


Réglages lors de la création de l'attribut
-------------------------------------------

L'attribut Décimal ne possède pas de réglages spécifiques. Seuls les réglages
généraux de l'attribut sont utilisés :

* Nom, nom de colonne, description
* Valeurs uniques
* Autoriser le remplacement dans les variantes


Réglages dans les réglages de rendu
-------------------------------------

L'attribut Décimal ne possède pas de réglages de rendu spécifiques. Dans la liste
des attributs d'un réglage de rendu, les options habituelles sont disponibles :

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Option
     - Description
   * - Template
     - Sélection d'un template propre pour l'affichage de la valeur décimale.
       Si aucun template n'est indiqué, l'affichage se fait sous forme de texte
       simple.
   * - Classe CSS
     - Classe CSS optionnelle ajoutée à l'élément de sortie.


Réglages dans le masque de saisie
-----------------------------------

Lorsque l'attribut Décimal est ajouté à un masque de saisie, les options suivantes
sont disponibles :

**Présentation**

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Option
     - Description
   * - Classe backend
     - Classes CSS pour l'affichage du champ dans le formulaire du backend (par
       ex. ``w50`` pour une demi-largeur).
   * - Template pour le backend
     - Sélection d'un template de widget propre pour le formulaire du backend.
   * - Template pour le frontend
     - Sélection d'un template de widget propre pour l'édition en frontend
       (disponible uniquement si l'extension « Frontend Editing » est installée).

**Fonctions**

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Option
     - Description
   * - Champ obligatoire
     - Rend le champ obligatoire.

**Aperçu (filtre et recherche backend)**

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Option
     - Description
   * - Filtrable
     - L'attribut est disponible comme critère de filtrage dans le backend.
   * - Cherchable
     - L'attribut est disponible comme champ de recherche dans le backend.


Règles de filtre
-------------------

L'attribut Décimal peut être utilisé avec les règles de filtre suivantes :

.. list-table::
   :header-rows: 1
   :widths: 30 70

   * - Règle de filtre
     - Remarque
   * - Valeur de/à pour un champ
     - Filtre par plage de/à pour un seul attribut Décimal ; par ex. pour une
       recherche par fourchette de prix avec valeur minimale et maximale.
   * - Valeur de/à pour deux champs
     - Filtre par plage sur deux attributs Décimal ; par ex. lorsqu'une plage
       de valeurs est représentée par un attribut « de » et un attribut « à »
       (par ex. la fourchette de prix d'une offre).
   * - Recherche par rayon
     - Pour les coordonnées géographiques : filtre selon un rayon autour d'un
       point de recherche, lorsque la latitude et la longitude sont enregistrées
       chacune dans un attribut Décimal.


Fonctions particulières
-------------------------

**Stockage en base de données**

La valeur est enregistrée sous la forme ``double NULL default NULL``. Une valeur
vide est enregistrée comme ``NULL`` (compatible avec le mode strict de MySQL).

**Validation de la saisie**

Le champ de saisie est soumis au contrôle par expression régulière ``digit``, qui
n'accepte que des saisies numériques (y compris le point décimal et le signe).


.. |svg_attr_decimal_22| image:: /_img/icons_svg/decimal.svg
   :width: 22px
.. |img_decimal| image:: /_img/icons/decimal.png

.. |br| raw:: html

   <br />
