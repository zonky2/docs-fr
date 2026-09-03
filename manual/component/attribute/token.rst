.. _component_attribute_token:

|svg_attr_token_22| |img_token| Token (à partir de MM 2.4)
============================================================

L'attribut « Token » génère, lors du premier enregistrement d'un
enregistrement, une chaîne de caractères aléatoire d'un point de vue
cryptographique et immuable (jeton). Domaines d'application typiques :

* Numéros de commande ou de dossier uniques (par ex. ``TKN-aB3xYqUK``)
* Clés d'accès ou liens de validation en frontend
* Identifiants de référence internes qui doivent rester stables

Le jeton est généré exactement une seule fois — lors du premier enregistrement,
tant que le champ est encore vide. Chaque enregistrement ultérieur laisse le
jeton existant inchangé. Même un appel direct à ``setDataFor()`` n'écrase pas
un jeton déjà présent (protection en écriture unique au niveau de la base de
données).

.. note:: Le jeton est toujours unique. L'option « Valeurs uniques » dans les
   réglages généraux de l'attribut est donc activée en permanence et ne peut
   pas être désactivée.

.. warning:: Lors de la duplication (copie) d'un enregistrement dans le
   backend, aucun jeton n'est repris. Le nouvel item reçoit automatiquement
   son propre jeton lors de l'enregistrement.


Installation
------------

L'attribut s'installe via le **Contao Manager** ou **Composer** :

.. code-block:: bash

   composer require metamodels/attribute_token


Réglages à la création de l'attribut
-------------------------------------

Outre les réglages généraux de l'attribut (nom, nom de colonne, description,
autoriser la surcharge de variante), l'attribut Token propose les options
spécifiques suivantes :

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Option
     - Description
   * - Jeu de caractères du jeton
     - Caractères utilisés pour la génération aléatoire. Saisies possibles :

       * Caractères simples : ``123ABC`` (chaque caractère pris individuellement)
       * Indication de plage entre crochets : ``[a-z][A-Z][0-9]``
       * Caractères spéciaux directs : ``$%=``
       * Combinaison : ``[A-F][0-9]`` (hexadécimal)

       Par défaut : ``[a-z][A-Z][0-9]`` (alphanumérique). Si le champ est
       laissé vide, cette valeur par défaut s'applique également.
   * - Longueur du jeton
     - Nombre de caractères générés aléatoirement (valeur minimale : 3, par
       défaut : 8).
   * - Préfixe du jeton
     - Texte fixe optionnel placé devant chaque jeton (par ex. ``TKN-`` donne
       ``TKN-aB3xYqUK``). |br|
       Le préfixe n'est pas compté dans la longueur du jeton.

Des exemples d'identifiants uniques sont les `règles applicables aux cartes
d'identité et passeports allemands
<https://de.wikipedia.org/wiki/Ausweisnummer>`_, qui utilisent actuellement
les caractères ``123456789CFGHJKMNPRTVWXYZ`` sur une longueur de 26
caractères, ou le `Record Locator <https://en.wikipedia.org/wiki/Record_locator>`_
que l'on connaît des billets d'avion, avec six caractères parmi
``23456789ABCDEFGHJKMNPQRSTXYZ`` — les caractères 0, 1, O, I, L étant exclus
pour une meilleure lisibilité.

Le nombre de combinaisons possibles ``V`` résulte du nombre de caractères
possibles ``n`` et de la longueur du jeton ``k`` — la formule est
``V = n**k``.

Avec le réglage par défaut ``[a-z][A-Z][0-9]``, soit 62 caractères ``n`` et
une longueur ``k`` de 8, on obtient environ 218 billions de combinaisons
possibles — avec trois caractères, ce n'est plus que 238 328.


Réglages dans les réglages de rendu
--------------------------------------

L'attribut Token ne possède pas de réglages de rendu qui lui soient propres.
Dans la liste des attributs d'un réglage de rendu, les options habituelles
sont disponibles :

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Option
     - Description
   * - Template
     - Choix d'un template personnalisé pour l'affichage de la valeur du
       jeton. Si aucun template n'est indiqué, l'affichage se fait sous forme
       de texte simple.
   * - Classe CSS
     - Classe CSS optionnelle ajoutée à l'élément de sortie.


Réglages dans le masque de saisie
------------------------------------

Lorsque l'attribut Token est ajouté à un masque de saisie, le champ est en
principe en lecture seule (``readonly``) dans le backend. Les options
suivantes sont disponibles :

