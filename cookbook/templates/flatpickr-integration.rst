.. _rst_cookbook_templates_flatpickr-integration:

Sélection de date simplifiée pour la règle de filtre from-to grâce à l'intégration de Flatpickr
========================================================================================================

Si l'on souhaite disposer d'un sélecteur pour le choix de date dans le widget FE de la règle de filtre From-To
(« Valeur de/à pour un champ date »), on peut y parvenir avec les adaptations suivantes :

Dans le BE, créer le template mm_filteritem_default.html5, le renommer en mm_filteritem_flatpickr.html5 et le
sélectionner comme template dans les réglages du filtre.

Les lignes suivantes doivent être ajoutées dans le template :

En premier lieu, intégrer les fichiers de Flatpickr - ceux-ci se trouvent sur
`Flatpickr <https://flatpickr.js.org>`_ :

.. code-block:: php
   :linenos:

   <?php
   $GLOBALS['TL_JAVASCRIPT'][] = 'files/resources/flatpickr/flatpickr.min.js';
   $GLOBALS['TL_JAVASCRIPT'][] = 'files/resources/flatpickr/l10n/de.js';
   $GLOBALS['TL_JAVASCRIPT'][] = 'files/resources/flatpickr/plugins/rangePlugin.js';
   $GLOBALS['TL_CSS'][]        = 'files/resources/flatpickr/flatpickr.min.css';
   ?>

En dernier lieu, saisir le code JavaScript suivant - ici, le nom de colonne de l'attribut est ``startDate`` et le
RangePlugin est utilisé - d'autres réglages se trouvent dans la
`documentation de Flatpickr <https://flatpickr.js.org>`_ :

.. code-block:: php
   :linenos:

   <script>
   flatpickr('#ctrl_startDate_0', {
      locale: "de",
      minDate: "today",
      enableTime: false,
      allowInput: true,
      disableMobile: true,
      dateFormat: "d.m.Y",
      defaultDate: ["today", new Date().fp_incr(14)],
      "plugins": [new rangePlugin({ input: "#ctrl_startDate_1"})]
   });
   </script>
