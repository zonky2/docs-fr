.. _rst_cookbook_checklists_attribut_new:

Ajouter un attribut à un MM existant
=====================================

Si un MetaModel existe déjà et que l'on souhaite simplement ajouter
un attribut supplémentaire pour la sortie dans le template, il faut
tenir compte des points suivants :

Checklist :

   |box| aller dans le MetaModel concerné et créer l'attribut (type, nom de colonne, nom, libellé, etc.)

   |box| dans les réglages de rendu pour la sortie frontend, par ex. « Liste FE », ouvrir la liste d'attributs via l'icône et ajouter l'attribut, par ex. via « Tout ajouter » - vérifier qu'il est bien réglé sur visible

   |box| dans les masques de saisie, choisir la saisie correspondante, ouvrir la liste d'attributs via l'icône et ajouter l'attribut, par ex. via « Tout ajouter » - vérifier qu'il est bien réglé sur visible

   |box| pour un jeu de données existant ou nouveau, remplir le nouvel attribut...

   |box| vérifier via la :ref:`sortie de débogage <rst_cookbook_debug_templates>` si l'attribut « arrive » bien dans le template et adapter le template comme souhaité

autres réglages :

   |box| si l'attribut doit également apparaître dans la vue en liste du BE, ajouter l'attribut dans les réglages de rendu pour la sortie backend, par ex. « Liste BE » (voir ci-dessus)

   |box| réglages tels que l'aperçu d'image, le template, le CSS dans réglages de rendu > attribut

   |box| réglages tels que champ obligatoire, TinyMCE, recherchable/filtrable dans masque de saisie > attribut


.. |box| raw:: html

   <span>&#9634;</span>


