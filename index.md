---
layout: default
title: Blog Posts
permalink: /
---

<div class="main-layout">
  <div class="blog-section">
    <h1>Recent Posts</h1>

    {% for post in site.posts %}
    <div class="post-card">
      <h2><a href="{{ post.url }}">{{ post.title }}</a></h2>
      <p class="meta">{{ post.date | date: "%B %d, %Y" }}</p>
      {% assign content_words = post.content | strip_html | split: ' ' | size %}
      {% if post.excerpt %}
        {% assign excerpt_words = post.excerpt | strip_html | split: ' ' | size %}
      {% endif %}
      {% if post.excerpt %}
        {% if excerpt_words < 40 %}
          <p>{{ post.excerpt | strip_html }}</p>
        {% else %}
          <p>{{ post.excerpt | strip_html | truncatewords: 40 }}</p>
        {% endif %}
      {% else %}
        {% if content_words < 40 %}
          <p>{{ post.content | strip_html }}</p>
        {% else %}
          <p>{{ post.content | strip_html | truncatewords: 40 }}</p>
        {% endif %}
      {% endif %}
      {% if post.excerpt %}
        {% if content_words > excerpt_words %}
      <p class="read-more"><a href="{{ post.url }}">Read more &rarr;</a></p>
        {% endif %}
      {% else %}
        {% if content_words > 40 %}
      <p class="read-more"><a href="{{ post.url }}">Read more &rarr;</a></p>
        {% endif %}
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
  </div>

  <div class="topics-sidebar">
    <h3>Topics &amp; Projects</h3>
    <div class="topics-list">
      {% for topic in site.topics limit: 5 %}
      <div class="topic-preview">
        <h4><a href="{{ topic.url }}">{{ topic.title }}</a></h4>
        {% if topic.updated %}
        <p class="meta-small">{{ topic.updated | date: "%b %d" }}</p>
        {% endif %}
        {% assign topic_words = topic.content | strip_html | split: ' ' | size %}
        {% if topic.excerpt %}
        <p>{{ topic.excerpt | strip_html | truncatewords: 25 }}{% if topic_words > 25 %}...{% endif %}</p>
        {% else %}
        <p>{{ topic.content | strip_html | truncatewords: 25 }}{% if topic_words > 25 %}...{% endif %}</p>
        {% endif %}
        {% if topic_words > 25 %}
        <p class="read-more-small"><a href="{{ topic.url }}">Read more &rarr;</a></p>
        {% endif %}
      </div>
      {% endfor %}
    </div>
    {% if site.topics.size > 5 %}
    <p class="view-all-topics"><a href="/topics/">View all topics &rarr;</a></p>
    {% endif %}
  </div>
</div>

<style>
  .main-layout {
    display: grid;
    grid-template-columns: 1fr;
    gap: 30px;
  }

  .blog-section {
    margin-right: 0;
  }

  .post-card {
    border: 1px solid var(--border-color);
    border-left: 3px solid var(--code-bg);
    margin-bottom: 15px;
    padding: 20px;
    border-radius: 6px;
    background: var(--code-bg);
    transition: all 0.2s;
  }

  .post-card:hover {
    border-left-color: var(--link-color);
    transform: translateX(5px);
  }

  .post-card h2 {
    margin-top: 0;
    font-size: 1.2em;
  }

  .post-card h2 a {
    text-decoration: none;
    color: var(--link-color);
  }

  .post-card h2 a:hover {
    color: var(--prompt-color);
  }

  .post-card .meta {
    color: var(--muted-color);
    font-size: 12px;
    margin: 4px 0 8px 0;
  }

  .post-card .meta::before {
    content: "$ ";
    color: var(--prompt-color);
  }

  .topics-sidebar {
    position: sticky;
    top: 20px;
    height: fit-content;
  }

  .topics-sidebar h3 {
    margin-top: 0;
    margin-bottom: 20px;
    color: var(--link-color);
    font-size: 1.3em;
  }

  .topics-list {
    display: flex;
    flex-direction: column;
    gap: 15px;
  }

  .topic-preview {
    border: 1px solid var(--border-color);
    border-left: 3px solid var(--code-bg);
    padding: 20px;
    border-radius: 6px;
    background: var(--code-bg);
    transition: all 0.2s;
  }

  .topic-preview:hover {
    border-left-color: var(--link-color);
    transform: translateX(5px);
  }

  .topic-preview h4 {
    margin: 0 0 4px 0;
    font-size: 1.1em;
  }

  .topic-preview h4 a {
    text-decoration: none;
    color: var(--link-color);
  }

  .topic-preview h4 a:hover {
    color: var(--prompt-color);
  }

  .topic-preview p {
    margin: 5px 0;
    font-size: 0.9em;
    color: var(--muted-color);
  }

  .topic-preview .meta-small {
    font-size: 11px !important;
    margin: 4px 0 8px 0;
  }

  .topic-preview .meta-small::before {
    content: "$ ";
    color: var(--prompt-color);
  }

  .meta-small {
    font-size: 0.8em !important;
  }

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

  .read-more-small {
    margin: 8px 0 0 0;
  }

  .read-more-small a {
    text-decoration: none;
    color: var(--link-color);
    font-size: 0.85em;
  }

  .read-more-small a:hover {
    color: var(--prompt-color);
    text-decoration: underline;
  }

  .view-all-topics {
    margin-top: 15px;
    text-align: center;
  }

  .view-all-topics a {
    text-decoration: none;
    color: var(--link-color);
    font-size: 0.9em;
  }

  .view-all-topics a:hover {
    color: var(--prompt-color);
  }

  @media (min-width: 769px) {
    .main-layout {
      grid-template-columns: 65% 1fr;
    }
  }

  @media (max-width: 768px) {
    .topics-sidebar {
      position: static;
      order: 2;
    }
  }
</style>