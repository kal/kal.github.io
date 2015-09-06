---
layout: post
title: "Pepys-Map :  5th November"
date: 2004-11-09 13:19
author: kal
comments: true
categories: [Pepys Diary]
---
I've fallen a little bit behind with the topic maps due to travelling.
The events modelled for <a href="http://www.pepysdiary.com/archive/1661/11/05/index.php">5th November 1661</a> are as follows:
<ul>
<li>Samuel works at the Navy Office.</li>
<li>Thomas Pepys and William Armiger dine with Samuel at the Pepys' house.</li>
<li>Samuel and William Penn pay a visit to Elizabeth Batten.</li>
<li>William Batten travels to Chatham (the travelling event started some time before Pepys and Penn visit Lady Batten).</li>
<li>Samuel, Penn and George Cocke go drinking at the Dolphin Tavern</li>
<li>Pepys and Penn return to Lady Batten's</li>
<li>Pepys returns home from the Batten's.</li>
</ul>

<!--more-->
In addition to posting this entry, I've begun to make changes to the representation of marriage. Up to now, marriage has been represented as a simple association like:
<pre>married-to(samuel-pepys : spouse, elizabeth-pepys : spouse)</pre>
Marriage is now modelled as an event, allowing us to specify the temporal bounds on the marriage and to use the marriage as a subject in its own right.
I've made use of scoped names to present different ways of presenting and indexing the marriage event. e.g.
<pre>[thomas-katherine-fenner-marriage
= "Marriage of Thomas Fenner and Katherine Kite"
= "Marriage to Katherine Kite";"Fenner, Thomas;marriage to Katherine Kite" / thomas-fenner
= "Marriage to Thomas Fenner";"Kite, Katherine;marriage to Thomas Fenner" / katherine-kite]
participation(
thomas-katherine-fenner-marriage : event,
katherine-kite : spouse,
thomas-fenner : spouse )</pre>
This is particularly useful for scoping the married name of women. e.g.
<pre>[katherine-kite : woman = "Katherine Kite"; "Kite, Katherine"
= "Katherine Fenner";"Fenner, Katherine" / thomas-katherine-fenner-marriage
@"http://www.pepysdiary.com/p/750.php"]</pre>
New and updated topic maps:
<a href="http://www.techquila.com/blog/archives/16611105.ltm">Topic map for 5th November 1661.</a>
<a href="http://www.techquila.com/blog/archives/family-relationships-ontology.ltm">Family relationships ontology.</a>
<a href="http://www.techquila.com/blog/archives/pepys-diary-people.ltm">People in the diary.</a>

