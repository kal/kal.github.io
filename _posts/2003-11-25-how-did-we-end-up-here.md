---
layout: post
title: How did we end up here ?
date: 2003-11-25 10:53
author: kal
comments: true
categories: [XML]
---
Take a read through <a href="http://lists.xml.org/archives/xml-dev/200311/msg00860.html">this interesting post</a> on XML Dev. From bitter experience, I can second the assertion that to be sure that you have a valid WXS schema instance you need to validate with at least two parsers and preferably more. Worse still we have XML editors that, because they use one or the other of the common (broken) parsers or their own (usually broken) implementation, will reject valid instances or let you create invalid instances. How did we get here ?
Not such a long time ago, XML was new. Lots of people wrote parsers, because it was an easy thing to do. Lots and lots of people used those parsers because many of them were open source and/or free. Bugs were found. Bugs were fixed. Now most people use one of a handful of XML parsers that, for DTD validation at least, are robust and reliable.
W3C XML Schema has been a recommendation now for 2 and a half years. Some implementations are older than the recommendataion of course, but most are of the order of 2 years old. Why are there so many bugs ? Could it be that not as many people are using the tools (and so reporting the bugs) ? Possible, but not likely given that the W3C juggernaut is forcing even relatively sane people to use schemas in order to unbreak the mess that is Namespaces or because they need to user other standards that require schemas. So perhaps its because the developers of these tools aren't fixing bugs ? Have developers/software companies suddenly decided that parser bugs are "no big deal" - I find that hard to believe.
More likely is that W3C XML Schemas are just too complex to implement. My guess is that there are no "little bugs" left in the parsers, just nasty, hard-to-fix, deep-in-the-code bugs. The sort of bugs you get from trying to implement a specification as impenetrable as the 3 part monster from the W3C.
There is another way - RelaxNG and Schematron - now both under the wing of ISO in the <a href="http://dsdl.org">DSDL work</a>. Both have features that WXS does not. Both are much easier to understand and easier to write. The tools for these schema languages are, in my experience, robust and reliable. Of course, the reality is that WXS is here to stay and we have to deal with it - like it or not. But if you do have the luxury of a choice of schema languages, the practical programmer should take a good look at the tool sets available for these non-W3C languages and think hard before following the crowd.

