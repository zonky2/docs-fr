.. _rst_cookbook_specials_picker-for-tinymce:

Sélecteur jumpTo (page de détail) pour TinyMCE et comme dcaPicker
======================================================================

.. note:: MM 2.4 minimum est requis. |br|
   Ceux qui souhaitent utiliser cette fonctionnalité peuvent obtenir davantage d'informations sur la configuration
   sur demande à mail@metamodel.me


TinyMCE
-------

MM dispose d'un insert-tag permettant de sortir, pour un réglage de rendu défini, le lien vers la page de détail
(jumpTo) - pour en savoir plus, voir :ref:`Insert-Tags <component_inserttags_jumpto>`.

Pour les rédacteurs qui souhaitent insérer, dans le « contenu normal » du site, un lien vers une page de détail
précise, la recherche du bon insert-tag ainsi que des identifiants correspondants du réglage de rendu et de
l'enregistrement peut s'avérer trop complexe.

Pour cela, un nouvel onglet peut être défini dans le sélecteur de liens de TinyMCE, permettant de résoudre facilement
cette tâche. Via une configuration de MM, une telle sélection est générée dans TinyMCE - voir l'exemple dans la
capture d'écran.

|img_picker_01.png|

Dans la configuration, outre le MetaModel, il faut indiquer l'ID du réglage de rendu qui génère l'URL vers la page
de détail - généralement le réglage de rendu de la vue en liste. Il est en outre possible d'indiquer une icône pour
l'onglet ainsi qu'une priorité. La priorité définit le positionnement de l'onglet par rapport aux autres onglets -
plus le nombre est élevé, plus l'onglet est placé à gauche ; la valeur par défaut est 0.

Les priorités typiques de Contao sont :

- Pages : 192
- Fichiers : 160
- News : 128
- Événements : 96
- FAQ : 64
- Articles : 0

Dans l'exemple de la capture d'écran, le sélecteur MM a une priorité de 144.

L'apparence du MetaModel dans le sélecteur est définie par le réglage de rendu configuré pour le groupe
d'utilisateurs concerné. Il faut noter que, pour un affichage sous forme de tableau dans le sélecteur, seul le
premier attribut est affiché (voir la capture d'écran).

Lorsqu'une sélection est effectuée dans le sélecteur, l'ID de l'enregistrement (27) est automatiquement inséré dans
l'insert-tag et une URL est affichée dans la sortie en frontend.

|img_picker_02.png|


dcaPicker
---------

Le sélecteur peut également être intégré dans son propre DCA. Cela peut par exemple se faire dans
:ref:`rst_extended_attribute_mcw`, un RS-CustomElement ou une adaptation DCA personnalisée. Un fournisseur de
sélecteur dédié est mis à disposition à cet effet, dont le nom se compose du nom de table du modèle et de l'ID du
réglage de rendu sous la forme ``metamodelPicker_<mm-tablename>_<rendersetting-id>``. Une configuration dans
l'attribut MCW pourrait par exemple se présenter comme suit :

.. code-block:: php
   :linenos:

   <?php
   // /contao/config/config.php
   //...
        'col_ma_detail'  => [
            'label'     => ['MA Detailseite'],
            'exclude'   => true,
            'inputType' => 'text',
            'eval'      => [
                'fieldType'  => 'radio',
                'dcaPicker'  => ['providers' => ['metamodelPicker_mm_employees_4']],
                'tl_class'   => 'wizard',
            ],
        ],
   //...

|img_picker_03.png|

En cliquant sur l'icône du sélecteur :

|img_picker_04.png|


Dons
----

Un grand merci pour les dons en faveur de cette fonctionnalité à :

* `BAR PACIFICO <https://www.bar-pacifico.de/>`_
* `GUTcert <https://www.gut-cert.de/>`_


.. |img_picker_01.png| image:: /_img/screenshots/extended/picker/picker_01.png
.. |img_picker_02.png| image:: /_img/screenshots/extended/picker/picker_02.png
.. |img_picker_03.png| image:: /_img/screenshots/extended/picker/picker_03.png
.. |img_picker_04.png| image:: /_img/screenshots/extended/picker/picker_04.png

.. |br| raw:: html

   <br />
