.. _component_filter_fromto:

|svg_filt_fromto_22| |img_filter_fromto| Valeur de/à pour un champ
======================================================================

La règle de filtre « Valeur de/à pour un champ » (paquet ``filter_fromto``)
filtre les éléments selon une plage de valeurs portant sur un seul attribut
numérique ou textuel. Les visiteurs peuvent saisir dans le frontend une valeur
« de », une valeur « à », ou les deux. La règle de filtre renvoie tous les
éléments dont la valeur d'attribut se situe dans la plage indiquée.

Domaines d'application typiques : filtre de prix (prix de X à Y), indications
de taille ou d'âge, ou filtres numériques généraux par plage.

.. seealso:: Pour la comparaison via deux attributs distincts (par ex.
   « Valide de » et « Valide à »), la règle de filtre
   :ref:`component_filter_range` est disponible. |br|
   Pour les valeurs de date, la règle de filtre
   :ref:`component_filter_fromto-date` est disponible.


Installation
------------

La règle de filtre s'installe via le **Contao Manager** ou **Composer** :

.. code-block:: bash

   composer require metamodels/filter_fromto


Réglages lors de la création de la règle de filtre
----------------------------------------------------

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Réglage
     - Description
   * - Type
     - Sélection du type de règle de filtre – ici : « Valeur de/à pour un
       champ ».
   * - Activé
     - Active ou désactive cette règle de filtre.
   * - Commentaire
     - Champ de texte libre pour décrire l'objectif de cette règle de filtre.
   * - Attribut
     - L'attribut selon la valeur duquel le filtrage doit être effectué (par
       ex. prix, âge).


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
     - Intitulé du widget de filtre.
   * - Masquer le libellé du widget de filtre
     - Supprime l'affichage du libellé.
   * - Template
     - Template pour l'affichage du widget. Par défaut : ``mm_filteritem_default``.
   * - Texte indicatif
     - Texte indicatif affiché dans les champs de saisie tant qu'ils sont
       vides.
   * - Supérieur ou égal (≥)
     - Si cette option est active, la valeur « de » est considérée comme
       incluse (``>=``). Sinon exclusive (``>``).
   * - Inférieur ou égal (≤)
     - Si cette option est active, la valeur « à » est considérée comme
       incluse (``<=``). Sinon exclusive (``<``).
   * - Afficher le champ « de »
     - Active l'affichage du champ de saisie « de » dans le widget.
   * - Afficher le champ « à »
     - Active l'affichage du champ de saisie « à » dans le widget.
   * - ID/Classe CSS
     - Définit un ID ou une classe CSS sur l'élément du widget.


Attributs compatibles
----------------------

La règle de filtre « Valeur de/à pour un champ » convient pour les attributs
comportant des valeurs numériques ou comparables :

* :ref:`Numérique <component_attribute_numeric>`
* :ref:`Décimal <component_attribute_decimal>`


.. |svg_filt_fromto_22| image:: /_img/icons_svg/filter_fromto.svg
   :width: 22px
.. |img_filter_fromto| image:: /_img/icons/filter_fromto.png

.. |br| raw:: html

   <br />
