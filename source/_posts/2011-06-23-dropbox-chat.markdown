---
layout: post
title: "Dropbox Chat"
date: 2011-06-23 23:37
comments: true
categories: [dropbox, ruby]
---

Have you ever wondered how well Dropbox would work as a chat application? I did and I finally created a client for it. The concept of having Dropbox handle all the complicated server side stuff is very appealing and actually works quite wel.

The use case I can imagine happening is that you want to share and store quick conversations you have with co-workers/friends while working on a project. Instead of navigating to Basecamp, emailing (which is less direct) or copy-pasting chat logs, you can just open the Dropbox chat client and have a short conversation. The chat log is right there in the same folder and the only thing you have to do to get it to work, is drop the application in the Dropbox project folder you’re working on.

The experiment is really easy to setup. Just clone/download [the repository on GitHub](https://github.com/boyvanamstel/Dropbox-Chat). Put the folder in your Dropbox folder and share the folder with your friends.

To run the application open a terminal window and navigate to the folder you just shared. Like this for instance (don’t type the $ sign):

    $ cd ~/Dropbox/Projects/DropboxChat

Now run the application.

    $ ruby chat.rb

If it throws an error, this means it might need to install some additional libraries called gems.

    $ gem install [gem name]

After it starts it’ll prompt you for a nickname, pick something original and that’s it. Just start typing  .

{% img /images/media/dropboxchat/dropboxchat1.png %}

{% img /images/media/dropboxchat/dropboxchat2.png %}
