---
layout: post
title: Pepys-Map : 3rd October 1661
date: 2004-10-04 11:57
author: kal
comments: true
categories: [Pepys Diary]
---
<a href="http://www.pepysdiary.com/archive/1661/10/03/index.php">Today's entry</a> makes use of topic map merging to handle a reference to a previous event.
The event in question is a disucssion of the performance of Vittoria Corombona that took place on 2nd October. To make a reference to the performance event, I have simply created a topic whose subject identifier is the address of the topic created for the performance event. The reference is made using a relative URI and it assumes that the topic map for 2nd October is located in the same directory as that for 3rd October (which is the case for the archived LTM files). The result is the following LTM code:
<pre>[event-16611002-05-ref @"16611002.ltm#event-16611002-05"]</pre>
I have also made an editorial pass through the topic types defined in the core ontology file today, creating sort names that omit the indefinite article to improve the sorting in displays like Omnigator and TM4Web.
This can then be used as any other event topic. For example, we discover today that Elizabeth Batten and her son had been at the same performance. We can model this as:
<pre>[event-16611002-05-ref @"16611002.ltm#event-16611002-05"]
participation(event-16611002-05-ref : event,
william-batten-son : audience,
elizabeth-batten : audience)</pre>
We can also use the event as the subject of the discussion event that takes place today:
<pre>[event-16611003-09 : discussion
= "Samuel discusses yesterday's performance of
'Vittoria Corombona' with the Battens (3rd October 1661)";"16611003-09"]
...
event-subject(event-16611003-09 : event, event-16611002-05-ref : subject)
</pre>

<!--more-->
New and updated topic maps:
<a href="http://www.techquila.com/blog/archives/16611003.ltm">Topic map for 3rd October 1661.</a>
<a href="http://www.techquila.com/blog/archives/pepys-diary-ontology.ltm">Core ontology for the diary.</a>
<a href="http://www.techquila.com/blog/archives/pepys-diary-people.ltm">People in the diary.</a>
<a href="http://www.techquila.com/blog/archives/pepys-diary-places.ltm">Places in the diary.</a>

