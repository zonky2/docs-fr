.. _rst_cookbook_specials_register-services:

Enregistrement de services
===========================

.. note:: Les possibilités présentées ci-dessous ne sont que des suggestions ou des exemples - pour son propre
   travail, il convient de développer sa propre configuration optimale - pour en savoir plus sur ce sujet, voir la
   `documentation Symfony <https://symfony.com/doc/6.4/index.html>`_.

MetaModels apporte de nombreuses fonctions qu'il suffit d'activer ou de configurer dans le backend. Cela ne permet
cependant pas de couvrir tous les réglages et fonctions imaginables. Pour des tâches de projet individuelles, les
possibilités implémentées peuvent ne pas suffire et doivent être complétées par des adaptations propres.

Différentes méthodes de MM ou aussi de DC_General (DCG) sont disponibles pour réaliser ces tâches en quelques lignes.

En particulier, les événements mis à disposition offrent un moyen simple d'implémenter sa propre logique ou
d'intervenir dans la logique existante. Une introduction au travail avec l':ref:`ref_api` est proposée par exemple par
la `conférence d'Ingolf Steinhardt à la CK23 <https://www.e-spin.de/contao-metamodels/metamodels-vortrag-contao-konferenz-2023.html>`_

Les différentes variantes d'implémentation sont présentées ci-après à l'aide du PrePersistModelEvent. Cet événement
est appelé depuis le masque de saisie « juste avant l'enregistrement en base de données », dès lors que la valeur
d'un champ a été modifiée. Il permet par exemple de manipuler les données saisies ou d'en générer de nouvelles
dynamiquement.

Les EventListeners, tout comme les autres services, s'enregistrent de manière analogue aux
`hooks Contao <https://docs.contao.org/dev/framework/hooks/#registering-hooks>`_.

.. note:: Contao 4.13 et PHP 8 au minimum sont requis. L'exemple détaillé en fin de page utilise toutefois des
   fonctions (par ex. le ``ContentUrlGenerator`` ainsi que des classes ``readonly``) et nécessite donc au minimum
   Contao 5.3 et PHP 8.2.


.. _register-services-with-attribute:
1. Enregistrement par attribut
-------------------------------

L'enregistrement par attribut offre la variante d'implémentation la plus simple - il suffit de créer le fichier
suivant et de vider le cache.

.. code-block:: php
   :linenos:

   <?php
   // src/EventListener/PrePersistModelEventListener.php
   namespace App\EventListener;

   use ContaoCommunityAlliance\DcGeneral\Event\PrePersistModelEvent;
   use Symfony\Component\EventDispatcher\Attribute\AsEventListener;

   #[AsEventListener(PrePersistModelEvent::NAME)]
   class PrePersistModelEventListener
   {
       public function __invoke(PrePersistModelEvent $event)
       {
           if ('mm_employees' !== $event->getEnvironment()->getDataDefinition()?->getName()) {
               return;
           }

           $model = $event->getModel();
       }
   }

Après avoir vidé le cache, l'enregistrement peut être vérifié comme suit

``php vendor/bin/contao-console debug:event-dispatcher dc-general.model.pre-persist``

La clé ``dc-general.model.pre-persist`` figure dans la classe correspondante et peut également être utilisée comme
paramètre dans l'attribut. Si l'enregistrement a réussi, l'entrée marquée devrait apparaître.

|img_register-services_01.png|

Si ce n'est pas encore le cas, l'exécution d'un ``composer install`` peut résoudre le problème.

Lorsque la méthode exécutée s'appelle ``__invoke``, la clé de l'attribut peut être écrite directement sur le nom de
la classe, comme dans l'exemple - si l'on souhaite utiliser un nom de méthode individuel, par ex. lorsque plusieurs
méthodes d'une même classe sont associées à différents événements, la clé de l'attribut doit être placée sur le nom
de méthode correspondant.

Cette variante ne fonctionne sous cette forme simple que si aucun autre événement, etc. n'est enregistré via le
``services.yml``. Si c'est le cas, on peut soit passer entièrement à l'enregistrement via ``services.yml`` - voir le
point 2 - soit ajouter les lignes suivantes dans le ``services.yml`` pour forcer un chargement automatique :

