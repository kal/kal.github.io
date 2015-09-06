---
layout: post
title: Pepys-Map: 2nd July 1661
date: 2004-07-10 17:22
author: kal
comments: true
categories: [Pepys Diary]
---
<a href="http://www.pepysdiary.com/archive/1661/07/02/index.php">Today's diary entry on pepysdiary.com</a>
<b>Topic-mapping this entry</b>
<blockquote>
To Westminster Hall and there walked up and down, it being Term time. Spoke with several, among others my cozen Roger Pepys, who was going up to the Parliament House, and inquired whether I had heard from my father since he went to Brampton, which I had done yesterday, who writes that my uncle is by fits stupid, and like a man that is drunk, and sometimes speechless.
</blockquote>
I have chosen to (for now) disregard some of the information given in this sentence. I will concentrate only on Sam's visit to Westminster Hall and his discussion with Roger Pepys.
In <a href="http://www.techquila.com/blog/archives/000040.html">yesterday's entry</a> I created a pattern for a "visiting" event that I can reuse here, even though Samuel is not visiting anyone in particular.
<pre>
[event-16610702-01:visiting-event
= "Samuel visits Westminster Hall"; "16610702-01"]
occurs(event-16610702-01 : event, today : on)
participation( event-16610702-01 : event,
samuel-pepys : visitor,
westminster-hall : place)
</pre>
Roger Pepys is a new character and so needs to be described in the topic map of people. This is is current entry.
<pre>
[roger-pepys : man = "Roger Pepys";"Pepys, Roger"
@"http://www.pepysdiary.com/p/247.php"]
</pre>
There is more information on Roger at the subject indicator URL, but I am not going to model that for now. One of the nice things about building a topic map in this way is that it is always possible to revisit the model and fill in details later on.
The discussion between Roger and Samuel focusses on Samuel's father and his uncle (the relationship of these men to Roger is not clear from the diary entry). To talk about these men as the subject of a conversation, topics are needed to represent them:
<pre>
[john-pepys : man = "John Pepys";"Pepys, John"
@"http://www.pepysdiary.com/p/154.php"]
parent-of(john-pepys : parent, samuel-pepys: child)
[robert-pepys ="Robert Pepys";"Pepys, Rober"
@"http://www.pepysdiary.com/p/884.php"]
sibling-of(john-pepys : sibling, robert-pepys : sibling)
</pre>
This introduces two new association types, 'parent-of' and 'sibling-of'. I have chosen to model these family relationships in a non-gender-specific manner for two reasons
1) It simplifies the model to not have to talk about son-of, daughter-of, and brother/sister relationships.
2) Gender is recorded on the topics that represent people (where known) which means that the gender-specific family relationship can be inferred from the types of the role-playing topics in the non-gender-specific associations.
To model this conversation I also need to create a new subclass of event, the "discussion" event. The participants in the coversation are the interlocutors, and a separate association is used to specify the subject of the conversation. In this case, the subject of the conversation are two other people. Here I have chosen to use a single association to describe the conversation subject in a 3-ary relationship rather than creating two separate binary relationships - as I read this entry, I think that the <empg>single</emph> subject of conversation is Samuel's father and his uncle, rather than there being two separate subjects of conversation.
<pre>
[event-16610702-02:discussion-event
= "Samuel's discussion with his cousin (2nd July 1661)";"16610702-02"]
occurs(event-16610702-02 : event, event-16610702-01 : during)
participation( event-16610702-02 : event,
samuel-pepys : interlocutor,
roger-pepys  : interlocutor)
event-subject( event-16610702-02 : event,
john-pepys   : subject,
robert-pepys : subject)
</pre>
<hr/>

<!--more-->
<blockquote>
Home, and after my singing master had done, took coach and went to Sir William Davenant’s Opera; this being the fourth day that it hath begun, and the first that I have seen it. To-day was acted the second part of “The Siege of Rhodes.”
</blockquote>
The singing lesson is glossed, but I have recorded it in the topic map nonetheless. The structure is the same as yesterday's entry.
The visit to the opera I model as being centered around the performance of the opera itself. This requires yet another new subclass of event, "performance" event, with a participation role played by the "company of performers", "Sir William Davenant's Opera Company". This is mentioned as being the second part of the opera, so I have titled the work accordingly.
<pre>
[event-16610702-04 : performance
= "Performance of 'The Siege Of Rhodes' (2nd July 1661)";"16610702-04"]
occurs(event-16610702-04 : event, today : on)
participation( event-16610702-04 : event,
davenants-opera : performer )
performed-work ( event-16610702-04 : performance,
the-seige-of-rhodes-part-ii : work )
[davenants-opera : company-of-performers
= "Sir William Davenant's Opera Company"]
[company-of-performers = "Company of Performers"
@"http://www.techquila.com/psi/art/#company-of-performers"]
[the-seige-of-rhodes-part-ii : opera = "The Seige Of Rhodes (Second Part)"]
</pre>
Samuel's participation in this event is as a member of the audience.
<pre>
participation( event-16610702-04 : event,
samuel-pepys : audience )
</pre>
There is also a brush with Royalty...
<blockquote>
We staid a very great while for the King and the Queen of Bohemia.
</blockquote>
So we have two new characters to add. "The King" is Charles II:
<pre>
[charles-ii : man = "Charles Stuart"; "Stuart, Charles"
= "Charles II" / charles-ii-king
@"http://www.pepysdiary.com/p/344.php"]
</pre>
His status as monarch I have modelled as a new type of event, an "office-holding" event. Within the scope of this event, "Charles Stuart" is known as "Charles II" hence this office-holding event is used to scope the name "Charles II". The office-holding event is modelled as:
<pre>
[charles-ii-king : office-holding-event = "Reign of Charles II"]
[monarch-of-england  : office = "Monarch Of England"]
occurs( charles-ii-king : event,
date-1660-05-29 : start,
date-1685-02-06 : end )
[date-1660-05-29 : date = "29th May 1660";"16600529"
@"http://www.techquila.com/psi/date-time/?gDateTime=1660-05-29"]
[date-1685-02-06 : date = "6th February 1685";"16850206"
@"http://www.techquila.com/psi/date-time/?gDateTime=1685-02-06"]
participation( charles-ii-king : event,
charles-ii : office-holder,
monarch-of-england : office-held )
</pre>
The "Queen of Bohemia" is the Lady Elizabeth Stuart.
<pre>
[elizabeth-stuart : woman = "Lady Elizabeth Stuart (The Queen of Bohemia)"
@"http://www.pepysdiary.com/p/833.php"]
</pre>
The attendence of these royal personages at the opera is modelled in the same way as Samuel's attendance - even if they did cause the whole proceeding to be held up ;-)
<pre>
participation( event-16610702-04 : event,
charles-ii : audience )
participation( event-16610702-04 : event,
elizabeth-stuart : audience )
</pre>
To find out if Samuel got to see the opera and what he thought of it, be sure to read the <a href="http://www.pepysdiary.com/archive/1661/07/02/index.php">entry at pepysdiary.com</a>
<a href="http://www.techquila.com/blog/archives/16610702.ltm">Download the topic map for today's entry</a><br/>
<a href="http://www.techquila.com/blog/archives/pepys-diary-ontology.ltm">Download the core ontology topic map</a><br/>
<a href="http://www.techquila.com/blog/archives/pepys-diary-people.ltm">Download the people topic map</a><br/>
<a href="http://www.techquila.com/blog/archives/pepys-diary-places.ltm">Download the places topic map</a>

