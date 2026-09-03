.. _rst_extended_notelist:

Liste de favoris pour MetaModels
=================================

La liste de favoris (Notelist) étend MetaModels avec la possibilité, dans
la sortie FE, d'ajouter (add) des enregistrements (Items) individuels à une
liste de favoris.

Les usages possibles de la liste de favoris vont d'une "liste de favoris
classique" en passant par des listes de comparaison, p. ex. de caractéristiques
de produits, jusqu'à des fonctions de panier d'achat.

Si un enregistrement est enregistré dans une liste de favoris, il peut bien
entendu aussi en être retiré à nouveau (remove).

Avec la liste de favoris, une nouvelle règle de filtre est disponible, avec
laquelle une liste MetaModels peut être filtrée en fonction des enregistrements
présents dans une liste de favoris.

Pour le générateur de formulaires, un nouveau widget a été créé, qui permet
de lister les enregistrements de la liste de favoris et de les transmettre
dans l'e-mail - un envoi de l'e-mail via le Notification-Center est également
possible.

Dans chaque MetaModels, plusieurs listes de favoris peuvent être créées. Il
est ainsi possible, par exemple, d'inscrire un enregistrement dans deux
listes de favoris comme "Favoris" et "Commander" ou de transférer un
enregistrement d'une liste de favoris comme "Mettre de côté" vers une autre
liste de favoris "Commander".

Dans la configuration d'une liste de favoris, un filtre peut être défini de
sorte que seuls certains enregistrements puissent être ajoutés à la liste
de favoris - p. ex. uniquement les collaborateurs du département "Ventes".

La liste de favoris fonctionne également avec des MetaModels traduits, de
sorte que les enregistrements d'une liste de favoris sont conservés même
lors d'un changement de langue.


Installation via Contao-Manager ou Composer
--------------------------------------------

Conditions préalables pour l'installation :

**Contao 5.7 :**

.. note:: La liste de favoris est immédiatement opérationnelle mais n'est débloquée qu'une fois le
   montant de collecte de fonds actuel de 4 335 € atteint. |br|
   Pour un accès, merci d'envoyer un e-mail à info@e-spin.de

* ^PHP 8.4
* MetaModels 2.5
* Notelist 2.5
* Notification Center 2.3 ou NCPro (optionnel)
* Accès au dépôt protégé - données fournies après don

**Contao 5.3 :**

.. note:: La liste de favoris est immédiatement opérationnelle mais n'est débloquée qu'une fois le
   montant de collecte de fonds actuel de 4 335 € atteint. |br|
   Pour un accès, merci d'envoyer un e-mail à info@e-spin.de

* ^PHP 8.2
* MetaModels 2.4
* Notelist 2.4
* Notification Center 2.3 ou NCPro (optionnel)
* Accès au dépôt protégé - données fournies après don

**Contao 4.13 :**

* ^PHP 8.1
* MetaModels 2.3
* Notelist 2.3
* Notification Center 1.7 ou 2.3 (optionnel)


Créer une liste de favoris
---------------------------

Après l'installation réussie de la liste de favoris, une nouvelle icône
apparaît dans la rangée des icônes MetaModels, qui permet de créer et
d'éditer les listes de favoris.

|img_notelist_icon|

Lorsqu'on crée une nouvelle liste de favoris, un nom peut lui être attribué.
Comme "adaptateur de stockage", la "session PHP" et la "session Contao"
sont actuellement disponibles. Avec la session Contao, les valeurs d'une
liste de favoris sont automatiquement enregistrées dans les valeurs de
session de la base de données pour les membres connectés et restent
disponibles lors d'une nouvelle connexion.

.. note:: Modification à partir de la version 2.4 (Contao 5.3) : dans Contao 5.3, la gestion des sessions
   a été remaniée, de sorte que seuls "Session Contao" ou des implémentations personnalisées sont
   disponibles comme adaptateur de stockage. Lorsqu'un membre est connecté au frontend, les données de la
   liste de favoris sont automatiquement enregistrées de façon persistante dans sa propre session Contao.
   Ces données sont également prioritaires lorsqu'un visiteur du site remplit la liste de favoris puis
   se connecte ensuite - après la connexion, les données des données de membre sont affichées.

