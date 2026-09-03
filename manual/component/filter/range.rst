.. _component_filter_range:

|svg_filt_range_22| |img_filter_range| Valeur de/à pour deux champs
========================================================================

La règle de filtre « Valeur de/à pour deux champs » (paquet ``filter_range``)
filtre les éléments selon une plage de valeurs définie par deux attributs
distincts. Le premier attribut représente la valeur de départ (« de »), le
second attribut la valeur finale (« à »). Un élément est inclus dans le
résultat si une valeur de recherche donnée se situe dans la plage définie par
les deux valeurs d'attributs.

Domaines d'application typiques : périodes de validité (« Valide de » /
« Valide à »), fourchettes de prix avec des champs distincts pour le prix
minimum et maximum, ou périodes d'événements.

.. seealso:: Pour la comparaison d'un seul attribut avec une plage saisie par
   le visiteur, la règle de filtre :ref:`component_filter_fromto` est
   disponible. |br|
   Pour deux champs date, la règle de filtre
   :ref:`component_filter_range-date` est disponible.


Installation
------------

La règle de filtre s'installe via le **Contao Manager** ou **Composer** :

.. code-block:: bash

   composer require metamodels/filter_range


Réglages lors de la création de la règle de filtre
----------------------------------------------------

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Réglage
     - Description
   * - Type
     - Sélection du type de règle de filtre – ici : « Valeur de/à pour deux
       champs ».
   * - Activé
     - Active ou désactive cette règle de filtre.
   * - Commentaire
     - Champ de texte libre pour décrire l'objectif de cette règle de filtre.
   * - Attribut (de)
     - Le premier attribut, contenant la valeur de départ de la plage.
   * - Attribut 2 (à)
     - Le second attribut, contenant la valeur finale de la plage.


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
     - Texte indicatif affiché dans les champs de saisie.
   * - Type de plage de filtre
     - Détermine comment la plage recherchée est comparée aux valeurs des
       attributs :

       * **s1** – La valeur recherchée se situe entièrement dans la plage de
         l'attribut
       * **s2** – La valeur recherchée chevauche la plage de l'attribut
       * **s3** – La valeur recherchée commence dans la plage de l'attribut
       * **s4** – La valeur recherchée se termine dans la plage de l'attribut
         (par défaut)
       * **s5** – La valeur recherchée contient entièrement la plage de
         l'attribut
   * - Supérieur ou égal (≥)
     - La valeur de recherche « de » est comparée de façon incluse (``>=``).
   * - Inférieur ou égal (≤)
     - La valeur de recherche « à » est comparée de façon incluse (``<=``).
   * - Afficher le champ « de »
     - Active l'affichage du champ de saisie « de » dans le widget.
   * - Afficher le champ « à »
     - Active l'affichage du champ de saisie « à » dans le widget.
   * - ID/Classe CSS
     - Définit un ID ou une classe CSS sur l'élément du widget.


Attributs compatibles
----------------------

La règle de filtre « Valeur de/à pour deux champs » convient pour les
attributs comportant des valeurs numériques :

* :ref:`Numérique <component_attribute_numeric>`
* :ref:`Décimal <component_attribute_decimal>`


.. |svg_filt_range_22| image:: /_img/icons_svg/filter_range.svg
   :width: 22px
.. |img_filter_range| image:: /_img/icons/filter_range.png

.. |br| raw:: html

   <br />
