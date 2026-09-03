.. _rst_cookbook_specials_export-excel:

Transférer des données vers un tableur
=======================================

Pour des analyses telles qu'une représentation graphique sous forme de diagrammes ou divers calculs, il arrive
fréquemment que l'on demande un export vers un tableur comme MS Excel, OpenOffice Calc ou Google Sheets.

Une possibilité consiste à créer un export des données actuelles dans un format approprié (XLSX, ODS, XLS)
(voir `Conférence MM 2023 <https://www.e-spin.de/contao-metamodels/metamodels-vortrag-contao-konferenz-2023.html>`_).

Une autre possibilité, plus simple, consiste à récupérer les données de manière dynamique. Il suffit pour cela de
sortir les données sous forme de tableau et de les mettre ainsi à disposition pour un import. Cela peut se faire au
moyen d'une page dédiée de la sortie FE ou par l'appel d'un `routage personnalisé <https://docs.contao.org/dev/framework/routing/#implementing-custom-routes>`_.

Les programmes correspondants peuvent alors récupérer ce tableau de données - pas seulement une fois, mais aussi,
selon le type, à l'ouverture du fichier ou même en continu après un intervalle de temps défini.

Pour préparer cette récupération de données, celles-ci doivent être sorties sous forme de tableau. Pour cela, une
page dédiée peut être mise en place, dans laquelle on renonce aux éléments superflus tels que l'en-tête, le pied de
page, etc. Grâce à un template approprié, les données sont sorties sous forme de tableau - par ex.

.. code-block:: php
   :linenos:

    <?php
    // templates/metamodel_pre_movies_table.html5
    if (count($this->data)): ?>
        <div class="layout_full">
            <table id="export">
                <thead>
                <tr>
                    <?php foreach ($this->data[0]['attributes'] as $attributeName): ?>
                        <th><?= $attributeName ?></th>
                    <?php endforeach; ?>
                </tr>
                </thead>
                <tbody>
                <?php foreach ($this->data as $arrItem): ?>
                    <tr>
                        <?php foreach ($arrItem['attributes'] as $field => $strName): ?>
                            <td><?= $arrItem['text'][$field] ?></td>
                        <?php endforeach; ?>
                    </tr>
                <?php endforeach; ?>
                </tbody>
            </table>
        </div>
    <?php else : ?>
        <?php $this->block('noItem'); ?>
        <p class="info"><?= $this->noItemsMsg ?></p>
        <?php $this->endblock(); ?>
    <?php endif; ?>

Dans les réglages du module CE/FE MM-Liste, aucune pagination ne devrait être configurée. Pour un grand nombre
d'enregistrements, le temps d'exécution de la sortie du tableau peut être réduit en cochant la case « Ne pas sortir
d'items analysés via "$data" » ou en créant un index dans la table MM - pour en savoir plus, voir
:ref:`rst_cookbook_tips_speedup_backend`.


Données dans Excel
-------------------

Pour l'import dans Excel, on peut utiliser le :download:`fichier d'exemple </_download/Movie-Database.xlsx.zip>`
ou partir d'un nouveau fichier. Pour en savoir plus, voir
`Excel <https://support.microsoft.com/de-de/office/importieren-von-daten-aus-dem-web-a1a6b325-17f3-45c8-ae72-c421cb2a8e90>`_.

Dans l'onglet « Données », on choisit le Web comme source de données.

|img_excel-export_01|

À l'étape suivante, on saisit l'URL - dans l'exemple https://a-movie-database.metamodel.me/de/excel-connect.html.

|img_excel-export_02|

Après avoir choisi le mode de connexion « Anonyme » et cliqué sur « Connecter », un assistant apparaît, permettant de
sélectionner le tableau souhaité.

|img_excel-export_03|

Avec « Charger », les réglages sont finalisés et les données deviennent visibles.

|img_excel-export_04|


Données dans LibreOffice Calc
------------------------------

Voir le `manuel LibreOffice <https://help.libreoffice.org/latest/de/text/scalc/01/04090000.html>`_ - après avoir saisi
l'URL, appuyer sur Entrée et attendre quelques secondes que la liste des tableaux HTML se remplisse.



Données dans OpenOffice Calc
------------------------------

Pour l'import dans Calc, on peut utiliser le :download:`fichier d'exemple </_download/Movie-Database.ods.zip>`
ou partir d'un nouveau classeur.

Sous « Insertion », on crée un « Lien vers des données externes ».

|img_oo-export_01|

À l'étape suivante, on saisit l'URL - si aucun affichage n'apparaît dans le champ « Tableaux/plages disponibles »
après la saisie, cliquer sur le bouton « ... », coller l'URL dans « Nom de fichier » et cliquer sur « Ouvrir ».
Sélectionner ensuite le tableau « HTML_export » (ID de tableau « export ») et cliquer sur « OK ».

|img_oo-export_02|

Les données sont alors disponibles dans la feuille de calcul.

|img_oo-export_03|


Données dans Google Sheets
----------------------------

L'import dans Google Sheets se fait via une formule - il suffit de saisir la formule suivante dans la cellule A1

``=importhtml("https://a-movie-database.metamodel.me/de/excel-connect.html"; "table"; 1)``

Le premier paramètre est l'URL, le deuxième le type et le troisième le numéro du tableau (en commençant par 1). Après
la saisie de la formule, les données sont chargées.

|img_google-sheet_01|


.. |img_excel-export_01| image:: /_img/screenshots/cookbook/specials/excel-export_01.jpg
.. |img_excel-export_02| image:: /_img/screenshots/cookbook/specials/excel-export_02.jpg
.. |img_excel-export_03| image:: /_img/screenshots/cookbook/specials/excel-export_03.jpg
.. |img_excel-export_04| image:: /_img/screenshots/cookbook/specials/excel-export_04.jpg
.. |img_oo-export_01| image:: /_img/screenshots/cookbook/specials/oo-export_01.jpg
.. |img_oo-export_02| image:: /_img/screenshots/cookbook/specials/oo-export_02.jpg
.. |img_oo-export_03| image:: /_img/screenshots/cookbook/specials/oo-export_03.jpg
.. |img_google-sheet_01| image:: /_img/screenshots/cookbook/specials/google-sheet_01.jpg
