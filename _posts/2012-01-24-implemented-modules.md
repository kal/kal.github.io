---
layout: page
title: Implemented Modules
date: 2012-01-24 16:30
author: kal
comments: true
categories: []
---
<h1>MDF Modules in the Java Implementation</h1>
The following table lists the modules which are currently part of the Java implementation of MDF which may be downloaded from <a href="http://www.techquila.com/mdf-dl.html">here</a>. All the modules are found in subpackages of the package com.techquila.mdf.impl
<table>
<tbody>
<tr>
<td>Module</td>
<td>Description</td>
</tr>
<tr>
<td><a href="http://www.techquila.com/modules.html#mdfapp">basic.MDFApp</a></td>
<td>This is not a module, but a simple MDF application which is configured by an XML file to build a chain of modules and pass one or more sets of data into the chain.</td>
</tr>
<tr>
<td><a href="http://www.techquila.com/modules.html#printer">basic.BasicPrinterModule</a></td>
<td>Writes the received metadata set to an output stream (stdout by default).</td>
</tr>
<tr>
<td><a href="http://www.techquila.com/modules.html#splitter">basic.SplitterModule</a></td>
<td>Creates multiple metadata values from a single value by dividing the string on specified characters.</td>
</tr>
<tr>
<td><a href="http://www.techquila.com/modules.html#translator">basic.TranslatorModule</a></td>
<td>Changes the key of specific entries in the metadata set.</td>
</tr>
<tr>
<td><a href="http://www.techquila.com/modules.html#spider">html.SpiderModule</a></td>
<td>Spiders over a specified URL, passing each spidered URL and a DOM representation of the HTML found to the downstream module.</td>
</tr>
<tr>
<td><a href="http://www.techquila.com/modules.html#rdfmapper">rdf.SimpleRDFMapper</a></td>
<td>Creates an RDF model from the recevied metadata sets. It is possible to specify which metadta properties define resources and which properties define values of specific RDF properties of those resources.</td>
</tr>
<tr>
<td><a href="http://www.techquila.com/modules.html#xtmmapper">xtm.SimpleXTMMapper</a></td>
<td>Creates an XTM model from the metadata sets. It is possible to specify which metadata properties define topics and which properties define names, occurrences, subject indicators or associations between those topics.</td>
</tr>
<tr>
<td><a href="http://www.techquila.com/modules.html#cxtmmapper">xtm.ConfigurableXTMMapper</a></td>
<td>Extends SimpleXTMMapper to allow configuration of the mapping from meta data sets to topics, associations and occurrences to be done using an XML file. This file may be passed to the module at initialisation time.</td>
</tr>
<tr>
<td><a href="http://www.techquila.com/modules.html#xpathex">xml.XPathExtractor</a></td>
<td>Extracts metadata sets from a DOM model using XPath expressions. It is possible to create multiple metadata sets from a single XML source.</td>
</tr>
<tr>
<td><a href="http://www.techquila.com/modules.html#cxpathex">xml.ConfigurableXPathExtractor</a></td>
<td>Extends xml.XPathExtractor to allow configuration of the extraction using an XML file. This file may be passed to the module at initialisation time and defines the metadata sets to be extracted and the properties to be found for each metadata set.</td>
</tr>
</tbody>
</table>
<div>
<h1>basic.MDFApp</h1>
A control framework application for constructing and running an MDF processing chain with one or more sets of meta data.

MDFApp reads a single XML configuration file which must be passed in to the application as the only command line parameter. This configuration file may contain the following elements which are recognised and processed by MDFApp. The following element descriptions all assume that the prefix 'mdf' is mapped to the MDFApp namespace: 'http://www.techquila.com/mdfapp/1.0'

<a name="mdfapp"></a>mdf:chain<dl><dd>The configuration file must have the mdf:chain element as its root document element. This element may contain the following elements recognised by MDFApp:

<a name="mdfapp"></a>
<ul>
	<li><a name="mdfapp"></a> <a href="http://www.techquila.com/modules.html#mdfapp.module">mdf:module</a> - Specifies one module in the chain.</li>
	<li><a href="http://www.techquila.com/modules.html#mdfapp.initialise">mdf:initialise</a> - Specifies the meta data set to be passed to all modules in the chain for initialisation.</li>
	<li><a href="http://www.techquila.com/modules.html#mdfapp.run">mdf:run</a> - Specifies a meta data set to be passed to the first module in the chain for processing.</li>
