.. _component_filter_register:

|svg_filt_register_22| |img_filter_default| Registre
========================================================

La règle de filtre « Registre » (paquet ``filter_register``) filtre les
éléments selon la lettre initiale de la valeur d'un attribut. Elle génère une
liste de toutes les lettres initiales existantes ou possibles sous forme de
navigation cliquable (A–Z), permettant aux visiteurs de restreindre l'affichage
aux éléments commençant par une lettre donnée.

Domaines d'application typiques : navigation alphabétique dans des annuaires
professionnels, listes de personnes, glossaires ou autres sorties triées par
ordre alphabétique.

Le template fourni ``mm_filteritem_register.html5`` est prévu pour l'affichage
spécifique au registre.


Installation
------------

La règle de filtre s'installe via le **Contao Manager** ou **Composer** :

.. code-block:: bash

   composer require metamodels/filter_register


Réglages lors de la création de la règle de filtre
----------------------------------------------------

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Réglage
     - Description
   * - Type
     - Sélection du type de règle de filtre – ici : « Registre ».
   * - Activé
     - Active ou désactive cette règle de filtre.
   * - Commentaire
     - Champ de texte libre pour décrire l'objectif de cette règle de filtre.
   * - Attribut
     - L'attribut textuel selon la lettre initiale duquel le filtrage doit
       être effectué (par ex. nom de famille, nom d'entreprise).

Réglages du widget frontend
----------------------------

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Réglage
     - Description
   * - Paramètre d'URL
     - La clé du paramètre d'URL pour la lettre sélectionnée.
   * - Type d'URL pour le paramètre
     - Détermine si le paramètre est transmis sous forme de slug (URL explicite)
       ou de paramètre GET (à partir de MM 2.4) - :ref:`voir SEO
       <rst_cookbook_tips_seo_filter-url>`
   * - Libellé
     - Intitulé du widget de filtre.
   * - Masquer le libellé du widget de filtre
     - Supprime l'affichage du libellé.
   * - Template
     - Template pour l'affichage du widget. Par défaut :
       ``mm_filteritem_register``.
   * - Afficher le nombre
     - Affiche derrière chaque lettre le nombre d'éléments correspondants.
   * - Masquer les lettres vides
     - Masque les lettres pour lesquelles aucun élément n'existe.
   * - Autoriser le filtrage multiple
     - Permet de filtrer simultanément selon plusieurs lettres initiales.
   * - Uniquement les valeurs restantes
     - N'affiche que les lettres pour lesquelles des résultats subsistent
       après application des autres filtres actifs.
   * - Ignorer ce filtre pour les valeurs restantes
     - Lors du calcul des valeurs restantes, ce filtre ne renvoie pas ses
       propres options comme restriction.
   * - ID/Classe CSS
     - Définit un ID ou une classe CSS sur l'élément du widget.


Attributs compatibles
----------------------

La règle de filtre « Registre » convient pour les attributs comportant des
valeurs textuelles :

* :ref:`Texte <component_attribute_text>`
* :ref:`Alias <component_attribute_alias>`
* :ref:`Entrées combinées <component_attribute_combinedvalues>`
* :ref:`Token <component_attribute_token>`
* :ref:`Texte traduit <component_attribute_translatedtext>`


Fonctions particulières
-------------------------

**Template mm_filteritem_register**

Le template fourni affiche la liste des lettres avec des liens. Le template
peut être adapté de la manière habituelle sous Contao (héritage de template),
par ex. pour intégrer une présentation différente ou des caractères spéciaux.


.. |svg_filt_register_22| image:: /_img/icons_svg/filter_register.svg
   :width: 22px
.. |img_filter_default| image:: /_img/icons/filter_default.png

.. |br| raw:: html

   <br />
