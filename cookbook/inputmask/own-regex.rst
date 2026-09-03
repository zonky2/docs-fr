.. _rst_cookbook_inputmask_regex:

Masque de saisie : validation RegEx personnalisée
=================================================

Si l'on a besoin d'une validation RegEx personnalisée pour un champ de saisie de
type texte dans un masque de saisie, cela peut être mis en place via le
gestionnaire d'événements suivant.

Pour l'intégrer, c'est-à-dire pour l'activer pour le champ dans le masque de
saisie, la vérification doit d'abord être disponible « avec les moyens du bord
de Contao ».

Pour cela, le hook « addCustomRegex » est créé comme suit - voir
`API : addCustomRegex <https://docs.contao.org/books/api/extensions/hooks/addCustomRegexp.html>`_

.. note:: La description suivante concerne encore Contao 4.4 - les implémentations actuelles devraient être
   placées dans le dossier `src/`

* créer un dossier pour son propre module sous /system/modules - par ex. « /metamodels_mycustoms »
* dans ce dossier metamodels_mycustoms, créer deux autres dossiers « /config » et « /classes »
* dans le dossier /classes, créer le fichier « MyClass.php » comme décrit dans l'API Contao
* dans le dossier /config, créer le fichier « config.php » comme décrit dans l'API Contao
* ajouter également dans le dossier /config le fichier « event_listeners.php » - la clé du tableau $options
  doit être identique à la valeur utilisée lors de la vérification de $strRegexp dans /MyClass ('plz')
* une fois tous les fichiers créés et remplis avec le code source, le fichier « autoload.php » peut être généré
  via les outils de développement du backend Contao, sous « Autoload-Creator »

Dans les réglages d'un champ de saisie d'un attribut de type « Texte », l'entrée « PLZ » devrait ensuite être
disponible lors du choix de la validation RegEx. Si ce n'est pas le cas, videz éventuellement tous les caches
dans le backend et vérifiez les fichiers.

|img_own-regex|


Codes sources
-------------

Les fichiers contiennent le code source suivant :

Fichier /system/modules/metamodels_mycustoms/classes/MyClass.php

.. code-block:: php
   :linenos:

   <?php
   class MyClass
   {
       public function myAddCustomRegexp($strRegexp, $varValue, Widget $objWidget)
       {
           if ($strRegexp == 'plz')
           {
               if (!preg_match('/^[0-9]{4,6}$/', $varValue))
               {
                   $objWidget->addError('Feld ' . $objWidget->label . ' sollte eine gültige PLZ enthalten.');
               }

               return true;
           }

           return false;
       }
   }


Fichier /system/modules/metamodels_mycustoms/config/config.php

.. code-block:: php
   :linenos:

   <?php
   $GLOBALS['TL_HOOKS']['addCustomRegexp'][] = array('MyClass', 'myAddCustomRegexp');


Fichier /system/modules/metamodels_mycustoms/config/event_listeners.php

.. code-block:: php
   :linenos:

   <?php
   use ContaoCommunityAlliance\DcGeneral\Contao\View\Contao2BackendView\Event\GetPropertyOptionsEvent;

   // Gestionnaire d'événements avec priorité « -1 »
   return array
   (
       GetPropertyOptionsEvent::NAME => array(
           array(
               function (GetPropertyOptionsEvent $event) {
                   if (($event->getEnvironment()->getDataDefinition()->getName() !== 'tl_metamodel_dcasetting')
                       || ($event->getPropertyName() !== 'rgxp')) {
                       return;
                   }

                   $options = $event->getOptions();

                   // Clé "plz" identique à la vérification $strRegexp de myAddCustomRegexp
                   $options['plz'] = 'PLZ';

                   $event->setOptions($options);
               },
               -1
           )
       )
   );


Après sa génération, le fichier autoload.php dans /system/modules/metamodels_mycustoms/config devrait
ressembler à ceci

.. code-block:: php
   :linenos:

   <?php
   ClassLoader::addClasses(array
   (
       // Classes
       'MyClass' => 'system/modules/metamodels_mycustoms/classes/MyClass.php',
   ));


**Remarque :** la validation RegEx a été reprise du manuel Contao et ne constitue qu'une vérification très
simple pour les codes postaux allemands. On trouve sur Internet des validations RegEx plus précises, ou l'on
pourrait aussi intégrer ici une vérification par rapport à une liste des codes postaux attribués en Allemagne.


.. |img_own-regex| image:: /_img/screenshots/cookbook/inputmask/own-regex.jpg