Via la sélection de filtre, l'ajout peut être restreint aux enregistrements
possédant certaines propriétés, comme p. ex. le "département" ou les groupes
de membres. Le filtrage sur les groupes de membres est par exemple possible
via l'extension "`condition membergroup filter
<https://github.com/cboelter/metamodels-filter_condition_membergroup>`_".

|img_nodelist_config|

La vue en liste donne accès à toutes les listes de favoris créées.

|img_notelist_overview|


Activer la liste de favoris dans une liste MetaModels
-------------------------------------------------------

Dans le CE liste MetaModels resp. le module FE, il existe une nouvelle
section "Notelist" dans laquelle une ou plusieurs des listes de favoris
créées peuvent être activées.

|img_notelist_ce_mm-list|

L'ordre des "sorties d'action" peut être modifié via le tri par
glisser-déposer des listes de favoris.

Si le template standard est utilisé pour la sortie, aucune autre
modification n'est nécessaire et dans la vue en liste FE, les enregistrements
devraient présenter un lien supplémentaire pour l'ajout à la liste de favoris.

Si l'on utilise son propre template, une adaptation correspondante est
nécessaire pour les nouveaux liens. Les liens sont contenus dans le nœud
`action` et peuvent par exemple être générés avec le code suivant (le
chiffre correspond à l'ID de la liste de favoris) :

.. code-block:: html
   :linenos:

   <a href="<?= $arrItem['actions']['notelist_1_button']['href'] ?>" class="<?= $arrItem['actions']['notelist_1_button']['class'] ?>"><?= $arrItem['actions']['notelist_1_button']['label'] ?></a>

|img_notelist_fe_list|


Sortie de la liste de favoris via un filtre
---------------------------------------------

La sortie de la liste de favoris dans le FE se fait via une liste MetaModels
normale, qui est filtrée sur les éléments de la liste de favoris.

Pour le filtrage, un filtre avec la nouvelle règle de filtre "Notelist" doit
être créé. Dans la règle de filtre, il suffit de sélectionner la liste de
favoris dont les éléments doivent être affichés.

|img_notelist_filterrule|

Dans la sortie FE de la liste filtrée, on ne voit plus que les collaborateurs
de la liste de favoris.

|img_notelist_filtered_list|

Dans la sortie de la liste, il serait par exemple possible d'activer une
autre liste de favoris, afin de transférer les éléments d'une liste de
favoris vers une autre - p. ex. de "Mettre de côté" vers "Commander".

Dans les paramètres de la liste de favoris, un filtre peut être défini en
option pour l'ajout à une liste de favoris. Si p. ex. seuls les
collaborateurs appartenant aux ventes sont autorisés, la liste se présente
comme suit :

|img_notelist_fe_list_with_filter|


.. _rst_extended_notelist_show_at_form:
Affichage des données et récupération dans le formulaire
------------------------------------------------------------

Dans le générateur de formulaires, un nouveau widget "MetaModels Notelist"
est disponible. Ce widget contrôle à la fois l'affichage des enregistrements
d'une liste de favoris dans le formulaire et dans l'e-mail. Si plusieurs
listes de favoris ont été créées pour un MetaModel, plusieurs peuvent
également être affichées.

Les possibilités de configuration ont dû être intégrées dans les interfaces
possibles d'un widget Contao, de sorte que des sélections doivent être
effectuées à plusieurs endroits.

Dans la section "Paramètres du template", il existe un template respectivement
pour la sortie dans le formulaire (template de champ de formulaire) et dans
l'e-mail (template d'e-mail), qui entoure la liste de sortie comme "wrapper".
Dans les templates, toutes les listes de favoris sont affichées en boucle
avec la sortie du nom, et à l'intérieur tous les enregistrements (voir
section "Configuration des champs"). Il faut noter que le template pour le
formulaire ``form_metamodels_notelist.html5`` est encore un "ancien"
template - alors que pour l'e-mail, c'est déjà un template Twig
``email_metamodels_notelist.text.html.twig``.

Dans la section "Configuration des champs", on peut sélectionner quelle(s)
liste(s) de favoris doivent être affichées. Pour la sortie en liste dans le
formulaire comme dans l'e-mail, des réglages de rendu correspondants doivent
être créés, qui affichent les attributs souhaités. De plus, pour chaque
liste de favoris, la case à cocher "Vider la liste" permet de déterminer si
la liste doit être vidée après le traitement du formulaire.

