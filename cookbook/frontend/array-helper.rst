.. _rst_cookbook_frontend_array-helper:

Array-Helper
============

Dans de nombreux cas, on construit son template pour la sortie
frontend à partir de HTML et d'« echo » des variables PHP du
tableau de sortie.

Si l'on a une sortie de débogage comme dans :ref:`rst_cookbook_debug_templates`,
on voit que le tableau disponible dans le template se présente avec ses
nœuds sous forme de structure arborescente.

Pour la reprise dans le template, cela peut devenir particulièrement
fastidieux lorsqu'il y a de nombreuses relations vers d'autres MetaModels.

Avec l'« Array-Helper » suivant, les nœuds du tableau sont affichés de
telle sorte qu'on puisse facilement les reprendre dans le template par
« copier-coller ».

Le template concerné est complété par les lignes suivantes en première
position :

.. code-block:: php
   :linenos:

    <?php
    // http://stackoverflow.com/a/14518402
    function printArray($array, $path=false, $top=true) {
        $data = ""; $delimiter = "~~|~~"; $p = null;
        if(is_array($array)){
            foreach($array as $key => $a){
                if(!is_array($a) || empty($a)){
                    if(is_array($a)){
                        $data .= $path."['{$key}'] = array();".$delimiter;
                    } else {
                        $data .= $path."['{$key}'] = \"".addslashes($a)."\";".$delimiter;
                    }
                } else {
                    $data .= printArray($a, $path."['{$key}']", false);
                }
            }
        }
        if($top){
            $return = "";
            foreach(explode($delimiter, $data) as $value){
                if(!empty($value)){ $return .= '$arrItem'.$value."\n"; }
            };

            return $return;
        }

        return $data;
    }

    echo "<!-- DEBUG START\n";
    echo "<pre>\n";
    // nur 0.-Knoten
    //print_r($this->items->parseAll($this->getFormat(), $this->view)[0]);
    echo printArray($this->items->parseAll($this->getFormat(), $this->view)[0]);
    echo "</pre>\n";
    echo "DEBUG ENDE -->\n";
    ?>

Le template devrait ensuite commencer par les lignes suivantes - pour une
meilleure lisibilité, passer en affichage du code source (Ctrl + u | Cmd + Alt + u) :


.. code-block:: html
   :linenos:

   <html>
    <!-- DEBUG START
    <pre>
    $arrItem['raw']['id'] = "93";
    $arrItem['raw']['pid'] = "0";
    $arrItem['raw']['sorting'] = "0";
    $arrItem['raw']['tstamp'] = "1484897086";
    $arrItem['raw']['name'] = "0";
    $arrItem['raw']['vorname'] = "Amir";
    $arrItem['raw']['email'] = "Amir.Avery@mmtest.com";
    $arrItem['raw']['abteilung']['__SELECT_RAW__']['id'] = "4";
    $arrItem['raw']['abteilung']['__SELECT_RAW__']['pid'] = "0";
    $arrItem['raw']['abteilung']['__SELECT_RAW__']['sorting'] = "0";
    $arrItem['raw']['abteilung']['__SELECT_RAW__']['tstamp'] = "1442499032";
    $arrItem['raw']['abteilung']['__SELECT_RAW__']['name'] = "Marketing";
    $arrItem['raw']['abteilung']['__SELECT_RAW__']['alias'] = "marketing";
    $arrItem['raw']['abteilung']['name'] = "Marketing";
    $arrItem['raw']['abteilung']['alias'] = "marketing";
    $arrItem['text']['name'] = "Avery";
    $arrItem['text']['vorname'] = "Amir";
    $arrItem['text']['email'] = "Amir.Avery@mmtest.com";
    $arrItem['text']['abteilung'] = "Marketing";
    $arrItem['attributes']['name'] = "Name";
    $arrItem['attributes']['vorname'] = "Vorname";
    $arrItem['attributes']['email'] = "E-Mail";
    $arrItem['attributes']['abteilung'] = "Abteilung";
    $arrItem['html5']['name'] = "<span class=\"text\">0</span>";
    $arrItem['html5']['vorname'] = "<span class=\"text\">Amir</span>";
    $arrItem['html5']['email'] = "<span class=\"text\">Amir.Avery@mmtest.com</span>";
    $arrItem['html5']['abteilung'] = "Marketing";
    $arrItem['class'] = "first even";
    $arrItem['jumpTo'] = array();
    </pre>
    DEBUG ENDE -->
    ...
   </html>

Dans le template, la sortie du département pourrait par exemple ressembler à
ceci :

.. code-block:: html
   :linenos:

   <html>
   ...
   <p><span class="label"><?= $arrItem['attributes']['abteilung'] ?>:</span> <?= $arrItem['raw']['abteilung']['name'] ?></p>
   ...
   </html>

On peut à nouveau supprimer la sortie en commentant le bloc de sortie,
en le supprimant ou en changeant de template.


