.. _component_filter_fromto-date:

|svg_filt_fromto_date_22| |img_filter_fromto| Valeur de/à pour un champ date
================================================================================

La règle de filtre « Valeur de/à pour un champ date » (paquet ``filter_fromto``)
filtre les éléments selon une plage de dates portant sur un seul attribut de
type date. Les visiteurs peuvent saisir dans le frontend une date « de », une
date « à », ou les deux. La règle de filtre compare les valeurs de date
stockées sous forme de timestamp UNIX avec la plage indiquée.

Domaines d'application typiques : filtres de dates (événements de la date X à
la date Y), périodes de validité, ou filtres généraux par plage de dates.

Un template dédié ``mm_filteritem_datepicker.html5`` est disponible pour une
saisie de date via le navigateur. Pour le champ de saisie HTML5 ``date``, la
date doit être transmise au format ``YYYY-MM-DD`` –
`plus d'informations <https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/input/date>`_.

.. seealso:: Pour la comparaison via deux attributs de date distincts, la
   règle de filtre :ref:`component_filter_range-date` est disponible. |br|
   Pour les valeurs numériques, la règle de filtre
   :ref:`component_filter_fromto` est disponible.

.. seealso:: Pour un sélecteur de date moderne dans le frontend :
   :ref:`rst_cookbook_templates_flatpickr-integration`


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
       champ date ».
   * - Activé
     - Active ou désactive cette règle de filtre.
   * - Commentaire
     - Champ de texte libre pour décrire l'objectif de cette règle de filtre.
   * - Attribut
     - L'attribut de type date selon la valeur duquel le filtrage doit être
       effectué.


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
     - Le format dans lequel la date est attendue dans le champ de saisie
       frontend (par ex. ``d.m.Y`` ou ``Y-m-d``). Par défaut : le format de
       date Contao issu des réglages système.
   * - Type horaire
     - Détermine si seule la date (``date``), la date et l'heure (``datim``)
       ou uniquement l'heure (``time``) sont comparées.
   * - Libellé
     - Intitulé du widget de filtre.
   * - Masquer le libellé du widget de filtre
     - Supprime l'affichage du libellé.
   * - Template
     - Template pour l'affichage du widget. Par défaut :
       ``mm_filteritem_default`` ; pour une saisie avec sélecteur de date :
       ``mm_filteritem_datepicker``.
   * - Texte indicatif
     - Texte indicatif affiché dans les champs de saisie.
   * - Supérieur ou égal (≥)
     - Si cette option est active, la date « de » est considérée comme
       incluse (``>=``).
   * - Inférieur ou égal (≤)
     - Si cette option est active, la date « à » est considérée comme
       incluse (``<=``).
   * - Afficher le champ « de »
     - Active l'affichage du champ de date « de » dans le widget.
   * - Afficher le champ « à »
     - Active l'affichage du champ de date « à » dans le widget.
   * - ID/Classe CSS
     - Définit un ID ou une classe CSS sur l'élément du widget.


Attributs compatibles
----------------------

La règle de filtre « Valeur de/à pour un champ date » convient pour l'attribut
:ref:`Date <component_attribute_timestamp>` – si le filtrage doit porter
uniquement sur des dates, il convient de régler l'option « Gestion de la date
et de l'heure » sur « Enregistrer uniquement la date sans l'heure ».


.. |svg_filt_fromto_date_22| image:: /_img/icons_svg/filter_fromto_date.svg
   :width: 22px
.. |img_filter_fromto| image:: /_img/icons/filter_fromto.png

.. |br| raw:: html

   <br />
