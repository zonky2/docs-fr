.. _extended_perimetersearch:

Recherche par rayon
====================


Introduction
------------

La recherche par rayon permet de filtrer les enregistrements selon leur position
géographique par rapport à une adresse donnée et un rayon. Le filtre détermine si
l'enregistrement correspondant se trouve dans le rayon indiqué, c'est-à-dire si la
distance géographique entre le point de saisie du filtre et celui de l'enregistrement
est inférieure à un seuil donné. Le point de référence ("centre") du "cercle de filtre"
est l'adresse saisie dans le filtre. La distance sphérique entre les deux points est
déterminée à l'aide de la `formule de Haversine <https://en.wikipedia.org/wiki/Haversine_formula>`_.

Le calcul de la distance des enregistrements par rapport à l'adresse saisie se fait sur la
base de la longitude et de la latitude. Ces deux valeurs doivent être disponibles aussi bien
pour l'adresse enregistrée dans le MetaModel que pour l'adresse saisie.

Pour les adresses enregistrées dans le MetaModel, il faut créer respectivement un attribut
pour la longitude et un pour la latitude, par ex. "geo_lat" et "geo_long" avec le type
"Décimal" ou "Texte".

La résolution de l'adresse saisie en longitude et latitude se fait directement lors de
l'envoi de la requête de filtre en frontend via un "lookup" - pour cela, les services de
Google-Maps ou d'OpenStreetMap sont disponibles.

Voici un guide rapide de configuration de la recherche par rayon.


Installer le filtre
--------------------

Installer le paquet "metamodels/filter_perimetersearch" via le Contao Manager ou en
console. Après l'installation, une règle de filtre supplémentaire "Recherche par rayon"
devrait être disponible.


Créer les attributs
--------------------

Pour la longitude (longitude) et la latitude (latitude), il faut créer respectivement un
attribut de type "Décimal" ou "Texte", par ex. "geo_lat" et "geo_long". Les attributs ne
sont nécessaires que pour le filtrage et n'ont pas besoin d'être configurés pour la
sortie en frontend.

|img_attribute_01|

Après avoir créé les deux attributs, ceux-ci peuvent être remplis avec des valeurs, par
ex. geo_lat : 52.517365 et geo_long : 13.353159 pour l'adresse du château de Bellevue à
Berlin (Spreeweg 1, 10557 Berlin, Allemagne).


Créer le filtre
----------------

Sous les ensembles de filtres, un nouvel ensemble de filtres est créé, par ex. avec le nom
"Recherche par rayon", puis une règle de filtre du type "Recherche par rayon" avec les
réglages suivants :

* Type : Recherche par rayon
* Mode de données : Mode multiple (actuellement seul le mode multiple est disponible)
* Attributs pour latitude et longitude : sélectionner les attributs correspondants
* Label : nom pour la saisie de l'adresse ("centre") - par ex. "Adresse"
* Label de plage : nom pour l'indication de la taille du rayon - par ex. "Rayon en km"
* Mode de plage : choix entre champ de saisie libre ou valeurs fixes (mode de sélection) - pour
  une liste de valeurs fixes, la valeur par défaut peut être prédéfinie
* Mode pays : définit si et, le cas échéant, quel pays doit être ajouté à l'adresse pour la
  recherche lookup (par ex. valeur par défaut "Allemagne")
* Service LookUp : choix entre Google-Map, OpenStreetMap ou coordonnées directes - plusieurs
  services peuvent également être créés ; ils sont alors traités les uns après les autres

|img_filter_01|


Configurer le filtre en frontend
----------------------------------

En frontend, une liste MetaModel à filtrer avec un ensemble de filtres activé (par ex.
"Recherche par rayon") doit être disponible.

Dans le filtre frontend MetaModel, le MetaModel correspondant ainsi que l'ensemble de filtres
"Recherche par rayon" sont activés. Les attributs du filtre Recherche par rayon doivent
également être activés.

Le réglage "Actualiser lors d'une modification" ne devrait pas être coché, sinon le formulaire
démarre déjà dès qu'une seule valeur d'adresse/rayon a été modifiée.

|img_fe-filter_01|

Dans la sortie frontend, un filtre avec deux possibilités de saisie devrait maintenant être
visible, permettant de filtrer la liste.

