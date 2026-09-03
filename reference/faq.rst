FAQ
===

.. _faq-searchable-pages:

Paramètres de recherche (Searchable Pages)
-------------------------------------------

| Q : Puis-je configurer la sitemap et l'index de recherche indépendamment l'un de l'autre ?
| R : Non, les deux sont alimentés en informations par la même fonction. Ceci est défini dans le Contao Core. Par conséquent, les mêmes configurations s'appliquent aux deux.

| Q : Puis-je utiliser la géo-protection ?
| R : En général, il ne faut pas utiliser de filtres qui exploitent le navigateur, l'IP ou d'autres données de l'utilisateur pour le filtrage. Il vaut mieux utiliser un filtre valable de manière générale.

| Q : Quand cette fonction est-elle utilisée ?
| R : Dès qu'une page est enregistrée, la sitemap est régénérée, c'est précisément à cet endroit que la nouvelle fonction intervient. Il en va de même lors de la création de l'index de recherche.

.. _faq-allgemein:

Général
-------

| Q : J'ai deux filtres MetaModels. Un sur la page d'accueil, un sur la page de résultats de recherche. Malheureusement, je n'arrive pas à faire en sorte que le filtre de la page de résultats soit contrôlé par la page d'accueil. Les deux filtres sont en soi identiques.
| R : Si je crée le filtre en tant que module et l'utilise aux deux endroits, cela fonctionne. Le POST contient l'ID du formulaire, ce qui fait que seul ce filtre peut traiter les données POST. Dès que tout passe par les données GET, cela n'a plus d'importance.
