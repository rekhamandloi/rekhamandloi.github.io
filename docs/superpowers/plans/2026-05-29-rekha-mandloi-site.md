# Rekha Mandloi GitHub Pages Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build a Jekyll-based personal literary website for Hindi poet Rekha Mandloi, hosted on GitHub Pages, with a Bio page, Poems listing, and Stories listing using a warm literary aesthetic.

**Architecture:** Jekyll with custom layouts and collections. `_poems` and `_stories` are Jekyll collections — each poem/story is a Markdown file with front matter. A shared `default.html` layout provides nav and footer; `poem.html` and `story.html` extend it. All styling in a single `style.css`.

**Tech Stack:** Jekyll, GitHub Pages, HTML, CSS, Google Fonts (Playfair Display, Lato, Tiro Devanagari Hindi)

---

## File Map

| File | Purpose |
|---|---|
| `_config.yml` | Jekyll config — site title, collections, baseurl |
| `_layouts/default.html` | Base layout: nav + footer + content slot |
| `_layouts/page.html` | Simple page wrapper extending default |
| `_layouts/poem.html` | Individual poem layout extending default |
| `_layouts/story.html` | Individual story layout extending default |
| `assets/css/style.css` | All styles — typography, colors, nav, cards, bio, responsive |
| `index.md` | Home page content |
| `bio.md` | Bio page content |
| `poems.md` | Poems listing page (card grid) |
| `stories.md` | Stories listing page (card grid) |
| `_poems/example-poem.md` | Sample poem to validate layout |
| `_stories/example-story.md` | Sample story to validate layout |
| `.gitignore` | Ignore `_site/`, `.jekyll-cache/`, `.superpowers/` |

---

## Task 1: Jekyll Config + .gitignore

**Files:**
- Create: `_config.yml`
- Create: `.gitignore`

- [ ] **Step 1: Create `_config.yml`**

```yaml
title: "Rekha Mandloi"
description: "Hindi poet and writer"
baseurl: ""
url: "https://rekhamandloi.github.io"
lang: "en"

# Collections
collections:
  poems:
    output: true
    permalink: /poems/:name/
  stories:
    output: true
    permalink: /stories/:name/

# Defaults
defaults:
  - scope:
      path: ""
      type: "poems"
    values:
      layout: "poem"
  - scope:
      path: ""
      type: "stories"
    values:
      layout: "story"

# Build
markdown: kramdown
kramdown:
  input: GFM
```

- [ ] **Step 2: Create `.gitignore`**

```
_site/
.jekyll-cache/
.jekyll-metadata
.sass-cache/
.superpowers/
Gemfile.lock
vendor/
```

- [ ] **Step 3: Commit**

```bash
git add _config.yml .gitignore
git commit -m "feat: add Jekyll config and gitignore"
```

---

## Task 2: Base Layout (`default.html`)

**Files:**
- Create: `_layouts/default.html`

- [ ] **Step 1: Create `_layouts/default.html`**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>{% if page.title %}{{ page.title }} — {% endif %}{{ site.title }}</title>
  <meta name="description" content="{{ page.description | default: site.description }}">
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,400;0,700;1,400&family=Lato:wght@400;700&family=Tiro+Devanagari+Hindi&display=swap" rel="stylesheet">
  <link rel="stylesheet" href="{{ '/assets/css/style.css' | relative_url }}">
</head>
<body>
  <header class="site-header">
    <nav class="nav-inner">
      <a href="{{ '/' | relative_url }}" class="site-title">{{ site.title }}</a>
      <ul class="nav-links">
        <li><a href="{{ '/' | relative_url }}" {% if page.url == '/' %}class="active"{% endif %}>Home</a></li>
        <li><a href="{{ '/bio' | relative_url }}" {% if page.url contains '/bio' %}class="active"{% endif %}>Bio</a></li>
        <li><a href="{{ '/poems' | relative_url }}" {% if page.url contains '/poems' %}class="active"{% endif %}>Poems</a></li>
        <li><a href="{{ '/stories' | relative_url }}" {% if page.url contains '/stories' %}class="active"{% endif %}>Stories</a></li>
      </ul>
    </nav>
  </header>

  <main class="main-content">
    {{ content }}
  </main>

  <footer class="site-footer">
    <p>&copy; {{ 'now' | date: "%Y" }} {{ site.title }}. All rights reserved.</p>
  </footer>
