.. _component_data-in-attributes:

Créer des types de données comme attributs
============================================

Lors de la planification de la structure de son MetaModels, outre la construction de la
:ref:`structure de base de données <component_relations_database_structure>`, il est important
de savoir avec quelles possibilités on peut enregistrer ses données réelles telles que des textes,
des nombres, des dates, des codes postaux, etc. Il faut ici tenir compte à la fois des types de
données de la base de données (MySQL/MariaDB) et des possibilités de saisie via les widgets de
Contao.

Voici un aperçu des attributs permettant de stocker les données souhaitées. De plus, la colonne
« Règle de filtre » indique quelles :ref:`règles de filtre pour le filtrage/la recherche
<component_filter>` peuvent être utilisées en frontend. Il est également indiqué quels attributs
sont disponibles pour l':ref:`édition en frontend (FEE) <rst_extended_frontend_editing>` (✔) - le
cas échéant, :ref:`d'autres dépôts doivent être installés <rst_extended_frontend_editing_installation>` (🗹).

Textes
------

.. csv-table::
   :header: "Type de données", "Attribut", "Nom du paquet", "Règle de filtre", "FEE", "Remarque"
   :widths: 10, 10, 10, 10, 10, 10

    "Textes courts", ":ref:`Texte <component_attribute_text>`", `attribute_text <https://github.com/MetaModels/attribute_text>`_, "Recherche textuelle, |br| Sélection simple, |br| Sélection multiple, |br| Requête simple, |br| Registre, |br| Levenshtein, |br| Loupe", "✔", "jusqu'à 255 caractères ; |br| nombre d'attributs limité |br| par la BD"
    "Textes longs", ":ref:`Texte long <component_attribute_longtext>`", `attribute_longtext <https://github.com/MetaModels/attribute_longtext>`_, "Recherche textuelle, |br| Levenshtein, |br| Loupe", "✔", "jusqu'à 65535 caractères ; |br| :ref:`personnalisable <rst_cookbook_inputmask_manipulate-select-values>`; |br| :ref:`Utilisation de fichier <rst_extended_file-usage>` ✔"
    "Texte comme alias", ":ref:`Alias <component_attribute_alias>`", `attribute_alias <https://github.com/MetaModels/attribute_alias>`_, "Recherche textuelle, |br| Requête simple, |br| Levenshtein, |br| Loupe", "✔", "jusqu'à 255 caractères ; |br| génération à partir d'un |br| ou plusieurs attributs"
    "Valeurs combinées", ":ref:`Entrées combinées <component_attribute_combinedvalues>`", `attribute_combinedvalues <https://github.com/MetaModels/attribute_combinedvalues>`_, "Recherche textuelle, |br| Sélection simple, |br| Sélection multiple, |br| Requête simple, |br| Registre, |br| Levenshtein, |br| Loupe", "✔", "jusqu'à 255 caractères ; |br| chaîne de résultat définissable via ``sprintf``"
    "Texte comme tableau", ":ref:`Tableau de texte <component_attribute_tabletext>`", `attribute_tabletext <https://github.com/MetaModels/attribute_tabletext>`_, "Levenshtein, |br| Loupe", ":ref:`🗹 <rst_extended_frontend_editing_installation>`", "jusqu'à 255 caractères par cellule"
    "Texte comme URL", ":ref:`URL <component_attribute_url>`", `attribute_url <https://github.com/MetaModels/attribute_url>`_, "Levenshtein, |br| Loupe", ":ref:`🗹 <rst_extended_frontend_editing_installation>`", "jusqu'à 255 caractères ; |br| nombre de caractères pour le titre et l'URL"
    "Texte comme token", ":ref:`Token <component_attribute_token>`", `attribute_token <https://github.com/MetaModels/attribute_token>`_, "Recherche textuelle, |br| Sélection simple, |br| Sélection multiple, |br| Requête simple, |br| Registre, |br| Levenshtein, |br| Loupe", "✔", "jusqu'à 255 caractères ; |br| nombre de caractères incluant un préfixe optionnel"
    "*Multilingue*"
    "Textes courts multilingues", ":ref:`Texte traduit <component_attribute_translatedtext>`", `attribute_translatedtext <https://github.com/MetaModels/attribute_translatedtext>`_, "voir Texte", "✔", "jusqu'à 255 caractères"
    "Textes longs multilingues", ":ref:`Texte long traduit <component_attribute_translatedlongtext>`", `attribute_translatedlongtext <https://github.com/MetaModels/attribute_translatedlongtext>`_, "voir Texte long", "✔", "voir Texte long ; |br| :ref:`Utilisation de fichier <rst_extended_file-usage>` ✔"
    "Texte comme alias multilingue", ":ref:`Alias traduit <component_attribute_translatedalias>`", `attribute_translatedalias <https://github.com/MetaModels/attribute_translatedalias>`_, "voir Alias", "✔", "voir Alias"
    "Valeurs combinées |br| multilingues", ":ref:`Entrées combinées traduites <component_attribute_translatedcombinedvalues>`", `attribute_translatedcombinedvalues <https://github.com/MetaModels/attribute_translatedcombinedvalues>`_, "voir |br| Entrées combinées", "✔", "voir Entrées combinées"
    "Texte comme |br| tableau multilingue", ":ref:`Tableau de texte traduit <component_attribute_translatedtabletext>`", `attribute_translatedtabletext <https://github.com/MetaModels/attribute_translatedtabletext>`_, "Levenshtein, |br| Loupe", ":ref:`🗹 <rst_extended_frontend_editing_installation>`", "voir Tableau de texte"
    "Texte comme |br| URL multilingue", ":ref:`URL traduite <component_attribute_translatedurl>`", `attribute_translateurl <https://github.com/MetaModels/attribute_translateurl>`_, "Levenshtein, |br| Loupe", ":ref:`🗹 <rst_extended_frontend_editing_installation>`", "voir URL"