</ul>
</dd><dt><a name="mdfapp.module"></a>mdf:module</dt><dd>The mdf:module element contains only #PCDATA. The content of the element must be the full Java class name of a class which implements the com.techquile.mdf.framework.Module interface. Modules are added to the processing chain in the order in which the mdf:module elements appear within the parent mdf:chain element.

</dd><dt><a name="mdfapp.initialise"></a>mdf:initialise</dt><dd>This element contains a list of <a href="http://www.techquila.com/modules.html#mdfapp.property">mdf:property</a> elements and defines a single meta data set which will be passed to each of the modules in the chain for initialisation prior to the first processing run.

</dd><dt><a name="mdfapp.run"></a>mdf:run</dt><dd>This element contains a list of <a href="http://www.techquila.com/modules.html#mdfapp.property">mdf:property</a> elements and defines a single meta data set which will be passed into the first module in the chain for processing. The parent mdf:chain element may contain multiple mdf:run child elements. These elements will be processed in the order in which they occur in the XML file.

</dd><dt><a name="mdfapp.property"></a>mdf:property</dt><dd>The mdf:property element defines a single property/value pair in a meta data set. The element may contain only #PCDATA which is treated as the value of the property./value pair. The element also has a single, required attribute, <code>mdf:key</code>, which specifies the property name of the property/value pair.

</dd></dl></div>
<div>
<h1>basic.BasicPrinterModule</h1>
Writes the contents of the received metadata set to an output stream.
<div>
<h2>Initialisation Parameters</h2>
<dl><dt>com.techquila.mdf.impl.basic.BasicPrinterModule.OUPUT_STREAM</dt><dd>OPTIONAL. Value must be a java.io.PrintStream (or a derived class). By default, output is written to System.out (the standard output).</dd></dl></div>
<h2>Processing</h2>
This module simply writes the key and string value of every entry in the received metadata set. String values are determined by calling .toString() on the value object.

</div>
<a name="printer"></a>
<div><a name="printer"></a>
<h1>basic.SplitterModule</h1>
Divides the string value of a specified property into multiple values for another property.
<div>
<h2>Initialisation Parameters</h2>
<dl><dt>com.techquila.mdf.impl.basic.SplitterModule.SPLIT_FIELD</dt><dd>Value specifies the key string for the property to be split.</dd></dl><dl><dt>com.techquila.mdf.impl.basic.SplitterModule.OUTPUT_FIELD</dt><dd>Value specifies the key string for the multi-valued property to receive the split values.</dd><dt>com.techquila.mdf.impl.basic.SplitterModule.SPLIT_CHARS</dt><dd>Value specifies the characters which may be used to divide the string value to be split.</dd></dl><dl><dt>com.techquila.mdf.impl.basic.SplitterModule.SPLIT_CHARS</dt><dd>Value specifies the characters which may be used to divide the string value to be split.</dd></dl></div>
<h2>Processing</h2>
If the input metadata set contains the key defined by <code>com.techquila.mdf.impl.basic.SplitterModule.SPLIT_FIELD</code> then the string value of that property is split on the characters defined by <code>com.techquila.mdf.impl.basic.SplitterModule.SPLIT_CHARS</code> and each split value is written to a property with the key string specified by <code>com.techquila.mdf.impl.basic.SplitterModule.OUTPUT_FIELD</code> with _<em>n</em> appended where <em>n</em> is an integer value starting from 0.

</div>
<a name="splitter"></a>
<div><a name="splitter"></a>
<h1>basic.TranslatorModule</h1>
Implements the translation of property names. An instance of this class could be placed between two processing modules, converting the names of properties generated by the upstream module into names that may be recognised and processed by the downstream module.

This class alters the names of properties only. It does not remove the property generated by the upstream module , but simply creates a new property with the same value but a different name.