</body>
</html>
```

- [ ] **Step 2: Commit**

```bash
git add _layouts/default.html
git commit -m "feat: add default layout with nav and footer"
```

---

## Task 3: Page, Poem, and Story Layouts

**Files:**
- Create: `_layouts/page.html`
- Create: `_layouts/poem.html`
- Create: `_layouts/story.html`

- [ ] **Step 1: Create `_layouts/page.html`**

```html
---
layout: default
---
<div class="page-content">
  {{ content }}
</div>
```

- [ ] **Step 2: Create `_layouts/poem.html`**

```html
---
layout: default
---
<article class="writing-single">
  <header class="writing-header">
    <h1>{{ page.title }}</h1>
    {% if page.date %}<p class="writing-date">{{ page.date | date: "%B %d, %Y" }}</p>{% endif %}
  </header>
  <div class="writing-body hindi-text">
    {{ content }}
  </div>
  <div class="writing-back">
    <a href="{{ '/poems' | relative_url }}">← Back to Poems</a>
  </div>
</article>
```

- [ ] **Step 3: Create `_layouts/story.html`**

```html
---
layout: default
---
<article class="writing-single">
  <header class="writing-header">
    <h1>{{ page.title }}</h1>
    {% if page.date %}<p class="writing-date">{{ page.date | date: "%B %d, %Y" }}</p>{% endif %}
  </header>
  <div class="writing-body hindi-text">
    {{ content }}
  </div>
  <div class="writing-back">
    <a href="{{ '/stories' | relative_url }}">← Back to Stories</a>
  </div>
</article>
```

- [ ] **Step 4: Commit**

```bash
git add _layouts/page.html _layouts/poem.html _layouts/story.html
git commit -m "feat: add page, poem, and story layouts"
```

---

## Task 4: Stylesheet

**Files:**
- Create: `assets/css/style.css`

- [ ] **Step 1: Create `assets/css/style.css`**

```css
/* ===== Reset & Base ===== */
*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

body {
  background-color: #FAF7F2;
  color: #2C2C2C;
  font-family: 'Lato', sans-serif;
  font-size: 17px;
  line-height: 1.7;
}

a {
  color: #B5541A;
  text-decoration: none;
}

a:hover {
  text-decoration: underline;
}

h1, h2, h3 {
  font-family: 'Playfair Display', serif;
  color: #2C2C2C;
  line-height: 1.3;
}

/* ===== Nav ===== */
.site-header {
  border-bottom: 1px solid #E0D8CE;
  padding: 1rem 0;
  background-color: #FAF7F2;
  position: sticky;
  top: 0;
  z-index: 100;
}

