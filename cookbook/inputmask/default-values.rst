.. _rst_cookbook_inputmask_default-values:

Masque de saisie : valeurs par défaut automatiques
==================================================

Les champs de saisie des masques de saisie peuvent être pré-remplis automatiquement avec des valeurs par défaut.
Cela facilite le remplissage des masques de saisie lors de la création d'un nouveau jeu de données.

Via le `BuildDataDefinitionEvent <https://github.com/contao-community-alliance/dc-general/blob/efe5e2de934946e1d51df56797b18d74b1683d12/src/Factory/Event/BuildDataDefinitionEvent.php>`_
du DCG, la valeur par défaut peut être définie - voici un exemple de EventListener correspondant permettant de
pré-remplir l'attribut ``name`` du modèle ``mm_employees`` avec « Moin ».

.. code-block:: php
   :linenos:

   <?php
   // src/EventListener/SetDefaultValueListener.php
   namespace App\EventListener;

   use ContaoCommunityAlliance\DcGeneral\DataDefinition\Palette\PaletteInterface;
   use ContaoCommunityAlliance\DcGeneral\Factory\Event\BuildDataDefinitionEvent;

   class SetDefaultValueListener
   {
       public function __invoke(BuildDataDefinitionEvent $event): void
       {
           // Get container.
           $container = $event->getContainer();
           // Check right table present.
           if ('mm_employees' !== $container->getName()) {
               return;
           }
           // Set default value.
           $container->getPropertiesDefinition()->getProperty('name')->setDefaultValue('Moin');
       }
   }

.. code-block:: yml
   :linenos:

   services:
   # src/Resources/config/services.yml
     App\EventListener\SetDefaultValueListener:
       public: true
       tags:
         - { name: kernel.event_listener, event: dc-general.factory.build-data-definition }


Valeurs par défaut avec du code Legacy
--------------------------------------

.. note:: Les valeurs par défaut avec le code Legacy ne devraient plus être utilisées. À partir de MM 2.3, pour un
          affichage correct du label du champ, une entrée avec une chaîne vide doit en plus être créée - par ex. |br|
          ``$GLOBALS['TL_DCA']['<Nom-Table-MM>']['fields']['<Nom-Colonne-Champ>']['label'] = '';``  |br|
         sinon, au lieu du label, s'affiche « LABEL NOT SET: <column> »

Les champs de saisie de MetaModels doivent être traités (presque) de manière identique aux champs du noyau Contao ou
des extensions habituelles créés avec un tableau DCA. Des différences apparaissent en partie du fait de la génération
dynamique des champs dans MetaModels par le DC-General.

Les valeurs par défaut des champs peuvent être définies en complétant le tableau DCA avec la clé « default » -
`voir le manuel Contao <https://docs.contao.org/dev/reference/dca/fields/>`_.

Pour définir une valeur par défaut, il faut connaître le nom (interne) du MetaModel ainsi que le nom de colonne de
l'attribut. Ces indications peuvent être complétées dans une entrée de tableau de la forme générale suivante

.. code-block:: php
   :linenos:

   <?php
   // contao/dca/<Nom-Table-MM>.php
   $GLOBALS['TL_DCA']['<Nom-Table-MM>']['fields']['<Nom-Colonne-Champ>']['default'] = <Valeur>;

Pour le champ e-mail ([text]) de :ref:`mm_first_index`, la valeur par défaut pourrait ressembler à ceci :

.. code-block:: php
   :linenos:

   <?php
   // contao/dca/mm_mitarbeiterliste.php
   $GLOBALS['TL_DCA']['mm_mitarbeiterliste']['fields']['email']['default'] = '@mmtest.com';

Pour chaque type d'attribut, il existe des indications spécifiques sur la forme sous laquelle les valeurs sont
attendues :

* **Texte** : texte entre guillemets simples par ex. '@mmtest.com' |br|
  ``...['default'] = '@mmtest.com';``
* **Timestamp** : entier pour le timestamp par ex. 1463657005 ou la fonction PHP time() |br|
  ``...['default'] = 1463657005;`` ou |br|
  ``...['default'] = time();``
* **Sélection simple [Select]** : entier de l'ID de la valeur entre guillemets simples |br|
  ``...['default'] = '2';``
* **Sélection multiple [Tags]** : tableau avec les valeurs d'alias issues de la colonne d'alias configurée |br|
  ``...['default'] = ['einkauf', 'marketing'];``
* **Case à cocher (Checkbox)** : true |br|
  ``...['default'] = true;``

Comme on peut le voir avec l'attribut « Timestamp », des valeurs par défaut dynamiques sont également réalisables.
Il serait ainsi également possible de s'appuyer sur des valeurs existantes de MetaModels et de les restituer comme
valeur par défaut - éventuellement après un calcul. Pour accéder à MetaModels, les méthodes de l'API
(:ref:`ref_api_interf_mm`) sont disponibles.

.. |br| raw:: html

   <br />
