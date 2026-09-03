.. _component_dca-combine:

|svg_dca_combine_32| |img_dca_combine_32| Affectations saisie/rendu
=====================================================================

.. note:: définir les options d'accès aux réglages de rendu et masques de saisie ;
  l'accès pour la ou les saisies du BE devrait au moins être activé pour le groupe
  d'utilisateurs 'Administrateur'

Introduction
------------

Les affectations saisie/rendu permettent de définir les droits pour les réglages de rendu créés.
Pour chaque entrée, les champs de sélection suivants sont disponibles :

* Groupe de membres
* Groupe d'utilisateurs
* Réglage de rendu
* Masque de saisie

Pour l'affichage et l'accès dans le backend, un masque de saisie et un réglage de rendu devraient
par défaut être activés pour le groupe d'utilisateurs « Administrateur ».

Il est possible de créer plusieurs affectations et ainsi de contrôler les accès à la sortie en
liste et aux masques de saisie. Les masques de saisie pour les membres ne sont pertinents que pour
l'édition en frontend.

Si plusieurs affectations (lignes) sont créées, elles sont traitées « de haut en bas », c'est-à-dire
que le premier groupe indiqué est évalué comme valide pour le groupe de membres ou d'utilisateurs.
Il faut noter que l'entrée « * » représente un « catch all » et s'applique aux réglages pour tous
les groupes restants.

Si l'on souhaite par ex. qu'aucun « catch all » ne s'applique dans une ligne, ou qu'aucun groupe ne
soit pris en compte, on peut créer un groupe de membres ou d'utilisateurs, par ex. « empty », auquel
aucun membre ni utilisateur n'est affecté.


Déroulement
-----------

Effectuer les sélections dans les colonnes prévues des affectations saisie/rendu et enregistrer.
Les possibilités de saisie du MetaModel devraient désormais être visibles dans le backend.


.. |svg_dca_combine_32| image:: /_img/icons_svg/dca_combine.svg
   :width: 32px
.. |img_dca_combine_32| image:: /_img/icons/dca_combine_32.png
.. |img_dca_combine| image:: /_img/icons/dca_combine.png
