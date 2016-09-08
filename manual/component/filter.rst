.. _component_filter:

|img_filter_32| Define filters
=============================

.. note:: Define optional filter sets for backend and frontend;
  Create filter sets and activate them within components or content elements/modules

Introduction
------------

The component "Define filters" is a comprehensive tool, which allows you to control the view or selection of the data records (items) of a MetaModel.
The filter sets reduce the total amount of the items, meaning, that a subset of these items is provided for output.
Please note that each filter returns only a list of IDs (of the items), respectively a filter rule passes on a list of IDs to the next filter rule. An alteration of the values, as for example by using a SQL query, is not possible.

Creating a filter set is done in two stages: first you'll have to create a designated filterset like a kind of "container", which itself may include one or more filter rules.
If there are several filter rules present on this level, they are automatically linked by AND. For a linking by OR, you'll need to create a filter rule OR, which itself can take additional filter rules. Nesting will allow you to emulate almost all AND/OR statements of a native SQL query.

With some filter rules you have the option to show only assigned or remaining tags to ensure a dynamic display of the filter sets.

The filter sets can be used in the backend as well as in the frontend.

The filter rules can partly be dynamically influenced e.g. by using GET/POST parameters. This results in very advanced filterings.


Types of filter rules
---------------------

* **Predefined set**: |br|
  You can enter a list of IDs to be used for filtering
* **Simple lookup**: |br|
  generates a filtering for an attribute; you can specify an URL parameter for filtering; selecting the option "Static  parameters" enables you to select a filtering value of this parameter within a FE module or Content element
* **Custom SQL**: |br|
  custom SQL condition for filtering; please note the |img_about| Help wizard (popup)
* **AND condition (AND)**: |br|
  A container for further filter rules with AND operation
* **ODER condition (OR)**: |br|
  A container for further filter rules with OR operation
* **Published state**: |br|
  checks an attribute value for 1; can be the attribute "published"
* **Translated published state**: |br|
  checks a translated attribute value for 1; can be the attribute "published"
* **Yes/No**: |br|
  Yes/No selection, e.g as radio buttons
* **Value from/to**: |br|
  From/to selection for values
* **Value from/to for date**: |br|
  From/to value for date
* **Value within 2 fields**: |br|
  Two fields with values
* **Value within 2 fields for date**: |br|
  Two fields with values for date
* **Single selection**: |br|
  einzelne Auswahl eines Wertes z.B. einer Select-Liste
  Single selection of a value e.g. in a select list
* **Multiple selection**: |br|
  multiple selection of values e.g. in a select list
* **Text filter**: |br|
  filters for a text input

Workflow
--------

A new filter set can be created by clicking on "|img_new| New". A name has to be assigned.

With a click on the icon "|img_filter_setting| Define attribute settings for filter setting" you reach the list of the filter rules. 
Here you can click again onto the icon "|img_new| New" to create a new filter rule. With a click onto one of those yellow icons with arrow "|img_pasteafter| Paste after" or "|img_pasteinto| Paste into" you can control the hierarchy while creating new filter rules and insert the new filter rule e.g. within an OR rule. 


.. |img_filter_32| image:: /_img/icons/filter_32.png
.. |img_filter| image:: /_img/icons/filter.png
.. |img_filter_setting| image:: /_img/icons/filter_setting.png
.. |img_new| image:: /_img/icons/new.gif
.. |img_about| image:: /_img/icons/about.png
.. |img_pasteafter| image:: /_img/icons/pasteafter.gif
.. |img_pasteinto| image:: /_img/icons/pasteinto.gif

.. |br| raw:: html

   <br />