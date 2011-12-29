---
layout: post
title: "Fiddling with NeXTSTEP"
date: 2011-12-29 22:36
comments: true
categories: [experiment, operating system]
---

I bought my first Mac just 3 or 4 years ago. Before that I used to alternate between Windows and Linux, mostly sticking to Linux. The flexibility and complexity was something I liked most about Linux. Compiling a new kernel each time I inserted a new piece of hardware into my computer and fixing errors until a game or application would compile and install successfully used to keep me entertained for days and nights on end. The absence of these exact things is what made me buy an Apple later; it just works.

This week I realised that while I'm quite familiar with the history of DOS, Windows, Linux, Amiga, C64, BeOS and so on, Mac OSX's predecessors are a mystery to me. A few brief experiences with NeXT workstations and iMacs in public places aside, I've never used the system before OSX. Obviously exploring this makes for a perfect spare time project. I managed to install [NeXTSTEP](http://en.wikipedia.org/wiki/NeXTSTEP) in [Parallels](http://en.wikipedia.org/wiki/Parallels,_Inc.) and tried to get past greyscale graphics, which proved to be difficult. After reading some experiences by others I swithed to [VirtualBox](https://www.virtualbox.org/), which allows you to customize hardware properties, like ethernet cards and sound devices. VirtualBox with [OPENSTEP](http://en.wikipedia.org/wiki/Openstep) (NeXTSTEP with OpenStep) and the latest update almost provides a plug and play experience due to much improved driver support. I took some screenshots running OPENSTEP 4.2 at 1024x768 pixels with 32bit colors (a setup that cost about $ 15,000 when it was released).

{% img /images/media/nextstep/openstep-dangercove.png %}
A screenshot of [DangerCove.com](http://dangercove.com). [OmniWeb](http://www.omnigroup.com/products/omniweb/) (like all browsers at the time) lacked support for stylesheets, or almost any of the features we're used to today. Enabling javascript caused every site I tried to crash.

{% img /images/media/nextstep/openstep-facebook-doom.png %}
This screenshot shows Facebook, looking rather broken, and DOOM in the front. id Software used NeXT systems to create the famous first person shooter. Relying on the Objective-C based development environment to create most of the tools, like the level editor. Speaking of which..

{% img /images/media/nextstep/openstep-xcode-interfacebuilder.png %}
While Xcode 4.2 and InterfaceBuilder 4.2 were released almost two decades apart, they feel strikingly similar; dragging and dropping components and attaching their outlets to 'First Responders', it's all there.

YouTube has some pretty cool videos that show Steve Jobs demoing NeXTSTEP. Like this one, where Steve talks about what he calls 'interpersonal computing':
<iframe width="420" height="315" src="http://www.youtube.com/embed/-1wYy5qvA24" frameborder="0" allowfullscreen></iframe>

Or this 'secret' video, supposedly only for the eyes of fresh NeXT employees:
<iframe width="420" height="315" src="http://www.youtube.com/embed/p9dmcRbuTMY" frameborder="0" allowfullscreen></iframe>

Fiddling around with NeXTSTEP has been fun. It reminded me that I tried, but never really liked, the Linux window manager called [WindowMaker](http://en.wikipedia.org/wiki/Window_Maker), which I did knew was based on NeXTSTEP. WindowMaker to me felt out of place on Linux and inferior to Gnome, KDE, Enlightenment and other window mangers at the time. Like OSX today, the NeXTSTEP interface feels a lot more comfortable on the system that it's been designed for.

Some sites to help install OPENSTEP yourself:

  * [Screenshot-supported walkthough on nextcomputer.org's forums](http://www.nextcomputers.org/forums/viewtopic.php?t=1663)
  * [Guide for VMWare and VirtualBox by Laurent Julliard](http://www.moldus.org/~laurent/GNUstep/OS42_Install.html)
  * [Massive list of downloadable NeXTSTEP games and demos at nextcomputer.org](http://www.nextcomputers.org/NeXTfiles/Software/NEXTSTEP/Apps/Games/)
