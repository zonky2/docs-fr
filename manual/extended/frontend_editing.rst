.. _rst_extended_frontend_editing:

Frontend-Editing (FEE)
=======================

.. note:: La prise en charge de certains attributs n'est disponible qu'à partir de MM 2.2.
   voir `Github <https://github.com/MetaModels/contao-frontend-editing/issues/15>`_.


L'extension Frontend-Editing (FEE) permet l'édition des données MetaModels en
frontend. Cela signifie que les visiteurs du site peuvent créer, modifier,
dupliquer et supprimer de nouveaux enregistrements.

En général, l'édition n'est pas rendue accessible à tous les visiteurs du site,
mais uniquement à un groupe d'utilisateurs déterminé. Pour cela, les modules
habituels de Contao pour la connexion et les droits d'accès sont utilisés.

Il est en outre possible d'attribuer des masques de saisie individuels aux groupes de
membres, afin par exemple de ne rendre modifiables que certains champs en frontend. Ces
attributions des autorisations d'édition se font actuellement exclusivement au niveau
des groupes de membres. De manière analogue au backend, les possibilités d'édition
peuvent être restreintes, de sorte que par exemple la suppression d'enregistrements ne
soit pas autorisée.

En frontend, les widgets de saisie sont affichés comme des champs de formulaire. Comme le
frontend n'est pas soumis à autant de restrictions que le backend (par ex. MooTools comme
framework JavaScript), l'affichage des widgets, y compris les pickers associés comme la
date, la couleur ou l'éditeur de texte enrichi, n'est pas directement du ressort du FEE.
Pour les widgets concernés, des classes CSS sont affichées, permettant d'intégrer
différents widgets via JavaScript.

Avec MM 2.2, pratiquement tous les attributs (unilingues) sont en principe disponibles
pour une édition en frontend. Les attributs pouvant être utilisés dans le FEE figurent
dans la :ref:`liste des attributs <component_data-in-attributes>`.

Les types de modèle suivants ne sont actuellement pas encore pris en charge :

* Modèle avec variantes (`#20 <https://github.com/MetaModels/contao-frontend-editing/issues/20>`_)
* Tables enfants (`#19 <https://github.com/MetaModels/contao-frontend-editing/issues/19>`_)
* Modèle avec hiérarchie (`#18 <https://github.com/MetaModels/contao-frontend-editing/issues/18>`_)

La première implémentation du Frontend-Editing a été financée via un
`financement participatif <https://now.metamodel.me/de/unterstuetzer/fundraising#frontend-editing>`_.
Pour le développement futur, la correction de bugs et les nouvelles fonctions, la
collaboration au projet ainsi que le
`soutien financier <https://now.metamodel.me/de/unterstuetzer/spenden>`_ sont importants !


.. _rst_extended_frontend_editing_installation:
Installation
------------

Le FEE s'installe via le Contao-Manager ou Composer.

FEE-Core : :code:`"metamodels/contao-frontend-editing"` |br|
(:code:`"contao-community-alliance/dc-general-contao-frontend"` est généralement intégré automatiquement)

.. note:: Les prises en charge suivantes sont disponibles à partir de MM 2.2 :

Widget MCW : :code:`"contao-community-alliance/contao-multicolumnwizard-frontend-bundle"` |br|
Widgets avec deux éléments de saisie comme par ex. URL : :code:`"contao-community-alliance/contao-textfield-multiple-bundle"` |br|
Upload de fichier avec Dropzone et miniatures : :code:`"metamodels/dropzone_file_upload"` |br|


Configuration dans le backend
-------------------------------

Dans la description suivante, on part du principe qu'un MetaModel, par ex. "Liste des
employés", a déjà été configuré. Seules les modifications apportées à ce MetaModel ou
aux réglages des modules sont donc présentées.

Pour la structure de l'exemple, il existe deux pages dans Contao :

