.. _rst_cookbook_templates_attribute_description.rst:

Afficher la description d'un attribut dans le template
============================================================

Dans le template de liste, le nom ou la désignation d'un attribut est disponible via le nœud ``attributes``.

Si l'on souhaite également accéder à la description issue des réglages de l'attribut, on peut apporter l'adaptation
suivante dans le template ``metamodels_prerendered.html5`` :

.. code-block:: php
   :linenos:

   <?php

   /**
    * Add description.
    */

   use Contao\System;
   use MetaModels\IMetaModel;

   /** @var IMetaModel $model */
   $model      = $this->items->getItem()->getMetaModel();
   $attributes = $model->getAttributes();

   $attributeDescriptions = [];
   foreach ($attributes as $attribute) {
       if (empty($attribute->getColName())) {
           continue;
       }
       $attributeDescriptions[$attribute->getColName()] = $attribute->get('description');
   }

   // Debug.
   if (System::getContainer()->get('kernel')->isDebug()) {
       dump($this->data);
   }
   ?>
   <?php if (\count($this->data)): ?>
       <div class="layout_full">
   // ....

Explication : avec $this->items->getItem(), nous récupérons un item - comme les indications d'attribut restent
toujours identiques, un seul item suffit pour interroger le MetaModel et, par son intermédiaire, ses attributs. Le
``foreach`` ne sert qu'à faciliter la manipulation dans la suite du template. L'ensemble pourrait aussi être
externalisé de manière plus élégante dans un helper -
`voir la conférence CK23 <https://www.e-spin.de/contao-metamodels/metamodels-vortrag-contao-konferenz-2023.html>`_

Dans la suite de la sortie, on peut afficher la description via le nom de colonne de l'attribut - |br|
par ex. ``<?= $attributeDescriptions['firstname'] ?? '' ?>``

Pour les modèles multilingues, la description correspondant à la langue FE est affichée.


.. |br| raw:: html

   <br />
