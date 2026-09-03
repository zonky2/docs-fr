.. _rst_extended_xliff_ex-import:

XLIFF-Ex-Import pour MetaModels
================================

L'outil XLIFF-Ex-Import permet d'exporter puis de réimporter les contenus
d'une installation Contao en vue d'une traduction. Outre les contenus
habituels de Contao, les contenus multilingues de MetaModels sont
également exportés, respectivement importés.

Pour en savoir plus, voir :ref:`Multilinguisme dans MetaModels <component_multi-language>`.

.. note:: L'outil XLIFF-Ex-Import est encore en phase de financement participatif
   et ne sera débloqué qu'une fois la somme cible actuelle de 5.397,50 € atteinte. |br|
   Une installation anticipée est possible via le "programme Early-Adopter" – `voir plus bas <#programme-early-adopter>`_

L'export produit un `fichier XLIFF <https://de.wikipedia.org/wiki/XML_Localization_Interchange_File_Format>`_
qui peut être relu par les outils de traduction courants. Par exemple avec
l'outil `Poedit <https://poedit.net/>`_. XLIFF est le standard utilisé dans
la collaboration avec les agences de traduction.

Une fois les traductions intégrées dans le fichier XLIFF exporté, celui-ci
peut être réimporté.

L'export et l'import s'effectuent par des appels en console - la
configuration se fait via un fichier YAML à créer soi-même.

Pour l'association des contenus Contao, un fournisseur de mapping (mapping
provider) est nécessaire - actuellement, l'extension
`Changelanguage <https://github.com/terminal42/contao-changelanguage>`_ est supportée.

Les modules/extensions suivants sont actuellement supportés :

* Contao (Core)
* MetaModels (données et backend)
* Isotope 2.x
* RockSolid Custom-Elements

Pour en savoir plus sur la planification et les extensions à venir, `voir plus bas <#possibilites-dextension>`_


Programme Early-Adopter
------------------------

Le projet est terminé en version 1.0 mais n'est actuellement pas encore
disponible librement. Le refinancement se fait via un "programme
Early-Adopter", c'est-à-dire que l'on peut utiliser la ou les extension(s)
immédiatement moyennant le versement d'un don. Ce versement autorise
l'utilisation pour un projet. Toute prétention juridique, quelle qu'elle
soit, est exclue après versement d'un don.

Le montant du don devrait être d'au moins 350 €*1.

Pour le don, une facture avec TVA indiquée est établie, ou en net pour
l'étranger UE en cas de numéro de TVA intracommunautaire existant. |br|
En cas d'intérêt ou pour toute question, merci d'envoyer un e-mail à info@e-spin.de

*1 Net – TVA éventuellement en sus.


Installation via Contao-Manager ou Composer
--------------------------------------------

Prérequis pour l'installation :

* MetaModels core 2.1/2.2/2.3/2.4
* Contao 4.4.x/4.9.x/4.13.x/5.3.x


Configuration
-------------

Après une installation réussie, l'export et l'import doivent être
configurés selon vos propres besoins et souhaits.

Un dossier ``/translations`` est d'abord créé dans le répertoire
d'installation de Contao. C'est là que sont déposés les fichiers XLIFF
exportés, et c'est également de là qu'ils sont relus lors de l'import.

Il faut ensuite créer, dans le dossier du projet de l'installation Contao,
un fichier de configuration ``.translation-jobs.yml``. Ce fichier de
configuration définit ce qui doit être exporté ou importé - par exemple
uniquement Contao, uniquement MM, ou les deux - et permet également d'y
définir des jobs individuels, qui sont lancés via un appel en console.

Le fichier de configuration se divise ainsi en deux sections
``dictionaries`` et ``jobs`` - les paramètres sont les suivants
(`voir aussi l'exemple <#exemple>`_) :

