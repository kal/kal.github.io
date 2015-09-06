---
layout: post
title: Measuring Out The Semantic Web - Definitions
date: 2009-12-10 16:05
author: kal
comments: true
categories: [hytime, ideas, Measuring The Semantic Web, RDF, Topic Maps]
---
In this post I'm going to look at <a title="ISO/IEC 10744 - Clause 9.1 Scheduling Concepts and Definitions" href="http://www1.y12.doe.gov/capabilities/sgml/wg8/document/n1920/html/clause-9.1.html" target="_blank">Clause 9.1</a> of the HyTime standard - hit the link to bring it up in a new window if you want to follow along.

<!--more-->

First off, the term "Scheduling" might strike you as an odd term - it certainly fooled me. In fact all of Clause 9, with its references to "events" and "scheduling" might make you think you have accidently stumbled into a meeting of the iCal working group. However the first sentence of Clause 9.1 reassures that "scheduling" an object is no more than "giving them a position and size". HyTime's language is time-oriented, but the standard itself - as the rest of this clause makes clear - is neutral about how many and what types of axes we use to give an object position and size. That said, we are going to have to get used to the fact that in the rest of our exploration of this standard "scheduling" means defining position and size - i.e. measuring; and "event" means the thing being measured.

What this clause of HyTime is aiming to do is to provide us with a mechanism for interchange of the measurement of objects (real or virtual) in a way that it is possible to ground an application with the minimal amount of predefined "magic" needing to be baked into[1] an application. To do that we need some sort of model, and in Clause 9.1 the model is described in high-level terms.

The scheduling of events (positioning of objects) in HyTime is done by first defining a set of bounded axes that define the space within which those events exist - this is called a "finite coordinate space" (FCS). Each FCS is made up of a finite number of such axes, and each axis in an FCS has a finite length and is assigned to some measurement domain that defines the units of measurement along that axis. The room I am sitting in now is a FCS, with three axes whose sizes are bounded by the length, breadth and height of the room and where the measurement domain can be most conveniently (for the purposes of interchange) be expressed in metres. A piece of music can be seen as a FCS with axes denoting pitch, volume and time. Pitch could be expressed in hertz, and volume in decibels. Time in music is somewhat different however - the time in a piece of music cannot be expressed in seconds because all the timings are relative to the tempo at which the piece is performed. For this purpose HyTime allows some axes to use virtual measurement units - that is measurement units that have no absolute physical basis. The standard also allows for the fact that an axis that uses a virtual measurement unit might at some point be projected on to real, physical measurement domain (when the musician picks up their instrument and starts to play at a given tempo). A note (Note 257 if you are looking at the text of the standard) also helpfully points out that the measurement domain for an axis can even be an ordered set of things (the standard calls them topics, but all Topic Mappers know that a topic is anything...right?). So I can say that the books on my bookshelf form a measurement domain, where 1 is the first book from the left, 2 is the second one and so on.

For our purposes of expressing measurements for Linked Data, I suspect that this last interpretation for axes is probably not of much use, but the idea of allowing for axes that have a physical measurement and axes that have a relative measurement is of immense use as is the concept of mapping relative measurements on to physical axes at run-time.

So to recap what we have learnt so far:
<ol>
	<li>To start measuring things we first need to define the space within which all of those measurements will lie.</li>
	<li>The space we define can have as many dimensions to it as we want. Each dimension has its own axis.</li>
	<li>Every axis must be bounded. That is it must have a start point and an end point.</li>
	<li>Every axis must have an associated measurement domain that defines the units used to measure along that axis.</li>
	<li>A measurement domain may be some real, physical domain such as length, frequency, volume or temperature. A measurement domain may be some virtual domain where positioning is all relative.</li>
</ol>
In the next post I'll be looking at what the HyTime standard and other unit ontology efforts have to say about units of measurement.

<em>[1] I suspect that the editors of the standard would use the more appropriate term "disclosed". All interchange syntaxes that deal with semantics need to be grounded in some set of "things that need to be known by the application in advance of processing this stuff". How a disclosure is made to an application is where standards get into the realms of hand-waving. Generally this means that a programmer (yes, you at the back) needs to hard-code stuff or write some clever (but non-standard) configuration voodoo.</em>
