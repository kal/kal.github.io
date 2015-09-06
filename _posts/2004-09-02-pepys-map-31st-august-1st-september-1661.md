---
layout: post
title: "Pepys-Map : 31st August - 1st September 1661"
date: 2004-09-02 21:24
author: kal
comments: true
categories: [Pepys Diary]
---
Two entries posted today.
In the entry for 31st August, Samuel describes his visit to Bartholomew Fair. The fair is an extended event starting on 23rd August and ending on 6th September. Within the span of this event, today describes a number of separate events that involve Samuel directly. To model this, I have created one recreation-event topic for the fair itself covering the complete 23/8-6/9 timespan. Then each event that occurs at the fair is created as a "subevent" of the fair event. This requires a new association type for relationship between an encompassing event and the events that it encompasses (which I've called superevent and subevent as a shorthand).

<!--more-->
For example a performance by dancing monkeys (no, really) at the fair is modelled as:
<pre>
[event-16610831-06 : performance = "Performance by dancing monkeys at Bartholomew Fair (31st August 1661)";"16610831-06"]
occurs(event-16610831-06 : event, today : on)
superevent-subevent(event-16610831-06 : subevent, bartholomew-fair : superevent)
</pre>
This type of relationship could also be useful for other spanning events, and could be treated as hierarchical. For example a war could be a spanning event (superevent) with each battle as an encompassed event (subevent). Then within the battle, each charge or manoeuver could be modelled as a subevent of the battle event.
Another slightly odd construct in the topic map for 31st August is the modelling of Samuel buying a bauble for each of three ladies in his company at Christ's Hospital. This is modelled as a single purchasing-event where three separate items are purchased, followed by three separate gift events, each with one of those purchased items and a different recipient:
<pre>
[event-16610831-09 : purchasing-event = "Samuel buys baubles for the ladies (31st August 1661)";"16610831-09"]
occurs(event-16610831-09 : event, event-16610831-07 : during)
participation(event-16610831-09 : event,
samuel-pepys : purchaser,
bauble-1 : purchased,
bauble-2 : purchased,
bauble-3 : purchased)
[bauble-1 : bauble = "A bauble for Jemima Carteret"]
[bauble-2 : bauble = "A bauble for Paulina Montague"]
[bauble-3 : bauble = "A bauble for Mlle Le Blanc"]</pre>
<pre>[event-16610831-10 : gift-event = "Samuel gives a bauble to Jemima Carteret (31st August 1661)";"16610831-10"]
occurs(event-16610831-10 : event, event-16610831-07 : during)
participation(event-16610831-10 : event,
bauble-1 : gift,
samuel-pepys : giver,
jemima-carteret : recipient)
<em>etc.</em>
</pre>
In the entry for 1st September, an interesting revalation is made. The tankard that was stolen from William Penn and which Sam wrote a joke confessional for a few days ago, was actually stolen as a joke by William Batten. So we have a bit of new information to add to the theft-event that was created in the topic map for 28th August 1661. To do this, I have added a subject indicator to the original theft event so that it can be imported into the topic map for 1st September. I can then use that imported topic to create a new association and an occurrence that describes the theft in Sam's own words. Although the topic map standard does allow me to simply refer to the address of the original event topic rather than do this import trick, using a full URI subject indicator is a bit more robust and won't break if the files are moved into different relative paths (e.g. split into separate directories for each month).
New and updated topic maps:
<a href="http://www.techquila.com/blog/archives/16610831.ltm">Topic map for 31st August 1661</a>
<a href="http://www.techquila.com/blog/archives/16610901.ltm">Topic map for 1st September 1661</a>
<a href="http://www.techquila.com/blog/archives/16610828.ltm">Modified topic map for 28th August 1661</a>
<a href="http://www.techquila.com/blog/archives/pepys-diary-ontology.ltm">Core ontology</a>
<a href="http://www.techquila.com/blog/archives/pepys-diary-artifacts.ltm">Artifacts in the diary.</a>
<a href="http://www.techquila.com/blog/archives/pepys-diary-culture.ltm">Culture in the diary.</a>
<a href="http://www.techquila.com/blog/archives/pepys-diary-dates.ltm">Dates in the diary.</a>
<a href="http://www.techquila.com/blog/archives/pepys-diary-people.ltm">People in the diary.</a>
<a href="http://www.techquila.com/blog/archives/pepys-diary-places.ltm">Places in the diary.</a>
<strong>TEASER:</strong> Look out for another month-end merged topic map tomorrow!

