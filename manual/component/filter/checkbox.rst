.. _component_filter_checkbox:

|svg_filt_checkbox_22| |img_filter_checkbox| État de la case à cocher
=======================================================================

La règle de filtre « État de la case à cocher » (paquet ``attribute_checkbox``) vérifie si la valeur d'un attribut de
type case à cocher est égale à ``1`` (actif). Elle est utilisée pour le contrôle de la publication : seuls les éléments
dont la case à cocher est activée (par ex. ``published = 1``) sont affichés dans le frontend. La règle n'affiche
**aucun** widget dans le frontend et n'ajoute aucun paramètre à l'URL.

.. warning:: À ne pas confondre avec la règle de filtre :ref:`« Oui / Non » <component_filter_yes-no>` (paquet
   ``filter_checkbox``) : c'est un widget pour les visiteurs. Elle ne filtre qu'une fois qu'un choix est fait et place un
   paramètre comme ``published/1`` dans chaque URL générée par le filtre, y compris dans les liens d'une liste vers la
   page de détail. Pour « uniquement les items publiés », « État de la case à cocher » est toujours le bon choix.

.. seealso:: Pour les MetaModels multilingues, la règle de filtre
   :ref:`component_filter_translated-checkbox` est disponible.


Installation
------------

La règle de filtre s'installe via le **Contao Manager** ou **Composer** :

.. code-block:: bash

   composer require metamodels/attribute_checkbox


Réglages lors de la création de la règle de filtre
----------------------------------------------------

.. list-table::
   :header-rows: 1
   :widths: 25 75

   * - Réglage
     - Description
   * - Type
     - Sélection du type de règle de filtre – ici : « État de la case à cocher ».
   * - Activé
     - Active ou désactive cette règle de filtre.
   * - Commentaire
     - Champ de texte libre pour décrire l'objectif de cette règle de filtre.
   * - Attribut
     - L'attribut de type case à cocher dont la valeur doit être vérifiée.
   * - Autoriser le remplacement
     - Un paramètre d'URL peut désactiver la règle de filtre (par ex. pour les liens d'aperçu).
   * - Ne pas utiliser le filtre dans l'aperçu frontend
     - La règle de filtre est ignorée lorsqu'un utilisateur backend utilise l'aperçu frontend de Contao. L'option
       « Afficher les éléments non publiés » est alors ignorée.


Attributs compatibles
----------------------

La règle de filtre « État de la case à cocher » convient exclusivement aux
attributs suivants :

* :ref:`Case à cocher <component_attribute_checkbox>`


Fonctions particulières
-------------------------

**Contrôle de la publication**

Le cas d'usage le plus fréquent est l'utilisation de cette règle de filtre comme « filtre de publication » : un attribut
de type case à cocher (nom de colonne habituel : ``published``) dont l'option « icône à bascule » est activée dans le
backend permet d'activer/désactiver rapidement des éléments. Dans le frontend, la règle de filtre « État de la case à
cocher » exclut les éléments inactifs – même si un visiteur a enregistré en favori le lien vers un élément et que le
filtre appartient à la page de détail.

Les règles de filtre d'un niveau sont toujours combinées avec ET : l'« État de la case à cocher » se place simplement à
côté des autres règles du filtre, aucune règle « ET » n'est nécessaire.


.. |svg_filt_checkbox_22| image:: /_img/icons_svg/filter_checkbox.svg
   :width: 22px
.. |img_filter_checkbox| image:: /_img/icons/filter_checkbox.png

.. |br| raw:: html

   <br />
