.. _component_contentelements:

Éléments de contenu/modules pour la sortie en frontend
==========================================================

.. note:: pour l'affichage en frontend, créer une liste MetaModel
  comme élément de contenu ou module FE ; en option, un filtre
  peut également être créé comme élément de contenu ou module FE

Introduction
------------

Pour la sortie en frontend, un élément de liste et un élément de filtre sont disponibles. Ceux-ci
peuvent être utilisés dans Contao aussi bien comme élément de contenu que comme module FE. Il n'y a
pas de différence dans les options de réglage entre l'élément de contenu et le module.

L'utilisation des modules est intéressante lorsque l'on souhaite afficher la même liste/le même
filtre à plusieurs endroits tout en ne saisissant les réglages qu'une seule fois.

Pour l'affichage en liste, les options de sélection les plus importantes sont le choix du
MetaModel (d'où proviennent les données), le réglage de rendu et le choix du template (comment les
données sont affichées) ainsi que, le cas échéant, le réglage de filtre (quelles données sont
affichées).

Il faut noter qu'une vue détaillée avec un seul Item n'est également qu'une « présentation en
liste », mais avec un filtrage correspondant pour une seule sortie.

Pour les réglages de filtre, les options de sélection les plus importantes sont le choix du
MetaModel (sur quelle base filtrer) et le choix de l'ensemble de filtres (quel filtrage doit être
utilisé).

De plus, pour les filtres, il existe un élément de contenu/module « Réinitialisation du filtre »
permettant de réinitialiser tous les réglages de filtre en frontend.

Pour certaines combinaisons alias-filtre, il peut être nécessaire de définir la priorité de route
dans les réglages de page - voir :ref:`rst_cookbook_tips_set-route-priority`

.. seealso:: Pour stocker des éléments de contenu Contao directement dans un enregistrement
   MetaModels, les attributs :ref:`Contenu d'un article <component_attribute_contentarticle>`
   (monolingue) ou :ref:`Contenu traduit d'un article <component_attribute_translatedcontentarticle>`
   (multilingue) sont disponibles.


Options CE/module Liste
--------------------------

* **Réglages MetaModel** : |br|
  sélection du MetaModel pour la source des données ainsi que l'offset et la limite de la liste
* **Réglage de rendu MetaModel** : |br|
  sélection d'un réglage de rendu créé, sélection du template ce/mod_metamodel_list et une option
  permettant de sortir les données non analysées (unparsed) ; |br|
  le template définit le wrapper qui englobe la liste et contient la liste ainsi que la
  pagination ; si l'on souhaite influencer la sortie des Items de la liste, cela devrait se faire
  dans le template du réglage de rendu (metamodel_prerendered) ; sortir les données non analysées
  peut être avantageux lorsque de très grandes quantités de données doivent être affichées, car
  cela permet d'éviter des analyses de template inutiles/redondantes.
* **Pagination MetaModel** : |br|
  la pagination permet de répartir la sortie de la liste complète en plusieurs pages. La
  surcharge de différents paramètres standard est possible.
* **Filtre MetaModel** : |br|
  sélection d'un ensemble de filtres créé ; |br|
  si l'option « Paramètre statique » est activée pour une règle de filtre « Requête simple », un
  champ de sélection apparaît ici pour choisir une valeur
* **Tri** : |br|
  ici est défini le tri des éléments de la liste. |br|
  Si un tri manuel des Items a été effectué, il convient de choisir « Tri ». Un tri individuel, par
  ex. selon plusieurs attributs, peut être réalisé via la règle de filtre « SQL personnalisé »
  (:ref:`voir le livre de recettes <rst_cookbook_filter_custom-sql_sortierung-der-ausgabe-nach-mehr-als-einem-attribut-fest>`).
  Si le paramètre « Autoriser la surcharge du tri » est activé, le tri peut être surchargé via l'URL,
  par ex. selon le schéma ``/orderBy/<nom de colonne de l'attribut>/orderDir/<DESC || ASC>`` ou en
  tant que paramètre GET. Pour créer les liens de tri, une méthode est disponible permettant de les
  générer pour chaque attribut - pour en savoir plus, voir le
  :ref:`« livre de recettes » <rst_cookbook_templates_fe_list_sorting>`. La surcharge de différents
  paramètres standard est possible.
* **Réglages des paramètres** : |br|
  les réglages des paramètres permettent de transmettre facilement des paramètres personnalisés au
  template - pour en savoir plus, voir le :ref:`« livre de recettes » <rst_cookbook_templates_fe_list_parameters>`