A translation is specified as a pair of names, the key name to translate from and the key name to translate to. A translation may be specified in one of two ways:
<ul>
	<li>By calling the addTranslation() function to add a translation to the map</li>
	<li>By including a Map of translations in the information map passed to the init() function. This Map must be stored under the key com.techquila.mdf.impl.basic.TranslatorModule.TranslationTable (this is defined as a static constant TRANS_TABLE in this class for convenience). The keys in the Map are treated as the key names to translate from and the corresponding values are the key names to translate to.</li>
</ul>
<div>
<h2>Initialisation Parameters</h2>
See description (above)

</div>
<h2>Processing</h2>
Any property in the received metadata set which has a key name which matches that in the translation table will be removed and its value reinserted with the translated key name specified in the translation table.

</div>
<a name="translator"></a>
<div><a name="translator"></a>
<h1>html.SpiderModule</h1>
Spiders a specified URL, generating a DOM representation of the HTML found there. The spidering follows only links in &lt;a&gt; tags and is performed in a depth-first manner. The maximum depth of the spidering may be controlled by module initialisation.
<div>
<h2>Initialisation Parameters</h2>
<dl><dt>com.techquila.mdf.impl.html.SpiderModule.SPIDER_MAX_HOPS</dt><dd>Specifies the maximum depth of the spidering. Depth 0 processes the specified URL only; depth 1 processes the specified URL and all pages it links to.</dd></dl><dl><dt>com.techquila.mdf.impl.html.SpiderModule.SPIDER_PARSER</dt><dd>Specifies the HTMLParserStrategy class for the spider to use. The default strategy uses an non-validating XML parser retrived from the JAXP interface. An alternative strategy is provided in the class com.techquila.mdf.impl.html.JTidyParserStrategy which uses JTidy to parse the HTML and is more robust in the face of badly formed HTML pages.</dd><dt>com.techquila.mdf.impl.html.SpiderModule.SPIDER_NON_LOCAL</dt><dd>Specifies whether or not the module should spider pages not on the same server as the first page processed. The value of this property should be a recognisable boolean value (either 'true', 'false', '1' or '0')</dd></dl><dl><dt>com.techquila.mdf.impl.html.SpiderModule.SPIDER_NON_LOCAL</dt><dd>Specifies whether or not the module should spider pages not on the same server as the first page processed. The value of this property should be a recognisable boolean value (either 'true', 'false', '1' or '0')</dd></dl></div>
<h2>Processing</h2>
<dl><dt>SOURCE_URL</dt><dd>IN: The URL to start spidering from. OUT: The URL of the page being spidered</dd></dl><dl><dt>SOURCE_DOM</dt><dd>OUT: The DOM Document created by parsing the page</dd></dl>Note: Each metadata set processed will result in one metadata set being generated for each page spidered. As well as the SOURCE_URL and SOURCE_DOM properties, all other properties in the initial metadata set will be copied to each generated metadata set.

</div>
<a name="spider"></a>
<div><a name="spider"></a>
<h1>rdf.SimpleRDFMapper</h1>
Maps the metadata in the received metadata sets into statements in an RDF model.

After processing, the RDF model may be retrieved by calling getModel() on the module, or it may be written to a file by calling the write() function.
<div>
<h2>Initialisation Parameters</h2>
Currenlty this module must be initialised programmatically by calling the function addProperty(). See the javadoc for this module for more information on this function. Calling this function specifies an RDF property, the key which is used to locate the subject(s) of the property and the key which is used to locate the object(s) of the property. Both subject and object may be found in multi-valued keys. When an object key may have multiple values, you may also specify whether the multiple values are collected together in an RDF Seq, Alt or Bag.

The mapper module may have any number of property definitions, and it is allowed for different property definitions to use the same metadata set values.

</div>
<h2>Processing</h2>
For each metadata set received, each property definition is processed and if the keys for both subject and object are found in the metadata set, a new RDF statement is generated.

</div>
<a name="rdfmapper"></a>
<div><a name="rdfmapper"></a>
<h1>xtm.SimpleXTMMapper</h1>
This module creates or updates a topic map from the received metadata sets.

Each metadata set may contain keys which define topics. For each topic, other keys in the same metadata set may define subject indicators, name strings or occurrences. Additionally, associations may be created between topics which are created from the same metadata set.

