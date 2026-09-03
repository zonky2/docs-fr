.. _rst_cookbook_checklists_attribut_change:

L'attribut ne s'affiche pas après une modification
====================================================

Après la modification d'un attribut (par ex. le type d'attribut),
celui-ci ne s'affiche plus (ou plus correctement) sur le site.

Attention : lors du changement du type d'attribut, les données
existantes en base sont supprimées !

Checklist :

   |box| vérifier les listes d'attributs dans les réglages de rendu et les masques de saisie

   |box| dans les réglages de rendu, supprimer l'attribut si besoin et le rajouter

   |box| vérifier que l'attribut est bien réglé sur visible dans les réglages de rendu et les masques de saisie

   |box| ressaisir si besoin les valeurs dans le masque de saisie après la modification

   |box| vérifier via la :ref:`sortie de débogage <rst_cookbook_debug_templates>` si l'attribut « arrive » bien dans le template


.. |box| raw:: html

   <span>&#9634;</span>