Nombres
-------

.. csv-table::
   :header: "Type de données", "Attribut", "Nom du paquet", "Règle de filtre", "FEE", "Remarque"
   :widths: 10, 10, 10, 10, 10, 10

    "Valeurs entières", ":ref:`Numérique <component_attribute_numeric>`", `attribute_numeric <https://github.com/MetaModels/attribute_numeric>`_, "Valeur de/à pour un attribut, |br| Valeur de/à pour deux attributs", "✔", "pour les codes postaux ou numéros de téléphone, utiliser l'attribut |br| Texte"
    "Nombres décimaux", ":ref:`Décimal <component_attribute_decimal>`", `attribute_decimal <https://github.com/MetaModels/attribute_decimal>`_, "Valeur de/à pour un attribut, |br| Valeur de/à pour deux attributs", "✔", "saisie avec le point comme séparateur décimal"
    "Date ou heure", ":ref:`Date <component_attribute_timestamp>`", `attribute_timestamp <https://github.com/MetaModels/attribute_timestamp>`_, "Valeur de/à pour un attribut de date, |br| Valeur de/à pour deux attributs de date", "✔", "stockage sous forme d'horodatage UNIX ; |br| la saisie peut être limitée à la date |br| seule ou à l'heure seule"
    "Coordonnées géographiques (combinées)", ":ref:`LatLong <component_attribute_latlong>`", `attribute_latlong <https://github.com/MetaModels/attribute_latlong>`_, "Recherche par périmètre", "**—**", "stockage en tant que ``POINT`` natif ; |br| index spatial optionnel pour une recherche |br| par périmètre plus rapide ; saisie au choix |br| via une recherche d'adresse avec carte"
    "Coordonnées géographiques (séparées)", "voir Décimal", , "Recherche par périmètre", "**—**", "créer un attribut respectivement |br| pour la latitude et la longitude"

Fichiers
--------

.. csv-table::
   :header: "Type de données", "Attribut", "Nom du paquet", "Règle de filtre", "FEE", "Remarque"
   :widths: 10, 10, 10, 10, 10, 10

    "Fichier", ":ref:`Fichier <component_attribute_file>`", `attribute_file <https://github.com/MetaModels/attribute_file>`_, , "✔ Upload", "consultable dans le BE par nom de fichier ou UUID ; |br| pour la sortie d':ref:`images, la taille de l'image <rst_cookbook_templates_fe_work_with_images>` est sélectionnable ; |br| :ref:`Utilisation de fichier <rst_extended_file-usage>` ✔"
    "*Multilingue*"
    "Fichier multilingue", ":ref:`Fichier traduit <component_attribute_translatedfile>`", `attribute_translatedfile <https://github.com/MetaModels/attribute_translatedfile>`_, , "✔ Upload", "voir Fichier ; |br| :ref:`Utilisation de fichier <rst_extended_file-usage>` ✔"

Transmission par ex. à un :ref:`Rocksilid-Slider <rst_cookbook_templates_fe_template_ce_elements_rstslider>`.

Valeur booléenne
----------------

.. csv-table::
   :header: "Type de données", "Attribut", "Nom du paquet", "Règle de filtre", "FEE", "Remarque"
   :widths: 10, 10, 10, 10, 10, 10

    "Valeur booléenne", ":ref:`Case à cocher <component_attribute_checkbox>`", `attribute_checkbox <https://github.com/MetaModels/attribute_checkbox>`_, "État de la case à cocher", "✔", "affichage possible dans la liste du BE sous forme d'icône bascule"
    "*Multilingue*"
    "Valeur booléenne multilingue", ":ref:`Case à cocher traduite <component_attribute_translatedcheckbox>`", `attribute_translatedcheckbox <https://github.com/MetaModels/attribute_translatedcheckbox>`_, "État de la case à cocher traduite", "✔", "voir Case à cocher"


Relations
---------

