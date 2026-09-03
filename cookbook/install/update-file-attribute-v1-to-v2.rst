.. _cookbook_install_update-file-attribute-v1-to-v2:

Mise à jour des champs de type fichier lors du passage de MetaModels 1.x à 2.x
==============================================================================

Ceux qui n'ont pas encore effectué le passage de Contao 2.x / MetaModels 1.x à Contao 3.x / MetaModels 2.x sont
confrontés au problème suivant : après une mise à jour réussie, les images ou fichiers intégrés ne s'affichent
plus dans le frontend. Cela s'explique par le fait que les champs correspondants sont encore, dans la base de
données, de type text (Contao 2.x / MetaModels 1.x), alors qu'ils doivent être de type blob pour Contao 3.x /
MetaModels 2.x. De plus, les références vers des fichiers ou des dossiers, enregistrées sous forme de texte,
doivent être converties dans les UUID correspondants.

L'instruction suivante décrit comment mettre à jour les champs de type fichier dans lesquels des fichiers
individuels ou des dossiers sont liés comme cibles. Nous partons ici, à titre d'exemple, du principe que nous
avons une installation avec une table **mm_movies** dans laquelle nous voulons mettre à jour les deux colonnes
**image** (fichier individuel) et **assets** (dossier).

#. Mettre à jour Contao, par exemple selon cette instruction : |br|
   `Mise à jour de Contao de 2.11 à 3.5 <https://community.contao.org/de/showthread.php?59748-Update-von-2-11-auf-3-5-Schritt-f%C3%BCr-Schritt>`_
   Veillez à ce que les tables MM ne soient pas supprimées lors de la mise à jour de la base de données.
#. Mettre à jour MM : |br|
   Il faut d'abord supprimer tous les dossiers MM sous */system/modules/*. Basculez ensuite la gestion des
   extensions vers Composer et installez la version actuelle de MM, par exemple entièrement via le paquet
   *metamodels/bundle_all*. |br|
   Après la mise à jour de la base de données, MetaModels 2.x devrait être disponible comme d'habitude dans
   le backend.
#. Gestion des fichiers |br|
   Si ce n'est pas encore fait, vous devriez appeler dans la gestion des fichiers la fonction
   « Synchroniser » afin de synchroniser les fichiers existants avec la base de données.
#. Mettre à jour les attributs |br|
   Appelez maintenant dans MetaModels l'attribut de type fichier correspondant, et mettez à jour ou corrigez-y
   les indications concernant le dossier racine avec la valeur d'avant la mise à jour.
#. Créer une sauvegarde de la base de données


Mettre à jour les champs de base de données pour les sélections de fichier individuel
..........................................................................................

* Ouvrez votre base de données dans phpMyAdmin ou un outil comparable et affichez la vue de structure de votre
  MetaModel (par ex. : mm_movies).
* Créez-y une colonne de sauvegarde pour la colonne de fichier correspondante avec l'instruction SQL suivante :
  ``UPDATE mm_movies SET image_backup=image``
* Modifiez ensuite le type de la colonne de l'attribut fichier en blob : |br|
  ``ALTER TABLE `mm_movies` CHANGE `image` `image` BLOB NULL DEFAULT NULL``
* Ensuite, insérez avec la commande suivante l'UUID des fichiers concernés dans les champs correspondants : |br|
  ``UPDATE mm_movies SET image=(SELECT uuid FROM `tl_files` WHERE tl_files.path=mm_movies.image_backup)``
* Après la mise à jour réussie, supprimez la colonne de sauvegarde.


Mettre à jour les champs de base de données pour les sélections de dossier
...............................................................................

* Appelez dans MetaModels l'attribut de type fichier correspondant, et mettez à jour ou corrigez-y les
  indications concernant le dossier racine avec la valeur d'avant la mise à jour.
* Ouvrez votre base de données dans phpMyAdmin ou un outil comparable et affichez la vue de structure de votre
  MetaModel. Créez-y de nouveau une colonne de sauvegarde pour la colonne de fichier correspondante et copiez-y
  le contenu de la colonne avec l'instruction SQL suivante : |br|
  ``UPDATE mm_movie SET assets_backup=assets``
* Modifiez ensuite le type de la colonne de l'attribut fichier en blob : |br|
  ``ALTER TABLE `mm_movies` CHANGE `assets` `assets` BLOB NULL DEFAULT NULL``
* Recherchez maintenant dans la colonne `backup_assets` les quinze premiers caractères (guillemets compris,
  jusqu'au début du chemin vers le dossier correspondant), qui ressemblent à peu près à ceci :
  ``a:1:{i:0;s:83:"``
* Adaptez maintenant la commande SQL suivante de sorte que la partie de `CONCAT` corresponde à vos
  indications : |br|
  ``UPDATE mm_movies SET assets=CONCAT('a:1:{i:0;s:83:"', (`` |br|
  ``SELECT uuid FROM tl_files WHERE path=SUBSTRING(assets_backup, 16, LENGTH(assets_backup)-16-2)), '";}'``  |br|
  ``) WHERE (``  |br|
  ``SELECT uuid FROM tl_files WHERE path=SUBSTRING(assets_backup, 16, LENGTH(assets_backup)-16-2)``  |br|
  ``) IS NOT NULL``
* Ensuite, les références vers les dossiers devraient à nouveau fonctionner correctement.


.. |br| raw:: html

   <br />
