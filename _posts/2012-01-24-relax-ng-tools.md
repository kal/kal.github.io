---
layout: page
title: RELAX-NG Tools
date: 2012-01-24 16:34
author: kal
comments: true
categories: []
---
The stylesheets presented here are geared towards the production of documentation from a RELAX-NG schema. The RELAX-NG syntax allows schemas to be annotated with documentation strings. The stylesheets use the structure of the RELAX-NG schema instance and the documentation strings to produce Docbook XML and SVG diagrams.

These stylesheets are licensed under the Apache Software Foundation license, the full text of the license can be found <a href="http://www.techquila.com/download/LICENSE.txt">here</a>.
<h1>RELAX-NG to Docbook (rng-doc.xsl)</h1>
<h2>What it does</h2>
This stylesheet takes a RELAX-NG schema and produces rudimentary documentation from it in Docbook XML. Each element and pattern definition gets its own documentation section. The content model of patterns/elements is described using an XML DTD-like shorthand notation.
<h2>Known Limitations</h2>
This stylesheet makes simplifying assumptions about the relationship between elements and their attributes. In particular it makes the assumption that for documentation purposes, you do not care about the use of patterns to define the attributes for your elements. It also assumes that there are not conditional relationships between elements and attributes in a content model.
<h2>How To Use It</h2>
Download the stylesheet from <a href="http://www.techquila.com/download/rng-tools/rng-doc.xsl">here.</a>

The stylesheet accepts the following parameters:

<dl><dt>title</dt><dd>The main title for the generated documentation. Defaults to "RELAX-NG Schema Documentation"</dd><dt>default.documentation.string</dt><dd>The text to provide as a default string for elements, patterns or attributes with no documentation strings.</dd><dt>intro</dt><dd>The name of an XML file to be included in the documentation. If specified, the content of this XML file should be an XML fragment rooted on the Docbook &lt;section&gt; tag.</dd><dt>target</dt><dd>If specified, limits the documentation generated to just the named element or define. If there are multiple matches (i.e. you have used the same name for both an element and a pattern) then documentation will be generated for all matches.</dd></dl>
<h1>RELAX-NG to SVG</h1>
<h2>What it does</h2>
This is a small system of stylesheets that preprocess a RELAX-NG schema into a simple tree-like structure and then renders it as a tree in SVG.

The stylesheets divide the work up into three distinct steps. This is controlled by the ANT build file included with the stylesheets in the download.
<ol>
	<li>RELAX-NG simplification.In this first step, <a href="http://dyomedea.com/">Eric van der Vlist's</a> stylesheet <code>rng-simplification.xsl</code> for applying the steps of RELAX-NG schema simplification is called. This performs (amongst other things) merging of imported schema files.

The output of step 7-12 of Eric's process is used as input into the stylesheet <code>rng-simplify-defines.xsl</code> which applies step 7-18 of the RELAX-NG schema simplification process (the intermediate steps are skipped because they would significantly impact the tree that describes the schema).</li>
	<li>Tree Generation.This step generates a simple tree representation of the entire schema. The output of this step is a render-neutral description of the schema tree. A lot of the complexity of (and information in) the source schema(s) is stripped out at this point.</li>
	<li>Diagram GenerationThis step generates one or more SVG files depending on the parameters used to invoke the process. By default one SVG file is created diagramming the entire schema, but you can produce a single diagram of a given element or pattern, or generate separate diagrams of every element and/or pattern defined in the schema.</li>
</ol>
<h2>Known Limitations</h2>
<ul>
	<li>Does not handle the <code>nsName</code> element.</li>
	<li>Does not handle the <code>choice</code> element inside <code>name.</code></li>
	<li>I'm sure there are some more. Let me know if you find them.</li>
</ul>
<h2>How To Use It</h2>
The complete package is available for download from <a href="http://www.techquila.com/download/rng-tools/rng-svg-latest.zip">here</a>. The zip file contains a README.txt file that explains everything!
