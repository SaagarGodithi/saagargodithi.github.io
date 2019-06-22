---
layout: page
title: 
---

<figure>
  <img src="public/imgs/stefan.png" alt="Stefan Burnett"/>
  <figcaption></figcaption>
</figure>

<figure>
  <p class="message">
  Responsibility's cool, but there’s more things in life 
  <br>Like getting your dick rode all fucking night
  <br>By the kind of girl that knows how to keep her shit tight
  <br>Legs in the air, looking like they feel nice
  <br>Volcano pussy melt your peter like ice
  <br>And the drugs got you going back for more cause you're like
  <br>I just can't get enough of that cum clutch, well alright
  <br>It's time to find one and take one
  <br>Right now
  <br>It's time to find one and make one say
  <br>"I'm down"
  </p>
  <figcaption><i>I Want It I Need It</i>, <b>Death Grips</b></figcaption>
</figure>

below are my posts
{% for post in site.posts %}
  * {{ post.date | date_to_string }} [ {{ post.title }} ]({{ post.url }})
{% endfor %}