**Présentation**

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Option
     - Description
   * - Classe backend
     - Classes CSS pour la présentation du champ dans le formulaire backend
       (par ex. ``w50`` pour une demi-largeur, ``clr`` pour un saut de ligne,
       ``long`` pour la pleine largeur).

**Aperçu (recherche backend)**

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Option
     - Description
   * - Utilisable pour la recherche
     - L'attribut est disponible dans le backend comme champ de recherche.

.. note:: Les options « Champ obligatoire », « Toujours enregistrer » et
   « Filtrable » ne sont pas disponibles pour l'attribut Token, car le champ
   est toujours enregistré en interne et est en lecture seule.


Règles de filtre
-------------------

L'attribut Token peut être utilisé avec les règles de filtre suivantes :

.. list-table::
   :header-rows: 1
   :widths: 30 70

   * - Règle de filtre
     - Remarque
   * - Requête simple
     - Filtre les enregistrements selon une valeur de jeton exacte ; utile
       pour les vérifications d'accès basées sur une URL |br|
       (par ex. ``?token=TKN-aB3xYqUK``).
   * - SQL personnalisé
     - Pour des filtrages plus complexes en combinaison avec d'autres
       paramètres.


Fonctions spéciales
---------------------

**Configuration via config.yaml**

Le nombre maximal de tentatives de génération avant qu'une exception ne soit
levée peut être adapté au projet dans ``config/config.yaml`` :

.. code-block:: yaml
   :linenos:

   meta_models_attribute_token:
       max_retries: 5   # Standard: 3

À chaque tentative, il est vérifié si le jeton généré existe déjà dans la
base de données. Si la vérification d'unicité échoue trois fois (ou autant de
fois que configuré), une ``RuntimeException`` est levée.

**Génération de jeton personnalisée par événement**

Via l'événement ``MetaModels\AttributeTokenBundle\Event\GenerateTokenEvent``,
la génération du jeton peut être remplacée ou étendue par du code
personnalisé. Si ``setToken()`` est appelé dans l'écouteur, MetaModels
ignore la génération aléatoire intégrée.

Exemple d'écouteur en tant que ``src/EventListener/MyTokenListener.php`` :

.. code-block:: php
   :linenos:

   <?php

   use MetaModels\AttributeTokenBundle\Event\GenerateTokenEvent;

   class MyTokenListener
   {
       public function onGenerateToken(GenerateTokenEvent $event): void
       {
           $prefix = $event->getAttribute()->get('token_prefix') ?? '';
           $event->setToken($prefix . strtoupper(bin2hex(random_bytes(8))));
       }
   }

Enregistrement dans ``config/services.yaml`` :

.. code-block:: yaml
   :linenos:

   App\EventListener\MyTokenListener:
       tags:
           - name: kernel.event_listener
             event: MetaModels\AttributeTokenBundle\Event\GenerateTokenEvent
             method: onGenerateToken

Les méthodes disponibles de l'événement :

.. list-table::
   :header-rows: 1
   :widths: 40 60

   * - Méthode
     - Description
   * - ``getAttribute(): Token``
     - Retourne l'attribut Token (accès au jeu de caractères, à la longueur,
       au préfixe).
   * - ``getItem(): IItem``
     - L'item MetaModel en cours d'enregistrement.
   * - ``setToken(string $token)``
     - Définit un jeton personnalisé ; empêche la génération intégrée.
   * - ``getToken(): ?string``
     - Retourne le jeton défini par l'écouteur, ou ``null``.
   * - ``isTokenProvided(): bool``
     - ``true`` si un écouteur a déjà appelé ``setToken()``.

**Protection en écriture unique au niveau de la base de données**

Même si ``setDataFor()`` est appelé directement, MetaModels n'écrase pas une
valeur de jeton déjà présente. La requête UPDATE contient une condition
``WHERE colonne IS NULL OR colonne = ''``, de sorte qu'un champ déjà rempli
reste toujours inchangé.

**Stockage en base de données**

Le jeton est stocké en tant que ``varchar(255) NULL`` dans la table du
MetaModel. Une valeur vide est enregistrée comme ``NULL`` (compatible avec
le mode strict de MySQL).


.. |svg_attr_token_22| image:: /_img/icons_svg/token.svg
   :width: 22px
.. |img_token| image:: /_img/icons/token.png

.. |br| raw:: html

   <br />
