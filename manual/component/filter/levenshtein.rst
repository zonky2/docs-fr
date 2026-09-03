.. _component_filter_levenshtein:

|svg_filt_levenshtein_22| |img_filter_default| Recherche assistée par Levenshtein
=====================================================================================

La règle de filtre « Recherche assistée par Levenshtein » (paquet
``attribute_levenshtein``) crée un index de texte intégral sur des attributs
sélectionnés et permet une recherche en texte intégral basée sur la similarité,
avec autocomplétion. La recherche repose sur l'algorithme de distance de
Levenshtein, qui trouve également les fautes de frappe et les termes à
consonance proche.

L'installation de l'attribut :ref:`Levenshtein <component_attribute_levenshtein>`
est un prérequis ; celui-ci construit l'index de recherche dans une table
dédiée. Le template fourni ``mm_filteritem_levenshtein.html5`` contient la
logique JavaScript nécessaire à l'autocomplétion.

.. seealso:: Documentation détaillée sur l'attribut Levenshtein :
   :ref:`component_attribute_levenshtein`


Installation
------------

La règle de filtre s'installe via le **Contao Manager** ou **Composer** :

.. code-block:: bash

   composer require metamodels/attribute_levenshtein


Réglages lors de la création de la règle de filtre
----------------------------------------------------

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Réglage
     - Description
   * - Type
     - Sélection du type de règle de filtre – ici : « Recherche assistée par
       Levenshtein ».
   * - Activé
     - Active ou désactive cette règle de filtre.
   * - Commentaire
     - Champ de texte libre pour décrire l'objectif de cette règle de filtre.
   * - Attribut
     - L'attribut Levenshtein qui fournit l'index de recherche.


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
     - Intitulé du champ de recherche.
   * - Masquer le libellé du widget de filtre
     - Supprime l'affichage du libellé.
   * - Template
     - Template pour l'affichage du widget. Par défaut :
       ``mm_filteritem_levenshtein`` (contient le JavaScript pour
       l'autocomplétion).
   * - Texte indicatif
     - Texte indicatif dans le champ de recherche.
   * - ID/Classe CSS
     - Définit un ID ou une classe CSS sur l'élément du widget.
   * - Activer l'autocomplétion
     - Active l'autocomplétion basée sur JavaScript pendant la saisie. Par
       défaut : active.
   * - Nombre minimal de caractères pour l'autocomplétion
     - Nombre de caractères à partir duquel l'autocomplétion se déclenche. Par
       défaut : 3.
   * - Soumettre automatiquement
     - Le formulaire de recherche est soumis automatiquement lorsqu'une
       suggestion d'autocomplétion est sélectionnée.


Attributs compatibles
----------------------

La règle de filtre « Recherche assistée par Levenshtein » fonctionne
exclusivement avec l'attribut Levenshtein spécial :

* :ref:`Levenshtein <component_attribute_levenshtein>`

L'attribut Levenshtein peut lui-même indexer plusieurs autres attributs (texte,
texte long, alias, etc.).


.. |svg_filt_levenshtein_22| image:: /_img/icons_svg/filter_levenshtein.svg
   :width: 22px
.. |img_filter_default| image:: /_img/icons/filter_default.png

.. |br| raw:: html

   <br />
