---
layout: post
title: "Data Grids with AngularJS"
description: "Seletion and implementation data grids using AngularJS"
category: development
tags: ['development', 'interlace']
---

## Criteria
As always, lets start with we want in our data grids. 

* Frontend (JS) driven - with all the tweaking that is expected of tables / grids, working from JS is just simpler instead of doing some processing in one language and some in another. I've run into problems using multiple languages previously where SQL was not flexible enough to do good processing of data. I then had to do some processing in a server side language (PHP) and some in the frontend using Javascript. This approach is way easier, just get the raw unformatted data from SQL and do everything in Javascript.
* Flexible - there is a tradeoff here. On the one hand, it would be good to have control over individual columns. On the other, it might be convenient to just give a widget data and have it show up. 
* Easy to manipulate - similar to flexible above, some of the problems with the Yii plugin we previously used is it was too rigid. You could only used the options that they already have built-in and it's not very declarative. 

## Options
- Using native Angular directives
- Using a pre-built Data-grid

### Native Angular
Angular directives give a great way to roll your own table using whatever data-types you prefer. The implementation of the table in the current layout is just the following:

{% highlight html %}
<table>
    <thead>
        <tr>
            <th ng-repeat="header in headers"> {% raw %} {{ header }} {% endraw %}</th>
        </tr>
    </thead>
    <tbody>
        <tr ng-repeat="value in values | filter:filterBy">
            <td> {% raw %} {{ value.Title }}       {% endraw %} </td>
            <td> {% raw %} {{ value.Description }} {% endraw %} </td>
            <td> {% raw %} {{ value.Date }}        {% endraw %} </td>
            <td> {% raw %} {{ value.Password }}    {% endraw %} </td>
        </tr>
    </tbody>
</table>
{% endhighlight %}

But where does the data come from. Well, in the controller you just use Angular's `$http` service to make a web call and set the returned value to a variable on the scope. The data-binding guarantees that the data shows up on the same variable in the HTML. 

{% highlight js %}

$http({method: 'GET', url: 'http://someserver'}).
    success(function(data, status, headers, config) {
        $scope.headers = Object.keys(data[0]); // get the headers from one row
        $scope.values  = data;
    });

{% endhighlight %}

And voila, the data fills up the table. Also, notice the filter "piped" after the `ng-repeat` directive. By simply adding: 

{% highlight html %}
<input ng-model="filterBy"></input>
{% endhighlight %}

to the page, the table is filtered by the values containing the string from input. No other code necessary. Isn't that cool...

Of course, we can also write other filters. In our application, filtering is a great tool because of the large lists we have. That coupled with the fact that I've never liked the look of data-grid (they seem too... serious) so this option is definitely my favorite. 

### Using a Pre-Built Data-grid
In this case, there are plenty of options to choose from. I couldn't get the ones I tried to work out of the box and it turned out it might have to do with setting some data before the HTTP call is made and then updating the data instead of setting it just on the success callback (now called promise).

Eventually, the one I'm using is called [ng-grid](http://angular-ui.github.io/ng-grid/). The only problem you need to be aware of with this (apart from the setting data as above) is that initially it might only show a couple rows of data. Turns out it's a bug in Javascript. There is a workaround suggested [here](https://github.com/angular-ui/ng-grid/issues/80) to make sure it uses `auto` height until the bug is fixed but it didn't work for me so I had to set the height manually. 

Others that might be of interest are : [Smart Table](http://lorenzofox3.github.io/smart-table-website/) and [Angular Table](http://angulartable.com/). 
Angular Table claims to be completely declarative which is cool. Unfortunately, I couldn't get it to work right in the limited time I had. Might have to give it another try soon.

## Conclusion
I'd love to just go with the native Angular table but I realize that might be too geeky overall. Will have to see what the group decides. Might just end up doing it with Yii in the end.
