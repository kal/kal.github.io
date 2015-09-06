---
layout: page
title: Download and Build
date: 2012-01-24 16:32
author: kal
comments: true
categories: []
---
<h1>Download</h1>
The latest version of MDF is release 0.3. Features of this release include:
<ul>
	<li>Bug fixes for the SimpleXTMMapper module which prevented associations from being correctly generated under certain circumstances</li>
	<li>A new ConfigurableXTMMapper module which enables topic map generation to be configured from an XML file.</li>
	<li>Configurable logging output using Log4J</li>
	<li>Fixed MDFApp to use name-spaced attributes.</li>
</ul>
Both binary and source distributions are available.

<strong>IMPORTANT for users of version 0.2.1</strong> - The MDFApp application now requires that the 'key' attribute of mdf:property elements be correctly namespaced (i.e. it shoul d be prefixed with the same prefix as the property element itself). Any existing MDF scripts must be updated to correctly namespace the key attribute.
<ul>
	<li>Download MDF 0.3 <a href="http://www.techquila.com/download/mdf/mdf-0.3-src.tar.gz">source distribution</a></li>
	<li>Download MDF 0.3 <a href="http://www.techquila.com/download/mdf/mdf-0.3-bin.tar.gz">binary distribution</a></li>
</ul>
Both packages include all of the libraries that you need to build the package and to create and run your own MDF processing chains.

A general overview of MDF can be found <a href="http://www.techquila.com/mdf.html">here</a> and documentation of the modules is available <a href="http://www.techquila.com/modules.html">here</a>.
<h1>Licensing</h1>
MDF is distributed under the same license as TM4J - the Apache Foundation license. You can read the license text <a href="http://www.techquila.com/mdf_LICENSE.txt">here</a>
<h1>Building</h1>
MDF can be built by executing either <code>build.sh</code> (on Linux) or <code>build.bat</code> (on Windows). You must execute this script from the base directory of the MDF code (the directory which contains the file <code>build.xml</code>). All of the libraries needed to build the current set of MDF modules are included in the source distribution.
<h1>Running MDF</h1>
MDF is primarily a developer's toolkit. There is one sample command-line application, com.techquila.mdf.impl.basic.MDFApp which reads an MDF processing chain definition from an XML file and executes it. See the <a href="http://www.techquila.com/modules.html">module documentation</a> for more information about the format of the configuration file it uses and how to run the application.

MDF makes use of the Log4J for reporting debug, informational, warning and error messages. By default, MDFApp and the processing modules are all fairly verbose. However, the level of output of each component is easily configured by creating a file named log4j.properties and placing it in a directory which is on the normal Java class loading path (e.g. in a directory on your CLASSPATH). To configure the level of output of the application as a whole, add the following line to log4j.properties:

<code>log4j.category.com.techquila.mdf=<em>level</em> </code>

where <em>level</em> is one of DEBUG, INFO, WARN, ERROR or FATAL

(Note that you should choose just one of the values shown above). This will configure the logging of the application as a whole to report only those messages of the specified level or greater.

You can configure individual modules to be more or less verbose by a line such as:

<code>log4j.category.<em>module-class-name</em>=<em>level</em> </code>

where <em>module-class-name</em> is the full Java class name of the module in question and <em>level</em> is one of DEBUG, INFO, WARN, ERROR or FATAL.
