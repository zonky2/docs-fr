.. _rst_extended_isotope:

MetaModels-2-Isotope
#####################

.. warning:: MetaModels-2-Isotope est encore en financement participatif et ne sera débloqué qu'une fois le
   montant restant du financement participatif, actuellement de 6 431,75 €, atteint. |br|
   Une installation anticipée est possible via le "programme Early-Adopter" – `voir ci-dessous <#early-adopter-programm>`_

Le projet "MetaModels-2-Isotope" met à disposition différents composants pour le projet
MetaModels (à partir de 2.1 ou 2.5) afin de transmettre des items (article, produit) depuis
MetaModels vers la boutique en ligne `Isotopeecommerce <https://isotopeecommerce.org>`_ (Isotope)
pour un achat (checkout).

**Prises en charge actuelles :**

* Contao 5.7 + MM 2.5 + Isotope 3.0-dev
* Contao 4.13 + MM 2.3 + Isotope 2.9

La transmission depuis MetaModels se fait via le panier d'Isotope. Le processus d'achat
se poursuit ensuite tel que configuré dans Isotope.

L'utilisation des modules pour MetaModels n'exclut pas que la boutique Isotope soit
également utilisée avec ses produits normaux. Le projet doit permettre d'offrir une
option d'achat supplémentaire lors de l'utilisation de MetaModels, ou également de
compléter Isotope avec les nombreuses possibilités de configuration et de filtrage
de MetaModels.

**Pour tester et comparer** l'extension par rapport à l'Isotope normal, une **boutique
de démonstration** a été mise en place : `https://isotope.metamodel.me <https://isotope.metamodel.me>`_

Le projet a été réalisé par Richard Henkenjohann, Carsten Merz et Ingolf Steinhardt.


Programme Early-Adopter
------------------------

Le projet est terminé en version 2.5 pour Contao 5.7 et Isotope 3.0-dev, mais n'est
actuellement pas encore disponible librement. Le refinancement se fait via un "programme
Early-Adopter", c.-à-d. que l'on peut utiliser la ou les extension(s) immédiatement
moyennant le versement d'un don. Le paiement autorise l'utilisation pour un projet.
Toute prétention juridique est exclue après le versement d'un don.

Il existe deux options pour le don :

* 1 : accès aux trois modules du projet pour l'installation : 390€*1 ou plus
* 2 : en plus du point 1, également la `boutique de démonstration <https://isotope.metamodel.me>`_ : 490€*1 ou plus

L'extension peut être installée via le Contao-Manager ou via la console (composer). La
boutique de démonstration comprend le composer.json, les templates, la base de données
ainsi que les fichiers de démonstration (/files).

Pour la contribution au projet, une facture avec TVA indiquée est établie, ou en net pour
l'étranger UE en cas d'identifiant de TVA intracommunautaire existant. |br|
En cas d'intérêt ou de questions supplémentaires, merci d'envoyer un e-mail à info@e-spin.de
- voir aussi la `page de financement participatif MM <https://now.metamodel.me/de/unterstuetzer/fundraising#isotope>`_.

*1 Net – TVA éventuellement en sus.


Fonctions
---------

Avec l'extension, des items peuvent être transmis depuis MetaModels vers Isotope pour un
processus d'achat et de paiement – il peut s'agir de produits d'un catalogue, de prestations
comme des voyages et événements, ou encore de droits d'accès pour des logiciels ou des logins.

Lors de la transmission vers Isotope, différentes informations de base comme le numéro
d'article, le nom et le prix sont requises comme champs obligatoires.

Si des produits avec un poids ou des quantités sont transmis à Isotope, un attribut pour
le calcul d'un prix de base est disponible en option – les indications de prix de base
sont affichées à partir de la configuration Isotope.

Il est possible de sélectionner un attribut de MetaModels pour la transmission du poids.

Une fonction de filtrage permet d'exclure des items de la livraison.

Il est également possible de définir un attribut fichier comme téléchargement pour
Isotope. Lors de l'implémentation via l'Isotope-Bridge, contrairement à Isotope, les
valeurs pour le nombre de téléchargements possibles et la date de fin du téléchargement
ne sont pas définies.

Si des variantes sont créées dans MetaModels, une transmission vers Isotope est également
possible ici. Il faut noter que dans MetaModels, les variantes (enfants) sont chacune des
enregistrements autonomes.


Composants
----------

Le projet met à disposition trois composants différents :

* isotope-bridge : composant principal pour la configuration
* attribute_isotopeprice : attribut décimal pour la saisie du prix et le choix de la taxe
* attribute_isotopebaseprice : attribut pour le choix du type de prix de base et la saisie de quantité
* attribute_isotopeshippingweight : attribut pour la transmission du poids


Configuration et utilisation
------------------------------

Il est présupposé qu'Isotope est installé et configuré, tout comme MetaModels.

Pour l'utilisation, le composant isotope-bridge doit être installé – l'attribut
attribute_isotopeprice devrait également être disponible. L'attribut
attribute_isotopebaseprice n'est nécessaire que si des indications de prix de base
sont utilisées.

Après l'installation, un nouvel icône avec le symbole Isotope apparaît dans la vue du
MetaModel – celui-ci est gris dans la configuration standard (voir Sweets), c.-à-d. que
l'Isotope-Bridge n'est pas encore activé.

|img_isotope_mm|

