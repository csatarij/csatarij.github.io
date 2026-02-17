---
layout: default
title: "All Tags"
permalink: /tags/
---

<h1>All Tags</h1>

<div class="tags-cloud">
  {% for tag in site.tags %}
  <a href="/tags/{{ tag[0] | slugify }}/" class="tag-link">#{{ tag[0] }} ({{ tag[1].size }})</a>
  {% endfor %}
</div>