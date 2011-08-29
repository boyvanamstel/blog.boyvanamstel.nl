---
layout: post
title: "Omniauth strategy for Google OpenID+OAuth Hybrid Protocol login"
date: 2011-07-12 23:40
comments: true
categories: [rails, oauth, google]
---

Quite the title and quite cool to use. The Hybrid Protocol combines OpenID and OAuth in such a way that with one flow you can ask for authentication (and get someones account information, like name and email) and authorization (a token) for a set of services specified in a scope

Apart from providing a much cleaner user experience, it’ll save you a bunch of code. Especially via Omniauth.

I’ve created [~~a fork~~](https://github.com/boyvanamstel/omniauth/tree/google-hybrid) (read update) that contains [the google_hybrid strategy](https://github.com/boyvanamstel/omniauth/blob/google-hybrid/oa-openid/lib/omniauth/strategies/google_hybrid.rb) and [an example project](https://github.com/boyvanamstel/Google-Hybrid-Omniauth-implementation) that implements it.

UPDATE: My strategy just got merged into Omniauth’s master branch. So just use [Omniauth](https://github.com/intridea/omniauth) instead of my fork.

To see how it works, [try this demo](http://googlehybrid.boyvanamstel.nl/auth/google_hybrid).

