.. _rst_extended_attribute_color:

Attribut Color
==============

L'attribut "`Color <https://github.com/MetaModels/attribute_color>`_"
met à disposition un champ de saisie pour un code couleur hexadécimal ainsi
qu'un champ de saisie pour l'opacité. Le champ de saisie du code couleur
dispose en plus d'un sélecteur de couleur. L'opacité est saisie sous forme
de pourcentage - par ex. "50" pour 50 pour cent.

|img_input_mask|

L'installation se fait via le gestionnaire de paquets de Contao. Pour cela,
saisissez "metamodels/attribute_color" dans le champ de recherche et installez
l'attribut.

Après l'installation réussie, l'entrée "Sélecteur de couleur" est disponible
lors du choix du type d'attribut. Aucun autre réglage n'est nécessaire pour
cet attribut.

Les deux valeurs - couleur et opacité - sont restituées dans les templates
texte et HTML5 sous forme de valeurs texte, par ex. "fafa05 50".

|img_output_text|

Avec un accès au nœud [raw], les deux valeurs sont accessibles sous forme de
tableau (array) de l'attribut avec la clé 0 pour la couleur et 1 pour
l'opacité. Ces valeurs permettent par exemple d'influencer un style CSS en
ligne. Dans la capture d'écran de la liste, le template a été adapté en
conséquence et un "motif en damier" a été inséré en arrière-plan via CSS pour
mieux visualiser l'opacité.

|img_output_css-color|

Les enregistrements peuvent être triés en fonction de la couleur et de
l'opacité. Un tri décroissant va du code couleur #FFFFFF (blanc) au
#000000 (noir) ainsi que de l'opacité 100 % à 0 %. Viennent ensuite tous les
enregistrements sans couleur assignée.

.. |img_input_mask| image:: /_img/screenshots/extended/attribute_color/input_mask.png
.. |img_output_text| image:: /_img/screenshots/extended/attribute_color/output_text.png
.. |img_output_css-color| image:: /_img/screenshots/extended/attribute_color/output_css-color.png