|img_nodelist_form_widget|

Pour les réglages de rendu, il faut noter que pour la sortie dans un e-mail
standard du formulaire Contao, seul le format texte est pris en charge -
pour les sorties en tant qu'e-mail HTML, il est conseillé d'utiliser
l'extension `Notification-Center <https://github.com/terminal42/contao-notification_center>`_.
Comme modèle pour les réglages de rendu, l'extension met à disposition les
fichiers ``metamodel_prerendered_notelists_form.html5`` et
``metamodel_prerendered_notelists_form.text``.

Avec les templates, les données qui peuvent être ajoutées en supplément à
chaque enregistrement de la liste de favoris (Payload) sont également
affichées automatiquement. Cela est possible via un
:ref:`"mini" formulaire <rst_extended_notelist_additional_form>`
ou un :ref:`écouteur d'événement <rst_extended_notelist_additional_events>`.

Dans les templates de liste, outre les nœuds habituels ``raw`` et ``text``,
``notelists_names`` est également présent comme liste des noms des listes
de favoris.

Le payload est transmis via les nœuds ``notelists_payload_values`` et
``notelists_payload_labels``.

Voici à nouveau la hiérarchie des templates :

Sortie du formulaire sur le site web :

- ``form_metamodels_notelist.html5`` - wrapper du widget de formulaire avec sortie de toutes les listes
  de favoris, nom inclus
    - ``metamodel_prerendered.html5`` - template de liste issu des réglages de rendu sélectionnés ; sinon,
      sélectionner le template ``metamodel_prerendered_notelists_form.html5`` pour la sortie du payload

Sortie dans l'e-mail :

- ``email_metamodels_notelist.text.html.twig`` - wrapper pour l'e-mail avec sortie de toutes les listes de
  favoris, nom inclus
    - ``metamodel_prerendered.html5`` - template de liste issu des réglages de rendu sélectionnés ; sinon,
      sélectionner le template ``metamodel_prerendered_notelists_form.html5`` pour la sortie du payload

.. note:: Cette option est disponible à partir de MM 2.4 avec Contao 5.3

Pour la sortie en tant qu'e-mail HTML, il est conseillé d'utiliser l'extension
`Notification-Center <https://github.com/terminal42/contao-notification_center>`_.
Des `Simple-Tokens <https://docs.contao.org/5.x/manual/de/artikelverwaltung/simple-tokens/>`_
propres, commençant par "##mm::", sont disponibles à cet effet - il y a

- ``##mm::notelist_name::<id-notelist>##`` - sortie du titre de la NL pour l'ID sous forme de texte
- ``##mm::notelist::<id-notelist>::<id-rendersetting>##`` - sortie des items de la NL pour l'ID avec l'ID
  du réglage de rendu sous forme de texte
- ``##mm::notelist::<id-notelist>::<id-rendersetting>::html##`` - sortie des items de la NL pour l'ID avec
  l'ID du réglage de rendu sous forme de HTML

En saisissant "##mm", les tokens possibles sont affichés.

Avec ces valeurs, une mise en forme individuelle de la sortie est possible
aussi bien dans le widget de formulaire que dans l'e-mail. Les templates
existants peuvent, comme d'habitude, être surchargés par des variantes
personnalisées.

.. note:: Une modification, p. ex. la suppression des éléments de la liste de favoris, n'est pas possible
   dans le formulaire, car lors d'un rechargement de la page, les données déjà saisies dans le formulaire
   seraient perdues.

On peut, avant l'affichage du formulaire, afficher une liste avec tous les
éléments de la liste de favoris et les modifier individuellement à cet
endroit, ou supprimer la liste entière - voir le lien.

.. code-block:: html
   :linenos:

   <p><a href="de/metamodels/note-list-contact-form.html?notelist_2_action=clear">Clear List 2</a></p>

|img_nodelist_form_fe_list_edit_items|

Les données sont transmises par e-mail et peuvent être adaptées dans
l'affichage via le template d'e-mail. Pour l'envoi, l'option de formulaire
Contao ou également le "Notification Center (NC)" sont disponibles.

|img_notelist_email_list|

