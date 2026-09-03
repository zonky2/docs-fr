.. _component_templates:

Templates dans MetaModels
===========================

Pour la saisie et la sortie des données ainsi que pour le filtrage, MetaModels propose différents
templates. Tous les templates peuvent être personnalisés et chargés comme variantes de template
propres.

Outre les templates listés ici, certains attributs ou extensions peuvent apporter des templates
séparés.


.. _component_templates_twig:
Templates Twig (à partir de MetaModels 2.5)
---------------------------------------------

À partir de MetaModels 2.5, chacun des templates décrits ci-dessous peut également être fourni
sous forme de **template Twig** (``.html.twig``). Si une variante Twig existe, elle est
**prioritaire** par rapport au ``.html5`` classique (frontend et backend, uniquement pour la
sortie HTML - le format ``.text`` reste sur le moteur précédent). Si la variante Twig est absente,
le ``.html5`` continue d'être utilisé sans changement.

Schéma de nommage :

* Le rendu propre à MetaModels (templates de liste/item et d'attribut ainsi que les widgets de
  filtre) se trouve dans le namespace Contao ``@Contao``, sous le sous-groupe ``metamodels/`` :

  * Item/liste ``metamodel_prerendered`` → ``@Contao/metamodels/item/prerendered.html.twig``
  * Attribut ``mm_attr_text`` → ``@Contao/metamodels/attribute/text.html.twig``
  * Widget de filtre ``mm_filteritem_default`` → ``@Contao/metamodels/filter/default.html.twig``

