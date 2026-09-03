.. _component_attribute_translatedfile:

|svg_attr_translatedfile_22| |img_file| Fichier traduit
=========================================================

L'attribut « Fichier traduit » est la variante multilingue de l'attribut
:ref:`Fichier <component_attribute_file>`. Il propose pour chaque langue son
propre sélecteur de fichiers permettant de choisir des fichiers dans le
répertoire de fichiers de Contao. Les valeurs ne sont pas stockées dans la
table du MetaModel, mais dans la table de traduction
``tl_metamodel_translatedlongblob``.

Domaines d'application typiques :

* Images de produits spécifiques à la langue (par ex. une photo de produit
  FR avec un texte imprimé en français, une photo de produit EN avec un
  texte imprimé en anglais)
* Différents PDF selon la langue (par ex. fiches techniques françaises et
  anglaises)
* Contenus multimédias dépendants de la langue tels que vidéos ou fichiers
  audio

.. seealso:: La variante monolingue de cet attribut est décrite dans
   :ref:`component_attribute_file`.

.. seealso:: Cet attribut est pris en charge par l'intégration
   :ref:`File-Usage <rst_extended_file-usage>`. Elle permet d'afficher dans
   la gestion des fichiers de Contao si et où un fichier est utilisé.

.. seealso:: Pour le téléversement de fichiers en frontend, l'extension
   :ref:`rst_extended_frontend_editing` est disponible.

.. seealso:: Des indications sur le multilinguisme dans MetaModels se
   trouvent sur la page :ref:`component_multi-language`.


Installation
------------

L'attribut s'installe via le **Contao Manager** ou **Composer** :

.. code-block:: bash

   composer require metamodels/attribute_translatedfile


Réglages à la création de l'attribut
-------------------------------------

Outre les réglages généraux de l'attribut, l'attribut Fichier propose les
options spécifiques suivantes :

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Option
     - Description
   * - Sélection multiple
     - Autorise la sélection de plusieurs fichiers. Si cette option n'est
       pas activée, un seul fichier peut être sélectionné.
   * - Indiquer un dossier racine
     - Restreint le sélecteur de fichiers à un dossier de départ donné dans
       le répertoire de fichiers.
   * - Types de fichiers valides
     - Liste des extensions de fichiers autorisées, séparées par des
       virgules (par ex. ``jpg,jpeg,png,gif``).
   * - Types de fichiers autorisés
     - Restriction de la sélection aux fichiers, aux dossiers ou aux deux.


Réglages dans les réglages de rendu
--------------------------------------

L'attribut possède ses propres réglages de rendu pour l'affichage :

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Option
     - Description
   * - Utiliser comme champ image avec vignette
     - Active l'affichage d'image avec génération de vignette. Cette option
       **doit** être activée pour tout affichage direct d'image dans le
       backend ou le frontend.
   * - Largeur et hauteur de l'image
     - Dimensions de la vignette générée (largeur × hauteur).
   * - Créer un lien comme téléchargement ou lightbox
     - Intègre le fichier dans un lien servant soit au téléchargement, soit
       à l'agrandissement dans une lightbox.
   * - Téléchargement protégé
     - L'URL de téléchargement n'est valide que temporairement (URL signée
       à durée limitée).
   * - Trier par
     - Détermine l'ordre de tri pour les fichiers multiples : nom croissant/
       décroissant, date croissante/décroissante ou aléatoire.
   * - Image comme espace réservé
     - Choix d'une image d'espace réservé affichée lorsqu'aucun fichier
       n'est sélectionné.


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
     - Classes CSS pour la présentation du champ dans le formulaire backend.
   * - Template pour le backend
     - Choix d'un template de widget personnalisé pour le formulaire backend.
   * - Template pour le frontend
     - Choix d'un template de widget personnalisé pour l'édition en frontend
       (uniquement si « Frontend Editing » est installé).
   * - Mode du widget
     - Détermine le mode d'affichage du widget de fichier. Modes disponibles :

       * **Normal** – sélecteur de fichiers standard
       * **Téléchargements** – affichage sous forme de liste de
         téléchargement
       * **Galerie** – affichage sous forme de galerie d'images
       * **FE téléversement simple** – téléversement frontend pour un seul
         fichier
       * **FE téléversement simple avec aperçu** – téléversement frontend
         avec vignette d'aperçu
       * **FE téléversement multiple** – téléversement frontend pour
         plusieurs fichiers
       * **FE téléversement multiple avec aperçu** – téléversement frontend
         avec vignettes d'aperçu