.nav-inner {
  max-width: 860px;
  margin: 0 auto;
  padding: 0 1.5rem;
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.site-title {
  font-family: 'Playfair Display', serif;
  font-size: 1.3rem;
  font-weight: 700;
  color: #2C2C2C;
  text-decoration: none;
}

.nav-links {
  list-style: none;
  display: flex;
  gap: 2rem;
}

.nav-links a {
  color: #2C2C2C;
  font-size: 0.95rem;
  text-decoration: none;
  letter-spacing: 0.02em;
}

.nav-links a:hover,
.nav-links a.active {
  color: #B5541A;
}

/* ===== Main Content ===== */
.main-content {
  max-width: 860px;
  margin: 0 auto;
  padding: 3rem 1.5rem;
}

/* ===== Footer ===== */
.site-footer {
  background-color: #3A2E2A;
  color: #C8B8A8;
  text-align: center;
  padding: 2rem 1.5rem;
  font-size: 0.9rem;
  margin-top: 4rem;
}

/* ===== Home Page ===== */
.home-hero {
  text-align: center;
  padding: 4rem 0 2rem;
}

.home-hero h1 {
  font-size: 3rem;
  margin-bottom: 0.5rem;
}

.home-hero .tagline {
  font-size: 1.1rem;
  color: #6B5B4E;
  margin-bottom: 2rem;
}

.home-hero blockquote {
  font-family: 'Playfair Display', serif;
  font-style: italic;
  font-size: 1.2rem;
  color: #4A3F38;
  border-left: 3px solid #B5541A;
  padding: 0.5rem 1.5rem;
  margin: 2rem auto;
  max-width: 600px;
  text-align: left;
}

.home-cta {
  display: flex;
  gap: 1rem;
  justify-content: center;
  margin-top: 2.5rem;
  flex-wrap: wrap;
}

.btn {
  display: inline-block;
  padding: 0.75rem 2rem;
  border: 2px solid #B5541A;
  color: #B5541A;
  font-family: 'Lato', sans-serif;
  font-size: 0.95rem;
  letter-spacing: 0.05em;
  text-decoration: none;
  transition: background-color 0.2s, color 0.2s;
}

.btn:hover {
  background-color: #B5541A;
  color: #FAF7F2;
  text-decoration: none;
}

.btn-primary {
  background-color: #B5541A;
  color: #FAF7F2;
}

.btn-primary:hover {
  background-color: #8F4014;
}

/* ===== Bio Page ===== */
.bio-photo {
  display: block;
  width: 180px;
  height: 180px;
  border-radius: 50%;
  object-fit: cover;
  margin: 0 auto 2rem;
  border: 3px solid #E0D8CE;
}

.bio-section {
  margin-bottom: 2.5rem;
}

.bio-section h2 {
  font-size: 1.5rem;
  margin-bottom: 1rem;
  color: #B5541A;
}

.bio-section p {
  margin-bottom: 0.75rem;
}

.awards-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(160px, 1fr));
  gap: 1rem;
  margin-top: 1rem;
}

.awards-grid img {
  width: 100%;
  aspect-ratio: 4/3;
  object-fit: cover;
  border: 1px solid #E0D8CE;
}

.awards-grid figcaption {
  font-size: 0.85rem;
  color: #6B5B4E;
  margin-top: 0.4rem;
  text-align: center;
}

.bio-quote {
  font-family: 'Playfair Display', serif;
  font-style: italic;
  font-size: 1.15rem;
  color: #4A3F38;
  border-left: 3px solid #B5541A;
  padding: 0.5rem 1.5rem;
  margin: 1.5rem 0;
}

.social-links {
  display: flex;
  flex-wrap: wrap;
  gap: 1rem;
  margin-top: 1rem;
}

.social-links a {
  font-size: 0.95rem;
  color: #B5541A;
}

/* ===== Card Grid (Poems & Stories) ===== */
.listing-intro {
  margin-bottom: 2rem;
}

.listing-intro h1 {
  font-size: 2.2rem;
  margin-bottom: 0.5rem;
}

.listing-intro p {
  color: #6B5B4E;
}

.card-grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 1.5rem;
}

.card {
  background-color: #F5F0E8;
  border: 1px solid #E0D8CE;
  padding: 1.5rem;
  text-decoration: none;
  color: #2C2C2C;
  display: block;
  transition: box-shadow 0.2s, border-color 0.2s;
}

.card:hover {
  box-shadow: 0 4px 16px rgba(0,0,0,0.08);
  border-color: #B5541A;
  text-decoration: none;
}

.card h2 {
  font-size: 1.2rem;
  margin-bottom: 0.5rem;
  color: #2C2C2C;
}

