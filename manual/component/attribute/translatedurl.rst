.. _component_attribute_translatedurl:

|svg_attr_translatedurl_22| |img_url| URL traduite
=====================================================

L'attribut « URL traduite » est la variante multilingue de l'attribut
:ref:`URL <component_attribute_url>`. Il stocke pour chaque langue un lien
propre composé d'un titre et d'une adresse URL. Les valeurs ne sont pas
stockées dans la table du MetaModel, mais dans la table de traduction
``tl_metamodel_translatedurl``.

Domaines d'application typiques :

* Liens dépendants de la langue vers des sites externes (par ex. page
  produit d'un fabricant en français et en anglais)
* Liens de téléchargement traduits (par ex. fiche technique FR et EN sous
  forme d'URL distinctes)
* Liens internes spécifiques à la langue vers différentes pages Contao

.. seealso:: La variante monolingue de cet attribut est décrite dans
   :ref:`component_attribute_url`.

.. seealso:: Des indications sur le multilinguisme dans MetaModels se
   trouvent sur la page :ref:`component_multi-language`.


Installation
------------

L'attribut s'installe via le **Contao Manager** ou **Composer** :

.. code-block:: bash

   composer require metamodels/attribute_translatedurl


Réglages à la création de l'attribut
-------------------------------------

Outre les réglages généraux de l'attribut, l'attribut propose l'option
spécifique suivante :

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Option
     - Description
   * - Supprimer le titre
     - Si cette option est activée, seul le champ URL est affiché et
       enregistré — le champ de titre disparaît. Utile lorsque seule l'URL
       pure est nécessaire, sans texte descriptif.


Réglages dans les réglages de rendu
--------------------------------------

L'attribut possède son propre réglage de rendu :

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Option
     - Description
   * - Ne pas ouvrir dans un nouvel onglet
     - Si cette option est active, le lien est produit **sans**
       ``target="_blank"`` — il s'ouvre alors dans la même fenêtre du
       navigateur. Par défaut (non activée) : les liens s'ouvrent dans un
       nouvel onglet.
   * - Template
     - Choix d'un template personnalisé pour l'affichage du lien.
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


Règles de filtre
-------------------

L'attribut URL traduite peut être utilisé avec les règles de filtre
suivantes :

.. list-table::
   :header-rows: 1
   :widths: 30 70

   * - Règle de filtre
     - Remarque
   * - Recherche par Levenshtein
     - Recherche par similarité avec tolérance aux fautes de frappe ;
       nécessite le paquet ``attribute_levenshtein``.
   * - Loupe
     - Recherche par index plein texte ; nécessite le paquet ``filter_loupe``
       (à partir de MM 2.4).


Fonctions spéciales
---------------------

**Stockage**

Les valeurs d'URL sont stockées de façon spécifique à la langue dans
``tl_metamodel_translatedurl``. Deux colonnes par langue sont enregistrées
pour chaque entrée : ``href`` (l'adresse URL) et ``title`` (le texte du
lien). La table du MetaModel ne reçoit pas de colonne propre.

**Liens dépendants de la langue**

Le titre et l'URL peuvent être totalement différents selon la version
linguistique. Dans le backend, un formulaire de saisie propre apparaît pour
chaque langue, avec un champ de titre et un champ URL (avec assistant
sélecteur de pages).

**Langue de repli**

S'il manque une valeur pour une langue, MetaModels se rabat sur la langue de
repli.

**Assistant de saisie**

Dans le backend, un assistant sélecteur de pages apparaît automatiquement à
côté du champ de texte, permettant de choisir des pages Contao internes.
Lorsque « Supprimer le titre » est activé, seul un simple champ de texte
est disponible.


.. |svg_attr_translatedurl_22| image:: /_img/icons_svg/url.svg
   :width: 22px
.. |img_url| image:: /_img/icons/url.png
.. |br| raw:: html

   <br />
