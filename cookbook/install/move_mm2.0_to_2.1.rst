.. _cookbook_move_mm2.0_to_2.1:

Migration de MetaModels 2.0 vers 2.1
====================================

La migration de MetaModels 2.0 (Contao 3.5) vers MetaModels 2.1 (Contao 4.4) se déroule selon le même schéma
de migration que celui utilisé généralement pour passer de C3 à C4.

Il existe différentes façons de procéder - en voici une :

* mettre à jour Contao 3.5 avec MM 2.0 - ainsi que toutes les autres extensions
* installer Contao 4 complètement
* installer via le Contao-Manager ou directement via Composer toutes les extensions disponibles sous forme de
  bundle C4
* copier dans /system/modules toutes les extensions pour lesquelles il n'existe pas de bundle
* copier la base de données de C3 vers C4 - ou adapter les identifiants de connexion MySQL vers l'ancienne base

Ensuite, le site devrait à nouveau fonctionner - le cas échéant, refaire un `composer update` ou vider le
cache et mettre à jour la base de données via l'outil d'installation.
