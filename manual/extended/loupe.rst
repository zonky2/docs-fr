.. _rst_extended_loupe:

Recherche plein texte avec Loupe
#################################

.. note:: Disponible à partir de MetaModels 2.4 - nécessite au moins PHP 8.3.

`Loupe <https://github.com/loupe-php/loupe>`_ est un moteur de recherche plein texte basé sur SQLite.
L'implémentation s'inspire entre autres du moteur de recherche `Meilisearch <https://www.meilisearch.com/>`_ mais
avec l'avantage de nécessiter relativement peu de ressources techniques - PHP et SQLite suffisent. `Loupe` propose
différentes fonctionnalités comme le stemming, la recherche par similarité selon Damerau-Levenshtein, le ranking,
les mots vides (stop words) et bien d'autres - `voir Loupe <https://github.com/loupe-php/loupe>`_.

Pour utiliser le moteur de recherche `Loupe`, une règle de filtre spécifique a été créée pour MetaModels. Dans les
réglages, on peut sélectionner les attributs à indexer et indiquer les seuils de tolérance aux fautes de frappe.

L'ordre des attributs à indexer entre en compte dans le `ranking <https://github.com/loupe-php/loupe/blob/develop/docs/ranking.md#4-attribute-ranking>`_,
c'est-à-dire que les attributs doivent être triés selon leur importance pour la recherche. Cette option peut être
désactivée avec la case à cocher `Désactiver le ranking selon l'ordre des attributs`.

Les seuils de tolérance aux fautes de frappe permettent d'indiquer, pour une longueur de mot donnée, combien de
"fautes d'orthographe" sont autorisées - des valeurs typiques sont par exemple une faute pour une longueur de mot
de cinq lettres et deux fautes à partir de neuf lettres.

L'indexation du contenu des attributs se fait automatiquement lors de l'enregistrement des ensembles de données. Une
réindexation complète se fait via une icône correspondante dans la liste des règles de filtre. Le déroulement précis
et les réglages nécessaires sont :ref:`expliqués ci-dessous <indexing_loupe>`.

La règle de filtre doit être placée en première position dans le filtre, car c'est elle qui détermine l'ordre des
résultats (items) - cet ordre reflète le ranking des occurrences trouvées (:ref:`voir plus bas <sorting_loupe>`).

Dans le frontend, un champ de saisie de texte est disponible pour la recherche. Des groupes de mots exacts peuvent
être délimités dans la chaîne de recherche avec des ``"``. Avec ``-``, on peut exclure des mots ou des groupes de mots.

Actuellement, les attributs suivants sont indexés :

- Texte
- Texte long
- Texte traduit
- Texte long traduit
- Sélection unique [select]
- Sélection multiple [tags]


.. _sorting_loupe:
Tri et sortie
-------------

Pour que les ensembles de données (items) soient triés selon la pertinence (score) de la recherche, la règle de
filtre doit être placée en première position dans le filtre. La première règle de filtre qui fournit une liste
d'ids d'items détermine toujours l'ordre de base des ensembles de données à afficher. Cela signifie qu'on peut créer,
après la règle de filtre Loupe, une règle de filtre "SQL personnalisé" qui fournit un tri lorsque Loupe n'est pas
sollicité du tout - par exemple par nom. De plus, aucun tri individuel ne doit être réglé dans les paramètres de la
liste - celui-ci écraserait toujours l'ordre défini.

Si le filtrage avec Loupe est présent dans le filtre, une clé ``loupe`` est disponible dans le tableau de sortie des
ensembles de données. Lors d'un filtrage avec Loupe, la pertinence calculée de l'ensemble de données est indiquée
dans ce nœud sous la clé ``score``.

.. code-block:: html
   :linenos:

   <?php if ($arrItem['loupe']['score'] ?? false): ?>
       <p>Score: <?= \Contao\System::getFormattedNumber($arrItem['loupe']['score'], 4) ?></p>
   <?php endif; ?>

Dans les réglages de la règle de filtre, l'option "Mise en évidence des termes de recherche" peut être activée. Si
c'est le cas, en plus du score, les attributs pour lesquels des occurrences ont pu être trouvées par la recherche
sont également affichés dans le nœud ``formattedHits``. Les occurrences trouvées sont présentes dans le tableau avec
un marquage inclus.

Voici en exemple la capture d'écran suivante - ici, une recherche a été effectuée pour "Moin" et il y a eu deux
occurrences. Bien que les deux ensembles de données contiennent le mot "Moin" avec la même orthographe, le score du
second ensemble de données est plus bas. Cela résulte de l'ordre configuré des attributs dans la règle de filtre :
d'abord le prénom (firstname), puis le nom (name).

|img_item_output|

