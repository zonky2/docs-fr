.. _component_dca:

|img_dca_32| Input screens
==========================

.. note:: Create input screens for data input;
  Add, activate and configure attributes; define display conditions of an input field; Definition of grouping and sorting of the stored items is possible

Introduction
------------

To be able to fill the database via the backend, input screens are required. Each input screen can include the attributes, which are defined for each MetaModel, as input elements.

You can create one or more different input screens for each MetaModel. That input screens can be equipped with different attribute input fields. This enables you to cover various user permissions or workflows.

Here too, the creation of the input screens is divided into the basic settings of the input screen, the part for the activation of the attributes as well as the selection of specific options of the individual attributes, such as mandatory field, arrangement, validation or similar.
Most of the settings options reflect the possibilities of the "DCA" of the "Contao framework" (see `DCA <https://docs.contao.org/books/api/dca/index.html>`_)
Read more about the options under the item "Procedure".

One of the most important things in the basic settings is the selection of the option integration where you can select either "Standalone" or "As child table". With "Standalone" the input screen will be integrated into one of the navigation blocks in Contao and with "As child table" it will be matched to an existing MetaModel table or Contao table.

The display of the input field in the backend can be influenced by further control parameters. Each input mask has an editing icon to create dependencies on when to display it and for the visibility dependencies ("Manage the visibility conditions").
This enables you e.g. to show one or more input fields only if a special checkbox is checked.

In order to obtain a clear display of the saved items you can define one or more grouping or sorting settings for each input mask.


Options of input screens
-------------------------
* **Name**: |br|
  Designation
* **Panel layout**: |br|
  Configuration of the tools, which you can find in the header of the page where you will add new entries, such as for searching, sorting, filtering and limiting the data records in the backend. To be able to search and filter the attributes, you will have to check this options inside the input screen settings ("Input screens in x" > "Edit the settings of input screen ID x" > "Edit setting ID x" then see at the bottom the section "Backend listing, filtering and sorting")
* **Integration**: |br|
  With the option "Standalone" you can choose the backend section, where the input screen should appear, with the option "As child table" you can select a parent table.
* **Render-Mode**: |br|
  Output mode of the listing as "Flat (without hierarchy)" or "Hierarchical", respectively when you use a child table also as "Parented".
* **Use column based layout**: |br|
  Select this option if you want to display the attributes as a table
* **Allow editing/creating/deleting of items**: |br|
  If checked the input screen will allow editing/creating/deleting of items

Options of an input field
--------------------------
You will find the following options by clicking on the "|img_dca_setting| Edit the settings of input screen ID x" and then on "|img_edit| Edit setting ID x" of the desired attribute.

* **Type**: |br|
  Legend: Dividers for the input panels ("Green lines") |br|
  Attribute: Display of the attribute options |br|
* **Functionality related options**: |br|
  Activation of "Read only" or "Mandatory" |br|
  further options are dependent on the chosen attribute type
* **Widget appearance related options**: |br|
  Specification of the Contao CSS backend classes, such as "w50" for a 50% width
* **Backend listing, filtering and sorting**: |br|
  Checkboxes "Filterable" and "Searchable" that allow you to make your attributes filterable and searchable in the backend (see also under the section above "Options of input screens" > "Panel layout").

Manage the visibility conditions of a property
----------------------------------------------
* **Type**: |br|
  Type of visibility condition: AND/OR/NOT for linking, respectively to set a    dependency on other attributes based on a property
* **Attribute/Value** |br|
  Selection of the attribute in case there is a dependency to another attribute

Options for grouping and sorting
--------------------------------
* **Name**: |br|
  Designation
* **Enable manual sorting**: |br|
  If this is enabled, the user will be able to perform manual sorting; 
  If this checkbox is not checked the user can set the following options:
* **Sorting attribute**: |br|
  Choose the attribute to sort by.
* **Grouping type**: |br|
  Grouping type e.g. initial letter, numeric order or such as "Group by day of date" or "Group by week of year"
* **Sorting direction**: |br|
  Sorting direction: ascending (ASC) or descending (DESC)

Workflow
--------

To create a new input screen click on "|img_new| New input screen".
After you have entered/chosen all the required options you can save your setting and your entry will appear in the list of available input screens of a MetaModel.
You can see the "|img_edit| pencil icon" and also an icon "|img_dca_setting| Edit the settings of input screen".
With a click onto this icon, a list of all attributes, which are activated for that input screen appears. If there are no attributes in this list available, you'll have to add some with a click onto the icon "|img_dca_setting_add| Add all". Alternatively you can click on "|img_new| New". If you choose to use "Add all" you will need to confirm twice.

After that, the attributes will be available to the input screen and, if appropriate, they also have to be activated.

You are able to add an individual CSS class for particular attributes with "|img_edit| Edit".

You can set the visibility of the input widget within an input screen with "|img_dca_condition| Manage the visibility conditions".

Finally you can create various settings for grouping and sorting for a saved item in the list view of the input screens with a click onto the icon "|img_dca_groupsortsettings| Edit the grouping and sorting settings".  


.. |img_dca_32| image:: /_img/icons/dca_32.png
.. |img_dca| image:: /_img/icons/dca.png
.. |img_dca_setting| image:: /_img/icons/dca_setting.png
.. |img_dca_setting_add| image:: /_img/icons/dca.png
.. |img_dca_groupsortsettings| image:: /_img/icons/dca_groupsortsettings.png
.. |img_dca_condition| image:: /_img/icons/dca_condition.png
.. |img_new| image:: /_img/icons/new.gif
.. |img_edit| image:: /_img/icons/edit.gif

.. |br| raw:: html

   <br />
