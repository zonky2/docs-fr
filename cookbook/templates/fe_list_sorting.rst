.. _rst_cookbook_templates_fe_list_sorting:

Liens pour basculer le tri d'une liste MM
=============================================

.. note:: Cette fonctionnalité est disponible à partir de MM 2.2.

Dans les réglages de la sortie de liste (élément de contenu / module FE), il existe une option permettant de
remplacer le tri par défaut (« Autoriser le remplacement du tri »). Si l'on active cette option, différents
paramètres peuvent être définis :

* Slug/clé GET pour remplacer ``orderBy`` comme clé de l'attribut à trier
* Slug/clé GET pour remplacer ``orderDir`` comme clé du sens du tri
* Fragment d'URL si le lien doit renvoyer vers un ancrage précis sur la page

|img_sorting_options|

Les liens souhaités pour le tri individuel peuvent être intégrés dans le template de liste MM ou ailleurs.

.. note:: Cette fonctionnalité est disponible à partir de MM 2.3.

Pour simplifier l'utilisation dans le template de liste MM, il est possible de générer, pour chaque attribut,
différents liens pour le nouveau tri. Il existe un « lien à bascule » (toggle) qui inverse à chaque fois le sens du
tri, ainsi qu'un lien pour le tri croissant et un lien pour le tri décroissant - les classes CSS correspondantes et
un paramètre d'activation sont également transmis. On peut également faire générer directement le lien complet, y
compris les classes CSS.

Voici un extrait de code en exemple pour les appels de l'attribut « Name » avec le nom de colonne ``name`` :

.. code-block:: php
   :linenos:

   <?php
   // Variante 1 mit 'generateSortingLink':
   <?php if ($sortingLinkToggle = $this->generateSortingLink('name', 'toggle')): ?>
   <a href="<?= $sortingLinkToggle['href'] ?>" class="<?= $sortingLinkToggle['class'] ?>" data-escargot-ignore rel="nofollow"><?= $sortingLinkToggle['label'] ?> (toggle)</a><br>
   <?php endif; ?>
   <?php if ($sortingLinkAsc = $this->generateSortingLink('name', 'asc')): ?>
   <a href="<?= $sortingLinkAsc['href'] ?>" class="<?= $sortingLinkToggle['class'] ?>" data-escargot-ignore rel="nofollow"><?= $sortingLinkAsc['label'] ?> (asc)</a><br>
   <?php endif; ?>
   <?php if ($sortingLinkDesc = $this->generateSortingLink('name', 'desc')): ?>
   <a href="<?= $sortingLinkDesc['href'] ?>" class="<?= $sortingLinkToggle['class'] ?>" data-escargot-ignore rel="nofollow"><?= $sortingLinkDesc['label'] ?> (desc)</a><br>
   <?php endif; ?>

   // Variante 2 mit 'renderSortingLink':
   <?= $this->renderSortingLink('name', 'toggle') ?> (toggle)<br>
   <?= $this->renderSortingLink('name', 'asc') ?> (asc)<br>
   <?= $this->renderSortingLink('name', 'desc') ?> (desc)<br>

   // Liste...
   <?php foreach ($this->data as $arrItem): ?>

Veuillez noter que, pour le lien correspondant aux réglages du tri par défaut, les paramètres slug/GET sont
supprimés - seul le fragment d'URL est conservé. L'attribut ``data-escargot-ignore`` empêche l'inclusion du lien
dans le crawler Contao pour l'indexation de la recherche.

L'appel de ``generateSortingLink`` avec les paramètres « nom de colonne » de l'attribut et le type de tri renvoie
les valeurs suivantes :

* « attribute » : référence de l'attribut
* « name » : nom de l'attribut
* « href » : lien pour le tri
* « direction » : sens de tri actuel (``asc`` || ``desc``)
* « active » : ``true`` s'il s'agit de l'attribut de tri, ``false`` sinon
* « class » : classes CSS
* « label » : libellé

``renderSortingLink`` génère un lien complet - le texte peut être personnalisé via l'adaptation du fichier de
langue.

.. |img_sorting_options| image:: /_img/screenshots/cookbook/templates/sorting_options.jpg