|img_fe-filter_02|


Remarques
---------

Pour le filtrage, l'adresse doit être saisie de manière aussi précise que possible.
Actuellement, il n'est pas vérifié si une saisie d'adresse donne lieu à plusieurs
"résultats" auprès du service LookUp.

Si, lors de la transmission des données dans le filtre frontend, les coordonnées concrètes
sont également transmises en plus de l'adresse - par ex. avec une détermination GPS via
JavaScript - le choix "coordonnées" devrait figurer en premier parmi les services LookUp.

La résolution d'une adresse en longitude et latitude lors de la saisie dans le backend peut
également être réalisée via le service LookUp -
`voir la présentation de la CK23 <https://www.e-spin.de/contao-metamodels/metamodels-vortrag-contao-konferenz-2023.html>`_

Dans un développement ultérieur de l'extension, les libellés deviendront multilingues.

Merci de signaler les erreurs et remarques sur `Github <https://github.com/MetaModels/filter_perimetersearch>`_
- les financements de fonctions supplémentaires ou du développement futur sont également les
bienvenus.


.. _extended_geodistance:
Distance géographique
======================

La recherche par rayon détermine les enregistrements qui se trouvent à l'intérieur d'un rayon.
Si l'on souhaite en outre savoir à quelle distance les points de données se trouvent de
l'adresse de référence, il faut installer en plus l'attribut "Distance géographique". Cet
"attribut virtuel" a pour seule fonction de calculer, lors d'un filtrage par recherche par
rayon, la distance correspondante et de la transmettre aux enregistrements. La valeur par
défaut de l'attribut est ``-1``. La sortie se fait en km.

Créer les attributs
--------------------

Les réglages de l'attribut sont analogues à ceux de la règle de filtre - il faut noter que le
champ "Paramètre GET pour l'adresse" doit avoir une valeur identique à celle du "paramètre URL"
de la règle de filtre Recherche par rayon.

* Paramètre GET pour l'adresse : paramètre URL de la règle de filtre Recherche par rayon
* Mode de données : Mode multiple (actuellement seul le mode multiple est disponible)
* Attributs pour latitude et longitude : sélectionner les attributs correspondants
* Pays par défaut : définit si et, le cas échéant, quel pays doit être ajouté à l'adresse pour
  la recherche lookup (par ex. valeur par défaut "Allemagne")
* Services LookUp : choix entre Google-Map, OpenStreetMap ou coordonnées directes - plusieurs
  services peuvent également être créés ; ils sont alors traités les uns après les autres

Remarques
---------

Si les résultats de la liste MM doivent être triés selon la distance géographique après une
recherche par rayon, il faut sélectionner l'attribut de distance géographique dans l'option
"Trier par" ainsi que Croissant (ASC).

Si l'on souhaite que la liste soit triée par défaut selon un autre attribut comme le nom ou
autre, et ne bascule que lors d'une recherche par rayon, il faut configurer cela en conséquence.
Il faut d'abord activer la case à cocher "Autoriser le remplacement du tri". Cela permet
d'adapter ou de changer dynamiquement le tri.

Pour cela, on peut par exemple mettre en place une redirection automatique dans le
:ref:`template de la liste MM <component_templates>` - le fait de savoir si la recherche par
rayon est active peut être déterminé par ex. via ``filterParams`` avec le paramètre URL
``adresse``

.. code-block:: php
   :linenos:

   <?php
   if(\array_key_exists('adresse', $this->filterParams)) {
       // Umleitung Sortierung Geo-Abstand (mit Parameter)...
   } else {
       // Umleitung Sortierung Standardsortierung (ohne Parameter)...
   }

Pour en savoir plus sur les :ref:`paramètres de tri, voir ici <rst_cookbook_templates_fe_list_sorting>`.



.. |img_attribute_01| image:: /_img/screenshots/extended/perimetersearch/attribute_01.png
.. |img_filter_01| image:: /_img/screenshots/extended/perimetersearch/filter_01.png
.. |img_fe-filter_01| image:: /_img/screenshots/extended/perimetersearch/fe-filter_01.png
.. |img_fe-filter_02| image:: /_img/screenshots/extended/perimetersearch/fe-filter_02.png
