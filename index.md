---
layout: default
---

<div class="listing">
{% for post in site.posts offset: 0 limit: 10 %}
  <div class="post">
    <p class="date">{{ post.date | date: "%B %e, %Y" }}</p>
    <h2><a href="{{ post.url }}">{{ post.title }}</a></h2>
    <p class="post-summary">{{ post.excerpt }}</p>
  </div>
{% endfor %}
</div>

---

[Full post archive](/archive/)