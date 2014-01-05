---
layout: post
title: "Integrating Yeoman based Project with Yii"
description: "Needs improvement"
category: development
tags: ['development', 'interlace']
---

## Options
The Yeoman based Angular project builds to HTML and Javascript. 

There are two main options for integrating with Yii.

- Static HTML served directly from a directory
- HTML injected into a Yii PHP view

## Static HTML
The Yeoman project is enclosed in a self enclosed directory named `app` during development and builds to a `dist` directory. All required HTML and CSS files are within the same directory. 
The Angular framework has a level of abstraction implemented via directives called `ng-app`. Each `ng-app` contains multiple controllers (via `ng-controller`) which are data bound with associated `Controller` functions in Javascript.
Routing can be implemented at the `ng-app` level with URL routes of the `#/<route>` pattern being assigned to various subviews by the Angular framework.
This provides a nice modulization of Javascript actions and DOM manipulation (something which is particularly annoying otherwise) and also allows for bookmarkable URLs. E.g. the view

    http://localhost/#/firstview
    http://localhost/#/secondview

can be implemented using different HTML files via the Angular routing mechanism. And be assigned to different `ng-controllers`.

### Implementation
The implementation in conjunction with Yii turns out to be simple. Copying the `app` (or `dist`) folder to the root of the Yii server creates the URL which simply loads the static HTML app. No problems at all. The Yii framework in the default configuration only routes the URL portion beyond the `/index.php/` to a Yii controller. Following are the two URL patterns.
    
    http://<serverroot>/<angular-app-directory>/
    http://<serverroot>/index.php/<controller>/<action>/

An Angular static HTML in conjuction with Yii simply works using the former URL scheme. 

## As a Yii View
Yii views are rendered as PHP files. The parser parses any PHP directives in the view files, but only if there are any (smirks). By copying the contents of the Angular app's HTML file to a PHP view file, it is simply rendered as HTML. The only problem now is making sure that the script loading tags work as expected.
This turns out to be not so simple using just strings. The paths have to be hard-coded because Yii does not allow access to relative paths in sub-directories.
Futhermore, the HTML files that make up the modularized views routed by the Angular app via URL routes must also be served as static files. 

### Implementation
Currently, the static files are served via hard-coded paths. Once a decision is reached on what pattern of development to follow, the scripts and stylesheets are best served via the Yii assets system. This system takes scripts / stylesheet URLs from a standard directory and serves them via relative paths built during the compile process.

### Layout Inheritance
As of this writing, the Angular app served the Yii view inherits some layout from the default Yii layout whereas some is derived from the HTML app. This results in some disarray in the overall layout. The feed column which is designed to take up about a quarter of the real estate is limited to just enough to hold the placeholder text. 
Updating the script loading as above and abstracing the common elements to a Yii layout should fix this problem pleasantly based on the decision on what method to use.

### Trailing Issues
The only remaining matter is the serving of the static HTML sub-view files. I'll need to investigate some more on this. Perhaps Yii offers a way to serve these similar to how scripts are served. 
In the case where that is not possible, some security review might be undertaken of the situation. It is all just HTML and JS and not data is actually used until the app is running and the server authorizes the data, but you never know.
