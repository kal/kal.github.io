---
layout: page
title: MDF Technical Specification
date: 2012-01-24 16:26
author: kal
comments: true
categories: []
---
<h1>Introduction</h1>
MDF is a framework for the creation of reusable metadata processing modules. The MDF specification defines a simple module interface and the processing model to be used by an MDF implementation. An application makes use of the MDF framework by connecting together a number of MDF modules to provide the desired processing functionality.

MDF has been designed strictly according to KISS and 80/20 principles. Both the interface for the modules and the means by which modules are combined has been deliberately kept as simple as possible. While this may mean that MDF is not applicable to all metadata processing applications, it is hoped that it can be useful in a large majority of cases.
<h1>Definitions</h1>
<dl><dt><a name="module"></a>module</dt><dd>In MDF, a 'module' is a processing function which may be plugged into the framework. An MDF module is responsible for processing one or more 'metadata sets' received from an application or another module and producing, as a result of that processing, zero or more metadata sets to be passed to a third module (or to the application). During this processing, a module may interact with other systems, reading from or writing to other datastores as necessary.</dd><dt><a name="downstream-module"></a>downstream module</dt><dd>The downstream module of a particular MDF <a href="#module">module</a> is the module which receives <a href="#metadata-sets">metadata sets</a> from this module</dd><dt><a name="metadata-set"></a>metadata set</dt><dd>A metadata set is a collection of property/value pairs stored in an implementation specific table which is accessible via the property. Properties should be strings. Values may be strings or other object types, although strings are to be preferred for purposes of simplyfying interfacing with other modules.</dd><dt><a name="processing-chain"></a>processing chain</dt><dd>A collection of MDF <a href="#module">modules</a> connected together such that one module forms the head of the chain, with no <a href="#upstream-module">upstream module</a> and connected to a single <a href="#downstream-module">downstream module</a>, one module forms the tail of the chain with no downstream module but a single upstream module and all other modules are connected to one upstream and one downstream module in such a way that no two modules have the same upstream module or the same downstream module. In otherwords, a simple chain of modules connected together.</dd><dt><a name="upstream-module"></a>upstream module</dt><dd>The upstream module of a particular MDF <a href="#module">module</a> is the module which provides <a href="#metadata-set">metadata sets</a> to that module for processing.</dd></dl>
<h1>MDF Modules</h1>
An MDF module is responsible for processing a series of metadata sets passed to it either by the application or by its upstream module. In addition to providing an interface for receiving a metadata set, a module also provides an interface for receiving initialisation information and for connecting the module to a downstream module.

In Java, the interface for an MDF module looks like this:
<pre>public interface MDFModule { 
    public boolean init(Hashtable metadata); 
    public void rcv(Hashtable metadata); 
    public void chain(MDFModule module); 
}</pre>
NOTE: This specification gives interface specifications using Java. However, an MDF framework may be implemented in any language that provides support for key-based lookup. Similarly, this specification uses a Java Hashtable (java.util.Hashtable) for the property/value map - obviously implementations in other languages should use whatever construct is available for providing a key-based lookup table.

The init() function is invoked either by the application (for the module at the start of the processing chain) or by the upstream module (for all other modules in the processing chain) at the start of each metadata processing session. The module may examine the received metadata set to see if any property/value pairs provide configuration information for the module and use the values found to initialise itself prior to receiving the first metadata set for processing. If a fatal error is encountered by a module while it is initialising (for example if some required resource is not available), then the module should return FALSE from the init() function without invoking any downstream modules. In all other cases, after initialising itself, the module MUST call the init() function of its downstream module and return the value returned from the downstream modules init() function. A module SHOULD NOT modify the metadata set received for initialisation purposes. It is recognised that in some (rare) cases, the initialisation status of one module may influence the initialisation process of some other modules in the chain and so while it is allowed for a module to modify a metadata set during the initialisation processing, it is recommended that this be done only with extreme caution. Only after all modules in the chain have processed the metadata set provided for initialisation should the application begin passing metadata sets for processing.

