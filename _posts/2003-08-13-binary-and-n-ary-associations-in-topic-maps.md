---
layout: post
title: Binary And N-Ary Associations In Topic Maps
date: 2003-08-13 15:20
author: kal
comments: true
categories: [Topic Maps]
---
A common modelling decision in creating a topic map is when to use an association with 3 or more roles (an n-ary association) and when to represent it as n-1 binary associations. Herewith a discussion on the relative merits of the two forms and some pointers (ok, opinions) on the Right Thing To Do.

<!--more-->
In many cases in creating topic maps we are presented with the issue of how to represent n-way associations. Some examples could be:
<ol>
<li>The members of a department (an association between one department and n-1 people)</li>
<li>The books written by an author (an association between 1 author and n-1 books)</li>
<li>The parts of an machine (an association between 1 whole and n-1 parts)
<li>A vote taken by a committee (an association between a decision and n-1 committee members)</li>
<li>A murder depicted in an opera (an association between a victim, a murderer and a method of death)</li>
</ol>
<p>The issue that comes up is whether to code these relationships in a single multi-legged association (an n-ary association) or several two-way associations (binary associations). There are trade-offs to be made, but in my opinion the first rule of thumb is:</p>
<p><b>Smaller is Better</b></p>
Or more specifically, "More granular is better" - the smaller statements we make, the more control we have over them. Breaking statements up without creating new topics gives us the ability to apply metadata to those statements individually and to query, traverse and modify one statement without any impact on or concern for the others.
Of course, there is a point of diminishing returns and this is when you need to start adding new classes of entity to your model to be able to split up n-way associations. In general, if you can break up an n-way association without creating new topics, do it. If you need to create a new topic to break up an association it is likely that you are creating a topic that represents the fact of the association - if you end up having a need for that, then all well and good, but in most cases, it is something to be avoided as once you start down this reification route, its hard to know when to stop.
The second rule of thumb I follow is to ask:
"Is the association divisible <b>without creating another topic</b>."
In other words would it make sense to divide up the association into smaller (typically binary) associations.
Another third useful rule of thumb is:
"Does the presence of one player of a given role have any bearing on the presence of the other players"
In other words, if one player were removed, would the statement being made suddenly become untrue (rather than just incomplete).
So, with those three rules of thumb in hand...lets play the "Binary or N-Ary Game"!
<ol>
<li><i>The members of a department (an association between one department and n-1 people)</i><br/>
<b>BINARY!</b> - If Fred, Joe and Barney are members of the Finance Department, Fred and Joe will still be members after Barney retires. There is no dependency between the players of the 'member' role, so we can model this association as 3 binary associations rather than one four-way association.</li>
<li><i>The books written by an author (an association between 1 author and n-1 books)</i><br/>
<b>BINARY!</b> - 'Hunter S. Thompson wrote "Fear and Loathing in Las Vegas" and "Hell's Angels"'. These are independent facts and the statement as it stands is incomplete anyway (Thompson wrote more than those two books). In both English and Topic Maps, I can break this statement up into 'Hunter S. Thompson wrote "Fear and Loathing in Las Vegas"' and 'Hunter S. Thompson wrote "Hell's Angels"'. So I would model this as two binary associations rather than a single 3-way association.</li>
<li><i>The parts of an machine (an association between 1 whole and n-1 parts)</i><br/>
<b>BINARY! or N-ARY!</b> - If the meaning of the association is that it is a closed and complete list of all the components which make up the machine, it is reasonable to argue that without one of the components, the machine is not complete so in this case we should use an N-ary association that explicitly groups together all the components. On the other hand, often such part-whole relationships are often not complete (e.g. "The engine contains a fuel pump, spark plugs and a carburettor"), in which case the individual parts are independently related to the whole and so should be represented with binary associations.</li>
<li><i>A vote taken by a committee (an association between a decision and n-1 committee members)</i><br/>
<b>N-ARY!</b> - There is an example in the <a href="http://www.w3.org/TR/1999/REC-rdf-syntax-19990222/#containers">RDF Model And Syntax Specification</a> (see section 3.5) which goes "The committee of Fred, Wilma, and Dino approved the resolution". The association between the resolution and Fred, Wilma and Dino cannot be subdivided as the decision was made collectively - we do not want to assert that one of the three made the decision, but instead that all three came to the decision (by some undocumented means). So in this case, an N-Ary association provides us with the necessary dependency between the committee members and the decision made.</li>
<li><i>A murder depicted in an opera (an association between a victim, a murderer and a method of death)</i><br/>
<b>N-ARY</b> - No article on topic maps is complete without a reference to <a href="http://www.ontopia.net/omnigator/models/topicmap_complete.jsp?tm=opera.xtm">Italian Opera</a> and this is no exception. The classic Ontopia topic map contains 4 way associations such as "Baron Scarpia was kiled by stabbing by Tosca in the opera Tosca" - the role players are Baron Scarpia (playing the role of victim), Tosca the character(playing the role of perpetrator), stabbing (playing the role of cause of death) and Tosca the opera (playing the role of opera). To break this down into binary associations we would need to create a new topic of type murder, then we could say:
<ul>
<li>The victim of the murder was Baron Scarpia</li>
<li>The perpetrator of the murder was Tosca</li>
<li>The method of the murder was stabbing</li>
<li>The murder is depicted in Tosca (the opera)</li>
</ul>
However, this requires us to create a new class of entity (the murder) and so to follow the rules of thumb above, and avoid this additional reification step, we instead use the n-ary association which adequately (for our purposes) expresses the dependencies between the four role players.</li>
<b>Conclusion</b>
Modelling associations is best done with a bit of thought. Although the temptation is to just stuff as much as possible into a single association (especially when writing XTM syntax by hand), using small associations where possible gives you more flexibility in the long run as it allows greater control over attaching metadata to specific statements.
More granular associations also enable a great deal more clarity. Allowing the author to be explicit about whether role players are interdependent or not is important and making use of standard topic map machinery to do that means that you need not be dependent on an ontology description to make clear what the topic map model is already capable of expressing.
Thinking about the arity of associations at the time you are constructing your topic map ontology will reap benefits in the long run.

