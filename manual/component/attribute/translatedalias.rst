.. _component_attribute_translatedalias:

|svg_attr_translatedalias_22| |img_alias| Alias traduit
=========================================================

L'attribut « Alias traduit » est la variante multilingue de
l'attribut :ref:`Alias <component_attribute_alias>`. Il génère pour chaque
langue son propre identifiant court adapté aux URL (slug). Les valeurs ne
sont pas stockées dans la table du MetaModel, mais dans la table de
traduction ``tl_metamodel_translatedtext``.

Domaines d'application typiques :

* Paramètres d'URL multilingues pour le filtrage (par ex.
  ``/produits/mon-produit`` en français, ``/products/my-product`` en anglais)
* Identifiants lisibles et stables pour les liens directs ou les
  :ref:`URL optimisées SEO <rst_cookbook_tips_seo_url>`
* Identifiants uniques générés automatiquement à partir de noms ou de titres

.. seealso:: La variante monolingue de cet attribut est décrite dans
   :ref:`component_attribute_alias`.

.. note:: Un alias n'est pas automatiquement unique. Pour garantir
   l'unicité, l'option « Valeurs uniques » doit être activée dans les
   réglages généraux de l'attribut.

.. warning:: Si l'option « Forcer la régénération de l'alias » est activée,
   les valeurs d'alias existantes sont régénérées à chaque modification des
   attributs source. Cela peut invalider des URL déjà publiées.

.. seealso:: Des indications sur le multilinguisme dans MetaModels se
   trouvent sur la page :ref:`component_multi-language`.


Installation
------------

L'attribut s'installe via le **Contao Manager** ou **Composer** :

.. code-block:: bash

   composer require metamodels/attribute_translatedalias


Réglages à la création de l'attribut
-------------------------------------

Outre les réglages généraux de l'attribut, l'attribut propose les options
spécifiques suivantes :

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Option
     - Description
   * - Champs pour l'alias
     - Choix d'un ou plusieurs attributs à partir desquels l'alias est formé.
       Outre les attributs MetaModels propres, les métachamps système (ID,
       PID, tri, etc.) sont également disponibles.
   * - Forcer la régénération de l'alias
     - Si la case est cochée, l'alias est automatiquement régénéré à chaque
       modification de l'un des attributs source. Le champ est alors affiché
       en lecture seule dans le backend.
   * - Caractères valides pour l'alias
     - Jeu de caractères pour la génération automatique : *chiffres et
       minuscules Unicode* (par défaut), *chiffres et lettres Unicode*,
       *chiffres et minuscules ASCII*, *chiffres et lettres ASCII*.
   * - Pas de préfixe entier
     - Si la case est cochée (par défaut), aucun préfixe ``id-`` n'est ajouté
       lorsque l'alias résultant est purement numérique.
   * - Préfixe et suffixe de l'alias
     - Préfixe et suffixe optionnels ajoutés respectivement avant et après
       l'alias. Contrairement à l'alias monolingue, un préfixe/suffixe
       propre peut être défini pour chaque langue (assistant multi-colonnes
       avec choix de la langue, champ de préfixe et champ de suffixe).

.. note:: L'option « Langue de conversion » de l'alias monolingue disparaît
   ici — la langue MetaModels active est utilisée automatiquement.


Réglages dans les réglages de rendu
--------------------------------------

L'attribut ne possède pas de réglages de rendu qui lui soient propres. Dans
la liste des attributs d'un réglage de rendu, les options habituelles
(template, classe CSS) sont disponibles.


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
     - Classes CSS pour la présentation (par ex. ``w50``, ``long``).
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
     - Réglé automatiquement lorsque « Forcer la régénération de l'alias »
       est actif.

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

Mêmes règles de filtre que pour l'attribut :ref:`Alias monolingue
<component_attribute_alias>` : requête simple, recherche textuelle,
Levenshtein, Loupe.


Fonctions spéciales
---------------------

**Stockage**

Les valeurs d'alias sont stockées de façon spécifique à la langue dans
``tl_metamodel_translatedtext`` (champs : ``att_id``, ``item_id``,
``langcode``, ``value`` en ``varchar(255)``). La table du MetaModel ne
reçoit pas de colonne propre.

**Préfixe/suffixe dépendant de la langue**

Contrairement à l'alias monolingue, chaque version linguistique peut se voir
attribuer son propre préfixe ou suffixe (par ex. ``fr-`` pour la variante
d'URL française, ``en-`` pour la variante anglaise).

**Unicité avec suffixe**

Lorsque l'unicité est activée, MetaModels vérifie séparément pour chaque
langue et ajoute automatiquement un compteur en cas de doublon
(``mon-produit-2``, etc.).


.. |svg_attr_translatedalias_22| image:: /_img/icons_svg/alias.svg
   :width: 22px
.. |img_alias| image:: /_img/icons/alias.png
.. |br| raw:: html

   <br />
