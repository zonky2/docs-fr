.. _component_attribute_translatedcheckbox:

|svg_attr_translatedcheckbox_22| |img_checkbox| Case à cocher traduite
========================================================================

L'attribut « Case à cocher traduite » est la variante multilingue de
l'attribut :ref:`Case à cocher <component_attribute_checkbox>`. Il stocke une
valeur booléenne propre (0 ou 1) pour chaque langue. Les valeurs sont
enregistrées dans la table de traduction dédiée
``tl_metamodel_translatedcheckbox``.

Domaines d'application typiques :

* Publication dépendante de la langue (par ex. publié en français, pas
  encore en anglais)
* Champs oui/non pouvant être définis différemment selon la langue

.. seealso:: La variante monolingue de cet attribut est décrite dans
   :ref:`component_attribute_checkbox`.

.. seealso:: Des indications sur le multilinguisme dans MetaModels se
   trouvent sur la page :ref:`component_multi-language`.


Installation
------------

L'attribut s'installe via le **Contao Manager** ou **Composer** :

.. code-block:: bash

   composer require metamodels/attribute_translatedcheckbox


Réglages à la création de l'attribut
-------------------------------------

Outre les réglages généraux de l'attribut, l'attribut propose les options
spécifiques suivantes :

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Option
     - Description
   * - Désactiver le mode de repli
     - Lorsque cette option est active, les valeurs sont enregistrées pour
       une langue même si elles sont identiques à la valeur de repli — cela
       garantit les filtrages habituels selon la publication par langue.
   * - Icône de bascule
     - Ajoute une icône supplémentaire (« œil ») dans la vue liste du
       backend, permettant de basculer directement le statut (dépendant de
       la langue). Le nom de colonne habituellement utilisé est
       ``published``.
   * - Option d'affichage inversée
     - Inverse le statut de bascule de l'icône : une case cochée
       (valeur ``1``) affiche alors le symbole inactif, une case décochée
       affiche le symbole actif ; utile par ex. pour un champ « Masquer »
       à l'image de l'élément de contenu Contao.
   * - Icône personnalisée
     - Active le choix d'icônes personnalisées. Contrairement à la variante
       monolingue, les icônes peuvent être définies séparément **par
       langue** (assistant multi-colonnes avec choix de la langue, icône
       active et icône inactive).


Réglages dans les réglages de rendu
--------------------------------------

Dans la liste des attributs d'un réglage de rendu, les options habituelles
sont disponibles :

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Option
     - Description
   * - Template
     - Choix d'un template personnalisé pour l'affichage de la valeur de la
       case à cocher. Si aucun template n'est indiqué, l'affichage se fait
       sous forme de texte simple (``1`` si actif ou vide si inactif).

       Le template principalement destiné à l'affichage en liste dans le BE
       est ``mm_attr_checkbox_icon``, qui affiche le statut avec des icônes
       UTF-8 sous forme de ☐ ou ☑ (à partir de MM 2.4).
   * - Classe CSS
     - Classe CSS optionnelle ajoutée à l'élément de sortie.


Réglages dans le masque de saisie
------------------------------------

Lorsque l'attribut est ajouté à un masque de saisie, les options suivantes
sont disponibles :

**Présentation**

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Option
     - Description
   * - Classe backend
     - Classes CSS pour la présentation (par ex. ``w50 cbx m12``).
   * - Template pour le backend
     - Choix d'un template de widget personnalisé pour le formulaire backend.
   * - Template pour le frontend
     - Choix d'un template de widget personnalisé pour l'édition en frontend
       (uniquement si « Frontend Editing » est installé).

**Fonctions**

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Option
     - Description
   * - Champ obligatoire
     - Rend le champ obligatoire.
   * - Enregistrer lors de la modification
     - Le masque de saisie est rechargé par Ajax lorsque la case à cocher
       est basculée (``submitOnChange``). Les données ne sont pas encore
       enregistrées à ce moment-là.

**Aperçu (filtre backend)**

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Option
     - Description
   * - Filtrable
     - L'attribut est disponible dans le backend comme critère de filtrage.


Règles de filtre
-------------------

.. list-table::
   :header-rows: 1
   :widths: 30 70

   * - Règle de filtre
     - Remarque
   * - Statut de case à cocher traduite
     - Vérifie si la valeur de la case à cocher dans la langue active est
       égale à ``1``. Utilisé typiquement pour le contrôle de publication
       dépendant de la langue.


Fonctions spéciales
---------------------

**Stockage**

Les valeurs sont stockées de façon spécifique à la langue dans
``tl_metamodel_translatedcheckbox`` (champs : ``att_id``, ``item_id``,
``langcode``, ``value`` en ``char(1)``). La table du MetaModel ne reçoit pas
de colonne propre.

**Icônes dépendantes de la langue**

Les icônes personnalisées pour actif/inactif peuvent être choisies
différemment selon la version linguistique — par ex. un drapeau FR pour la
publication française et un drapeau GB pour la publication anglaise.

**Langue de repli**

S'il manque une valeur pour une langue, MetaModels se rabat sur la langue de
repli. Les ID sans valeur dans la langue de repli sont traités comme
inactifs (``''``).


.. |svg_attr_translatedcheckbox_22| image:: /_img/icons_svg/checkbox.svg
   :width: 22px
.. |img_checkbox| image:: /_img/icons/checkbox.png
.. |br| raw:: html

   <br />