The initialisation of this module is complex and can only be done programatically (as opposed to using the metadata set passed to the init() function). See the javadoc for more details.
<h2>Processing</h2>
For each metadata set received, each topic definition is processed and if the key which 'triggers' the creation of that topic is found then a new topic is created. For each characteristic definition of the topic definition, if the key for that characteristic definition is present, then the characteristic is created using the value mapped to the key for that definition. For names, the string value of the value is used as the name string. For occurrences, the string value is used as either the occurrence reference or occurrence data (depending upon the configuration of the characteristic definition). For subject identities, the string value is prepended with a fixed string defined in the subject identity characteristic definition.

</div>
<a name="xtmmapper"></a>
<div><a name="xtmmapper"></a>
<h1>xml.XPathExtractor</h1>
This module extracts one or more metadata sets from an XML source. A metadata set is defined for each node which matches a specified XPath expression. Properties within that set are defined for each node which match another XPath expression (using the node which defines the metadata set as the root of the expression).

This module may generate many metadata sets for downstream modules as the result of processing a single metadata set from an upstream module.
<div>
<h2>Initialisation Parameters</h2>
Definition of the metadata set and property xpaths is currently possible only through additional functions in the module's API. See the javadoc for more details.

The module xml.ConfigurableXPathExtractor allows an XPathExtractor to be configured by passing an XML file name in the initialisation metadata set

<dl><dt>com.techquila.mdf.impl.xml.XPathExtractor.SOURCE_TYPE</dt><dd>The value of this property defines how the XML to be processed is to be passed to this module. Allowed values are 0 for XML passed as a DOM document and 1 for XML passed as a URL of the file to be parsed.</dd><dt>com.techquila.mdf.impl.xml.XPathExtractor.SOURCE_PROPERTY</dt><dd>The value of this property defines the key under which the processor will find the XML source DOM/URL in the metadata sets passed for processing.</dd></dl><dl><dt>com.techquila.mdf.impl.xml.XPathExtractor.SOURCE_PROPERTY</dt><dd>The value of this property defines the key under which the processor will find the XML source DOM/URL in the metadata sets passed for processing.</dd></dl></div>
<h2>Processing</h2>
For each metadata set received, the property under the key defined by the com.techquila.mdf.impl.xml.XPathExtractor.SOURCE_PROPERTY initialisation property will be located and the source DOM/URL will be extracted.

For each metadata set definition specified for this module, the set of nodes which match the XPath expression for that metadata set definition will be extracted from the XML. For each node in that set, one metadata set will be passed on to the downstream module. For each metadata set to be passed on, the property definitions of that set will be enumerated and for each property definition, the XPath expression will be executed using the node of the parent metadata set as the root. For each node which matches, the string value of that node will be inserted under the key defined for that property.

</div>
<a name="xpathex"></a>
<div><a name="xpathex"></a>
<h1>xml.ConfigurableXPathExtractor</h1>
This module performs the same processing as the xml.XPathExtractor module, but is configurable from an XML file.

The configuration file contains elements to define the XML source to parse, the metadata sets to be created and the properties to be defined for each of those metadata sets. In the following element descriptions, the prefix 'ex' should be mapped to the namespace http://www.techquila.com/mdf/xpathextractor/1.0