Pour l'activer, cliquez sur le crayon d'édition du MetaModel correspondant et cochez la
case "Enable Isotope bridge" dans la section "Réglages avancés". Après l'enregistrement
et la fermeture, l'icône Isotope change et devient colorée (voir Cars) et est alors
disponible pour la configuration.

Avant de configurer l'Isotope-Bridge, les attributs du MetaModel devraient être vérifiés
ou complétés. Les attributs suivants devraient être présents :

Champs obligatoires :

* Nom (attribut Texte, CombinedValues ou similaire)
* Description (attribut Texte long)
* SKU/numéro d'article (attribut Alias, Texte, Numérique ou similaire)
* Prix (attribut Price (Isotope) ou Décimal (les taxes ne sont alors pas possibles))

Optionnel :

* Image (attribut Fichier)
* Prix de base (attribut Baseprice (Isotope))
* Téléchargement (attribut Fichier)
* Poids (attribut Décimal)

Une fois la vérification des attributs effectuée, la configuration peut être ouverte en
cliquant sur l'icône Isotope dans l'affichage des MetaModels. Les attributs mentionnés
ci-dessus sont alors associés aux options et paramètres d'Isotope.

|img_isotope_config|

En complément des réglages de base, deux autres réglages peuvent encore être effectués :

* "Exempt from shipping" définit un filtre pour les items qui ne doivent pas être
  livrés, comme par ex. les téléchargements – de manière analogue au réglage Isotope
* "Jump to render settings" définit le réglage de rendu de MetaModels créé pour
  l'affichage en liste, afin de déterminer l'"adresse jumpTo" pour un affichage détaillé ;
  ce réglage est nécessaire lorsqu'il existe également une page de détail pour les items

Pour l'affichage de l'option d'achat dans le CE/module frontend Liste MetaModels, il faut
encore activer l'Isotope-Bridge. Pour cela, créez ou ouvrez la liste MM correspondante et
activez l'option "Enable Isotope bridge". Les options pour le panier, le nombre d'articles
etc. sont alors disponibles comme dans la boutique Isotope.

|img_isotope_enable_bridge|

Les réglages sont alors terminés et dans la vue en liste en frontend, les boutons configurés
pour l'ajout au panier devraient maintenant être visibles pour chaque item. Toutes les autres
configurations comme le panier et le checkout se font dans Isotope.

|img_isotope_fe-addtocart|

Si un item a été acheté, il ne peut plus être supprimé dans le backend, comme avec Isotope.


Boutique de démonstration
---------------------------

Pour tester et comparer l'extension par rapport à l'Isotope normal, une boutique de
démonstration a été mise en place : `https://isotope.metamodel.me <https://isotope.metamodel.me>`_

Les produits et groupes de produits ont été créés de manière identique dans le "MM-Shop"
et dans l'"Isotope-Shop" pour une meilleure comparabilité. Pour les distinguer dans le
panier et lors des commandes, les numéros d'article ont respectivement un préfixe "MM-"
ou "ISO-".

Voici encore quelques remarques sur les différents groupes de produits :

* les bonbons/Sweets sont créés comme un MetaModel unilingue, il n'y a donc pas de
  changement de texte lors du changement de langue FE ; pour ce groupe de produits, le
  prix de base a été implémenté
* les voitures/Cars sont créées comme un MetaModel multilingue, c.-à-d. que les textes et
  images (drapeaux !) changent lors du changement de langue ; dans le panier et le
  checkout, les liens vers la page de détail correspondent au "jumpTo" des réglages de
  rendu par langue ; pour la Mercedes, des variantes ont été créées et le template de
  sortie a été adapté de manière à n'afficher que l'enregistrement parent, les
  enregistrements enfants étant sélectionnables via un menu déroulant
* les téléchargements sont également multilingues


Prérequis
---------

Pour l'installation des modules, les prérequis actuels suivants s'appliquent :

* Contao 5.7 + Isotope 3.0-dev + MetaModels 2.5
* Contao 4.13 + Isotope à partir de 2.8 + MetaModels 2.3
* Contao 4.4.x/4.9.x + Isotope à partir de 2.5 + MetaModels 2.1/2.2

(Il n'existe pas d'Isotope pour Contao 5.3)


Dons
----

Un grand merci pour les dons* pour cette extension à :

* NN : 342 €
* Carsten Merz - `Fitkurs <https://www.fitkurs.de>`_ : 390 €
* Oliver Willmes - `oliverwillmes.de <https://www.oliverwillmes.de>`_ : 390 €
* iD visuelle Kommunikation - `id-kommunikation.ch <http://www.id-kommunikation.ch>`_ : 390 €
* ghost.company - `ghostcompany.com <http://www.ghostcompany.com>`_ : 490 €
* iD visuelle Kommunikation - `id-kommunikation.ch <http://www.id-kommunikation.ch>`_ : 390 €
* Hallenberger - `hallenberger.com <https://hallenberger.com/>`_ : 390 €

(*Dons nets)


.. |br| raw:: html

   <br />


.. |img_isotope_mm| image:: /_img/screenshots/extended/isotope/isotope_mm.jpg
.. |img_isotope_config| image:: /_img/screenshots/extended/isotope/isotope_config.jpg
.. |img_isotope_enable_bridge| image:: /_img/screenshots/extended/isotope/isotope_enable_bridge.jpg
.. |img_isotope_fe-addtocart| image:: /_img/screenshots/extended/isotope/isotope_fe-addtocart.jpg
