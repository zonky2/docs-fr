.. _mm_first_attribute:

|img_fields_32| Attributes
==========================

After the table "mm_employeelist" was created in the database, we also have to create the fields/table columns to store the data, which are called the "attributes". We can do this with the component "|img_fields| attributes"

According to our task, we will need to create the following fields:

+-----------------+----------------+----------+
| **Name** | **Column name** | **Attr. type** |
+-----------------+----------------+----------+
| Name            | name           | Text     |
+-----------------+----------------+----------+
| First name      | firstname      | Text     |
+-----------------+----------------+----------+
| Email           | email          | Text     |
+-----------------+----------------+----------+
| Department      | department     | Text     |
+-----------------+----------------+----------+
| Published       | published      | Checkbox |
+-----------------+----------------+----------+


In the MetaModel "Employee list" go to the component "attributes" wth a click on the icon |img_fields|. After that you can create the first attribute with a click on "|img_new| New attribute". The input screen for the new attribute will not open immediately, but a "|img_pasteafter| Clip folder icon" on which you have to click (see screenshot below).

|img_attribute_01_en|

The input screen for the attribute opens with a click onto the "|img_pasteafter| Clip folder icon". Here, first choose the attribute type "Text" from the dropdown menu. The input screen will then refresh and show further options according to your selection. For the first attribute "Name" you will have to fill the fields in as shown below in the screenshot.

|img_attribute_02_en|

By clicking "Save and close" your first attribute "Name" is created - which means that the column "name" was generated in the database - then you can see the new attribute in the attribute overview.
This attribute creation steps have to be repeated now for the other fields "First name", "Email" and "Department".

Note that for the attribute "Published" we will choose "Checkbox" as attribute type. For this attribute we will also activate the option "Publishing checkbox" in the "Advanced settings" (see screenshot below).

|img_attribute_03_en|

Now you should be able to see the list of created attributes as shown in the screenshot below.

|img_attribute_04_en|


.. |img_fields_32| image:: /_img/icons/fields_32.png
.. |img_fields| image:: /_img/icons/fields.png
.. |img_new| image:: /_img/icons/new.gif
.. |img_pasteafter| image:: /_img/icons/pasteafter.gif

.. |img_attribute_01_en| image:: /_img/screenshots/metamodel_first/img_attribute_01_en.png
.. |img_attribute_02_en| image:: /_img/screenshots/metamodel_first/img_attribute_02_en.png
.. |img_attribute_03_en| image:: /_img/screenshots/metamodel_first/img_attribute_02_en.png
.. |img_attribute_04_en| image:: /_img/screenshots/metamodel_first/img_attribute_04_en.png

.. |br| raw:: html

   <br />
   
.. |nbsp| unicode:: 0xA0 
   :trim:

