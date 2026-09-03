.. _component_attribute_combinedvalues:

|svg_attr_combinedvalues_22| |img_combinedvalues| Valeurs combinées
======================================================================

L'attribut « Valeurs combinées » réunit les valeurs de plusieurs attributs existants
en une nouvelle valeur texte enregistrée. Cas d'utilisation typiques :

* Composer prénom et nom en « Nom, Prénom » pour l'affichage ou la recherche
* Créer des identifiants composés à partir de plusieurs champs, par ex. pour l'attribut
  :ref:`Sélection unique <component_attribute_select>` ou :ref:`Sélection multiple <component_attribute_tags>`
* Préparer des textes de sortie devant être combinés et enregistrés de manière fixe

La combinaison s'effectue via une chaîne de format ``sprintf``. Tous les attributs
MetaModels existants ainsi que les méta-champs système (ID, PID, tri, etc.) peuvent
être choisis comme champs source.

.. seealso:: Pour les MetaModels multilingues, l'attribut
   :ref:`component_attribute_translatedcombinedvalues` est disponible.


Installation
------------

L'attribut s'installe via le **Contao Manager** ou **Composer** :

.. code-block:: bash

   composer require metamodels/attribute_combinedvalues


Réglages lors de la création de l'attribut
-------------------------------------------

Outre les réglages généraux de l'attribut (nom, nom de colonne, description, valeurs
uniques, autoriser le remplacement dans les variantes), l'attribut propose les options
spécifiques suivantes :

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Option
     - Description
   * - Format
     - Chaîne de format ``sprintf`` définissant comment les valeurs source sont
       combinées. Un espace réservé ``%s`` doit exister pour chaque valeur de
       champ sélectionnée. Exemples :

       * ``%s, %s`` → « Dupont, Jean »
       * ``%s (%s)`` → « Produit A (Catégorie B) »
       * ``%s-%s-%s`` → « 2024-01-15 »

       Toutes les variantes d'espaces réservés de ``sprintf`` sont possibles
       (voir https://www.php.net/sprintf).
   * - Champs
     - Sélection des attributs source dans l'ordre dans lequel ils sont insérés
       dans le format. Outre les attributs propres au MetaModel, des méta-champs
       système sont également disponibles : ID, PID, tri, horodatage, groupe de
       variante, base de variante.
   * - Forcer l'actualisation
     - Si cette case est cochée, la valeur combinée est automatiquement
       régénérée à chaque modification de l'un des attributs source. Le champ
       est alors affiché en lecture seule dans le backend. Sans cette option,
       une valeur déjà générée reste inchangée.


Réglages dans les réglages de rendu
-------------------------------------

L'attribut « Valeurs combinées » ne possède pas de réglages de rendu spécifiques.
Dans la liste des attributs d'un réglage de rendu, les options habituelles sont
disponibles :

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Option
     - Description
   * - Template
     - Sélection d'un template propre pour l'affichage de la valeur combinée. Si
       aucun template n'est indiqué, l'affichage se fait sous forme de texte
       simple.
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
     - Classes CSS pour l'affichage du champ dans le formulaire du backend (par
       ex. ``long`` pour la pleine largeur).
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
     - Rend le champ obligatoire. Automatiquement défini si l'option « Valeurs
       uniques » est activée.
   * - Toujours enregistrer
     - Le champ est enregistré même si sa valeur n'a pas changé. Automatiquement
       défini si « Forcer l'actualisation » est activé.

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

L'attribut « Valeurs combinées » peut être utilisé avec les règles de filtre
suivantes :

.. list-table::
   :header-rows: 1
   :widths: 30 70

   * - Règle de filtre
     - Remarque
   * - Recherche textuelle
     - Saisie de texte libre pour rechercher dans la valeur combinée.
   * - Requête simple
     - Filtre selon une valeur exacte ou partielle via un paramètre d'URL.
   * - Sélection unique
     - Sélection d'une valeur parmi la liste des valeurs combinées existantes.
   * - Sélection multiple
     - Sélection multiple parmi la liste des valeurs combinées existantes.
   * - Registre
     - Filtre selon la première lettre de la valeur combinée.
   * - Recherche assistée par Levenshtein
     - Recherche par similarité avec tolérance aux fautes de frappe ; nécessite
       le paquet ``attribute_levenshtein``.
   * - Loupe
     - Recherche par index plein texte ; nécessite le paquet ``filter_loupe``
       (à partir de MM 2.4).


Fonctions particulières
-------------------------

**Unicité avec numérotation automatique**

Si « Valeurs uniques » est activé, MetaModels vérifie après la génération si la
valeur combinée existe déjà. En cas de doublon, un compteur entre parenthèses est
automatiquement ajouté : ``Dupont, Jean (2)``, ``Dupont, Jean (3)``, etc.

**Comportement lors de la copie d'un jeu de données**

Si « Forcer l'actualisation » est activé, aucune valeur n'est reprise lors de la
duplication d'un jeu de données. La valeur combinée est automatiquement régénérée
à l'enregistrement du nouveau jeu de données (comportement ``doNotCopy``).

**Espaces réservés de format**

Tous les espaces réservés ``sprintf`` peuvent être utilisés, pas uniquement ``%s``.
Par exemple, ``%05d`` formate un nombre avec des zéros initiaux sur 5 chiffres. Le
nombre d'espaces réservés doit correspondre au nombre de champs sélectionnés.

**Stockage en base de données**

La valeur combinée est enregistrée sous la forme ``text NULL``. Une valeur vide est
enregistrée comme ``NULL`` (compatible avec le mode strict de MySQL).


.. |svg_attr_combinedvalues_22| image:: /_img/icons_svg/combinedvalues.svg
   :width: 22px
.. |img_combinedvalues| image:: /_img/icons/combinedvalues.png

.. |br| raw:: html

   <br />
