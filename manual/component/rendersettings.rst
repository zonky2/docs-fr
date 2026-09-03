.. _component_rendersettings:

|svg_rendersettings_32| |img_rendersettings_32| Réglages de rendu
=====================================================================

.. note:: créer des vues en liste pour le backend et le frontend ;
  ajouter et activer des attributs

Introduction
------------

Les « réglages de rendu » permettent de définir les paramètres de base pour la liste ou
l'affichage des enregistrements à saisir ou à afficher, aussi bien pour le backend que pour le
frontend - séparément dans chaque cas. Les enregistrements individuels stockés dans un MetaModel
sont également appelés « Items ».

Dans le backend, les Items doivent être listés pour permettre leur saisie ou leur modification, et
dans le frontend pour un affichage ou une sortie. Même si divers aspects diffèrent entre le
backend et le frontend, de nombreux points restent néanmoins similaires, de sorte que les réglages
sont regroupés dans le composant « Réglages de rendu ».

Pour le backend, chaque MetaModel a besoin d'un réglage de rendu, car c'est uniquement via celui-ci
qu'un masque de saisie peut être appelé pour la saisie et la modification des données.

Pour le frontend, des réglages de rendu ne doivent être créés que pour les MetaModels dont les
Items doivent également être listés ou affichés en tant que tels. Les MetaModels reliés à un autre
MetaModel via une relation (attribut « Sélection » ou « Sélection multiple ») n'ont donc pas
nécessairement besoin d'un réglage de rendu pour le frontend.

Outre les différentes exigences pour le backend et le frontend, les réglages de rendu permettent
également de couvrir d'autres besoins. Pour chaque MetaModel, un grand nombre de réglages de rendu
différents peuvent être créés, par exemple pour générer des sorties différenciées. Ainsi, un
réglage de rendu pourrait produire une liste avec des informations de base, et un autre réglage de
rendu une sortie détaillée (une sortie détaillée est « une liste avec un seul Item »). En outre,
l'accès à certains réglages de rendu peut être accordé à des groupes d'utilisateurs et/ou de
membres via :ref:`component_dca-combine`.

Une fois qu'un réglage de rendu est créé et que les réglages de base sont renseignés, il faut,
comme étape suivante, activer les attributs pour ce réglage. Pour en savoir plus, voir le point
« Déroulement ». Comme autre possibilité de réglage, un template individuel peut être sélectionné
pour chaque attribut d'un réglage de rendu (s'il a été créé au préalable), ainsi qu'une classe CSS
personnalisée, par ex. pour une mise en évidence dans le backend.

Options
-------

* **Nom** |br|
  le nom peut être choisi librement ; pour une meilleure distinction, les abréviations « BE » et
  « FE » pour backend et frontend sont souvent placées avant le nom, par ex. « BE Liste »,
  « BE Saisie » ou « FE Liste complète »
* **Template** |br|
  ici, un template est sélectionné, dans lequel tous les Items sont affichés en boucle ; le
  template peut être facilement surchargé de la manière habituelle sous Contao ; il faut
  simplement noter que les templates pour le backend ne doivent pas être créés dans un
  sous-dossier de templates ; tous les attributs sont transmis au template dans le type « raw »,
  et seuls les attributs actifs sont transmis dans les types « html » et « text »
* **Format de sortie** |br|
  les choix possibles sont HTML5 et Texte ; en l'absence d'exigences particulières, la sélection
  peut rester vide ; le format XHTML n'est plus pris en charge depuis MM 2.2
* **Page de redirection** |br|
  la page de redirection avec sélection de page et filtre n'est utilisée que pour la sortie
  frontend, par ex. pour créer un lien vers une page de détail ; la page de détail devrait
  contenir un élément de liste avec un filtre correspondant ; pour les MetaModels multilingues, il
  existe un réglage de sélection de page et de filtre par langue
* **Masquer les entrées vides** |br|
  les entrées vides des attributs sont ignorées - important en combinaison avec l'affichage des
  labels des attributs
* **Masquer les labels** |br|
  les noms des attributs ne sont pas affichés en tant que « label »
* **Rendre les attributs uniquement à la demande [Lazy] (à partir de MM 2.5)** |br|
  un attribut n'est rendu que lorsque le template y accède réellement, au lieu de générer
  immédiatement, comme auparavant, les deux formats de sortie (HTML5 et Texte) pour chaque
  attribut ; cela est intéressant lorsqu'un template n'utilise qu'une partie des attributs ou
  n'utilise systématiquement qu'un seul format de sortie - si un template accède en revanche à
  tous les attributs dans les deux formats, l'option n'apporte aucun avantage et peut représenter
  un léger surcoût ; désactivée par défaut, elle est sélectionnable pour chaque réglage de rendu en
  fonction du template utilisé
* **Wrapper dans le template de liste [ancien comportement, déprécié] (à partir de MM 2.5)** |br|
  affiche le bloc englobant (champ, label, valeur) dans le template de liste comme jusqu'à MM 2.4,
  au lieu de le faire - comme c'est l'usage à partir de la 2.5 - dans les templates d'attribut
  eux-mêmes ; activé automatiquement lors de la mise à niveau pour les réglages de rendu existants,
  afin que rien ne change dans la sortie ; les réglages de rendu nouvellement créés démarrent sans
  cette option ; marquée dès le départ comme ancien comportement, elle disparaît dans
  MetaModels 3.0 - modèle et exemple pour des templates d'attribut personnalisés sous
  :ref:`component_templates_attribute-wrapper`