.. code-block:: yaml
   :linenos:

   # config/services.yml
   services:
     _defaults:
       autowire: true
       autoconfigure: true
       public: false

     App\:
       resource: '../src/*'


.. _register-services-with-services:
2. Enregistrement sans attribut via services.yml
--------------------------------------------------

Comme alternative à l'enregistrement par attribut, on peut faire l'appel via le `services.yml` - en particulier si
l'on a différents réglages et que l'on ne souhaite pas se fier à l'enregistrement automatique.

La classe se présente alors comme suit :

.. code-block:: php
   :linenos:

   <?php
   // src/EventListener/PrePersistModelEventListener.php
   namespace App\EventListener;

   use ContaoCommunityAlliance\DcGeneral\Event\PrePersistModelEvent;

   class PrePersistModelEventListener
   {
       public function __invoke(PrePersistModelEvent $event)
       {
           if ('mm_employees' !== $event->getEnvironment()->getDataDefinition()?->getName()) {
               return;
           }

           $model = $event->getModel();
       }
   }

Il faut de plus ajouter l'entrée suivante dans le ``services.yml`` :

.. code-block:: yaml
   :linenos:

   # config/services.yml
   services:
     App\EventListener\PrePersistModelEventListener:
       tags:
         - { name: kernel.event_listener, event: dc-general.model.pre-persist }

Si la méthode ne porte pas le nom ``__invoke``, le nom de la méthode doit être ajouté aux tags du ``services.yml`` -
il est en outre possible d'indiquer une priorité. Pour en savoir plus, voir
`Symfony <https://symfony.com/doc/6.4/event_dispatcher.html>`_


.. _register-services-with-attribute-and-other:
3. Enregistrement par attribut et intégration d'autres services
--------------------------------------------------------------------

Si l'on a besoin, dans sa classe, d'accéder à d'autres services, on peut les intégrer automatiquement via le
``constructor``.

.. code-block:: php
   :linenos:

   <?php
   // src/EventListener/PrePersistModelEventListener.php
   namespace App\EventListener;

   use ContaoCommunityAlliance\DcGeneral\Event\PrePersistModelEvent;
   use MetaModels\IFactory;
   use Symfony\Component\EventDispatcher\Attribute\AsEventListener;

   #[AsEventListener(PrePersistModelEvent::NAME)]
   class PrePersistModelEventListener
   {
       public function __construct(private readonly IFactory $factory)
       {
       }

       public function __invoke(PrePersistModelEvent $event)
       {
           if ('mm_employees' !== $event->getEnvironment()->getDataDefinition()?->getName()) {
               return;
           }

           $model = $event->getModel();

           $anotherMetaModel = $this->factory->getMetaModel('mm_another_model');
       }
   }


.. _register-services-with-services-and-other:
4. Enregistrement sans attribut via services.yml et intégration d'autres services
------------------------------------------------------------------------------------

Si l'on a besoin, dans sa classe, d'accéder à d'autres services, on peut les intégrer via le ``constructor`` en
transmettant le service comme argument dans le ``services.yml``.

.. code-block:: php
   :linenos:

   <?php
   // src/EventListener/PrePersistModelEventListener.php
   namespace App\EventListener;

   use ContaoCommunityAlliance\DcGeneral\Event\PrePersistModelEvent;
   use MetaModels\IFactory;

   class PrePersistModelEventListener
   {
       public function __construct(private readonly IFactory $factory)
       {
       }

       public function __invoke(PrePersistModelEvent $event)
       {
           if ('mm_employees' !== $event->getEnvironment()->getDataDefinition()?->getName()) {
               return;
           }

           $model = $event->getModel();

           $anotherMetaModel = $this->factory->getMetaModel('mm_another_model');
       }
   }

.. code-block:: yaml
   :linenos:

   # config/services.yml
   services:
     App\EventListener\PrePersistModelEventListener:
     arguments:
       - '@metamodels.factory'
       tags:
         - { name: kernel.event_listener, event: dc-general.model.pre-persist }


.. _register-services-all-in-src:
5. Tous les fichiers dans src/ et namespace App
--------------------------------------------------