* une page de liste sur laquelle une liste de tous les employés sera visible
* une page de détail sur laquelle l'édition d'un enregistrement employé a lieu

|img_seitenstruktur|

Sur la page de liste, on insère un élément de contenu de type "Metamodel List". Celui-ci a
été configuré conformément au :ref:`guide <component_contentelements>`
- avec deux ajouts que permet la nouvelle extension :

* activer l'édition en frontend
* sélectionner une page d'édition
* changer le template pour `ce_metamodel_frontend_edit`

|img_metamodellist|

|img_metamodellistedit|

La page de liste avec les liens d'édition devrait être exclue de l'indexation Contao, afin
que le robot d'indexation ne suive pas les liens d'édition - notamment si l'option
"Autoriser la suppression" est activée pour ce masque de saisie.

.. note:: Dans MM 2.3, les liens d'édition possèdent les attributs HTML `data-escargot-ignore rel="nofollow"`,
   afin que le robot d'indexation Contao ne suive pas les liens.

Sur la page de détail, on insère un nouvel élément de contenu "Metamodels Frontend Editing".

|img_metamodelfee|

Dans celui-ci, on sélectionne le MetaModel qui doit être édité.

|img_metamodelfeeedit|

Comme dernière étape, le masque de saisie configuré pour le backend doit encore être
activé pour le frontend. Pour cela, on ouvre dans le backend la page des "Associations de
saisie/rendu" |svg_dca_combine_22| |img_dca_combine| et on sélectionne dans la colonne
"Groupe de membres" une entrée appropriée pour les droits en frontend - veuillez consulter
les :ref:`explications relatives aux réglages <component_dca-combine>`.


|img_fee-dca-zuordnung|

Les réglages dans le backend sont ainsi terminés et l'on peut désormais vérifier en
frontend les réglages, respectivement l'édition des employés.

.. warning:: L'association à un groupe de membres ne protège pas automatiquement les
   données contre l'édition par d'autres membres.


Travailler en frontend
------------------------

Dans la liste du MetaModel, deux nouvelles possibilités sont désormais disponibles :

* ajouter un enregistrement et
* éditer un enregistrement.

Pour l'affichage du lien "Ajouter un enregistrement", le template `ce_metamodel_list_edit.html5`
doit être sélectionné dans le CE/module frontend Liste MM - les liens "Éditer
l'enregistrement" sont ajoutés via le template standard de la liste dans le bloc "action".

|img_liste|

Le masque de création d'un nouvel enregistrement contient par défaut tous les champs du
MetaModel. Après l'enregistrement, on a une entrée de plus dans la liste.

|img_newfile|

Lors de l'édition de l'enregistrement, on peut modifier tous les champs du MetaModel.
"Enregistrer" ramène à la liste.

|img_editfile|


Configuration de masques de saisie différents pour BE/FE
-------------------------------------------------------------

Si l'on souhaite ne rendre disponibles que certains champs pour l'édition en FE, un
masque de saisie séparé doit être créé pour cela.

La création du masque de saisie se fait de manière analogue au masque du backend. La
sélection, respectivement l'activation des attributs définit les champs de formulaire
pour l'édition.

Le masque de saisie peut désormais être sélectionné pour le FE via les "Associations de
saisie/rendu" |svg_dca_combine_22| |img_dca_combine|.

|img_fee-dca-zuordnung2|

L'ordre du réglage d'association est important, car celui-ci est traité "de haut en bas".
Ainsi, par exemple, le masque de saisie défini dans le backend pour le groupe
d'utilisateurs "Administrator" est trouvé en premier et affiché en conséquence. Pour le
groupe de membres "general Members", le masque "FEE Eingabe" est trouvé et affiché en
premier.

L'entrée "*" (jusqu'à MM 2.1 "-") pour les groupes est un "catch all", c.-à-d. que cette
entrée s'applique à tous les groupes, dans la mesure où aucune entrée n'a déjà été prise
en compte auparavant dans le traitement.

