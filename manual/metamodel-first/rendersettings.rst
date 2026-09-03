.. _mm_first_rendersettings:

|svg_rendersettings_32| |img_rendersettings_32| Réglages de rendu
===================================================================

Dans cette étape, les réglages de rendu du MetaModel « Liste des employés » sont
créés. Un réglage de rendu est nécessaire pour le backend (saisie des données) et
un autre pour le frontend (affichage des données).

Pour accéder aux réglages de rendu, on active de nouveau la vue d'ensemble des
MetaModels, de sorte que l'entrée « Liste des employés » soit visible. On clique
alors sur l'icône « |svg_rendersettings_22| |img_rendersettings| Réglages de rendu »
et la vue bascule sur la vue d'ensemble des réglages de rendu - celle-ci est encore
vide pour l'instant.

Après un clic sur « |img_new| Nouveau », le masque de saisie du premier réglage de
rendu s'ouvre immédiatement. Dans le champ « Nom », on saisit une désignation
pertinente comme par exemple « BE Liste » (voir la copie d'écran), on coche la case
« Standard » et on enregistre la saisie avec « Enregistrer et fermer ».

|img_rendersettings_01|

Dans la vue d'ensemble des réglages de rendu, la première entrée « BE Liste »
devrait maintenant être visible - voir la copie d'écran.

|img_rendersettings_02|

En cliquant sur l'icône « |svg_rendersetting_22| |img_rendersetting| Réglages de
rendu des attributs », le niveau suivant s'ouvre pour les attributs. C'est à cet
endroit que sont sélectionnés, respectivement activés, les attributs à afficher
dans la liste correspondante du réglage de rendu.

Une manière simple d'ajouter les attributs créés consiste à cliquer sur l'icône
« |svg_rendersettings_add_22| |img_rendersettings_add| Tout ajouter » dans l'en-tête -
après avoir cliqué sur les boutons « Suivant » et « Enregistrer et fermer », tous les
attributs existants sont ajoutés au réglage de rendu. Par défaut, les attributs ne
sont pas activés - cela peut se faire facilement via l'« icône œil ». Dans cet
exemple, les attributs « Nom » et « Prénom » sont activés - la liste des attributs
devrait maintenant ressembler à la copie d'écran.

|img_rendersettings_03|

Les réglages de rendu pour l'affichage dans le backend sont ainsi terminés.
Il reste ensuite à réaliser les réglages de rendu pour l'affichage dans le frontend.

La procédure est analogue à celle du « BE Liste » - dans les réglages de rendu, on
peut saisir par exemple « FE Liste » comme nom. De plus, l'affichage des libellés
des attributs est désactivé via la case à cocher « Masquer les libellés »
(voir la copie d'écran).

|img_rendersettings_04|

Pour l'affichage dans le frontend, tous les attributs nécessaires sont activés,
c'est-à-dire tous sauf l'attribut « Publié », qui est nécessaire pour le filtre
et qui ne doit pas, respectivement ne doit pas non plus, être affiché (voir la
copie d'écran).

|img_rendersettings_05|

Les préparatifs pour les listes du backend et du frontend sont ainsi achevés et
la vue d'ensemble des réglages de rendu devrait maintenant afficher les deux listes
(voir la copie d'écran).

|img_rendersettings_06|


.. |svg_rendersettings_32| image:: /_img/icons_svg/rendersettings.svg
   :width: 32px
.. |img_rendersettings_32| image:: /_img/icons/rendersettings_32.png
.. |svg_rendersettings_22| image:: /_img/icons_svg/rendersettings.svg
   :width: 22px
.. |img_rendersettings| image:: /_img/icons/rendersettings.png
.. |svg_rendersetting_22| image:: /_img/icons_svg/rendersetting.svg
   :width: 22px
.. |img_rendersetting| image:: /_img/icons/rendersetting.png
.. |svg_rendersettings_add_22| image:: /_img/icons_svg/rendersettings_add.svg
   :width: 22px
.. |img_rendersettings_add| image:: /_img/icons/rendersettings_add.png
.. |img_new| image:: /_img/icons/new.gif
.. |img_edit| image:: /_img/icons/edit.gif

.. |img_rendersettings_01| image:: /_img/screenshots/metamodel_first/rendersettings_01.png
.. |img_rendersettings_02| image:: /_img/screenshots/metamodel_first/rendersettings_02.png
.. |img_rendersettings_03| image:: /_img/screenshots/metamodel_first/rendersettings_03.png
.. |img_rendersettings_04| image:: /_img/screenshots/metamodel_first/rendersettings_04.png
.. |img_rendersettings_05| image:: /_img/screenshots/metamodel_first/rendersettings_05.png
.. |img_rendersettings_06| image:: /_img/screenshots/metamodel_first/rendersettings_06.png
