.. _rst_features:

Function overview
==================

Data models
-----------

MetaModels allow you to easily define data models in the Contao backend with (almost) no restrictions and without programming skills.

There are different data types availablefor the data fields (attributes), as for example text, picture, numbers, date and files. 
If you reach a limit and a desired data type is not available to you, an implementation is still possible.

Created tables can be linked together with relations (1:n, m:n). It is also possible to connect the tables with tables in the Contao core, to establish "parent-child-connections" or to implement variant inputs.

Input mask
----------

You can define complex input masks for the backend, which enable you to provide the Contao backend "look-and-feel" to the editors, which they are alraedy familiar with. Within an entry mask you are able to respond to the input of values or checkboxes to optionally show different sub-palettes.

It is possible to extend the view with different filters, search- and grouping functions for an easy orientation in the data.

The flexible user rights system, which has been developed for MetaModels, allows you to define different backend views for both editor and administrator user groups.

The backend can be customized in such a way, that only specified user groups are allowed to access particular input fields. Additionally you can customize the order of those input fields individually for each user group.

Multilingualism
----------------

From the beginning, MetaModels have been developed with the claim for multilingualism.
Therefore attributes are able to support translations of the data which is stored within them in multiple languages.
The language changer in the backend enables you to just switch to the desired language and immediately be able to edit the data set.

Best of all, untranslatable attributes are not going to be translated. This allows you e.g. to only make the product names and descriptions translatable, but not the EAN-Code and the measurements.

Filters
-------

MetaModels has a powerful filter concept, which enables you to realize complex tasks. The website administrator can adapt the filter interactions completely to their requirements. This can be achieved by configuration and combination of filter settings and their parameters.

MetaModels doesn't limit filter combinations and masters very complex filter scenarios. Thanks to the open structure of the API, you are able to easily program your own filters.

MetaModels is delivered with various filter settings, to generate filter input fields in the frontend, such as select boxes, range filters, free text search etc.
If you combine this filters with filter settings such as AND/OR-conditions or individual SQL-queries, complex and interactive filters can be set up.


Dynamic views
-------------

In MetaModels, the "partial"-template concept which is used in Contao, was implemented in an extended way with the help of the output settings. The user is enabled to customize every aspect of the views at attributes and data records level.

A lot of general settings can be specified in the backend configuration.
But they can also be overwritten, tweaked or completely ignored, by specifying a an own template at attributes and data records level. This output settings provide a flexible way to define "data views".

Designers can define a completely different view for each purpose, whether it's a simple list, a teaser for the homepage or a detail view of a data set. They can specify when and where this view should be used as well.

Outlook
-------

We are working on Metamodels to continuously improve functionality.
Further planned features:

* Extended outputs such as RSS-feeds and other syndications forms, XML, CSV
* Export/Import functions
* Front-End-Editing
* API for the onlineshop modul 'Isotope'

Financial support or ordered programming work will allow us to rapidly implement additional functionality   - Further informations are available on the project website: <https://now.metamodel.me>`_.
