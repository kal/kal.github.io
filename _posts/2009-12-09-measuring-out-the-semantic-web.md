---
layout: post
title: Measuring Out The Semantic Web
date: 2009-12-09 16:09
author: kal
comments: true
categories: [hytime, ideas, Measuring The Semantic Web, RDF, Topic Maps]
---
<strong>Introduction</strong>

In his closing keynote at this years TMRA conference (you weren't there? you should have been!), Steve Newcomb made reference to the wonders of ISO/IEC 10744 or HyTime to its friends.

HyTime is a monster standard - it is complex and so difficult to implement in its entirety that I believe only one person has ever tried. That said, the standard contains so much that is useful and generally required for a functioning Web, that many of its pieces got cannibalized, stripped down and turned into hacker-friendly W3C "standards" - XLink. Just as XML owes its very existence to SGML, so XLink and SMIL both need to look back to HyTime as an ancestor (albeit one that never gets invited to the family parties). Anyway, Steve talked about how there is still much left in HyTime that could be useful and in particular picked out Clause 9 - Scheduling as one such piece. IMHO he is right on the money.

<strong>The Problem Statement</strong>

One of the biggest problems on the semantic web or linked data web is that we have no way to communicate measurements or positions using a grounded algorithm. There is no way that a fully conformant Topic Maps processor, RDF processor or OWL reasoner can tell that a given property is actually a point on some axis. And there is no way that these processors could convert from one axis type to another (say feet to metres). To do all this with current technology you need to bake in to your application some ontology-specific knowledge - something that tells you "Values of property X are always expressed in milimeters, and values of property Y are always expressed in seconds since midnight on 1st January 1970".

It is staggering to realise that we can't do this yet on the Semantic Web when you think about it. Its even more staggering to see bold statements being made for the "Web of Linked Data" without addressing the basic problem of "How do I know what units this data is expressed in". I believe that this is where carcass of HyTime can be picked over once more :-)

<strong>What I'm going to attempt</strong>

I have decided to go back to the HyTime standard and see what can be taken away from it for the benefit of those currently struggling with merging, comparing and meaningfully transforming Linked Data. HyTime is a massive spec, and as the <a title="A Reader's Guide to the HyTime Standard" href="http://www.hytime.org/papers/htguide.html">Readers Guide To HyTime</a> recommends, I'm not going to even attempt to read all 450 pages but will instead focus just on <a title="ISO/IEC 10744 Draft" href="http://www1.y12.doe.gov/capabilities/sgml/wg8/document/n1920/html/clause-9.html">Clause 9</a>. This part of the HyTime specification deals with the issue of describing the positioning and extent of an object in N-dimensional space and provides a mechanism for defining the units used for measuring along each axis.

My hope is that this facility can be used not only for defining the size and position of objects but also as a general purpose facility for expressing measurements of all kinds, and that is going to be my closed set of problems to address:
<ol>
	<li>Specifying a measurement with a value and units in a way that allows an application to automatically compare and convert measurements that use different scales or units.</li>
	<li>Specifying a location and/or extent of an object in N dimensions where each dimension has its own associated measurement domain.</li>
</ol>
Because this will probably take some time, and because I know you are too busy to read a three-screen-long thesis, and because I would  actually value feedback as I go along, I'm going to break this exploration up into a number of separate posts. I'll create a Category to group all the posts together as I go. Please feel free to hit up the links above and dive in there and stick around for the next post where I'll start to actually read this stuff.

<strong>What Do You Think ?</strong>

I would be interested in what others think about this. Do you know of some other existing ontology for measurements ? Have you tried to do something similar yourself (and if so what were your experiences) ? What chapter did you get to in the HyTime spec ? All comments, suggestions and peanuts from the gallery are welcome in the comments!
