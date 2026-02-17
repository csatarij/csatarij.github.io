---
layout: default
title: Blog Posts
permalink: /
---

<h1>Recent Posts</h1>

{% for post in site.posts %}
<div class="post-preview">
  <h2><a href="{{ post.url }}">{{ post.title }}</a></h2>
  <p class="meta">{{ post.date | date: "%B %d, %Y" }}</p>
  {% if post.excerpt %}
  <p>{{ post.excerpt | strip_html | truncatewords: 40 }}</p>
  {% else %}
  <p>{{ post.content | strip_html | truncatewords: 40 }}</p>
  {% endif %}
</div>
{% endfor %}

{% if site.paginate %}
<div class="pagination">
  {% if paginator.next_page %}
  <a href="{{ paginator.next_page_path }}">Older posts &rarr;</a>
  {% endif %}
</div>
{% endif %}