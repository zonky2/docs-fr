.. _new_in_mm260:

Modifications et fonctionnalités de MM 2.6
==========================================

Vous trouverez ci-dessous un aperçu des modifications et fonctionnalités de MetaModels 2.6, rendues possibles/en
cours grâce au « **programme early adopter** » (EAP) - pour en savoir plus, voir la rubrique **Fundraising** sur le
`site web de MM <https://now.metamodel.me/de/unterstuetzer/fundraising#metamodels_2-6>`_.

Pour une **vérification après une mise à niveau** vers MM 2.6, voir :ref:`plus d'indications ci-dessous
<check_upgrade_mm260>`.


Généralités et Core
-------------------

MetaModels 2.6 nécessite **Contao 6.x** et **PHP 8.4** - ainsi, actuellement encore, une
`clé d'accès EAP <https://now.metamodel.me/de/unterstuetzer/fundraising#metamodels_2-6>`_.

Les principales nouvelles fonctionnalités sont :

* **API et MCP pour agents IA** : les enregistrements des MetaModels sont accessibles via la Contao-API (lire, créer,
  modifier, supprimer - avec les droits et la validation du backend), voir :ref:`Contao-API <rst_extended_contao-api>`.
  Via le serveur MCP de Contao, un agent IA peut aussi consulter et configurer MetaModels, voir
  :ref:`Administration MCP <rst_extended_mcp-admin>`.


Problèmes connus
----------------

* lors du basculement vers/depuis le mode débogage dans le BE via le bouton, la page de référence n'est plus correcte
  et il faut rappeler la page - par ex. avec « retour » dans le navigateur et rechargement de la page |br|
  La cause est le lien de basculement ``?do=debug&key=enable&referer=…`` généré par Contao : sur les pages backend
  de MetaModels basées sur les routes (par ex. ``/contao/metamodel/mm_employees``), le paramètre ``referer`` reste
  **vide**, de sorte que Contao, après le basculement, ramène au tableau de bord du backend au lieu de la page de
  départ. Cela concerne le propre sélecteur de débogage de Contao et n'est pas couvert par la nouvelle gestion du
  Referer du DC_General (boutons « Retour » propres) - Contao n'offre ici aucune possibilité d'influencer le
  Referer. |br|
  Un correctif a été proposé : `contao/contao PR #10206 <https://github.com/contao/contao/pull/10206>`_.


.. _check_upgrade_mm260:
Vérifications pour la mise à niveau vers MM 2.6
-----------------------------------------------

En principe, une mise à niveau au sein de la branche MM 2.x est possible sans problème et les adaptations éventuellement
nécessaires des désignations et les modifications de la base de données sont gérées par des migrations. Il existe
cependant quelques points qui ne peuvent pas, ou seulement très difficilement, être pris en charge ainsi. C'est
pourquoi, lors du passage à MM 2.6, les points suivants doivent être gardés à l'esprit :



Refinancement
-------------
.. seealso:: Pour un refinancement des travaux importants réalisés, l'équipe MM sollicite un soutien financier.
   Comme ordre de grandeur, il convient de se baser sur l'ampleur du projet à réaliser et de prévoir environ 10 %
   de son montant - d'après l'expérience des derniers soutiens reçus, il s'agit de montants compris entre 100 €
   et 500 € (net) - une facture incluant la TVA est bien entendu toujours établie. `En savoir plus...
   <https://now.metamodel.me/de/unterstuetzer/spenden>`_



.. |br| raw:: html

   <br />
