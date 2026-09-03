.. _new_in_mm230:

Changements et fonctionnalités de MM 2.3
========================================

Voici un aperçu des changements et fonctionnalités de MetaModels 2.3, rendus possibles grâce au
"programme early adopter" - pour en savoir plus sur le Fundraising, consultez la
`page web de MM <https://now.metamodel.me/de/unterstuetzer/fundraising#metamodels_2-3>`_.

Pour une vérification après une mise à jour vers MM 2.3, voir :ref:`les indications ci-dessous <check_upgrade_mm230>`.

.. note:: Pour la création des tables mm_* et des colonnes des attributs, une migration de base de données doit
   être effectuée - voir :ref:`Schemamanager <component_schema-manager>`. |br|
   Après la création ou la modification des libellés des modèles, attributs ou légendes, veuillez vider le cache
   (de traduction) - voir :ref:`component_translations`.


Général et Core
---------------

Les prérequis d'installation pour MetaModels 2.3 sont :

* un Contao 4.13.x (LTS) fonctionnel
* PHP 8.1 minimum
* MySQL à partir de la version 5.5.5 (InnoDB), MariaDB (y compris "strict mode")
* ``memory_limit`` de 512 Mo ou plus (recommandé)

* intégration d'un nouveau gestionnaire de schéma - :ref:`plus d'infos <component_schema-manager>`
* les entrées de tri/regroupement disposent d'un bouton de bascule permettant de les activer/désactiver
  (`#1380 <https://github.com/MetaModels/core/issues/1380>`_)
* remarque pour les développeurs : il existe une nouvelle classe permettant de trier les attributs par nom
  (src/CoreBundle/Sorter/AttributeSorter.php) - elle est utilisée par exemple lors de la sélection de l'attribut
  pour le tri (ceux-ci sont désormais triés par ordre croissant)
* lorsque le premier tri est créé, la case à cocher "Standard" est désormais présélectionnée
  (`#1472 <https://github.com/MetaModels/core/issues/1472>`_)
* lorsque le mode de rendu du masque de saisie est réglé sur "Hiérarchie", une indication apparaît désormais
  précisant que le tri doit être réglé sur "Manuel" (`#1324 <https://github.com/MetaModels/core/issues/1324>`_)
* la case à cocher "Variante" au niveau des attributs est désactivée si le modèle n'est pas variant
  (`#884 <https://github.com/MetaModels/core/issues/884>`_)
* pour les items de variante, les boutons de déplacement sont désactivés (`#871 <https://github.com/MetaModels/core/issues/871#issuecomment-2558575073>`_)
* pour les items de variante, les attributs non variants ne sont désormais plus masqués dans le masque, mais
  affichés en lecture seule
* la classe "getSearchablePages" (indexation des pages de détail) a été entièrement réécrite et fonctionne
  désormais de manière plus efficace/rapide
* il existe un nouvel événement pour manipuler le sous-titre du masque de saisie
  `GetEditMaskSubHeadlineEvent <https://github.com/contao-community-alliance/dc-general/blob/39ec68cee8b7034e5c1900692cd1b0eeaa7d4c7e/src/Contao/View/Contao2BackendView/Event/GetEditMaskSubHeadlineEvent.php>`_
* pour le masque de saisie, on peut désormais configurer l'affichage de valeurs de l'item dans le titre du masque
  lors de l'édition
* les inserttags ont été entièrement retravaillés - :ref:`veuillez tenir compte de la syntaxe partiellement modifiée <component_inserttags>`
* adaptation au changement de Contao pour les indications de locale (désormais ``_`` au lieu de ``-``) - toutes les
  indications $GLOBALS[TL_LANGUAGE] sont marquées comme obsolètes (deprecated)
* le tri au niveau du CE/module dispose d'un réglage permettant d'ajouter un fragment d'URL pour atteindre un point
  d'ancrage, pour ``generateSortingLink`` et ``renderSortingLink``
* dans le template de liste ``metamodels_prerendered``, deux méthodes sont désormais disponibles pour générer, pour
  un attribut, des liens de changement de tri - plus d'informations dans le ":ref:`cookbook <rst_cookbook_templates_fe_list_sorting>`"
* support du nouveau routage intégré dans Contao 4.10 - ce qui permet de désactiver le routage legacy via config.yml
  (``legacy_routing: false``)
