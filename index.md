---
layout: default
title: Welcome
---
<figure>
  <img src="public/imgs/sarah_eyes.png" alt="."/>
  <figcaption></figcaption>
</figure>

#### Things I'm currently consuming:

- **Books:** *Hero of Ages (Mistborn), American Pastoral, Pachinko, The Last Wish (The Witcher)*
- **TV & Film:** *N/A* 
- **Albums:** *N/A*
- **Other:** *TikToks about TikTok getting banned...*

{% for post in site.posts %}
  * {{ post.date | date_to_string }} [ {{ post.title }} ]({{ post.url }})
{% endfor %}
