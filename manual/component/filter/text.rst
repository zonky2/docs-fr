.. _component_filter_text:

|svg_filt_text_22| |img_filter_text| Filtre texte
======================================================

La règle de filtre « Filtre texte » (paquet ``filter_text``) filtre les
éléments selon une saisie de texte dans le frontend. Les visiteurs saisissent
un terme de recherche dans un champ de texte, et les éléments sont filtrés
selon les correspondances avec la valeur de l'attribut choisi. Différents modes
de recherche permettent des recherches exactes ou flexibles, y compris les
expressions régulières.

Domaines d'application typiques : recherche en texte libre dans des champs de
titre, recherche par mots-clés dans des descriptions, ou recherches combinées
avec plusieurs règles de filtre.


Installation
------------

La règle de filtre s'installe via le **Contao Manager** ou **Composer** :

.. code-block:: bash

   composer require metamodels/filter_text


Réglages lors de la création de la règle de filtre
----------------------------------------------------

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Réglage
     - Description
   * - Type
     - Sélection du type de règle de filtre – ici : « Filtre texte ».
   * - Activé
     - Active ou désactive cette règle de filtre.
   * - Commentaire
     - Champ de texte libre pour décrire l'objectif de cette règle de filtre.
   * - Attribut
     - L'attribut textuel dans lequel la recherche doit s'effectuer.


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
     - Template pour l'affichage du widget. Par défaut : ``mm_filteritem_default``.
   * - Mode de recherche
     - Détermine comment le terme de recherche est comparé à la valeur de
       l'attribut :

       * **Exact** – Le terme de recherche doit correspondre exactement à la
         valeur de l'attribut.
       * **Commence par** – La valeur de l'attribut doit commencer par le
         terme de recherche.
       * **Se termine par** – La valeur de l'attribut doit se terminer par le
         terme de recherche.
       * **N'importe quel mot** – Au moins l'un des mots séparés par le
         séparateur doit être contenu dans la valeur de l'attribut. |br|
         Option supplémentaire : **Séparateur** (par ex. espace ou virgule).
       * **Tous les mots** – Tous les mots séparés par le séparateur doivent
         être contenus dans la valeur de l'attribut. |br|
         Option supplémentaire : **Séparateur**.
       * **Expression régulière** – La valeur de l'attribut est vérifiée par
         rapport à une expression régulière. |br|
         Option supplémentaire : **Motif** (par ex. ``%s`` pour le terme de
         recherche).
   * - Texte indicatif
     - Texte indicatif affiché dans le champ de saisie lorsqu'il est vide.
   * - ID/Classe CSS
     - Définit un ID ou une classe CSS sur l'élément du widget.


Attributs compatibles
----------------------

La règle de filtre « Filtre texte » convient pour les attributs stockant des
valeurs textuelles :

* :ref:`Texte <component_attribute_text>`
* :ref:`Texte long <component_attribute_longtext>`
* :ref:`Alias <component_attribute_alias>`
* :ref:`Entrées combinées <component_attribute_combinedvalues>`
* :ref:`Token <component_attribute_token>`
* :ref:`Texte traduit <component_attribute_translatedtext>`
* :ref:`Texte long traduit <component_attribute_translatedlongtext>`


Fonctions particulières
-------------------------

**Expressions régulières**

Dans le mode de recherche « Expression régulière », un motif regex PHP peut
être indiqué. Le paramètre ``%s`` est remplacé par le terme de recherche saisi.
Exemple : ``^%s`` recherche les valeurs commençant par le terme de recherche.

**Recherche multi-mots avec séparateur**

Dans les modes « N'importe quel mot » et « Tous les mots », le terme de
recherche est décomposé en mots individuels selon le séparateur configuré,
avant que chaque mot ne soit recherché séparément.


.. |svg_filt_text_22| image:: /_img/icons_svg/filter_text.svg
   :width: 22px
.. |img_filter_text| image:: /_img/icons/filter_text.png

.. |br| raw:: html

   <br />
