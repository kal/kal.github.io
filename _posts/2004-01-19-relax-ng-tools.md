---
layout: post
title: RELAX-NG Tools
date: 2004-01-19 22:12
author: kal
comments: true
categories: [Techquila, XML]
---
Today sees the first release of a set of stylesheets for creating documentation and diagrams from <a href="http://relaxng.org/">RELAX-NG</a> schemas.
The stylesheet rng2docbook.xsl does more or less what it says in the file name, creates a Docbook XML instance from a RELAX-NG schema. The stylesheet will document the content model and attributes of each element and each define in a RELAX-NG schema. Any documentation strings included in the default RELAX-NG documentation namespace will also appear in the Docbook output.
The second set of stylesheets creates one or more SVG diagrams from a RELAX-NG schema. You can choose to have the whole schema in a single diagram or to have separate diagrams for specific elements and defines (or for all elements and/or defines).
Read the full details on the stylesheets <a href="http://www.techquila.com/rng-tools.html">here</a>.

