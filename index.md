---
layout: page
title: Why are you here?
---

<p class="message">
  Hey there! You shouldn't be here. Leave!
</p>

### Why are you still here? 
  My name is **Saagar** and you should *leave*!

### Since you are still here, you might as well read my posts. 
{% for post in site.posts %}
  * {{ post.date | date_to_string }} [ {{ post.title }} ]({{ post.url }})
{% endfor %}
