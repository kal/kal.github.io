---
layout: page
title: MDF - A Metadata Processing Framework
date: 2012-01-24 16:17
author: kal
comments: true
categories: []
---
MDF is a combination of a simple approach to creating reusable modules for the processing of metadata and an implementation of that approach using Java. The idea came to me when I was working as an independent consultant helping a variety of customers with XML metadata management issues. Finding that I was spending a lot of my time writing and rewriting the same sort of metadata munging code, I decided to try and find some way to make these bits of code reusable.

The driving concept behing MDF is that the processing of metadata involves a number of different stages. Depending on the source and eventual usage of the metadata any one or all four of the following stages may be required:
<ul>
	<li>Discovery: the act of trawling some resource set for metadata resources (which may or may not be combined with the content the metadata describes).</li>
	<li>Extraction: the retrieval of metadata from some set of resources.</li>
	<li>Cleaning: the processing of metadata from its retrieved format into a format which is consistent with the final application. This may include lexical processing, reformatting of data and/or the combining of multiple diverse metadata vocabularies into a single consistent vocabulary.</li>
	<li>Aggregation: the storing of the cleaned metadata together with other similarly processed metadata.</li>
</ul>
Within each of these stages, there are any number of different approaches which could be taken. For example, discovery could be by web-crawling, by executing searches or by recursing through file system directories. Extraction may require processing specific to the format of the resource retrieved. Cleaning could involve simple lexical processing (such as forcing all strings to a single case or splitting a string on particular boundaries) or complex extraction processing (such as named entity recognition on text). Finally the aggregation step might write RDF; a topic map in the XTM interchange syntax; a topic map in ISO 13250; or might be used to update a database or other datastore.

MDF attempts to improve the reusability of the different processing functions for each of these stages by defining a framework in which the functions may be designed and implemented separately and then linked together in any combination to provide the desired processing.

MDF is described in more detail in the <a href="http://www.techquila.com/mdf-techspec.html">technical specification</a>. You can also download the <a href="http://www.techquila.com/mdf-dl.html">Java MDF implementation</a>; or read about the <a href="http://www.techquila.com/modules.html">MDF modules</a> provided with the Java MDF implementation.
