.. _rst_extended_translator-bridge:

Translator-Bridge pour MetaModels
===================================

Avec la Translator-Bridge, des boutons pour la **traduction automatique comme par ex. DeepL** |deepl_icon| sont
intégrés directement dans le masque d'édition du backend Contao. D'un simple clic, l'extension transmet le contenu
du champ de la langue de repli au fournisseur de traduction configuré et saisit automatiquement le résultat dans le
champ de traduction en cours d'édition.

Pour en savoir plus sur le sujet : :ref:`Multilinguisme dans MetaModels <component_multi-language>`.

.. note:: L'extension Translator-Bridge est encore en financement participatif et ne sera débloquée qu'une fois le
   montant cible actuel de 2 562,50 € atteint. |br|
   Une installation anticipée est possible via le "programme Early-Adopter" –
   `voir ci-dessous <#early-adopter-programm>`_

Actuellement, **DeepL** est pris en charge comme fournisseur de traduction – aussi bien l'API Free-Tier gratuite que
l'API Pro. L'extension est conçue de manière ouverte, de sorte que d'autres fournisseurs (par ex. ChatGPT,
LibreTranslate) peuvent être ajoutés en tant que services Symfony propres –
`voir ci-dessous <#fournisseurs-de-traduction-personnalises>`_.

Le bouton apparaît exclusivement lorsque :

* un MetaModel multilingue est en cours d'édition,
* la langue d'édition active **n'est pas** la langue de repli et
* le champ d'attribut est traduisible et non protégé en écriture.

.. note:: En option, la traduction peut également être activée pour les contenus Contao -
   `voir ci-dessous <#traduire-les-elements-de-contenu-contao>`_

Prérequis
---------

* à partir de MetaModels core 2.4
* à partir de Contao 5.3.x
* Clé API valide du fournisseur de traduction concerné
  (par ex. DeepL Free ou Pro)


Installation via Contao-Manager ou Composer
---------------------------------------------

.. code-block:: bash

   composer require metamodels/translator-bridge


Configuration
-------------

Après l'installation, la clé API du fournisseur de traduction est enregistrée dans la
configuration Symfony. Pour cela, créez dans le dossier du projet le fichier
``config/config.yaml`` ou modifiez-le :

.. code-block:: yaml

   meta_models_translator_bridge:
       deepl_api_key: '%env(DEEPL_API_KEY)%'

