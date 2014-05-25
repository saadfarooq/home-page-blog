---
layout: post
title: Using Google Spreadsheets as a Database with OAUTH
publish: false
---

Say you are working on a simple data acquisition project. You gather some data using a mobile device and you want to be able to manage the collected data quickly and easily. You end up implementing a web hosted SQL database that you send you data to. Then later, you go through all the hassles of exporting and importing that data into a format that you are more comfortable working with and sharing with others. Probably a spreadsheet.

One fine day, you realize, wouldn't it be nice if I could just send that data directly to a spreadsheet instead of going through those additional steps. You think of Google Spreadsheets and you are pretty confident that you enough about HTTP to be able to get the data through. It seems a great solution so you start looking at communicating with Google Spreadsheets from your app.

But then, you run into all the authentication problems and the complexity associated with the GDATA (Google Data) API's and you think about pulling your (remaining) hair out.

Wouldn't it be great if there was a quick and easy way to just send your data to be added to a Google Spreadsheet without having to worry about all this authentication stuff. Well, lucky you. Cause today we're going to walk through how to do that.

STEP 1: Set up your recipient spreadsheet

Go to Google Docs (or Drive now) and create a new Spreadsheet and give it a name.

Then give the columns you need to use appropriate headers. I'm going to assume I'm cataloging data on flowers so I'll give it three columns; Name, Family, Color.

Go to Tools -> Create a Form.

![create form](/img/post_spreadsheet_form.png "Create a form")

Un-check the "Require sign-in to view this form." checkbox (this allows you to post to the form without authenticating).

![remove authentication](/img/post_spreadsheet_authenticate.png "Remove authentication option") 

Save and close the form windows. You should notice a "Timestamp" column. Now go to Form -> Go to Live Form. You should see something like this.

![live form](/img/post_spreadsheet_live_form.png "Check the live form")

You can enter data into this form and it will populate the spreadsheet. We're going to have a look under the hood now to see how this is done and how we can do it using other methods.

Step 2: Get the HTTP POST parameters

Right click on the page and choose 'View page source'. You'll notice that the webpage uses  an HTML form to submit the data. The following defines the form action.

    <form action="https://docs.google.com/a/dfarooq.com/spreadsheet/formResponse?formkey=dHYwFVNKTsd2VzAteEpieTB3NjgTenc6MQ&amp;ifq" method="POST" id="ss-form">

The 'action' attribute define the Google Spreadsheet form URL where the data will be posted to by the form. Input elements in the HTML defines the form inputs.The first input box for 'Name' is given as :

    <input type="text" name="entry.0.single" value="" class="ss-q-short" id="entry_0">

The next box defines the 'Family' parameter.

    <input type="text" name="entry.1.single" value="" class="ss-q-short" id="entry_1">

Finally, the 'Color' input box corresponds to.

    <input type="text" name="entry.2.single" value="" class="ss-q-short" id="entry_2">

There are also two other inputs that you'll need

    <input type="hidden" name="pageNumber" value="0">
    <input type="hidden" name="backupCache" value="">

and form submit input 

    <input type="submit" name="submit" value="Submit">

Based on the above, something like the following sent to the form action URL should result in a row addition to the spreadsheet.

    entry.0.single=Sunflower&entry.1.single=Asteraceae&entry.2.single=Yellow&pageNumber=0&backupCache=""

Notice that we also send the hidden inputs but that they take the same values as described in the form. The content type for the POST call is the standard form input 'application/x-www-form-urlencoded'.

Once you've performed the POST, you should get something like this.

![resulting spreadsheet](/img/post_spreadsheet_final.png "Spreadsheet with entry") 

Step 3: Using a client to POST

Whatever platform you use there should be a number of examples out there on how to perform POST calls. All you'll ready need to do is replace the values for your form.

Happy Coding !!!


