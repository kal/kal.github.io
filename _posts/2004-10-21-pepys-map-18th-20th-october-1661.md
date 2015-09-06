---
layout: post
title: Pepys-Map :  18th-20th October 1661
date: 2004-10-21 10:22
author: kal
comments: true
categories: [Pepys Diary]
---
<a href="http://www.pepysdiary.com/archive/1661/10/18/index.php">Three</a> <a href="http://www.pepysdiary.com/archive/1661/10/19/index.php">new</a> <a href="http://www.pepysdiary.com/archive/1661/10/20/index.php">entries</a> mapped today with one new concept added.

<!--more-->
The diary entry for <a href="http://www.pepysdiary.com/archive/1661/10/18/index.php">18th October</a> gives details of Pepys' self-treatment for his swollen groin. To model this I have created a new type of event, "medication-event" which should typically have role players "patient", "applied-by" (not necessarily a doctor, as in this case) and "medication". I have created a subclass of medication "poultice" to cover this particular treatment, and then made an instance of this class ("bran and vinegar poultice"). The entry for the diary event is:
<pre>[event-16611018-06 : medication-event
= "Samuel applies a poultice to his tumor (18th October 1661)";"16611018-06"]
occurs(event-16611018-06 : event, today : on)
participation(event-16611018-06 : event,
samuel-pepys : patient,
samuel-pepys : applied-by,
bran-poultice : medication)
[bran-poultice : poultice = "A poultice of bran and vinegar"]
{bran-poultice, description,
[[...a poultice of a good handful of bran with half a pint of vinegar and a pint of
water boiled till it be thick, and then a spoonful of honey put to it and so spread
in a cloth and laid to it]] } / samuel-pepys</pre>
Note: the definitions for the medication-event topic type and the patient and applied-by role types are contained in the pepys-diary-ontology.ltm file. The definitions for the medication topic type and the poultice topic type are in the pepys-diary-culture.ltm file.
New and updated topic maps:
<a href="http://www.techquila.com/blog/archives/16611018.ltm">Topic map for 18th October 1661.</a>
<a href="http://www.techquila.com/blog/archives/16611019.ltm">Topic map for 19th October 1661.</a>
<a href="http://www.techquila.com/blog/archives/16611020.ltm">Topic map for 20th October 1661.</a>
<a href="http://www.techquila.com/blog/archives/pepys-diary-ontology.ltm">Core ontology for the diary.</a>
<a href="http://www.techquila.com/blog/archives/pepys-diary-culture.ltm">Cultural artifacts in the diary.</a>
<a href="http://www.techquila.com/blog/archives/pepys-diary-people.ltm">People in the diary.</a>
<a href="http://www.techquila.com/blog/archives/pepys-diary-places.ltm">Places in the diary.</a>

