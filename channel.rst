.. index::
    single: Integration
    single: Channel; Channel type

Introduction to Channels
========================

Overview
--------

**OroCRM** comes to us as multi channel CRM system based on **Oro Platform**.
So what exactly *"multi channel"* means? What is *"channel"*? Multi channel implies that **OroCRM** could work with data
that come from different sources such as contact forms, e-commerce websites, ERP-systems or whatever you want. So basically
**channel** is some kind of data source to work with.

Oro Platform built-in facilities
--------------------------------

In the same time **Oro Platform** is the foundation for modern web applications(where the lion's share are e-commerce
specific applications) and it comes with set of built-in features that relates to integration and bossiness entities.

**OroBusinessEntitiesBundle** - defines abstraction classes for the most popular data types. There are *cart*, *cart item*,
*order*, *order item*, *person*, *person group* and *product* entities. Those classes are based on generalized structures from
`schema.org <http://schema.org>`_ with some enchantments. Those entities could be extended with platform specific fields,
but definition on the platform level might be useful when some kind of data processing needs to be done for all types of
data. For example it might be useful to display grid with all customers that come from different systems and have different
sets of attributes, but developer could rely on fields from abstraction level and show information that shared between
all of them.

**OroIntegrationBundle** - is responsible for interaction between third party systems/services and platform. It extends
**OroImportExportBundle** to process data in background using other platform features such as cron and process queue.
General purpose of this bundle is to allow developers create integration bundles and provide basic UI for its configuration.

OroIntegrationBundle's terms
----------------------------

.. image:: images/elephants.jpg
   :alt:   Integration bundle elephants
   :align: right

OroIntegrationBundle provides 4 terms:  *channel type*, *channel*, *transport*, *connector* so let's determine what's
each of them mean.

Channel type
    Groups related to single third party application service classes and objects. For example: magento channel type,
    google channel type etc..

Channel
    Configured instance of some channel type and include set of configuration(such as connection settings etc)

Transport
    It's an object that knows how to retrieve data from channel instance. It knows  which entity should store connection settings,
    label for UI usage, and form type that is responsible to bring settings from channel creation page. Example of transport:
    SOAP transport, REST transport, direct database connection and much more.

Connector
    Generally it's reader in terms of OroImportExportBundle. Connector knows how to retrieve data of the given type from remote instance
    using any type of compatible transport for the given channel. Example of connector: Customer connector for ebay channel type.

Let's put them in one chain. So, we are able to create *channel* which is an instance of some *channel type* and contains
some set of configuration such as which *transport* to use to retrieve data specified by enabled *connectors*.

More technical information could be found in bundle's `readme <https://github.com/orocrm/platform/blob/master/src/Oro/Bundle/IntegrationBundle/README.md>`_.