Il existe parfois des constellations dans lesquelles on souhaite "sauter" une ligne lors
du traitement dans une colonne - par ex. pour ne pas avoir de "catch all *" sur la première
ligne pour le groupe de membres. Pour cela, on peut créer un groupe auquel aucun
utilisateur/membre n'est attribué - par ex. "Anonymous" ou "empty".

Si aucun réglage approprié pour le masque de saisie ne peut être trouvé pour le visiteur
FE du site, par ex. parce que la page n'est protégée par aucune connexion ou que le groupe
de membres n'a pas été défini dans les associations, une exception est émise :
"Definition basic is not registered in the configuration mm_xyz".

L'émission de cette exception peut être évitée en sélectionnant, comme dernière
configuration pour le groupe de membres, le "catch-all" (*) ainsi qu'un masque de saisie
"vide" sans autorisation de création ni d'édition. Une erreur 403 est alors émise, qui
peut être interceptée par une page correspondante dans Contao.


.. _extended_frontend_editing_headlines:
Adaptation du titre
---------------------

.. note:: Cette fonctionnalité est disponible à partir de MM 2.3.

Lorsqu'un enregistrement est édité en FE, le titre est "Édition de l'enregistrement <ID>".
Il n'apparaît pas très clairement pour les membres éditeurs, sur la base de l'indication de
l'ID, quel enregistrement ils sont en train d'éditer. Pour une identification plus claire,
il est possible, dans les réglages du masque de saisie, de générer un texte correspondant
à partir des données de l'item et de l'afficher à la place de l'ID.

Dans le champ de texte, les valeurs de l'item peuvent être transmises sous forme de
"Simple Tokens" comme par ex. ``##model_name##``.

L'adaptation de l'affichage est également possible dans le BE.

Réglage dans le BE : |br|
|img_fee-own-headline|

Affichage dans le FE : |br|
|img_fee-own-headline2|


.. _extended_frontend_editing_multilanguage:
Multilinguisme
----------------

.. note:: Cette fonctionnalité est disponible à partir de MM 2.4.

Pour les MetaModels multilingues, un sélecteur de langue comme dans le backend est
affiché dans le masque de saisie en frontend. On peut adapter le sélecteur de langue via
le template ``dcfe_general_edit`` - à partir de MM 2.5, au choix en ``.html5`` ou en
``.html.twig``. Il en va de même pour les widgets du masque de saisie :
``form_upload-on-steroids`` (fichiers), ``form_mcw`` (MultiColumnWizard) et
``form_text_multiple`` (champ texte multiple). Si les deux variantes existent, la version
Twig a la priorité ; un override ``.html5`` propre avec une priorité plus élevée conserve
la sienne.

.. important:: Quiconque écrit son propre template Twig pour un widget devrait, dans son
   bloc ``label``, n'afficher que le label lui-même. Si un champ porte un badge de langue
   (voir « Indications de langue dans le masque de saisie » plus bas), MetaModels étend le
   template et **remplace entièrement son bloc ``label``** - tout ce qui s'y trouve par
   ailleurs disparaît précisément pour ces champs. Les contenus tels que les listes de
   fichiers ou ``{% add … to stylesheets %}`` doivent donc être placés dans le bloc
   ``field`` ; cela ne change rien à l'ordre d'affichage, puisque Contao rend de toute
   façon le bloc ``label`` avant le bloc ``field``.

Il faut noter que, comme dans le backend, lors de la création d'un nouvel enregistrement,
la langue de repli doit toujours être remplie en premier - le masque de saisie bascule
automatiquement sur la langue correspondante.

Si l'on souhaite définir un "lien profond" (deeplink) pour une édition incluant la
sélection de la langue, on peut utiliser le paramètre GET ``__setlng`` avec le code de
langue correspondant, par ex.
``domain.com/en/fee-processing?act=edit&id=mm_employees_trans%::42&__setlng=de`` - le
paramètre est automatiquement supprimé après un rechargement.

