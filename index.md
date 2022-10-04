---
layout: default
---

<div class="home">

  {% if site.paginate %}
    {% assign posts = paginator.posts %}
  {% else %}
    {% assign posts = site.posts %}
  {% endif %}

  {%- if posts.size > 0 -%}
    <ul class="post-list">
      {%- assign date_format = site.date_format | default: "%b %-d, %Y" -%}
      {%- for post in posts limit:10 -%}
      <li>
        <h2>
          <a href="{{ post.url | relative_url }}">
            {{ post.title | escape }}
          </a>
        </h2>
        <p class="post-meta">
          <time class="dt-published" datetime="{{ post.date | date_to_xmlschema }}" itemprop="datePublished">
            {{ post.date | date: date_format }}
          </time>
          {%- if jekyll.environment == "production" and site.disqus -%}
            • <a href="{{ post.url | relative_url }}#disqus_thread">
                <span class="disqus-comment-count" data-disqus-url="{{ post.url | absolute_url }}"></span>
              </a>
          {%- endif -%}
        </p>
        {%- if post.show_excerpts != false -%}
          <div class="post-excerpt">{{ post.excerpt | strip_html }}</div>
        {%- endif -%}
      </li>
      {%- endfor -%}
    </ul>

  {%- endif -%}
  
</div>

---

[Full post archive](/archive/)