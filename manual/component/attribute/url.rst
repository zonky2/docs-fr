.. _component_attribute_url:

|svg_attr_url_22| |img_url| URL
=================================

L'attribut « URL » stocke un lien composé d'un titre et d'une adresse URL.
Il peut aussi être configuré pour une sortie URL pure (sans titre). Domaines
d'application typiques :

* Liens externes vers des sites web, documents ou profils de réseaux sociaux
* Liens internes vers des pages Contao (via le sélecteur de pages)
* Liens de téléchargement avec un titre descriptif

Saisir les liens externes avec leur protocole (par ex.
``https://www.example.com``). Les liens internes Contao peuvent être choisis
via le sélecteur de pages intégré.

.. seealso:: Pour les MetaModels multilingues, l'attribut
   :ref:`component_attribute_translatedurl` est disponible.


Installation
------------

L'attribut s'installe via le **Contao Manager** ou **Composer** :

.. code-block:: bash

   composer require metamodels/attribute_url


Réglages à la création de l'attribut
-------------------------------------

Outre les réglages généraux de l'attribut (nom, nom de colonne, description,
autoriser la surcharge de variante), l'attribut URL propose l'option
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

L'attribut URL possède son propre réglage de rendu :

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

Lorsque l'attribut URL est ajouté à un masque de saisie, les options
suivantes sont disponibles :

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
       (disponible uniquement si l'extension « Frontend Editing » est
       installée).

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

L'attribut URL peut être utilisé avec les règles de filtre suivantes :

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

**Stockage en base de données**

Si « Supprimer le titre » est désactivé, la paire ``[Titre, URL]`` est
stockée comme tableau sérialisé dans un champ ``blob NULL``. Si « Supprimer
le titre » est activé, seule l'URL est stockée comme simple chaîne de
caractères.

**Assistant de saisie**

Dans le backend, un assistant sélecteur de pages apparaît automatiquement à
côté du champ de texte, permettant de choisir des pages Contao internes.
Lorsque « Supprimer le titre » est activé, seul un simple champ de texte
est disponible.


.. |svg_attr_url_22| image:: /_img/icons_svg/url.svg
   :width: 22px
.. |img_url| image:: /_img/icons/url.png
.. |br| raw:: html

   <br />
