.. _component_attribute_translatedcombinedvalues:

|svg_attr_translatedcombinedvalues_22| |img_combinedvalues| Entrées combinées traduites
==========================================================================================

L'attribut « Entrées combinées traduites » est la variante multilingue de
l'attribut :ref:`Entrées combinées <component_attribute_combinedvalues>`. Il
combine les valeurs de plusieurs attributs en une valeur de texte stockée —
séparément pour chaque langue. Si des attributs source traduits sont
utilisés, la valeur combinée est calculée dans la variante linguistique
correspondante des champs source. Les valeurs sont enregistrées dans la
table de traduction ``tl_metamodel_translatedtext``.

Domaines d'application typiques :

* Assemblage du prénom et du nom dans un ordre dépendant de la langue
  (par ex. « Jean Dupont » en français, « Dupont Jean » dans d'autres langues)
* Identifiants combinés basés sur des attributs source traduits
* Valeurs de recherche ou d'affichage spécifiques à la langue

.. seealso:: La variante monolingue de cet attribut est décrite dans
   :ref:`component_attribute_combinedvalues`.

.. seealso:: Des indications sur le multilinguisme dans MetaModels se
   trouvent sur la page :ref:`component_multi-language`.


Installation
------------

L'attribut s'installe via le **Contao Manager** ou **Composer** :

.. code-block:: bash

   composer require metamodels/attribute_translatedcombinedvalues


Réglages à la création de l'attribut
-------------------------------------

Outre les réglages généraux de l'attribut, l'attribut propose les options
spécifiques suivantes :

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Option
     - Description
   * - Format
     - Chaîne de format ``sprintf`` déterminant comment les valeurs source
       sont combinées. Un espace réservé ``%s`` doit exister pour chaque
       valeur de champ sélectionnée. Exemples :

       * ``%s, %s`` → « Dupont, Jean »
       * ``%s (%s)`` → « Produit A (Catégorie B) »
       * ``%s-%s-%s`` → « 2024-01-15 »

       Toutes les variantes d'espaces réservés de ``sprintf`` sont possibles
       (voir https://www.php.net/sprintf).
   * - Champs
     - Choix des attributs source, dans l'ordre où ils sont insérés dans le
       format. Outre les attributs MetaModels propres, les métachamps
       système sont également disponibles : ID, PID, tri, horodatage,
       groupe de variantes, base de variante.
   * - Forcer l'actualisation
     - Si cette case est cochée, la valeur combinée est régénérée
       automatiquement à chaque modification de l'un des attributs source.
       Le champ est alors affiché en lecture seule dans le backend.


Réglages dans les réglages de rendu
--------------------------------------

L'attribut ne possède pas de réglages de rendu qui lui soient propres. Dans
la liste des attributs d'un réglage de rendu, les options habituelles sont
disponibles :

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Option
     - Description
   * - Template
     - Choix d'un template personnalisé pour l'affichage de la valeur
       combinée.
   * - Classe CSS
     - Classe CSS optionnelle ajoutée à l'élément de sortie.


Réglages dans le masque de saisie
------------------------------------

Lorsque l'attribut est ajouté à un masque de saisie, les options suivantes
sont disponibles :

**Présentation**

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Option
     - Description
   * - Classe backend
     - Classes CSS pour la présentation du champ dans le formulaire backend
       (par ex. ``long`` pour la pleine largeur).
   * - Template pour le backend
     - Choix d'un template de widget personnalisé pour le formulaire backend.
   * - Template pour le frontend
     - Choix d'un template de widget personnalisé pour l'édition en frontend
       (uniquement si « Frontend Editing » est installé).

**Fonctions**

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Option
     - Description
   * - Champ obligatoire
     - Rend le champ obligatoire.
   * - Toujours enregistrer
     - Le champ est enregistré même si sa valeur n'a pas changé. Réglé
       automatiquement lorsque « Forcer l'actualisation » est actif.

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

.. list-table::
   :header-rows: 1
   :widths: 30 70

   * - Règle de filtre
     - Remarque
   * - Recherche textuelle
     - Saisie libre pour la recherche dans la valeur combinée de la langue
       active.
   * - Requête simple
     - Filtre selon une valeur exacte ou partielle via un paramètre d'URL.
   * - Sélection simple
     - Choix d'une valeur dans une liste des entrées combinées existantes.
   * - Sélection multiple
     - Sélection multiple dans une liste des entrées combinées existantes.
   * - Registre
     - Filtre selon la première lettre de la valeur combinée.
   * - Recherche par Levenshtein
     - Recherche par similarité avec tolérance aux fautes de frappe ;
       nécessite le paquet ``attribute_levenshtein``.
   * - Loupe
     - Recherche par index plein texte ; nécessite le paquet ``filter_loupe``
       (à partir de MM 2.4).


Fonctions spéciales
---------------------

**Stockage**

Les valeurs combinées sont stockées de façon spécifique à la langue dans
``tl_metamodel_translatedtext`` (champs : ``att_id``, ``item_id``,
``langcode``, ``value`` en ``varchar(255)``). La table du MetaModel ne
reçoit pas de colonne propre.

**Combinaison dépendante de la langue**

La combinaison est calculée séparément pour chaque langue. Si des attributs
traduits sont utilisés comme champs source (par ex. « Texte traduit »), les
valeurs spécifiques à la langue de l'attribut source correspondant sont
automatiquement utilisées.

**Langue de repli**

S'il manque une valeur combinée pour une langue, MetaModels se rabat sur la
langue de repli.

**Unicité avec numérotation automatique**

Si « Valeurs uniques » est actif, MetaModels vérifie séparément pour chaque
langue si la valeur combinée existe déjà. En cas de doublon, un compteur est
ajouté automatiquement : ``Dupont, Jean (2)``, ``Dupont, Jean (3)``, etc.


.. |svg_attr_translatedcombinedvalues_22| image:: /_img/icons_svg/combinedvalues.svg
   :width: 22px
.. |img_combinedvalues| image:: /_img/icons/combinedvalues.png
.. |br| raw:: html

   <br />