<dl><dt>ex:source</dt><dd>This element defines the source XML file to be processed to produce metadata sets. It must have a <code>type</code> attribute which may have one of the following values: FILE, DOM or STRING. If <code>type</code> is file, then the element may have an attribute <code>src</code> which specifies the file name of the source to be parsed. Otherwise, the element must have an attribute <code>property</code> which defines the property which specifies the source to be parsed. If <code>type</code> is FILE, then the property specified will be expected to contain a file name. If <code>type</code> is DOM, the the property will be expected to contain a DOM Document. If <code>type</code> is STRING, then the property will be a string which can be parsed as XML. This element has no content model.</dd><dt>ex:meta-set</dt><dd>This element defines a single metadata set which may be extracted from the XML. It may have the attribute <code>name</code> which specifies an identifier for the metadata set definition. It must have the attribute <code>xpath</code> which specifies the XPath expression for locating the root node of the metadata set. Note that one metadata set will be created for each node that the expression resolves to.</dd><dt>ex:property</dt><dd>This element defines one property in a metadata set. It must have the attribute <code>property</code> which defines the key string of the property. It must have the attribute <code>xpath</code> which specifies the XPath expression to be executed from the root node of the metadata set to determine values for the property. It may have the attribute <code>multi</code> which if present and specified with any value indicates that the resulting nodes should be treated as separate values for a multi-valued property. If the <code>multi</code> attribute is specified then the string value of each node which results from evaluating the XPath expression will be assigned to a key value <em>property_n</em> where <em>property</em> is the property name specified by the <code>property</code> attribute and <em>n</em> is an integer value starting from 0. If the <code>multi</code> attribute is not specified then only a single value is added to the metadata set, using the value of the <code>property</code> attribute as the key and the concatenation of the string values of all nodes matching the XPath expression as a value.</dd></dl>
<div>
<h2>Initialisation Parameters</h2>
<dl><dt>com.techquila.mdf.impl.xml.ConfigurableXPathExtractor.MDF_CONFIG</dt><dd>Defines the name of the XML file which contains the configuration to be read.</dd></dl></div>
</div>
<a name="cxpathex"></a>
<div><a name="cxpathex"></a>
<h1>ConfigurableXTMMapper</h1>
This module performs the same function as the SimpleXTMMapper, but is configurable from an XML file.

The configuration file contains elements to define the mapping from properties in meta data sets to topics and / or associations between topics to be created. In the following element descriptions, the prefix 'xtm' should be mapped to the namespace http://www.techquila.com/mdf/xtm/mapper/1.0

<a name="cxtmmapper"></a><dl><dt><a name="cxtmmapper"></a> <a name="cxtm.topic"></a>xtm:topic</dt><dd>This element is used to define a mapping from a property in the metadata set to a topic to be created. This element has the following attributes:
<ul>
	<li><code>xtm:property</code> - REQUIRED - specifies the property key which must be present in the meta data set for the topic to be created. if a meta data set is received which contains a property with this key value, then a topic will always be created. if a meta data set is received which does not contain a property with this key value, a topic will never be created</li>
</ul>
This element may have the following child elements:
<ul>
	<li><a href="http://www.techquila.com/modules.html#cxtm.type-identity">xtm:type-identity</a> - OPTIONAL</li>
	<li><a href="http://www.techquila.com/modules.html#cxtm.type-names">xtm:type-names</a> - OPTIONAL</li>
	<li><a href="http://www.techquila.com/modules.html#cxtm.subjectIndicator">xtm:subjectIndicator</a> - OPTIONAL, REPEATABLE</li>
	<li><a href="http://www.techquila.com/modules.html#cxtm.name">xtm:name</a> - OPTIONAL, REPEATABLE</li>
	<li><a href="http://www.techquila.com/modules.html#cxtm.occurrence">xtm:occurrence</a> - OPTIONAL, REPEATABLE</li>
</ul>
</dd><dt><a name="cxtm.association"></a>xtm:association</dt><dd>This element defines a mapping from two or more properties in a meta data set to an association structure in the output topic map. An association is created only if one or more topics has been created for each of the members of the association during the processing of the current meta data set.

This element may contain the following child elements:
<ul>
	<li><a href="http://www.techquila.com/modules.html#cxtm.type-identity">xtm:type-identity</a> - OPTIONAL</li>
	<li><a href="http://www.techquila.com/modules.html#cxtm.type-names">xtm:type-names</a> - OPTIONAL</li>
	<li><a href="http://www.techquila.com/modules.html#cxtm.root-member">xtm:root-member</a> - REQUIRED</li>
	<li><a href="http://www.techquila.com/modules.html#cxtm.member">xtm:member</a> - REQUIRED, REPEATABLE</li>
</ul>
</dd><dt><a name="cxtm.type-identity"></a>xtm:type-identity</dt><dd>This element may appear as a child of the following elements:
<ul>
	<li><a href="http://www.techquila.com/modules.html#cxtm.association">xtm:association</a></li>
	<li><a href="http://www.techquila.com/modules.html#cxtm.member">xtm:member</a></li>
	<li><a href="http://www.techquila.com/modules.html#cxtm.occurrence">xtm:occurrence</a></li>
	<li><a href="http://www.techquila.com/modules.html#cxtm.root-member">xtm:root-member</a></li>
	<li><a href="http://www.techquila.com/modules.html#cxtm.topic">xtm:topic</a></li>
