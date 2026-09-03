.. _rst_cookbook_filter_exclusion:

Règle de filtre en exclusion
=================================

Si l'on souhaite créer un filtre qui ne « restreint » pas un attribut mais l'« exclut », on peut y parvenir avec un
agencement particulier des règles de filtre.

Comme exemple, on peut reprendre la :ref:`liste des employés <mm_first_conclusion>`.
Si un filtre est créé sur le département, les résultats sont restreints exactement au
département sélectionné dans le filtre, c.-à-d. que seuls les items pour lesquels
« département égal à la valeur du filtre » sont affichés - par ex. « Filtrer tous les
employés du département 'Marketing' ».

Si l'on souhaite au contraire tous les départements **sauf** celui sélectionné dans le
filtre (donc l'exclure, par ex. « Filtrer tous les employés qui ne sont pas dans le
département 'Marketing' »), on peut procéder comme suit :

* on ajoute une règle de filtre « Condition OU (OR) » avec la case « Arrêter après la première correspondance »
  cochée
* dans cette règle de filtre viennent une règle de filtre « SQL personnalisé » ainsi qu'une règle de filtre
  telle que « Sélection simple »

Les règles de filtre devraient ensuite être agencées à peu près comme sur la capture d'écran.

|img_exclusion|

Dans la règle de filtre « SQL personnalisé », on saisit la requête suivante :

.. code-block:: php
   :linenos:

   SELECT id
   FROM {{table}}
   WHERE abteilung IN (
     SELECT id
     FROM mm_abteilung
     WHERE alias != {{param::get?name=abteilung}}
     OR ({{param::get?name=abteilung}} IS NULL)
   )

**Contexte :** La règle de filtre « Sélection simple » sert uniquement à créer, respectivement afficher, le
widget de formulaire en frontend. Le filtrage à proprement parler s'effectue dans la règle de filtre « SQL
personnalisé ». Le traitement des autres règles de filtre dans la « branche OU » est cependant interrompu, de
sorte que la règle de filtre « Sélection simple » elle-même n'entre plus en jeu.


.. |img_exclusion| image:: /_img/screenshots/cookbook/filter/exclusion.jpg

