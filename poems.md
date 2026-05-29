---
layout: default
title: Poems
---

<div class="listing-intro">
  <h1>Poems</h1>
  <p>A collection of Hindi poetry.</p>
</div>

<div class="card-grid">
  {% assign sorted_poems = site.poems | sort: 'date' | reverse %}
  {% for poem in sorted_poems %}
  <a href="{{ poem.url | relative_url }}" class="card">
    <h2>{{ poem.title }}</h2>
    {% if poem.excerpt %}
    <p class="card-excerpt">{{ poem.excerpt | strip_html | truncatewords: 15 }}</p>
    {% endif %}
  </a>
  {% endfor %}
</div>