En plus de la sortie dans le frontend, la recherche peut également être effectuée via la console - par exemple pour
vérifier l'index ; l'ID de la règle de filtre et la chaîne de recherche sont transmis comme paramètres.

.. code-block:: shell

   php contao/bin/console metamodels:loupe:test-index 11 "Am Ried"

En plus de l'ID de l'index et du score, la sortie contient également l'indication de l'attribut et un marquage
en couleur de la correspondance.

|img_console_output|


.. _indexing_stop-words:
Réglage des mots vides (stop words)
------------------------------------

Pour la recherche, on peut définir des mots isolés qui doivent être ignorés lors de la recherche et du ranking -
plus d'informations à ce sujet chez `Loupe <https://github.com/loupe-php/loupe/blob/main/docs/searching.md#stop-words>`_.

Le traitement des mots vides inclut également le traitement des mots formés par exemple par
`stemming <https://github.com/loupe-php/loupe/blob/main/docs/tokenizer.md#stemming>`_. Si l'on souhaite par exemple
éviter que la saisie de recherche ``forms`` déclenche également une recherche du terme fréquent ``for``, il faut
inscrire ``for`` dans la liste des mots vides.

Les mots vides ne sont pas exclus lors de l'indexation, mais seulement lors de la recherche. Si un mot vide est
saisi seul en tant que tel, comme ``for``, la recherche est tout de même effectuée.

La liste des mots vides est définie dans son propre fichier ``config.yml``. Pour chaque langue créée dans le
MetaModel, une section propre peut être définie - pour tous les modèles monolingues, la liste se place sous
``default``.

Voici un exemple :

.. code-block:: yaml
   :linenos:

   # config/config.yml
   meta_models_filter_loupe:
     stop_words:
       default:
         - ein
         - der
         - die
         - das
         - für
       en:
         - a
         - an
         - by
         - for
       de:
         - der
         - die
         - das
         - ein
         - für


.. _indexing_loupe:
Déroulement de l'indexation et réglages
-----------------------------------------

Lorsqu'un ensemble de données dont le contenu des attributs à indexer a été modifié est enregistré, ou que la
réindexation est lancée dans la règle de filtre, le traitement ne s'effectue pas directement dans l'appel web
(de manière synchrone), mais un message est transmis au `Symfony-Messenger <https://symfony.com/doc/6.4/messenger.html>`_
pour un traitement asynchrone. Pour en savoir plus à ce sujet, voir le `manuel Contao <https://docs.contao.org/dev/framework/async-messaging>`_
ou la `présentation à la CK23 <https://www.youtube.com/watch?v=bm9rTe2w1-M>`_.

Les "tâches du messenger" sont enregistrées dans la table ``tl_message_queue`` - celle-ci est créée si nécessaire.

Actuellement, une `"configuration de transport" <https://docs.contao.org/dev/framework/async-messaging/#the-transport-configuration>`_
doit être définie dans le ``config.yml`` pour le traitement des tâches du messenger - voici un exemple pour Loupe :

.. code-block:: yaml
   :linenos:

   # config/config.yml
   framework:
     messenger:
       routing:
         MetaModels\FilterLoupe\*: contao_prio_high
   # Alternativ: separate Einstellung möglich
   #      MetaModels\FilterLoupe\Messenger\IndexMessage: contao_prio_high
   #      MetaModels\FilterLoupe\Messenger\ReIndexMessage: contao_prio_normal

Dans une des prochaines versions, nous procéderons à une intégration complète avec l'implémentation de Contao, de
sorte que cela ne sera plus nécessaire.

Le messenger, quant à lui, attend d'être sollicité pour poursuivre le traitement. Cela se fait via la tâche cron
(cron-job) de Contao - celle-ci doit être `configurée <https://docs.contao.org/manual/de/performance/cronjobs/>`_
en conséquence.

Pendant l'indexation, un index propre est créé pour chaque règle de filtre sous forme de base de données SQLite -
pour les modèles multilingues ou les attributs multilingues, il existe également un index propre pour chaque
langue. Les données se trouvent sous ``var/mm_loupe_index/<id-Loupe-Filterregel>/``.

La réindexation peut être lancée manuellement après la création d'une nouvelle règle de filtre ou lors de
modifications des réglages. La base de données de l'index est alors vidée au préalable. Le lancement s'effectue via
l'icône dans la liste des règles de filtre ou via la console - avec le paramètre optionnel ``-p``, on peut adapter
le nombre d'items traités par entrée dans la ``tl_message_queue`` ; la valeur par défaut est 50.

.. code-block:: shell

   php contao/bin/console metamodels:loupe:reindex -p 1000


.. |img_item_output| image:: /_img/screenshots/extended/loupe/item_output.png
.. |img_console_output| image:: /_img/screenshots/extended/loupe/console_output.png