.. note:: si le message suivant apparaît lors du `composer update` |br|
   `No default map builder defined, please install an extension that provides "cyberspectrum_i18n.contao.default_map_builder".` |br|
   c'est le signe qu'une extension telle que `Changelanguage <https://github.com/terminal42/contao-changelanguage>`_ ou équivalent fait défaut

dictionaries
............

* ``*`` Nom de la source : désignation utilisée pour l'appel dans les jobs via ``source`` ou ``target``, ou pour le type ``xliff`` il s'agit de la désignation du fichier .xlf
* ``type`` Type : ``contao``, ``metamodels``, ``compound``, ``memory`` ou ``xliff``
* ``name`` Nom : dépend du type

  * ``contao`` : ``contao``
  * ``metamodels`` : ``<table_name>``
  * ``compound`` : ``*`` librement attribuable
  * ``memory`` : ``*`` librement attribuable
  * ``xliff`` : ``*`` librement attribuable

Les dictionaries de type ``compound`` peuvent à leur tour contenir des
dictionaries existants et les compléter par d'autres sources - `voir l'exemple <#exemple>`_

jobs
....

* ``*`` Nom du job : désignation utilisée pour l'appel en console ou dans un autre job
* ``type`` Type : ``copy`` pour copier les données de traduction, ou ``batch`` pour appeler/regrouper des jobs existants

Type ``copy`` :

* ``source`` : désignation de la source issue des dictionaries
* ``target`` : désignation de la cible issue des dictionaries
* ``source_language`` : code de langue, p. ex. ``en``, ``de``, pour la langue source
* ``target_language`` : code de langue, p. ex. ``de``, ``en``, pour la langue cible
* ``copy-source`` : détermine le comportement lors de la copie de la source vers la cible

  * ``true`` (par défaut) : la source est toujours copiée vers la cible
  * ``if-empty`` : la source n'est copiée vers la cible que si celle-ci est vide ou absente
  * ``false`` : rien n'est copié

* ``copy-target`` : détermine le comportement lors de la copie de la cible vers la source

  * ``true`` (par défaut) : la cible est toujours copiée vers la source
  * ``if-empty`` : la cible n'est copiée vers la source que si celle-ci est vide ou absente
  * ``false`` : rien n'est copié

* ``remove-obsolete`` : détermine la suppression d'un nœud de texte

  * ``false`` (par défaut) : rien n'est supprimé
  * ``true`` : le nœud de texte est supprimé si la source est vide ou n'existe plus

* ``filter`` : liste de filtres RegEx appliqués à l'``id`` du nœud ``trans-unit`` pour exclure certains contenus

Type ``batch``

* ``jobs`` : liste des désignations de jobs à traiter


Export
------

L'export s'effectue via un appel en console avec un nom de job en
paramètre - p. ex.

``php vendor/bin/contao-console i18n:process export-all -c`pwd`/.translation-jobs.yml``

Il est également possible d'exporter une seule langue, si un job
correspondant a été défini - p. ex.

``php vendor/bin/contao-console i18n:process export-en-ru -c`pwd`/.translation-jobs.yml``

Le paramètre ``--help`` affiche tous les paramètres, p. ex. le paramètre
verbeux (``-v, -vv -vvv``) pour des informations plus détaillées sur
l'appel, ou ``--dry-run`` pour une simulation ("essai à blanc").


Import
------

L'import s'effectue de manière analogue à l'export - p. ex.

``php vendor/bin/contao-console i18n:process import-all -c`pwd`/.translation-jobs.yml``

ou

``php vendor/bin/contao-console i18n:process import-en-ru -c`pwd`/.translation-jobs.yml``


Débogage
--------

Il est possible d'examiner le mapping de la traduction pour détecter
d'éventuels problèmes. Actuellement, `ChangeLanguage <https://github.com/terminal42/contao-changelanguage>`_
est disponible comme fournisseur de mapping.

Pour le débogage, l'appel se fait avec les paramètres de la table de la
langue source ainsi que de la langue cible. Le paramètre ``--help``
permet d'afficher un texte d'aide.

