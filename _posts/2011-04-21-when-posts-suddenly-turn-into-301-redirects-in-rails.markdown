---
layout: post
title: "When POSTs suddenly turn into 301 redirects in Rails"
date: 2011-04-21 22:34
comments: true
categories: [programming, fixes]
---

Everything worked fine in my development environment, but when I ran the application from my server every POST would just show the page it was suppost to POST to via GET. Displaying a 301 redirect in Chrome’s developers tools.

After some fiddling around, I commented line 351 in the .htaccess file:

    <IfModule mod_rewrite.c>
      RewriteCond %{REQUEST_FILENAME} !-f
      RewriteCond %{REQUEST_URI} !(\.[a-zA-Z0-9]{1,5}|/|#(.*))$
      #RewriteRule ^(.*)$ /$1/ [R=301,L] # <-- this one
    </IfModule>

After that everything worked as expected. Weird..

