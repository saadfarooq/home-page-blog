---
layout: post
title: "In Search of a Front End Development Framework"
description: ""
category: development
tags: ['interlace','development']
video_url: http://www.youtube.com/embed/iUQ1fvdO9GY
---

# Front-end Development Framework
As bad as it is, Javascript is here to stay and server side development still doesn't help get rid of it (and introduces plenty of problems of it's own). So if we're in this mess, might as well try to make it a little less gross.
Many have tried (and continue to try) to make web app development less painful. We're giving one of our projects a makeover so I though I might as well try to find a new framework that works better than our current setup (PHP Yii, arghh).

## Criteria
The main criteria that I want in the new framework:

* Decoupling Server and Client - the framework should be frontend driven i.e. the front end is a Javascript based client app and the backend is comprised of RESTFul web services. The separation gives us some separation of concerns and makes extending the platform to use mobile based clients easier.
* Support for testing - I suck at testing. I write stuff and assume it's true for the completely plausible reason that I wrote it. I was introduced to the `Test Driven Development` philosophy recently and I totally buy into it. So I would like to have support for testing in the framework.
* Support for modularization - I don't think I can get this is Javascript. In fact, this should be on the list. It should be a given but since we are working with Javascript, this will probably only remain on the list and never see fruition.

Apart from that, I wouldn't mind these features:

* Package Management 
* Dependency Management
* Scaffolding
* Bootstrapping that's close to what I'm looking for

## Introducing Yeoman
I went over a lot of stuff over the past few days and [Yeoman](http://www.yeoman.io) seems to be the way to go. The `1.0` version of Yeoman aims at bringing existing tools together instead of trying to do everything itself.
It seems to try to mimic a `Rails` type system. `Grunt` is the build tool and `Bower` is the package/dependency manager. 

Yoeman includes a tool called `Yo`. It also has a variety of generators that can be used to scaffold apps. They seem to work pretty great out of the box.

## Current Status
The generators I'm currently exploring are `generator-webapp` and `generator-angular`.
The testing framework for the `webapp` generator is [Mocha](http://visionmedia.github.io/mocha/) and it uses [ChaiJS](http://chaijs.com/) and [ExpectJS](https://github.com/LearnBoost/expect.js/) for assertion (I don't know why, it's kinda weird).
The [AngularJS](http://angularjs.org/) generator uses [Karma](http://karma-runner.github.io/0.8/index.html) as their testing framework.

## What now ?
I haven't tested the two options enough yet, but I feel like Angular has more momentum and it's easier to get starting using TDD with Angular just because they have more documentation available. I tried Mocha + Chai + Expect but kept getting lost with who's doing what so it's higly probably that I'm gonna go with Angular via Yeoman. 

## Extras
Below is a video on getting starting the Yeoman by Addy Osmani from Google.
