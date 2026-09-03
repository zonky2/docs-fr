.. _rst_cookbook_tips_set-route-priority:

Définir la priorité de route
================================

.. note:: La priorité de route est implémentée à partir de Contao 4.13 et est prise en compte à partir de MM 2.3.

Contao et MetaModels doivent extraire d'une URL donnée la page via l'alias et les éventuels paramètres slug
(paires clé-valeur) qu'elle contient, et réagir en conséquence. Cela peut entraîner des chevauchements et
différentes « possibilités d'interprétation » quant à la signification des éléments de l'URL. La priorité de route
permet d'influencer l'ordre de traitement. Les exemples suivants doivent donner un aperçu des possibilités.


Filtrage avec « folderurl » et « auto_item »
------------------------------------------------

Une structure typique pour l'affichage de données avec MM est une page de liste et une page de détail. Sur la page
de détail, la clé pour le filtrage via le paramètre d'URL « auto_item » est souvent masquée. En outre, la page de
détail est souvent une sous-page de la page de liste. Avec ``folderurl`` activé, les pages pourraient être
structurées comme suit :

* Alias de la page de liste : ``projekte``
* Alias de la page de détail : ``projekte/projekt``

Avec une valeur de filtre MM ``test``, l'URL complète serait ``projekte/projekt/test`` (sans domaine ni suffixe).

Cela pourrait alors être interprété comme

* Alias : ``projekte`` avec clé : ``projekt`` et valeur : ``test`` - ou
* Alias : ``projekte/projekt`` avec clé : ``auto_item`` et valeur : ``test``

Sans priorisation de la résolution, il serait plus ou moins laissé au hasard de savoir quelle variante est résolue
en premier. Si l'on définit dans les propriétés de la page de détail une priorité de route plus élevée (10) que
celle de la page de liste (0), le traitement devient univoque et s'effectue proprement.

Si l'alias de la page de détail est par ex. simplement ``projekt-details``, la résolution ne pose aucun problème et
la priorité de route n'est pas nécessaire.


Page de liste et de détail avec le même alias
---------------------------------------------------

Si l'on souhaite afficher la page de liste et la page de détail avec le même alias de page, cela peut être obtenu
avec les réglages suivants :

**Page de liste :**

* Titre : Liste
* Alias : liste
* Priorité de route : 0
* Élément requis : désactivé
* MM Liste - dans les réglages de rendu, réglages de redirection vers la page « Détails » + filtre

**Page de détail :**

* Titre : Détails
* Alias : liste
* Priorité de route : 10
* Élément requis : activé
* MM-Liste avec règle de filtre « Requête simple » et paramètre d'URL « auto_item »

La liste est alors par ex. accessible via l'alias ``projekte``, et une vue de détail via ``projekte/test``.


Lien vers une page de détail dans la navigation
------------------------------------------------

Si l'on souhaite intégrer une ou plusieurs pages de détail MM dans la navigation de page Contao normale, il
convient de travailler avec des extensions appropriées et d'utiliser leurs hooks ou événements.

Une solution rapide consiste à créer une page Contao normale, par ex. avec l'alias ``projekte/test``, ainsi qu'une
page de détail avec l'alias ``projekte``, dont la vue de détail peut être appelée via ``projekte/test``
(paramètre d'URL « auto_item »).

Si l'on donne à la page de détail MM une priorité de route plus élevée (10) que la page Contao normale (0), le lien
est résolu proprement.