La clé elle-même doit être saisie dans le fichier ``.env.local``
(jamais directement dans le fichier YAML, afin qu'elle ne soit pas publiée, par ex. via un dépôt) :

.. code-block:: bash

   DEEPL_API_KEY=dein-deepl-schluessel-hier

.. note:: Les clés Free-Tier de DeepL se terminent par ``:fx`` et utilisent automatiquement
   le point de terminaison API gratuit ``api-free.deepl.com``. Les clés Pro sans ce suffixe
   utilisent ``api.deepl.com``. L'extension détecte le type de clé automatiquement.


Variantes linguistiques préférées
-----------------------------------

Pour certaines langues, DeepL distingue des variantes régionales – par ex. l'anglais
britannique (``EN-GB``), l'anglais américain (``EN-US``) ou le portugais brésilien
(``PT-BR``). Le réglage ``preferred_language_variant`` permet de définir la variante à
utiliser pour une langue cible :

.. code-block:: yaml

   meta_models_translator_bridge:
       deepl_api_key: '%env(DEEPL_API_KEY)%'
       preferred_language_variant:
           en: en-GB
           pt: pt-BR

La clé est le code de la langue cible (tel qu'il est utilisé par ex. dans le champ
``mm_lang`` ou comme langue d'édition active), la valeur est la variante DeepL souhaitée.
Cette association ne s'applique **exclusivement** qu'à la langue cible de la traduction.

.. note:: Des codes de langue cible DeepL valides doivent être utilisés. La liste complète
   se trouve dans la
   `documentation DeepL <https://developers.deepl.com/docs/getting-started/supported-languages>`_.
   Une valeur invalide (par ex. ``en-BR``) entraîne le rejet de la requête par DeepL avec
   une erreur (HTTP 400).

Après des modifications de la configuration, videz le cache Symfony :

.. code-block:: bash

   php bin/console cache:clear


Utilisation dans le masque de saisie d'un enregistrement
------------------------------------------------------------

Dès que l'extension est configurée, un petit bouton avec le logo du fournisseur de
traduction (par ex. le logo DeepL) apparaît à côté de chaque champ d'attribut traduit.

Un clic sur le bouton |deepl_icon| :

1. lit le contenu du champ dans la langue de repli,
2. l'envoie au fournisseur de traduction,
3. et saisit le résultat traduit directement dans le champ de saisie actuel.

|translator_01|

Les champs avec contenu HTML (par ex. les champs TinyMCE ou zone de texte avec balises)
sont automatiquement détectés et traduits avec le mode HTML correspondant, de sorte que
la structure du balisage soit conservée.

Les inserttags Contao (par ex. ``{{link::123}}`` ou ``{{env::request}}``) sont
automatiquement remplacés par des espaces réservés internes avant la traduction, puis
restaurés ensuite – ils ne sont donc **pas** traduits et restent inchangés dans le
résultat.

Le résultat peut être retravaillé manuellement avant l'enregistrement – l'extension
n'écrase jamais automatiquement une valeur déjà enregistrée ; elle ne fait que remplir le
champ de saisie dans le navigateur.

.. tip:: Avec le raccourci clavier :kbd:`Alt+T` (macOS : :kbd:`Option+T`), tous les champs
   traduits du masque d'édition actuel sont traduits en une seule fois – sans devoir
   cliquer sur chaque bouton individuellement.


Attributs pris en charge
-------------------------

Le bouton est affiché pour les types d'attributs traduits suivants :

* :ref:`Texte traduit <component_attribute_translatedtext>`
* :ref:`Texte long traduit <component_attribute_translatedlongtext>`
* :ref:`Alias traduit <component_attribute_translatedalias>`
* :ref:`URL traduite <component_attribute_translatedurl>`
* :ref:`Table de texte traduite <component_attribute_translatedtabletext>`
* :ref:`Table multiple traduite (MCW) <component_attribute_translatedtablemulti>`
* :ref:`Article de contenu traduit <component_attribute_translatedcontentarticle>`
  – les boutons apparaissent dans la fenêtre popup de l'élément de contenu


Traduire les éléments de contenu dans le popup
--------------------------------------------------

L'attribut *Article de contenu traduit* ouvre les éléments de contenu dans une fenêtre
popup. Là aussi, les boutons de traduction sont automatiquement affichés à côté de tous
les champs appropriés. La langue cible est alors lue directement à partir du champ
``mm_lang`` de l'élément de contenu, la langue source à partir de la langue de repli du
MetaModel.

.. note:: L'élément de contenu dans le popup doit être enregistré une fois après sa création, afin que
   l'association de langue puisse être créée. Après l'enregistrement, les boutons de traduction sont
   également visibles.

.. note:: Même les éléments de contenu **imbriqués** - par exemple à l'intérieur d'un accordéon, d'un groupe
   d'éléments ou d'un slider - reçoivent les boutons de traduction. La langue cible est alors déterminée
   via la chaîne parent jusqu'à l'enregistrement réellement associé, et pas seulement au niveau de
   l'élément de contenu parent direct.

Sont considérés comme types de champs appropriés : ``text``, ``textarea``, ``inputUnit`` et
``listWizard``. Les règles suivantes s'appliquent :

* Les champs avec une **expression de validation technique** (``rgxp``) sont exclus,
  dans la mesure où il s'agit d'un contenu non linguistique – par ex. date, e-mail,
  téléphone, chiffres ou code de langue. Les champs Alias (``rgxp=alias``) reçoivent en
  revanche **toujours** un bouton.
* Les **champs éditeur ACE** (``rte=ace|…``) ne sont exclus que si une syntaxe de code y
  est définie (par ex. ``ace|php``, ``ace|css``, ``ace|json``). Les syntaxes
  ``ace|html`` et ``ace|markdown`` sont considérées comme du contenu traduisible – les
  champs correspondants (par ex. l'élément de contenu *HTML* ou l'élément de contenu
  *Markdown*) reçoivent également un bouton.


Administration MetaModels avec des saisies multilingues
------------------------------------------------------------

Dans l'**administration MetaModels** – par ex. lors de la création ou de la modification
d'attributs – des champs comme *Légende* ou *Texte de description* apparaissent sous
forme de tableau multilingue (MultiColumnWizard avec des lignes de langue). Le bouton de
traduction y est intégré directement dans chaque ligne de langue autre que la langue de
repli.

Un clic sur le bouton |deepl_icon| dans une ligne de langue :

1. lit la valeur de la **ligne de la langue de repli** du même champ,
2. l'envoie au fournisseur de traduction,
3. et saisit le résultat traduit dans le champ de saisie de la ligne de langue cible
   correspondante – la ligne de repli reste inchangée.

|translation-attributes|

.. tip:: Le raccourci clavier :kbd:`Alt+T` (macOS : :kbd:`Option+T`) traduit également en une seule fois
   toutes les lignes de ces tableaux multilingues sur la page actuelle.


Traduire les éléments de contenu Contao
------------------------------------------

Par défaut, les boutons de traduction n'apparaissent que dans les champs d'attributs
MetaModels. Pour l'attribut *Article de contenu traduit* (``attribute_translatedcontentarticle``),
les boutons sont **toujours** affichés – la fenêtre popup de l'élément de contenu est
alors automatiquement prise en charge, sans configuration supplémentaire.

Pour étendre les boutons également aux tables Contao générales
(``tl_content`` avec un article parent normal, ``tl_article``, ``tl_page``),
activez le paramètre ``translate_contao`` :

.. code-block:: yaml

   meta_models_translator_bridge:
     deepl_api_key: '%env(DEEPL_API_KEY)%'
     translate_contao: true   # par défaut : false

Enfin, videz le cache Symfony :

.. code-block:: bash

   php bin/console cache:clear

.. note:: La langue source est déterminée automatiquement à partir de l'arborescence des pages Contao :
   l'extension lit le réglage de langue du nœud racine marqué comme **point de départ de repli**
   et le transmet comme langue source explicite au fournisseur de traduction.
   Les boutons n'apparaissent que dans les arborescences de pages ou d'articles qui **ne sont pas**
   l'arborescence de repli elle-même – dans l'arborescence de repli, il n'y a rien à traduire.
   Cela vaut également pour les éléments de contenu **imbriqués** - par exemple à l'intérieur d'un
   accordéon, d'un groupe d'éléments ou d'un slider : la langue source est déterminée via la chaîne
   parent jusqu'à la page ou l'article réellement associé, et pas seulement au niveau de l'élément
   de contenu parent direct.


Afficher l'utilisation des caractères
----------------------------------------

Les fournisseurs qui le prennent en charge (par ex. DeepL) peuvent afficher la
consommation actuelle de leur quota de caractères – à deux endroits :

**Dans la console**, la commande affiche ``<utilisé> / <limite> (<pourcentage>)`` :

.. code-block:: bash

   php vendor/bin/contao-console metamodels:translator:deepl:usage
   # Exemple de sortie : 497 / 500.000 (< 1%)

Le nom de la commande suit le modèle ``metamodels:translator:<identifiant>:usage`` et
est automatiquement mis à disposition pour chaque fournisseur prenant en charge le suivi
d'utilisation.

**Dans le backend**, le raccourci clavier :kbd:`Alt+U` (macOS : :kbd:`Option+U`) ouvre,
sur une page d'édition de traduction, une popup affichant
*« <utilisé> caractères utilisés sur <limite> (<pourcentage>) »*. La popup se ferme via
le ``×``, un clic en dehors de la popup ou la touche :kbd:`Échap`.

.. note:: Les nombres sont affichés avec les séparateurs de milliers de la langue
   respective. Si une consommation existe déjà mais que la valeur arrondie est de 0 %,
   ``< 1%`` est affiché (au lieu de ``0%``).


Messages d'erreur
------------------

Si une traduction échoue, un message d'avertissement rouge apparaît directement sous le
champ concerné. Il disparaît automatiquement après 8 secondes ou par un clic dessus. Le
message technique est en outre consigné dans la console du navigateur.

Causes et messages typiques :

.. list-table::
   :header-rows: 0
   :widths: 50 50

   * - Clé API manquante ou incorrecte
     - *DeepL : échec de l'autorisation – veuillez vérifier la clé API.*
   * - Trop de requêtes (limite de débit)
     - *DeepL : trop de requêtes – veuillez patienter un instant.*
   * - Quota de traduction épuisé
     - *DeepL : quota de traduction épuisé.*
   * - Serveur inaccessible
     - *DeepL : connexion au service de traduction impossible.*


Fournisseurs de traduction personnalisés
--------------------------------------------

L'extension peut être étendue via un tag de service Symfony. Les fournisseurs
personnalisés implémentent l'interface
``MetaModels\TranslatorBridge\Api\TranslatorProviderInterface`` et sont enregistrés
via le tag ``metamodels.translator_provider`` :

.. code-block:: yaml

   # config/services.yaml
   App\Translation\MyProvider:
       tags:
           - { name: metamodels.translator_provider }

L'interface requiert les méthodes suivantes :

* ``getIdentifier(): string`` – identifiant unique (par ex. ``'myprovider'``)
* ``getLabel(): string`` – nom affiché pour le bouton
* ``isAvailable(): bool`` – indique si le fournisseur est opérationnel
* ``translate(string $text, string $sourceLang, string $targetLang): string`` –
  effectue la traduction proprement dite ; en cas d'erreur, une
  ``\RuntimeException`` avec un message **lisible par l'utilisateur** doit être levée
  (pas d'exceptions HTTP brutes)
* ``getSupportedLanguages(): array`` – liste des codes de langues cibles pris en charge

Un fournisseur peut également implémenter en option l'interface
``MetaModels\TranslatorBridge\Api\UsageAwareTranslatorInterface``.
Celle-ci requiert la méthode ``getUsage(): TranslatorUsage`` et active ainsi la
commande console ``metamodels:translator:<identifiant>:usage`` ainsi que
l'affichage :kbd:`Alt+U` dans le backend pour ce fournisseur (voir
`Afficher l'utilisation des caractères <#afficher-l-utilisation-des-caracteres>`_).

Pour que la commande console puisse être nommée correctement, le tag de service doit
contenir l'attribut ``identifier`` (correspondant à la valeur de retour de
``getIdentifier()``) :

.. code-block:: yaml

   # config/services.yaml
   App\Translation\MyProvider:
       tags:
           - { name: metamodels.translator_provider, identifier: myprovider }


Ordre en cas de plusieurs fournisseurs
------------------------------------------

Si plusieurs fournisseurs sont actifs, un bouton propre apparaît pour chacun d'eux par
champ. L'ordre peut être contrôlé via l'attribut ``priority`` –
une valeur plus élevée apparaît plus à gauche (valeur par défaut : ``0``) :

.. code-block:: yaml

   App\Translation\MyProvider:
       tags:
           - { name: metamodels.translator_provider, priority: 10 }

L'icône du fournisseur est intégrée dans le masque de saisie via une instruction CSS :

.. code-block:: css

   button.mm-translate[data-provider="myprovider"]::after {
       background-image: url(../mypath/icons/myprovider.svg);
   }

   html[data-color-scheme="dark"] button.mm-translate[data-provider="myprovider"]::after {
       background-image: url(../mypath/icons/myprovider--dark.svg);
   }


Programme Early-Adopter
-------------------------

Le projet est terminé, mais actuellement pas encore disponible librement.
Le refinancement se fait via un "programme Early-Adopter", c.-à-d. que l'on peut
utiliser l'extension immédiatement moyennant le versement d'un don. Le paiement
autorise l'utilisation pour un projet. Toute prétention juridique est exclue après
le versement d'un don.

Le montant du don devrait être d'au moins 200€*1.

Pour le don, une facture avec TVA indiquée est établie, ou en net pour l'étranger UE en
cas d'identifiant de TVA intracommunautaire existant. |br|
En cas d'intérêt ou de questions supplémentaires, merci d'envoyer un e-mail à info@e-spin.de

*1 Net – TVA éventuellement en sus.


Dons
----

Un grand merci pour les dons* pour cette extension à :

* `AntwortInternet <https://www.antwortinternet.com/>`_ : 680€
* `GUTcert Berlin <https://www.gut-cert.de/>`_ : 680€


(Dons nets)

.. |deepl_icon| image:: /_img/screenshots/extended/translator-bridge/deepl.svg
   :width: 16px
   :height: 16px

.. |translator_01| image:: /_img/screenshots/extended/translator-bridge/translator_01.png
.. |translation-attributes| image:: /_img/screenshots/extended/translator-bridge/translation-attributes.png

.. |br| raw:: html

   <br />
