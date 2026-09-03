.. _component_filter_loupe:

|svg_filt_loupe_22| |img_filter_default| Loupe
==================================================

La règle de filtre « Loupe » (paquet ``filter_loupe``, à partir de MM 2.4) crée
un index de texte intégral sur des attributs sélectionnés dans une base de
données SQLite dédiée et permet une recherche en texte intégral performante
avec recherche par similarité (recherche floue). L'implémentation repose sur la
bibliothèque PHP `Loupe <https://github.com/loupe-php/loupe>`_.

Contrairement à la :ref:`recherche Levenshtein <component_filter_levenshtein>`,
Loupe utilise une base de données SQLite autonome pour l'index et propose des
possibilités de configuration étendues pour la distance floue et le classement.

.. seealso:: Documentation détaillée sur Loupe : :ref:`rst_extended_loupe`


Installation
------------

La règle de filtre s'installe via le **Contao Manager** ou **Composer** :

.. code-block:: bash

   composer require metamodels/filter_loupe


Réglages lors de la création de la règle de filtre
----------------------------------------------------

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Réglage
     - Description
   * - Type
     - Sélection du type de règle de filtre – ici : « Loupe ».
   * - Activé
     - Active ou désactive cette règle de filtre.
   * - Commentaire
     - Champ de texte libre pour décrire l'objectif de cette règle de filtre.
   * - Attributs à indexer
     - Sélection des attributs (assistant de cases à cocher) à inclure dans
       l'index de recherche Loupe. Champ obligatoire.
   * - Distance floue
     - Tableau MCW qui définit, pour différentes longueurs de mot (nombre
       minimal de caractères), la distance de Levenshtein autorisée (distance
       floue, 0–10). |br|
       Par défaut : longueur de mot 5 → distance 1 ; longueur de mot 9 →
       distance 2.
   * - Classement équipondéré
     - Si cette option est active, tous les résultats sont classés de façon
       équivalente, indépendamment de leur pertinence (pas de classement par
       pertinence).
   * - Utiliser les valeurs formatées
     - Si cette option est active, ce sont les valeurs de sortie formatées des
       attributs qui sont indexées (au lieu des valeurs brutes de la base de
       données).


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
   * - Ignorer ce filtre pour les valeurs restantes
     - Lors du calcul des valeurs restantes, ce filtre ne renvoie pas ses
       propres options comme restriction.
   * - ID/Classe CSS
     - Définit un ID ou une classe CSS sur l'élément du widget.


Attributs compatibles
----------------------

La règle de filtre « Loupe » peut indexer les types d'attributs suivants :

* :ref:`Texte <component_attribute_text>`
* :ref:`Texte long <component_attribute_longtext>`
* :ref:`Alias <component_attribute_alias>`
* :ref:`Entrées combinées <component_attribute_combinedvalues>`
* :ref:`Token <component_attribute_token>`
* :ref:`Texte traduit <component_attribute_translatedtext>`
* :ref:`Texte long traduit <component_attribute_translatedlongtext>`


Fonctions particulières
-------------------------

**Reconstruire l'index**

Dans la liste des règles de filtre, un symbole d'opération supplémentaire
(icône Loupe) apparaît pour les règles de filtre Loupe, permettant de
reconstruire manuellement l'index de recherche SQLite. L'index est en outre mis
à jour automatiquement lors des modifications apportées aux éléments indexés.

**Base de données SQLite**

L'index Loupe est stocké dans un fichier SQLite autonome (pas dans la base de
données Contao principale). Cela permet des recherches en texte intégral
rapides, même avec de grands volumes de données.


.. |svg_filt_loupe_22| image:: /_img/icons_svg/loupe-emblem.svg
   :width: 22px
.. |img_filter_default| image:: /_img/icons/filter_default.png

.. |br| raw:: html

   <br />
