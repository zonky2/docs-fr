.. _mm_first_dca:

|svg_dca_32| |img_dca_32| Masques de saisie
=============================================

Dans cette étape, le masque de saisie du MetaModel « Liste des employés » est créé ;
c'est par son intermédiaire que les données des attributs sont enregistrées dans
la base de données.

Pour accéder aux masques de saisie, on active de nouveau la vue d'ensemble des
MetaModels, de sorte que l'entrée « Liste des employés » soit visible. On clique
alors sur l'icône « |svg_dca_22| |img_dca| Masques de saisie » et la vue bascule
sur la vue d'ensemble des masques de saisie - celle-ci est encore vide pour l'instant.

Après un clic sur « |img_new| Nouveau masque de saisie », le masque de réglage du
masque de saisie s'ouvre immédiatement. Dans le champ de saisie « Nom », on entre
une désignation telle que « Saisie ». Une autre saisie importante est la sélection
« Intégration », pour laquelle on choisit « Indépendant » et, dans la sélection
qui s'ajoute alors, « Zone du backend », l'entrée « MetaModels » doit être
sélectionnée. De plus, les trois cases à cocher du bloc « Data manipulation
permissions » doivent être activées - voir la copie d'écran. La saisie est
enregistrée avec « Enregistrer et fermer ».

|img_dca_01|

Dans la vue d'ensemble des masques de saisie, la première entrée « Saisie »
devrait maintenant être visible - voir la copie d'écran.

|img_dca_02|

En cliquant sur l'icône « |svg_dca_setting_22| |img_dca_setting| Réglages », le
niveau suivant s'ouvre pour les attributs. C'est à cet endroit que sont
sélectionnés, respectivement activés, les attributs à afficher dans le masque
de saisie.

Comme pour les réglages de rendu, les attributs créés peuvent également être
ajoutés en une seule étape. Pour cela, il suffit de cliquer sur l'icône dans
l'en-tête « |svg_dca_add_22| |img_dca_add| Tout ajouter », puis de confirmer avec
les boutons « Suivant » et « Enregistrer et fermer ». Tous les attributs existants
sont alors ajoutés au masque de saisie. Par défaut, les attributs ne sont pas
activés - cela peut se faire facilement via l'« icône œil ».

Dans cet exemple, tous les attributs sont activés - la liste des attributs
devrait maintenant ressembler à la copie d'écran.

|img_dca_03|

Le masque de saisie n'est toujours pas visible dans le backend. Cela ne se produit
qu'une fois l'étape :ref:`component_dca-combine` terminée.


.. |svg_dca_32| image:: /_img/icons_svg/dca.svg
   :width: 32px
.. |img_dca_32| image:: /_img/icons/dca_32.png
.. |svg_dca_22| image:: /_img/icons_svg/dca.svg
   :width: 22px
.. |img_dca| image:: /_img/icons/dca.png
.. |svg_dca_setting_22| image:: /_img/icons_svg/dca_setting.svg
   :width: 22px
.. |img_dca_setting| image:: /_img/icons/dca_setting.png
.. |img_dca_setting_add| image:: /_img/icons/dca_setting_add.png
.. |svg_dca_add_22| image:: /_img/icons_svg/dca_add.svg
   :width: 22px
.. |img_dca_add| image:: /_img/icons/dca_add.png
.. |img_dca_groupsortsettings| image:: /_img/icons/dca_groupsortsettings.png
.. |img_dca_condition| image:: /_img/icons/dca_condition.png
.. |img_new| image:: /_img/icons/new.gif
.. |img_edit| image:: /_img/icons/edit.gif

.. |img_dca_01| image:: /_img/screenshots/metamodel_first/dca_01.png
.. |img_dca_02| image:: /_img/screenshots/metamodel_first/dca_02.png
.. |img_dca_03| image:: /_img/screenshots/metamodel_first/dca_03.png