The rcv() function is invoked by the upstream module (or the application if the module has no upstream module) once for each metadata set. A module MAY perform any processing in response to this module that it likes. A module MAY modify the received metadata set in any way. A module MAY generate one or more additional metadata sets and pass those to the rcv() function of the downstream module. A module MAY refuse to pass the received metadata set on to the downstream module (effectively terminating all processing of that metadata set).

The chain() function is invoked by the application to notify a module of its downstream module. The module must record this downstream module's interface address for the purpose of invoking init() and rcv() functions on the downstream module. A module MAY support multiple downstream modules, however the semantics of doing so are not constrained by this specification. However, if a module only supports a single downstream module, the module passed to the chain() function MUST replace the existing downstream module if there is one.
<h1>MDF Module Conventions</h1>
<h2>Simple Modules</h2>
A simple MDF module is defined as a module which receives a metadata set from an upstream module, performs some internal processing which MAY modify the received metadata set and that then passes that metadata set on to its downstream module. This is anticipated to be the most common form of module and so worthy of support in all implementations of MDF. The simple module interface should add the following functions to the basic module interface:

<code> public boolean initialise(Hashtable metadata); public void process(Hashtable metadata); public void notify(hashtable metadata); </code>

The initialise() function is provided as an overrideable function within which classes derived from the simple module may specify their own initialisation code. The derived classes do not need to be responsible for passing the metadata set on to the downstream module.

The process() function is provided as an overrideable function within which classes derived from the simple module may specify their own processing code. The derived classes do not need to be responsible for passing the metadata set on to the downstream module.

The notify() function provides an interface for the processing code of derived classes to pass any additional, generated metadata sets on to the downstream module. This allows classes derived from the simple module to generate multiple metadata sets for the downstream module without needing to be aware of the mechanism by which the module chaining has been implemented.

The implementation of the simple module should provide default implementations of the init(), rcv(), chain(), initialise(), process(), and notify() functions as described below:

The chain() function should record the module passed in as a parameter as this module's downstream module. If the module already has a downstream module, then it should be replaced by this new value. The module should be recorded in such a way that its init() and rcv() functions may be invoked.

The init() function should pass the received metadata set to the initialise() function of this module and then invoke the init() function of the downstream module with the metadata set. The metadata set should be passed to the initialise() function by reference, so that modifications made to the metadata set are reflected in the metadata set passed to the downstream module's init() function.

The rcv() function should pass the received metadata set to the process() function of this module and should then invoke the rcv() function of the downstream module with the metadata set. The metadata set should be passed to the initialise() function by reference, so that modifications made to the metadata set are reflected in the metadata set passed to the downstream module's rcv() function.

The initialise() function should be implemented as a null-op.

The process() function should be implemented as a null-op

The notify() function should pass the metadata set received as a parameter to the rcv() function of the downstream module.
<h2>Handling Multiple Values</h2>
Some metadata properties may be assigned multiple values. For example a list of keywords for a document. While MDF does not restrict a module from defining a single property with a value which is a collection, it may also be desirable to be able to serialise the multiple values as a set of property/value pairs in a metadata set. By convention such multiple property/value pairs should have a property string of the form <em>propertyName_N</em> where <em>propertyName</em> is a string key for the property and <em>N</em> is an integer value beginning with 0 for the first member of the collection and incrementing by one for each collection member serialised.

For example the property/value pair:

<code>KEYWORDS: {mdf, modules, metadata}</code>(where {} denotes an implementation specific collection)

can be serialised as:

<code> KEYWORD_0: mdf KEYWORD_1: modules KEYWORD_2: metadata </code>
<h2>Reporting Errors</h2>
By convention, if a non-fatal error is encountered during initialisation or running of a module, the module should add an error message to the metadata set being processed. The conventional key for this error message is the fully qualified name of the MDF module (in Java, the class name is used) with the string ".ERROR" appended. The value of this entry should be a string detailing the error which occurred.

The Java implementation provides this functionality in the class com.techquila.mdf.framework.BasicMDFModuleAdapter. A class derived from this class may register and error message by passing the metadata set to be modified and the message to be added to the function setError().
