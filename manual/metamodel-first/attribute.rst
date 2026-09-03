.. _mm_first_attribute:

|svg_fields_32| |img_fields_32| Attributs
==========================================

Une fois la table « mm_listeemployes » créée dans la base de données, il faut y
créer les champs, respectivement les colonnes de table, permettant de stocker
les données - c'est-à-dire les attributs. Cette étape se déroule via le composant
du même nom « |svg_fields_22| |img_fields| Attributs ».

D'après l'énoncé de la tâche, les champs suivants sont nécessaires :

+-----------------+----------------+----------+
| **Désignation** | **Attr.-Name** | **Type** |
+-----------------+----------------+----------+
| Nom             | name           | Text     |
+-----------------+----------------+----------+
| Prénom          | vorname        | Text     |
+-----------------+----------------+----------+
| E-mail          | email          | Text     |
+-----------------+----------------+----------+
| Département     | abteilung      | Text     |
+-----------------+----------------+----------+
| Publié          | published      | Checkbox |
+-----------------+----------------+----------+

Dans un premier temps, on passe dans le MetaModel « Liste des employés » au composant
« Attributs » en cliquant sur l'icône |svg_fields_22| |img_fields|. Ensuite, le premier
attribut peut être créé via « |img_new| Nouvel attribut ». Le clic sur
« |img_new| Nouvel attribut » n'ouvre pas immédiatement le masque de saisie, mais fait
apparaître une « |img_pasteafter| icône de pochette » sur laquelle il faut cliquer
(voir la copie d'écran).

|img_attribute_01|

Le clic sur l'« |img_pasteafter| icône de pochette » ouvre le masque de saisie pour
l'attribut. On y choisit d'abord le type d'attribut « Text » dans la liste de sélection
et, après actualisation du masque de saisie, les champs nécessaires sont disponibles
pour la saisie. Ceux-ci sont remplis pour le premier attribut « Nom » comme indiqué
dans la copie d'écran.

|img_attribute_02|

Avec « Enregistrer et fermer », l'attribut « Nom » est créé, c'est-à-dire que la
colonne « name » est générée dans la table de la base de données, puis on est
redirigé vers la vue d'ensemble des attributs. Ces étapes de création d'un attribut
sont ensuite répétées pour Prénom, E-mail et Département.

Pour l'attribut « Publié », un nouvel attribut est également créé, mais en choisissant
le type d'attribut « Case à cocher (Checkbox) ». Pour cet attribut, l'option
« Publication » est activée dans les « réglages avancés » (voir la copie d'écran).

|img_attribute_03|

La liste des attributs créés devrait maintenant s'afficher comme indiqué dans la
copie d'écran.

|img_attribute_04|


.. |img_fields_32| image:: /_img/icons/fields_32.png
.. |img_fields| image:: /_img/icons/fields.png
.. |svg_fields_22| image:: /_img/icons_svg/fields.svg
   :width: 22px
.. |svg_fields_32| image:: /_img/icons_svg/fields.svg
   :width: 32px
.. |img_new| image:: /_img/icons/new.gif
.. |img_pasteafter| image:: /_img/icons/pasteafter.gif

.. |img_attribute_01| image:: /_img/screenshots/metamodel_first/attribute_01.png
.. |img_attribute_02| image:: /_img/screenshots/metamodel_first/attribute_02.png
.. |img_attribute_03| image:: /_img/screenshots/metamodel_first/attribute_03.png
.. |img_attribute_04| image:: /_img/screenshots/metamodel_first/attribute_04.png

.. |br| raw:: html

   <br />

.. |nbsp| unicode:: 0xA0
   :trim:
