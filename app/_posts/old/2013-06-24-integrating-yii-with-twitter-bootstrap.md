---
layout: post
title: "Integrating Yii with Twitter Bootstrap"
description: ""
category: development
tags: ['development','yii','interlace']
---

# Why Twitter Boostrap?
I would like to include [Twitter Bootstrap](http://twitter.github.com/bootstrap). The primary reason for doing so if to get the [grid](http://twitter.github.io/bootstrap/scaffolding.html#gridSystem) capability which is just way more convenient that setting weird CSS on elements. 

## Options
There seem to be two ways to do this.
One is using Yii's [Twitter Bootstrap extension](http://www.cniska.net/yii-bootstrap/). Using this extension you would add Twitter components to your page using snippets like this: 

{% highlight php %}
<?php $this->widget('bootstrap.widgets.TbButton', array(
    'label'=>'Primary',
    'type'=>'primary', // null, 'primary', 'info', 'success', 'warning', 'danger' or 'inverse'
    'size'=>'large', // null, 'large', 'small' or 'mini'
)); ?>
{% endhighlight %}

As opposed to : 

{% highlight html %}
<button class="btn btn-primary">Button</button>
{% endhighlight %}

So that settles it. I'm going to go for the latter. 

## How To Use It
Yii supports layout inheritance. You can define layouts at the Application, Controller or View level. Since, I'm going to be using the same layout throughout the views I'll be setting it up at the Controller level.

I create a new file called `twitter-bootstrap.php` in the `views/layouts` folder.

{% highlight php %}

class DashboardController extends Controller
{
    public $layout='//layouts/twitter-bootstrap';
}
{% endhighlight %}

Simple. All views of this controller will now use the layout defined in `twitter-bootstrap.php`

## Now the Hard Part
How to define the layout itself ? Should be simple enough:

{% highlight html %}
<!DOCTYPE html>
<html>
<head>
    <?php echo CHtml::cssFile(Yii::app()->baseUrl.'/css/bootstrap.css'); ?>
</head>
<body>
<div class="container-fluid">
    <div class="row-fluid">
        <div id="header">
            ...site logo and other header content...
        </div>
    </div>

    <?php echo $content; ?>

    <div class="row-fluid" id="footer">
        ...footer content...
    </div><!-- footer -->

</div><!-- container -->

</body>
</html>
{% endhighlight %}


