---
layout: default
title: Stories
---

<div class="listing-intro">
  <h1>Stories</h1>
  <p>A collection of Hindi short stories.</p>
</div>

<div class="card-grid">
  {% assign sorted_stories = site.stories | sort: 'date' | reverse %}
  {% for story in sorted_stories %}
  <a href="{{ story.url | relative_url }}" class="card">
    <h2>{{ story.title }}</h2>
    {% if story.excerpt %}
    <p class="card-excerpt">{{ story.excerpt | strip_html | truncatewords: 15 }}</p>
    {% endif %}
  </a>
  {% endfor %}
</div>