**Indications de langue dans le masque de saisie** |br|
De manière analogue au backend, plusieurs indications concernant la langue d'édition
actuelle sont affichées dans le masque de saisie FE :

* Dans le **menu déroulant de sélection de langue**, la langue de repli est signalée par
  le complément ``[Fallback]``.
* Dans le **titre** (sub_headline), le nom de la langue actuellement éditée est affiché ;
  si l'on se trouve dans la langue de repli, un badge coloré ``[Fallback]`` apparaît en
  plus à cet endroit.
* Sur chaque **label de widget** d'un attribut traduit apparaît un badge coloré :

  * **[Fallback]** (orange) : la valeur provient de la langue de repli - il n'existe pas
    encore de traduction propre dans la langue actuelle.
  * **[Traduit]** (vert) : le champ possède une traduction propre dans la langue actuelle.

  La phrase explicative apparaît sous forme de tooltip sur le badge. Dans la langue de
  repli elle-même, il n'y a rien à signaler, aucun badge n'y apparaît.

|img_fee-multilanguage2|

Pour en savoir plus : :ref:`component_multi-language`.


Réglage des droits d'accès pour l'édition
---------------------------------------------

Dans la plupart des cas, l'édition des données ne doit pas être disponible pour tous les
visiteurs du site. La page de détail peut être protégée via les droits d'accès habituels
de Contao et l'édition rendue possible uniquement pour un ou plusieurs groupes de membres
autorisés.

Il faut tenir compte de l'interaction entre les droits d'accès et le masque de saisie
affiché. Si la page avec le masque de saisie est protégée, un masque de saisie doit
également être défini pour ce groupe de membres. Si ce n'est pas le cas, il s'agit d'une
mauvaise configuration qui entraîne une exception.


Gestion avancée des droits
-----------------------------

Avec les droits d'accès, on peut effectuer des autorisations générales du masque de
saisie sur la base des groupes de membres de Contao. Des autorisations plus individuelles,
comme par ex. "seuls les membres d'un groupe de membres peuvent éditer" (dans la mesure où
plusieurs groupes sont autorisés) ou chaque membre ne peut éditer que ses propres
enregistrements, peuvent être obtenues par des adaptations. Différents événements sont
disponibles à cet effet :

* `PreEditModelEvent <https://github.com/contao-community-alliance/dc-general/blob/a91084614d92875bf41427de0a1ed2ab28589917/src/Event/PreEditModelEvent.php>`_ :
  vérification des droits avant le chargement du masque de saisie
* `PrePersistModelEvent <https://github.com/contao-community-alliance/dc-general/blob/a91084614d92875bf41427de0a1ed2ab28589917/src/Event/PrePersistModelEvent.php>`_ :
  vérification des droits avant l'enregistrement d'un item
* `PreDuplicateModelEvent <https://github.com/contao-community-alliance/dc-general/blob/a91084614d92875bf41427de0a1ed2ab28589917/src/Event/PreDuplicateModelEvent.php>`_ :
  vérification des droits avant la duplication d'un item
* `PreDeleteModelEvent <https://github.com/contao-community-alliance/dc-general/blob/a91084614d92875bf41427de0a1ed2ab28589917/src/Event/PreDeleteModelEvent.php>`_ :
  vérification des droits avant la suppression d'un item

Pour l'enregistrement automatique de l'ID du membre ou de son groupe, le `PrePersistModelEvent <https://github.com/contao-community-alliance/dc-general/blob/a91084614d92875bf41427de0a1ed2ab28589917/src/Event/PrePersistModelEvent.php>`_
peut également être utilisé.

Il convient en outre de vérifier la connexion et le frontend. De plus, une page "Error-403"
devrait être créée pour le cas où les autorisations seraient insuffisantes.

.. note:: Cette fonctionnalité est disponible à partir de MM 2.3.

