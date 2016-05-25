.. _component_index:

Components of a MetaModel
===========================

.. warning:: The manual is still under construction! |br|
   Starting 4. December 2015 the MetaModels designations and icons will be adjusted - see also :ref:`manual_new_labels`

The following chapter will show you the structure of MetaModels to understand the "logic" behind the extension.

First of all we should understand two terms:
with **MetaModel** (singular) we are hereafter talking about a data table with its attributes, input/output possibilities, filters etc.
The term "MetaModels" (plural) will be exclusively used to describe the extension package for Contao.

After you have created a MetaModel, there are the following components available for you for editing:

 |img_fields|  :ref:`component_attribute` |br|
 |img_rendersettings|  :ref:`component_rendersettings` |br|
 |img_dca|  :ref:`component_dca` |br|
 |img_searchable_pages|  :ref:`component_searchable-pages` |br|
 |img_filter|  :ref:`component_filter` |br|
 |img_dca_combine|  :ref:`component_dca-combine`

In case that you are creating a (simple) MetaModel you can work through the the components one after another in the order as shown above.
But with growing complexity of a MetaModel - e.g if multiple MetaModel interact with each other - it can not be avoided to further modify and enhance particular data inputs in a MetaModel, which has been already created.

The MetaModels extension makes two new content elements, respectively modules available for the front-end.
The content element "MetaModel list" enables you to display data records individually or as a list on your website. 
The content element / module "MetaModel frontend filter" provides you with a front-end filter. Find out more on  :ref:`component_contentelements`.

.. toctree::
    :hidden:
    :maxdepth: 1
    
    new-mm
    attribute
    rendersettings
    dca
    searchable-pages
    filter
    dca-combine
    contentelements


.. |br| raw:: html

   <br />
   
.. |nbsp| unicode:: 0xA0 
   :trim:

.. |img_fields| image:: /_img/icons/fields.png
.. |img_rendersettings| image:: /_img/icons/rendersettings.png
.. |img_dca| image:: /_img/icons/dca.png
.. |img_searchable_pages| image:: /_img/icons/searchable_pages.png
.. |img_filter| image:: /_img/icons/filter.png
.. |img_dca_combine| image:: /_img/icons/dca_combine.png
