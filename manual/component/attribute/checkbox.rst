.. _component_attribute_checkbox:

|svg_attr_checkbox_22| |img_checkbox| Case à cocher (Checkbox)
===============================================================

L'attribut « Case à cocher (Checkbox) » stocke une valeur booléenne (0 ou 1).
Cas d'utilisation typiques :

* Statut de publication d'un jeu de données (actif/inactif)
* Champs Oui/Non (par ex. « Recommandation », « Afficher sur la page d'accueil »)
* Valeurs d'état binaires telles que « Disponible », « Abonné », etc.

La valeur enregistrée en base de données est ``'1'`` (actif) ou ``''`` (vide = inactif).
Dans le backend, l'attribut apparaît sous forme de widget de type case à cocher. Lorsque
l'option de publication est activée, un commutateur (« icône œil ») s'affiche en plus
dans la liste des jeux de données.

.. seealso:: Pour les MetaModels multilingues, l'attribut
   :ref:`component_attribute_translatedcheckbox` est disponible.


Installation
------------

L'attribut s'installe via le **Contao Manager** ou **Composer** :

.. code-block:: bash

   composer require metamodels/attribute_checkbox


Réglages lors de la création de l'attribut
-------------------------------------------

Outre les réglages généraux de l'attribut (nom, nom de colonne, description,
autoriser le remplacement dans les variantes), l'attribut Checkbox propose les
options spécifiques suivantes :

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Option
     - Description
   * - Icône de bascule
     - Si cette option est activée, une icône supplémentaire (« œil ») est insérée
       dans la vue en liste du backend. Le statut de publication d'un jeu de
       données peut ainsi être basculé directement d'un clic. Le nom de colonne
       habituellement utilisé pour cela est ``published``. Le filtrage effectif
       des jeux de données publiés en frontend doit être mis en place séparément
       via un jeu de filtres avec la règle de filtre « Statut checkbox ».
   * - Option d'affichage inversée
     - Inverse l'état d'affichage de l'icône : une case cochée (valeur ``1``)
       affiche alors le symbole inactif, une case décochée affiche le symbole
       actif ; utile par ex. pour un champ « Masquer » à l'instar de l'élément
       de contenu Contao.
   * - Icône personnalisée
     - Active la sélection d'icônes propres pour la vue en liste du backend. Si
       cette option est activée, deux champs supplémentaires apparaissent :

       * **Icône active** – icône affichée pour la valeur ``1`` (sélection d'un
         fichier image)
       * **Icône inactive** – icône affichée pour une valeur vide (sélection
         d'un fichier image)

       Formats pris en charge : jpg, jpeg, gif, png, tif, tiff, svg.


Réglages dans les réglages de rendu
-------------------------------------

L'attribut Checkbox ne possède pas de réglages de rendu spécifiques. Dans la liste
des attributs d'un réglage de rendu, les options habituelles sont disponibles :

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Option
     - Description
   * - Template
     - Sélection d'un template propre pour l'affichage de la valeur checkbox. Si
       aucun template n'est indiqué, l'affichage se fait sous forme de texte
       simple (``1`` si actif ou ``''`` si inactif).

       Pour l'affichage en liste dans le BE, on utilise principalement le
       template ``mm_attr_checkbox_icon``, qui affiche le statut avec des icônes
       UTF8 ☐ et ☑ (à partir de MM 2.4).
   * - Classe CSS
     - Classe CSS optionnelle ajoutée à l'élément de sortie.


Réglages dans le masque de saisie
-----------------------------------

Lorsque l'attribut Checkbox est ajouté à un masque de saisie, les options suivantes
sont disponibles :

**Présentation**

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Option
     - Description
   * - Classe backend
     - Classes CSS pour l'affichage du champ dans le formulaire du backend (par
       ex. ``w50`` pour une demi-largeur, ``cbx m12`` pour les espacements
       propres aux cases à cocher).
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
     - Rend le champ obligatoire (rarement utile pour les cases à cocher, car une
       case non cochée correspond déjà à une valeur définie).
   * - Enregistrer lors de la modification
     - Le masque de saisie est rechargé en Ajax dès que la case à cocher est
       basculée (``submitOnChange``). Les données ne sont pas encore
       enregistrées à ce moment-là.

**Aperçu (filtre backend)**

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Option
     - Description
   * - Filtrable
     - L'attribut est disponible comme critère de filtrage dans le backend.


Règles de filtre
-------------------

L'attribut Checkbox peut être utilisé avec les règles de filtre suivantes :

.. list-table::
   :header-rows: 1
   :widths: 30 70

   * - Règle de filtre
     - Remarque
   * - Statut checkbox
     - Vérifie si la valeur de la case à cocher est égale à ``1``. Généralement
       utilisée pour le contrôle de la publication. Cette règle de filtre
       propose deux options supplémentaires :

       * **Autoriser le remplacement** – un paramètre d'URL peut désactiver la
         règle de filtre (par ex. pour les liens d'aperçu).
       * **Ne pas utiliser le filtre dans l'aperçu frontend** – la règle de
         filtrage est ignorée lorsqu'un utilisateur backend utilise l'aperçu
         frontend de Contao.
   * - Requête simple
     - Filtre selon une valeur checkbox précise via un paramètre d'URL ; utile
       lorsque les visiteurs doivent pouvoir filtrer eux-mêmes entre actif et
       inactif.


Fonctions particulières
-------------------------

**Statut de publication (icône de bascule)**

Si « Icône de bascule » est activée, MetaModels enregistre une opération de bascule
dans la vue en liste du backend. Un clic sur l'icône bascule directement la valeur du
jeu de données entre ``1`` et ``''``, sans devoir ouvrir le formulaire d'édition. Le
filtrage des jeux de données publiés en frontend doit se faire via un jeu de filtres
propre avec la règle de filtre « Statut checkbox » (paquet ``filter_checkbox``).

**Mode inversé**

L'option « Option d'affichage inversée » ne modifie que l'*affichage* de l'icône —
la valeur enregistrée reste inchangée (``1`` = actif, ``''`` = inactif). Ceci est utile
lorsque la sémantique d'un champ est formulée à l'envers (par ex. « Masqué » au lieu
de « Visible ») à l'instar de l'élément de contenu Contao.

**Stockage en base de données**

La valeur est enregistrée sous la forme ``char(1) NOT NULL default ''`` :
``'1'`` signifie actif, ``''`` (chaîne vide) signifie inactif.


.. |svg_attr_checkbox_22| image:: /_img/icons_svg/checkbox.svg
   :width: 22px
.. |img_checkbox| image:: /_img/icons/checkbox.png

.. |br| raw:: html

   <br />
