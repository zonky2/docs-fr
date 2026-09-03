.. _rst_cookbook_filter_filter-with-static-parameter:

Restreindre les items dans le CE/module FE Liste MM et MM-Filter
======================================================================

La sortie d'une liste MM peut être contrôlée via un filtre - par exemple si l'on a une liste d'employés qui doit
être affichée filtrée par département.

On crée donc un filtre pour « Département xy » et on le sélectionne dans les réglages du CE/module FE Liste MM.

Mais si l'on souhaite afficher un département spécifique sur plusieurs pages, il devient assez fastidieux et peu
pratique de créer un filtre séparé pour chaque département.

On peut éviter cela si la :ref:`règle de filtre « Recherche simple » <component_filter_simplelookup>` est
intégrée pour l'attribut « Département » et que l'on y coche la case « Paramètre statique ».

Une fois cela fait, un champ de sélection supplémentaire apparaît dans les réglages de filtrage du CE/module FE
Liste MM. Celui-ci liste, dans notre exemple, tous les départements et permet de sélectionner un département à
afficher.

|img_static-parameter.png|

Dans la sélection « Valeur de filtre pour l'attribut * », outre les valeurs de l'attribut, les réglages « - » pour
une chaîne vide et « - sans valeur [null] - » pour la valeur en base ``NULL`` sont également disponibles.

.. note:: Si la chaîne vide est sélectionnée, seuls les items pour lesquels la valeur de l'attribut est une chaîne
   vide sont affichés - si aucune affectation n'existe, la valeur en base est typiquement ``NULL``.

Il est également possible d'utiliser plusieurs règles « Recherche simple », par ex. si l'on peut sélectionner deux
départements, ou un département ainsi qu'une autre catégorisation.

Comme alternative, on peut également mettre à disposition des rédacteurs un
:ref:`élément de contenu prédéfini correspondant <rst_cookbook_specials_ce_element_for_editors>`.

.. note:: À partir de la version 2.4, ce réglage est également possible pour MM-Filter.

L'élément de contenu ainsi que le module FE MM-Filter peuvent désormais, comme Liste MM, être dotés d'un préréglage.
Si une règle de filtre « Recherche simple » avec l'option « Paramètre statique » est définie, les options de
sélection pour « Écraser les réglages de filtrage » apparaissent également ici et restreignent les autres valeurs
de filtre en conséquence, dans la mesure où l'option « Uniquement les valeurs restantes » a été définie pour
celles-ci.



.. |img_static-parameter.png| image:: /_img/screenshots/cookbook/filter/static-parameter.png


