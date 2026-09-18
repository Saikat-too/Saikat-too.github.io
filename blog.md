---
layout: default
title: Blog
permalink: /blog/
---

<div class="blog-container">
  <header class="blog-header">
    <h1 class="page-title">Blog</h1>
    <p class="page-description"> This is my space to share insights, studies, and reflections.</p>
  </header>

  <div class="posts-list">
    {% assign sorted_posts = site.blogs | sort: 'date' | reverse %}
    {% for post in sorted_posts %}
      <div class="post-item">
        <div class="post-date">{{ post.date | date: "%b %-d, %Y" }}</div>
        <h2 class="post-title">
          <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
        </h2>
      </div>
    {% endfor %}
  </div>
</div>