.card .card-excerpt {
  font-family: 'Tiro Devanagari Hindi', serif;
  font-size: 0.95rem;
  color: #6B5B4E;
  line-height: 1.9;
}

/* ===== Individual Poem / Story ===== */
.writing-single {
  max-width: 680px;
  margin: 0 auto;
}

.writing-header {
  margin-bottom: 2rem;
  padding-bottom: 1rem;
  border-bottom: 1px solid #E0D8CE;
}

.writing-header h1 {
  font-size: 2rem;
  margin-bottom: 0.5rem;
}

.writing-date {
  color: #6B5B4E;
  font-size: 0.9rem;
}

.writing-body {
  font-size: 1.1rem;
  line-height: 1.9;
}

.hindi-text {
  font-family: 'Tiro Devanagari Hindi', serif;
}

.hindi-text p {
  margin-bottom: 1.5rem;
}

.writing-back {
  margin-top: 3rem;
  padding-top: 1.5rem;
  border-top: 1px solid #E0D8CE;
}

.writing-back a {
  font-size: 0.95rem;
  color: #B5541A;
}

/* ===== Page Layout ===== */
.page-content h1 {
  font-size: 2.2rem;
  margin-bottom: 1.5rem;
}

/* ===== Responsive ===== */
@media (max-width: 640px) {
  .home-hero h1 { font-size: 2rem; }
  .card-grid { grid-template-columns: 1fr; }
  .nav-links { gap: 1rem; }
  .awards-grid { grid-template-columns: repeat(2, 1fr); }
}
```

- [ ] **Step 2: Commit**

```bash
git add assets/css/style.css
git commit -m "feat: add full stylesheet with warm literary design"
```

---

## Task 5: Home Page

**Files:**
- Create: `index.md`

- [ ] **Step 1: Create `index.md`**

```markdown
---
layout: default
title: Home
---

<section class="home-hero">
  <h1>Rekha Mandloi<br><span style="font-size:0.7em; font-weight:400;">रेखा मंडलोई</span></h1>
  <p class="tagline">Hindi poet &amp; storyteller</p>

  <blockquote>
    <!-- Replace with her actual writing philosophy quote -->
    "Words are the breath of the soul — I write to remember what the heart already knows."
  </blockquote>

  <div class="home-cta">
    <a href="/poems" class="btn btn-primary">Read Poems</a>
    <a href="/stories" class="btn">Read Stories</a>
  </div>
</section>
```

- [ ] **Step 2: Commit**

```bash
git add index.md
git commit -m "feat: add home page"
```

---

## Task 6: Bio Page

**Files:**
- Create: `bio.md`

- [ ] **Step 1: Create `bio.md`**

```markdown
---
layout: page
title: Bio
---

<section class="bio-section" style="text-align:center;">
  <img src="/assets/images/profile/rekha.jpg" alt="Rekha Mandloi" class="bio-photo">
</section>

<section class="bio-section">
  <h2>About</h2>
  <!-- Replace with her actual bio -->
  <p>Rekha Mandloi is a Hindi poet and writer based in [City], India. Her writing explores themes of memory, womanhood, nature, and the rhythms of everyday life.</p>
</section>

<section class="bio-section">
  <h2>Experience &amp; Credentials</h2>
  <!-- Replace with actual credentials -->
  <p>Add credentials, affiliations, publications, and experience here.</p>
</section>

<section class="bio-section">
  <h2>Awards &amp; Recognition</h2>
  <div class="awards-grid">
    <!-- Add one <figure> per award photo -->
    <!-- Example:
    <figure>
      <img src="/assets/images/awards/award-1.jpg" alt="Award Name">
      <figcaption>Award Name, Year</figcaption>
    </figure>
    -->
    <p style="color:#6B5B4E; font-style:italic;">Award photos coming soon.</p>
  </div>
</section>

