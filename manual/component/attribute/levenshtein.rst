.. _component_attribute_levenshtein:

|svg_attr_levenshtein_22| |img_levenshtein| Levenshtein
=======================================================

L'attribut « Levenshtein » crée un index de recherche plein texte pour des attributs
MetaModels sélectionnés et permet une recherche par similarité avec une tolérance
d'erreur configurable (fautes de frappe, orthographes proches). Cas d'utilisation
typiques :

* Recherche de produits avec tolérance aux fautes de frappe
* Recherche de noms (par ex. « Meier » trouve aussi « Mayer », « Maier »)
* Recherche plein texte sur plusieurs attributs simultanément

L'attribut lui-même n'enregistre aucune valeur de données propre, mais crée et
entretient un index de recherche séparé. La recherche proprement dite s'effectue via
une règle de filtre dédiée en frontend.


Installation
------------

L'attribut s'installe via le **Contao Manager** ou **Composer** :

.. code-block:: bash

   composer require metamodels/attribute_levenshtein


Réglages lors de la création de l'attribut
-------------------------------------------

L'attribut Levenshtein propose les réglages spécifiques suivants :

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Option
     - Description
   * - Attributs à indexer
     - Sélection de tous les attributs MetaModels dont les valeurs doivent être
       incluses dans l'index de recherche. Plusieurs attributs peuvent être
       sélectionnés simultanément (liste de cases à cocher).
   * - Distance de Levenshtein maximale
     - Assistant à plusieurs colonnes pour configurer l'écart autorisé par
       longueur minimale de mot. Pour chaque longueur minimale, la distance de
       Levenshtein maximale est définie :

       * **Longueur minimale du mot** – à partir de quelle longueur de mot la
         distance s'applique
       * **Distance autorisée** – nombre d'écarts de caractères autorisés
         (0–10)

       Réglage par défaut : mots à partir de 3 caractères → distance 1, à
       partir de 5 caractères → 2, à partir de 9 caractères → 5.
   * - Longueur minimale des mots
     - Les mots comportant moins de caractères que cette valeur ne sont pas
       inclus dans l'index de recherche (par défaut : ``3``).
   * - Longueur maximale des mots
     - Les mots comportant plus de caractères que cette valeur ne sont pas
       inclus dans l'index de recherche (par défaut : ``20``).


Réglages dans les réglages de rendu
-------------------------------------

L'attribut ne possède pas de réglages de rendu spécifiques, car il ne contient
aucune valeur de données à afficher. Il n'apparaît généralement pas dans les
réglages de rendu.


Réglages dans le masque de saisie
-----------------------------------

L'attribut Levenshtein n'apparaît pas comme champ de saisie dans le masque de
saisie — l'index de recherche est automatiquement mis à jour lors de
l'enregistrement des jeux de données.


Règles de filtre
-------------------

L'attribut Levenshtein met à disposition une règle de filtre propre :

.. list-table::
   :header-rows: 1
   :widths: 30 70

   * - Règle de filtre
     - Remarque
   * - Recherche assistée par Levenshtein
     - Recherche par similarité dans l'index de recherche avec tolérance aux
       fautes de frappe. Prend en charge les jokers (``*`` et ``?``). Dans les
       réglages du filtre, un paramètre d'URL, un template et des options
       d'autocomplétion (nombre minimal de caractères, envoi automatique)
       peuvent être configurés.


Fonctions particulières
-------------------------

**Stockage**

L'attribut n'enregistre aucune valeur propre dans la table du MetaModel. L'index
de recherche est stocké dans deux tables dédiées : ``tl_metamodel_levenshtein``
contient une entrée par jeu de données indexé, ``tl_metamodel_levenshtein_index``
les mots qui en résultent (colonnes : ``word``, ``transliterated``). La table du
MetaModel ne reçoit aucune colonne propre.

.. note:: Jusqu'à MetaModels 2.4, le type d'attribut, les deux tables et deux
   colonnes de ``tl_metamodel_attribute`` étaient mal orthographiés
   ``levensthein`` (le ``h`` et le ``t`` étaient inversés). À partir de
   MetaModels 2.5, tout s'appelle uniformément ``levenshtein`` ; une migration
   renomme automatiquement les installations existantes tout en conservant
   l'index de recherche, voir :ref:`new_in_mm250`.

**Mise à jour de l'index**

L'index de recherche est automatiquement mis à jour via un hook ``modelSaved``
dès qu'un jeu de données MetaModels est enregistré. L'opération de liste du
backend « Reconstruire l'index » (icône dans la liste des attributs) permet de
régénérer entièrement l'index manuellement.

**Autocomplétion**

La règle de filtre prend en charge l'autocomplétion en frontend. Les réglages
du filtre permettent de configurer un nombre minimal de caractères à partir
duquel les suggestions apparaissent, ainsi que l'envoi automatique du formulaire.

**Mots vides**

Les mots très courts ou très fréquents (mots vides) ne sont pas indexés. En plus
de la longueur minimale configurée, l'extension contient une liste de mots vides
(par ex. les articles anglais comme « a », « an », « are »).

**Prise en charge multilingue**

L'index est créé en tenant compte de la langue — pour les MetaModels
multilingues, la langue active est prise en compte lors de la construction de
l'index.


.. |svg_attr_levenshtein_22| image:: /_img/icons_svg/levenshtein.svg
   :width: 22px
.. |img_levenshtein| image:: /_img/icons/levenshtein.png
.. |br| raw:: html

   <br />
