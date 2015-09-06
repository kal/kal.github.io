---
layout: post
title: "Pepys-Map : Note about dates"
date: 2004-07-21 15:03
author: kal
comments: true
categories: [Pepys Diary]
---
Having just borrowed a copy of the Pepys' diaries (edited by R.C. Latham and W. Matthews), I have discovered from reading the notes that the diary entry dates are given not in the Gregorian calendar, but in the Julian calendar. This means that the dates given in the diary are actually 10 days earlier than the corresponding Georgian calendar date.
From now on I will be using the Julian dates in the titles of date and date-time instances, but will translate the subject indicator URI properly. e.g.
<pre>
[today : date = "Saturday 20th July 1661"; "16610720"
@"http://www.techquila.com/psi/date-time/?gDateTime=1661-06-30"]
</pre>
During the forthcoming refactoring of the already published topic maps I'll be updating all date-time subject indicators to make them consistent.

