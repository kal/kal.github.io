---
layout: post
title: Pepys-Map: 4th July 1661
date: 2004-07-12 20:30
author: kal
comments: true
categories: [Pepys Diary]
---
The events described by <a href="http://www.pepysdiary.com/archive/1661/07/04/index.php">this diary entry</a> are:
1) Samuel visits the theatre to see a performance of "Clarcilla". A combination
of the annotations on the pepysdiary.com site and some quick googling shows
that this is a play (not an opera), performed by the theatre company of
Sir Thomas Killigrew, also known as the "King's Company".
2) Samuel calls on his father
3) Samuel visits the Royal Exchange
4) Samuel goes to the Mitre tavern with his uncle William Wight. The
Mitre is typed as a "tavern" which is a subclass of "building"
which is in turn a subclass of "place". The location of the Mitre
is given in the pepysdiary.com annotations as Fenchurch Street.
Fenchurch Street is modelled as a "thoroughfare" and the location
of the Mitre is given by a "located-on" association.
<pre>
[the-mitre : tavern = "The Mitre"
@"http://www.pepysdiary.com/p/910.php"]
[fenchurch-st : thoroughfare = "Fenchurch Street"]
located-on(the-mitre : place, fenchurch-st : route)
</pre>
5) Samuel and William discuss the fact that Samuel's father has travelled to
the Pepys' farm at Brampton. This implies and event of John Pepys travelling
to Brampton.
6) Samuel and Mr Batersby (also known as John Battersby) the apothecary
discuss Samuel's uncle's haemmoroids (I wonder just how "merry" Sam
had to be to get on to this topic of conversation!).

<!--more-->
<b>New and updated topic map files:</b>
<a href="http://www.techquila.com/blog/archives/16610704.ltm">Topic map for this entry.</a>
<a href="http://www.techquila.com/blog/archives/family-relationships-ontology.ltm">Family relationships ontology.</a>
<a href="http://www.techquila.com/blog/archives/pepys-diary-ontology.ltm">Core diary ontology.</a>
<a href="http://www.techquila.com/blog/archives/pepys-diary-people.ltm">People in the diary.</a>
<a href="http://www.techquila.com/blog/archives/pepys-diary-places.ltm">Places in the diary.</a>

