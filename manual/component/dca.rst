.. _component_dca:

|svg_dca_32| |img_dca_32| Masques de saisie
=============================================

.. note:: créer des masques de saisie pour la saisie de données ;
  ajouter, activer et configurer les attributs ; définir en option
  une condition d'affichage du champ de saisie ; définition
  possible du groupement et du tri des Items enregistrés

Introduction
------------

Pour remplir la base de données depuis le backend, des masques de saisie sont nécessaires. Chaque
masque de saisie peut intégrer, comme éléments de saisie, les attributs définis pour chaque
MetaModel.

Pour chaque MetaModel, un ou plusieurs masques de saisie différents peuvent être créés, dotés de
différents champs de saisie d'attributs. Cela permet de couvrir différentes autorisations ou
différents workflows.

La création des masques de saisie se divise ici aussi en réglages de base du masque de saisie,
activation des attributs ainsi que sélection des options spécifiques de chaque attribut, comme par
ex. champ obligatoire, disposition, validation ou similaire. La plupart des options de réglage
reflètent les possibilités du « DCA » du « Contao Framework » (voir
`DCA <https://docs.contao.org/books/api/dca/index.html>`_). Pour en savoir plus sur les options,
voir le point « Déroulement ».

L'un des points les plus importants dans les réglages de base est le choix de l'option
« Intégration » avec les possibilités « Indépendant » ou « Table enfant ». Avec « Indépendant », le
masque de saisie est intégré dans l'un des blocs de navigation de Contao, et avec « Table enfant »,
il est associé à une table MetaModel ou Contao existante.

Lors du choix « Table enfant », il faut noter que le « Mode de rendu » doit être réglé sur « Élément
parent présent » si une association univoque des Items enfants à un Item parent doit avoir lieu.
Sinon, tous les Items enfants sont listés pour tous les Items parents.

