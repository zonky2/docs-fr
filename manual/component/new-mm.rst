.. _component_new-mm:

|img_new| Nouveau MetaModel
=============================

.. note:: créer un nouveau MetaModel (table de base de données), activer si nécessaire la
   traduction ou les variantes |br|
   Pour créer la table mm_*, effectuer une migration de base de données - :ref:`voir Gestionnaire
   de schéma <component_schema-manager>`


Introduction
------------
En cliquant sur l'icône « |img_new| Nouveau MetaModel », un masque de saisie s'ouvre pour créer un
nouveau MetaModel. Lors de l'enregistrement du nouveau MetaModel, une nouvelle table propre est
créée dans la base de données pour accueillir les valeurs à stocker.

Pour l'enregistrement du nouveau MetaModel, deux saisies sont donc obligatoires : le nom du
MetaModel ainsi que le nom de la table.

Le nom du MetaModel sert à la désignation dans le backend et peut être choisi librement. La
désignation devrait cependant permettre de déduire raisonnablement le contenu pour la suite du
travail, par ex. « Adresses ».

Il en va de même pour le nom de la table, le préfixe « mm\_ » pouvant être saisi dans le nom de la
table ou étant ajouté automatiquement. La table pourrait par ex. s'appeler « mm_address » - il
existe différents « courants d'opinion » quant à savoir si le nom doit être au singulier ou au
pluriel.

Lors de la création de la table, seules quelques colonnes nécessaires au bon fonctionnement avec
l'extension MetaModels sont créées, comme id, pid, timestamp, etc. Les autres colonnes
individuelles sont créées sous forme de « attributs » et dotées de leurs options spécifiques. Pour
en savoir plus, voir le point :ref:`component_attribute`.


Options
-------

Lors de la création d'un nouveau MetaModel, il existe les options supplémentaires « Traduction » et
« Variantes ».

Si l'option « Traduction » a été sélectionnée, plusieurs langues sont disponibles à la sélection
après un rechargement de la page. L'une des langues devrait être activée comme « repli
(fallback) » - si cela n'est pas fait, la première langue sélectionnée est utilisée comme langue de
repli. Si l'option « Traduction » est activée dans le MetaModel, des attributs multilingues
spéciaux sont également proposés en supplément à la sélection.

En cas d'activation ultérieure du multilinguisme, les attributs existants ou les valeurs saisies ne
sont pas repris automatiquement. Il convient donc de clarifier autant que possible en amont si un
multilinguisme est nécessaire.

Si l'option « Variantes » a été sélectionnée, on ne constate d'abord aucune autre modification du
MetaModel. Si l'option est activée, il devient possible d'activer l'option « Écraser les variantes »
au niveau des attributs. Avec tous les attributs pour lesquels l'option « Écraser les variantes »
est activée, d'autres masques de saisie peuvent être créés pour la saisie des variantes, par ex.
pour « écraser » les « valeurs parentes ». Les masques de saisie des variantes sont accessibles via
l'icône « |img_variants| Nouvelle variante » dans l'affichage en liste des éléments parents.

Avec les variantes se crée une « relation parent-enfant » au sein d'une table de base de données
MetaModel, qui peut être retracée via différentes valeurs dans la table - par ex. avec un filtre SQL
personnalisé. Les enregistrements parents se caractérisent par le fait que, dans la table de base
de données, les enregistrements parents ont la valeur varbase égale à 1 et vargroup égale à leur
propre ID. Les enregistrements enfants ont les valeurs varbase égale à 0 et vargroup égale à l'ID de
l'enregistrement parent.


.. |img_variants| image:: /_img/icons/variants.png
.. |img_new| image:: /_img/icons/new.gif


.. |nbsp| unicode:: 0xA0
   :trim:

.. |br| raw:: html

   <br />
