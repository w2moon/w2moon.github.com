---
layout: page
title: Day Day Up!
tagline: to be continue...
---
{% include JB/setup %}
<ul class="posts">
  {% for post in site.posts limit:5  %}
    <h3 href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</h3>
<hr/>
{{post.content}}
  {% endfor %}
</ul>


