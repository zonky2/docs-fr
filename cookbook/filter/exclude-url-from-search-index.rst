.. _rst_cookbook_filter_exclude-url-from-search-index:

Exclure les URL de filtre de l'index de recherche Contao
============================================================

Si l'on souhaite qu'une liste MM soit intégrée dans l'index de recherche, mais pas l'appel de la liste avec des
paramètres de filtre, cela ne peut pas être configuré depuis le backend.

Un filtre FE génère, pour la « transmission des données » à une liste MM, différentes URL avec des « paires
clé-valeur » pour le filtrage. L'intégration de ces URL dans l'index de recherche est dans la plupart des cas
superflue, voire indésirable, car l'index ne fait que grossir sans apporter de résultat de recherche substantiel.

Pour les widgets de filtre qui génèrent directement une URL, par ex. une liste de liens, l'intégration de cette URL
dans l'index est généralement empêchée en indiquant l'attribut ``data-escargot-ignore`` dans le template du widget.

Cependant, l'appel des URL de filtre par le visiteur du site les fait tout de même intégrer dans l'index de
recherche, dans la mesure où la page de base de la liste n'a pas été exclue de la recherche. Avec peu de filtres,
cette intégration ne pose pas de problème. Mais si de nombreuses combinaisons de filtres sont possibles, cela peut
entraîner un index de recherche en constante croissance et des résultats de recherche peu pertinents.

Pour éviter cela, on peut par ex. empêcher l'indexation avec le code suivant lorsqu'un filtrage est défini. Cet
extrait de code doit être inséré dans le template de la liste MM.

.. note:: Pour MM 2.4 / Contao 5.3

.. code-block:: php
   :linenos:

   <?php

   use Contao\CoreBundle\Routing\ResponseContext\JsonLd\ContaoPageSchema;
   use Contao\CoreBundle\Routing\ResponseContext\JsonLd\JsonLdManager;
   use Contao\System;

   if (!empty($this->filterParams)) {
       $responseContext = System::getContainer()->get('contao.routing.response_context_accessor')->getResponseContext();
       if ($responseContext?->has(JsonLdManager::class)) {
           /** @var JsonLdManager $jsonLdManager */
           $jsonLdManager = $responseContext->get(JsonLdManager::class);
           $schema        =
               $jsonLdManager->getGraphForSchema(JsonLdManager::SCHEMA_CONTAO)->get(ContaoPageSchema::class);
           $schema->setNoSearch(true);
       }
   }
   ?>

.. note:: Pour MM 2.3 / Contao 4.13

.. code-block:: php
   :linenos:

    <?php
    if (!empty($this->filterParams)) {
        global $objPage;
        $objPage->noSearch = true;
    }
    ?>
