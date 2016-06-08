.. _component_attribute:

|img_fields_32| Attributes
==========================

.. note:: create and configure own columns of the database table as attributes 

Introduction
------------

The attributes component is one of the very basic settings in a MetaModel. The attributes component allows you to define custom, specific data fields and create them within the data base table as columns.

When creating an attribute "|img_new| New attribute" there are two mandatory fields defined: selection of the attribute type and the entry of the column name. The column name defines - as indicated by the name  - the designation of the column in the data base table. Additionally you can enter a name and a description, which will also appear as designation and description within the input mask.

.. warning:: When changing an attribute type as well as when deleting an attribute, the already entered values will be deleted. However, if you need to change an attribute value while keeping the values, you should accompany this directly at database level, e.g. with the attribute column per CSV. A changed attribute should be added again in the render settings and input screens.

Depending on the attribute type there will be new entry options, respectively specific options available to you after reloading a page. Below you find a list of the attribute types where the specific options are pointed out:

* **Alias**: Alias-field, e.g. for URLs  |br|
  the alias can be created as a combination of different (existing) attributes; optionally you can enforce the regeneration upon changes in the original attributes (Force alias regenerating); an alias will not be created automatically as an unique value - for this you need to activate the checkbox "Unique values"
  
* **Checkbox**: Single Checkbox for boolean values |br|
  with the checkbox you can set boolean values (0|1); a special variant is the option "Publishing checkbox"  - with this option checked, an "eye icon" will appear in the backend, whereby you'll still have to create the filtering for the "publication" by yourself; in general "published" will be used as the column name for the publishing value; with the option "Listview checkbox" you are able to use an own icon in the backend to display the status
* **Combined values**: Combination of different attributes |br|
  all availabe attributes, as well as the "system attributes", such as ID, PID etc. can be combined to a new attribute; this combination can be realised with a sprintf-formatting; the attributes "name" and "surname" e.g. could be combined using the statement "%s, %s"; optionally you can enforce the regeneration upon changes of the values by checking "Force regenerating"
* **Country**: Country selection |br|
  this attribute will make a country selection available to you; using the option "Filter available countries" will limit the selection of countries
* **Decimal**: Decimal numbers |br|
  this attribute can be used to store decimals, as for example money amounts; there are two decimal places
* **File**: File picker |br|
  the attribute "file" provides you with a file picker to select a file, respectively using the option "Multiple selection" enables you to select multiple files; 
  additional file options can be set during the selection with the option "Customize the file tree";
  when using pictures, note that if you want to (directly) display a thumbnail preview of a picture in the backend or in the frontend, you will have to set the option "Enable as image field with thumbnail" in the render settings of the file attribute 
* **Langcode**: Selection of ISO language codes |br|
  this attribute provides you a selection of language codes; the language codes can be selected with a checkbox
* **Longtext**: Text input |br|
  Attribute for longer text entries
* **Numeric**: Entry of whole-numbered values (integer)
* **Rating**: rating module with stars |br|
  this attribute module is used to output a "star rating" in the frontend;
  you can set several options in the backend, such as number of stars etc.
* **Select**: Relation (1:n) to another MetaModel |br|
  with the attribute "Select" you can create a 1:n-relation to another MetaModel; the MetaModel table, the attribute etc. can be set within the options
* **Text table**: Input of values as a table |br| 
  the attribute "Text table" defines a number of columns including the column designation and the column width; in the input mask you can generate any number of lines, e.g. to store several URLs or phone numbers 
* **Multiple selection**: Relation (m:n) to another MetaModel |br|
  the attribute "Multiple selection"  creates a m:n relation to another MetaModel; the MetaModel table, the attribute etc. is set within the options; 
  the resolution of the relation takes place within a particular table of MetaModels, so that no column will be created in the MetaModel table for the attribute
* **Text**: simple text field
* **Date**: Date, respectively date and time |br|
  the data are stored as Unix timestamp; if you use own SQL filtering you might need to perform conversions
* **URL**: Link text and URL |br|
  entry of external links (enter with "\http://") or use the page picker
  internal links; you can display only the URL by choosing the option "Remove title"
  
If the option "Translation" is activated in the MetaModel, the following attributes will be additionally availabe to you for multilingualism:

* Translated checkbox
* Translated combined values.
* Translated file
* Translated longtext
* Translated select
* Translated table text
* Translated tags
* Translated text

These attributes differ from their monolingual attributes only regarding the multilingual informations for name and description. Special tables of the extension will be used for the translated attributes, not the table which has been generated when creating the MetaModel.

Note that you usually *don't* need to choose between the options "Translated select" and "Translated tags" regarding relations per "Select" or "Multiple select"  between two MetaModel with translations.

MetaModels will recognize and switch between languages automatically. The two "translated variants" are mainly determined to bind tables which do not belong to MetaModels and have independent fields for the language variant.

More attributes can be provided by additional extensions of MetaModels besides the above mentioned. 

The sequence of creating attributes is freely definable. Only for attributes with relations to other attributes, e.g. an "alias" or "Combined values", a subsequent creation makes sense.

Regarding the attributes "Select" and "Multiple selection" the referencing MetaModel have to be created first.

Options
-------

Two options are available for all attributes: "Enable variant override" and "Unique values".

By using the option "Enable variant override" the attribute will also be available in the input masks of the variant input. A precondition of this is, that the option "Variants" has been set before in the MetaModel.

By using the option "Unique values" attribute inputs will be checked for uniqueness.

Work flow
---------

A new attribute is opened by clicking "|img_new| New attribute". After you have entered, respectively selected all necessary options, the setting will be saved and it appears in the attribute list of the existing MetaModel.
The order of the list has no further impact.


.. |img_fields_32| image:: /_img/icons/fields_32.png
.. |img_fields| image:: /_img/icons/fields.png
.. |img_new| image:: /_img/icons/new.gif

.. |br| raw:: html

   <br />
   
.. |nbsp| unicode:: 0xA0 
   :trim:

