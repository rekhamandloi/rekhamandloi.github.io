# Rekha Mandloi GitHub Pages — Design Spec
**Date:** 2026-05-29

## Overview

A personal literary website for Hindi writer and poet Rekha Mandloi, hosted on GitHub Pages using Jekyll. The site showcases her bio, poems, and stories with a warm & literary aesthetic. UI language is English; all poem and story content is in Hindi.

---

## Technology

- **Platform:** Jekyll (GitHub Pages native, no CI needed)
- **Hosting:** GitHub Pages (`rekhamandloi.github.io`)
- **Fonts:** Google Fonts — Playfair Display (headings), Lato (body/UI), Tiro Devanagari Hindi (Hindi text)
- **No JavaScript frameworks** — plain HTML/CSS/minimal JS only

---

## Repository Structure

```
rekhamandloi.github.io/
├── _config.yml
├── _layouts/
│   ├── default.html
│   ├── page.html
│   ├── poem.html
│   └── story.html
├── _poems/              # One .md file per poem
├── _stories/            # One .md file per story
├── assets/
│   ├── css/
│   │   └── style.css
│   └── images/
│       ├── profile/     # Author photo
│       └── awards/      # Award photos
├── index.md
├── bio.md
├── poems.md
└── stories.md
```

---

## Pages

### Home (`index.md`)
- Author name in English + Devanagari script
- One-line tagline (e.g., "Hindi poet & storyteller")
- Featured quote from her writing philosophy (styled blockquote)
- Two CTA buttons: "Read Poems" and "Read Stories"

### Bio (`bio.md`)
- Profile photo (top, centered)
- Short intro paragraph
- Credentials & experience section
- Awards section — photo grid (images in `assets/images/awards/`)
- Writing philosophy — her personal quote in a styled blockquote
- Contact / social links (email, Facebook, Instagram, etc.)

### Poems (`poems.md`)
- Page heading + one-line intro
- Card grid (2-col desktop, 1-col mobile)
- Each card: poem title + first 1-2 lines as excerpt
- Card links to individual poem page

### Stories (`stories.md`)
- Same structure as Poems page

### Individual Poem page (`_poems/<slug>.md`)
- Title
- Optional: date
- Full Hindi text with generous line-height (1.9)
- "← Back to Poems" navigation link

### Individual Story page (`_stories/<slug>.md`)
- Same structure as individual poem page
- "← Back to Stories" navigation link

---

## Visual Design

### Color Palette
| Role | Value |
|---|---|
| Background | `#FAF7F2` (warm off-white) |
| Primary text | `#2C2C2C` (dark charcoal) |
| Accent (links, headings) | `#B5541A` (muted terracotta) |
| Card background | `#F5F0E8` (soft cream) |
| Footer background | `#3A2E2A` (dark warm brown) |

### Typography
- **Headings:** Playfair Display (serif, literary)
- **Body / UI labels:** Lato (clean, readable)
- **Hindi content:** Tiro Devanagari Hindi
- Hindi text line-height: `1.9`

### Layout
- Max content width: `860px`, centered
- Navigation: top bar — site name left, page links right
- Cards: 2-column grid on desktop, 1-column on mobile
- Generous padding throughout; no heavy ornamentation

---

## Content To Be Provided

- [ ] Author photo (`assets/images/profile/`)
- [ ] Award photos (`assets/images/awards/`)
- [ ] Bio text: credentials, experience
- [ ] Writing philosophy quote
- [ ] Contact / social media links
- [ ] Poems (Hindi text, one per file)
- [ ] Stories (Hindi text, one per file)

---

## Out of Scope

- CMS or admin interface
- Comments or user interaction
- Search functionality
- Analytics (can be added later via `_config.yml`)
