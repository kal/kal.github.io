---
layout: post
title: Pepys-Map : 21st - 22nd February 1662
date: 2005-02-23 21:08
author: kal
comments: true
categories: [Pepys Diary]
---
Two more entries posted today, both of which introduce new items to the ontology.
The <a href="http://www.pepysdiary.com/archive/1662/02/21/index.php">entry for 21st February</a> records the fact that Sam receives 80l. from Jaspar Trice. This is modelled as a "payment" event, with Samuel playing the role of recipient and Jaspar Trice playing the role of "payer". The sum paid is recorded as an occurrence of type "value" (previously used to record the value of items) on the payment event topic itself. So we have:
<pre>[event-16620221-04 : payment = "Samuel receives a payment from Jasper Trice (21st February 1662)";"16620221-04"]
occurs(event-16620221-04 : event, event-16620221-03 : during)
participation(event-16620221-04 : event,
samuel-pepys : recipient,
jasper-trice : payer)
{event-16620221-04, value, [[80l.]]}</pre>
In the <a href="http://www.pepysdiary.com/archive/1662/02/22/index.php">entry for 22nd February 1662</a> we learn that a group of five men have been sent to Newgate Prison for the murder of a tanner in Stoke Newington. The murder itself is modelled as a new event of type "murder", with the alleged murderers playing the role "accused", the tanner playing the role "victim" and the place "Stoke Newington" playing the role "scene". A more generalised event type of "crime" has also been created and both the new "murder" event type and the existing "theft" event type have been made subclasses of it.
<pre>[event-16620222-11 : murder = "Murder of a tanner in Newington";"16620222-11"]
occurs(event-16620222-11 : event, event-16620222-10 : end)
participation(event-16620222-11 : event,
thomas-wentworth : accused,
john-belasyse : accused,
henry-belasyse : accused,
edward-sackville : accused,
charles-sackville : accused,
unamed-tanner : victim,
newington : scene)</pre>
The gaoling of the five men is recorded as a separate event of type "imprisonment" with the murder event playing the role "charge" (meaning that the charge on which the men are imprisoned is for the crime described by the murder event); the men play the role "imprisoned" and "Newgate Prison" plays the role "gaol".
<pre>[event-16620222-10 : imprisonment = "Imprisonment of the Sackvilles, Belasyses and Thomas Wentworth on a charge of murder (22nd February 1662)";"16620222-10"]
occurs(event-16620222-10 : event, today : end)
participation(event-16620222-10 : event,
thomas-wentworth : imprisoned,
john-belasyse : imprisoned,
henry-belasyse : imprisoned,
edward-sackville : imprisoned,
charles-sackville : imprisoned,
newgate : gaol,
event-16620222-11 : charge)</pre>

<!--more-->
New and updated topic maps:
<a href="http://www.techquila.com/blog/archives/16620221.ltm">Topic map for 21st February 1662</a>
<a href="http://www.techquila.com/blog/archives/16620222.ltm">Topic map for 22nd February 1662</a>
<a href="http://www.techquila.com/blog/archives/pepys-diary-ontology.ltm">Core ontology for the diary.</a>
<a href="http://www.techquila.com/blog/archives/pepys-diary-dates.ltm">Dates in the diary.</a>
<a href="http://www.techquila.com/blog/archives/pepys-diary-people.ltm">People in the diary.</a>
<a href="http://www.techquila.com/blog/archives/pepys-diary-places.ltm">Places in the diary.</a>