Lors de l'utilisation du NC, la sortie texte du rendu de l'e-mail peut
également être convertie en HTML via un Simple-Token personnalisé, p. ex.
les sauts de ligne en balises ``<br>``. Dans le
`NCpro <https://extensions.terminal42.ch/docs/notification-center-pro/de/eigene-tokens/>`_,
il est très simple de définir ses propres tokens dans le backend - les
filtres Twig ``nl2br`` et ``raw`` aident pour la sortie.


.. _rst_extended_notelist_additional_form:
Transmission de données supplémentaires pour chaque item
------------------------------------------------------------

En option, des données supplémentaires peuvent être transmises à la liste
de favoris pour chaque item, comme p. ex. une quantité, un texte libre ou
similaire. Pour cela, on crée via le générateur de formulaires un formulaire
contenant les champs à afficher, p. ex. un champ de sélection pour une
quantité et un champ texte pour une courte information - un champ d'envoi
n'est pas nécessaire et est généré automatiquement.

Ce formulaire créé est désormais disponible dans les paramètres de la liste
de favoris - les formulaires qui contiennent déjà un élément de formulaire
liste de favoris ne sont pas affichés (récursion !).

Dans l'affichage de la liste, le formulaire est désormais affiché pour
chaque item, avec un bouton "Ajouter/Éditer". Les données sont également
traitées par le formulaire et par exemple envoyées avec l'e-mail
(:ref:`voir ci-dessus <rst_extended_notelist_show_at_form>`).

|img_notelist_fe_list_with_form|


InsertTags
----------

Pour la sortie du nombre d'items dans les listes de favoris, différents
InsertTags sont implémentés. Ceux-ci affichent le nombre comme suit
('mm_mitarbeiterliste' est le MetaModels correspondant) :

* nombre de tous les items : {{metamodels_notelist::sum::mm_mitarbeiterliste}}
* nombre de tous les items de la liste de favoris ID 1 : {{metamodels_notelist::sum::mm_mitarbeiterliste::1}}
* nombre de tous les items des listes de favoris ID 1 et 2 : {{metamodels_notelist::sum::mm_mitarbeiterliste::1,2}}

S'il n'y a aucun item dans la liste de favoris, 0 (zéro) est affiché.


.. _rst_extended_notelist_additional_events:
Événements
----------

Si la manipulation d'une Notelist (add, remove, clear) doit être surveillée,
un écouteur d'événement est disponible à cet effet.

Avec l'écouteur d'événement, une réponse au site web peut par exemple être
donnée, ou un logging/suivi des actions effectué.

À titre d'exemple pour une réponse, un écouteur peut être créé comme suit
(voir aussi :ref:`rst_cookbook_specials_register-services`) :

.. code-block:: php
   :linenos:

   <?php
   // src/EventListener/ManipulateNoteListListener.php
   namespace App\EventListener;

   use Contao\Message;
   use MetaModels\NoteListBundle\Event\ManipulateNoteListEvent;
   use Terminal42\ServiceAnnotationBundle\Annotation\ServiceTag;

   /**
    * @ServiceTag("kernel.event_listener", event="metamodels.note-list.manipulate")
    */
   class ManipulateNoteListListener
   {
       public function __invoke(ManipulateNoteListEvent $event)
       {
           // Only handle note list "1".
           if ('1' !== ($listId = $event->getNoteList()->getStorageKey())) {
               return;
           }

           switch ($event->getOperation()) {
               case ManipulateNoteListEvent::OPERATION_ADD:
                   Message::addConfirmation('Added ' . $event->getItem()->get('id') . ' to ' . $listId);
                   // Add your own notes in metaData.
                   $metaData = $event->getNoteList()->getMetaDataFor($event->getItem());
                   $metaData['tstamp'] = time();
                   $event->getNoteList()->updateMetaDataFor($event->getItem(), $metaData);
                   break;
               case ManipulateNoteListEvent::OPERATION_REMOVE:
                   Message::addConfirmation('Removed ' . $event->getItem()->get('id') . ' to ' . $listId);
                   break;
               case ManipulateNoteListEvent::OPERATION_CLEAR:
                   Message::addConfirmation('Cleared ' . $listId);
                   break;
               default:
                   throw new \RuntimeException('Unknown note list operation: ' . $event->getOperation());
           }
       }
   }

Sur le site web, la réponse peut être affichée dans un template via la
sortie du message Contao - p. ex. avec le code suivant dans un template
personnalisé comme ce_html_message.html5

