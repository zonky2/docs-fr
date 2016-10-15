.. _component_rendersettings:

|img_rendersettings_32| Render settngs
============================================

.. note:: How to create list views for back end and front end; how to add attributes and activate them

Introduction
------------

"Render settings" allow you to determine the basic parameters for the listings and the views of the data records, which have to be input and output. This can be done separately for the front end as well as for the backend. The individual data records, which are stored into a MetaModel are also called "items".

In the back end you will have to list those items for further input or to make changes. For the front end you also have to create lists for front end views / output. Some aspects are different between back end and front end, but there are still a lot of similarities. That's why those settings are combined within the "render settings" component.

Each MetaModel requires a render setting for the back end, because only this input mask can be used for data input and changes.

Regarding the front end, you only need to create a render setting for a MetaModel, whose items as such have to be listed and displayed. Thus, MetaModel which are linked by a relation (attribute "Select" or "Multiselect) to another MetaModel, do not necessarily need a render setting for the front end.

Among different requirements for back end and front end, you can meet further demands with the render settings. You can create many different render settings for each MetaModel, e.g. to generate differentiated outputs. That way one render setting could process a list with basic informations and another render setting a detail view (remember that a detail view is also just a list but with one single item!). Further you can grant access onto particular render settings from user groups or member groups by using :ref:`component_dca-combine`.

Once a render setting is created and the basic settings are entered, you will have to activate the attributes for that render setting in a next step.
More about that below, under the topic "Workflow". A further setting option for each attribute in a render setting allows you to select an individual template (if you created one before) and a custom CSS class, e.g. to put emphasis on it in the back end. 

Options
-------

* **Name** |br|
  the name can be chosen freely; but to distinguish more effectively you will find often the abbreviations "BE" and "FE"  for back end and front end preceding the name. 
  E.g "BE list", "BE collection" oder "FE list complete". 
* **Template** |br|
  here you can select a template, in which all items are output in loop; 
  the template can be overwritten easily in the usual way you are used to from Contao.
  Just note, that a template for the back end should not be created within a template subfolder;
  all attributes are passed to the template as a type of "raw" - only activated attributes are passed on as type "html" and "text".
* **Output format** |br|
  you can choose HTML5, XHTML and text; if there are no special requirements you can leave this field empty
* **JumpTo page** |br|
  this is the page which will be used for the front end output, for example to show a "details page".
  There should be a list element provided on this detail page with an appropriate filter setting; when using a multilingual MetaModel you will have a setting for link and filter for each language.
* **Hide empty values** |br|
  Empty values are skipped - a useful setting, if you want to display also the labels of the attributes
* **Hide labels** |br|
  The attribute names are not displayed as a "label"
* **Additional CSS/Javascript files** |br|
  For output formatting and interaction you can use additional CSS and/or JS files

Workflow
--------

To add a render setting, open a new input screen with a click on "|img_new| New".
After you have entered and selected all the required options, save your setting. It will then appear in the list of existing render settings of the MetaModel.

Besides the "|img_edit| pencil icon" there is also the icon "|img_rendersetting| Define attribute settings".
A click on the icon shows a list with the attributes that are activated for this render setting. If there are no attributes available you can add them with a click onto the icon "|img_rendersettings_add| Add all"  - alternatively you can click on "|img_new| New". If you use "|img_rendersettings_add| Add all" you will have to confirm twice.

Then the attributes will be available for the render setting. You might have to activate them, if you want them to be visible in the list view. 

You can change the applied template for each attribute and/or you can apply a custom CSS class ("|img_edit| Edit").


.. |img_rendersettings_32| image:: /_img/icons/rendersettings_32.png
.. |img_rendersettings| image:: /_img/icons/rendersettings.png
.. |img_rendersetting| image:: /_img/icons/rendersetting.png
.. |img_rendersettings_add| image:: /_img/icons/rendersettings_add.png
.. |img_new| image:: /_img/icons/new.gif
.. |img_edit| image:: /_img/icons/edit.gif

.. |br| raw:: html

   <br />