La vérification la plus fréquente, à savoir que chaque membre ne peut éditer que ses
propres enregistrements, est implémentée dans le FEE. Les éléments suivants sont
nécessaires pour cela :

* attribut Sélection unique [Select] avec une relation vers la table ``tl_member`` ainsi
  que le réglage de l'alias sur la colonne ``username``
* activer la vérification des droits dans le masque de saisie pour le FEE et y
  sélectionner l'attribut correspondant pour le membre - seuls les attributs de sélection
  unique disposant de la configuration adéquate sont affichés
* en option, la liste peut être filtrée sur les enregistrements du membre - pour cela,
  ajouter au filtre de la liste la règle de filtre "Member permissions" et y sélectionner
  également l'attribut correspondant pour le membre - si aucun filtrage n'est mis en
  place, les liens d'action pour l'édition ne sont affichés que pour les items appropriés

Masque de saisie : |br|
|img_fee-rights-at-inputmask|

Règle de filtre : |br|
|img_fee-member-filterrule|


Boutons individuels dans le masque FE
-----------------------------------------

.. note:: Cette fonctionnalité est disponible à partir de MM 2.2.

Via la configuration du masque de saisie, l'affichage et le fonctionnement des boutons
affichés en FE peuvent être configurés. Par défaut, "Enregistrer" et "Enregistrer et
nouveau" sont affichés comme boutons.

Avec la configuration, aussi bien le libellé du bouton que l'action peuvent être modifiés.
Ainsi, par exemple, "Enregistrer et retour", "Enregistrer et nouveau" ou encore
"Enregistrer" avec une redirection vers une "page de remerciement", de manière similaire
au générateur de formulaires, sont possibles.
La modification du libellé du bouton ne peut actuellement pas se faire directement dans
le backend. Celui-ci peut soit rester vide, soit être rempli avec MSC.'name'. La
traduction se fait via une entrée dans le fichier de langue correspondant du MetaModel,
par ex. contao/languages/fr/mm_table.php. |br|
Si l'entrée est vide, elle sera par ex. : ``$GLOBALS['TL_LANG']['mm_table']['MSC']['closeNback'] = 'Abbrechen'``; |br|
Si elle est définie avec MSC.'name', elle sera par ex. : ``$GLOBALS['TL_LANG']['MSC']['closeNback'] = 'Abbrechen'``; |br|

|img_fee-eigene-buttons|

Si un bouton est défini avec la case à cocher "Not save", aucun enregistrement des
données n'a lieu. On peut ainsi définir par ex. un bouton "Annuler" ou "Retour". La
validation HTML5 des champs obligatoires est contournée par JavaScript lors d'un clic sur
un tel bouton.

Dans le champ Paramètre, on peut accéder aux valeurs de l'enregistrement et les remplacer
par des "Simple Tokens". On peut ainsi injecter des valeurs dynamiques dans l'URL. La
structure des tokens est ``##model_<nom-de-propriété>##``. Le préfixe "model_" a été
ajouté afin d'avoir la possibilité d'intégrer également d'autres données, comme celles de
l'utilisateur. L'intégration peut se faire sous forme de paramètres GET ou slug
classiques :

* GET : la valeur doit alors commencer par ``?``, par ex. ``?act=edit&id=mm_test::##model_pid##``
  donne l'URL ``domain.tdl/liste.html?act=edit&id=mm_test::3``
* Slug : tout doit être relié par ``/``, par ex. ``pid/##model_pid##`` donne l'URL
  ``domain.tdl/liste/pid/3.html``

.. note:: Les prises en charge suivantes sont disponibles à partir de MM 2.3 :

Dans le champ Paramètre, un inserttag peut également être saisi - d'autres adaptations
dynamiques sont ainsi possibles.


|img_fee-simple-tokens|


Notifications via le Notification Center
-------------------------------------------

.. note:: Cette fonctionnalité est disponible à partir de MM 2.2 - à partir de MM 2.3, le NC 2.x est pris en charge.

