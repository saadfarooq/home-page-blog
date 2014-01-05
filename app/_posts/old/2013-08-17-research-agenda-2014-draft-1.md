---
layout: post
title: "Research Agenda 2014 - Draft 1"
description: ""
category: research
tags: ['research', 'csed','computational thinking']
---

The realms of programming has traditionally been one dimensional i.e. all creation takes place in the realm of a computer program. The realm itself may be compound, for example: a program syntactically in text following a functional paradigm or visual programming using object-oriented programming.

However, computer science is somewhat unique compared to other areas such as engineering in that a single program is like an organism that has multiple layers and many of those layers are accessible.

In engineering design for example, the designer is working at a higher level. A bridge designer does not work with nor have access to the modules that comprise the bridge. The realm of the engineer is just engineering design. The materials he uses were part of a design but the realm of that design may have been completely different. The designer of the trusses may have used completely different tools; different methods of calculations. The bridge designer might not even be able to design the truss. Even if he does, the thinking paradigm changes and there is a noticable change where it does.

That is not so in computer science... well... specifically computer programming. The program designer will usually be the one writing all the way down in CS and in the one domain; whether that be functional or object oriented or whatever.

Much has been written on the feasiblity of different paradigms to programming for beginners giving an insight into how people think about programming natuarlly. It is clear that OO is not the way to go. Fucntional has it's advantages but it breaks down as soon as state comes into play.

## Overall Language Design:

A language that has multiple realms i.e. the software engineering is at a higher level using some sort of blocks etc. The blocks are encapsulated functions that perform some sort of computation on input data.

## Key features:

- Control flow is taken care of at the engineering level i.e. there are no ifs a the functional level.
- The function performs a specific computation and enforces constraints on inputs and outputs
- The function implementation is free of state
- The engineering implementation level defines contracts on the function blocks which are themselves a separate realm and provide a handy testing mechanism
- Mock values for computation functions are used to test functional flow as soon as engineering is complete

## Advantages:

- Segration between software engineering and computation.
- Some sort of insight into computational thinking
- TDD from the get go (more specifically TDL)

## Disadvantages:

- Doesn't cover the feasibility of the syntax etc. just the cognitive feasibility of using a higher level data flow language and a lower level functional language

## Research Questions:

- Does having a higher level 'engineering' language help students make sense of the code they are writing ?
- Are bugs reduced when using higher level engineering ?
- How does having a built in testing framework with a mock use case affect student's grasp of other cases ?

## Study:

- Develop and test a language that works with some existing programming language taught at high schools in the area. Maybe a layer over Snap, Scratch or Alice

## Inspirations
David S Jenzen		: http://users.csc.calpoly.edu/~djanzen/
Michael Kolling 	: http://www.cs.kent.ac.uk/people/staff/mik/
Michael Casperson	: http://cs.au.dk/~mec/
