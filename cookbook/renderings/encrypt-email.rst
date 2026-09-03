.. _rst_cookbook_rendering_encrypt-email:

Rendu : chiffrer l'affichage des e-mails
========================================

.. note:: Le chiffrement des e-mails pour l'affichage en HTML5 est désormais inclus automatiquement dans le
   rendu des textes - voir `Github <https://github.com/MetaModels/core/issues/1233>`_

Les e-mails saisis dans Contao sont affichés chiffrés dans le code source, afin de compliquer la récupération
automatique des adresses e-mail.

MetaModels ne dispose pas d'un « attribut e-mail » spécifique pour cette option - mais la fonction peut
rapidement être ajoutée avec un template adapté pour un attribut « Texte ».

Il suffit de créer et d'activer un template spécial pour le rendu. Pour cela, effectuez les étapes suivantes :

* dans le backend, sous « Templates », créer un template « mm_attr_text.html5 »
* renommer le template en « mm_attr_text_email.html5 »
* dans le nouveau template, insérer le code source |br|
  ``<span class="text<?= $this->additional_class ?>">{{email::<?= $this->raw ?>}}</span>``
* dans les réglages de rendu de l'attribut texte correspondant, sélectionner le nouveau template
  « mm_attr_text_email »

|img_encrypt-email|


.. |br| raw:: html

   <br />

.. |img_encrypt-email| image:: /_img/screenshots/cookbook/renderings/encrypt-email.jpg
