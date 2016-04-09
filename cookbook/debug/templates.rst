.. _rst_cookbook_debug_templates:

Debug templates
===============

If you need a custom template - e.g for displaying a frontend list - or if you want to find out which attribute values are sent to the template, you can print those attribute values out to the HTML source code. An easy way to do this is the output of the item array with "print_r" .

The default template is "metamodel_prerendered" or respectively the template, which was selected in the output render settings.

In case that there is no custom template in use yet, you will have to create a copy of "metamodel_prerendered" within the Contao folder named "Templates".

The following code is added to the respective template: 

.. code-block:: php
   :linenos:

   <?php 
   echo "<!-- DEBUG START \n";
   echo "<pre>\n";
   print_r($this->items->parseAll($this->getFormat(), $this->view));
   echo "</pre>\n";
   echo "\n DEBUG ENDE -->";
   ?>

Subsequently the template should start with the code as follows:

 
.. code-block:: php
   :linenos:

   <?php 
   echo "<!-- DEBUG START \n";
   echo "<pre>\n";
   print_r($this->items->parseAll($this->getFormat(), $this->view));
   echo "</pre>\n";
   echo "\n DEBUG ENDE -->";
   ?>
   
   <?php $strRendersettings = isset($this->settings)? 'settings' : 'view'; ?>
   <?php if (count($this->data)): ?>
    
   <div class="layout_full">
    
   <?php foreach ($this->data as $arrItem): ?>
   <div class="item <?php echo $arrItem['class']; ?>">
    
   <?php foreach ($arrItem['attributes'] as $field => $strName): ?>
   //...

If the website with this listing is called in a browser, you should find the debug output in the source code.

Browser rendering can become very slow in case that the output is very extensive. It might then be helpful to output only one item node.


.. code-block:: php
   :linenos:

   <?php 
   echo "<!-- DEBUG START \n";
   echo "<pre>\n";
   // nur 0.-Knoten
   print_r($this->items->parseAll($this->getFormat(), $this->view)[0]);
   echo "</pre>\n";
   echo "\n DEBUG ENDE -->";
   ?>

You can remove the output by commenting out the output block, by deleting it or by switching to another template. 


