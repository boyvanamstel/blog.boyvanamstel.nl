---
layout: post
title: "Omniauth + Facebook = OpenSSL::SSL::SSLError"
date: 2011-05-05 23:19
comments: true
categories: [programming, fixes] 
---

~~I’ve run into this issue twice and now I’m writing down the solution. When authenticating with Facebook via Omniauth, my server always fails with the following error:~~

    OpenSSL::SSL::SSLError (SSL_connect returned=1 errno=0 state=SSLv3 read server certificate B: certificate verify failed):

~~This is easily fixed by adding the following to one of the initializers:~~

    OpenSSL::SSL::VERIFY_PEER = OpenSSL::SSL::VERIFY_NONE

~~It’s probably not the best solution, as this turns off SSL peer verification..~~

A better solution:

[http://stackoverflow.com/questions/5711190/how-to-get-rid-of-opensslsslsslerror](http://stackoverflow.com/questions/5711190/how-to-get-rid-of-opensslsslsslerror)
