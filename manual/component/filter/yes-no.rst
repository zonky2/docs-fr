.. _component_filter_yes-no:

|svg_filt_yes_no_22| |img_filter_checkbox| Oui / Non
=========================================================

La règle de filtre « Oui / Non » (paquet ``filter_checkbox``) affiche un widget
frontend permettant aux visiteurs de choisir entre deux états : « Oui »
(valeur ``1``) ou « Non » (valeur ``0`` ou vide). Selon le mode, le widget
apparaît sous forme de case à cocher, de deux cases à cocher distinctes
(Oui/Non) ou de boutons radio.

La règle de filtre filtre les éléments selon la valeur choisie d'un attribut de
type case à cocher et convient pour des sélections explicites Oui/Non dans le
widget de filtre frontend.

.. note:: Dans le menu de sélection du backend pour le type de règle de
   filtre, cette règle est affichée sous le nom « Oui / Non ». Elle est
   techniquement identique à la règle de filtre :ref:`État de la case à cocher
   <component_filter_checkbox>`, mais est configurée avec le mode « Boutons
   radio » ou « Case à cocher Oui/Non ».


Installation
------------

La règle de filtre s'installe via le **Contao Manager** ou **Composer** :

.. code-block:: bash

   composer require metamodels/filter_checkbox


Réglages lors de la création de la règle de filtre
----------------------------------------------------

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Réglage
     - Description
   * - Type
     - Sélection du type de règle de filtre – ici : « Oui / Non ».
   * - Activé
     - Active ou désactive cette règle de filtre.
   * - Commentaire
     - Champ de texte libre pour décrire l'objectif de cette règle de filtre.
   * - Attribut
     - L'attribut de type case à cocher selon la valeur duquel le filtrage
       doit être effectué.


Réglages du widget frontend
----------------------------

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Réglage
     - Description
   * - Paramètre d'URL
     - La clé du paramètre d'URL utilisée pour transmettre la valeur du filtre.
       Si elle n'est pas précisée, le nom de colonne de l'attribut est utilisé.
       Avec ``auto_item``, seule la valeur – sans clé – est intégrée dans l'URL.
   * - Type d'URL pour le paramètre
     - Détermine si le paramètre est transmis sous forme de slug (URL explicite)
       ou de paramètre GET (à partir de MM 2.4) - :ref:`voir SEO
       <rst_cookbook_tips_seo_filter-url>`
   * - Paramètre statique
     - Si cette option est active, la valeur du filtre est obtenue à partir
       d'une liste de sélection dans l'élément de contenu/module plutôt que de
       l'URL.
   * - Libellé
     - Intitulé du widget de filtre.
   * - Masquer le libellé du widget de filtre
     - Supprime l'affichage du libellé.
   * - Template
     - Template pour l'affichage du widget. Par défaut :
       ``mm_filteritem_default`` ; pour un affichage spécifique aux cases à
       cocher : ``mm_filteritem_checkbox``.
   * - Mode
     - Choisit le mode d'affichage du widget :

       * **Case à cocher Oui** – Case à cocher unique ; filtre sur ``1`` si
         cochée
       * **Case à cocher Non** – Case à cocher unique ; filtre sur ``0``/vide
         si cochée
       * **Boutons radio** – Deux boutons radio (Oui/Non) ; l'option
         « Permettre une sélection vide » apparaît en plus pour une option
         « Tous »
   * - « Oui/Non » au lieu du nom de l'attribut
     - Affiche « Oui » et « Non » comme désignations d'option à la place du
       nom de l'attribut.
   * - Permettre une sélection vide
     - (uniquement en mode « Boutons radio ») Ajoute une option vide
       (« Tous ») permettant de désactiver la règle de filtre.
   * - Désignation de l'option comme paramètre
     - La valeur du paramètre d'URL est le texte de l'option (« Oui »/« Non »)
       au lieu d'un nombre.
   * - ID/Classe CSS
     - Définit un ID ou une classe CSS sur l'élément du widget.


Attributs compatibles
----------------------

La règle de filtre « Oui / Non » convient exclusivement pour les attributs
suivants :

* :ref:`Case à cocher <component_attribute_checkbox>`
* :ref:`Case à cocher traduite <component_attribute_translatedcheckbox>`


.. |svg_filt_yes_no_22| image:: /_img/icons_svg/filter_yes-no.svg
   :width: 22px
.. |img_filter_checkbox| image:: /_img/icons/filter_checkbox.png

.. |br| raw:: html

   <br />
