---
layout: post
title: Measuring The Semantic Web - Measurement Units
date: 2009-12-12 23:05
author: kal
comments: true
categories: [htyime, ideas, Measuring The Semantic Web, RDF, Topic Maps]
---
In the last post I introduced the concept from HyTime of a finite coordinate space (FCS) consisting of a number of axes each of which is tied to a measurement domain where the measurement domain might be physical or virtual. In this post we will take a look at Clause 9.2 of the standard which talks about how to define the units of measurement for a measurement domain.

Before we go there, lets just pause a moment to think about the problem here. Take length as an example. For most folks going about their daily business, the metre is a good unit of length to use for most things - I'm 1.9m tall, my room is 3.5m by 2.5m. However, for some things we tend to prefer to use smaller length units such as the corner-to-corner size of my monitor (22"), the depth of my desk (40cm...I'm guessing that one), the diameter of the jack that goes into my iPod (3.5mm). The folks that make the chips that power my PC work in nanometres, cellular scientists probably dream in picometers. Physicists are the worst - depending on their speciality a picometer might be way too big or a kilometre way too small.  If we want a measurement system that works we need some way for all of these folks to express measurements in terms of the units that make the most sense to them but at the same time be able to freely map between them.

The HyTime answer to this is to provide a way to specify a measurement domain in terms of some basic unit of measurement and then to define as many other units of measurement for that domain in terms of their ratio to the basic measurement unit. For physical measurements of space and time, HyTime provides definitions measurement domains based on the Systeme Internationale (SI) units of SI second and SI meter. The

Its probably easier to understand this if we take one of these definitions as an example (the following are all snippets from the text of clause 9.2)

Firstly our measurement domain is defined in terms of a standard measurement unit (SMU). The standard measurement unit has an identifier, and this being HyTime and based on SGML, the identifier is a formal public identifier (FPI):
<pre>&lt;!notation
   SImeter        -- Systeme International meter --
                  -- Reference unit of real length --

   PUBLIC "ISO/IEC 10744:1997//NOTATION
           Systeme International meter//EN"
&gt;</pre>
If you come from the world of XML, just think of "ISO/IEC 10744:1997//NOTATION Systeme International meter//EN" as a funny-shaped URI and you'll be doing fine. You can also think of this &lt;!notation&gt; tag as declaring a mapping from the short string "SImeter" to the longer identifier string. So this is essentially an SGML-flavoured namespace declaration.

Now we have a standard measurement unit defined and assigned an identifier we move on to use that identifier in a resource that describes our measurement domain and all of the different measurement units that can be used in it. In the HyTime specification each of these units is called a granule and a measurement domain can contain any number of granules. Every granule is defined as a multiple of some other granule in the same measurement domain (with at least one granule based on the SMU). The multiplier is expressed as a ratio of two numbers. These granule declarations are made in an SGML resource like this (I've left out many of the granules defined in the standard for brevity):
<pre><span style="font-family: Courier;">&lt;measure smu=SImeter&gt;
  &lt;granule gn=um&gt;                    1   1000 mm
  &lt;granule gn=mm&gt;                    1     10 cm
  &lt;granule gn=cm&gt;                    1     10 dm
  &lt;granule gn=dm&gt;                    1     10 meter
  &lt;granule gn=meter&gt;                 1      1 SImeter
  &lt;granule gn=dam&gt;                  10      1 meter
  &lt;granule gn=hm&gt;                   10      1 dam
  &lt;granule gn=km&gt;                   10      1 hm
  &lt;granule gn=pica&gt;                  1      6 inch
  &lt;granule gn=barleycorn&gt;            1      3 inch
  &lt;granule gn=inch&gt;                254    100 cm
&lt;/measure&gt;</span></pre>
This being SGML, end-tags are optional, so if you are an XML-head you will have to imagine a &lt;/granule&gt; inserted in the relevant places. For each granule, the granule's magnitude is specified with two numbers and a reference to another granule. The two numbers define the ratio for one granule of the type being defined to the granule referenced by the granule definition. So, a mm is 1/10th of a cm, which is in turn 1/10 of a dm, which is 1/10 of a meter, which is exactly 1 SImeter. Note that this principle works for more complex ratio's such as 1 inch being 254/100 cm (i.e. 1"=2.54cm). In this way, the standard measurement unit of an SI meter (with its FPI) is used as a base for defining all units of length measurement in a way which allows a conversion between any two particular units of measurement.

To my mind, this is a really cool facility because it means that all units are defined by the mathematical relationship between them making it possible for a machine to simply compare measurements given in different units (indeed, it provides a means for a machine to determine *if* a pair of measurements can be converted).

When I published the first post in this series, Bob DuCharme gave me a pointer to <a href="http://qudt.org/">an ontology for Quantities, Units, Dimensions and Types</a>. This has a similar approach to defining units. I think that I prefer the HyTime approach of defining conversions as a ratio of integers as it enables irrational numbers to be used in conversions (cf the definition of a barleycorn above as 1/3 of 1 inch) . What the QUDT ontology also does, which is extremely cool, is allow the definition of what HyTime calls "measurement domains" as a combination of other measurement domains. For example, a measurement domain for speed or acceleration could be defined in terms of the measurement domains for length and time.

Another interesting piece of work is <a href="http://forge.morfeo-project.org/wiki_en/index.php/Units_of_measurement_ontology">this part of the Morfeo project</a>. As with the QUDT ontology, it allows derivation of measurement domains. The wiki page I have linked to also discusses the problems of attaching measurement units to RDF property values, describing 4 different patterns with their pros and cons. For a topic map practitioner, these are instructive if we consider that an (unscoped) occurrence with a data resource is the same functionally equivalent to an RDF property with a literal value.

In the next post, I'll try to start pulling together some thoughts on a Topic Maps ontology for defining measurement units and a pattern for expressing measurements.
