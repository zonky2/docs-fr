.. _component_attribute_color:

|svg_attr_color_22| |img_color| Sélecteur de couleur
=====================================================

L'attribut « Sélecteur de couleur » permet de choisir une couleur web, y compris une
valeur de saturation, via un widget de sélecteur de couleur intégré. Cas d'utilisation
typiques :

* Couleurs de fond, couleurs de texte ou couleurs d'accentuation pour des éléments de
  mise en page
* Marquage par couleur de catégories ou d'événements
* Valeurs de couleur avec transparence (couleur + saturation)

Dans le backend, deux champs de saisie apparaissent : un champ texte pour le code
couleur hexadécimal (6 caractères, par ex. ``ff0000``) et un second champ pour la
valeur de saturation. La couleur peut être choisie visuellement via l'icône du
sélecteur de couleur.


Installation
------------

L'attribut s'installe via le **Contao Manager** ou **Composer** :

.. code-block:: bash

   composer require metamodels/attribute_color


Réglages lors de la création de l'attribut
-------------------------------------------

L'attribut Sélecteur de couleur ne possède pas de réglages spécifiques lors de sa
création. Les réglages généraux de l'attribut sont utilisés :

* Nom, nom de colonne, description
* Autoriser le remplacement dans les variantes

.. note:: L'option « Valeurs uniques » n'est pas disponible pour cet attribut, car les
   valeurs de couleur sont enregistrées sous forme de données sérialisées.


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
     - Sélection d'un template propre pour l'affichage de la valeur de couleur.
   * - Classe CSS
     - Classe CSS optionnelle ajoutée à l'élément de sortie.


Réglages dans le masque de saisie
-----------------------------------

Lorsque l'attribut est ajouté à un masque de saisie, les options suivantes sont
disponibles :

**Présentation**

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Option
     - Description
   * - Classe backend
     - Classes CSS pour l'affichage du champ dans le formulaire du backend.
   * - Template pour le backend
     - Sélection d'un template de widget propre pour le formulaire du backend.
   * - Template pour le frontend
     - Sélection d'un template de widget propre pour l'édition en frontend
       (uniquement si « Frontend Editing » est installé).

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

L'attribut Sélecteur de couleur peut être utilisé avec les règles de filtre
suivantes :

.. list-table::
   :header-rows: 1
   :widths: 30 70

   * - Règle de filtre
     - Remarque
   * - Requête simple
     - Filtre selon une valeur de couleur exacte via un paramètre d'URL.
   * - Sélection unique
     - Sélection d'une valeur de couleur parmi une liste de valeurs existantes.


Fonctions particulières
-------------------------

**Stockage en base de données**

La valeur de couleur est enregistrée sous forme de tableau PHP sérialisé dans un champ
``TINYBLOB NULL``. Le tableau contient deux éléments : le code couleur hexadécimal
(sans ``#``) et la valeur de saturation. Une valeur vide est enregistrée comme
``NULL``.

**Widget sélecteur de couleur**

Dans le backend, un assistant de sélection de couleur s'affiche à côté du champ texte,
permettant de choisir la couleur visuellement. Le premier champ texte reçoit le code
couleur hexadécimal à six chiffres, le second la valeur de saturation.

**Tri par valeur de couleur**

Le tri par valeur de couleur s'effectue via une conversion des valeurs hexadécimales
en clés de tri numériques, de sorte que les couleurs puissent être ordonnées de
manière cohérente selon leur valeur numérique.


.. |svg_attr_color_22| image:: /_img/icons_svg/color.svg
   :width: 22px
.. |img_color| image:: /_img/icons/color.png
.. |br| raw:: html

   <br />