* la gestion de session a été convertie de la session Contao vers la session Symfony
* gestion de la priorité de route - voir :ref:`rst_cookbook_tips_set-route-priority`
* possibilité de choisir les templates de widget pour le masque de saisie (backend) - voir Attributs
* les modèles liés en tant que table enfant peuvent désormais contenir des variantes (`#1054 <https://github.com/MetaModels/core/issues/1054>`_)
* la liste en backend peut être regroupée par semaine calendaire - le formatage peut être adapté individuellement
  par langue via une clé de langue
* les traductions sont passées du `CCA-Translator <https://github.com/contao-community-alliance/translator>`_ et des
  `tableaux de langue globaux <https://symfony.com/doc/current/translation.html>`_ au Symfony-Translator. Les
  traductions sont ainsi conservées dans le catalogue de messages Symfony correspondant, ce qui accélère la
  construction des pages en backend. Les traductions personnalisées peuvent désormais aussi être gérées au format
  Xliff. |br|
  En backend, peu d'endroits sont concernés par ce changement - il a par exemple été possible de corriger la vue en
  tableau des items lorsqu'un attribut de la liste n'était pas présent dans le masque de saisie correspondant. Jusqu'ici,
  seule la clé de traduction apparaissait à cet endroit - désormais, c'est le titre correspondant de l'attribut qui
  s'affiche. |br|
  Les textes de traduction personnalisés existants, créés sous forme de tableau PHP,
  `doivent être transférés dans un fichier XLIFF <https://metamodels.readthedocs.io/de/latest/manual/component/translations.html#eigene-anpassung-von-ubersetzungen>`_. |br|
  Plus d'informations à ce sujet dans :ref:`component_translations`
* un changement de routage a été effectué : les masques de MM en backend ne sont désormais plus accessibles via le
  paramètre GET ``...contao?do=metamodels_<model-name>``, mais via la route ``...contao/metamodels/<model-name>``.
  Cela a permis une simplification, par exemple, de la gestion des droits en backend. Auparavant, il fallait
  effectuer les réglages correspondants à la fois au niveau des affectations de saisie et de rendu ("dernière icône")
  pour les groupes d'utilisateurs et au niveau des réglages des groupes d'utilisateurs de Contao - les réglages côté
  Contao ont disparu et il suffit désormais d'attribuer les droits dans MM (masque de saisie + affectations). |br|
  Avec le nouveau routage, il y a un problème avec la bascule du mode debug en backend - Contao attend la valeur du
  referer sous une forme précise, que nous ne pouvons actuellement pas simplement réécrire ; après la bascule, on
  atterrit sur une "page par défaut" de Contao - cela n'a pas d'autre conséquence (voir "Problèmes connus").
* dans les réglages de rendu, le type de référence pour la génération de l'URL peut désormais être indiqué pour les
  liens de redirection (jumpTo) - il est ainsi par exemple possible de définir une URL absolue incluant le domaine ;
  voir `Symfony UrlGeneratorInterface <https://github.com/symfony/routing/blob/f8dd6f80c96aeec9b13fc13757842342e05c4878/Generator/UrlGeneratorInterface.php#L34-L55>`_
* les templates des attributs dans les réglages de rendu sont désormais des champs obligatoires
* pour les modèles multilingues, le panel (filtre/recherche) de la liste en backend réagit désormais au réglage de
  langue de la liste
* le core, les attributs et les filtres ont été vérifiés avec la collection d'outils `PHPCQ <https://github.com/phpcq/phpcq>`_
  et adaptés en conséquence - voir `Github <https://github.com/MetaModels/core/issues/1502>`_
* :ref:`Intégration File-Usage <rst_extended_file-usage>`


Attributs
---------

* pour tous les attributs, les templates HTML5 ont été retravaillés : classe CSS avec type d'attribut et type de
  sortie, code court PHP, balise HTML englobante avec affichage de la classe CSS optionnelle
* pour tous les attributs, le template pour le backend peut être choisi via un select - pour le frontend, voir FEE

* Alias
    * vérification de la combinaison Variant et Unique - `voir News janvier 2025 <https://now.metamodel.me/de/mm-eap-newsletter-2-3/details/eap-info-mm-2-3-januar-i-2025>`_
* Fichier
    * support des dimensions prédéfinies pour les tailles d'image de `config.yaml` -
      voir `contao.image.sizes:... <https://docs.contao.org/dev/framework/image-processing/image-sizes/#size-configuration>`_
    * support de la recherche de fichiers en backend - on peut rechercher par nom de fichier ou par UUID ; les
      items dans lesquels le fichier est intégré sont affichés - que ce soit par sélection directe du fichier ou
      lorsque le dossier parent a été sélectionné
    * :ref:`Intégration File-Usage <rst_extended_file-usage>`
