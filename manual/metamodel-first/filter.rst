.. _mm_first_filter:

|svg_filter_32| |img_filter_32| Jeux de filtres
==================================================

L'étape « Jeux de filtres » fait partie des composants optionnels et contrôle
différents paramètres de l'affichage. Dans notre exemple, un filtre doit être créé
qui, pour l'affichage en frontend, n'affiche que les entrées dont l'attribut
« Publié » est activé.

Pour accéder aux filtres, on active de nouveau la vue d'ensemble des MetaModels,
de sorte que l'entrée « Liste des employés » soit visible. On clique alors sur
l'icône « |svg_filter_22| |img_filter| Filtre » et la vue bascule sur la vue
d'ensemble des filtres - celle-ci est encore vide pour l'instant.

Après un clic sur « |img_new| Nouveau », le masque de création d'un filtre
s'ouvre immédiatement. Seule une désignation pour le filtre est saisie dans le
champ « Nom » - par exemple « Publié » (voir la copie d'écran).

|img_filter_01|

Dans la vue d'ensemble des filtres, la première entrée « Publié » devrait
maintenant être visible - voir la copie d'écran.

|img_filter_02|

En cliquant sur l'icône « |svg_filter_setting_22| |img_filter_setting| Attributs »,
le niveau suivant s'ouvre pour les attributs de filtrage. C'est à cet endroit que le
filtre est configuré avec ses attributs de filtrage. Les attributs de filtrage
peuvent être combinés et imbriqués de différentes manières. Pour cet exemple, un
seul attribut de filtrage est ajouté au filtre, en cliquant sur l'icône
« |img_new| Nouveau » dans l'en-tête.

Après le clic, seule l'icône de pochette |img_pasteinto| est visible dans un
premier temps - un clic sur cette icône ouvre le masque de configuration.

Pour filtrer le statut de publication, il existe sous « Type » un filtre spécial
qui est sélectionné. Comme attribut, on sélectionne « Publié »
(voir la copie d'écran).

|img_filter_03|

Après un clic sur « Activé » puis « Enregistrer et fermer », l'attribut de
filtrage est terminé et la vue de liste suivante devrait apparaître
(voir la copie d'écran).

|img_filter_04|

Le filtre est ainsi défini et peut être activé dans différents composants.


.. |svg_filter_32| image:: /_img/icons_svg/filter.svg
   :width: 32px
.. |img_filter_32| image:: /_img/icons/filter_32.png
.. |svg_filter_22| image:: /_img/icons_svg/filter.svg
   :width: 22px
.. |img_filter| image:: /_img/icons/filter.png
.. |svg_filter_setting_22| image:: /_img/icons_svg/filter_setting.svg
   :width: 22px
.. |img_filter_setting| image:: /_img/icons/filter_setting.png
.. |img_new| image:: /_img/icons/new.gif
.. |img_about| image:: /_img/icons/about.png
.. |img_help| image:: /_img/icons/help.svg
.. |img_pasteinto| image:: /_img/icons/pasteinto.gif

.. |img_filter_01| image:: /_img/screenshots/metamodel_first/filter_01.png
.. |img_filter_02| image:: /_img/screenshots/metamodel_first/filter_02.png
.. |img_filter_03| image:: /_img/screenshots/metamodel_first/filter_03.png
.. |img_filter_04| image:: /_img/screenshots/metamodel_first/filter_04.png
