.. _rst_extended_metadata_extractor:

File-Metadata-Extractor pour MetaModels
==========================================

.. warning:: L'outil File-Metadata-Extractor est encore en financement
   participatif et ne sera débloqué qu'une fois le montant cible de
   4 200,00 € actuellement atteint. |br|
   Une installation anticipée via le "programme Early-Adopter" est
   possible – `voir ci-dessous <#early-adopter-programm>`_

Le File-Metadata-Extractor lit dans les fichiers ce que l'on appelle des
métadonnées - les métadonnées sont des informations supplémentaires
"cachées" dans le fichier. On connaît par exemple les données EXIF et IPTC,
qui contiennent dans les formats d'image comme JPG/PNG diverses informations
sur la date de la prise de vue, l'exposition, le type d'appareil photo, le
flash, l'auteur, les coordonnées géographiques, etc. Mais des métadonnées
existent aussi dans les formats de texte comme DOC/DOCX/PDF sous forme
d'auteur, de description, etc. De même que les données patient dans les
clichés numériques IRM/scanner/radiographie au format DICOM.

Cet outil permet de simplifier considérablement les saisies, par exemple
pour les bases de données d'images et de vidéos, les collections
bibliographiques, les catalogues au format PDF. Les métadonnées n'ont pas
besoin d'être transférées manuellement par "copier-coller" depuis d'autres
programmes.

Les métadonnées disponibles dépendent du format de fichier correspondant.

Avec le File-Metadata-Extractor, ces données spécifiques peuvent être lues
dans un fichier puis transmises vers un ou plusieurs attributs/champs de
saisie pour être enregistrées dans MetaModels. Une fois les données
enregistrées dans MetaModels, les outils standards de MM comme les filtres
ou la recherche peuvent être utilisés.

La reprise des données se fait de manière transparente dans le masque de
saisie, une fois un fichier sélectionné. Il existe deux modes pour cette
reprise :

* Update metadata : seuls les champs de saisie vides sont alors remplis
* Override metadata : les saisies existantes sont écrasées

Pour indiquer quel champ de métadonnées doit alimenter quel champ de saisie
d'attribut, il existe un tableau de correspondance (mapping) approprié. Dans
ce tableau de correspondance, il est possible, pour chaque ligne, de préciser
une conversion de données. Actuellement sont disponibles :

* substr : pour extraire des parties de texte comme l'extension de fichier
* implode : pour concaténer les données d'un tableau sous forme de chaîne,
  par exemple séparée par des virgules
* format : pour convertir des indications de date et d'heure


Programme Early-Adopter
--------------------------

Le projet est terminé dans sa version 1.0 mais n'est actuellement pas encore
librement disponible. Le refinancement se fait via un "programme
Early-Adopter", c'est-à-dire que l'on peut utiliser la ou les extensions
immédiatement en versant un don. Le paiement autorise l'utilisation pour un
projet. Toute prétention juridique, quelle qu'elle soit, est exclue après
le versement d'un don.

Le montant du don devrait être d'au moins 350 €*1.

Pour l'accès au module, les dépôts sont ouverts via une clé publique SSH
pour une installation via Composer.

Pour le don, une facture avec TVA indiquée est établie, ou en montant net
pour les pays de l'UE disposant d'un numéro de TVA intracommunautaire. |br|
En cas d'intérêt ou pour toute question supplémentaire, merci d'envoyer un
e-mail à info@e-spin.de

*1 Net – TVA éventuellement en sus


Installation via Composer
-----------------------------

Conditions préalables à l'installation :

* MetaModels Core à partir de la version 2.1


Métadonnées prises en charge
--------------------------------

Formats de fichiers :

* jpg
* png

Métadonnées :

* informations natives du fichier comme le nom de fichier, le type MIME
* Exif
* GPS
* IFD
* IPTC
* MakerNote
* Vignette

Le module est conçu de sorte que d'autres formats de fichiers ou
métadonnées puissent être facilement implémentés.


Créer et configurer le File-Metadata-Extractor
---------------------------------------------------

Pour le File-Metadata-Extractor, un attribut Fichier doit être présent.
Les réglages doivent ici être choisis de manière à ce qu'un seul fichier
puisse être sélectionné.

|img_attribute_file|

Les réglages suivants sont effectués pour cet attribut au niveau du masque
de saisie. Dans les réglages, le mapping des métadonnées peut être activé
via une case à cocher. Dans le tableau de correspondance, une entrée des
métadonnées est sélectionnée comme source ainsi qu'un attribut comme cible.
Avec les saisies du "Content modifier", les valeurs peuvent être manipulées
avant leur reprise dans l'attribut cible.

|img_inputmask_widget_file|

Dans le masque de saisie de l'item se trouvent désormais, à côté de la
sélection de fichier de l'attribut Fichier, deux autres boutons pour le
transfert des données vers les champs de saisie. Lorsque l'un des deux est
cliqué, les données sont transférées dans les champs de saisie et peuvent
encore être corrigées/complétées. Ce n'est qu'en enregistrant l'ensemble
de données que les métadonnées sont enregistrées dans MetaModels.

|img_item_inputmask|


Dons
------

Un grand merci pour les dons* en faveur de l'extension à :

* N.N. : 350 €
* Liebchen+Liebchen : 1 210 €
* Liebchen+Liebchen : 350 €
* Liebchen+Liebchen : 450 €
* Liebchen+Liebchen : 570 €
* Liebchen+Liebchen : 400 €


(Dons en net)


.. |br| raw:: html

   <br />


.. |img_attribute_file| image:: /_img/screenshots/extended/metadata_extractor/attribute_file.jpg
.. |img_inputmask_widget_file| image:: /_img/screenshots/extended/metadata_extractor/inputmask_widget_file.jpg
.. |img_item_inputmask| image:: /_img/screenshots/extended/metadata_extractor/item_inputmask.jpg
