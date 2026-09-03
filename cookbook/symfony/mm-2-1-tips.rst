.. _rst_cookbook_symfony_mm-2-1-tips:

Astuces Symfony et MM 2.x
=========================

Pour travailler avec MM 2.x sous Symfony, voici quelques astuces pour bien démarrer
ou comme « pense-bête ».

Les appels en console partent toujours du répertoire d'installation de Contao - c'est-à-dire
là où se trouve le composer.json, donc avant tout appel, il faut d'abord se placer dans ce répertoire :

``cd /var/www/mein-contao``

Ensuite, il faut s'assurer que la version de PHP utilisée en console est la même que celle utilisée pour le
site web (voir dans le Contao-Manager sous Outils > PHPINFO). En console, on peut le vérifier avec :

``php -v``

Si la version de PHP n'est pas identique, il faut appeler les commandes avec un chemin vers le binaire PHP.
Ce chemin est par exemple indiqué lors du contrôle système du Contao-Manager ou dans la documentation/le wiki
du fournisseur.

``/usr/bin/php82 -v``


Mise à jour Composer
--------------------

La commande suivante déclenche une mise à jour :

``/usr/bin/php82 web/contao-manager.phar.php composer update -v``

ou avec attribution de mémoire et de temps d'exécution

``/usr/bin/php82 -d memory_limit=-1 -d max_execution_time=900 public/contao-manager.phar.php composer update -v``

ou pour les installations plus anciennes avec le chemin `web`

``/usr/bin/php82 -d memory_limit=-1 -d max_execution_time=900 web/contao-manager.phar.php composer update -v``

Avec le paramètre « -v », « -vv » ou « -vvv », on obtient différents niveaux de détail de la sortie. Avec le
paramètre supplémentaire « --dry-run », un « test à blanc » est effectué.

Après une mise à jour, appelez éventuellement l'outil d'installation, afin que les modifications de la base
de données soient effectuées (souvent oublié :D).

Le composer.phar devrait être mis à jour régulièrement - pour cela, exécutez la commande suivante :

``/usr/bin/php82 web/contao-manager.phar.php self-update``

La migration de la base de données peut être déclenchée comme suit - :ref:`voir le gestionnaire de schéma <component_schema-manager>`

``/usr/bin/php82 vendor/bin/contao-console contao:migrate``

Déterminer la version d'un paquet
---------------------------------

En cas de message d'erreur ou de question auprès des développeurs, il est important de connaître la version
installée d'une extension. On peut la déterminer via le nom du paquet, par ex. pour le DC_General

``/usr/bin/php82 public/contao-manager.phar.php composer show | grep dc-general``

Avec

``/usr/bin/php82 public/contao-manager.phar.php composer show``

tous les paquets sont affichés.

Pour une version de développement, par ex. obtenue via l'« EAP », il n'y a pas encore de numéro de version -
mais on peut déterminer le numéro du commit actuel à partir du fichier ``composer.lock``. On peut par exemple
y rechercher ``"name": "metamodels/core"``. Dans le nœud ``reference`` se trouve le numéro de commit - les huit
premiers caractères suffisent en général, par ex. ``8da81418``.


Vider le cache
--------------

En cas d'adaptations, vider le cache de Contao :

« Doux » (recommandé) :

``/usr/bin/php82 vendor/bin/contao-console cache:clear --env=prod`` |br|
``/usr/bin/php82 vendor/bin/contao-console cache:warmup``

ou la « manière forte » :

``rm -rf var/cache/{dev,prod}``

qui supprime « tout » dans dev et prod.


.. _rst_cookbook_symfony_mm-2-1-tips_toolbar:
Barre d'outils Symfony
----------------------

La barre d'outils Symfony facilite l'affichage des valeurs des templates et le débogage pendant la
création d'un projet avec MetaModels.

Le mode debug peut être activé depuis le backend ou le Contao-Manager, ou durablement via une entrée dans le
fichier d'environnement ``.env`` ou ``.env.local`` avec l'entrée

``APP_ENV=dev``

L'activation durable ne devrait se faire qu'en local ou sur des sites protégés d'une autre manière.

En mode debug, la mise en cache de Contao est également désactivée et il n'est pas nécessaire de vider le
cache aussi souvent - mais cela signifie aussi que le site peut « avoir un aspect différent ». De plus, la
barre d'outils de débogage de Symfony s'affiche dans le navigateur.

|img_symfony-toolbar|

Si vous devez déboguer quelque chose dans le code source, utilisez la fonction de débogage ``debug()`` de
Symfony - la sortie s'affiche alors dans la barre d'outils de débogage et peut être consultée via l'« icône
de réticule ».

Pour le débogage des templates, une description est disponible ici : :ref:`rst_cookbook_debug_templates`

Si vous souhaitez examiner les appels SQL, par ex. d'une règle de filtre « SQL personnalisé », vous pouvez
aller sur la barre d'outils de débogage dans « Doctrine » - tous les appels SQL y sont listés. Via la
recherche du navigateur et certains éléments comme le nom de la table ou similaire, la requête est
généralement vite trouvée. La barre d'outils propose le code SQL dans différents formats, de sorte que la
requête puisse être facilement reprise et testée dans phpMyAdmin.


Désactiver les avertissements en mode debug
-------------------------------------------

Si vous souhaitez consulter une sortie de débogage, il peut arriver qu'un message d'avertissement empêche
l'affichage de s'effectuer. Le message d'avertissement peut par exemple provenir d'un thème ou d'une autre
extension et n'avoir rien à voir avec MetaModels. Pour que l'affichage souhaité s'affiche malgré tout via la
barre d'outils Symfony, vous pouvez supprimer les avertissements. Pour cela, ajoutez l'entrée suivante dans
le ``config.yml`` :

.. code-block:: php
   :linenos:

    // config/config.yml
    framework:
      profiler:
        only_exceptions: true
    # ou
    contao:
        error_level: 8181


.. |img_symfony-toolbar| image:: /_img/screenshots/cookbook/debug/symfony-toolbar.jpg

.. |br| raw:: html

   <br />