L'affichage du champ de saisie peut être influencé par d'autres paramètres de contrôle. Chaque
réglage de rendu possède une icône d'édition permettant de créer des dépendances d'affichage ou de
visibilité (« conditions d'affichage »). Ainsi, un ou plusieurs champs de saisie du masque de saisie
peuvent n'être visibles que si, par ex., une case à cocher particulière est cochée.

Pour chaque masque de saisie, on peut définir un ou plusieurs groupements et tris pour une
présentation claire des Items enregistrés.

Si l'on souhaite afficher les Items de la vue en liste sous forme de structure arborescente ou
hiérarchique, deux réglages de base sont nécessaires :

* dans les propriétés du masque de saisie, régler le « Mode de rendu » sur « Hiérarchie »
  (affichage en tableau désactivé)
* dans le tri du masque de saisie, définir un tri par défaut avec « Activer le tri manuel »



Options du masque de saisie
------------------------------
* **Nom** : |br|
  désignation
* **Disposition du panneau** : |br|
  configuration des outils dans l'en-tête : recherche, tri, filtrage, limite ; pour la recherche et
  le filtrage des attributs, l'option correspondante doit être activée au niveau des widgets de
  saisie
* **Intégration** : |br|
  « Indépendant » avec sélection de la zone du backend ; « Comme table enfant » avec sélection de la
  table parente
* **Mode de rendu** : |br|
  mode de sortie de la liste sous forme « Un niveau (sans hiérarchie) » ou « Hiérarchie », ou, pour
  les tables enfants, également « Élément parent présent »
* **Affichage sous forme de tableau** : |br|
  option pour afficher les attributs sous forme de tableau
* **Autoriser l'édition/la création/la suppression** : |br|
  autorisation de modifier, créer, supprimer des saisies

Options du champ de saisie
------------------------------
* **Type** : |br|
  légende : subdivision du panneau de saisie (« ligne verte ») |br|
  attribut : affichage des options de l'attribut
* **Réglages liés à la fonction** : |br|
  activation de « lecture seule » ou « champ obligatoire » |br|
  d'autres options selon le type d'attribut, par ex. validation de la saisie, activation de
  TinyMCE, etc.
* **Options d'affichage** : |br|
  indication des classes CSS backend de Contao, par ex. « w50 » pour une largeur de 50 %
* **Liste, filtrage et tri dans le backend** : |br|
  cases à cocher Filtrable et/ou Consultable - selon le type d'attribut

Options des conditions d'affichage du widget de saisie
------------------------------------------------------------
* **Type** : |br|
  type des conditions d'affichage : ET/OU/NON pour la combinaison, ou dépendance par propriété
  vis-à-vis d'autres attributs
* **Attribut/Valeur** |br|
  sélection en cas de dépendance vis-à-vis d'un autre attribut

Options du groupement et du tri
-----------------------------------
* **Nom** : |br|
  désignation
* **Activer le tri manuel** : |br|
  si cette valeur est activée, les Items peuvent être triés manuellement ; si la case n'est pas
  cochée, les options suivantes peuvent être définies :
* **Attribut de groupement** : |br|
  sélection de l'attribut selon lequel le groupement doit s'effectuer
* **Longueur de groupement** : |br|
  le nombre de lettres utilisées pour le groupement (si le type de groupement est défini)
* **Type de groupement** : |br|
  type de groupement, par ex. par lettre initiale ou par période comme semaine, mois
* **Attribut de tri** : |br|
  sélection de l'attribut selon lequel le tri doit s'effectuer (le cas échéant au sein d'un
  groupement)
* **Sens du tri** : |br|
  sens du tri : croissant (ASC) ou décroissant (DESC)

L'affichage du groupement par semaine peut être personnalisé via une clé de langue. Avec
``$GLOBALS['TL_LANG']['MSC']['week_format'] = 'K\W W. Y';``, on obtient par ex. la sortie
``KW 43. 2023`` (le `formatage de date PHP <https://www.php.net/manual/de/datetime.format.php>`_
est utilisé ; le premier ``W`` est échappé avec un ``\`` afin d'être affiché tel quel plutôt que
d'être interprété comme formatage de date PHP).

Déroulement
-----------

Une nouvelle saisie pour le réglage du masque de saisie s'ouvre via « |img_new| Nouveau masque de
saisie ». Une fois toutes les options nécessaires renseignées ou sélectionnées, le réglage est
enregistré et apparaît dans la liste des masques de saisie existants d'un MetaModel.

À côté de l'icône « |img_edit| crayon » se trouve l'icône « |img_dca_setting| Réglages du masque de
saisie ». Un clic sur cette icône ouvre une liste des attributs activés pour le masque de saisie.
S'il n'y a pas d'attributs, ou si des attributs doivent être ajoutés, cela peut se faire via l'icône
« |img_dca_setting_add| Tout ajouter » - ou, alternativement, via « |img_new| Nouveau ». En passant
par « Tout ajouter », une double confirmation est nécessaire.

Les attributs du masque de saisie sont ensuite disponibles et doivent, le cas échéant, encore être
activés.

Pour chaque attribut, le template à utiliser peut être modifié et/ou une classe CSS particulière
peut être renseignée (« |img_edit| Éditer »).

Via « |img_dca_condition| Conditions d'affichage », la visibilité du widget de saisie dans le
masque de saisie peut être réglée.

Ensuite, dans la vue en liste des masques de saisie, différentes entrées pour le tri et le
groupement des Items enregistrés peuvent être créées via l'icône
« |img_dca_groupsortsettings| Tri et groupement ».

.. seealso:: Dans le livre de recettes :

   * :ref:`rst_cookbook_inputmask_dca`
   * :ref:`rst_cookbook_inputmask_default-values`
   * :ref:`rst_cookbook_inputmask_regex`


.. |svg_dca_32| image:: /_img/icons_svg/dca.svg
   :width: 32px
.. |img_dca_32| image:: /_img/icons/dca_32.png
.. |img_dca| image:: /_img/icons/dca.png
.. |img_dca_setting| image:: /_img/icons/dca_setting.png
.. |img_dca_setting_add| image:: /_img/icons/dca.png
.. |img_dca_groupsortsettings| image:: /_img/icons/dca_groupsortsettings.png
.. |img_dca_condition| image:: /_img/icons/dca_condition.png
.. |img_new| image:: /_img/icons/new.gif
.. |img_edit| image:: /_img/icons/edit.gif

.. |br| raw:: html

   <br />
