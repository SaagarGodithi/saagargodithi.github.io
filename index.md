---
layout: default
title: Welcome
---
# Song of the Week
<figure>
  <img src="public/imgs/sarah_eyes.png" alt="."/>
  <figcaption></figcaption>
</figure>
{% for post in site.posts %}
  * {{ post.date | date_to_string }} [ {{ post.title }} ]({{ post.url }})
{% endfor %}
