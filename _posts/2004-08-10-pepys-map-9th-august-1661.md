---
layout: post
title: "Pepys-Map: 9th August 1661"
date: 2004-08-10 01:49
author: kal
comments: true
categories: [Pepys Diary]
---
<p>A very busy day <a href="http://www.pepysdiary.com/archive/1661/08/09/index.php">today</a>. The following events are modelled:</p>
<ul>
<li>Samuel goes to the office, where he receives news that Andrew Pearse is dying.</li>
<li>Samuel visits Pearce, and then returns to the office.</li>
<li>Receiving news that Sir George Carteret has invited officers to lunch, Samuel leaves the office to see if he is called to join them; he is not.</li>
<li>Dining at home instead, Thomas Hayter brings news that his wife is in labour, and Elizabeth Pepys leaves with him to see her.</li>
<li>Samuel goes to Whitehall, where he meets the Lord Privy Seal, and conducts some business with him.</li>
<li>Samuel and M d'Esquier visit Elizabeth Pearce, who is pregnant, and meet a Mrs Clifford there.</li>
<li>Samuel visits his father, and returns home, where his wife informs him Mrs Hayter is still in labour.</li>
</ul>

<!--more-->
<p>Not just a lot of events, but a lot of difficult ones as well today.</p>
<p>Samuel's leaving of the office to see if he is actually called to lunch with Sir George I have simply left as an event.  Henry Moore's reading of the bills in the Lord Privy's chambers is also classed just as an event; this is more because it seems to be some kind of legal protocol, and I don't know the details.</p>
<p>The main point of note, though, is an illness, pregnancy, and labour all being mentioned on one day have led me to create a class of health events, with subclasses of pregnancy, labour, and illness (more subclasses will undoubtably come... just wait for <a href="http://en.wikipedia.org/wiki/Great_Plague">1665</a>).  There is a patient role, and the individual events are given occurs associations using start-before today, or start on today. I included the individual events in the pepys-diary-people map as it directly relates to them, and may be referenced on more than one day.  So, for instance:</p>
<pre>/* In pepys-diary-people.ltm */
[mrs-hayter-labour : labour = "Mrs Hayter's labour (9th August 1661)
@"http://www.techquila.com/psi/pepys/people/#mrs-hayter-labour"]
occurs ( mrs-hayter-labour : event, date-16610809 : start )
participation ( mrs-hayter-labour : event,
mrs-hayter : patient )
/* In 16610809.ltm */
[event-16610809-08 : news-event =
"Samuel and his wife receive news from Thomas Hayter that his wife is pregnant (9th August 1661)";"16610809-08"]
occurs ( today : on,
event-16610809-08 : event )
participation ( event-16610809-08 : event,
samuel-pepys : recipient,
elizabeth-pepys : recipient,
thomas-hayter : informant,
seething-lane-house : place )
event-subject ( event-16610809-08 : event,
mrs-hayter-labour : subject )</pre>
<p>I may retrospectively implement these classes in previous entries.</p>
<p><b>New and updated topic map files:</b></p>
<p><a href="http://www.techquila.com/blog/archives/16610809.ltm">Topic map for this entry.</a></p>
<p><a href="http://www.techquila.com/blog/archives/pepys-diary-ontology.ltm">Core diary ontology.</a></p>
<p><a href="http://www.techquila.com/blog/archives/pepys-diary-places.ltm">Places in the diary.</a></p>
<p><a href="http://www.techquila.com/blog/archives/pepys-diary-people.ltm">People in the diary.</a></p>
<p><a href="http://www.techquila.com/blog/archives/pepys-diary-dates.ltm">Dates in the diary.</a></p>

