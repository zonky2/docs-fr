.. _rst_cookbook_sql-tips:

Astuces SQL
===========

Même si MetaModels décharge l'utilisateur d'une grande partie du
travail de programmation pur, il faut de temps en temps se plonger
directement dans la couche base de données. Que ce soit pour
vérifier des données ou pour en modifier.

Ces astuces supposent une bonne maîtrise d'outils comme phpMyAdmin
ainsi que les bases de (My)SQL.

Voici quelques astuces pour afficher ou modifier des données :

Afficher les champs BLOB :
***************************

.. code-block:: sql
   :linenos:

   SELECT CONVERT(my_blob_attribute USING utf8) AS 'blob_as_text' FROM table

   > a:5:{s:9:"invoiceid";s:1:"8";s:8:"balance";i:5;s:14:"broughtforward";i:3;s:6:"userid";s:5:"13908";s:10:"customerid";s:1:"3";}


Extraire des données sérialisées :
************************************

.. code-block:: sql
   :linenos:

   SELECT
   SUBSTRING_INDEX(SUBSTRING_INDEX(blob_as_text,';',1),':',-1) AS fieldname1,
   SUBSTRING_INDEX(SUBSTRING_INDEX(blob_as_text,';',2),':',-1) AS fieldvalue1,
   SUBSTRING_INDEX(SUBSTRING_INDEX(blob_as_text,';',3),':',-1) AS fieldname2,
   SUBSTRING_INDEX(SUBSTRING_INDEX(blob_as_text,';',4),':',-1) AS fieldvalue2,
   SUBSTRING_INDEX(SUBSTRING_INDEX(blob_as_text,';',5),':',-1) AS fieldname3,
   SUBSTRING_INDEX(SUBSTRING_INDEX(blob_as_text,';',6),':',-1) AS fieldvalue3,
   SUBSTRING_INDEX(SUBSTRING_INDEX(blob_as_text,';',7),':',-1) AS fieldname4,
   SUBSTRING_INDEX(SUBSTRING_INDEX(blob_as_text,';',8),':',-1) AS fieldvalue4,
   SUBSTRING_INDEX(SUBSTRING_INDEX(blob_as_text,';',9),':',-1) AS fieldname5,
   SUBSTRING_INDEX(SUBSTRING_INDEX(blob_as_text,';',10),':',-1) AS fieldvalue5
   FROM table;


Ici, les chiffres de 1 à 10 correspondent au nombre, respectivement à la position, des
points-virgules dans une chaîne sérialisée. Si l'on reprend le premier exemple, ce serait
``blob_as_text,';',2`` le deuxième point-virgule, donc à ``..."8";s:8...`` et donnerait
comme « fieldvalue1 » un ``"8"``.

Supprimer les guillemets :
***************************

.. code-block:: sql
   :linenos:

   SELECT TRIM(BOTH '"' FROM fieldvalue1) AS 'fieldvalue1_pure' FROM table

Avec cette commande, les guillemets sont supprimés en première et dernière position
dans l'exemple précédent - le résultat serait alors ``8``.

Restriction à une valeur sérialisée dans une clause WHERE :
****************************************************************

Si l'on a par exemple dans l'attribut Sélection multiple ([tags]) une relation vers
la table des utilisateurs (tl_user) et que l'on souhaite ne récupérer que les utilisateurs
d'un groupe d'utilisateurs donné, il faut filtrer sur la colonne ``groups``. Dans ``groups``,
l'appartenance au groupe est cependant stockée sous forme de tableau sérialisé, de sorte
qu'il faut effectuer une recherche dans la chaîne sérialisée.

Dans les réglages de l'attribut Sélection multiple, on peut mettre en place un filtrage SQL
comme suit :

.. code-block:: sql
   :linenos:

   CONVERT(tl_users.groups USING utf8) LIKE '%"2"%'

Ainsi, seuls les utilisateurs du groupe d'utilisateurs ``2`` sont affichés dans le
masque de saisie.

Rechercher des fichiers via l'UUID :
****************************************************************

L'UUID d'un fichier ou d'un dossier peut être consultée dans le gestionnaire de fichiers via
le bouton d'information. La recherche en base de données est un peu plus délicate, car les UUID
ne sont pas stockées « en clair » dans la base. Pour la recherche, il faut d'abord convertir
l'UUID pour la base. Pour cela, il suffit de retirer les tirets de l'UUID et d'ajouter « 0x »
devant. Pour une UUID « 2abbf0c1-e76f-43e5-a123-00ac10d40e00 », cela donnerait par exemple :

.. code-block:: sql
   :linenos:

   SELECT * FROM tl_files
   WHERE uuid = 0x2abbf0c1e76f43e5a12300ac10d40e00

   -- ou via une conversion automatique
   SELECT * FROM tl_files
   WHERE LOWER(CONCAT(
        LEFT(HEX(uuid), 8),
        '-', MID(HEX(uuid), 9,4),
        '-', MID(HEX(uuid), 13,4),
        '-', MID(HEX(uuid), 17,4),
        '-', RIGHT(HEX(uuid), 12))
      ) = '2abbf0c1-e76f-43e5-a123-00ac10d40e00';

