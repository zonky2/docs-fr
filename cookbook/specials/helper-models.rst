.. _rst_cookbook_specials_helper-models:

Modèle auxiliaire - regrouper différentes données de sélection dans un MetaModel
==================================================================================

Lors de la construction d'une structure de données, il est fréquent d'avoir besoin de sélections simples telles que
civilité, titre académique, sexe, couleurs, unités de mesure, remises, etc. Il faudrait alors créer chacune de ces
listes comme un modèle distinct et l'intégrer dans le modèle souhaité sous forme de relation via une sélection
simple ou multiple.

Cela aurait pour conséquence de devoir créer une multitude de modèles qui, au final, ne comportent chacun que deux
attributs : nom et alias.

La construction et la maintenance de ces « données auxiliaires » peuvent être simplifiées en gérant les données dans
une construction de modèle auxiliaire et en n'affichant, dans le masque de saisie, que les valeurs correspondantes
grâce à un filtrage.

L'inconvénient de cette variante est cependant un manque de flexibilité lors des adaptations : il peut être
nécessaire de réintégrer certaines plages de valeurs dans un modèle séparé. Par exemple, si les entrées « Remises »
doivent ultérieurement recevoir, en plus de la désignation, une valeur de remise numérique.

Voici un exemple de structure possible : on crée deux MetaModels - l'un pour les désignations des groupes de
désignations, par ex. « Groupes de taxonomie », et un MetaModel pour les valeurs de désignation, par ex. « Valeurs de
taxonomie ». Dans le modèle où les valeurs sont nécessaires en tant que sélection, on crée une référence sous forme
de sélection simple ou multiple vers le modèle « Valeurs de taxonomie », ainsi qu'un filtre qui n'affiche que les
valeurs du groupe de taxonomie souhaité. Les étapes seraient les suivantes :

**1. Créer le MetaModel « Groupes de taxonomie »**

* Attribut Texte ou Texte traduit avec « Nom », champ obligatoire
* Attribut Alias avec « Alias » sur « Nom », valeurs uniques et forcer la recréation

**2. Créer le MetaModel « Valeurs de taxonomie »**

* Attribut Sélection simple avec « Groupes de taxonomie » sur le modèle « Groupes de taxonomie », champ obligatoire
* Attribut Texte ou Texte traduit avec « Nom », champ obligatoire
* Attribut Alias ou Alias traduit avec « Alias » sur « Nom », valeurs uniques et forcer la recréation
* Tri sur « Groupes de taxonomie », type de regroupement « Première lettre » et longueur de regroupement 0
* Filtre « Sélection du groupe » avec la règle de filtre « Sélection simple » sur l'attribut « Groupes de
  taxonomie » et cocher la case « Paramètre statique »

|img_helper-models_01|

**3. Intégration dans le MetaModel avec sélection**

* Attribut Sélection simple ou multiple sur le modèle « Valeurs de taxonomie », filtre « Sélection du groupe » et,
  dans le paramètre de filtre de la sélection, choisir un groupe, par ex. « Civilité ».

|img_helper-models_02|

Outre cette variante à deux tables, il est également possible de travailler avec une seule table, par ex. avec les
options « Variantes » ou le mode de rendu « Hiérarchie » - les réglages du filtre doivent alors être adaptés en
conséquence.


.. |img_helper-models_01| image:: /_img/screenshots/cookbook/specials/helper-models_01.png
.. |img_helper-models_02| image:: /_img/screenshots/cookbook/specials/helper-models_02.png
