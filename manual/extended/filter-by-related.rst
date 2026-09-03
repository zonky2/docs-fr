.. _rst_extended_filter_by_related:

Filter-by-related pour MetaModels
==================================

.. note:: Le Filter-by-related est encore en financement participatif et ne sera débloqué qu'une fois le montant
   cible actuel de 3 575,00 € atteint. |br|
   Une installation anticipée est possible via le "programme Early-Adopter" – `voir ci-dessous <#early-adopter-programm>`_  |br|
   La règle de filtre "Filter-Parent" a été intégrée dans cette règle de filtre - la restriction de la relation
   aux tables enfants a été supprimée.

Le Filter-by-related permet de filtrer des items en fonction des propriétés d'un MetaModel lié (relation). Une
sélection unique (Select) ou une table enfant sont possibles comme relations.

Exemples : nous avons des employés et des déplacements professionnels - les déplacements professionnels sont
définis comme table enfant des employés. Si l'on souhaite maintenant afficher par exemple tous les déplacements
professionnels dont l'employé appartient au service xy, il faut un filtre spécial - notamment si l'on souhaite
rendre ce filtrage variable en frontend.

Un autre exemple serait les dates de séminaires, lorsque les mêmes séminaires se répètent à différents jours. Pour
le séminaire, on pourrait définir toutes les propriétés de base d'un séminaire comme le titre, le contenu mais
aussi la catégorie etc., et pour la date, il y aurait une sélection unique vers le séminaire ainsi que la date, le
nombre de participants etc. Si l'on souhaite maintenant filtrer la liste des dates par exemple selon une catégorie
des séminaires, cela est possible avec cette règle de filtre.


Programme Early-Adopter
------------------------

Le refinancement se fait via un "programme Early-Adopter", c.-à-d. que l'on peut utiliser la ou les extension(s)
immédiatement moyennant le versement d'un don. Le paiement autorise l'utilisation pour un projet. Toute prétention
juridique est exclue après le versement d'un don.

Le montant du don devrait être d'au moins 200€*1.

Pour le don, une facture avec TVA indiquée est établie, ou en net pour l'étranger UE en cas d'identifiant de TVA
intracommunautaire existant. |br|
En cas d'intérêt ou de questions supplémentaires, merci d'envoyer un e-mail à info@e-spin.de

*1 Net – TVA éventuellement en sus.


Installation via Composer
--------------------------

Conditions préalables à l'installation :

* MetaModels Core à partir de la version 2.4 avec au moins PHP 8.2

Le module peut être installé via la console ou via le Contao-Manager.

Créer une règle de filtre
--------------------------

La règle de filtre est créée comme d'habitude sous Filtre. Les réglages sont dérivés de la règle de filtre "Requête
simple". Comme type de filtre, on sélectionne "Filtre sur l'attribut du modèle avec une relation". Le masque suivant
apparaît alors :

|img_filterparameter|

Dans les réglages, il faut sélectionner le "Modèle pour la relation" ainsi que l'attribut faisant office de filtre
en tant qu'"Attribut du modèle de la relation". Pour "Colonne/attribut de la relation", il faut sélectionner la PID
pour les tables enfants, et l'attribut correspondant pour une liaison par sélection unique.

Les autres paramètres de réglage sont analogues à ceux de la règle de filtre "Requête simple".

Si le type de widget "Texte" est choisi, le réglage "Type de recherche" apparaît en plus. Il permet de définir
comment le terme de recherche saisi est comparé à la valeur de l'attribut lié – par défaut, la valeur doit
contenir le terme de recherche, mais on peut aussi choisir une correspondance exacte, un début ou une fin
correspondants. Une étoile (``*``) saisie par le visiteur agit comme un joker et prévaut sur le réglage.


Dons
----

Un grand merci pour les dons* pour cette extension à :

* N.N. : 400 €
* N.N. : 400 €
* `Agentur Markenzoo <https://markenzoo.de/>`_ : 200€
* `GUTcert GmbH <https://www.gut-cert.de/>`_ : 212,50€
* `Naturpark Dümmer <https://www.naturpark-duemmer.de/>`_ : 350€
* `RSM certification GmbH <https://www.rsm-certification.de/>`_ : 350€


(Dons nets)


.. |br| raw:: html

   <br />


.. |img_filterparameter| image:: /_img/screenshots/extended/filter-by-related/filterparameter.jpg
