.. _component_attribute_text:

|svg_attr_text_22| |img_text| Texte
===================================

L'attribut « Texte » est le champ de texte le plus simple de MetaModels et stocke
de courts textes jusqu'à 255 caractères. Domaines d'application typiques :

* Noms, titres, intitulés
* Descriptions courtes, sous-titres
* Codes, références articles, références
* Numéros de téléphone, codes postaux (en tant que texte, pas en tant que nombre)

.. note:: Pour des textes plus longs (au-delà de 255 caractères), il convient
   d'utiliser l'attribut :ref:`component_attribute_longtext`.

.. seealso:: Pour les MetaModels multilingues, l'attribut
   :ref:`component_attribute_translatedtext` est disponible.


Installation
------------

L'attribut s'installe via le **Contao Manager** ou **Composer** :

.. code-block:: bash

   composer require metamodels/attribute_text


Réglages à la création de l'attribut
-------------------------------------

L'attribut Texte ne possède pas de réglages spécifiques propres à sa création.
Seuls les réglages généraux de l'attribut sont utilisés :

* Nom, nom de colonne, description
* Valeurs uniques
* Autoriser la surcharge de variante


Réglages dans les réglages de rendu
--------------------------------------

L'attribut Texte ne possède pas de réglages de rendu qui lui soient propres.
Dans la liste des attributs d'un réglage de rendu, les options habituelles
sont disponibles :

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Option
     - Description
   * - Template
     - Choix d'un template personnalisé pour l'affichage de la valeur du texte.
       Si aucun template n'est indiqué, l'affichage se fait sous forme de texte simple.
   * - Classe CSS
     - Classe CSS optionnelle ajoutée à l'élément de sortie.


Réglages dans le masque de saisie
------------------------------------

Lorsque l'attribut Texte est ajouté à un masque de saisie, les options
suivantes sont disponibles :

**Présentation**

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Option
     - Description
   * - Classe backend
     - Classes CSS pour la présentation du champ dans le formulaire backend
       (par ex. ``w50`` pour une demi-largeur, ``long`` pour la pleine largeur).
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
   * - Regular Expression
     - Validation de la saisie à l'aide d'une expression régulière prédéfinie.
       Modèles disponibles :

       * **digit** – uniquement des chiffres
       * **natural** – nombres entiers positifs
       * **alpha** – uniquement des lettres
       * **alnum** – lettres et chiffres
       * **extnd** – tout sauf ``#`` et ``<>``
       * **date** – date au format configuré
       * **time** – heure au format configuré
       * **datim** – date et heure
       * **friendly** – nom convivial (pour e-mail)
       * **email** – adresse e-mail
       * **emails** – adresses e-mail séparées par des virgules
       * **url** – adresse URL
       * **alias** – caractères valides pour un alias
       * **phone** – numéro de téléphone
       * **prcnt** – pourcentage (0–100)
       * **locale** – code de langue (par ex. ``de``, ``de_DE``)
       * **language** – code de langue
       * **fieldname** – nom de champ valide

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

L'attribut Texte peut être utilisé avec les règles de filtre suivantes :

.. list-table::
   :header-rows: 1
   :widths: 30 70

   * - Règle de filtre
     - Remarque
   * - Recherche textuelle
     - Saisie libre pour la recherche dans le champ de texte.
   * - Requête simple
     - Filtre selon une valeur exacte ou partielle via un paramètre d'URL.
   * - Sélection simple
     - Choix d'une valeur dans une liste des valeurs de texte existantes.
   * - Sélection multiple
     - Sélection multiple parmi les valeurs de texte existantes.
   * - Registre
     - Filtre selon la première lettre de la valeur de texte.
   * - Recherche par Levenshtein
     - Recherche par similarité avec tolérance aux fautes de frappe ; nécessite
       le paquet ``attribute_levenshtein``.
   * - Loupe
     - Recherche par index plein texte ; nécessite le paquet ``filter_loupe``
       (à partir de MM 2.4).


Fonctions spéciales
---------------------

**Sélecteur d'icônes**
L'attribut Texte convient également pour intégrer un :ref:`sélecteur d'icônes
pour le masque de saisie <rst_cookbook_specials_picker-for-icons>`.


**Stockage en base de données**

Le texte est stocké en tant que ``varchar(255) NULL``. Une valeur vide est
enregistrée comme ``NULL`` (compatible avec le mode strict de MySQL). La
limite de 255 caractères est fixée par le type de colonne en base de données.

**Entités HTML**

L'attribut traite automatiquement les entités HTML de Contao (``basicEntities``).
Les caractères spéciaux sont correctement encodés et décodés lors de
l'enregistrement et de l'affichage.


.. |svg_attr_text_22| image:: /_img/icons_svg/text.svg
   :width: 22px
.. |img_text| image:: /_img/icons/text.png
.. |br| raw:: html

   <br />
