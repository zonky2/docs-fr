.. _rst_cookbook_frontend_output-item-count:

Afficher le nombre d'items
============================

Si l'on souhaite afficher le nombre d'items dans le template FE, deux
variables sont disponibles :

* `count($this->data)` - retourne le nombre actuel d'items affichés
  dans le template, c.-à-d. que seuls les items actuellement affichés
  sont comptés ; si une pagination est configurée, ce sera au maximum
  la taille de la pagination qui sera retournée
* `$this->total` - retourne le nombre total d'items affichés dans le
  template ; une pagination n'a aucune influence sur cette sortie

Le template concerné peut par exemple être complété avec les sorties
suivantes :

.. code-block:: php
   :linenos:

    <?php if (count($this->data)): ?>

    <div class="layout_full">
        <div class="count_data">Anzahl data: <?= count($this->data) ?></div>
        <div class="count_total">Anzahl total: <?= $this->total ?></div>
        <?php foreach ($this->data as $arrItem): ?>
        <div class="item <?= $arrItem['class'] ?>">
    //....



