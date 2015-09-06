---
layout: post
title: "Pepys-Map : 13th September 1661"
date: 2004-09-14 20:44
author: kal
comments: true
categories: [Pepys Diary]
---
<a href="http://www.pepysdiary.com/archive/1661/09/13/index.php">Today's entry</a> has a couple of interesting points to the model.
In the first event of the day, Samuel is called to his uncle's house to discuss arrangements for the burial of his Aunt Kite who died yesterday. There are two things to note here. Firstly, we don't need to model the death as an event, because that was already entered in the biographical topic map when Aunt Kite was first introduced about a week ago. Secondly, we need to model the event of Aunt Kite's funeral in advance of its occurrence. To facilitate the merging of the event information that we have from todays entry (which is scant) with information we will probably get when the funeral takes place, I have created a subject identifier for the funeral event.
The second item of note actually comes from annotations on the PepysDiary.com site. The annotations for <a href="http://www.pepysdiary.com/p/1228.php">Doctors Commons</a> (both the map referred to from the annotations and the text of one annotation) describe the geographical location of the Doctors' Commons by the streets that form its boundary. This seemed like a good thing to model. So I have created an association type "bounded-by" and role types "bounded" for the place whose bounds are described by the association and then north-bounds, south-bounds, east-bounds and west-bounds for the four compass points (all that I need for now). The association itself is expressed as a 5-way relationship between the Doctor's Commons and the four streets that form its boundary:
<pre>bounded-by(drs-commons : bounded,
great-knightrider-st : north-bounds,
st-bennets-hill : east-bounds,
addle-hill : west-bounds,
thames-st : south-bounds)</pre>
My reason for doing this (rather than four binary relationships) is that I want the single association to capture all of the information about the boundary - in practice there can be no boundary without all of the sides being enumerated, so to my mind it doesn't make sense to have four separate partial descriptions.
I could have chosen to create a "borders-with" association, which <em>would</em> make sense to be modelled as four separate binary relationships as the fact that X border's Y is not dependent on the fact that X also borders Z.
The association and role types are all defined in the "places" topic map.

<!--more-->
New and updated topic maps:
<a href="http://www.techquila.com/blog/archives/16610913.ltm">Topic map for today's entry.</a>
<a href="http://www.techquila.com/blog/archives/pepys-diary-artifacts.ltm">Artifacts in the diary.</a>
<a href="http://www.techquila.com/blog/archives/pepys-diary-people.ltm">People in the diary.</a>
<a href="http://www.techquila.com/blog/archives/pepys-diary-places.ltm">Places in the diary.</a>

