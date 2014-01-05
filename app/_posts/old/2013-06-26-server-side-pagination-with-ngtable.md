---
layout: post
title: "Server Side Pagination with ngTable"
description: ""
category: development
tags: ['development','interlace','angular']
---

## What is Server Side Pagination?
Sometimes you just have too much data to fit comfortably on a single page of a table or data-grid. There are two ways to deal with this. Client side pagination is when you get all the data from the server and use Javascript to show only some of it on the one page. Upon navigation to a different page, a new set of data is loaded.
In server side pagination, only the amount of data to be shown on one page is loaded from the server. Upon navigation to a different page a new call is made to the server to get data for that page.

## Server Side Pagination with ngTable
I chose ngTable as my standard table view. The reasons for this choice are detailed [elsewhere](2013-06-23-data-grids-with-angularjs.html)

## Getting Totals
As explained [here](http://www.arraystudio.com/as-workshop/mysql-get-total-number-of-rows-when-using-limit.html) getting the total values that "would" be returned is absolutely essential if you are going to have pagination.