* **Fichiers CSS/Javascript supplémentaires** |br|
  pour la mise en forme de la sortie et l'interaction, des fichiers CSS et/ou Javascript peuvent
  être affichés avec la liste ; leur intégration ne se fait toutefois que si au moins un Item est
  affiché dans la liste


Déroulement
-----------

Une nouvelle saisie pour le réglage de rendu s'ouvre via « |img_new| Nouveau ». Une fois toutes les
options nécessaires renseignées ou sélectionnées, le réglage est enregistré et apparaît dans la
liste des réglages de rendu existants d'un MetaModel.

À côté de l'icône « |img_edit| crayon » se trouve l'icône « |img_rendersetting| Réglages de rendu
des attributs ». Un clic sur cette icône ouvre une liste des attributs activés pour le réglage de
rendu. S'il n'y a pas d'attributs, ou si des attributs doivent être ajoutés, cela peut se faire via
l'icône « |img_rendersettings_add| Tout ajouter » - ou, alternativement, via « |img_new| Nouveau ».
En passant par « Tout ajouter », une double confirmation est nécessaire.

Les attributs du réglage de rendu sont ensuite disponibles et doivent, le cas échéant, encore être
activés - seuls doivent être activés ceux qui doivent être affichés dans la vue en liste.

Pour chaque attribut, le template à utiliser peut être modifié et/ou une classe CSS particulière
peut être renseignée (« |img_edit| Éditer »).


Indications sur « Rendre les attributs uniquement à la demande [Lazy] » (à partir de MM 2.5)
-----------------------------------------------------------------------------------------------

Sans cette option, MetaModels rend, lors de la construction d'une liste, **les deux** formats de
sortie pour **chaque** attribut activé - aussi bien le format demandé (généralement HTML5) que la
valeur texte - indépendamment du fait que le template de liste affiche finalement l'un des deux,
les deux, ou aucun des deux. Avec un grand nombre d'attributs et d'enregistrements, cela coûte un
temps sensible, consacré à des valeurs jamais utilisées.

Si l'option est activée, le template reçoit à la place, pour chaque format, un espace réservé
propre, qui ne rend réellement un attribut que lorsque le template y accède concrètement - et ce,
indépendamment pour chaque format : si le template n'accède qu'à ``html5``, ``text`` n'est même pas
calculé pour cet attribut, et inversement. Pour les auteurs de templates, l'utilisation ne change
pas : l'accès à ``html5``, ``text``, ``raw`` et ``attributes`` fonctionne comme d'habitude.

**Quand cela vaut-il le coup :** cette option est utile chaque fois qu'un template n'accède pas de
toute façon à tous les attributs activés dans les deux formats - par ex. parce que seule une
partie des attributs est réellement affichée, ou parce que le template n'utilise systématiquement
qu'un seul format (par ex. uniquement ``text`` pour un index de recherche, ou uniquement ``html5``
pour la sortie visible). Si un template accède en revanche de toute façon à tous les attributs
dans les deux formats, Lazy n'apporte aucun avantage et peut même être légèrement plus lent en
raison de l'accès général un peu plus coûteux. Il n'y a donc pas de comportement fondamentalement
« meilleur » - c'est pourquoi l'option doit être activée ou désactivée pour chaque réglage de rendu
en fonction du template utilisé, et le réglage par défaut est désactivé aussi bien pour les
nouveaux réglages de rendu que pour les réglages existants.

**Valeurs mesurées :** à titre indicatif, plusieurs scénarios ont été mesurés sur une page de test
réelle avec 13 et 208 Items respectivement et 25 attributs configurés (temps CPU pur plutôt que
temps réel, afin d'exclure la charge système de la machine de mesure ; chaque mesure reproduite
plusieurs fois) :

=================================================  ===================  ===================
Scénario                                           13 Items             208 Items
=================================================  ===================  ===================
Tous les attributs, deux formats utilisés          aucune différence    aucune différence
Tous les attributs, seul HTML5 utilisé             14-20 % plus rapide  10-11 % plus rapide
Tous les attributs, seul Texte utilisé             63-69 % plus rapide  70-71 % plus rapide
Seuls 3 attributs sur 25 utilisés                  37-45 % plus rapide  36-43 % plus rapide
=================================================  ===================  ===================

L'effet est le plus important en cas d'utilisation exclusive du texte, car le rendu HTML5 demande,
par attribut, sensiblement plus d'effort que la simple sortie texte - s'il est entièrement
contourné grâce à Lazy, cela pèse d'autant plus lourd.


.. seealso:: :ref:`rst_cookbook_rendering_encrypt-email`


.. |svg_rendersettings_32| image:: /_img/icons_svg/rendersettings.svg
   :width: 32px
.. |img_rendersettings_32| image:: /_img/icons/rendersettings_32.png
.. |img_rendersettings| image:: /_img/icons/rendersettings.png
.. |img_rendersetting| image:: /_img/icons/rendersetting.png
.. |img_rendersettings_add| image:: /_img/icons/rendersettings_add.png
.. |img_new| image:: /_img/icons/new.gif
.. |img_edit| image:: /_img/icons/edit.gif

.. |br| raw:: html

   <br />