</ul>
This element contains only #PCDATA

The #PCDATA content of this element defines the subject indicator URI of a topic which will be used to type the topic map object created by the parent element. By default, the processor will create a single, unnamed topic with this subject indicator URI before beginning the mapping process and all objects which specify this URI as their type-identity value will regard the generated topic as defining their type (or their roleSpec, in the case of association members.

</dd><dt><a name="cxtm.type-names"></a>xtm:type-names</dt><dd>This element may appear as a child of the following elements:
<ul>
	<li><a href="http://www.techquila.com/modules.html#cxtm.association">xtm:association</a></li>
	<li><a href="http://www.techquila.com/modules.html#cxtm.member">xtm:member</a></li>
	<li><a href="http://www.techquila.com/modules.html#cxtm.occurrence">xtm:occurrence</a></li>
	<li><a href="http://www.techquila.com/modules.html#cxtm.root-member">xtm:root-member</a></li>
	<li><a href="http://www.techquila.com/modules.html#cxtm.topic">xtm:topic</a></li>
</ul>
This element wraps a list of xtm:name elements which are used to provide base name strings for the topic used to represent the type of the object generated by the parent element. This element has no attributes and contains one or more <a href="http://www.techquila.com/modules.html#cxtm.name">xtm:name</a> elements.

</dd><dt><a name="cxtm.name"></a>xtm:name</dt><dd>This element appears only within an <a href="http://www.techquila.com/modules.html#cxtm.type-names">xtm:type-names</a> element, an <a href="http://www.techquila.com/modules.html#cxtm.assoc-names">xtm:assoc-names</a> element, or an <a href="http://www.techquila.com/modules.html#cxtm.topic">xtm:topic</a> element.

This element may contain only #PCDATA

This element has the following attributes:
<ul>
	<li><code>xtm:property</code> - OPTIONAL - If specified, then the property named in the attribute value will be used to provide the content of the name string. In this case, the content of this element will be ignored.</li>
	<li><code>xtm:prefix</code> - OPTIONAL - The content of this attribute will be prefixed to the generated name string.</li>
	<li><code>xtm:suffix</code> - OPTIONAL - The content of this attribute will be appended to the generated name string.</li>
</ul>
This element defines the value of a base name string to be assigned to either the typing topic of the object generated by the parent of the xtm:type-names element which contains this element, or to the topic generated as a result of processing the parent xtm:topic element of this element.

The name string value is either simply copied from the content of this element, or if the xtm:property attribute is specified, the name string value is taken from the value of the named property in the meta data set. Each xtm:name element defines a separate base name string. Multiple names may be assigned by the use of multiple xtm:name elements, where allowed by the containing element.

</dd><dt><a href="http://www.techquila.com/cxtm.subjectIndicator">xtm:subjectIndicator</a></dt><dd>This element may appear only as a child of an <a href="http://www.techquila.com/cxtm.topic">xtm:topic</a> element.

This element must be empty

This element has the following attributes:
<ul>
	<li><code>xtm:property</code> - REQUIRED - The property which will provide the value string for the subject indicator. If this property is not present in the processed meta data set, then no subject indicator will be generated. If the property is present, then the generated subject indicator will use the value of this property.</li>
	<li><code>xtm:prefix</code> - OPTIONAL - A string which will be prefixed to the value of the property specified by xtm:property in order to create the subject indicator.</li>
</ul>
</dd><dt><a name="cxtm.occurrence"></a>xtm:occurrence</dt><dd>This element may appear as a child of the <a href="http://www.techquila.com/modules.html#cxtm.topic">xtm:topic</a> element.

This element may contain the following child elements:
<ul>
	<li><a href="http://www.techquila.com/modules.html#cxtm.type-identity">xtm:type-identity</a> - defines the URI of the subject indicator for the topic which types this occurrence.</li>
	<li><a href="http://www.techquila.com/modules.html#cxtm.type-names">xtm:type-names</a> - defines one or more base name strings for the topic which types this occurrence.</li>
