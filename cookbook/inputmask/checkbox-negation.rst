.. _rst_cookbook_inputmask_checkbox-negation:

Condition d'affichage : afficher quand une case à cocher n'est pas cochée
=========================================================================

.. note:: Depuis la version 2.3, cette configuration n'est plus nécessaire - les valeurs « - » et « Inactif » sont
   équivalentes, si bien que le sélecteur revient automatiquement à la première valeur « - » après l'enregistrement.


Si l'on souhaite créer une condition d'affichage qui affiche le champ correspondant
lorsqu'une case à cocher n'est **pas** cochée, cela ne peut pas être obtenu avec un
déclencheur sur la valeur « Inactif » de la case à cocher.

La raison en est le traitement différent, entre MetaModels et le noyau Contao, de la
valeur pour « non coché » - dans le noyau Contao, au lieu d'un zéro (0), c'est une
chaîne vide '' qui est enregistrée. Cela ne peut actuellement pas être traité par
MetaModels ni par le DCG.

Le problème peut être contourné avec une petite astuce : on déclenche la visibilité
sur « coché », mais on inverse la vérification avec un NON (NOT). Pour cela, on crée
d'abord une condition NON dans les conditions d'affichage, puis on y place la
vérification de la case à cocher sur « Actif » (voir la capture d'écran).

|img_checkbox-negation_01|

Sur les deux captures d'écran suivantes, on voit le masquage du masque de saisie
de l'e-mail lorsque la case à cocher est cochée.

E-mail affiché

|img_checkbox-negation_02|

E-mail masqué

|img_checkbox-negation_03|

.. |img_checkbox-negation_01| image:: /_img/screenshots/cookbook/inputmask/checkbox-negation_01.jpg
.. |img_checkbox-negation_02| image:: /_img/screenshots/cookbook/inputmask/checkbox-negation_02.jpg
.. |img_checkbox-negation_03| image:: /_img/screenshots/cookbook/inputmask/checkbox-negation_03.jpg


.. |br| raw:: html

   <br />