Si l'on souhaite, pour simplifier la maintenance des données, regrouper tous les fichiers - y compris par ex. le
`service.yml` - de manière compacte dans le dossier `src/` tout en travaillant avec le namespace `App`, on peut
consulter l'exemple de la `conférence d'Ingolf Steinhardt à la CK23
<https://www.e-spin.de/contao-metamodels/metamodels-vortrag-contao-konferenz-2023.html>`_, voire télécharger le
dossier `src/` pour le tester et adapter le ``composer.json`` en conséquence.

Il faut prêter attention à l'entrée
`foo <https://github.com/e-spin/vortrag-contao-konferenz-2023/blob/main/src/Resources/config/foo.yml>`_ -
elle est nécessaire pour contourner une partie de la « magie Contao » liée au namespace...


.. _register-services-all-in-src-own-namespace:
6. Tous les fichiers dans src/ et bundles propres
-----------------------------------------------------

Si l'on souhaite travailler avec un namespace propre et moins de magie Contao ou Symfony, il faut créer davantage de
fichiers dans ``src/``. Cela peut par exemple être utile lorsqu'on souhaite travailler avec plusieurs bundles
séparés et leurs namespaces respectifs. Dans ce cas, on créerait des sous-dossiers supplémentaires, par ex.
``src/ProjectOneBundle``.

Si ce n'est pas le cas, tous les fichiers peuvent être placés directement dans ``src/`` avec le namespace, par ex.
``AppBundle``.


.. _register-services-example-of-services:
Exemples de services et de leur intégration
-----------------------------------------------

.. note:: Les exemples nécessitent au minimum Contao 5.3 et PHP 8.2.

Les deux fichiers suivants présentent des services typiques et la manière de les intégrer :

.. literalinclude:: ./register-services/service.yaml
   :language: yaml
   :linenos:

.. literalinclude:: ./register-services/MetaModelsServiceExamplesListener.php
   :language: php
   :linenos:


.. _register-services-security:
Déterminer l'utilisateur actuel (Security)
-----------------------------------------------

Pour déterminer l'utilisateur frontend actuellement connecté, l'exemple propose trois voies, qui opèrent à des
niveaux différents. La première voie, via ``security.helper``, est recommandée.

**Recommandé** – ``security.helper``

Le ``security.helper`` (``Symfony\Bundle\SecurityBundle\Security``) regroupe l'``AuthorizationChecker`` et le
``TokenStorage``. C'est la seule des trois voies capable à la fois de **vérifier les droits** (``isGranted()``)
*et* de **récupérer l'utilisateur** (``getUser()``). ``getUser()`` renvoie l'objet utilisateur Symfony ; le
``MemberModel`` Contao avec tous les champs de la base de données est ensuite rechargé via ``findByUsername()``.

* *Avantage :* standard moderne, couvre à la fois la vérification des droits et la récupération de l'utilisateur.
* *Inconvénient :* pour les seuls champs de la base de données, une requête supplémentaire est nécessaire.

**Alternative 1** – ``contao.framework`` (Legacy)

La voie classique de Contao via l'adaptateur du framework. Important : pour l'utilisateur *actuel*, c'est le
singleton ``getInstance()`` qui est prévu - ``createInstance()`` créerait une nouvelle instance vide et serait donc
incorrect.

* *Avantage :* fournit directement l'objet utilisateur Contao, y compris les champs de la base de données
  (par ex. ``$member->email``), sans requête supplémentaire.
* *Inconvénient :* spécifique à Contao, aucune vérification des droits, motif obsolète, pertinent uniquement dans le
  scope frontend.

**Alternative 2** – ``security.token_storage`` (bas niveau)

La variante Symfony pure ne fournit que le token ou l'utilisateur - **sans** ``AuthorizationChecker``. C'est
précisément la base sur laquelle repose en interne le ``security.helper``.

* *Avantage :* minimaliste, fonctionne partout.
* *Inconvénient :* ne peut pas vérifier les droits ; la gestion du cas null (non connecté = pas de token) doit être
  traitée soi-même.

En résumé : utiliser ``security.helper`` comme standard. ``token_storage`` uniquement si l'on a délibérément besoin
*uniquement* du token, et ``framework``/``getInstance()`` uniquement pour du legacy ou lorsqu'on a besoin directement
du modèle Contao avec ses champs.


.. |img_register-services_01.png| image:: /_img/screenshots/cookbook/specials/register-services_01.png
.. |img_register-services_02.png| image:: /_img/screenshots/cookbook/specials/register-services_02.png
