.. _rst_cookbook_templates_fe_list_parameters:

Paramètres individuels pour la sortie de liste MM en frontend
==================================================================

.. note:: Cette fonctionnalité est disponible à partir de MM 2.2.

Dans les réglages de la sortie de liste (élément de contenu / module FE), il existe une option permettant de
transmettre ses propres valeurs au template. Il peut s'agir de textes ou de valeurs numériques. Cela permet
facilement à un rédacteur de piloter ou de moduler, avec le même template FE de sortie de liste, celle-ci au moyen
de paramètres. On peut ainsi généraliser davantage un template de liste et le piloter depuis le backend, par ex.
avec des libellés, des traductions ou des paramètres pour la sortie ou des contenus JavaScript.

Via un MCW, on peut créer ses propres « paires clé-valeur », qui sont disponibles dans le template sous forme de
tableau via ``$this->parameter``.

Les deux captures d'écran suivantes montrent une saisie possible dans le backend et ce qui est transmis au
template :

|img_settings-wizard_01|

|img_settings-wizard_02|

Le code suivant peut être intégré dans la partie supérieure du :ref:`template de liste <component_templates_fe-list>`
et montre, à titre d'exemple, l'accès aux valeurs y compris une valeur par défaut :

.. code-block:: php
   :linenos:

   <?php
   // Get value for "key".
   $extract = fn(string $keyName, string $default = ''): string =>
       (false !== $index = \array_search($keyName, \array_column($this->parameter, 'key'), true))
       ? $this->parameter[$index]['value']
       : $default;
   $valueOne = $extract('key1', 'value0');
   $valueTwo = $extract('key2', '');
   // dump($this->parameter, $valueOne, $valueTwo);


.. |img_settings-wizard_01| image:: /_img/screenshots/metamodel_new_features/settings-wizard_01.jpg
.. |img_settings-wizard_02| image:: /_img/screenshots/metamodel_new_features/settings-wizard_02.jpg

