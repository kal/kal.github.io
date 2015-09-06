---
layout: post
title: Pepys-Map: 8th - 13th July 1661
date: 2004-07-16 21:17
author: kal
comments: true
categories: [Pepys Diary]
---
The topic map for <a href="http://www.pepysdiary.com/archive/1661/07/13/index.php">this diary entry</a> records two linked events and it is worth examining these in a bit of detail. Much of the start of the entry I have ignored for now as it deals with a general process of arranging the estate of Robert Pepys. The events I have modelled are the return of Mr Phillips from London to Brampton, and the disucssion between Samuel Pepys, John Pepys and Mr Phillips regarding the estate of Robert.
The travelling is modelled using a topic in much the same way as Samuel's journey to Brampton was:
<pre>
[event-16610713-1 : travelling-event
= "Lewis Phillips travels from London to Brampton"]
participation(event-16610713-1 : event, lewis-phillips : traveller)
route-taken( event-16610713-1 : event, london : from, brampton : to)
</pre>
The difference here is that we are not told exactly when this journey occurs, we only have the date range of the entry to go on. The diary entry makes it clear that Mr. Phillips arrival was towards the end of the period covered, which means that we can justifiably rule out any day before 8th July as the start date for the travel, and we know that he arrived by the end of the period covered. So we have earliest and latest bounds for both the start and end of the event and use these to make a 4-ary association describing when the event occurs.
<pre>
occurs(event-16610713-1 : event,
entry-start : start-after,
today : start-before,
entry-start : end-after,
today : end-before)
</pre>
The second event (the discussion) must follow the first as Mr. Phillips must have arrived in Brampton before having the discussion. So we can use the first event as an earliest bound on the discussion event and the end of the diary entry period as a ltest bound.
<pre>
[event-16610713-2 : discussion
= "Samuel and John Pepys discuss Robert Pepys' estate with Mr. Phillips"]
occurs( event-16610713-2 : event,
event-16610713-1 : start-after,
today : end-before )
participation( event-16610713-2 : event,
john-pepys : interlocutor,
samuel-pepys : interlocutor,
lewis-phillips : interlocutor)
event-subject( event-16610713-2 : event,
robert-pepys-estate : subject)
[robert-pepys-estate = "The estate of Robert Pepys"]
</pre>
Note that for now, the estate of Robert Pepys is simply named and not assigned a subject identifier - if future diary entries make further reference to it, it may be necessary to create and assign a subject identifier for this topic.

<!--more-->
<b>New and updated topic map files:</b>
<a href="http://www.techquila.com/blog/archives/16610713.ltm">Topic map for this entry.</a>
<a href="http://www.techquila.com/blog/archives/family-relationships-ontology.ltm">Family relationships ontology.</a>
<a href="http://www.techquila.com/blog/archives/pepys-diary-ontology.ltm">Core diary ontology.</a>
<a href="http://www.techquila.com/blog/archives/pepys-diary-people.ltm">People in the diary.</a>
<a href="http://www.techquila.com/blog/archives/pepys-diary-places.ltm">Places in the diary.</a>