* Contenu d'un article
    * adaptation du template
    * modification de l'affichage en backend dans la vue en liste - au lieu de l'aperçu des types d'éléments, c'est
      désormais le rendu original qui est affiché ; ceci est par exemple nécessaire pour l'indexation des recherches
      en texte intégral - le template de sortie peut être adapté individuellement
    * :ref:`Intégration File-Usage <rst_extended_file-usage>`
* Valeurs combinées
    * vérification de la combinaison Variant et Unique - `voir News janvier 2025 <https://now.metamodel.me/de/mm-eap-newsletter-2-3/details/eap-info-mm-2-3-januar-i-2025>`_
* Texte long
    * le texte long supporte désormais le readonly avec TinyMCE et ACE - `voir <https://github.com/contao/contao/pull/5985>`_
    * correction des templates pour l'affichage du texte : toutes les balises HTML sont supprimées
    * :ref:`Intégration File-Usage <rst_extended_file-usage>`
* Tableau-Multi (MCW)
    * support du readonly et des classes CSS pour le tl_class du widget
* Tableau de texte
    * support du readonly
* Alias traduit
    * vérification de la combinaison Variant et Unique - `voir News janvier 2025 <https://now.metamodel.me/de/mm-eap-newsletter-2-3/details/eap-info-mm-2-3-januar-i-2025>`_
* Fichier traduit
    * support des dimensions prédéfinies pour les tailles d'image de `config.yaml` -
      voir `contao.image.sizes:... <https://docs.contao.org/dev/framework/image-processing/image-sizes/#size-configuration>`_
    * support de la recherche de fichiers en backend - on peut rechercher par nom de fichier ou par UUID ; les
      items dans lesquels le fichier est intégré sont affichés - que ce soit par sélection directe du fichier ou
      lorsque le dossier parent a été sélectionné
    * :ref:`Intégration File-Usage <rst_extended_file-usage>`
* Contenu traduit d'un article
    * adaptation du template
    * modification de l'affichage en backend dans la vue en liste - au lieu de l'aperçu des types d'éléments, c'est
      désormais le rendu original qui est affiché ; ceci est par exemple nécessaire pour l'indexation des recherches
      en texte intégral - le template de sortie peut être adapté individuellement
    * :ref:`Intégration File-Usage <rst_extended_file-usage>`
* Valeurs combinées traduites
    * vérification de la combinaison Variant et Unique - `voir News janvier 2025 <https://now.metamodel.me/de/mm-eap-newsletter-2-3/details/eap-info-mm-2-3-januar-i-2025>`_
* Texte long traduit
    * le texte long supporte désormais le readonly avec TinyMCE et ACE - `voir <https://github.com/contao/contao/pull/5985>`_
    * correction des templates pour l'affichage du texte : toutes les balises HTML sont supprimées
    * :ref:`Intégration File-Usage <rst_extended_file-usage>`
* Tableau de texte traduit
    * support du readonly
* Tableau-Multi traduit (MCW)
    * support du readonly et des classes CSS pour le tl_class du widget


Filtre
------

* pour le CE/module filtre, le type est désormais également indiqué dans les libellés des règles de filtre
  (`#1473 <https://github.com/MetaModels/core/issues/1473>`_)
* pour le CE/module filtre, l'ID pour "FORM_SUBMIT" peut être surchargé - voir :ref:`rst_cookbook_filter_filter-with-forwarding`
* en complément de la gestion des droits FEE, il existe une nouvelle règle de filtre qui filtre la liste selon les
  items associés à un membre connecté
* le template pour l'affichage du filtrage sous forme de liste de liens a été retravaillé, de sorte que le crawler
  Contao ne suit plus ces liens pour l'indexation de recherche
* Statut de case à cocher (anciennement statut de publication) et Statut de case à cocher traduit (anciennement statut de publication traduit)
    * la règle de filtre a été renommée de "statut de publication" en "statut de case à cocher", car la case à
      cocher ne pilote pas forcément une publication
    * l'option "ne pas utiliser le filtre dans l'aperçu frontend" réagit désormais au statut Contao "aperçu" - jusqu'ici
      elle réagissait à la connexion au backend
* SQL personnalisé
   * le type "list" a désormais été ajouté au paramètre d'inserttag "aggregate" - il était certes déjà toujours décrit
     dans l'infobulle, mais n'était pas encore implémenté jusqu'ici ; il permet désormais de transmettre des listes de
     valeurs séparées par des virgules comme valeur GET
   * vérification des requêtes SQL personnalisées avec ``SUBSTRING_INDEX(SUBSTRING_INDEX('{{env::request}}', '/', -1), '?', 1)``
     et adaptation au nouveau routage - voir :ref:`rst_cookbook_filter_custom-sql`
   * il est désormais possible de limiter l'exécution à certains environnements, comme le frontend
