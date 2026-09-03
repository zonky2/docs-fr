.. _component_filter_range-date:

|svg_filt_range_date_22| |img_filter_range| Valeur de/à pour deux champs date
=================================================================================

La règle de filtre « Valeur de/à pour deux champs date » (paquet
``filter_range``) filtre les éléments selon une plage de dates définie par deux
attributs de type date distincts. Le premier attribut de date contient le point
de départ (« de »), le second le point final (« à »). Un élément est inclus
dans le résultat si une date de recherche donnée se situe dans la période
définie par les deux valeurs d'attributs.

Domaines d'application typiques : périodes d'événements, périodes de
réservation, périodes de validité avec des attributs de date distincts.

Un template dédié ``mm_filteritem_datepicker.html5`` est disponible pour une
saisie de date via le navigateur. Pour le champ de saisie HTML5 ``date``, la
date doit être transmise au format ``YYYY-MM-DD`` –
`plus d'informations <https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/input/date>`_.

.. seealso:: Pour les comparaisons numériques à deux champs, la règle de
   filtre :ref:`component_filter_range` est disponible.


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
       champs date ».
   * - Activé
     - Active ou désactive cette règle de filtre.
   * - Commentaire
     - Champ de texte libre pour décrire l'objectif de cette règle de filtre.
   * - Attribut (de)
     - Le premier attribut de date, contenant le point de départ.
   * - Attribut 2 (à)
     - Le second attribut de date, contenant le point final.


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
   * - Format de date
     - Le format dans lequel la date est attendue (par ex. ``d.m.Y`` ou
       ``Y-m-d``).
   * - Type horaire
     - Détermine si la date (``date``), la date et l'heure (``datim``) ou
       l'heure (``time``) sont comparées.
   * - Libellé
     - Intitulé du widget de filtre.
   * - Masquer le libellé du widget de filtre
     - Supprime l'affichage du libellé.
   * - Template
     - Template pour l'affichage du widget. Pour un sélecteur de date :
       ``mm_filteritem_datepicker``.
   * - Texte indicatif
     - Texte indicatif dans les champs de saisie.
   * - Type de plage de filtre
     - Détermine comment la plage de dates recherchée est comparée aux
       valeurs des attributs (s1–s5, par analogie avec la règle de filtre
       :ref:`component_filter_range`).
   * - Supérieur ou égal (≥)
     - La date de recherche « de » est comparée de façon incluse (``>=``).
   * - Inférieur ou égal (≤)
     - La date de recherche « à » est comparée de façon incluse (``<=``).
   * - Afficher le champ « de »
     - Active l'affichage du champ de date « de » dans le widget.
   * - Afficher le champ « à »
     - Active l'affichage du champ de date « à » dans le widget.
   * - ID/Classe CSS
     - Définit un ID ou une classe CSS sur l'élément du widget.


Attributs compatibles
----------------------

La règle de filtre « Valeur de/à pour deux champs date » convient pour
l'attribut :ref:`Date <component_attribute_timestamp>` – si le filtrage doit
porter uniquement sur des dates, il convient de régler l'option « Gestion de la
date et de l'heure » sur « Enregistrer uniquement la date sans l'heure ».


.. |svg_filt_range_date_22| image:: /_img/icons_svg/filter_rangedate.svg
   :width: 22px
.. |img_filter_range| image:: /_img/icons/filter_range.png

.. |br| raw:: html

   <br />