Si l'extension `Notification Center <https://github.com/terminal42/contao-notification_center>`_ (NC)
est installée, il est possible de déclencher une réaction à la modification d'un
enregistrement et de créer une "notification" via le NC - par ex. l'envoi d'un e-mail.

Les déclencheurs (triggers) suivants sont disponibles :

* Création
* Modification
* Copie
* Suppression

Dans le NC, un type de notification est disponible pour chaque déclencheur, sous le
groupe "MetaModels frontendenditing". Pour une nouvelle notification, une notification
doit d'abord être créée pour le déclencheur souhaité.

Pour les informations de la notification, il existe des "Simple Tokens" propres avec les
pré-/postfix "##" comme :

* model_* - toutes les valeurs d'attributs saisies
* model_original_* - toutes les valeurs d'attributs précédemment enregistrées (uniquement
  pour Modification et Copie)
* member_* - toutes les données du membre, s'il est connecté
* property_label_* - toutes les désignations des attributs
* data - toutes les données
* admin_email - e-mail issu de la configuration Contao

par ex. ##model_name## le contenu de l'attribut "name".

Si une notification a été créée pour un ou plusieurs types de déclencheur, celle-ci peut
être sélectionnée dans les réglages du masque de saisie.


.. _extended_frontend_editing_upload:
Téléchargement de fichiers - Dropzone en option
----------------------------------------------------

Dans le masque de saisie en FE, aucun picker pour la gestion des fichiers n'est
implémenté, car la transmission des données du BE vers le FE, y compris les différentes
autorisations, est très complexe et les fichiers éventuels devraient également d'abord
être intégrés dans la gestion des fichiers.

Pour le masque de saisie en FE, il existe cependant la possibilité de procéder à un
téléchargement de fichiers. Pour le téléchargement, différentes options de manipulation
du chemin cible, du nom de fichier et de l'affichage après le téléchargement en FE sont
disponibles.

Le téléchargement peut se faire via le widget de téléchargement standard ou par
glisser-déposer via `Dropzone <https://www.dropzone.dev/>`_.

Pour le téléchargement, l'attribut correspondant du type :ref:`Fichier <component_attribute_file>`
(ou :ref:`Fichier traduit <component_attribute_translatedfile>`) doit être intégré dans le
masque et défini comme "mode Widget" sur "Téléchargement de fichier unique", "Téléchargement
de fichiers multiples avec affichage des vignettes de prévisualisation", "Téléchargement de
fichiers multiples" et "Téléchargement de fichiers multiples avec affichage des vignettes
de prévisualisation".

|img_fee-upload|

Les réglages suivants sont disponibles :

* "Répertoire home" - répertoire cible pour les membres connectés ; le repli est la
  sélection sous "Dossier cible"
* "Dossier cible" - stockage des fichiers ; le cas échéant, repli pour "Répertoire home"
* "Normaliser le dossier" / "Normaliser le nom de fichier" - les chaînes correspondantes
  sont normalisées comme des alias
* "Étendre le dossier" / "Préfixe/postfixe du nom de fichier" - adaptation des chaînes ;
  utilisation d'inserttags possible |sup*|
* "Désélectionner le fichier" - permet de retirer l'enregistrement du fichier dans
  l'enregistrement MM
* "Supprimer le fichier" - le fichier est alors supprimé du serveur et retiré de
  l'enregistrement MM
* "Largeur et hauteur des vignettes de prévisualisation" - taille de sortie des vignettes
  en mode "avec affichage des vignettes de prévisualisation"
* "Dropzone" - réglages de `Dropzone <https://www.dropzone.dev/>`_

.. note:: |sup*| À partir de MM 2.3, la résolution des inserttags ne se fait plus via la
   règle de filtre "SQL personnalisé", mais via la résolution standard de Contao ; on peut
   accéder à d'autres données du masque de saisie avec ``{{post::<nom-de-colonne-attribut>}}``