* Requête simple
    * si l'option "paramètre statique" est activée, une valeur peut désormais être sélectionnée pour la règle de
      filtre dans le CE/module MM-Liste - nouvelle option "sans valeur de donnée [null]", lorsqu'aucune sélection -
      pas même une chaîne vide - ne doit être définie
* Sélection unique [select]
    * type d'attribut Numérique (Integer) et Valeurs combinées possibles
    * attribut ``data-escargot-ignore`` inséré dans le template d'affichage en liste, afin que les liens ne soient pas indexés
* Sélection multiple [Tags]
    * type d'attribut Numérique (Integer) possible
    * attribut ``data-escargot-ignore`` inséré dans le template d'affichage en liste, afin que les liens ne soient pas indexés
* Registre
    * le template pour l'affichage du filtrage sous forme de liste de liens a été retravaillé, de sorte que le crawler
      Contao ne suit plus ces liens pour l'indexation de recherche (``data-escargot-ignore``)
    * des blocs pour `formlabel` et `formfield` ont été insérés dans le template
    * un fragment d'URL peut désormais être indiqué - la page se positionne ainsi sur le point d'ancrage après le rechargement


Frontend-Editing (FEE)
----------------------

* une gestion simple des droits a été intégrée, qui permet, une fois activée, que chaque membre connecté ne puisse
  plus modifier que ses propres entrées (`#14 <https://github.com/MetaModels/contao-frontend-editing/issues/14>`_)
* en complément de la gestion des droits, il existe une nouvelle règle de filtre qui filtre la liste selon les
  items associés à un membre connecté
* il existe un nouvel événement pour manipuler le sous-titre du masque de saisie
  `GetEditMaskSubHeadlineEvent <https://github.com/contao-community-alliance/dc-general/blob/39ec68cee8b7034e5c1900692cd1b0eeaa7d4c7e/src/Contao/View/Contao2BackendView/Event/GetEditMaskSubHeadlineEvent.php>`_
* pour le masque de saisie, on peut désormais configurer l'affichage de valeurs de l'item dans le titre du masque
  lors de l'édition (`#14 <https://github.com/MetaModels/contao-frontend-editing/issues/43>`_) - :ref:`voir FEE <extended_frontend_editing_headlines>`
* le lien "Create" n'est plus présent dans le template standard du module frontend - le template a été aligné sur celui du CE
* modification de la résolution des inserttags lors du :ref:`téléversement de fichiers <extended_frontend_editing_upload>` - à adapter le cas échéant
* les miniatures des fichiers image dans la dropzone sont désormais affichées après un rechargement de la page
* possibilité de choisir les templates de formulaire pour le masque de saisie (FEE) pour tous les attributs non traduits
* lors de la surcharge des boutons du masque de saisie, un inserttag peut désormais également être inséré dans
  "Paramètre", en plus des "Simple Tokens"
* le template de la dropzone a été adapté - vérifier le cas échéant ses propres adaptations
* support des dimensions prédéfinies pour les tailles d'image de `config.yaml` pour les miniatures -
  voir `contao.image.sizes:... <https://docs.contao.org/dev/framework/image-processing/image-sizes/#size-configuration>`_
* l'option "téléversement de fichier unique" est de nouveau supportée
* adaptation de l'affichage en liste en backend pour "Contenu d'un article" ainsi que "Contenu traduit d'un article"
* support du Notification-Center version 2.x pour les notifications lors de la création ou de la modification
  d'enregistrements - lors de la mise à niveau vers NC 2.x, les clés éventuellement présentes issues de la version
  1.7 sont migrées dans la table "tl_nc_notification" ; voir le message affiché lors de l'exécution de la migration
  de base de données
* la génération des liens d'édition en frontend a été retravaillée, de sorte que le crawler Contao ne suit plus ces
  liens pour l'indexation de recherche (``data-escargot-ignore``) - avec le lien "Supprimer", cela peut entraîner
  une perte de données


Extensions
----------

* la :ref:`liste de favoris (Notelist) <rst_extended_notelist>` a été publiée pour MM 2.3



Problèmes connus
----------------

* lors de la bascule vers/depuis le mode debug en backend via le bouton, la page de référence n'est plus correcte
  et il faut de nouveau accéder à la page - par exemple avec "retour" dans le navigateur et rechargement de la page |br|
  Contao n'offre actuellement aucun moyen d'influencer le referer à cet endroit


