---
layout: post
title: Representing Events In Topic Maps
date: 2004-06-10 08:19
author: kal
comments: true
categories: [Topic Maps]
---
Some thoughts on representation of historical events using topic maps.
In a large part, the thoughts here are inspired by <a href="http://www.heml.org/">Historial Event Markup Language</a>.

<!--more-->
An event representation pattern must address at least the questions:
<ul>
<li> What ? </li>
<li> Who ? </li>
<li> Where ? </li>
<li> When ? </li>
</ul>
The pattern should be extensible to enable <i>Why ?</i> and <i>How ?</i> to be represented using additional topic map constructs.
<h2> What ? Event type </h2>
The basis of the pattern is that events are represented as topics - this enables an event to be treated as a thing in its own right, to be named and to be related to other resources and topics. Creating a topic for an event essentially answers the "What ?" question by providing a topic proxy for the "What".
<h2> Who ? Event Participation </h2>
Event participation is best represented using an association. There are two possible choices here:
<ol>
<li>An association meta-type could be used to identify participation associations. In this case the types of the associations would be unrestricted as long as those types are themselves typed with the "event participation association" meta-type. However, this could be quite heavyweight and may not be necessary.</li>
<li> An association type for event participation with a single defined role for the event participated in. The role played by each participant could then be unrestricted. If multiple roles are played in an event by the same participant, there should be one association role for each role played. </li>
</ol>
<h2> Where ? Event Location </h2>
Again there are two possible solutions to this.
<ol>
<li> Use a defined occurrence type to allow a geolocation code to be specified for an event. </li>
<li> Use a defined association type to allow a relationship between a geographic region and an event to be made. </li>
</ol>
In practice, (1) would be most suitable when there is point data. Some point data may require multiple separate axes in which case it might be best to simply define a meta-type for "location component" occurrences. This would enable not only normal GPS-style geolocation coordinate systems but also more complex location systems such as those used in astronomy. (2) would be more suitable when an identifiable place such as a city, country or region is involved, and ideally where there is a controlled list of such places.
There is nothing, of course to prevent these two solutions being combined and if "location component" occurrences are also used to provide location information for "location" topics, this enables inferencing to be used to extract relevant location information.
<h2> When ? Event Times </h2>
This is complex as HEML shows.
Factors to consider include:
<ul>
<li> There are <a href="http://astro.nmsu.edu/~lhuber/leaphist.html">multiple calender systems</a> to consider. Most are dirunal which means that there should be a one-to-one mapping between a date in one calendar system and a date in another system. </li>
<li> Some calendar systems involve multiple epochs (e.g. the Chinese and Japanese systems of measuring years in the reign of the Emporer). </li>
<li> Some events are macro with respect to our standard calendar systems (e.g. evolutionary events such as the era(s) of a particular dinosaur's existence). </li>
<li> Some events are micro with respsec to our standard calendar systems (e.g. the events occuring inside a high-energy physics experiment. </li>
<li> Some events have a range (start date/time and end date/time). </li>
<li> Some events have an unknown or only roughly known start/end time. </li>
<li> Some events are known only to have preceded or followed other events, but may have no fixed time themselves. </li>
It appears that HEML provides a way forwards for handling most if not all of these issues so the next step must be to attempt to create a set of topic map PSIs that can reflect the HEML model.