</ul>
This element may have the following attributes:
<ul>
	<li><code>xtm:property</code> - REQUIRED - Specifies the key of the meta data set property which provides the value for this occurrence. If a property with this key is not found in the received meta data set, then no occurrence will be generated.</li>
	<li><code>xtm:inline</code> - OPTIONAL - If specified with the value "1", then the value of the occurrence will be resourceData rather than resourceRef, that is the value of the property specified by xtm:property will be used as an inline resource string rather than as the address of an out-of-line occurrenve resource.</li>
	<li><code>xtm:multi-valued</code> - OPTIONAL - If specified with the value "1", then the property named by xtm:property may occur more than once in the processed meta data set. The processor will create one occurrence for each property. NOTE that the representation of multiple values is (property name)_x where x is an integer value starting from 0 - the value of the xtm:property attribute should only be the property name, the suffix will be determined automatically by the processor.</li>
</ul>
</dd><dt><a name="cxtm.member"></a>xtm:member</dt><dd>This element defines a mapping from a property in the processed meta data set to one or more players of a given role in the association. For this mapping to take place, the same property must be used to create topics in the topic map (i.e. the same property key must also appear as a value of an xtm:property attribute of an xtm:topic element).

This element may appear only as a child of an <a href="http://www.techquila.com/modules.html#cxtm.association">xtm:association</a> element.

This element may contain the following child elements:
<ul>
	<li><a href="http://www.techquila.com/modules.html#cxtm.type-identity">xtm:type-identity</a> - defines the URI of the subject indicator for the topic which defines this member roleSpec</li>
	<li><a href="http://www.techquila.com/modules.html#cxtm.type-names">xtm:type-names</a> - defines one or more base name strings for the topic which defines this member roleSpec</li>
	<li><a href="http://www.techquila.com/modules.html#cxtm.assoc-names">xtm:assoc-names</a> - defines one or more base name strings for the topic which defines the type of the parent association. These name strings are scoped by the topic which defines this member roleSpec and so would be a suitable choice for a name string when displaying this association in the context of a player of this role.</li>
</ul>
This element may have the following attributes:
<ul>
	<li><code>xtm:property</code> - REQUIRED - specifies the property which is used to create the role players of this member. This property must be used to generate one or more topics in the topic map (that is, the same value must appear in an xtm:property attribute of an xtm:topic element).</li>
	<li><code>xtm:multi-valued</code> - OPTIONAL - If specified with the value "1", then the property named in the xtm:property attribute will be treated as multi-valued. Each value of the property will result in the creation of a single player of this role.</li>
</ul>
</dd><dt><a name="cxtm.assoc-names"></a>xtm:assoc-names</dt><dd>Defines a list of base name strings for the topic which types the association created by the containing xtm:association element, where each name is scoped by the topic which defines the roleSpec created by the containing xtm:member or xtm:root-member element.

This element may occur only as a child of an <a href="http://www.techquila.com/modules.html#cxtm.member">xtm:member</a> or <a href="http://www.techquila.com/modules.html#cxtm.root-member">xtm:root-member</a> element.

This element may contain the following child elements:
<ul>
	<li><a href="http://www.techquila.com/modules.html#cxtm.name">xtm:name</a> - REQUIRED, REPEATABLE - specifies the base name string to be assigned.</li>
</ul>
This element has no recognised attributes.

</dd><dt><a name="cxtm.root-member"></a>xtm:root-member</dt><dd>Defines the anchor member of an association. The processing of this element is almost exactly the same as the processing of an <a href="http://www.techquila.com/modules.html#cxtm.member">xtm:member</a> element. The only difference is that if this element is specified as being multi-valued (by having the value "1" for its <code>xtm:multi-valued</code> attribute, then one association is created for each value of the property. In each association thus created, the players of other members which are also defined as multi-valued will be taken only from the value with the matching index of the root-member.

</dd></dl>
<div>
<h2>Initialisation Parameters</h2>
<dl><dt>com.techquila.mdf.framework.XML_CONFIG</dt><dd>Defines the name of the XML file which contains the configuration to be read. The special value '_CFG_SRC_' may be used to indicate that the configuration information is contained within the MDF configuration file being read by the processing application. This allows the definition of the MDF processing chain and the XTM mapping to be contained within the same XML file.</dd></dl></div>
</div>