.. _check_upgrade_mm230:
Vérification pour la mise à jour vers MM 2.3
--------------------------------------------

En principe, une mise à jour au sein de la branche MM 2.x est possible sans problème, et les adaptations
nécessaires aux libellés ainsi que les modifications de base de données sont prises en charge par les migrations.
Il y a toutefois quelques points que celles-ci ne peuvent pas gérer, ou seulement très difficilement. C'est
pourquoi il convient de garder à l'esprit les points suivants lors du passage à MM 2.3 :

* veuillez tenir compte de toutes les indications de :ref:`MM 2.2 <check_upgrade_mm220>`
* si une mise à jour a été effectuée, veuillez supprimer les données de session de l'utilisateur en backend afin
  d'éviter l'affichage de "pseudo-erreurs" (par exemple `Cannot assign null ... $intAmount of type int <https://now.metamodel.me/de/mm-eap-newsletter-2-3/details/eap-info-mm-2-3-dezember-ii-2023>`_)
* pour une mise à jour depuis une version antérieure à 2.2, veuillez consulter la :ref:`liste de vérification pour MM 2.2 <check_upgrade_mm220>`
* effectuer une migration de base de données pour la création des tables mm_* et des colonnes des attributs -
  :ref:`voir Schemamanager <component_schema-manager>`
* les favoris enregistrés vers MM en backend ne sont plus valides en raison du nouveau routage - `voir la newsletter <https://now.metamodel.me/de/mm-eap-newsletter/details/eap-info-mm-2-3-juli-ii-2024#nl-reader>`_
* les autorisations pour les groupes d'utilisateurs sont désormais attribuées uniquement dans MM (voir ci-dessus
  "changement de routage") - supprimer les cases à cocher superflues des groupes d'utilisateurs dans "modules backend"
* vérification des templates HTML5 - ils ont été retravaillés (voir Attributs, Filtre et FEE)
* vérification des templates HTML5 des widgets de filtre qui affichent des listes de liens - le crawling des URL a été empêché
* vérification des templates HTML5 avec traductions - par exemple ContentArticle
* correction des templates pour l'affichage du texte des deux attributs Texte long : toutes les balises HTML sont supprimées
* vérifier les filtres avec la priorité de route "auto_item" - voir :ref:`rst_cookbook_tips_set-route-priority`
* pour FEE et le module frontend, changer le cas échéant le template pour le lien "Create"
* pour FEE, vérifier le mode d'upload :ref:`téléversement de fichiers <extended_frontend_editing_upload>`
* pour FEE, vérifier la résolution des inserttags lors du :ref:`téléversement de fichiers <extended_frontend_editing_upload>`
* pour FEE, vérifier que la page de liste et la page d'édition sont exclues de la recherche Contao
* vérification de ses propres traductions - `passage au format Xliff <https://metamodels.readthedocs.io/de/latest/manual/component/translations.html#eigene-anpassung-von-ubersetzungen>`_
* vérification des :ref:`valeurs par défaut personnalisées pour le masque de saisie <rst_cookbook_inputmask_default-values>`
* vérification :ref:`des libellés des masques de saisie en cas d'adaptations personnalisées - "LABEL NOT SET" <component_translations_lns>`
* vérification des requêtes SQL personnalisées avec ``SUBSTRING_INDEX(SUBSTRING_INDEX('{{env::request}}', '/', -1), '?', 1)``
  et adaptation au nouveau routage - voir :ref:`rst_cookbook_filter_custom-sql`
* lorsque l'option "Variant" du modèle est activée, une vérification de la combinaison non supportée Variant et
  Unique est effectuée par migration au niveau des attributs -
  `voir News janvier 2025 <https://now.metamodel.me/de/mm-eap-newsletter-2-3/details/eap-info-mm-2-3-januar-i-2025>`_
* pour la liste MM et le preset via "Requête simple" avec "paramètre statique", tenir compte du nouveau réglage
  "- sans valeur de donnée [null] -"


Refinancement
-------------
.. seealso:: Pour un refinancement de ces travaux considérables, l'équipe MM demande une contribution
   financière. Comme ordre de grandeur, il convient de prendre l'ampleur du projet à réaliser et de
   prévoir environ 10 % - d'après l'expérience des contributions passées, il s'agit de montants
   compris entre 100 € et 500 € (hors taxes) - une facture incluant la TVA est bien sûr toujours
   établie. `Plus... <https://now.metamodel.me/de/unterstuetzer/spenden>`_


.. |br| raw:: html

   <br />
