# Al Majid Concept — Complete Project Guide

## Table of Contents
1. [What is This?](#what-is-this)
2. [Quick Start](#quick-start)
3. [How the Page is Built](#how-the-page-is-built)
4. [The Two Languages](#the-two-languages)
5. [The Canvas Plates](#the-canvas-plates)
6. [Routing](#routing)
7. [The Design System](#the-design-system)
8. [Editing the Content](#editing-the-content)
9. [Deployment](#deployment)
10. [Rules for This Project](#rules-for-this-project)

---

## What is This?

An unofficial redesign concept for the corporate website of Juma Al Majid Holding Group in Dubai,
built as a front-end design study and portfolio sample.

It is **not affiliated with, commissioned by or endorsed by** the group. The contact form sends and
stores nothing.

Live at https://keerthishree20.github.io/al-majid-concept/.

---

## Quick Start

The whole site is one file, `index.html`, with no build step and no dependencies beyond Google Fonts.

```bash
python3 -m http.server 8000
# open http://localhost:8000
```

Or open `index.html` directly in a browser.

---

## How the Page is Built

One HTML file holding the markup, a `<style>` block and a `<script>` block.

Sections, by id:

| id | section |
|---|---|
| `top` | hero |
| `about` | about the group |
| `businesses` | business divisions |
| `history` | timeline |
| `careers` | careers |
| `news` | news |
| `contact-top` | contact teaser |

A separate contact page is shown through the hash router, described below.

Layout uses CSS logical properties throughout, such as `margin-inline-start` instead of
`margin-left`, so the whole page mirrors correctly for Arabic.

Accessibility: visible focus rings, `prefers-reduced-motion` support, and a layout that works from
360 px wide upward.

---

## The Two Languages

Every piece of translatable text carries both versions as attributes:

```html
<a href="#/contact" data-en="Contact" data-ar="اتصل بنا">Contact</a>
```

The language toggle swaps each element's text to the chosen attribute and sets `dir="rtl"` or
`dir="ltr"` on the page. Arabic text uses IBM Plex Sans Arabic.

To add text, give the element both `data-en` and `data-ar`, with the English also as its initial
content.

---

## The Canvas Plates

Instead of photographs, seven image slots hold generative illustrations drawn on `<canvas>` with a
fixed random seed, so they look the same on every load. The drawing functions include `skyline`,
`map`, `section`, `shaft`, `towers`, `routes` and `strata`, called from `drawPlates()`. They depict a
skyline, a street map, an MEP riser diagram, tower elevations, a route network and a capital
allocation chart.

Each plate is declared in the markup with the drawing to use and its seed:

```html
<div class="plate-frame"><canvas data-plate="skyline" data-seed="1950"></canvas></div>
```

Change `data-seed` for a different variation of the same drawing.

### Swapping in real photos
Each slot is a `.plate` wrapper that controls its aspect ratio, crop and caption. Replace the
`<canvas>` inside with an `<img>`. No CSS change is needed.

---

## Routing

A small hash router shows the home page or the contact page from the same file:
- `#/contact` shows the contact page with its form,
- anything else shows the home page.

The contact form has inline validation, `aria-invalid` states, focus moved to the first error, and a
success message. It does not send data anywhere.

---

## The Design System

| role | typeface |
|---|---|
| display | Bodoni Moda |
| body | Archivo |
| figures and labels | IBM Plex Mono |
| Arabic | IBM Plex Sans Arabic |

| colour | value |
|---|---|
| lacquer petrol-black | `#0C1113` |
| limestone | `#EFEDE6` |
| aged brass | `#C4913F` |

The page has one theme on purpose, with no light and dark switch.

---

## Editing the Content

Everything is in `index.html`. Search for the section id, edit the English text and its `data-en`
attribute, and edit the matching `data-ar` attribute.

---

## Deployment

The live site is served by GitHub Pages from the repository `keerthishree20/al-majid-concept`. Push
to the default branch and Pages republishes it.

---

## Rules for This Project

- **Never invent figures.** Every number on the page is sourced from the group's own pages,
  Wikipedia, or Forbes Middle East's Top 100 Arab Family Businesses list. An unknown value shows
  "to confirm" rather than a plausible guess.
- **Never invent addresses or contact details.**
- **Keep the disclaimer** in the README and on the page. Company names and marks belong to their
  owners.
