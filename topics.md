---
layout: default
title: Topics
permalink: /topics/
---

<h1>Topics & Projects</h1>

<p>Documentation and ongoing projects organized by topic. These pages are updated continuously.</p>

<div style="margin-top: 30px;">
  {% for topic in site.topics %}
  <div class="topic-card">
    <h2><a href="{{ topic.url }}">{{ topic.title }}</a></h2>
    {% if topic.updated %}
    <p class="meta">Last updated: {{ topic.updated | date: "%B %d, %Y" }}</p>
    {% endif %}
    {% assign topic_full_words = topic.content | strip_html | split: ' ' | size %}
    {% if topic.excerpt %}
    <p>{{ topic.excerpt | strip_html | truncatewords: 30 }}{% if topic_full_words > 30 %}...{% endif %}</p>
    {% else %}
    <p>{{ topic.content | strip_html | truncatewords: 30 }}{% if topic_full_words > 30 %}...{% endif %}</p>
    {% endif %}
    {% if topic_full_words > 30 %}
    <p class="read-more"><a href="{{ topic.url }}">Read more &rarr;</a></p>
    {% endif %}
  </div>
  {% endfor %}
</div>

<style>
  .topic-card {
    border-bottom: 1px solid var(--border-color);
    margin-bottom: 30px;
    padding-bottom: 20px;
  }

  .topic-card h2 { margin-top: 0; }
  .topic-card h2 a { text-decoration: none; color: var(--text-color); }
  .topic-card .meta { color: #888; font-size: 0.9em; }

  .read-more {
    margin: 10px 0 0 0;
  }

  .read-more a {
    text-decoration: none;
    color: var(--link-color);
    font-size: 0.9em;
  }

  .read-more a:hover {
    color: var(--prompt-color);
    text-decoration: underline;
  }
</style>