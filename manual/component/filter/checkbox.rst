.. _component_filter_checkbox:

|svg_filt_checkbox_22| |img_filter_checkbox| État de la case à cocher
=======================================================================

La règle de filtre « État de la case à cocher » (paquet ``filter_checkbox``)
vérifie si la valeur d'un attribut de type case à cocher est égale à ``1``
(actif). Elle est typiquement utilisée pour le contrôle de la publication :
seuls les éléments dont la case à cocher est activée (par ex. ``published = 1``)
sont affichés dans le frontend.

En règle générale, cette règle de filtre agit sans widget frontend, mais elle
peut également être configurée de manière à ce que les visiteurs puissent
choisir eux-mêmes l'état de la case à cocher via un widget frontend.

.. seealso:: Pour les MetaModels multilingues, la règle de filtre
   :ref:`component_filter_translated-checkbox` est disponible.


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
     - Sélection du type de règle de filtre – ici : « État de la case à cocher »
       (ou « Oui / Non » dans le menu de sélection du backend).
   * - Activé
     - Active ou désactive cette règle de filtre.
   * - Commentaire
     - Champ de texte libre pour décrire l'objectif de cette règle de filtre.
   * - Attribut
     - L'attribut de type case à cocher dont la valeur doit être vérifiée.


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
   * - Libellé
     - Intitulé du widget de filtre dans le frontend.
   * - Masquer le libellé du widget de filtre
     - Supprime l'affichage du libellé dans le frontend.
   * - Template
     - Template pour l'affichage du widget de filtre. Par défaut :
       ``mm_filteritem_default`` ; pour un affichage spécifique aux cases à
       cocher : ``mm_filteritem_checkbox``.
   * - Mode
     - Détermine si la règle de filtre est configurée comme case à cocher Oui,
       case à cocher Non ou boutons radio (sélection Oui/Non) :

       * **Case à cocher Oui** – Filtre sur ``1`` (actif)
       * **Case à cocher Non** – Filtre sur ``0`` ou vide (inactif)
       * **Boutons radio** – Affiche des boutons radio Oui/Non ; l'option
         supplémentaire « Permettre une sélection vide » (``blankoption``)
         apparaît
   * - « Oui/Non » au lieu du nom de l'attribut
     - Affiche « Oui/Non » à la place du nom de l'attribut dans le widget.
   * - Désignation de l'option comme paramètre
     - La valeur du paramètre d'URL est la désignation de l'option (texte) au
       lieu d'un nombre.
   * - ID/Classe CSS
     - Définit un ID ou une classe CSS sur l'élément du widget de filtre.


Attributs compatibles
----------------------

La règle de filtre « État de la case à cocher » convient exclusivement aux
attributs suivants :

* :ref:`Case à cocher <component_attribute_checkbox>`


Fonctions particulières
-------------------------

**Contrôle de la publication**

Le cas d'usage le plus fréquent est l'utilisation de cette règle de filtre comme
« filtre de publication » : un attribut de type case à cocher (nom de colonne
habituel : ``published``) dont l'option « icône à bascule » est activée dans le
backend permet d'activer/désactiver rapidement des éléments. Dans le frontend,
la règle de filtre « État de la case à cocher » exclut les éléments inactifs.

**Template mm_filteritem_checkbox**

Le template fourni ``mm_filteritem_checkbox.html5`` propose un affichage
spécifique aux cases à cocher pour le widget de filtre.


.. |svg_filt_checkbox_22| image:: /_img/icons_svg/filter_checkbox.svg
   :width: 22px
.. |img_filter_checkbox| image:: /_img/icons/filter_checkbox.png

.. |br| raw:: html

   <br />
