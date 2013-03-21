---
layout: page
title: "Games"
comments: true
sharing: true
footer: true
---

Video games have been a pretty constant hobby for me, but it seems to have changed in some form of hoarding; buying more than I want or can play. Instead of just buying a single game and finish it, now I play several, usually depending on the situation/location I'm in. These are the games I'm currently playing or look forward to playing.

<h2>Big screen game</h2>
The game I play on my computer or consoles.

<strong>Tomb Raider and Starcraft II: Heart of the Swarm.</strong>

They both blow me away. Super much fun to play. Tomb Raider does remind me a little too much of Uncharted (which of course is funny, as Uncharted borrows a lot from the earlier Tomb Raider games) and focuses too much on shoot-outs to my taste, but plays like a dream. Very adventurous.

Heart of the Swarm grips me a lot faster than Wings of Liberty. The story feels better and is much more exciting.

<h2>Bed game</h2>
The game that's on my nightstand.

<strong>Resident Evil 2/Lumines</strong>

Sony finally added Resident Evil 2 for PS Vita to the European Playstation Store. Still is one of my favorite parts in the series.

<h2>Toilet game</h2>
Or the game that I play when I have a few minutes to spare.

<strong>Carmageddon on iOS</strong>

I backed [the Kickstarter project](http://www.kickstarter.com/projects/stainlessgames/carmageddon-reincarnation) and the iOS game is just the right appetizer. Plays wonderfully (or at least just as crappy as I remember) and looks great.

<iframe width="480" height="270" src="http://www.youtube.com/embed/7BwcC7Bsfsc?rel=0" frameborder="0" allowfullscreen></iframe>
Carmageddon on iOS.

<h2>Related posts</h2>
<div id="blog-archives" class="category">
{% for post in site.categories['games'] %}
{% capture this_year %}{{ post.date | date: "%Y" }}{% endcapture %}
{% unless year == this_year %}
  {% assign year = this_year %}
  <h2>{{ year }}</h2>
{% endunless %}
<article>
  {% include archive_post.html %}
</article>
{% endfor %}
</div>
