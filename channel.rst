.. index::
    single: Integration
    single: Channel; Channel type

Introduction to Channels
========================

Overview
--------

**OroCRM** comes to us as multi channel CRM system based on **Oro Platform**.
What does exactly *"multi channel"* mean? What is *"channel"*? Multi channel implies that **OroCRM** can work with data
that comes from different sources, such as contact forms, e-commerce websites, ERP-systems or whatever you want. So, basically
**channel** is some kind of data source to work with.

Oro Platform built-in facilities
--------------------------------

In the same time **Oro Platform** is the foundation for modern web applications(where the lion's share is e-commerce
specific applications) and it comes with set of built-in features that relate to integration and business entities.

**OroBusinessEntitiesBundle** - defines abstraction classes for the most popular data types. There are *cart*, *cart item*,
*order*, *order item*, *person*, *person group* and *product* entities. Those classes are based on generalized structures from
`schema.org <http://schema.org>`_ with some improvements. Those entities may be extended with platform specific fields,
but definition on the platform level might be useful when some kind of data processing needs to be done for all types of
data. For example, it might be useful to display grid with all customers that come from different systems and have different
sets of attributes, but developer could rely on fields from abstraction level and show information that is shared between
all of them.

**OroIntegrationBundle** - is responsible for interaction between third party systems/services and the platform. It extends
**OroImportExportBundle** to process data in background using other platform features, such as cron and process queue.
General purpose of this bundle is allowing developers to create integration bundles and providing basic UI for its configuration.

OroIntegrationBundle's terms
----------------------------

.. image:: images/elephants.jpg
   :alt:   Integration bundle elephants
   :align: right

OroIntegrationBundle provides 4 terms:  *channel type*, *channel*, *transport*, *connector*.

So, let's determine what each of them means.

Channel type
    It groups related to single third party application service classes and objects. For example: magento channel type,
    google channel type etc

Channel
    It is configured instance of specific channel type and includes set of configuration(such as connection settings etc)

Transport
    It's an object that knows how to retrieve data from channel instance. It knows which entity should store connection settings,
    label for UI usage and form type, that is responsible for bringing settings from channel creation page. Example of the transport:
    SOAP transport, REST transport, direct database connection and much more.

Connector
    Generally, it is a reader in terms of OroImportExportBundle. Connector knows how to retrieve data of the specific type from remote instance,
    using any type of compatible transport for determined channel. Example of the connector: Customer connector for ebay channel type.

Let's put them in one chain. So, we are able to create *channel* that is an instance of some *channel type* and contains
some set of configuration, such as which one *transport* to use to retrieve data specified by enabled *connectors*.

More technical information can be found in bundle's `readme <https://github.com/orocrm/platform/blob/master/src/Oro/Bundle/IntegrationBundle/README.md>`_.
