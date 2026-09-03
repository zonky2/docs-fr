.. _rst_cookbook_filter_filter-with-forwarding:

Filtre avec redirection
==========================

Si l'on souhaite répartir le filtrage d'une liste MM sur plusieurs pages, on peut utiliser l'option
« Redirection » et y indiquer la page cible. Par exemple, sur un site de voyages, on pourrait intégrer sur
différentes pages une demande de départ de voyage et de nombre de personnes comme « pré-filtrage », puis rediriger
vers la page de liste proprement dite avec des requêtes supplémentaires.

Dans MM, un élément de filtre est également chargé de convertir les paramètres POST envoyés avec le formulaire de
filtre en paramètres GET pour le filtrage de la liste. Pour cette raison, il est nécessaire qu'un filtre soit
également intégré sur la page cible, afin qu'il assure cette tâche.

La responsabilité du traitement du formulaire est gérée par Contao via la valeur du champ « FORM_SUBMIT » - cette
valeur doit être identique. Il existe deux façons d'y parvenir :

**Module FE MM-Filter**

Si l'on crée un module FE MM-Filter et qu'on l'intègre sur les pages souhaitées via la sélection de module CE, la
valeur de « FORM_SUBMIT » est toujours identique. L'inconvénient est que la sélection des widgets de filtre dans
les réglages du module est également identique partout. On peut contourner cet inconvénient en intégrant sur la
page cible un filtre supplémentaire pour d'autres options. Si les paramètres d'URL des widgets de filtre sont
identiques entre les filtres, le second filtre réagit également aux paramètres GET existants.

**CE MM-Filter avec ID de formulaire personnalisé**

.. note:: L'ID de formulaire peut être personnalisé à partir de MM 2.3.

On peut créer un CE MM-Filter sur la ou les pages de départ ainsi que sur la page cible, et saisir la même valeur
dans le champ ID de formulaire. Le filtre sur la page cible reprend alors le traitement correspondant des
paramètres POST. L'avantage ici est qu'il est plus facile de sélectionner les widgets de filtre à afficher pour un
CE MM-Filter.

Le filtre, qu'il s'agisse d'un module FE ou d'un CE, qui assure la conversion « POST-vers-GET », n'a pas besoin
d'être visible sur la page cible et peut également être masqué si nécessaire.


