.. _component_contentelements:

Content elements/modules for output in the frontend
===================================================

.. note:: For output in the frontend use the MetaModel list as a content element or a FE module; optionally you can also create a filter by using a content element or a FE module.

Introduction
------------

To display lists and filters in the frontend there is a list element and a filter element available to you. These two can be used in Contao as a FE module as well as a content element. There is no difference in the setting options between content element and module.

The most important selection options for a list element are the selection of the MetaModel (where does data come from), the render setting and the template selection (how will the data look like) and - when appropriate - the filter setting (which data will be output)

Please note that a detail view with a single item is also just a "list view" but with an appropriate filtering for only one output.

The most important selection options of the filter settings are the selection of the MetaModel (on which basis shall be filtered) and the selection of the filter sets (which filtering shall be used).

Additionally there is a content element/module called "MetaModel clear all" available to you, which enables you to reset all the filter settings in the frontend.

Options CE list
---------------

* **MetaModel**: |br|
  Selection of the MetaModel for the data source
* **Items per page, offset and limit** |br|
  Settings for pagination, respectively settings if you want to limit the items listed.  
* **MetaModel filter**: |br|
  Selection of the filter set and the sorting; If a filter setting is of type "Simple lookup" and the option "Static parameter" is checked, then a select field will be available here to choose a value; if the parameter "Allow sort override" is checked, you will be able to override the order per URL with the following scheme: /orderBy/<column name of attribute>/orderDir/<DESC || ASC>.html, respectively as a GET-parameter.
* **MetaModel Rendering**: |br|
  Selection of the render setting; if you want to control the output of the   items in the output list, you should use the template of the render setting (metamodel_prerendered) and not the "template to use for generating" (ce_metamodel_list)

Options CE Filter
-----------------

* **MetaModel**: |br|
  Selection of the MetaModel which shall be the base of the filtering
* **Filter settings to apply**: |br|
  Selection of the filter set
* **Attributes**: |br|
  Attributes, which shall be used in this frontend filter

Work flow
---------

Creating a content element, respectively a FE module is the same procedure as with the classical elements of Contao including the usual methods, such as activating access protection or applying CSS / ID classes. 


.. |img_filter| image:: /_img/icons/filter.png

.. |br| raw:: html

   <br />
