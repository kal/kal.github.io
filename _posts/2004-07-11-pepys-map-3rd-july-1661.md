---
layout: post
title: Pepys-Map: 3rd July 1661
date: 2004-07-11 15:20
author: kal
comments: true
categories: [Pepys Diary]
---
<a href="http://www.pepysdiary.com/archive/1661/07/03/index.php">Today's entry</a> introduces quite a few new characters and many new social relationships.

<!--more-->
The events identified in todays entry:
1) Visit to Mr. Edward Montagu
2) Dining with Lady Jemima Montagu ("my Lady")
3) The death of Samuel Crew - a retrospective event as the death occurred on 2nd July 1661
4) Samuel enquires after some "Spanish books" in Duck Lane
5) Samuel visits Sir William Batten (with others)
6) Elizabeth Pepys and Lady Elizabeth Batten attend the funeral of an unnamed daughter of Sir John Lawson
7) The employment of Samuel Pepys by Sir Edward Montagu.
(1) and (2) are modelled in the same way as preceding events of a similar type. (2) also introduces "the Wardrobe" as a new place.
Although (3) actually happened the day before, it is modelled in the topic map for this entry:
<pre>
/* Retrospective event : Samuel Crew dies of spotted fever */
[event-16610702-r01 : death
= "Death of Samuel Crew (2nd July 1661)"; "event-16610702-r01"]
participation( event-16610702-r01 : result,
samuel-crew : deceased )
cause-of-death( event-16610702-r01 : death,
spotted-fever : cause )
[spotted-fever : disease = "Spotted Fever"]
{spotted-fever, description, [[ "A fever characterised by the appearance of spots on the skin; now spec. (a) epidemic cerebrospinal meningiti; (b) typhus; (c) Rocky Mountain spotted fever" ]]} / soed
</pre>
Note that I have also included a new occurrence type of "description" which, for the "spotted fever" topic I have use to quote from the Shorter Oxford English Dictionary (my new prized possession ;-) - hence the strangely named "soed" topic used to scope the occurrence.
(4) I struggle to model properly. Ideally I would like to model the intent to purchase Spanish books from a Duck Lane. I suspect that Tom Passin's suggestion of using thematic roles and bringing the model closer to that of conceptual graphs will help here. So I am temporarly putting off modelling this event.
(5) Is simply modelled as another "visiting event"
(6) Introduces some interesting problems:
<blockquote>
This day my Lady Batten and my wife were at the burial of a daughter of Sir John Lawson’s, and had rings for themselves and their husbands.
</blockquote>
I have chosen to model the funeral as another subclass of event. The daughter of Sir John Lawson is unamed, so she is modelled using a topic that plays the role of "child" in a parent-of relationship with the topic that stands for Sir John Lawson.
<pre>
[event-16610703-04 : funeral
= "Funeral of Sir John Lawson's daughter"; "16610703-04"]
participation( event-16610703-04 : event,
unknown-daughter : deceased,
lady-elizabeth-batten : mourner,
elizabeth-pepys : mourner )
[unknown-daughter : woman = "Unnamed Daughter of Sir John Lawson"]
parent-of(sir-john-lawson : parent, unknown-daughter : child)
</pre>
Item (7), the employment of Samuel Pepys by Sir Edward Montagu is not explicit in the diary entry, but it is an important background fact. I have chosen to model employment as a subclass of the office-holding event (which was used in <a href="http://www.techquila.com/blog/archives/000041.html">yesterday's entry</a> to model Charles Stuart holding the office of King). As we cannot tell from this entry when that employment started (or when it will end), it is not posisble to attach an "occurs" association to this topic, but it is possible to identify the key participants:
<pre>
[event-unknown-date-01 : employment
= "Employment of Samuel Pepys by Sir Edward Montagu"]
participation( event-unknown-date-01 : event,
samuel-pepys : employee,
sir-edward-montagu : employer)
</pre>
<b>New and updated topic map files:</b>
<a href="http://www.techquila.com/blog/archives/16610703.ltm">Topic map for this entry.</a>
<a href="http://www.techquila.com/blog/archives/family-relationships-ontology.ltm">Family relationships ontology.</a>
<a href="http://www.techquila.com/blog/archives/pepys-diary-ontology.ltm">Core diary ontology.</a>
<a href="http://www.techquila.com/blog/archives/pepys-diary-people.ltm">People in the diary.</a>
<a href="http://www.techquila.com/blog/archives/pepys-diary-places.ltm">Places in the diary.</a>

