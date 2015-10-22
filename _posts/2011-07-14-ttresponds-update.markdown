---
layout: post
title: "TTResponds update"
date: 2011-07-14 23:44
comments: true
categories: [google, cloud, javascript]
---

I’ve updated [TTResponds](http://blog.boyvanamstel.nl/2011/05/google-apps-script-ttresponds/) to include some requests people have made.

<!-- more -->

* You can now specify if you want to send HTML emails.
* You can set the sheet being used for the form (defaults to the first one).
* You can limit the amount of emails being sent. Just the first 10 entries for example (-1 is unlimited).

The script has been submitted to the Apps Script Gallery, but may take a while to appear. You can grab it right now from [Github](https://github.com/boyvanamstel/TTResponds).

Notice: if you’re already using a previous version of the script. Remove the config sheet. Open the scripts editor, copy-paste the new script over the old one. Run the createMenu method. And then select Create config from the TTResponds menu item. This will make sure the new configuration options appear on your configuration screen.