Un appel de débogage peut par exemple se présenter ainsi :

``php vendor/bin/contao-console debug:i18n-map tl_article.tl_content en de``

S'ensuit une liste tabulaire du mapping. Le cas échéant, des indications
sur d'éventuels problèmes sont affichées au préalable, comme par exemple :

.. code-block:: bash

   WARNING   [app] Article 17 (index: 0) has no fallback set, expect problems, I guess it is 13
   ["id" => 17,"index" => 0,"guessed" => 13,"msg_type" => "article_fallback_guess"]


Dans ce cas, il convient de rechercher l'article avec l'ID 17 dans le
backend et de vérifier l'indication de l'article de repli (fallback).

.. code-block:: bash

   WARNING   [app] Content element 6997 has different type as element in main. Element skipped.
   ["id" => 6997,"mainId" => 7515,"msg_type" => "article_content_type_mismatch"]

Le fournisseur de mapping "Change-Language" ne permet la référenciation
qu'au niveau des pages. Les articles et leurs éléments de contenu sont
comparés en fonction de leur ordre. Lorsque des différences de type
apparaissent, le message ci-dessus est affiché ; l'ID du CE dans la
langue principale serait ici "7515".

Si, par exemple, des éléments existent dans la langue à traduire qui ne
peuvent pas être identifiés dans la langue principale, le message suivant
apparaît :

.. code-block:: bash

   WARNING   [app] Content element 7956 has no mapping in main. Element skipped.
   ["id" => 7956,"msg_type" => "article_content_no_main"]


Exemple
-------

.. code-block:: yaml
   :linenos:

    dictionaries:
      contao_all:
        type: contao
        name: contao

      combined-content:
        type: compound
        name: content
        dictionaries:
          content: contao_all
          my_staff_export:
            type: metamodels
            name: mm_staff
          # Shorthand version: name as key
          # mm_staff:
          #   type: metamodels
          mm_division:
            type: metamodels
          mm_projects:
            type: metamodels

      mmworkshop:
        type: xliff

    jobs:
      ## Export

      # EN => DE
      export-en-de:
        type: copy
        source: combined-content
        target: mmworkshop
        source_language: en
        target_language: de
        copy-source: true
        copy-target: if-empty
        remove-obsolete: true
        filter:
          - /^content\.tl_article\.[0-9]+\.title$/
          - /^content\.tl_article\.[0-9]+\.alias$/

      # Export all.
      export-all:
        type: batch
        jobs:
          - export-en-de

      ## Import

      # EN => DE
      import-en-de:
        type: copy
        source: mmworkshop
        target: combined-content
        source_language: en
        target_language: de
        copy-source: false
        copy-target: true
        remove-obsolete: false
        filter:
          - /^content\.tl_article\.[0-9]+\.title$/
          - /^content\.tl_article\.[0-9]+\.alias$/

      # Import all.
      import-all:
        type: batch
        jobs:
          - import-en-de

      all:
        type: batch
        jobs:
          - export-all
          - import-all

Les dictionaries ``mm_staff``, ``mm_division`` et ``mm_projects`` sont les
MetaModels traduits - à partir de ``mmworkshop`` est formé le nom de
fichier ``mmworkshop.xlf``. Avec les noms de jobs, p. ex. ``export-all``
ou ``import-all``, les jobs sont appelés en console.

Un fichier XLIFF exporté peut être ouvert et édité dans un éditeur XLIFF
comme `Poedit <https://poedit.net/>`_ - voir la capture d'écran :

|img_poedit|


Possibilités d'extension
-------------------------

Types de sortie

* po
* csv
* xml


Dons
----

Un grand merci pour les dons* reçus pour cette extension à :

* N.N. : 2.700 €
* iMi : 350 €
* Paus medien : 350 €


(Dons en net)


.. |br| raw:: html

   <br />


.. |img_poedit| image:: /_img/screenshots/extended/xliff_ex-import/poedit.png
