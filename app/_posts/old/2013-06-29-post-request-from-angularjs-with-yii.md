---
layout: post
title: "POST request from AngularJS with Yii"
description: ""
category: development
tags: ['development','interlace', 'angular', 'yii']
---

I don't like Yii much. Maybe it's cause of the overbloatedness of PHP. 

AngularJS, which is what I'm using in the front-end, allows you to send Javascript objects using POST requests via JSON. When you do that, you expect there to be a `$_POST` object in Yii from which you can conveniently partake of your desired data. 

After spending some time trying to figure out why that is so, I came upon [this](http://learnyii.blogspot.com/2011/11/yii-json-post-model-save.html) post. It's annoying but basically you have to just do a low-level PHP read using.

{% highlight php %}
$post = file_get_contents("php://input");
{% endhighlight %}

Oh Yii !! How I hate thee...