.. note:: |sup*| À partir de MM 2.4, l'inserttag ``{{post::<...>}}`` n'existe plus - on peut
   désormais accéder aux données POST avec un Simple Token
   ``##post::<nom-de-colonne-attribut>##`` par ex. ``##post::lastname##`` - les inserttags
   (propres) continuent cependant également à être résolus

L'affichage dans le masque FE peut par exemple se présenter comme suit :

|img_fee-upload2|


.. |img_paketverwaltung| image:: /_img/screenshots/extended/frontend_editing/fee-paketverwaltung.png
.. |img_paket| image:: /_img/screenshots/extended/frontend_editing/fee-feepaket.png
.. |img_paketzwei| image:: /_img/screenshots/extended/frontend_editing/fee-feepaket2.png
.. |img_paketvormerken| image:: /_img/screenshots/extended/frontend_editing/fee-feepaketvormerken.png
.. |img_paketaktualisieren| image:: /_img/screenshots/extended/frontend_editing/fee-feepaketaktualisieren.png

.. |img_seitenstruktur| image:: /_img/screenshots/extended/frontend_editing/fee-seitenstruktur.png
.. |img_metamodellist| image:: /_img/screenshots/extended/frontend_editing/fee-metamodellist.png
.. |img_metamodellistedit| image:: /_img/screenshots/extended/frontend_editing/fee-metamodellistedit.png
.. |img_metamodelfee| image:: /_img/screenshots/extended/frontend_editing/fee-metamodelfee.png
.. |img_metamodelfeeedit| image:: /_img/screenshots/extended/frontend_editing/fee-metamodelfeeedit.png

.. |img_login| image:: /_img/screenshots/extended/frontend_editing/fee-login.png
.. |img_liste| image:: /_img/screenshots/extended/frontend_editing/fee-liste.png
   :width: 700px

.. |img_newfile| image:: /_img/screenshots/extended/frontend_editing/fee-newfile.png
   :width: 300px

.. |img_editfile| image:: /_img/screenshots/extended/frontend_editing/fee-editfile.png
   :width: 300px

.. |img_fee-dca-zuordnung| image:: /_img/screenshots/extended/frontend_editing/fee-dca-zuordnung.png
.. |img_fee-dca-zuordnung2| image:: /_img/screenshots/extended/frontend_editing/fee-dca-zuordnung2.png

.. |svg_dca_combine_22| image:: /_img/icons_svg/dca_combine.svg
   :width: 22px
.. |img_dca_combine| image:: /_img/icons/dca_combine.png

.. |img_fee-own-headline| image:: /_img/screenshots/extended/frontend_editing/fee-own-headline.png
.. |img_fee-own-headline2| image:: /_img/screenshots/extended/frontend_editing/fee-own-headline2.png

.. |img_fee-multilanguage| image:: /_img/screenshots/extended/frontend_editing/fee-multilanguage.png
.. |img_fee-multilanguage2| image:: /_img/screenshots/extended/frontend_editing/fee-multilanguage2.png

.. |img_fee-rights-at-inputmask| image:: /_img/screenshots/extended/frontend_editing/fee-rights-at-inputmask.png
.. |img_fee-member-filterrule| image:: /_img/screenshots/extended/frontend_editing/fee-member-filterrule.png

.. |img_fee-eigene-buttons| image:: /_img/screenshots/extended/frontend_editing/fee-eigene-buttons.png
.. |img_fee-simple-tokens| image:: /_img/screenshots/extended/frontend_editing/fee-simple-tokens.png

.. |img_fee-upload| image:: /_img/screenshots/extended/frontend_editing/fee-upload.png
.. |img_fee-upload2| image:: /_img/screenshots/extended/frontend_editing/fee-upload2.png

.. |br| raw:: html

   <br />

.. |sup*| raw:: html

   <sup><strong>*</strong></sup>
