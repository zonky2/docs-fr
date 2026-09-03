.. _rst_cookbook_templates_fe_template_schema_org:

Afficher des données structurées dans le template FE
============================================================

Les données MM peuvent être enrichies, dans le code source, de ce que l'on appelle des « données structurées » afin
de faciliter l'analyse de leur contenu, par ex. par les moteurs de recherche. L'un des catalogues les plus connus
pour ce type de balisage se trouve sur `Schema.org <https://schema.org>`_.

Ces schémas peuvent être créés selon les encodages ``RDFa``, ``Microdata`` et ``JSON-LD`` et intégrés à la page.
Jusqu'à Contao 4.9, l'encodage utilisé par Contao était ``Microdata`` - depuis Contao 4.12, c'est ``JSON-LD`` qui
est employé.

Pour intégrer le balisage, on crée un template dédié à partir de ``metamodels_prerendered.html5`` et on l'adapte
comme le montrent les exemples suivants pour une offre d'emploi - voir `JobPosting <https://schema.org/JobPosting>`_.

Ces balisages peuvent par ex. être vérifiés avec les outils suivants :

* `Résultats de recherche enrichis <https://search.google.com/test/rich-results>`_
* `Validateur de schéma <https://validator.schema.org/>`_

Plus d'informations à ce sujet se trouvent sur la page :ref:`rst_cookbook_tips_seo`.

Balisage avec ``JSON-LD``
------------------------------

.. note:: Cette prise en charge n'est disponible qu'à partir de Contao 4.13 avec MM 2.3.

.. code-block:: php
   :linenos:

   <?php

   use Contao\CoreBundle\Routing\ResponseContext\JsonLd\JsonLdManager;
   use Contao\System;
   use Spatie\SchemaOrg\JobPosting;
   use Spatie\SchemaOrg\Organization;
   use Spatie\SchemaOrg\Place;
   use Spatie\SchemaOrg\PostalAddress;
   use Spatie\SchemaOrg\PropertyValue;

   $jsonLdGraph     = null;
   $responseContext = System::getContainer()->get('contao.routing.response_context_accessor')->getResponseContext();
   if ($responseContext && $responseContext->has(JsonLdManager::class))
   {
       /** @var JsonLdManager $jsonLdManager */
       $jsonLdManager = $responseContext->get(JsonLdManager::class);
       $jsonLdGraph   = $jsonLdManager->getGraphForSchema(JsonLdManager::SCHEMA_ORG);
   }
   ?>
   <?php if (count($this->data)): ?>
       <div class="layout_full">
           <?php foreach ($this->data as $arrItem): ?>
               <?php
               // Build Schema.org data.
               $schemaData = (new JobPosting())
                   ->identifier((new PropertyValue())->propertyID('jobId')->value($arrItem['raw']['id']))
                   ->hiringOrganization((new Organization())->name($arrItem['text']['corporation_name']))
                   ->title($arrItem['text']['name'])
                   ->datePosted(date('Y-m-d', $arrItem['raw']['created_date']))
                   ->jobLocation((new Place())->address((new PostalAddress())->addressCountry($arrItem['text']['country'])))
                   ->description($arrItem['text']['description']);
               ?>
               <div class="item <?= $arrItem['class'] ?>">
                   <h2 itemprop="title"><?= $arrItem['text']['title'] ?></h2>
                   <div>
                       <p><strong>Location:</strong><?= $arrItem['text']['city'] ?> <?= $arrItem['text']['region'] ?>
                       </p>
                   </div>
                   ...
                   <div class="actions">
                       <?php if (null !== ($href = $arrItem['actions']['jumpTo']['href'] ?? null)) {
                           $schemaData->url($href);
                       } ?>
                       <?php foreach ($arrItem['actions'] as $action): ?>
                           <?php $this->insert('mm_actionbutton', ['action' => $action]); ?>
                       <?php endforeach; ?>
                   </div>
               </div>
               <?php /* Add Schema.org data. */ $jsonLdGraph?->add($schemaData, 'job-' . $arrItem['raw']['id']); ?>
           <?php endforeach; ?>
       </div>
   <?php else : ?>
       <?php $this->block('noItem'); ?>
       <p class="info"><?= $this->noItemsMsg ?></p>
       <?php $this->endblock(); ?>
   <?php endif; ?>

L'intégration via ``JSON-LD`` demande certes quelques lignes de programmation supplémentaires, mais en contrepartie
le balisage est détaché du code source HTML pour l'affichage dans le navigateur. Les templates existants peuvent
ainsi être adaptés plus facilement ou complétés par d'autres balisages.

Lorsque plusieurs enregistrements sont insérés dans le graphe - par ex. pour une sortie de liste MM - la
transmission d'un identifiant unique est nécessaire : ``$jsonLdGraph?->add($schemaData, <Unique-ID>)``.


Balisage avec ``Microdata``
--------------------------------

Pour le balisage via « Microdata », des adaptations plus importantes du template sont nécessaires - l'intégration
en JSON-LD est donc recommandée.

.. code-block:: php
   :linenos:

   <?php if (count($this->data)): ?>
       <div class="layout_full">
           <?php foreach ($this->data as $arrKey => $arrItem): ?>
               <div class="item <?= $arrItem['class'] ?>" itemscope itemtype="https://schema.org/JobPosting">
                   <h2 itemprop="title"><?= $arrItem['text']['title'] ?></h2>
                   <div>
                       <p><strong>Location:</strong> <span itemprop="jobLocation" itemscope
                                                           itemtype="https://schema.org/Place">
                               <span itemprop="address" itemscope itemtype="https://schema.org/PostalAddress">
                               <span itemprop="addressLocality"><?= $arrItem['text']['city'] ?></span>
                                   <span itemprop="addressRegion"><?= $arrItem['text']['region'] ?></span>
                               </span>
                           </span>
                       </p>
                   </div>
                   ...
               </div>
           <?php endforeach; ?>
       </div>
   <?php else : ?>
       <?php $this->block('noItem'); ?>
       <p class="info"><?= $this->noItemsMsg ?></p>
       <?php $this->endblock(); ?>
   <?php endif; ?>