.. code-block:: php
   :linenos:

   <?php
   $message = \Contao\Message::generateUnwrapped(null, true);
   ?>
   <?php if ($message): ?>
   <div class="alert alert-primary" role="alert">
       <p class="mb-0"><?= $message?></p>
   </div>
   <?php endif; ?>

De plus, des informations supplémentaires peuvent également être enregistrées
via cet événement - voir chez `OPERATION_ADD`.


Problèmes connus et prochaines fonctionnalités
------------------------------------------------

* les pages avec liste de favoris/Notelist ne doivent pas être mises en cache
* dans Contao à partir de la 4.9, les templates avec les extensions ``.text`` et ``.twig`` ne peuvent
  plus être créés dans la section Templates, car Contao ne le prend plus en charge - créer les fichiers
  via SSH/SFTP ou localement


Dons
----

Un grand merci pour les dons* pour l'extension à :

**Version 2.5 :**

**Version 2.4 :**

* `dpmed GmbH <https://www.dpmed.de>`_ : 350 €
* `afm werbestudio & agentur <https://www.afm-werbestudio.de/>`_ : 350 €
* `Nationalfonds AT <https://www.nationalfonds.org/>`_ : 350 €
* `AntwortInternet <https://www.antwortinternet.com/>`_ : 350 €
* Johannes Bittner : 350 €


**Version 2.0 à 2.3 :**

* `Sebastian Krull <http://www.sebastiankrull.de>`_ : 350 €
* `Westwerk GmbH & Co. KG <https://www.westwerk.ac>`_ : 350 €
* `Carsten Merz <http://www.fitkurs.de>`_ : 350 €
* Next Home Creation : 350 €
* `Niels Hegmanns <http://www.heimseiten.de>`_ : 350 €
* `Hofer Werbung <http://www.hofer-werbung.de>`_ : 350 €
* `Nationalfonds AT <https://www.nationalfonds.org>`_ : 350 €
* `AFM-Werbestudio <https://www.afm-werbestudio.de>`_ : 350 €
* `PITSol <https://www.pitsol.de/>`_ : 350 €
* `ghost.company <https://www.ghostcompany.com/>`_ : 350 €
* Druckhaus S+F : 350 €
* w3scout : 350 €
* `Nationalfonds AT <https://www.nationalfonds.org>`_ : 350 €
* `Nationalfonds AT <https://www.nationalfonds.org>`_ : 350 €
* `AFM-Werbestudio <https://www.afm-werbestudio.de>`_ : 350 €
* `Ulf Spethmann <https://derdigitalist.de>`_ : 350 €
* `Sienos <https://www.sineos.de>`_ : 350 €


(*dons nets)


.. |br| raw:: html

   <br />


.. |img_notelist_icon| image:: /_img/screenshots/extended/notelist/notelist_icon.png
.. |img_nodelist_config| image:: /_img/screenshots/extended/notelist/nodelist_config.png
.. |img_notelist_overview| image:: /_img/screenshots/extended/notelist/notelist_overview.png
.. |img_notelist_ce_mm-list| image:: /_img/screenshots/extended/notelist/notelist_ce_mm-list.png
.. |img_notelist_fe_list| image:: /_img/screenshots/extended/notelist/notelist_fe_list.png
.. |img_nodelist_form_fe_list_edit_items| image:: /_img/screenshots/extended/notelist/nodelist_form_fe_list_edit_items.png
.. |img_notelist_filterrule| image:: /_img/screenshots/extended/notelist/notelist_filterrule.png
.. |img_notelist_filtered_list| image:: /_img/screenshots/extended/notelist/notelist_filtered_list.png
.. |img_notelist_fe_list_with_filter| image:: /_img/screenshots/extended/notelist/notelist_fe_list_with_filter.png
.. |img_nodelist_form_widget| image:: /_img/screenshots/extended/notelist/nodelist_form_widget.png
.. |img_nodelist_form_fe_list| image:: /_img/screenshots/extended/notelist/nodelist_form_fe_list.png
.. |img_notelist_email_list| image:: /_img/screenshots/extended/notelist/notelist_email_list.png
.. |img_notelist_fe_list_with_form| image:: /_img/screenshots/extended/notelist/notelist_fe_list_with_form.png
