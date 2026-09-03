.. _ref_api:

Référence et API MetaModels
=============================

.. warning:: Encore en construction !

L'API MetaModels constitue l'interface pour votre propre programmation et vos propres extensions.


.. _ref_api_interf:
Interfaces MetaModels
-----------------------

L'API de MetaModels met à disposition des interfaces permettant d'accéder à différentes classes
sous forme d'« `Interfaces <http://php.net/manual/de/language.oop5.interfaces.php>`_ ».

Les interfaces peuvent par exemple être utilisées dans vos propres programmations ou fonctions,
dans des événements/hooks ou dans des templates. Elles permettent de récupérer facilement
différentes données ou propriétés, voire de les manipuler.

Les groupes d'interfaces suivants sont disponibles :

.. _index_api_interfaces:

.. toctree::
    :maxdepth: 1

    interfaces/metamodels
    interfaces/attribute
    interfaces/filter
    interfaces/dcgeneral-datadefinition

La documentation de ces groupes présente des exemples de base. D'autres exemples se trouvent notamment dans la section ":ref:`Cookbook <rst_cookbook>`",
la `présentation d'Ingolf Steinhardt à la CK23 <https://www.e-spin.de/contao-metamodels/metamodels-vortrag-contao-konferenz-2023.html>`_ et
":ref:`rst_cookbook_specials_register-services`".


.. _ref_api_dcg:
DC_General (DCG)
-------------------

Le DC_General gère l'affichage et le traitement des données dans le backend, ainsi qu'en partie l'édition côté frontend
(FEE). Plus d'informations sur `DC_General <https://dc-general.readthedocs.io>`_.