* Les wrappers d'élément de contenu/module Contao conservent leur nom simple dans le namespace
  ``@Contao``, par ex. ``@Contao/ce_metamodel_list.html.twig``,
  ``@Contao/mm_filter_default.html.twig``, ``@Contao/mm_clearall_default.html.twig``,
  ``@Contao/mm_pagination.html.twig`` ainsi que le ``@Contao/mm_actionbutton.html.twig`` séparé
  (les templates de liste l'intègrent via ``include``, de sorte que des templates de bouton
  d'action personnalisés peuvent continuer à le surcharger).

Dans les templates Twig, les mêmes variables que dans le ``.html5`` sont disponibles (par ex.
``{{ raw }}``, ``{{ data }}``, ``{{ additional_class }}``). À partir de MM 2.5, les templates
d'attribut reçoivent en plus ``{{ label }}``, ``{{ colName }}``, ``{{ hideLabels }}`` et
``{{ legacyAttributeWrapper }}`` - voir :ref:`component_templates_attribute-wrapper`. Comme les
templates se trouvent dans le namespace géré ``@Contao``, ils sont modifiables dans le
**Template Studio** de Contao et peuvent être surchargés via les dossiers de thème ainsi que le
répertoire ``templates/`` du projet. Une surcharge existante sur le nom ``.html5`` simple (par ex.
``templates/metamodel_prerendered.html5``) conserve provisoirement la priorité - cette tolérance
disparaît dans MetaModels 3.0.

Les templates Twig propres à un paquet se trouvent - comme dans les bundles de Contao - sous une
racine de namespace (dossier ``twig/`` avec un fichier marqueur vide ``.twig-root``) ; dans le
projet, le dossier ``templates/`` suffit.

Voir aussi :ref:`new_in_mm250`.


.. _component_templates_fe-list:
Liste frontend
--------------

Pour la sortie en frontend, une hiérarchie de templates à trois niveaux est disponible.

Le **premier niveau** correspond aux templates de la liste MetaModels en tant qu'élément de
contenu ``ce_metamodel_list`` ou module FE ``mod_metamodel_list``. Ce template sert de « wrapper »
pour la sortie et est sélectionné dans l'élément de contenu ou le module FE respectif. La sortie de
la liste (« deuxième niveau ») ainsi que la pagination y sont intégrées par défaut.

Le **deuxième niveau** est constitué par le template du rendering ``metamodel_prerendered`` ou
``metamodel_unrendered`` - c'est ici que tous les enregistrements sont affichés dans une boucle.
C'est dans ce template que la plupart des adaptations pour une sortie individuelle sont
généralement effectuées. Ces templates sont sélectionnés dans les réglages du rendering.

.. note:: Le template standard ``metamodel_prerendered`` suffit pour une première sortie et
   affiche tous les attributs activés dans les réglages de rendu. Pour une sortie individuelle, on
   peut créer son propre template sur la base de ``metamodel_prerendered_debug`` et y insérer son
   propre balisage HTML.

Dans le template, on peut accéder à différentes données - par ex.

* ``$this->total``: :ref:`nombre total d'Items <rst_cookbook_frontend_output-item-count>`
* ``$this->data``: tableau avec tous les enregistrements (voir ci-dessous)
* ``$this->generateSortingLink``: :ref:`liens pour changer le tri <rst_cookbook_templates_fe_list_sorting>`
* ``$this->renderSortingLink``: :ref:`liens pour changer le tri <rst_cookbook_templates_fe_list_sorting>`
* ``$this->filterParams``: si la liste est filtrée, on a ici accès aux données du filtre
* ``$this->parameter``: :ref:`rst_cookbook_templates_fe_list_parameters`

Pour la sortie des enregistrements, une boucle sur les données est intégrée dans le template via
``foreach ($this->data as $item)``. Dans chaque ``$item``, on a accès aux nœuds suivants du tableau
d'un enregistrement :

* ``$this->raw``: données brutes de l'enregistrement, y compris les colonnes système comme ``id``,
  ``tstamp``, etc. ; les valeurs numériques ainsi que les dates sont affichées ici telles qu'elles
  sont stockées dans la BD ; pour les attributs de relation, on a ici la possibilité d'accéder
  également à l'enregistrement lié (voir ":ref:`component_relations_standard-relations`") ; pour
  les fichiers, on a accès aux métadonnées, aux chemins, à l'UUID ; etc.
* ``$this->text``: liste avec la sortie sous forme de représentation texte (template du
  « troisième niveau »)
* ``$this->html5``: liste avec la sortie sous forme de représentation HTML (template du
  « troisième niveau »)
* ``$this->attributes``: liste avec la sortie de la valeur « Nom » issue de la configuration de
  l'attribut respectif (:ref:`en cas de multilinguisme, dans la traduction correspondante
  <component_multi-language_attribute>`)
* ``$this->actions``: nœud ``jumpTo`` avec le lien issu des réglages de rendu - généralement le
  lien vers la page de détail ; d'autres indications peuvent aussi être présentes, par ex. issues
  de la :ref:`liste de favoris <rst_extended_notelist>`.
* ``$this->jumpTo``: ce nœud est déprécié - utiliser le nœud ``$this->actions``
* d'autres nœuds, par ex. issus de la :ref:`liste de favoris <rst_extended_notelist>`

La sortie des widgets pré-rendus (prerendered) rend la sortie très simple - mais le rendu a
également un coût en temps de calcul. En cas de très nombreuses sorties simultanées, cela peut
entraîner des problèmes de charge du serveur. En alternative, on peut activer des sorties non
rendues dans le module CE liste MM.

Si l'on souhaite intégrer certaines conditions d'affichage dans le template de liste, par ex.
l'affichage de blocs uniquement si des valeurs sont définies ou ont une valeur particulière, la
vérification de la condition doit toujours se faire avec les valeurs du nœud raw (éventuellement le
nœud text si les templates n'ont pas été adaptés). Dans le nœud html5, des balises sont
généralement toujours présentes, ce qui les rend le plus souvent inutilisables pour une
vérification.

Le template de liste peut recevoir des paramètres supplémentaires pour la sortie FE, par ex. pour
piloter un slider ou pour des traductions, etc. - voir
":ref:`rst_cookbook_templates_fe_list_parameters`".

Le **troisième niveau** est constitué par les templates des attributs ``mm_attr_<type
d'attribut>``. La sélection s'effectue dans les réglages de rendu, pour chaque attribut. Ces
templates sont plutôt modifiés lorsque l'adaptation doit s'appliquer à différents réglages de
rendu - par ex. il existe pour l'attribut Fichier un template de sortie en « ul » et un en « div ».
Dans les réglages d'attribut des réglages de rendu, une classe CSS personnalisée peut également
être transmise au template.

Dans les templates de MM, les templates de Contao peuvent également être intégrés, par exemple
pour obtenir, pour l'attribut Texte, une sortie sous forme d'élément de contenu YouTube - voir
":ref:`rst_cookbook_templates_fe_template_ce_elements`".


.. _component_templates_attribute-wrapper:

Le bloc englobant (à partir de MetaModels 2.5)
..................................................

Jusqu'à MM 2.4, le bloc entourant chaque valeur d'attribut provenait du **template de liste**
(« deuxième niveau ») :

.. code-block:: html

   <div class="field <spaltenname>">
     <div class="label">Beschriftung:</div>   <!-- entfällt bei "Labels verbergen" -->
     <div class="value">…</div>
   </div>

Le template de l'attribut ne fournissait que le fragment le plus interne, généralement un
``<span class="text …">``. Celui qui voulait façonner la sortie se trouvait donc trop bas dans le
DOM et n'avait pas accès au conteneur englobant.

À partir de MM 2.5, le **template de l'attribut** (« troisième niveau ») affiche lui-même ce bloc.
Il devient ainsi possible d'adapter, pour chaque type d'attribut, non seulement la valeur mais
aussi son conteneur.

Pour les sorties existantes, **rien ne change** : dans les réglages de rendu, il existe la
nouvelle option « Wrapper dans le template de liste (ancien comportement, déprécié) ». Une
migration l'active lors de la mise à niveau pour **tous les réglages de rendu existants**, dont la
sortie reste ainsi inchangée. Seuls les réglages de rendu **nouvellement créés** démarrent sans
cette option et reçoivent le bloc depuis le template de l'attribut.

.. note:: L'option est marquée comme dépréciée dès le départ et disparaît dans MetaModels 3.0.
   D'ici là, les templates personnalisés devraient être migrés.

Points à noter :

* Les **templates d'attribut personnalisés** n'affichent pas le bloc tant qu'ils n'ont pas été
  adaptés. Si l'on crée un nouveau réglage de rendu, il y manquera. Il faut alors soit mettre à
  jour le template, soit activer l'option dans ce réglage de rendu.
* **En mode colonnes** de la liste backend (« afficher les colonnes »), aucun bloc n'est affiché -
  l'en-tête de colonne porte déjà le libellé à cet endroit. Le template de liste est de toute façon
  ignoré dans ce mode.
* **Les valeurs vides** se comportent comme auparavant. L'option « Masquer les entrées vides »
  fonctionne sans changement, elle est évaluée à partir de la valeur brute avant l'exécution de
  tout template.
* **Le nœud** ``html5`` contient ensuite le bloc. Celui qui l'utilise en dehors du template de
  liste - par ex. dans du code PHP personnalisé via ``parseAll()`` ou ``parseValue()`` - obtiendra
  des valeurs différentes pour les nouveaux réglages de rendu. Les nœuds ``text``, ``raw`` et
  ``attributes`` restent inchangés ; qui a besoin de données structurées est de toute façon mieux
  servi par ceux-ci.

Le libellé passe dans les deux cas par la même clé de traduction qu'auparavant, c'est pourquoi les
deux-points sont conservés.

Pour qu'un template d'attribut puisse afficher le bloc, il reçoit depuis MM 2.5 ces valeurs
supplémentaires :

* ``label``: le nom traduit de l'attribut (dans la langue active en cas de multilinguisme)
* ``colName``: le nom de colonne, qui sert également de classe CSS sur le conteneur
* ``hideLabels``: indique si « Masquer les labels » est activé dans les réglages de rendu
* ``legacyAttributeWrapper``: indique si le template de liste affiche le bloc - voir ci-dessus

.. note:: Ces valeurs sont résolues dans le Core et transmises toutes prêtes. Un template ne doit
   **pas** les récupérer lui-même via ``settings.getParent()`` : Twig ne connaît pas de
   ``try``/``catch``, et le réglage de rendu ne possède pas toujours une collection parente -
   l'appel décomposerait alors la sortie.

Un template d'attribut personnalisé suit donc ce modèle - le contenu est d'abord collecté, afin
qu'aucun bloc ne soit généré si le résultat est vide :

.. code-block:: twig

   {% set mmFieldContent %}<span class="text meintyp{{ additional_class|default('') }}">{{ raw|default('')|raw }}</span>{% endset %}
   {% if mmFieldContent|trim is not empty %}
       {%- if legacyAttributeWrapper -%}
           {{- mmFieldContent|raw -}}
       {%- else -%}
           <div class="field {{ colName }}">
               {%- if not hideLabels %}<div class="label">{{ 'field_label'|trans({'%field_label%': label}, 'metamodels_list') }}</div>{% endif -%}
               <div class="value">{{ mmFieldContent|raw }}</div>
           </div>
       {%- endif -%}
   {% endif %}

Les templates ``.text`` ne reçoivent **pas** ce bloc - ils fournissent la représentation purement
textuelle.

Pour les templates de liste et d'attribut (« niveaux deux et trois »), il existe des **templates
dans les types ou extension** ``.text`` **et** ``.html5``, toujours avec le même nom de fichier. Le
rendu en ``.text`` est toujours présent et est utilisé dans la sortie aussi bien dans le nœud
``text`` que dans ``raw``. Le fait que le ``.html5`` soit également utilisé dépend des réglages du
réglage de rendu. La sortie peut être influencée par le choix du « format de sortie ». Si aucune
sélection n'y est faite, la sortie standard du site web est utilisée - généralement ``HTML5`` dans
le BE et le FE. Il est cependant aussi possible de fixer la sortie sur un format correspondant
comme par ex. ``Text``.

Si l'on a créé un template individuel en ``html5``, par ex. ``mm_attr_text_special.html5``, la
recherche s'effectue également pour ``mm_attr_text_special.text`` - si celui-ci n'est pas trouvé,
le template standard ``mm_attr_text.html5`` est utilisé. L'affichage pour les templates html5
personnalisés peut être optimisé en créant un template text correspondant - cela raccourcit la
recherche d'un template adapté.

Si l'on souhaite que les templates text soient éditables dans le backend au niveau des templates,
les entrées suivantes doivent être créées dans son propre fichier ``tl_templates.php`` :

.. code-block:: php
   :linenos:

   <?php
   // contao/dca/tl_templates.php
   if (!empty($GLOBALS['TL_DCA']['tl_templates']['config']['validFileTypes'])) {
       $GLOBALS['TL_DCA']['tl_templates']['config']['validFileTypes'] .= ',text';
   }
   if (!empty($GLOBALS['TL_DCA']['tl_templates']['config']['editableFileTypes'])) {
       $GLOBALS['TL_DCA']['tl_templates']['config']['editableFileTypes'] .= ',text';
   }

Outre ``.text`` et ``.html5``, d'autres formats comme ``.json`` ou ``.xml`` pourraient apparaître à
l'avenir - le format ``.xhtml`` n'existe quant à lui plus désormais.

**De plus**, il existe un template pour la sortie de la pagination ``mm_pagination`` et un pour les
boutons d'action ``mm_actionbutton``.


Filtrage frontend
-------------------

Pour la sortie des filtres frontend, il existe un « template wrapper » nommé ``mm_filter_default``,
sélectionné au niveau du CE ou du module FE « Filtre frontend MetaModels ». Dans ce template, le
formulaire est construit et tous les filtres individuels sont affichés dans une boucle.

Pour les règles de filtre, un template correspondant ``mm_filteritem_*`` peut être activé - le
standard est ``mm_filteritem_default``. Outre « default », il existe également d'autres templates
prédéfinis comme « ..checkbox », « ..linklist », « ..radiobuttons ».

Pour les règles de filtre, un ID ou des classes CSS personnalisés peuvent également être transmis.

L'adaptation de la sortie du « réinitialisation du filtre MetaModel » est possible avec le template
``mm_clearall_default``.


Liste backend
-------------

Dans le backend, la sortie peut être influencée via les réglages du réglage de rendu. Dans
l'affichage en liste via ``metamodel_prerendered`` - mais uniquement si la sortie ne s'effectue pas
sous forme de tableau - ainsi que pour les attributs via ``mm_attr_<type d'attribut>``.


Masque de saisie backend
---------------------------

Dans les réglages d'attribut du masque de saisie, des templates personnalisés des widgets backend
peuvent être chargés. Une adaptation serait également possible via les événements du
`DC_G <https://github.com/contao-community-alliance/dc-general/>`_.


Édition en frontend (FEE)
----------------------------

Pour afficher un lien permettant de créer un nouvel enregistrement, il existe pour le « wrapper de
liste » le template ``ce_metamodel_list_edit`` ou ``mod_metamodel_list_edit``.

Sur la page d'affichage du masque de saisie FEE, il existe comme « template wrapper »
``ce_metamodel_frontend_edit`` ou ``mod_metamodel_frontend_edit``. Ce template affiche tous les
widgets de saisie et contient un extrait JavaScript pour les
:ref:`conditions d'affichage <mm_special_visibility-conditions>` - les templates existent également
sans JavaScript sous la forme ``*_nojs``.

Une adaptation des widgets de saisie peut se faire au niveau des attributs dans les réglages de
rendu - il faut noter qu'il ne s'agit pas ici de widgets BE mais de widgets de formulaire (FE) à
créer et à sélectionner.

.. |br| raw:: html

   <br />
