---
layout: post
title: "Html5-boilerplate gem and no more posting/deleting etc."
date: 2011-07-19 23:46
comments: true
categories: [rails]
---

For no apparent reason all the post/delete/put requests I was doing in my brand new Rails project where failing… Forms would not create anything. The problem only appeared occurred on my live server running Phussion Passenger. No issues on WEBrick.

After a little searching I found the issue in the .htaccess files. Created by the html5-boilerplate gem in /public/.htaccess.

Comment the following lines on line 348 and the problem goes away:

    <IfModule mod_rewrite.c>
      RewriteCond %{REQUEST_FILENAME} !-f
      RewriteCond %{REQUEST_URI} !(\.[a-zA-Z0-9]{1,5}|/|#(.*))$
      RewriteRule ^(.*)$ /$1/ [R=301,L]
    </IfModule>

I’m guessing the other rewrite rules are problematic as well. A better fix would be to only rewrite when using GET.

