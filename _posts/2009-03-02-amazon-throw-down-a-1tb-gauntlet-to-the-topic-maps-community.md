---
layout: post
title: Amazon throw down a 1TB gauntlet to the Topic Maps Community
date: 2009-03-02 21:40
author: kal
comments: true
categories: [ideas, opendata, Semantic Web, Topic Maps]
---
It is very interesting to see that Amazon have now made available over <a href="http://aws.amazon.com/publicdatasets/">1TB of public data</a>. Its great that all of this data is now available in one place, ready shredded into queryable structures that allows developers to get to grips with it and start to do something really interesting. But wait a minute, if I want the DBPedia dump I have to go here..., if I want the Wikipedia english articles I need to go over there. If I want the US census data from 2000 its this place, if its the census data from 1990, its somewhere else. Oh and don't even get me started on having to choose between Windows and Linux. What these data sets are are essentially separate database snapshots that you can load into your own EC2 instance in the Amazon cloud and then start processing.

...and thats kind of disappointing. Having lots of open data is a great start, but it is only a start. And here is the challenge - there are no consistent semantics acrosss these data sets, there is a great deal of wet-ware time that needs to be invested in working out the linkages between them and in getting hold of some consistent notions of identity that could assist in merging. The easy way out is to pick and choose and make a "mash-up", but there is nothing reusable in a mash-up, and a million mash-ups do not make a viable platform for building the really cool apps of the next decade on. Topic maps on the other hand has a model for reflecting a consistent notion of identity, for reconciling different identity notions and different entity schemas.

There's the challenge - can we integrate all of this data using topic maps ? Can we make use of the tools provided by the Amazon platform to build something even more cool - a cloud based index of the entities and relations in these data sets ? Because I believe that when we can do that we will really have 1TB (or given the expansion of the topic maps model probably 1PB ;-) of useful knowledge, rather than 1TB of bits and bytes that you can hack with a mash-up.

There's the glove. Who's going to pick it up ?
