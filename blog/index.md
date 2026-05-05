---
layout: default
title: Blog
---

<div class="blog-list">
  {% for post in site.posts %}
  <div class="blog-post">
    <h2><a href="{{ post.url }}">{{ post.title }}</a></h2>
    <span class="blog-date">{{ post.date | date: "%B %-d, %Y" }}</span>
    <p class="blog-excerpt">{{ post.excerpt | strip_html | truncatewords: 40 }}</p>
  </div>
  {% endfor %}
</div>
