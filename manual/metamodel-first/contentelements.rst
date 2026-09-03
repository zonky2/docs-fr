.. _mm_first_contentelements:

Éléments de contenu/modules pour l'affichage frontend
=======================================================

Une fois tous les composants de saisie des données configurés, l'affichage des
données peut être mis en place. Plusieurs possibilités sont disponibles pour
l'affichage des données - dans cet exemple, l'affichage se fera via l'élément de
contenu d'article « Liste MetaModel ».

En préparation de l'affichage, il faut qu'une page correspondante soit créée dans
Contao, avec un article recevant l'élément de contenu. Un nouvel élément de contenu
est créé et les réglages suivants sont activés (voir la copie d'écran) :

* Type d'élément : Liste MetaModel
* Trier par : Nom
* Réglages de filtre à appliquer : Publié
* Réglages de rendu à appliquer : FE Liste

|img_contentelements_01|

Après « Enregistrer et fermer », l'élément de contenu est disponible et
l'affichage peut être vérifié dans le frontend.

L'affichage devrait maintenant faire apparaître la phrase « Votre recherche n'a
donné aucun résultat correspondant. », car aucune donnée n'a encore été saisie.

Pour tester l'affichage, il est nécessaire de créer quelques enregistrements dans
la liste des employés. Pour cela, dans la navigation de gauche du backend, sous
« MetaModels », on clique sur l'icône « |img_metamodels| Liste des employés », puis
sur l'icône « |img_new| Nouvel enregistrement ».

Le masque de saisie s'ouvre avec les champs prédéfinis (attributs), qui peuvent
être remplis avec les premières données (voir la copie d'écran).

|img_contentelements_02|

Après « Enregistrer et fermer », l'enregistrement est visible avec les attributs
activés du réglage de rendu « BE Liste » (Nom et Prénom) (voir la copie d'écran).

|img_contentelements_03|

L'enregistrement peut être modifié à nouveau via l'icône en forme de crayon, et le
statut « Publié » peut être basculé via l'« œil » (alternative à la case à cocher
du masque de saisie).

L'affichage dans le frontend devrait maintenant ressembler à peu près à ceci
(copie d'écran).

|img_contentelements_04|

Si l'on introduit quelques données de test dans la base de données - ou qu'on les
saisit manuellement - la liste des employés dans le backend ressemble à peu près
à la copie d'écran

|img_contentelements_05|

et de la façon suivante dans le frontend

|img_contentelements_06|

Pour l'affichage dans le frontend, les attributs sont générés par le template
standard sous forme de conteneurs HTML DIV individuels, avec des classes CSS
spécifiques. La mise en forme peut se faire soit via une feuille CSS, soit via
une adaptation du template, de sorte que l'affichage se fasse ici sous forme de
tableau HTML.

Avec quelques indications CSS telles que les suivantes

.. code-block:: css
   :linenos:

	.ce_metamodel_content .item {
	    display: table;
	    width: 100%;
	}
	.ce_metamodel_content .item.even {
	    background-color: #f4f2f0;
	    border-bottom: 1px solid #d4cbc5;
	    border-collapse: collapse;
	}
	.ce_metamodel_content .item.odd {
	    background-color: #f6f6f6;
	    border-bottom: 1px solid #d4cbc5;
	    border-collapse: collapse;
	}
	.ce_metamodel_content .item .field {
	    display: table-cell;
	}
	.ce_metamodel_content .item .field.name {
	    width: 20%;
	}
	.ce_metamodel_content .item .field.vorname {
	    width: 20%;
	}
	.ce_metamodel_content .item .field.email {
	    width: 40%;
	}
	.ce_metamodel_content .item .field.abteilung {
	    width: 20%;
	}

l'affichage est déjà plus présentable - voir la copie d'écran

|img_contentelements_07|


.. _mm_first_contentelements_detailpage:
Page de détail d'un enregistrement
-----------------------------------

En général, la vue en liste n'affiche pas tout le contenu d'un enregistrement,
mais seulement ce qui est nécessaire pour une recherche ou une sélection. On peut
présenter l'enregistrement complet sur une page de détail.

Pour cela, il faut d'abord créer une page de détail dans Contao - par exemple
``domain.tld/detail-employe.html``.

Sur cette page, on insère un élément de contenu Liste MM comme module ou CE - le
MetaModel est de nouveau ``mm_listeemployes``.

Un réglage de rendu est également nécessaire pour l'affichage - il est recommandé
de créer pour la page de détail un réglage de rendu séparé « FE - Détails ». Avec
un :ref:`template <component_templates>` propre, l'affichage peut être personnalisé.

Pour que la page n'affiche pas tous les enregistrements mais uniquement celui
souhaité, un filtre correspondant est nécessaire. Comme règle de filtre, il est
recommandé d'utiliser la :ref:`« recherche simple » <component_filter_simplelookup>`
et comme attribut un :ref:`alias <component_attribute_alias>`, respectivement un
:ref:`alias traduit <component_attribute_translatedalias>`. Selon les besoins,
d'autres règles de filtre, comme « Publié », sont également possibles. Le
filtre créé doit être sélectionné dans la Liste MM de la page de détail.

Avec une URL telle que par exemple ``domain.tld/detail-employe/alias/avery-amir.html``,
l'enregistrement correspondant devrait s'afficher.

Pour que les liens vers la page de détail soient générés automatiquement dans
l'affichage en liste, il faut sélectionner, dans le réglage de rendu de la liste,
section « Réglages de la redirection (jump-to) », la page de détail avec le filtre
correspondant. L'affichage des liens dans le template se fait dans le nœud
``actions``.




.. |img_new| image:: /_img/icons/new.gif
.. |img_metamodels| image:: /_img/icons/metamodels.png

.. |img_contentelements_01| image:: /_img/screenshots/metamodel_first/contentelements_01.png
.. |img_contentelements_02| image:: /_img/screenshots/metamodel_first/contentelements_02.png
.. |img_contentelements_03| image:: /_img/screenshots/metamodel_first/contentelements_03.png
.. |img_contentelements_04| image:: /_img/screenshots/metamodel_first/contentelements_04.png
.. |img_contentelements_05| image:: /_img/screenshots/metamodel_first/contentelements_05.png
.. |img_contentelements_06| image:: /_img/screenshots/metamodel_first/contentelements_06.png
.. |img_contentelements_07| image:: /_img/screenshots/metamodel_first/contentelements_07.png
