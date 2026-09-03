.. warning:: Ces indications ne concernent pas la version actuelle de MetaModels 2.2
   mais la version 2.1 et antérieures

.. _cookbook_install_mm2.0-and-older:

Installation de MM 2.1 et antérieurs
====================================


Installation de MM 2.1 pour Contao 4.4
--------------------------------------

Les conditions d'installation pour MetaModels 2.1 sont :

* un Contao 4.4.x (LTS) fonctionnel et
* PHP 7.1/7.2
* MySQL à partir de 5.5.5 (InnoDB), MariaDB (sans `strict mode`)

Des versions plus récentes de Contao et/ou PHP sont possibles, mais ne sont pas officiellement supportées.


Installation de MetaModels 2.0 pour Contao 3.5
----------------------------------------------

Pour l'installation de MetaModels 2.0 pour Contao 3, une version Contao LTS est requise,
c'est-à-dire un Contao 3.5.x - ainsi que les `prérequis système identiques à ceux de la
Contao LTS <https://docs.contao.org/books/manual/3.5/de/01-installation/den-live-server-konfigurieren.html>`_.

Depuis janvier 2018, MM 2.0 requiert une version de PHP d'au moins 5.6.

Lors d'une mise à jour depuis un « nightly-build », il peut arriver que deux tables du noyau MM ne soient pas
encore présentes et ne puissent pas être créées par la migration Contao. Si c'est le cas, veuillez créer
vous-même les deux tables suivantes :

* tl_metamodel_dcasetting_condition.php
* tl_metamodel_searchable_pages.php


Remarques et instructions pour des versions (encore) plus anciennes de Contao et MM
-----------------------------------------------------------------------------------

:ref:`cookbook_install_update-file-attribute-v1-to-v2`

.. |br| raw:: html

   <br />