**Réglages de téléversement** (uniquement pour les modes d'édition frontend)

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Option
     - Description
   * - Dossier de destination
     - Dossier du répertoire de fichiers dans lequel les fichiers
       téléversés sont enregistrés.
   * - Utiliser le répertoire personnel
     - Enregistre le fichier dans le répertoire personnel du membre connecté.
   * - Étendre le dossier
     - Étend dynamiquement le chemin du dossier de destination via des
       insert-tags ou des tokens ``##post_*##``.
   * - Normaliser le dossier étendu
     - Normalise le chemin du dossier étendu avec le générateur d'alias.
   * - Normaliser les noms de fichiers
     - Normalise le nom de fichier lors du téléversement avec le générateur
       d'alias.
   * - Préfixe / suffixe de nom de fichier
     - Ajoute un texte fixe ou dynamique avant ou après le nom de fichier.
   * - Conserver les fichiers existants
     - Ajoute un suffixe numérique en cas de noms de fichiers en double, au
       lieu d'écraser le fichier.
   * - Désélectionner le fichier
     - Permet à l'utilisateur de retirer un fichier de l'enregistrement.
   * - Supprimer le fichier
     - Permet à l'utilisateur de retirer un fichier et de le supprimer du
       répertoire de fichiers.
   * - Trier par
     - Détermine l'ordre de tri des fichiers multiples téléversés.
   * - Largeur et hauteur des vignettes
     - Taille des vignettes affichées dans le widget de téléversement.

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
     - L'attribut est disponible dans le backend comme critère de filtrage.
   * - Utilisable pour la recherche
     - L'attribut est disponible dans le backend comme champ de recherche.


Règles de filtre
-------------------

Pour l'attribut Fichier traduit, aucune règle de filtre frontend propre
n'est actuellement disponible. Dans le backend, une recherche par nom de
fichier ou UUID est possible.


Fonctions spéciales
---------------------

**Stockage**

Les références de fichiers sont stockées de façon spécifique à la langue
dans ``tl_metamodel_translatedlongblob`` (champs : ``att_id``, ``item_id``,
``langcode``, ``value`` en ``blob``). La table du MetaModel ne reçoit pas de
colonne propre. L'ordre défini manuellement pour plusieurs fichiers est
contenu dans la valeur elle-même.

.. note:: Jusqu'à MetaModels 2.4, le champ ``value_sorting`` de la même
   table contenait l'ordre de tri. Contao ayant supprimé l'option de widget
   correspondante ``orderField`` avec la version 5.0, ce champ disparaît
   avec MetaModels 2.5 — une migration transfère l'ordre existant dans la
   valeur puis supprime le champ. Voir :ref:`new_in_mm250`.

**Fichiers dépendants de la langue**

Chaque version linguistique peut référencer un fichier totalement différent.
Dans le backend, le widget de fichier apparaît pour chaque langue avec la
valeur spécifique à la langue.

**Langue de repli**

S'il manque un fichier pour une langue, MetaModels se rabat sur la langue de
repli.

**Tri des fichiers multiples**

L'ordre de plusieurs fichiers peut être configuré indépendamment dans les
réglages de rendu (pour l'affichage) et dans les réglages du masque de
saisie (pour le téléversement en frontend).

Indépendamment de cela, l'ordre peut être défini **manuellement par
glisser-déposer, par langue**, dans le masque de saisie : dans les modes de
widget *Galerie* et *Téléchargements*, les fichiers sélectionnés sont
triables lorsque la *Sélection multiple* est active. Un bouton rouge se
trouve en outre sur les vignettes, permettant de retirer un fichier de la
sélection sans ouvrir le sélecteur de fichiers.


.. |svg_attr_translatedfile_22| image:: /_img/icons_svg/file.svg
   :width: 22px
.. |img_file| image:: /_img/icons/file.png
.. |br| raw:: html

   <br />
