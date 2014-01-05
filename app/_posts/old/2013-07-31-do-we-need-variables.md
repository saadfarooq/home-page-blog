---
layout: post
title: "Do we need variables?"
description: ""
category: research
tags: ['research','ideas','opinions','unscientific']
---

In my mission to reduce redunancy in the various concepts we are taught along the course of our education, one of my goals is to take out things we don't need from programming. Or more precisely, categorize things in terms of what are necessities and what are facilities.

Which brings me to the topic of variables...

While looking for research on the the use of programming in CS education, I ran across a paper called ['Why calculating is better than scheming'](http://www.cs.kent.ac.uk/people/staff/dat/miranda/wadler87.pdf) by Philip Wadler. One of his other works is a programming langauge called [`Links`](http://groups.inf.ed.ac.uk/links/). The language is __'designed to make web programming easier'__. The aim is to replace the myriad of languages used during standard web development (I use JS, HTML, PHP and MySQL in one of my projects) with a single one. The idea is novel and something that NodeJS aimed at by allowing web developers to use Javascript on both server and client.

My own thougts when I read about this stack was; why do we need variables. How did I make the mental leap? Well, when you consider the most common usage of variables in programming, there are two main ones:

	- Pass values to functions
	- Store values in an common accessible location for later retrieval

Now, considering the concept of a `literacy of functional computation` (which I will elaborate in a separate post but basically it means that the unit of data is a function and values are a special case of function i.e. a function that always returns the same value); and combining it with the general pattern of web programming where a database is used for persistance of data, it may be possible to define a scheme where variables are not needed.

For the two use cases defined above: if you are passing values to a function, just pass a function and if you need to persist data for a longer period or share it across various resources, save it the database.

The success of this relies on the proof of the two claims; one, that all uses of variables fall into the two broad categories and two, that the concept of saving to a database if clearer in the minds of novice programmer than the concept of storing in memory.

More on this as the story evolves...