<section class="bio-section">
  <h2>Writing Philosophy</h2>
  <blockquote class="bio-quote">
    <!-- Replace with her actual quote -->
    "Words are the breath of the soul — I write to remember what the heart already knows."
  </blockquote>
</section>

<section class="bio-section">
  <h2>Connect</h2>
  <div class="social-links">
    <!-- Replace href values with actual links -->
    <a href="mailto:email@example.com">Email</a>
    <a href="https://facebook.com/" target="_blank" rel="noopener">Facebook</a>
    <a href="https://instagram.com/" target="_blank" rel="noopener">Instagram</a>
  </div>
</section>
```

- [ ] **Step 2: Create placeholder image directories**

```bash
mkdir -p assets/images/profile assets/images/awards
touch assets/images/profile/.gitkeep assets/images/awards/.gitkeep
```

- [ ] **Step 3: Commit**

```bash
git add bio.md assets/images/
git commit -m "feat: add bio page and image directories"
```

---

## Task 7: Poems Listing Page

**Files:**
- Create: `poems.md`

- [ ] **Step 1: Create `poems.md`**

```markdown
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
```

- [ ] **Step 2: Commit**

```bash
git add poems.md
git commit -m "feat: add poems listing page"
```

---

## Task 8: Stories Listing Page

**Files:**
- Create: `stories.md`

- [ ] **Step 1: Create `stories.md`**

```markdown
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
```

- [ ] **Step 2: Commit**

```bash
git add stories.md
git commit -m "feat: add stories listing page"
```

---

## Task 9: Sample Poem and Story

**Files:**
- Create: `_poems/pehli-baarish.md`
- Create: `_stories/example-story.md`

- [ ] **Step 1: Create `_poems/pehli-baarish.md`**

```markdown
---
title: "पहली बारिश"
date: 2024-01-01
---

पहली बारिश की खुशबू में,
कुछ पुराने सपने भीगे।

मिट्टी ने जब साँस ली,
यादें फिर से जागीं।

<!-- Replace with the actual poem -->
```

- [ ] **Step 2: Create `_stories/example-story.md`**

```markdown
---
title: "एक कहानी"
date: 2024-01-01
---

यहाँ कहानी का पहला अनुच्छेद लिखें।

<!-- Replace with the actual story -->
```

- [ ] **Step 3: Commit**

```bash
git add _poems/ _stories/
git commit -m "feat: add sample poem and story as content placeholders"
```

---

## Task 10: Verify Locally

- [ ] **Step 1: Install Jekyll if not already installed**

```bash
gem install bundler jekyll
```

- [ ] **Step 2: Create `Gemfile`**

```ruby
source "https://rubygems.org"
gem "github-pages", group: :jekyll_plugins
```

- [ ] **Step 3: Install gems**

```bash
bundle install
```

- [ ] **Step 4: Serve locally**

```bash
bundle exec jekyll serve
```

Open `http://localhost:4000` in your browser. Verify:
- Home page shows name in English + Devanagari, tagline, quote, two CTA buttons
- Bio page shows all sections with placeholder text
- Poems page shows the sample poem card
- Stories page shows the sample story card
- Clicking a card opens the full poem/story
- "← Back to Poems" and "← Back to Stories" links work
- Nav highlights the active page
- Footer appears on all pages
- Mobile: resize browser to < 640px, confirm single-column card grid

- [ ] **Step 5: Commit Gemfile.lock**

```bash
git add Gemfile Gemfile.lock
git commit -m "chore: add Gemfile for local Jekyll development"
```

---

## Task 11: GitHub Pages Deploy

- [ ] **Step 1: Push to GitHub**

```bash
git push origin main
```

- [ ] **Step 2: Enable GitHub Pages**

In the GitHub repo settings → Pages → Source: set to `Deploy from branch`, Branch: `main`, folder: `/ (root)`. Save.

- [ ] **Step 3: Verify live site**

Wait ~1-2 minutes, then open `https://rekhamandloi.github.io`. Confirm all pages load correctly.
