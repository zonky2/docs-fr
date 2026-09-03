.. _rst_extended_boilerplate:

"Boilerplate" MetaModels
==========================

.. warning:: Ces informations sont obsolètes et ne devraient plus être utilisées ainsi !

Avec l'extension "Boilerplate" est installé un module Contao pour le
travail avec MetaModels, qui contient différents modèles pour
l'adaptation individuelle de MetaModels.

Dans les fichiers boilerplate, la plupart des adaptations sont
mises en commentaire et doivent, selon les besoins, être
"décommentées" et adaptées au MetaModel existant. Les points
suivants sont préparés comme modèles :

* point de navigation propre pour le backend (actif)
* modèle pour un hook Contao (inactif)
* modèle pour un événement (MM/DCG) (inactif)
* modèle pour des valeurs par défaut du masque de saisie (inactif)


Installation de l'extension "Boilerplate"
--------------------------------------------

Une installation via le gestionnaire d'extensions ou le gestionnaire
de paquets (Composer) n'est pas possible, car lors d'une mise à jour,
vos propres adaptations et réglages seraient écrasés. C'est pourquoi
l'extension doit être transférée "manuellement" sur le serveur par FTP.

L'extension se trouve sur Github à l'adresse `MetaModels/boilerplate/ <https://github.com/MetaModels/boilerplate/>`_
- voir le bouton "Clone or download". Il est conseillé d'enregistrer
l'extension en local et de la transférer sur le serveur après les
adaptations. Le dossier "metamodelsboilerplate" doit pour cela être
copié dans le dossier "/system/modules/".

Les adaptations possibles sont décrites dans les sections suivantes.


Point de navigation propre pour le backend
--------------------------------------------

.. note:: :ref:`rst_cookbook_tips_backend-section`

En tant que fonction de base du module, l'implémentation d'un point
de navigation propre est activée. Une fois l'extension installée sur
le serveur, une nouvelle zone de backend est disponible dans les
réglages du masque de saisie pour le type d'intégration "Indépendant"
(voir la capture d'écran).

|img_backend-integration|

Ce n'est que lorsque le premier MetaModel est attribué à la zone de
backend - et pas avant - que le nouveau groupe de navigation apparaît
dans la navigation de gauche.

L'intitulé du groupe de navigation est adapté dans les fichiers de
langue du dossier "/laguages/de" ou "/languages/en", dans le fichier
"modules.php". Pour changer l'intitulé en "Liste des employés",
il faut modifier l'entrée suivante :

.. code-block:: php
   :linenos:

   <?php
   /**
    * eigene Bezeichnung einer Navigationsgruppe im Backend
    */
   $GLOBALS['TL_LANG']['MOD']['metamodelsboilerplate'] = 'Mitarbeiter';

La position du nouveau groupe de navigation est déterminée dans le
fichier "config.php" du dossier "/config". Avec le code suivant

.. code-block:: php
   :linenos:

   <?php
   /**
    * NAVIGATION
    *
    * Add own navigation group at backend
    * include before e.g. "Design"
    */
   $i = array_search('design', array_keys($GLOBALS['BE_MOD']));
   $GLOBALS['BE_MOD'] = array_merge(array_slice(
       $GLOBALS['BE_MOD'], 0, $i),
       array('metamodelsboilerplate' => array()
       ),
       array_slice($GLOBALS['BE_MOD'], $i)
   );

le groupe de navigation est intégré avant "design" (intitulé "Layout").
La navigation du backend pourrait ensuite se présenter comme suit :

|img_backend-navigation|

Lors de l'intégration au backend, une icône propre peut également
être attribuée au MetaModel, à condition que le fichier icône se
trouve sous "/files/...". Un jeu d'icônes complet est par exemple
`"Fugue Icons" <http://p.yusukekamiyamane.com/>`_.


Modèle pour un hook Contao
----------------------------

Un modèle pour un hook Contao se trouve dans le dossier "/classes"
avec le fichier "MyMetaModelClass.php".

Informations sur les hooks Contao : voir le `manuel Contao <https://docs.contao.org/books/manual/3.4/de/07-contao-anpassen/contao-hooks.html>`_

Un exemple en interaction avec MetaModels : voir :ref:`rst_cookbook_inputmask_regex`


Modèle pour un événement (MM/DCG)
------------------------------------

Un modèle pour un hook Contao se trouve dans le dossier "/config"
avec le fichier "event_listeners.php".

Une introduction au travail avec les événements : par exemple
`"Event-Dispatcher" <https://github.com/contao-community-alliance/event-dispatcher>`_.


Modèle pour des valeurs par défaut du masque de saisie
----------------------------------------------------------

Un modèle pour des valeurs par défaut du masque de saisie se trouve
dans le dossier "/config" avec le fichier "config.php".

Plus d'informations sous :ref:`rst_cookbook_inputmask_default-values`



.. |img_backend-integration| image:: /_img/screenshots/extended/boilerplate/backend-integration.png
.. |img_backend-navigation| image:: /_img/screenshots/extended/boilerplate/backend-navigation.png

.. |br| raw:: html

   <br />
