.. _rst_extended_file-usage:

Intégration File-Usage
#######################

.. note:: Disponible à partir de MetaModels 2.3 - pour l'activation, merci d'envoyer un e-mail à mail@metamodel.me.

Avec l'extension `File-Usage <https://github.com/inspiredminds/contao-file-usage>`_, vous pouvez voir dans le
gestionnaire de fichiers si et où un fichier est utilisé dans Contao. La prise en charge de MM est assurée à partir
de la version 4.1 de File-Usage.

Pour l'affichage des images intégrées dans les enregistrements de MetaModels, des fournisseurs (providers)
correspondants ont été créés. Les attributs suivants sont actuellement pris en charge :

* :ref:`Contenu d'un article <component_attribute_contentarticle>`
* :ref:`Fichier <component_attribute_file>`
* :ref:`Texte long <component_attribute_longtext>`
* :ref:`Table multiple (MCW) <component_attribute_tablemulti>`
* :ref:`Contenu traduit d'un article <component_attribute_translatedcontentarticle>`
* :ref:`Fichier traduit <component_attribute_translatedfile>`
* :ref:`Texte long traduit <component_attribute_translatedlongtext>`
* :ref:`Table multiple traduite (MCW) <component_attribute_translatedtablemulti>`

Selon l'attribut, la recherche porte sur le ou les UUID enregistrés du ou des fichiers, ou bien sur les
inserttags existants avec intégration de fichiers (`file`, `picture`, `figure`).

Comme dans `File-Usage à partir de la version 4.1.0 <https://github.com/inspiredminds/contao-file-usage/releases/tag/4.1.0>`_,
les chemins textuels comme `/file/content/my_file.jpg` sont également recherchés dans les attributs HTML `href` et
`src`, par ex. dans les textes.

Pour MetaModels, il existe des sorties propres avec le nom du modèle, de l'attribut et, pour les attributs
multilingues, également la langue. Le crayon permet d'accéder directement à l'enregistrement correspondant - voir la
capture d'écran. Pour les MetaModels multilingues, la langue du masque de saisie est définie en conséquence via un
paramètre GET.

|img_mm_file-usage|


Dons
----

Un grand merci pour les dons* reçus pour cette extension (objectif 2 613,75 €) :

* `AntwortInternet <https://www.antwortinternet.com/>`_ : 340 €
* `AntwortInternet <https://www.antwortinternet.com/>`_ : 340 €
* `P KREATIV <https://p-kreativ.at/>`_ : 250 €
* `GUTcert <https://www.gut-cert.de/>`_ : 340 €

(*Dons nets)


.. |manual@metamodel.me| raw:: html

   <a href="mailto:manual@metamodel.me">sur demande</a>

.. |img_mm_file-usage| image:: /_img/screenshots/extended/file-usage/mm_file-usage.png
