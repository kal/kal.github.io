---
layout: post
title: Pepys-Map : 30th August 1661
date: 2004-08-31 21:45
author: kal
comments: true
categories: [Pepys Diary]
---
<a href="http://www.pepysdiary.com/archive/1661/08/30/index.php">Today's entry</a> is quite short but introduces the use of scope to distinguish between sources.
The main events of the day are:
<ul>
<li>Samuel and Elizabeth go to Wardrobe Court for dinner with "the children" (the youngest children of Sir Edward Montague). There they also visit Lady Jemima Montague.</li>
<li>Samuel and Elizabeth then go on to a play which Sam does not like at all - possibly because of it being French...</li>
<li>At the play Elizabeth meets a friend of hers, described only as a son of Lord Somerset.</li>
</ul>

<!--more-->
According to the diary we know only that the play was performed at some location on Drury Street. This is modelled as a fairly light "participation" association:
<pre>participation(event-16610830-03 : event, unamed-theatre-drury-lane : place)</pre>
However, Latham & Matthews add a footnote that says that the play was most probably a performance of "Orpheus and Eurydice" at the Cockpit Theatre, performed by a company under Jean Channoveau. This gives a much richer participation association:
<pre>participation(event-16610830-03 : event,
cockpit-theatre : place,
orpheus-and-eurydice : performed-work,
channoveaus-company : performer)</pre>
However, as Latham & Matthews is a secondary source, we may want to distinguish between that information and the information extracted from the text. So this second association is scoped, using the topic for the Latham & Masters text as a scoping topic:
<pre>participation(event-16610830-03 : event,
cockpit-theatre : place,
orpheus-and-eurydice : performed-work,
channoveaus-company : performer) / lm-ii</pre>
Note, that up to now this approach of distinguishing secondary information from primary information has not been used. In future I intend to principally use it where secondary information contradicts the primary information. Going back through the posts and determining what really comes from the primary source is an excercise for the reader right now!
One other item of note for today's entry. On the pepysdiary.com site, "Lord Somersett" is linked to a page for a Thomas Somerset. A bit of googling and browsing of peerage websites leads me to believe that the Lord Somerset of 1661 was an Edward Somerset, not Thomas. I have used Edward in my representation of this event.
New and updated topic maps:
<a href="http://www.techquila.com/blog/archives/16610830.ltm">Topic map for today's entry.</a>
<a href="http://www.techquila.com/blog/archives/pepys-diary-people.ltm">People in the diary.</a>
<a href="http://www.techquila.com/blog/archives/pepys-diary-dates.ltm">Dates in the diary.</a>
<a href="http://www.techquila.com/blog/archives/pepys-diary-culture.ltm">Culture in the diary.</a>
<a href="http://www.techquila.com/blog/archives/pepys-diary-places.ltm">Places in the diary.</a>

