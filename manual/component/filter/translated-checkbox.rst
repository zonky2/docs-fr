.. _component_filter_translated-checkbox:

|svg_filt_translated_checkbox_22| |img_filter_checkbox| État de la case à cocher traduite
==============================================================================================

La règle de filtre « État de la case à cocher traduite » (paquet
``filter_checkbox``) vérifie si la valeur d'un attribut de case à cocher traduit
est égale à ``1`` (actif). Elle correspond dans sa fonction à la règle de
filtre :ref:`component_filter_checkbox`, mais est prévue pour être utilisée
avec le type d'attribut :ref:`Case à cocher traduite
<component_attribute_translatedcheckbox>` dans les MetaModels multilingues.

L'état de la case à cocher traduite est évalué en fonction de la langue : dans
la langue active, la valeur de la case à cocher traduite est vérifiée. Cela
permet de piloter les états de publication par langue.

.. seealso:: Pour les MetaModels monolingues, la règle de filtre
   :ref:`component_filter_checkbox` est disponible.


Installation
------------

La règle de filtre s'installe via le **Contao Manager** ou **Composer** :

.. code-block:: bash

   composer require metamodels/filter_checkbox


Réglages lors de la création de la règle de filtre
----------------------------------------------------

Les réglages correspondent entièrement à ceux de la règle de filtre
:ref:`component_filter_checkbox`. Seul le type d'attribut doit être une
:ref:`component_attribute_translatedcheckbox`.

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Réglage
     - Description
   * - Type
     - Sélection du type de règle de filtre – ici : « État de la case à cocher
       traduite ».
   * - Activé
     - Active ou désactive cette règle de filtre.
   * - Commentaire
     - Champ de texte libre pour décrire l'objectif de cette règle de filtre.
   * - Attribut
     - L'attribut de case à cocher traduit dont la valeur doit être vérifiée.
   * - Paramètre d'URL
     - La clé du paramètre d'URL utilisée pour transmettre la valeur du filtre.
       Si elle n'est pas précisée, le nom de colonne de l'attribut est utilisé.
       Avec ``auto_item``, seule la valeur – sans clé – est intégrée dans l'URL.
   * - Type d'URL pour le paramètre
     - Détermine si le paramètre est transmis sous forme de slug (URL explicite)
       ou de paramètre GET (à partir de MM 2.4) - :ref:`voir SEO
       <rst_cookbook_tips_seo_filter-url>`

Réglages du widget frontend
----------------------------

Identiques aux réglages de la règle de filtre :ref:`component_filter_checkbox`
– les mêmes options (paramètre d'URL, mode, template, etc.) sont disponibles.


Attributs compatibles
----------------------

La règle de filtre « État de la case à cocher traduite » convient
exclusivement pour l'attribut suivant :

* :ref:`Case à cocher traduite <component_attribute_translatedcheckbox>`


.. |svg_filt_translated_checkbox_22| image:: /_img/icons_svg/filter_checkbox.svg
   :width: 22px
.. |img_filter_checkbox| image:: /_img/icons/filter_checkbox.png

.. |br| raw:: html

   <br />
