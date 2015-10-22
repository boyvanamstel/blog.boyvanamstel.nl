---
layout: post
title: "Maintenance page while deploying with Capistrano"
date: 2011-06-18 23:35
comments: true
categories: [rails, capistrano, deployment]
---

I got tired pretty fast of staring at Passenger’s 500 errors while Capistrano and Rails are busy setting up a new release of a project.

Of course other people got tired as well and came up with numerous fixes. The one I like best is where you first put up a maintenance page, deploy and after all went well, remove the maintenance page. Kind of like how Apple disables the store when they’re adding new stuff, but less flashy I suppose..

It’s pretty easy to do this and I’m just going to provide two links that explain it very well. One for [Apache](http://stackoverflow.com/questions/2244263/capistrano-to-deploy-rails-application-how-to-handle-long-migrations) and one for [Nginx](https://boxpanel.bluebox.net/public/the_vault/index.php/Custom_Rails_Maintenance_Pages_With_Capistrano). They’re both very similar and you can easily pick either of the deploy.rb parts.

That’s about it. It’s very easy to do and probably something a lot of people know already, but definitely something that’ll make you feel more comfortable while deploying.

