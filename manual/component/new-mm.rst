.. _component_new-mm:

|img_new| New MetaModel
===========================

.. note:: create a new MetaModel (database table),
  if necessary activate translations and variants

Introduction
------------

A click on the icon "|img_new| New MetaModel" opens an input mask to create a new MetaModel. With a click on save, a new particular database table will be created for this new MetaModel to store its values.

For this, two input fields are mandatory to save a new MetaModel: the name of the MetaModel and the name of the table.

The name of the MetaModel is used for the designation in the backend and is freely selectable. But it is recommended for subsequent work to choose a name which is indicative of the content of the MetaModel, e.g. "adresses".

Same for the table name, whereby the prefix "mm\_" in the table name may be added, respectively is automatically added. The table may be named e.g "mm_adress". Opinions differ over whether one should use singular or plural for the name.

Only some of the columns, which are needed to interact with the MetaModels extension are setup within the table, at the time when you save it. These columns are e.g. id, pid, timestamp etc. Other individual columns can be added as so-called "attributes" provided with their specific options. Read more at :ref:`component_attribute`.

Options
-------

When you create a new MetaModel you have further options, called "translation" and "variants".

If the option "translation" is checked, a selection of multiple languages will be available to you after a reload of the page. You should activate one of those languages as the fallback language - if you don't do so, the first selected language will be used as the fallback language.
If the option "translation" is activated in the MetaModel, there will be additionally special, multilingual attributes made available to you. 

If multilingualism is activated at a later point in time, the existing attributes, respectively the entered values will not be passed automatically. Therefore it should be clarified in advance, whether multilingualism is required or not.

If the option "variants" has been selected you will first not see any change of the MetaModel. If the option has been selected, it is possible to activate the option "overwrite variants" in the attributes.
You can create additional input masks for entering data of variants - e.g. to "overwrite parent values" - with every attribute for which you have selected the option "overwrite variants".
You can find the input mask for the variants with a click on the icon "|img_variants| New Variant" within the list view of the parent elements.

The use of variants results in a "parent-child relationship" within a MetaModel database table, which is traceable over different values within the table - e.g with an own SQL filter.
Parent data records are characterised by the fact that the values within the database table of the parent records are equal to 1 for varbase. Values for vargroup are the same as their own ID.
The child records are characterised by having the values for varbase equal to 0 and the values for vargroup equal to the ID of the parent data record.  


.. |img_variants| image:: /_img/icons/variants.png
.. |img_new| image:: /_img/icons/new.gif

   
.. |nbsp| unicode:: 0xA0 
   :trim: