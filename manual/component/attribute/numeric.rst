.. _component_attribute_numeric:

|svg_attr_numeric_22| |img_numeric| Numérique
=============================================

L'attribut « Numérique » enregistre des valeurs entières (integer). Cas
d'utilisation typiques :

* Quantités, nombres d'unités, niveaux de stock
* Années, indications d'âge
* Valeurs de tri ou de priorité
* Compteurs et classements

.. note:: Pour les codes postaux ou les numéros de téléphone, l'attribut « Texte »
   devrait être utilisé, car il ne s'agit pas de véritables valeurs numériques et
   les zéros initiaux seraient perdus.


Installation
------------

L'attribut s'installe via le **Contao Manager** ou **Composer** :

.. code-block:: bash

   composer require metamodels/attribute_numeric


Réglages lors de la création de l'attribut
-------------------------------------------

L'attribut Numérique ne possède pas de réglages spécifiques. Seuls les réglages
généraux de l'attribut sont utilisés :

* Nom, nom de colonne, description
* Valeurs uniques
* Autoriser le remplacement dans les variantes


Réglages dans les réglages de rendu
-------------------------------------

L'attribut Numérique ne possède pas de réglages de rendu spécifiques. Dans la
liste des attributs d'un réglage de rendu, les options habituelles sont
disponibles :

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Option
     - Description
   * - Template
     - Sélection d'un template propre pour l'affichage de la valeur numérique.
       Si aucun template n'est indiqué, l'affichage se fait sous forme de texte
       simple.
   * - Classe CSS
     - Classe CSS optionnelle ajoutée à l'élément de sortie.


Réglages dans le masque de saisie
-----------------------------------

Lorsque l'attribut Numérique est ajouté à un masque de saisie, les options
suivantes sont disponibles :

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

L'attribut Numérique peut être utilisé avec les règles de filtre suivantes :

.. list-table::
   :header-rows: 1
   :widths: 30 70

   * - Règle de filtre
     - Remarque
   * - Valeur de/à pour un champ
     - Filtre par plage de/à pour un seul attribut Numérique ; par ex. pour une
       recherche par tranche d'âge ou un filtrage par quantité.
   * - Valeur de/à pour deux champs
     - Filtre par plage sur deux attributs Numérique ; par ex. lorsqu'une plage
       de valeurs est représentée par un attribut « de » et un attribut « à ».


Fonctions particulières
-------------------------

**Validation de la saisie**

Le champ de saisie est soumis au contrôle par expression régulière ``digit`` et
n'accepte que des saisies numériques entières. La longueur maximale est de 10
caractères (correspondant à la plage de valeurs d'un entier 32 bits).

**Stockage en base de données**

La valeur est enregistrée sous la forme ``int(10) NULL default NULL``. Une
valeur vide est enregistrée comme ``NULL`` (compatible avec le mode strict de
MySQL).


.. |svg_attr_numeric_22| image:: /_img/icons_svg/numeric.svg
   :width: 22px
.. |img_numeric| image:: /_img/icons/numeric.png
.. |br| raw:: html

   <br />
