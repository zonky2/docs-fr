.. _component_translations:

Symfony-Translation
====================

.. note:: Symfony-Translation est implémenté à partir de la version 2.3 de MetaModels.

.. _component_translations_info:
Bref aperçu
-----------

Les sorties applicatives de MetaModels dans Contao sont proposées en plusieurs langues. Cela
concerne toutes les sorties de navigation, les libellés et descriptions des widgets de saisie, les
légendes des masques de saisie, etc. mais pas les « données utilisateur » saisies. À partir de la
version 2.3 de MetaModels, cette mise à disposition est assurée par
`Symfony-Translation <https://symfony.com/doc/current/translation.html>`_, qui se distingue par
différents avantages, comme par ex. un bon système de cache.

Pour charger des saisies nouvelles ou modifiées, le cache Symfony-Translations doit être vidé.
Cela peut se faire via la console ou via le Manager.

.. note:: Le vidage du cache Symfony-Translations peut également se faire dans le backend - voir
   Réglages > Maintenance du système > Symfony-Translator |br|
   Attention : seul le cache de l'environnement de travail actuellement configuré (prod ou dev)
   est vidé !

Les traductions elles-mêmes continuent d'être gérées via le site web de
`Transifex <https://app.transifex.com/metamodels/>`_. Chacun peut participer, via Transifex, à la
traduction de notre langue de base, l'anglais, vers d'autres langues.

Les textes de traduction personnalisés existants, créés sous forme de tableau PHP, doivent être
transférés dans un fichier XLIFF (voir « Personnalisation des traductions »).

Contexte
--------

Dans Contao ainsi que dans MetaModels, de plus en plus de composants natifs de Symfony sont
utilisés, remplaçant les développements propres existants. Dans la version 2.3 de MetaModels, la
traduction a été en grande partie migrée vers le composant Symfony
`Translation <https://symfony.com/doc/current/translation.html>`_ et les traductions sont
désormais conservées directement au format XLIFF.

Symfony-Translation offre un très bon système de cache des textes traduits et accélère ainsi la
construction du backend. Ce cache est généré une fois - s'il n'existe pas déjà - au démarrage de
Contao, puis reste disponible pour tous les appels suivants.

Contrairement à d'autres extensions, MetaModels présente la particularité que des saisies sont
également effectuées dans MetaModels qui concernent l'affichage dans le backend - par ex. les
Models dans la navigation principale, le nom et les descriptions des attributs pour les widgets de
saisie, etc. Cela a pour conséquence que le cache de traduction doit être reconstruit lors de
nouvelles saisies ou de modifications de textes. On force cette reconstruction en vidant le cache
- ce qui peut se faire via le Contao-Manager ou via la console.

Le cache se trouve généralement dans les dossiers

- var/cache/dev/translations
- var/cache/prod/translations

Les fichiers XLIFF se trouvent désormais dans les dépôts MM, dans le dossier
``Resources/translations/`` - quelques rares traductions, transmises directement à Contao, ont dû
rester dans ``Resources/contao/languages``.

Les traductions peuvent désormais être facilement vérifiées via la barre d'outils Symfony. Dans le
panneau « Translation », des informations sur les traductions trouvées et non trouvées ainsi que
sur les fallbacks sont listées.


.. _component_translations_modifications:
Personnalisation des traductions
---------------------------------

Les nouvelles surcharges doivent être créées sous forme de fichier XLIFF. La structure peut être
observée dans le fichier dont on souhaite modifier la valeur. Il faut noter que les fichiers
XLIFF sont en version 2.0 pour le DCG et en version 1.2 pour MetaModels - la structure diffère
quelque peu.

Exemple : si l'on souhaite renommer, pour le français, le bouton « Filtrer » en « Recherche », il
faut créer un fichier

- translations/metamodels_filter.fr.xlf ou
- src/Resources/translations/metamodels_filter.fr.xlf

avec le contenu suivant

.. code-block:: xliff
   :linenos:

   <?xml version="1.0" ?>
   <xliff xmlns="urn:oasis:names:tc:xliff:document:1.2" version="1.2">
     <file source-language="en" datatype="plaintext" original="src/CoreBundle/Resources/translations/metamodels_filter.en.xlf" target-language="fr">
       <body>
         <trans-unit id="submit" resname="submit">
           <source>Filter</source>
           <target>Recherche</target>
         </trans-unit>
       </body>
     </file>
   </xliff>

Pour que la modification soit prise en compte, ne pas oublier de vider le cache de traduction !

.. _component_translations_lns:
Message « LABEL NOT SET »
--------------------------

Si le message « LABEL NOT SET » s'affiche comme libellé dans le masque de saisie, cela peut avoir
plusieurs causes :

La raison la plus simple est que le libellé a été modifié, mais que le cache n'a pas été renouvelé
- veuillez le vider (:ref:`voir ci-dessus <component_translations_info>`)

Si des personnalisations propres ont été apportées via le DCA aux widgets de saisie, par ex. pour
des valeurs par défaut ou pour intégrer une icône de wizard personnalisée, la « magie de Contao »
s'applique malheureusement et tente d'ajouter le libellé à partir du tableau des traductions - qui
n'existe cependant plus avec Symfony-Translations.

Le message se corrige facilement en ajoutant en plus un libellé dans le fichier DCA - la valeur
peut rester vide, par ex. pour le MM « mm_employees » et l'attribut « name » :

.. code-block:: php
   :linenos:

   // src/Resources/contao/dca/mm_employees.php or contao/dca/mm_employees.php

   // Add label to fix Contao "magic add".
   $GLOBALS['TL_DCA']['mm_employees']['fields']['name']['label'] = '';

.. |br| raw:: html

   <br />
