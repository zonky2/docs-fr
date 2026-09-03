.. _component_inserttags:

Insert-Tags
===========

.. note:: Affichage des valeurs d'un Model, d'un Item ou d'un attribut via Insert-Tag |br|
  Les Insert-Tags ont été entièrement retravaillés dans MM 2.3 et ne sont en partie
  disponibles (fonctionnels) qu'à partir de cette version.



Introduction
------------

Pour permettre différentes sorties de MetaModels dans le contenu Contao habituel,
différents Insert-Tags sont disponibles, comme par ex. le nombre total d'enregistrements
(publiés) ou encore des valeurs individuelles d'un ou plusieurs Items.

Des Insert-Tags personnalisés peuvent être créés facilement soi-même via le hook Contao
`replaceInsertTags <https://docs.contao.org/dev/reference/hooks/replaceInsertTags/>`_ en
combinaison avec l':ref:`API MM <ref_api>`.


.. _component_inserttags_count:
Nombre total d'Items
---------------------

Si aucun Item n'est trouvé, par ex. en raison du filtrage, le chiffre ``0`` est affiché.

* FE-Model liste MM : ``{{mm::total::mod::[ID]}}`` - par ex. ``{{mm::total::mod::22}}``
* CE liste MM : ``{{mm::total::ce::[ID]}}`` - par ex. ``{{mm::total::ce::33}}``
* MetaModel : ``{{mm::total::mm::[MM Table-Name|ID](::[ID filter])}}`` - par ex.
  ``{{mm::total::mm::mm_employees}}``, ``{{mm::total::mm::1}}``, ``{{mm::total::mm::1::44}}``


.. _component_inserttags_items:
Affichage d'un ou plusieurs Items
-----------------------------------

Affichage d'un ou plusieurs Items avec indication facultative du type de sortie.

* ``{{mm::item::[MM Table-Name|ID]::[Item ID|ID,ID,ID]::[ID render setting](::[Output (Default:text)|html5])`` - par ex.
  ``{{mm::item::mm_employees::1,3,42::5}}``, ``{{mm::item::1::1,3,42::5}}``


.. _component_inserttags_attributes:
Affichage d'un attribut
------------------------

Affichage d'un attribut avec indication facultative du type de sortie.

* ``{{mm::attribute::[MM Table-Name|ID]::[Item ID]::[ID render setting]::[Attribute Col-Name|ID](::[Output (Default:text)|html5|raw])`` - par ex.
  ``{{mm::attribute::mm_employees::42::5::combined_name}}``, ``{{mm::attribute::mm_employees::42::5::date_start::raw}}``


.. _component_inserttags_jumpto:
Affichage des paramètres de la redirection vers la page de détail
---------------------------------------------------------------------

Affichage de l'URL, du libellé, de l'ID de page ou des valeurs du nœud « param » comme par ex.
l'alias d'une redirection (jumpTo) d'un Item - la redirection doit être configurée en conséquence
dans les réglages de rendu.

* ``{{mm::jumpTo::[MM Table-Name|ID]::[Item ID]::[ID render setting](::[Parameter (Default:url)|label|page|params.attname])}}`` - par ex.
  ``{{mm::jumpTo::mm_employees::42::5}}``, ``{{mm::jumpTo::mm_employees::42::5::page}}``, ``{{mm::jumpTo::mm_employees::42::5::params.alias}}``

La création du lien avec :ref:`l'affichage d'une URL vers la page de détail peut également se
faire via un picker <rst_cookbook_specials_picker-for-tinymce>`, ce qui est plus simple à utiliser
pour les rédacteurs.



.. |br| raw:: html

   <br />
