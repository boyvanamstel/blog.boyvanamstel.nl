---
layout: post
title: "Hip Like Heroku"
date: 2011-04-30 23:13
comments: true
categories: [cloud, programming, rails]
---

Usually I deploy projects on my physical server, located at the server park called “former bedroom at my parents’”. This allows me to see how a project develops and migrate to a better server (which costs more money) if it’s successful. This is also the case for [hiplikejapie.nl](http://hiplikejapie.nl/).

<!-- more -->

I’ve been deploying a couple of experiments to Heroku and the platform really appeals to me. Deploying itself is a breeze and the “add-ons” model is pretty cool. Also, it’s free if you can manage with a 5mb database, 1 dyno en 0 workers. Projects in a developing stage usually do. I’ve never launched a project from it though. Primarily because I don’t want the to run into insane hosting costs if something like [Please Rob Me](http://pleaserobme.com/) happens. In any case the ability to scale a project and not worrying about server setup and stuff is awesome.

Hip Like Japie hasn’t really took off (yet?), but is doing mildly ok with a bunch of visitors every day. It being a finished product made it interesting for me to see how well it would deploy.

I’ve got Heroku’s command line tool installed, but if you haven’t install it like this:

    $ sudo gem install heroku

Next you need to setup a Git repository for your project if you haven’t already.

    $ git init
    $ git add .
    $ git commit -m 'initial import'

Let Heroku add it’s remote.

    $ heroku create

Login with your Heroku credentials and you’re done setting up!

This would usually be the point where you start developing your application, but Hip Like Japie being already done allows me to skip directly to deploying.

    $ git push heroku master

Did you see what they did there? They just added a new remote, super nice. Anyway, this should start deploying the app. After it’s done, migrate the database.

    $ heroku rake db:migrate

I thought about looking online for correct settings to Heroku’s database setup, but decided to just run rake and see what happens. Turns out that Heroku just made it work. My production setup was set to use Sqlite3, but Heroku automatically changed it to their PostgreSQL database.

Technically I was done, but opening the website would give me an error. Crap, something went wrong. You can check the server’s log by issuing the following command:

    $ heroku logs

This showed me that a database query failed, due to running on PostgreSQL instead of Sqlite3. I applied a dirty little patch.

    if ActiveRecord::Base.connection.instance_values["config"][:adapter] == 'postgresql'
      @comparisons = Comparison.find_by_sql(
          "SELECT * FROM (SELECT DISTINCT ON (username) * FROM comparisons ORDER BY username, id DESC) foo ORDER BY id DESC LIMIT 10"
          )
    else
      @comparisons = Comparison.all(
          :order => "id DESC", :limit => 10, :group => 'username'
          )
    end

After that the site worked fine: [hiplikejapie.heroku.com](http://hiplikejapie.heroku.com). There’s an add-on that allows you to hook up your custom domain name to the project. It’s conveniently called “Custom Domains” and can be used via the command line.

    $ heroku addons:add custom_domains

This may prompt you to verify your account, by entering your creditcard details (on Heroku’s website, not the command line). After that you’re ready to add your domain names.

    $ heroku domains:add www.hiplikejapie.nl
    $ heroku domains:add hiplikejapie.nl

I added both the domain and the www. sub-domain. To activate this, you need to change your domain’s DNS settings. It comes down to adding three A records and a CNAME.

    @ A 75.101.163.44
    @ A 75.101.145.87
    @ A 174.129.212.2
    www CNAME proxy.heroku.com.

That’s it, [hiplikejapie.nl](http://hiplikejapie.nl) points directly to Heroku, awesome!

EDIT:

The website failed if the worker would spin down. The error logs showed that Compass couldn’t compile the Sass files. Which is obvious as Heroku is read-only. This line in config/environments/production.rb fixes it:

    Compass.configuration.sass_options={:never_update=>true}