Options CE/module Filtre
---------------------------

* **MetaModel** : |br|
  sélection du MetaModel qui constitue la base du filtrage
* **Réglage de filtre à appliquer** : |br|
  sélection d'un ensemble de filtres créé
* **Attributs** : |br|
  règles de filtre du réglage de filtre qui doivent être affichées en frontend
* **Actualiser lors d'une modification** : |br|
  si l'option est activée, le formulaire de filtre est envoyé directement après une saisie/sélection
  au lieu d'utiliser le bouton de soumission.
* **Page de redirection** : |br|
  la page de redirection est appelée avec les paramètres de filtre de l'URL vers la page
  sélectionnée.

.. note:: Réglages de la page de redirection à partir de MM 2.3

À partir de MM 2.3, il est possible d'indiquer un ID de formulaire. Un autre filtre peut ainsi
prendre en charge le traitement des données - voir :ref:`rst_cookbook_filter_filter-with-forwarding`

La variante précédente, consistant à intégrer le filtre comme module, peut toujours être utilisée
dans MM 2.3.

.. note:: Réglages de la page de redirection jusqu'à MM 2.3

Si l'on souhaite intégrer également le même filtre sur la page de redirection, cela doit se faire
via un module. On peut placer un filtre et la liste sur des pages différentes et définir une page
de redirection au niveau de l'élément de filtre. Cependant, pour que les paramètres GET de la liste
soient générés à partir des paramètres POST de l'élément de filtre, le même élément de filtre doit
être intégré sur la page de la liste - il suffit que l'élément de filtre soit présent en tant
qu'élément de contenu masqué.

Contao effectue une vérification de sécurité selon laquelle seuls des formulaires identiques
peuvent traiter les mêmes données, c'est-à-dire que l'élément de filtre doit être créé comme module
et intégré respectivement sur la page avec le filtre visible et sur la page de liste.

Le déclenchement du filtre peut se faire via un bouton ou automatiquement via JavaScript, lorsque
les valeurs de filtre sont modifiées dans un widget de filtre (case à cocher « Actualiser lors d'une
modification »).

.. note:: Depuis MM 2.2, le JavaScript ne nécessite plus Mootools ni jQuery (« Vanilla Script »).

Si l'on souhaite intervenir dans le déroulement du JavaScript, cela est possible via différents
appels - voir le commentaire dans le fichier JavaScript ``metamodels.js``.

Exemple d'appel personnalisé de 'submitonchange' :

.. code-block:: js
   :linenos:

    <script>
    // Remove 'submitonchange'.
    window.MetaModelsFE.removeClassHook('submitonchange', window.MetaModelsFE.applySubmitOnChange);
    // Add own 'submitonchange'.
    window.MetaModelsFE.addClassHook('submitonchange', (el, helper) => {
        helper.bindEvent({
            object: el,
            type  : 'change',
            func  : (event) => {
                // Your code...
            },
        });
    });
    </script>

Exemple d'appel personnalisé de 'submitonchange' lorsque plusieurs éléments de filtre se trouvent
sur la page :

.. code-block:: js
   :linenos:

    <script>
    window.MetaModelsFE.addClassHook('submitonchange', (el, helper) => {
        // Check right element.
        if (el.withoutChange) {
             return;
        }
        // Remove 'submitonchange'
        helper.unbindEvents({object: el, type: 'change'});
        // Add own 'submitonchange'.
        helper.bindEvent({
            object: el,
            type  : 'change',
            func  : (event) => {
                // Own code...
            },
        });
    });
    </script>

Options CE/module Réinitialisation du filtre
-----------------------------------------------

Cet élément permet d'intégrer un bouton pour réinitialiser toutes les valeurs de filtre (reset). En
réglage, il est possible de choisir un template personnalisé et de définir un fragment d'URL comme
ancre de saut.


Déroulement
-----------

La création de l'élément de contenu ou du module FE se déroule de manière analogue aux éléments
classiques de Contao, y compris les possibilités habituelles, comme l'activation de la protection
d'accès ou l'indication de classes CSS/ID.

.. seealso:: Dans le livre de recettes :

   * :ref:`rst_cookbook_specials_ce_element_for_editors`
   * :ref:`rst_cookbook_templates_fe_redirect_to_list`


.. |img_filter| image:: /_img/icons/filter.png

.. |br| raw:: html

   <br />
