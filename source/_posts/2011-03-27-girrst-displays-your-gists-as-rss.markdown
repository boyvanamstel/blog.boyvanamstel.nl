---
layout: post
title: "Girrst displays your Gists as RSS"
date: 2011-03-27 22:31
comments: true
categories: [programming, web apps, inspiration, cloud]
---

Do you use GitHub’s Gists? Then you might like this.

Sharing code among co-workers and friends is quite easy using various ‘code snippit’ sharing websites. I personally like GitHub’s Gists. To make sharing even easier and keep everybody up to date of what’s being shared, I wanted to create a feed out of my Gists. Of course I could just use GitHub’s own RSS feeds, but that would screw up my reason to do something with App Engine.

<!-- more -->

{% img /images/media/girrst/appengine.png %}

Using Python and App Engine I threw together a script that will take your GitHub username and turn all your Gists into a convenient RSS feed. You can then use the feed to include it anywhere, like your favorite RSS reader or your blog.

To make things even easier, use the [GitHub bundle for TextMate](https://github.com/drnic/github-tmbundle) to be able to create Gists from your favorite editor. Don’t forget to [setup your GitHub username and token](http://help.github.com/git-email-settings/):

    $ git config --global github.user username
    $ git config --global github.token 0123456789yourf0123456789token

Try it: [girrst.appspot.com](http://girrst.appspot.com)
