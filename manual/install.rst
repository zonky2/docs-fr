.. _manual_install:

Install and update MetaModels
==============================

You will need a Contao-LTS-version to be able to install MetaModels
- the current version is Contao 3.5.x


Installation via Composer
-------------------------

MetaModels and all its dependencies can be installed with the `Composer package manager <https://c-c-a.org/ueber-composer>`_
in the Contao backend.

If your Contao installation is already using the new Composer package manager, you can easily install MetaModels by selecting, respectively typing in the package name into the search field, as follows:

* `metamodels/bundle_all <https://packagist.org/packages/MetaModels/bundle_all>`_

Regarding the bundle, you will have to select version "2.0.x" at the moment - this bundle will automaticaly install the complete "MetaModels core" with it. While selecting restrictions you can choose between different stages, such as "bugfix release", "feature release" etc. - the current MetaModels functions will be activated with "feature release".

In case that you don't need all filters and attributes, you can also install them separately or you can select another `Bundle package <https://github.com/MetaModels?query=bundle>`_. The packages mentioned above are grouped together and should meet most requirements.

You can find an overview of your already installed packages in the display of the dependency graph (checkbox) in the Contao Composer client ("Package management"). 

Installaton via Nightly build
------------------------------

Alternatively to the installation via Composer, you can install MetaModels via FTP. To do this, you will have to download the current version of MetaModels from the `project website http://now.metamodel.me/ <http://now.metamodel.me/>`_
unzip it and upload it via FTP to your server. Most of the folders have to be saved into the folder `/system/module` - only two PHP files which are supporting the Ajax functions have to be saved into the Contao root directory.

Afterwards you will have to update the database in the "extension manager".
If the following error message appears  ``Fatal error: Class 'MetaModels\Helper\UpgradeHandler' ....!metamodels-tng-branch/config/runonce_0.php`` you should purge the internal cache. This option can be found in the menu item "Maintenance" of the Contao backend.


Testing of special packages via Composer
----------------------------------------

The bundle 'bundle_all' contains all currently available and released MetaModels packages. Additionally there are packages with bugfixes or brandnew functions that have to be tested. For the MetaModels core this could be e.g. a package called "dev-hotfix-xyz". You can see those packages inter alia on Github within the corresponding repository (e.g. MetaModels/core) in the
`'branches' tab <https://github.com/MetaModels/core/branches>`_.

In case that you want to test a package like this, you'll have to separately select and install it in the package management.
For the selection in the package management, check the checkbox "dependencies i nstalled" and then click on the corresponding package, e.g. 'metamodels/core' and aditionally in the following options click on e.g. 'dev-hotfix-xyz'.

After "Reserve package for installation" you'll have to make some small changes to Composer-JSON. To do this go to the package manager to "settings" and there click onto "expert mode". The displayed JSON file has to be extended with the entry "as 2.0.0" within the node "require". If you happen to have several extra packages you have to do this for every entry.

for example: |br|
``"metamodels/core": "dev-hotfix-xyz"`` modify to |br|
``"metamodels/core": "dev-hotfix-xyz as 2.0.0"``

After the installation via "update packages" you should delete the Composer cache in the "settings" of the package management.

As MetaModels is closely interlinked with the DC_general (DCG), you will frequently need to update to a newer version here as well for testing.
The procedure is the same as for MetaModels including the adjustment of the JSON entry with the "as 2.0.0".

To come back to the initial version , just delete the package in the package management.

Please never forget to provide the MetaModels developer team with your valuable feedback after your test on  
`Github <https://github.com/MetaModels>`_. 


Update MetaModels 
-----------------

If you installed MetaModels via Composer you will also have to update it that way.

With the manual MetaModel installation you have to consider several aspects.
The following procedure has shown itself to be the most efficient: 

* delete ALL old MetaModel folders (you can check which folders these are by double-checking the previous download) - really **ALL**
* Clear the Contao cache -> /system/cache (everything there within this folder)
* **NEVER EVER** do a database update (otherwise all will be gone)
* download the new nightly build files, unzip and upload them (via FTP)
* update the database via /contao/install.php

You can find the most current information in the `forum <https://community.contao.org/de/showthread.php?56725-MetaModels-aktualisieren-%28ohne-Composer%29>`_

Switch MetaModels from "Nightly build" to "Composer"
-----------------------------------------------------

The procedure is similar to "Update MetaModels". By switching to Composer you should consider that Composer is a memory intensive application. Based on experience, you should have at least 100MB. The exact required memory size is dependent on other installed packages and also on the server configuration of your provider.

The following procedure has shown itself to be the most efficient: 

* install Composer
* delete ALL old MetaModel folders (you can see which folders these are by double-checking your previous "nightly" download) - really **ALL**
* Clear the Contao cache -> /system/cache (everything there within this folder)
* **NEVER EVER** do a database update (otherwise all will be gone)
* in Composer select the desired MetaModel version, reserve for installation, then install
* the database update should then automatically being proposed and done

You can find the most current information in the
`forum <https://community.contao.org/de/showthread.php?59961-MetaModels-aktualisieren-%28von-Nightly-Build-zu-Composer%29>`_
.

.. |br| raw:: html

   <br />