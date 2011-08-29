---
layout: post
title: "Google Apps Script: TTResponds"
date: 2011-05-13 23:25
comments: true
categories: [cloud, programming, google, javascript]
---

##Introduction

TTResponds is a Google Apps Script that allows you to automatically send a confirmation to people who’ve filled out a Google Form.

It’s been available for a while in the Script Gallery, but I haven’t gotten around to write about it. The reason I’m doing so right now, is because I’ve received a couple of returning questions that I can probably better answer right here.

## Installing

First login to your Google Docs environment, [docs.google.com](http://docs.google.com) and Google Apps both work fine. After that, choose to create a new Form.

{% img /images/media/ttresponds/newform.png %}

This will present you with a pop-up that allows you to customize the fields. For basis functionality it should at least contain a name field first and an email address second. After that you can add anything you want.

{% img /images/media/ttresponds/setupform.png %}

Clicking save will send you to the Spreadsheet, setup to receive form submissions. The next step is to add TTResponds. You can do so by clicking ‘Tools’ and then ‘Script gallery…’.

{% img /images/media/ttresponds/scriptgallery.png %}

Search for ‘TTResponds’ and click install.

{% img /images/media/ttresponds/findttresponds.png %}

Authorize the script to read your Spreadsheet and send out emails.

{% img /images/media/ttresponds/accept.png %}

A new menu item called ‘TTResponds’ just appeared. Click it and select ‘Create config’. This should add an extra sheet called ‘TTRespondsConfig’, you can change the properties to provide a more relevant response. After you’re done, make sure all ‘Triggers’ are setup correctly by clicking ‘Tools’ and after that ‘Script editor…’.

{% img /images/media/ttresponds/scripteditor.png %}

In the pop-up select ‘Triggers’ and then ‘All your triggers…’.

{% img /images/media/ttresponds/triggers.png %}

Make sure your setup looks like the image above. If it doesn’t, click ‘Add a new trigger’ and set it to ‘onFormSubmit’, ‘From spreadsheet’ and ‘On form submit’. That’s it! Fill out your own form and you’ll receive a confirmation automatically!

## HTML Email

Per default the script sends text-only emails. You can change this to HTML email pretty easily (I’ll probably add it as an option in an update). First open the script editor again and navigate to line 119.

{% img /images/media/ttresponds/htmlemail.png %}

You’ll see that is says:

    { name: _config.from }

Change it to this:

    { name: _config.from, htmlBody: _config.body }

The script will now send the confirmation as HTML, allowing you to send a fancier response  .

## Collaborating

I’ve created [a GitHub repo for TTResponds](https://github.com/boyvanamstel/TTResponds). If you’re adding features, or fixing bugs, please fork the project and send me a pull request.

## Let me know

It would be awesome if you let me know if you use and/or like the script through the comments, thanks!
