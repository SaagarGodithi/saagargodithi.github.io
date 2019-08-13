---
layout: default
title: Welcome
---
# Song of the Week
<figure>
  <img src="public/itekoma.png" alt="Itekoma Hits"/>
  <figcaption></figcaption>
</figure>

<figure>
  <p class="message">
  Don't Don’t Don’t Don’t
  <br>Don't light my fire
  <br>Don’t light my fire
  <br>Don't GO Don't GO Don't GO GO GO
  <br>Don't light my fire
  <br>Or not GO TO HELL
  <figcaption><i>Don't light my fire</i>, <b>Otoboke Beaver</b></figcaption>
</figure>

<p align="center"><iframe src="https://open.spotify.com/embed/track/18ThXUp9jiQg26iD1w8reE" width="300" height="380" frameborder="0" allowtransparency="true" allow="encrypted-media"></iframe></p>

***


{% for post in site.posts %}
  * {{ post.date | date_to_string }} [ {{ post.title }} ]({{ post.url }})
{% endfor %}
