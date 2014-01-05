---
layout: post
title: "Image/Thumbnail Gallery with AngularJS"
description: ""
category: development
tags: ['twitter-bootstrap', 'interlace', 'development', 'angularjs']
---

I need to add a thumbnail gallery for the reports we provide on our online platform. Twitter Bootstrap has a great framework for setting this up quite easily using available CSS classes. 

For now, I'm just going to use the default setup and use CSS3 animations to fade in and out the images based on what's being hovered over.

This is what it looks like right now:

{% highlight css %}
<div class="row-fluid" ng-controller="ThumbnailsCtrl">
        <ul class="thumbnails">
            <li class="span4" ng-repeat="report in reports">
                <div class="thumbnail">
                    <img data-src="holder.js/300x200" alt="300x200" style="width: 300px; height: 200px;">
                    <div class="caption">
                        <h3>{% highlight raw %}{{ report.title }}{% endhighlight %}</h3>
                        <p>{% highlight raw %}{{ report.details }}{% endhighlight %}</p>
                        <p><a href="#" class="btn btn-primary">Go To Report</a>
                    </div>
                </div>
            </li>
        </ul>
    </div>
{% endhighlight %}
