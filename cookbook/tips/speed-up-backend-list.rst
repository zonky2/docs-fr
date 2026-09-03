.. _rst_cookbook_tips_speedup_backend:

Accélération de l'affichage dans le backend en présence de nombreux enregistrements
=========================================================================================

Avec un très grand nombre d'enregistrements - à partir d'environ 5 000 ou plus - la construction de la vue en liste
ou du masque de saisie peut prendre beaucoup de temps et consommer beaucoup de mémoire. Cela dépend de différents
facteurs, tels que les types d'attributs présents ou les réglages du panneau de la liste ou du masque de saisie.
Voici quelques conseils pour accélérer l'affichage :

1. Régler la limite |br|
   Dans les réglages du masque de saisie, saisir la clé « limit » dans le champ « Panel-Layout ».
   La vue en liste est ainsi paginée.
2. Supprimer/modifier les filtres |br|
   Si certains attributs sont activés pour un filtrage, il vaut mieux ne pas les utiliser en présence de très
   grandes quantités de données. Les filtres ne fonctionnent pas indépendamment les uns des autres, de sorte que
   les requêtes à exécuter deviennent très longues à traiter à mesure que le nombre de filtres et d'enregistrements
   augmente. Comme alternative au filtrage, les attributs peuvent être activés pour une recherche. La
   restriction de la liste reste identique - simplement, aucune donnée prédéfinie n'est présente dans le panneau.
   Pour MM 3.x, une optimisation supplémentaire est prévue à ce niveau.
3. Doter la table en base de données d'un index |br|
   L'affichage avec de grandes quantités de données peut être accéléré en créant un ou plusieurs index. Avec peu
   d'enregistrements, cela peut au contraire ralentir l'exécution des requêtes, c'est pourquoi ces index ne sont pas
   créés automatiquement par MM. Les colonnes de la table utilisées dans une recherche devraient recevoir un index,
   par ex. la colonne « surname » dans la table « mm_employees ». Cela peut être créé avec la requête suivante : |br|
   ```create index mm_employees_surname_id_index on mm_employees (surname, id);``` |br|
   De même, les masques de saisie peuvent présenter une construction ralentie - par ex. en cas de références vers
   d'autres tables, comme une sélection sur des membres - dans ce cas, créer également un index sur la colonne
   correspondante |br|
   ```create index mm_employees_member_index on mm_employees (member);```

.. |br| raw:: html

   <br />