.. csv-table::
   :header: "Type de données", "Attribut", "Nom du paquet", "Règle de filtre", "FEE", "Remarque"
   :widths: 10, 10, 10, 10, 10, 10

    "1:n", ":ref:`Sélection simple [select] <component_attribute_select>`", `attribute_select <https://github.com/MetaModels/attribute_select>`_, "Sélection simple, |br| Filtre sur un attribut du Model avec une relation", "✔", "relation vers une autre table pour une valeur |br| tables MM ou autres tables Contao"
    "m:n", ":ref:`Sélection multiple [tags] <component_attribute_tags>`", `attribute_tags <https://github.com/MetaModels/attribute_tags>`_, "Sélection multiple, |br| Filtre sur un attribut du Model avec une relation", "✔", "relation vers une autre table pour plusieurs valeurs |br| tables MM ou autres tables Contao"
    "*Multilingue* |br| la sélection simple et multiple peuvent |br| gérer nativement les MM multilingues"
    "1:n", ":ref:`Sélection simple traduite [select] <component_attribute_translatedselect>`", `attribute_translatedselect <https://github.com/MetaModels/attribute_translatedselect>`_, "Sélection simple", "✔", "uniquement pour des cas particuliers avec une colonne propre pour la clé de langue"
    "m:n", ":ref:`Sélection multiple traduite [tags] <component_attribute_translatedtags>`", `attribute_translatedtags <https://github.com/MetaModels/attribute_translatedtags>`_, "Sélection multiple", "✔", "uniquement pour des cas particuliers avec une colonne propre pour la clé de langue"

De plus amples informations se trouvent sur la page :ref:`component_relations`.

Autres données
--------------

.. csv-table::
   :header: "Type de données", "Attribut", "Nom du paquet", "Règle de filtre", "FEE", "Remarque"
   :widths: 10, 10, 10, 10, 10, 10

    "Valeur de couleur", ":ref:`Sélecteur de couleur <component_attribute_color>`", `attribute_color <https://github.com/MetaModels/attribute_color>`_, , ":ref:`🗹 <rst_extended_frontend_editing_installation>`", "opacité/transparence également sélectionnable ; |br| tri par couleur possible ; |br| :ref:`voir attribut Color <rst_extended_attribute_color>`"
    "Éléments de contenu", ":ref:`Contenu d'un article <component_attribute_contentarticle>`", `attribute_contentarticle <https://github.com/MetaModels/attribute_contentarticle>`_, , "**—**", "plusieurs éléments de contenu comme dans l'article ; |br| :ref:`Utilisation de fichier <rst_extended_file-usage>` ✔"
    "Noms de pays", ":ref:`Pays <component_attribute_country>`", `attribute_country <https://github.com/MetaModels/attribute_country>`_, , "✔", "pays possibles limitables"
    "Codes de langue", ":ref:`Clé de langue <component_attribute_langcode>`", `attribute_langcode <https://github.com/MetaModels/attribute_langcode>`_, , "✔", "langues possibles limitables"
    "Distance géographique", ":ref:`Distance géographique <component_attribute_geodistance>`", `attribute_geodistance <https://github.com/MetaModels/attribute_geodistance>`_, , "**—**", "indication supplémentaire pour le tri |br| de la recherche par périmètre"
    "Évaluation par étoiles", ":ref:`Évaluation <component_attribute_rating>`", `attribute_rating <https://github.com/MetaModels/attribute_rating>`_, , "**—**", "nombre d'étoiles sélectionnable"
    "Tableau MCW", ":ref:`Tableau multi (MCW) <component_attribute_tablemulti>`", `attribute_tablemulti <https://github.com/MetaModels/attribute_tablemulti>`_, , ":ref:`🗹 <rst_extended_frontend_editing_installation>`", ":ref:`voir attribut pour Multi-Column-Wizard <rst_extended_attribute_mcw>`; |br| :ref:`Utilisation de fichier <rst_extended_file-usage>` ✔"
    "Pin pour Cowegis-Map", "Cowegis-Marker", `cowegis-layer <https://github.com/MetaModels/cowegis-layer>`_, , "✔", ":ref:`voir intégration Cowegis-Layer pour marqueur <extended_cowegis-layer-marker>`"
    "*Multilingue*"
    "Éléments de contenu |br| multilingues", ":ref:`Contenu traduit d'un article <component_attribute_translatedcontentarticle>`", `attribute_translatedcontentarticle <https://github.com/MetaModels/attribute_translatedcontentarticle>`_, , "**—**", "voir Contenu d'un article ; |br| :ref:`Utilisation de fichier <rst_extended_file-usage>` ✔"
    "Tableau MCW |br| multilingue", ":ref:`Tableau multi (MCW) traduit <component_attribute_translatedtablemulti>`", `attribute_translatedtablemulti <https://github.com/MetaModels/attribute_translatedtablemulti>`_, , ":ref:`🗹 <rst_extended_frontend_editing_installation>`", "voir Tableau multi (MCW) ; |br| :ref:`Utilisation de fichier <rst_extended_file-usage>` ✔"

Sortie par ex. comme :ref:`CE-YouTube <rst_cookbook_templates_fe_template_ce_elements_youtube>`.

.. |br| raw:: html

   <br />
