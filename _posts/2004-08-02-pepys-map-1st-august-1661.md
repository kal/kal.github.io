---
layout: post
title: Pepys-Map: 1st August 1661
date: 2004-08-02 20:16
author: kal
comments: true
categories: [Pepys Diary]
---
<p>In <a href="http://www.pepysdiary.com/archive/1661/08/01/index.php">today's entry</a> the following events are modelled:</p>
<ul>
<li>Samuel travels to Walthomstow with a number of others.</li>
<li>On the way, he gossips with Mrs Browne.</li>
<li>He gives Mrs Browne a gift for her boy.</li>
<li>They dine at Walthomstow.</li>
<li>Samuel hears some opinion on Lady Batten.</li>
<li>They return home.</li>
</ul>

<!--more-->
<p>Although not much happens, this entry has led to a lot of ontological development.</p>
<p>Firstly, I introduced a gift event type, and giver and gift roles (the existing recipient topic is used for that role); so:</p>
<pre>[event-16610801-03 : gift-event
= "Samuel gives Mrs Browne six silver spoons for her boy (1st August 1661)" ;"16610801-03"]
occurs ( event-16610801-03 : event, event-16610801-01 : during )
participation (event-16610801-03 : event,
samuel-pepys : giver,
mrs-browne : recipient,
spoons : gift )</pre>
<p>Secondly, due to the plethora of venison pasties consumed this month, I added a foodstuff type (individual instances thereof to occur in the culture map), and a consumed role to be added to dining events:</p>
<pre>[event-16610801-04 : dining-event
= "Samuel and company dine at Walthamstow (1st August 1661)";"16610801-04"]
occurs ( event-16610801-04 : event, today : on )
participation( event-16610801-04 : event,
samuel-pepys : diner,
elizabeth-pepys : diner,
william-batten : diner,
william-penn : diner,
margaret-penn : diner,
venison-pasty : consumed,
walthamstow : place )
/* In culture */
[venison-pasty : foodstuff = "Venison Pasty"
@"http://www.techquila.com/psi/pepys/subjects/#venison-pasty"]</pre>
<p>This has been retrospectively added to the previous entries in which the food consumed is named (see the next post for the updates).</p>
<p>Finally, as once more there is reported news (see <a href="http://www.techquila.com/blog/archives/000064.html">29th July</a>) I have included a news event association type:</p>
<pre>[event-16610801-05 : news-event
= "Samuel hears his nurse's husband's opinion of Lady Batten (1st August 1661)";"16610801-05"]
occurs ( event-16610801-05 : event, today : on )
participation( event-16610801-05 : event,
samuel-pepys : recipient )
event-subject ( event-16610801-05 : event,
lady-batten : subject )
event-subject ( event-16610801-05 : event,
nurses-husband : subject )
{lady-batten, description,
[[She was such a man's whore, who indeed is known to leave her her estate.]]} / nurses-husband event-16610801-05</pre>
<p>The timescale of this entry is a little unclear &#x2013; I have worked on the principle that Mrs Browne is coincidentally in the same coach to Walthamstow, and that the interactions with her take place on the journey. Another possible interpretation is that it is she they are visiting in Walthamstow. I have also only included Samuel and Elizabeth on the return journey, as there is no explicit mention of the others returning.</p>
<p><b>New and updated topic map files:</b></p>
<p><a href="http://www.techquila.com/blog/archives/16610801.ltm">Topic map for this entry.</a></p>
<p><a href="http://www.techquila.com/blog/archives/pepys-diary-ontology.ltm">Core diary ontology.</a></p>
<p><a href="http://www.techquila.com/blog/archives/pepys-diary-people.ltm">People in the diary.</a></p>
<p><a href="http://www.techquila.com/blog/archives/pepys-diary-culture.ltm">Culture in the diary.</a></p>
<p><a href="http://www.techquila.com/blog/archives/pepys-diary-places.ltm">Places in the diary.</a></p>
<p><a href="http://www.techquila.com/blog/archives/pepys-diary-dates.ltm">Dates in the diary.</a></p>

