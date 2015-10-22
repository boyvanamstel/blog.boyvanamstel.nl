---
layout: post
title: "WordPress Project Creator"
date: 2011-01-13 22:15
comments: true
categories: [programming, wordpress, streamlining, python]
---

Working on WordPress projects can be a hassle. Especially if there’s more than one developer. There are a lot of files and chances are huge that you’ll be working on the same files quite often. This slows down development tremendously, not to mention the annoyance it causes.

<!-- more -->

You can fix the ‘working on the same file’ and ‘working on the live server’ issues quite adequately by using version control. I prefer Git, because of it’s distributed character. WordPress has another issue however, when trying to run the same site on different machines. Among the data it stores are urls, absolute urls.. This means that if you’d load a database dump from a live WordPress site into your local install, nothing will work correctly.

[WordPress Project Creator](https://github.com/boyvanamstel/Wordpress-Project-Creator) [github] is a tool I created to streamline working on WordPress projects with multiple people. It does a couple of things:

* Download WordPress
* Create a new Git repo out of your wp-content folder
or clone an existing wp-content folder into the WordPress folder
* Easily import database dumps by alterering absolute urls
* Create wp-config.php file
* Create .htaccess file

Adding new developers to your project is as easy as allowing them access to the Git repo and running wpprojectcreator. If  you clone an existing project, the only things you’ll have to do is run the python script, import the dump using setup.php and you’re ready to work on the website as if it were live.

![Wordpress Project Creator](/images/media/wpprojectcreator/wpprojectcreator.png)

I released it on GitHub so everyone can give it a go. Or everyone.. at least everyone running OSX, Linux or 32bit Windows. Git on 64bit Windows can’t be installed in such a way that it’s accessible from the command line, which is required by wpprojectcreator. Be sure to read the README  .

Check out [WordPress Project Creator on GitHub](https://github.com/boyvanamstel/Wordpress-Project-Creator).
