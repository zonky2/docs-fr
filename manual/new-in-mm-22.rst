.. _new_in_mm220:

Changements et fonctionnalités de MM 2.2
========================================

Voici un aperçu des changements et fonctionnalités de MetaModels 2.2, rendus possibles grâce au
"programme early adopter" - pour en savoir plus sur le Fundraising, consultez la
`page web de MM <https://now.metamodel.me/de/unterstuetzer/fundraising#metamodels_2-2>`_.

Pour une vérification après une mise à jour vers MM 2.2, voir :ref:`les indications ci-dessous <check_upgrade_mm220>`.

Général et Core
---------------

MetaModels 2.2 apporte une compatibilité complète avec Contao 4.9 ainsi que diverses fonctionnalités et
optimisations. Par exemple, MM 2.2 est compatible avec le `strict mode` des versions récentes de MySQL ou
de MariaDB actuel, ainsi qu'avec le tri manuel des fichiers.

Les prérequis d'installation pour MetaModels 2.2 sont :

* un Contao 4.9.x (LTS) fonctionnel
* PHP 7.4
* MySQL à partir de la version 5.5.5 (InnoDB), MariaDB (y compris "strict mode")
* ``memory_limit`` de 512 Mo ou plus (recommandé)

Des versions plus récentes de Contao peuvent fonctionner, mais ne sont pas officiellement supportées.

* compatible avec le `strict mode` de MySQL et MariaDB ; toutes les requêtes ont été réécrites avec le queryBuilder
  et un préfixe de table a été ajouté aux requêtes - la vérification des mots réservés de MySQL devient ainsi superflue
* diverses optimisations pour un affichage plus rapide des données
* backend de MM "nettoyé" et réglages habituels définis par défaut (environ 30 % de clics en moins lors de la création)
* tous les dépôts sont passés à Github-Actions pour une vérification automatique du code
* dans le backend, le panel (zone au-dessus de la vue en liste) utilise désormais les icônes standard de Contao pour
  le filtrage et la réinitialisation des filtres, à la place des "flèches jaunes"
* dans le domaine des MetaModels traduits, une bonne partie du code a été refactorisée - ainsi, une nouvelle interface
  ITranslatedMetaModel a été ajoutée pour une interface plus simple et propre d'accès aux données.
  Pour "l'utilisateur final de MM", rien ne change visiblement dans un premier temps, mais cela simplifie et sécurise
  le travail/développement du multilinguisme dans MM.
* révision de toutes les migrations pour le support du `strict mode`, désormais `case sensitive` pour les noms de colonnes
* suppression des fichiers de template xhtml qui ne sont plus supportés par Contao ; la migration affiche une
  indication si d'anciens fichiers de template xhtml de MM, non supportés par Contao, sont trouvés - ils ne peuvent
  malheureusement pas être adaptés automatiquement.
* dans la liste des attributs, recherche et filtrage par nom ou par type
* dans les réglages du masque de saisie, suppression des popups DCA (défectueux) - remplacés par un popup d'aide ("panneau de signalisation")
* support du caching (balises ESI)
* affichage amélioré lors de la sélection d'attributs - désormais selon le schéma 'Nom-attribut [Type, "nom-colonne"]'
* nouveau template de sortie frontend pour l'affichage de débogage : metamodel_prerendered_debug.html5
* pour l'URL de la page de redirection (jumpTo), il fallait auparavant indiquer dans les rendersettings à la fois
  la page et un filtre - désormais, seule la sélection de la page est nécessaire et l'URL est générée dans le
  template de liste. On peut ainsi, par exemple depuis le backend, créer sur la page de détail un lien retour vers
  la page de liste sans devoir indiquer de filtre. Pour vérifier si des paramètres de filtre ont été définis, il
  existe désormais le nœud "deep" - qui vaut `true` si des paramètres sont présents.
* nouvelles options pour la pagination de la sortie en liste de MM (voir captures d'écran ci-dessous)

  * un paramètre dynamique empêche les "interférences" entre la pagination de différentes listes
  * le nom du paramètre de pagination peut être choisi librement
  * un template personnalisé pour la pagination est possible - par défaut "mm_pagination.html5"
  * on peut choisir si le paramètre est transmis via slug (/page_mmce42/3) ou GET (?page_mmce42=3)
  * les liens de pagination peuvent être complétés par un fragment d'URL (ancre) - adapter le cas échéant ses propres templates
* nouvelles options pour la surcharge du tri dans la sortie en liste de MM (voir captures d'écran ci-dessous)

  * le nom des paramètres standard "orderBy" et "orderDir" peut être remplacé par des valeurs personnalisées
  * les paramètres peuvent être indiqués au choix en slug et/ou en GET
* nouvelle option pour transmettre des paramètres personnalisés depuis les réglages de la sortie en liste
  (CE/module frontend) vers le template de liste. Via un MCW, on peut créer ses propres "paires clé-valeur", qui
  sont disponibles dans le template sous forme de tableau via "$this->params". Cela permet de généraliser davantage
  un template de liste et de le piloter depuis le backend, par exemple avec des libellés, des traductions ou des
  paramètres pour la sortie ou le contenu JavaScript. Voir :ref:`rst_cookbook_templates_fe_list_parameters`.
* le comptage des items dans les widgets du filtre frontend a été désactivé - voir `Github <https://github.com/MetaModels/core/issues/312#issuecomment-686963070>`_
* dans l'élément de contenu MM-Liste, la vue en liste de l'article affiche désormais les sélections de filtre du
  "paramètre statique" en plus de l'indication du nom du filtre
* nouvel inserttag pour le nombre d'items (total count) : `{{mm::total::mm::[MM Name|ID](::[ID filter])}}` - un
  CE/module MM supplémentaire n'est ainsi plus nécessaire
* l'inserttag MM "Item" appliquait par défaut un filtrage sur une éventuelle case à cocher avec "Publier" activé -
  pour un comportement identique à celui des listes MM, cette vérification automatique a été supprimée de l'inserttag
* les attributs marqués comme variante sont désormais signalés dans la liste des attributs
* toutes les requêtes SQL ont été munies de préfixes de table, de sorte qu'une vérification des `mots réservés de MySQL <https://dev.mysql.com/doc/refman/5.7/en/keywords.html>`_ n'est plus nécessaire
* les conditions d'affichage pour les widgets du masque de saisie ont été adaptées : une "non-sélection", par exemple
  d'un paramètre select ou tags, est désormais correctement évaluée, c'est-à-dire que si "Rien" a été choisi comme
  condition, le widget est visible - jusqu'à ce qu'une sélection soit faite (ce qui évite un opérateur NOT)
* dans le masque "Tout ajouter" du masque de saisie, il existe désormais un champ de saisie permettant d'attribuer
  directement une ou plusieurs classes CSS aux attributs - lorsqu'on ajoute les attributs individuellement, la classe
  CSS standard est "w50" - cette fonctionnalité permet d'éviter de devoir éditer chaque attribut séparément
* lorsqu'on clique sur "Enregistrer et nouveau" lors de la création d'un attribut, le type d'attribut est repris
  et présélectionné
* lorsqu'un attribut est supprimé, une éventuelle condition d'affichage ou un tri/regroupement associé est désormais
  automatiquement supprimé aussi
* pour le multilinguisme, l'indication de territoire dans la locale est désormais également supportée, par exemple
  ch_DE, ch_FR, etc. dans les réglages du modèle, une case à cocher permet d'étendre la liste des "langues" avec les
  indications de territoire ; la liste indique à chaque fois à quoi doit ressembler l'entrée dans le point de départ
  du site web
* l'affichage du masque de saisie pour les variantes a été adapté. Jusqu'ici, les attributs sans variation étaient
  masqués dans le masque de variante - désormais, ces attributs sont affichés en lecture seule.


Attributs
---------
* Alias
    * générateur de slug pour les caractères spéciaux
    * option pour empêcher le préfixe "id-" pour les nombres
* Case à cocher
    * les icônes personnalisées optionnelles sont rendues sous forme de miniatures 16x16px
    * si les cases à cocher sont en `readonly`, elles sont affichées dans la vue en liste, mais n'ont pas de fonction de bascule
    * le widget en `readonly` fonctionne désormais correctement dans le masque de saisie
* ContentArticle
    *  un aperçu des éléments créés, avec leur type et leur visibilité, est disponible aussi bien dans le masque
       de saisie que dans la vue en liste
* Fichier
    * support du tri manuel des fichiers
    * fonctionne désormais avec la "picture factory" - ce qui permet le chargement différé (lazy-load) des réglages d'image
    * l'option "Lecture seule" (readonly) est désormais possible
    * la restriction de sélection "fichiers uniquement" a été étendue à "dossiers uniquement" - par défaut, fichiers et dossiers restent proposés
    * support de la taille d'image pour une lightbox avec des valeurs issues des réglages de mise en page
    * une image de remplacement peut être sélectionnée
    * option indiquant si un lien de téléchargement est protégé via la session ou non ; pour des raisons de
      rétrocompatibilité, la valeur est définie via une migration si la case "lien de téléchargement" est activée ; si
      la protection est désactivée, aucun cookie n'est défini par la fonction et la page peut être mise en cache
* Date
    * dans les réglages du masque de saisie, on peut définir quelle partie du timestamp doit être "mise à zéro",
      afin par exemple d'enregistrer l'heure sans indication de jour, ou une date sans complément d'heure - cela peut
      être important pour un filtrage correct par heure ou par date
* Sélection unique [select]
    * avec la nouvelle interface ITranslatedMetaModel, un alias traduit peut désormais être utilisé dans les
      réglages de l'attribut pour l'alias - jusqu'ici, il devait s'agir d'un attribut avec des valeurs "unique"
    * avec le passage à l'interface ITranslatedMetaModel, l'API attend, pour la méthode `widgetToValue`, la valeur
      de donnée sélectionnée comme alias pour l'attribut - jusqu'ici fixée sur `id`
    * le widget en `readonly` fonctionne désormais correctement dans le masque de saisie ; également dans le popup-picker
    * un filtre activé dans les réglages de l'attribut a désormais aussi un effet sur la sortie en frontend - par
      exemple, les items référencés ne sont plus affichés lorsqu'un filtre les restreint, de manière analogue à
      l'affichage en backend
      (`à prendre en compte pour le "SQL personnalisé" <https://metamodels.readthedocs.io/de/latest/cookbook/filter/custom-sql.html#filterunterscheidung-von-frontend-und-backend>`_)
* Recherche assistée par Levenshtein (indexation en texte intégral avec recherche par similarité)
    * renommage vers l'orthographe correcte ("sht" au lieu de "sth") - à vérifier dans composer.json
    * la désactivation automatique de l'autosubmit pour le CE/module MM-Filter a été supprimée - grâce aux
      nouvelles possibilités de réglage, cela n'est plus nécessaire
    * possibilité de régler la longueur des mots (min + max) recherchée dans l'index
    * explication des possibilités de réglage au niveau de l'attribut
    * l'autocomplétion du widget de recherche en frontend est passée de Mootools à "Vanilla Script", devenant ainsi
      indépendante de Mootools - *veillez à sélectionner le (nouveau) template*
    * l'autocomplétion peut être désactivée et une longueur minimale de caractères peut être indiquée
    * dans les réglages du filtre, le template correspondant doit être choisi pour l'autocomplete ; celui-ci peut
      aussi être désactivé via une case à cocher - on peut en outre activer l'envoi du formulaire lors du clic sur une
      entrée en autosubmit
* Sélection multiple [tags]
    * avec la nouvelle interface ITranslatedMetaModel, un alias traduit peut désormais être utilisé dans les
      réglages de l'attribut pour l'alias - jusqu'ici, il devait s'agir d'un attribut avec des valeurs "unique"
    * avec le passage à l'interface ITranslatedMetaModel, l'API attend, pour la méthode `widgetToValue`, la valeur
      de donnée sélectionnée comme alias pour l'attribut - jusqu'ici fixée sur `id`
    * le widget en `readonly` fonctionne désormais correctement dans le masque de saisie ; également dans le popup-picker
    * un filtre activé dans les réglages de l'attribut a désormais aussi un effet sur la sortie en frontend - par
      exemple, les items référencés ne sont plus affichés lorsqu'un filtre les restreint, de manière analogue à
      l'affichage en backend
      (`à prendre en compte pour le "SQL personnalisé" <https://metamodels.readthedocs.io/de/latest/cookbook/filter/custom-sql.html#filterunterscheidung-von-frontend-und-backend>`_)
* Rating ("notation par étoiles")
    * passage de Mootools à "Vanilla Script", devenant ainsi indépendant de Mootools
    * tri en backend tenant compte du nombre d'évaluations
* Tableau de texte
    * réglages pour indiquer le nombre min. et max. de lignes
    * case à cocher pour désactiver le tri manuel
* Alias traduit
    * générateur de slug pour les caractères spéciaux
    * option pour empêcher le préfixe "id-" pour les nombres
* Case à cocher traduite
    * les icônes personnalisées optionnelles sont rendues sous forme de miniatures 16x16px
    * un jeu d'icônes propre peut être sélectionné par langue
    * dans la vue en liste, les icônes suivent désormais l'ordre dans lequel les langues du modèle sont définies -
      auparavant, l'icône de la langue de repli (fallback) était toujours en première position
    * si les cases à cocher sont en `readonly`, elles sont affichées dans la vue en liste, mais n'ont pas de fonction de bascule
    * support de l'option "Inverse", qui inverse le comportement d'affichage ; cela permet de reproduire le
      fonctionnement du ContaoCore pour les éléments de contenu, qui sont par nature toujours visibles et peuvent
      être rendus invisibles via une case à cocher. Attention : les icônes dans la vue en liste du backend changent
      également en conséquence.
* ContentArticle traduit
    *  un aperçu des éléments créés, avec leur type et leur visibilité, est disponible aussi bien dans le masque
       de saisie que dans la vue en liste
* Fichier traduit
    * support du tri manuel des fichiers
    * fonctionne désormais avec la "picture factory" - ce qui permet le chargement différé (lazy-load) des réglages d'image
    * l'option "champ obligatoire" est désormais disponible
    * l'option "Lecture seule" (readonly) est désormais possible
    * la restriction de sélection "fichiers uniquement" a été étendue à "dossiers uniquement" - par défaut, fichiers et dossiers restent proposés
    * support de la taille d'image pour une lightbox avec des valeurs issues des réglages de mise en page
    * une image de remplacement peut être sélectionnée
    * option indiquant si un lien de téléchargement est protégé via la session ou non ; pour des raisons de
      rétrocompatibilité, la valeur est définie via une migration si la case "lien de téléchargement" est activée ; si
      la protection est désactivée, aucun cookie n'est défini par la fonction et la page peut être mise en cache
* Tableau de texte traduit
    * réglages pour indiquer le nombre min. et max. de lignes
    * case à cocher pour désactiver le tri manuel


Filtre
------
* CE/module filtre frontend et réinitialisation du filtre (clear all)
    * l'autosubmit du CE/module filtre frontend est désormais écrit en Vanilla Script, donc indépendant de Mootools ou jQuery
    * le CE/module de réinitialisation du filtre dispose désormais de son propre template (mm_clearall_default.html5),
      qui est également présélectionné à la création. Jusqu'ici, il fallait changer manuellement le template de
      "mm_filter_default" à "mm_filter_clearall" lors de la création. Lors de la migration, un message s'affiche si
      un template personnalisé "mm_filter_clearall*.*" est encore trouvé, invitant à effectuer ce changement - ils
      ne peuvent malheureusement pas être adaptés automatiquement. Si un message d'erreur apparaît en frontend
      indiquant que l'ancien template est introuvable, veuillez réenregistrer le CE/module frontend une fois.
    * les widgets pour les filtres frontend ont désormais la propriété "used" avec les valeurs "true|false" -
      "true" si le widget est utilisé
    * l'affichage du compteur pour les widgets du filtre frontend n'est plus supporté - les templates ont été
      adaptés en conséquence.
      `explication voir Github <https://github.com/MetaModels/core/issues/312#issuecomment-686963070>`_
    * pour le CE/module MM-Filter, un fragment d'URL peut désormais être indiqué - la page se positionne ainsi
      sur le point d'ancrage après le rechargement (adapter le cas échéant ses propres templates de type liste de liens)
    * pour le CE/module de réinitialisation du filtre MM, un fragment d'URL peut désormais être indiqué - la page
      se positionne ainsi sur le point d'ancrage après le rechargement
    * les templates pour l'affichage des widgets de filtre ont été retravaillés pour un balisage plus propre -
      `voir le ticket Github <https://github.com/MetaModels/core/issues/374>`_ - adapter le cas échéant ses propres templates
* SQL personnalisé
    * il est désormais possible d'intégrer d'autres inserttags (Contao) dans les inserttags de paramètre - par
      exemple, |br|
      :code:`SELECT * FROM  WHERE year = {{param::get?name=year&default={{date::Y}}}}` |br|
      est désormais possible. De plus, l'inserttag renvoie désormais :code:`null` si la clé de paramètre n'existe pas.
* Requête simple
    * option pour ne pas afficher le libellé du widget de filtre
    * indication d'un ID CSS et de classes CSS possible pour le widget frontend
    * option pour indiquer si la règle de filtre doit afficher un widget frontend (jusqu'à MM 2.0, à régler via
      l'option "paramètre statique" et l'option "paramètre GET" - veuillez effectuer manuellement l'adaptation du réglage)
    * option pour trier les items du filtre selon un "tri naturel" - croissant ou décroissant
    * une case à cocher permet d'afficher le libellé comme option vide (au lieu de "Ne pas filtrer") dans le select
* Sélection unique [select]
    * types d'attribut Alias et Alias traduit possibles
    * option pour ne pas afficher le libellé du widget frontend
    * indication d'un ID CSS et de classes CSS possible pour le widget frontend
    * option pour trier les items du filtre selon un "tri naturel" - croissant ou décroissant
    * une case à cocher permet d'afficher le libellé comme option vide (au lieu de "Ne pas filtrer") dans le select
* Oui / Non
    * en alternative aux valeurs GET "1" et "-1", les valeurs "oui" et "non" peuvent être transmises (ou la
      traduction correspondante)
    * type d'attribut "Case à cocher traduite" possible
    * option pour ne pas afficher le libellé du widget frontend
    * indication d'un ID CSS et de classes CSS possible pour le widget frontend
* Recherche assistée par Levenshtein (indexation en texte intégral avec recherche par similarité)
    * voir sous Attributs
* Sélection multiple [Tags]
    * types d'attribut Alias et Alias traduit possibles
    * option pour ne pas afficher le libellé du widget frontend
    * indication d'un ID CSS et de classes CSS possible pour le widget frontend
    * option pour trier les items du filtre selon un "tri naturel" - croissant ou décroissant
* Registre (filtre par lettre initiale)
    * affichage correct des classes CSS active
    * possibilité optionnelle de filtrer sur plusieurs lettres
    * option pour ne pas afficher le libellé du widget frontend
    * indication d'un ID CSS et de classes CSS possible pour le widget frontend
* Recherche par périmètre (Perimetersearch)
    * nouveau service de lookup "Coordonnées" ajouté. On peut ainsi travailler directement avec les coordonnées et
      intégrer un bouton "Ma position"
    * pour la sélection de plage (range), il est désormais possible de définir une valeur par défaut ; ainsi, si
      les plages proposées sont par exemple 5, 10, 20, 50 km, la valeur par défaut du select en frontend peut être
      fixée à 10 km.
* Valeur de/à pour un champ (from-to)
    * option pour ne pas afficher le libellé du widget de filtre
    * indication d'un ID CSS et de classes CSS possible pour le widget frontend
    * texte de substitution pour le widget frontend
* Valeur de/à pour deux champs (range)
    * option pour ne pas afficher le libellé du widget frontend
    * indication d'un ID CSS et de classes CSS possible pour le widget frontend
    * texte de substitution pour le widget frontend
    * il existe désormais cinq variantes différentes déterminant comment le filtre doit réagir lors de la
      comparaison entre les valeurs présentes en base de données et les valeurs de filtre saisies ; une description
      des variantes peut être consultée via l'assistant d'aide
      |img_help| (popup).


Frontend-Editing (FEE)
______________________
* aperçu des attributs supportés - `voir Github <https://github.com/MetaModels/contao-frontend-editing/issues/15>`_
* possibilité de téléversement de fichiers avec divers paramètres tels que dossier cible, chemins dynamiques,
  nettoyage des noms de fichiers ainsi que des images d'aperçu, entre autres - en option avec support de Dropzone.js
  pour un ou plusieurs fichiers
* support des attributs "sélecteur de couleur" et "URL", chacun affiché avec deux champs de saisie.
* configuration des boutons du masque de saisie dans le FEE, avec option pour la page de redirection et
  "Ne pas enregistrer" ; l'option de la page de redirection peut être définie dynamiquement avec des "Simple Tokens"
* intégration du Notification Center pour l'envoi d'e-mails lors de la création/copie/modification/suppression
  d'enregistrements dans le FEE
* support du "`MCW <https://github.com/contao-community-alliance/contao-multicolumnwizard-bundle>`_" dans le FEE
  (en Vanilla Script), par exemple pour l'attribut Tableau de texte et Tableau multiwidget, pour la duplication et
  le tri des lignes
* support du min/max pour l'attribut Tableau de texte et Tableau multiwidget en frontend
* dans le masque de saisie FEE, les widgets ont désormais une classe CSS composée de `prop-<nom-colonne-attribut`,
  ce qui permet de mieux les organiser/styliser en CSS
* une exception propre est levée lorsqu'un enregistrement ne peut pas être supprimé
* dans le CE/module "MetaModels Frontend-Bearbeitung" (édition frontend), un template personnalisé peut désormais
  être choisi pour le wrapper - le template standard intègre un JavaScript et un CSS pour l'actualisation du masque
  en fonction des conditions d'affichage ; un autre template est également disponible, qui ne contient pas ces
  deux fichiers intégrés

Captures d'écran
----------------

Réglages pour la pagination et le tri dans la liste MM :

|img_settings-pagination-sort|

.. _check_upgrade_mm220:
Vérification pour la mise à jour vers MM 2.2
--------------------------------------------

En principe, une mise à jour au sein de la branche MM 2.x est possible sans problème, et les adaptations
nécessaires aux libellés ainsi que les modifications de base de données sont prises en charge par les migrations.
Il y a toutefois quelques points que celles-ci ne peuvent pas gérer, ou seulement très difficilement. C'est
pourquoi il convient de garder à l'esprit les points suivants lors du passage à MM 2.2 :

* les développements personnalisés doivent être vérifiés pour savoir si la méthode "widgetToValue" des attributs
  Select et Tags reçoit bien la valeur pour "Alias" telle que sélectionnée dans les réglages de l'attribut - par
  exemple lors du traitement de données de formulaire ; jusqu'ici, un ID était toujours attendu
* pour la pagination, le paramètre GET n'est plus simplement "page", mais une clé unique est générée pour chaque
  pagination - qui le souhaite peut la remplacer via les nouveaux réglages de pagination
* si la pagination ne s'affiche pas en frontend après la mise à jour, ouvrir le CE/module frontend Liste dans le
  backend et l'enregistrer à nouveau - l'attribution du nouveau template de pagination se met alors en place
* les liens de pagination peuvent être complétés par un fragment d'URL (ancre) - adapter le cas échéant ses propres templates
* le CE/module frontend "Clear all" dispose désormais de son propre template - à vérifier le cas échéant
* adapter le cas échéant ses propres templates pour les widgets de filtre au nouveau template
* pour la règle de filtre "Requête simple" avec un affichage de widget souhaité en frontend, une case à cocher
  distincte doit être activée dans la règle de filtre
* les filtres réglés pour les attributs Select et Tags s'appliquent désormais aussi à l'affichage en frontend ;
  s'ils ne doivent servir qu'au filtrage du masque de saisie, la requête doit être adaptée le cas échéant -
  `voir ici <https://metamodels.readthedocs.io/de/latest/cookbook/filter/custom-sql.html#filterunterscheidung-von-frontend-und-backend>`_
* le support JavaScript est désormais passé à "Vanilla-Script" dans le core, les attributs et les filtres - les
  dépendances à jQuery ou Mootools disparaissent ainsi. Veuillez adapter vos propres scripts le cas échéant.
* pour les attributs Select et Tags, une restriction WHERE peut être indiquée - lorsque la relation pointe vers
  une table qui n'est pas une table MM. Il faut alors utiliser l'alias de table "t" pour Tags et "sourceTable" pour Select.
* pour la recherche assistée par Levenshtein, tenir compte de la nouvelle orthographe (sht au lieu de sth) ainsi
  que de la sélection du template pour l'autocomplétion dans les réglages de la règle de filtre

Diverses fonctionnalités sont désormais disponibles "out-of-the-box", comme par exemple l'image de remplacement,
de sorte que d'éventuelles adaptations personnalisées peuvent être supprimées.


Refinancement
-------------
.. seealso:: Pour un refinancement de ces travaux considérables, l'équipe MM demande une contribution
   financière. Comme ordre de grandeur, il convient de prendre l'ampleur du projet à réaliser et de
   prévoir environ 10 % - d'après l'expérience des contributions passées, il s'agit de montants
   compris entre 100 € et 500 € (hors taxes) - une facture incluant la TVA est bien sûr toujours
   établie. `Plus... <https://now.metamodel.me/de/unterstuetzer/spenden>`_

.. |img_about| image:: /_img/icons/about.png
.. |img_help| image:: /_img/icons/help.svg
.. |img_settings-pagination-sort| image:: /_img/screenshots/metamodel_new_features/settings-pagination-sort.jpg

.. |br| raw:: html

   <br />
