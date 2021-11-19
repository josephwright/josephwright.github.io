---
layout: archive-years
permalink: /archive/
---

<div class="listing">
{% for post in site.posts %}
  <div class="post">
    <p class="date">{{ post.date | date: "%B %e, %Y" }}</p>
    <h2><a href="{{ post.url }}">{{ post.title }}</a></h2>
  </div>
{% endfor %}
</div>
