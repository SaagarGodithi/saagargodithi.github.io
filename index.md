---
layout: default
title: Welcome
---

<figure>
  <img src="public/imgs/stefan.png" alt="Stefan Burnett"/>
  <figcaption></figcaption>
</figure>

<figure>
  <p class="message">
  Her boob gets so floppy
  <br>She uses it as a fan to wave away his sickening B.O.​
  <br>Now rubbing it off with a brick
  <br>Dust for his panettone
  <br>Every frog hops right up into her butthole
  <br>Every frog eats a single butthole flea on its way in
  <br>She brown box squeezes them all into froghost
  <br>A flock of erect dicks on bat wings
  <br>Pee-pees into her sleeping face
  <br>And pointlessly tries to fuck a blue sky
  </p>
  <figcaption><i>Girl with a Basket of Fruit</i>, <b>Xiu Xiu</b></figcaption>
</figure>

<p align="center"><iframe src="https://open.spotify.com/embed/track/2WuS3PjLJW15ckkwWXO8V2" width="300" height="80" frameborder="0" allowtransparency="true" allow="encrypted-media" ></iframe></p>


***

{% for post in site.posts %}
  * {{ post.date | date_to_string }} [ {{ post.title }} ]({{ post.url }})
{% endfor %}
