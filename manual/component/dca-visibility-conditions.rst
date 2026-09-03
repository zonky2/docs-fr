.. _component_dca_visibility-conditions:

|svg_dca_condition_22| |img_dca_condition| Propriétés d'affichage / Sous-palettes
==================================================================================

Les propriétés d'affichage sont également désignées par le terme « sous-palettes », car elles
permettent d'afficher ou de masquer de manière ciblée le widget de saisie d'un attribut dans un
masque de saisie, en fonction des valeurs d'un autre widget.

Un exemple pour illustrer cela : dans un masque de saisie, il existe une case à cocher « Adresse
de facturation » et l'on souhaite que, lorsqu'elle est cochée, trois autres champs de saisie (rue,
code postal, ville) apparaissent dans le masque de saisie - et uniquement lorsque la case est
cochée.

Dans ce cas, les trois champs (rue, code postal, ville) réagissent à la valeur de la case à cocher
« Adresse de facturation » (valeur = 1) et sont affichés lorsque la case est cochée, et c'est
uniquement dans ce cas que les données sont également enregistrées.

L'idée d'afficher ou de masquer les champs via une légende (« ligne de séparation verte ») est
insuffisante - cela ne fait que régler la visibilité actuelle sous forme d'un accordéon, sans
influencer l'enregistrement. De plus, les propriétés d'affichage/sous-palettes permettent
également d'établir des règles complexes définissant sous quelle condition un widget de saisie
doit être visible ou non.

Il faut noter que les propriétés d'affichage ne sont pas créées comme un accordéon avec deux
« éléments d'encadrement » englobant plusieurs widgets de saisie ; les conditions doivent au
contraire être définies séparément pour chaque widget. C'est seulement ainsi qu'il est possible
d'établir des règles d'affichage très complexes et dépendantes les unes des autres.

Si l'on a créé une règle complexe pour un widget de saisie et que l'on souhaite l'attribuer
facilement à d'autres widgets de saisie, on peut utiliser le type de propriété « La propriété est
visible... » (voir ci-dessous).

Pour créer une propriété d'affichage, on clique dans la liste des attributs d'un masque de saisie
sur l'icône |img_dca_condition_1| « Conditions d'affichage du champ de saisie ID n ». Dans
l'aperçu des propriétés d'affichage qui s'ouvre, une nouvelle propriété d'affichage est ajoutée en
cliquant sur le bouton |img_new| « Nouveau » et en l'insérant via le presse-papiers.

Dans le masque de saisie qui s'ouvre, il faut d'abord sélectionner le type de condition dans la
configuration de base. Deux groupes de types de conditions sont disponibles :

* les conditions qui se rapportent à un attribut ou à un widget de saisie
* les conditions sous forme d'opérateurs logiques (ET/OU/NON)

Comme aide-mémoire, les types et leur utilisation sont décrits dans l'assistant d'aide |img_help|.

Pour les widgets ayant une condition d'affichage définie, l'icône est mise en évidence par une
couleur |img_dca_condition|.

Les types de conditions suivants sont implémentés :

* |svg_condition_propertyvalueis_22| **La valeur de la propriété est...** |br|
  La condition est remplie lorsque la valeur de l'attribut est égale à la valeur définie.
  Peuvent être sélectionnés comme attributs ceux avec sélection simple, comme par ex. Select ou
  Case à cocher. \*
* |svg_condition_propertycontainanyof_22| **La valeur de la propriété peut contenir...** |br|
  La condition est remplie lorsqu'une valeur quelconque de l'attribut est égale à la valeur
  définie respectivement (intersection ou OU). Peuvent être sélectionnés comme attributs ceux
  avec sélection multiple, comme par ex. Tags.
* |svg_condition_propertyvisible_22| **La propriété est visible...** |br|
  La condition est remplie lorsque toutes les conditions d'un attribut sélectionné sont remplies.
  En d'autres termes, l'attribut est visible uniquement lorsque l'attribut sélectionné (ou
  « référencé ») est également visible. Ce type de condition évite de dupliquer les conditions
  d'affichage déjà créées pour un attribut.
* |svg_condition_or_22| **OU** |br|
  Une condition quelconque doit être remplie.
* |svg_condition_and_22| **ET** |br|
  Toutes les conditions doivent être remplies.
* |svg_condition_not_22| **NON** |br|
  Inverse le résultat d'une condition donnée.

.. note:: \* à partir de la version 2.3, la condition vide ou non renseignée d'un widget Select ou
   Case à cocher peut également être utilisée sans configuration supplémentaire - :ref:`jusqu'à
   MM 2.2, un « NOT » supplémentaire était nécessaire <rst_cookbook_inputmask_checkbox-negation>`.
   Veuillez noter que pour une case à cocher, les valeurs « - » et « Inactif » sont équivalentes,
   de sorte que le Select revient à la première valeur « - » après l'enregistrement.


.. |svg_dca_condition_22| image:: /_img/icons_svg/dca_condition.svg
   :width: 22px
.. |img_dca_condition| image:: /_img/icons/dca_condition.png
.. |svg_condition_propertyvalueis_22| image:: /_img/icons_svg/condition_propertyvalueis.svg
   :width: 22px
.. |svg_condition_propertycontainanyof_22| image:: /_img/icons_svg/condition_propertycontainanyof.svg
   :width: 22px
.. |svg_condition_propertyvisible_22| image:: /_img/icons_svg/condition_propertyvisible.svg
   :width: 22px
.. |svg_condition_or_22| image:: /_img/icons_svg/condition_or.svg
   :width: 22px
.. |svg_condition_and_22| image:: /_img/icons_svg/condition_and.svg
   :width: 22px
.. |svg_condition_not_22| image:: /_img/icons_svg/condition_not.svg
   :width: 22px
.. |img_dca_condition_1| image:: /_img/icons/dca_condition_1.png
.. |img_new| image:: /_img/icons/new.gif
.. |img_about| image:: /_img/icons/about.png
.. |img_help| image:: /_img/icons/help.svg

.. |br| raw:: html

   <br />
