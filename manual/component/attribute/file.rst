.. _component_attribute_file:

|svg_attr_file_22| |img_file| Fichier
=====================================

L'attribut « Fichier » met à disposition un sélecteur de fichiers permettant de
choisir un ou plusieurs fichiers dans le répertoire de fichiers de Contao. Cas
d'utilisation typiques :

* Images pour des produits, des personnes ou des articles (image unique ou galerie)
* Fichiers à télécharger tels que des PDF, documents ou archives
* Vidéos, fichiers audio ou autres fichiers multimédias

L'attribut prend en charge différents modes de widget selon les cas d'usage dans le
backend et le frontend. Pour l'affichage d'images, l'option « Utiliser comme champ
image avec image miniature » doit être activée dans les réglages de rendu.

.. seealso:: Pour les MetaModels multilingues, l'attribut
   :ref:`component_attribute_translatedfile` est disponible.

.. seealso:: Cet attribut est pris en charge par l'intégration
   :ref:`File-Usage <rst_extended_file-usage>`. Elle permet d'afficher dans la
   gestion des fichiers de Contao si et où un fichier est utilisé.

.. seealso:: Pour le téléversement de fichiers en frontend, l'extension
   :ref:`rst_extended_frontend_editing` est disponible.


Installation
------------

L'attribut s'installe via le **Contao Manager** ou **Composer** :

.. code-block:: bash

   composer require metamodels/attribute_file


Réglages lors de la création de l'attribut
-------------------------------------------

Outre les réglages généraux de l'attribut (nom, nom de colonne, description,
autoriser le remplacement dans les variantes), l'attribut Fichier propose les
options spécifiques suivantes :

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Option
     - Description
   * - Sélection multiple
     - Autorise la sélection de plusieurs fichiers. Si cette option n'est pas
       activée, un seul fichier peut être sélectionné.
   * - Indiquer un dossier racine
     - Restreint le sélecteur de fichiers à un dossier de départ déterminé dans
       le répertoire de fichiers. Si aucun dossier n'est choisi, le sélecteur
       démarre à la racine.
   * - Types de fichiers valides
     - Liste d'extensions autorisées séparées par des virgules (par ex.
       ``jpg,jpeg,png,gif``), permettant de remplacer le réglage par défaut de
       Contao.
   * - Types de fichiers autorisés
     - Restriction de la sélection aux fichiers, aux dossiers ou aux deux
       (par défaut : aucune restriction).


Réglages dans les réglages de rendu
-------------------------------------

L'attribut Fichier possède ses propres réglages de rendu :

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Option
     - Description
   * - Utiliser comme champ image avec image miniature
     - Active l'affichage sous forme d'image avec génération d'une miniature.
       Sans cette option, seul le chemin du fichier est affiché. Cette option
       **doit** être activée pour tout affichage direct d'image dans le
       backend ou le frontend.
   * - Largeur et hauteur de l'image
     - Dimensions de la miniature générée (largeur × hauteur). Si un seul des
       deux champs est renseigné, la mise à l'échelle est proportionnelle. En
       laissant les deux champs vides, l'image est affichée dans sa taille
       d'origine.
   * - Créer un lien en téléchargement ou lightbox
     - Intègre le fichier dans un lien servant soit au téléchargement, soit à
       l'affichage agrandi dans une lightbox.
   * - Téléchargement protégé
     - L'URL de téléchargement n'est valable que temporairement (URL signée à
       durée limitée).
   * - Trier par
     - Détermine l'ordre de tri pour les fichiers multiples : nom croissant/
       décroissant, date croissante/décroissante ou aléatoire.
   * - Image comme espace réservé
     - Sélectionne une image d'espace réservé affichée lorsqu'aucun fichier
       n'est sélectionné.


Réglages dans le masque de saisie
-----------------------------------

Lorsque l'attribut Fichier est ajouté à un masque de saisie, les options suivantes
sont disponibles :

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
       (disponible uniquement si l'extension « Frontend Editing » est installée).
   * - Mode du widget
     - Détermine le mode d'affichage du widget de fichier. Modes disponibles :

       * **Normal** – sélecteur de fichiers standard
       * **Téléchargements** – affichage sous forme de liste de téléchargements
       * **Galerie** – affichage sous forme de galerie d'images
       * **Téléversement FE unique** – téléversement en frontend d'un seul
         fichier
       * **Téléversement FE unique avec aperçu** – téléversement en frontend
         avec image miniature
       * **Téléversement FE multiple** – téléversement en frontend de
         plusieurs fichiers
       * **Téléversement FE multiple avec aperçu** – téléversement en frontend
         avec images miniatures

**Réglages de téléversement** (uniquement pour les modes d'édition en frontend)

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Option
     - Description
   * - Dossier cible
     - Dossier du répertoire de fichiers dans lequel les fichiers téléversés
       sont enregistrés.
   * - Utiliser le répertoire personnel
     - Enregistre le fichier dans le répertoire personnel du membre connecté.
   * - Étendre le dossier
     - Étend dynamiquement le chemin du dossier cible via des insert-tags ou
       des jetons ``##post_*##``.
   * - Normaliser le dossier étendu
     - Normalise le chemin du dossier étendu avec le générateur d'alias.
   * - Normaliser le nom de fichier
     - Normalise le nom de fichier lors du téléversement avec le générateur
       d'alias.
   * - Préfixe / suffixe du nom de fichier
     - Ajoute un texte fixe ou dynamique avant ou après le nom de fichier.
   * - Conserver les fichiers existants
     - Ajoute un suffixe numérique en cas de noms de fichiers identiques, au
       lieu d'écraser le fichier.
   * - Désélectionner le fichier
     - Permet à l'utilisateur de retirer un fichier du jeu de données (sans le
       supprimer).
   * - Supprimer le fichier
     - Permet à l'utilisateur de retirer un fichier tout en le supprimant du
       répertoire de fichiers.
   * - Trier par
     - Détermine l'ordre de tri des fichiers multiples téléversés.
   * - Largeur et hauteur des miniatures
     - Taille des images miniatures affichées dans le widget de téléversement.

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
     - L'attribut est disponible comme critère de filtrage dans le backend
       (recherche par nom de fichier ou UUID).
   * - Cherchable
     - L'attribut est disponible comme champ de recherche dans le backend.


Règles de filtre
-------------------

Aucune règle de filtre propre au frontend n'est actuellement disponible pour
l'attribut Fichier. Dans le backend, une recherche par nom de fichier ou par UUID
est possible.


Fonctions particulières
-------------------------

**Stockage en base de données**

Les fichiers individuels sont enregistrés sous forme d'UUID binaire. Plusieurs
fichiers sont stockés sous forme de tableau sérialisé d'UUID dans un champ
``blob NULL``. L'ordre défini manuellement est intégré dans la valeur elle-même.

.. note:: Jusqu'à MetaModels 2.4, lorsque l'option *Sélection multiple* était
   activée, la colonne ``<nom_colonne>__sort`` était en plus créée pour l'ordre de
   tri. Contao ayant supprimé l'option de widget ``orderField`` correspondante en
   version 5.0, cette colonne disparaît avec MetaModels 2.5 - une migration
   transfère l'ordre existant dans la valeur puis supprime la colonne. Voir
   :ref:`new_in_mm250`.

**Tri des fichiers multiples**

L'ordre de plusieurs fichiers peut être configuré indépendamment aussi bien dans
les réglages de rendu (pour l'affichage) que dans les réglages du masque de
saisie (pour le téléversement en frontend).

Indépendamment de cela, l'ordre peut être défini **manuellement par glisser-
déposer** dans le masque de saisie : dans les modes de widget *Galerie* et
*Téléchargements*, les fichiers sélectionnés sont triables lorsque la *sélection
multiple* est active. Un bouton rouge est en outre présent sur les images
miniatures, permettant de retirer un fichier de la sélection sans devoir ouvrir
le sélecteur de fichiers.


.. |svg_attr_file_22| image:: /_img/icons_svg/file.svg
   :width: 22px
.. |img_file| image:: /_img/icons/file.png

.. |br| raw:: html

   <br />
