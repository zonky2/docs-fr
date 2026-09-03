.. _rst_cookbook_templates_fe_redirect_to_list:

Redirection automatique de la page de détail vers la page de liste ou « Erreur 404 »
==========================================================================================

La sortie des données sur la page de détail est souvent pilotée par un ou plusieurs paramètres, ou bien la sortie
est filtrée - le plus souvent via `auto_item`.

Si aucun enregistrement ne peut être trouvé en raison du filtrage, ou si la page de détail est appelée sans aucune
indication du paramètre (de filtre) dans l'URL, un message tel que « Aucune donnée n'a pu être trouvée » s'affiche.

Si ce n'est pas le comportement souhaité et que l'on veut alors passer directement à la vue en liste, cela peut être
obtenu avec le code suivant dans le template de la vue de détail :

.. code-block:: php
   :linenos:

    // redirect if data empty
    if (!count($this->data)) {
        $pageId  = 192; // Page id
        $page    = \PageModel::findByPK($pageId);
        $pageURL = $page->getFrontendUrl();
        \Controller::redirect($pageURL);
    }

Si la page de base de Contao est appelée sans indication du paramètre (de filtre), on peut également faire délivrer
automatiquement une « erreur 404 ». Pour cela, il faut cocher la case « Élément requis » dans les réglages de la
page.
