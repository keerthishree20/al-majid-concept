# Al Majid Concept — Complete Project Guide

A complete guide to a one-file, bilingual corporate site redesign concept: every feature, every design
decision and the reason behind it, with the real code. It is self-contained: you can paste it into any
AI chat and ask questions about the project without sharing the repository.

**Repository:** https://github.com/keerthishree20/al-majid-concept
**Live:** https://keerthishree20.github.io/al-majid-concept/
**All projects:** https://github.com/keerthishree20

---

## Table of Contents

1. [Project Overview](#1-project-overview)
2. [Tech Stack & Why](#2-tech-stack--why)
3. [Project Setup from Scratch](#3-project-setup-from-scratch)
4. [File Anatomy](#4-file-anatomy)
5. [Page Sections](#5-page-sections)
6. [Design System](#6-design-system)
7. [Responsive Layout & Logical Properties](#7-responsive-layout--logical-properties)
8. [Reveal on Scroll & the Hero Sequence](#8-reveal-on-scroll--the-hero-sequence)
9. [Animated Counters](#9-animated-counters)
10. [Sector Accordion](#10-sector-accordion)
11. [Mobile Navigation](#11-mobile-navigation)
12. [Canvas Plates: Generative Illustrations](#12-canvas-plates-generative-illustrations)
13. [Hash Router: Two Pages, One File](#13-hash-router-two-pages-one-file)
14. [Contact Form Validation](#14-contact-form-validation)
15. [English ⇄ Arabic with RTL](#15-english--arabic-with-rtl)
16. [Accessibility](#16-accessibility)
17. [Sourcing Rules](#17-sourcing-rules)
18. [Editing the Content](#18-editing-the-content)
19. [Deployment](#19-deployment)
20. [Troubleshooting](#20-troubleshooting)
21. [Complete Feature Summary](#21-complete-feature-summary)

---

## 1. Project Overview

An **unofficial redesign concept** for the corporate website of Juma Al Majid Holding Group, a Dubai
holding group. It was built as a front-end design study and portfolio sample.

> It is **not affiliated with, commissioned by or endorsed by** the group. Company names and marks
> belong to their owners. The contact form sends nothing and stores nothing.

What it shows off:
- **one HTML file**, no build step, no framework,
- **two pages** from that file with a hash router (home and `#/contact`),
- **English ⇄ Arabic** with a real right-to-left flip,
- **seven generative canvas illustrations** instead of photos,
- a contact form with **accessible inline validation**,
- scroll reveals, animated counters, an accordion, a mobile menu,
- responsive from **360 px**, with `prefers-reduced-motion` support.

**Status:** complete and live on GitHub Pages.

---

## 2. Tech Stack & Why

| Technology | Role | Why We Chose It |
|---|---|---|
| **HTML** | Markup and both pages | one file anyone can open |
| **CSS** (custom properties, grid, logical properties) | Styling | full control; logical properties make RTL work automatically |
| **Vanilla JavaScript** (one IIFE) | Behaviour | the features are small; a framework would add weight and a build |
| **Canvas 2D** | Illustrations | no licensed photos needed; drawn to fit any size |
| **Google Fonts** | Typography | Bodoni Moda, Archivo, IBM Plex Mono, IBM Plex Sans Arabic |
| **GitHub Pages** | Hosting | free, deploys on push |

### Why no framework?
A design study should load instantly and be readable as one file. Every behaviour here (router, toggle,
validation, accordion) is 10–40 lines of plain JavaScript.

---

## 3. Project Setup from Scratch

```bash
git clone https://github.com/keerthishree20/al-majid-concept.git
cd al-majid-concept
python3 -m http.server 8000        # open http://localhost:8000
```

Or double-click `index.html`. Nothing to install.

---

## 4. File Anatomy

`index.html` (~1,740 lines):

```
<head>
  <title>Al Majid Group Concept</title>
  Google Fonts link (preconnect first)
  <script>document.documentElement.classList.add("js");</script>   ← marks "JS is on"
  <style>  :root tokens → base → nav → hero → sections → plates → contact → media queries
</head>
<body>
  <nav id="nav"> … language button #lang, toggle #navtoggle, links #navlinks
  <div id="v-home">     hero #top · band · #about · #businesses · #history · #careers · #news
  <div id="v-contact" hidden>   #contact-top page with the form #cform and success panel #csent
  <footer>
  <script> (function(){ "use strict"; … })();   ← all behaviour
</body>
```

### Why add a `js` class first?
CSS can hide reveal-on-scroll elements only when `html.js` is present. If JavaScript fails, nothing is
hidden and the page is still readable.

---

## 5. Page Sections

| id | Section | Headline (English) |
|---|---|---|
| `top` | Hero | load-sequence animation |
| (band) | Full-width plate | skyline illustration |
| `about` | About the group | "A family business that kept the country's pace." |
| `businesses` | Sectors, with accordion | "Five sectors. One balance sheet." |
| `history` | Timeline | "1950 to now, in agencies won." |
| `careers` | Careers | a headline built on the workforce figure |
| `news` | News | "Latest from the group" |
| `contact-top` | Contact page (router) | "Reach the right desk, first time." |

The five sectors in the accordion are **Commercial** (automotive, electronics, FMCG, building
materials), **Contracting & Services** (MEP, HVAC, fire protection, facilities management), **Real
Estate** (development, leasing, hospitality assets), **Travel & Tourism** (corporate travel, leisure,
hotel management) and **Investment** (portfolio, treasury, new ventures).

---

## 6. Design System

All in `:root`:

```css
:root{
  --ink:        #0C1113;   /* lacquer petrol-black */
  --paper:      #EFEDE6;   /* limestone */
  --brass:      #C4913F;   /* aged brass */
  --brass-lo:   #8E6726;
  --brass-hi:   #E3BE7C;
  --on-ink:     #F3F1EC;   --on-ink-mid: #A6AFB2;   --on-ink-dim: #6C777B;
  --on-paper:   #10171A;   --on-paper-mid: #55605F;

  --display: "Bodoni Moda", "Didot", "Times New Roman", serif;
  --body:    "Archivo", "Helvetica Neue", Arial, sans-serif;
  --mono:    "IBM Plex Mono", "SFMono-Regular", Menlo, monospace;
  --arabic:  "IBM Plex Sans Arabic", "Noto Sans Arabic", sans-serif;

  --gut:  clamp(20px, 4.5vw, 64px);    /* side gutter scales with the screen */
  --maxw: 1360px;
  --sec-y: clamp(72px, 9vw, 148px);    /* section spacing */
  --ease: cubic-bezier(.22,.61,.36,1);
}
```

| Role | Typeface | Why |
|---|---|---|
| Display | Bodoni Moda | high-contrast serif: old-money, established |
| Body | Archivo | plain, readable grotesque |
| Figures and labels | IBM Plex Mono | numbers line up like a ledger |
| Arabic | IBM Plex Sans Arabic | designed to pair with the Plex family |

Sections alternate between dark **ink** and light **paper** (`class="sec paper"`), with brass accents.
The page has **one theme on purpose**. A holding group's identity is a fixed palette, not a light/dark
preference.

`clamp()` for spacing means sizes scale smoothly between phone and desktop with no breakpoints.

---

## 7. Responsive Layout & Logical Properties

Grids collapse to one column at breakpoints between 560 and 920 px (hero, chapters, split, cards,
contact grid, footer).

**Logical properties** are used throughout: `margin-inline-start` instead of `margin-left`,
`padding-block-start` instead of `padding-top`, and so on. They follow the reading direction, so when
the page switches to `dir="rtl"` the whole layout mirrors with no extra CSS. The only RTL-specific rule
is the nav underline animation origin:

```css
html[dir="rtl"] .nav-links a::after{ --o:right; }
```

---

## 8. Reveal on Scroll & the Hero Sequence

```js
var reduce = window.matchMedia("(prefers-reduced-motion: reduce)").matches;
var revealables = document.querySelectorAll(".rv, .hero-anim");

if (!("IntersectionObserver" in window) || reduce) {
  revealables.forEach(function(el){ el.classList.add("in"); });     // show everything at once
} else {
  var io = new IntersectionObserver(function(entries){
    entries.forEach(function(e){
      if (e.isIntersecting){ e.target.classList.add("in"); io.unobserve(e.target); }
    });
  }, { rootMargin: "0px 0px -8% 0px", threshold: 0.06 });
  revealables.forEach(function(el){ io.observe(el); });

  /* hero plays as an orchestrated load sequence, not on scroll */
  document.querySelectorAll(".hero-anim").forEach(function(el, i){
    io.unobserve(el);
    el.style.transitionDelay = (0.08 * i + 0.05) + "s";               // stagger
    requestAnimationFrame(function(){ requestAnimationFrame(function(){ el.classList.add("in"); }); });
  });
}
```

- Elements with `.rv` fade in once as they scroll into view.
- Hero elements play on load, each 80 ms after the previous.
- **Double `requestAnimationFrame`** makes sure the browser has painted the hidden state first;
  otherwise the transition would be skipped.
- Reduced motion or an old browser: everything is shown immediately.

---

## 9. Animated Counters

Elements like `<span class="count" data-to="7500">` count up when 40% visible:

```js
function runCount(el){
  var target = parseFloat(el.getAttribute("data-to"));
  if (reduce || !isFinite(target)) { return; }       // leave the real number in place
  var dur = 1400, t0 = null;
  function frame(t){
    if (t0 === null) t0 = t;
    var p = Math.min((t - t0) / dur, 1);
    var eased = 1 - Math.pow(1 - p, 3);              // ease-out cubic: fast start, gentle stop
    el.textContent = Math.round(target * eased).toLocaleString("en-US");
    if (p < 1) requestAnimationFrame(frame);
  }
  el.textContent = "0";
  requestAnimationFrame(frame);
}
```

The HTML already contains the final number, so without JavaScript or with reduced motion the correct
figure shows. Every `data-to` value is a sourced figure (see [Sourcing Rules](#17-sourcing-rules)).

---

## 10. Sector Accordion

```js
var rows = document.querySelectorAll("#index .row");
rows.forEach(function(row){
  var btn = row.querySelector(".row-btn");
  btn.addEventListener("click", function(){
    var open = row.getAttribute("data-open") === "true";
    rows.forEach(function(r){                                   // close all
      r.setAttribute("data-open", "false");
      r.querySelector(".row-btn").setAttribute("aria-expanded", "false");
    });
    if (!open){                                                 // open the clicked one
      row.setAttribute("data-open", "true");
      btn.setAttribute("aria-expanded", "true");
    }
  });
});
```

One sector open at a time. `aria-expanded` tells screen readers the state. CSS styles
`[data-open="true"]`. After opening, plates inside are redrawn at 60 ms and 480 ms, once the panel has
its final size.

---

## 11. Mobile Navigation

```js
toggle.addEventListener("click", function(){
  var open = nav.getAttribute("data-open") === "true";
  nav.setAttribute("data-open", open ? "false" : "true");
  toggle.setAttribute("aria-expanded", open ? "false" : "true");
});
document.getElementById("navlinks").addEventListener("click", function(e){
  if (e.target.tagName === "A"){ nav.setAttribute("data-open", "false"); toggle.setAttribute("aria-expanded","false"); }
});
```

Below 900 px the links collapse behind a toggle. Tapping a link closes the menu (event delegation: one
listener on the list, not one per link).

---

## 12. Canvas Plates: Generative Illustrations

Seven image slots are drawn in code:

```html
<div class="plate-frame"><canvas data-plate="skyline" data-seed="1950"></canvas></div>
```

| Plate | Seed | Depicts |
|---|---|---|
| `skyline` | 1950 | layered city skyline |
| `map` | 156 | street map |
| `section` | 0158 | cross-section of a shed or warehouse |
| `shaft` | 1967 | MEP riser diagram |
| `towers` | 2023 | tower elevations |
| `routes` | 1988 | route network |
| `strata` | 2027 | capital allocation chart |

### Seeded randomness
```js
function mulberry32(a){                 // tiny, fast seeded PRNG
  return function(){
    a |= 0; a = a + 0x6D2B79F5 | 0;
    var t = Math.imul(a ^ a >>> 15, 1 | a);
    t = t + Math.imul(t ^ t >>> 7, 61 | t) ^ t;
    return ((t ^ t >>> 14) >>> 0) / 4294967296;
  };
}
```
`Math.random()` would draw a different picture every load. A seeded generator gives the **same picture
every time**, and a new seed gives a different variation.

### Drawing at the right size
```js
function drawPlates(){
  document.querySelectorAll("canvas[data-plate]").forEach(function(cv){
    var box = cv.parentNode.getBoundingClientRect();
    var w = Math.round(box.width), h = Math.round(box.height);
    if (!w || !h) return;                                            // hidden: skip
    if (cv.dataset.w === String(w) && cv.dataset.h === String(h)) return;   // unchanged: skip
    var dpr = Math.min(window.devicePixelRatio || 1, 2);            // sharp on retina, capped at 2x
    cv.width = w*dpr; cv.height = h*dpr;
    cv.dataset.w = w; cv.dataset.h = h;
    var c = cv.getContext("2d");
    c.setTransform(dpr,0,0,dpr,0,0);
    var fn = PLATES[cv.getAttribute("data-plate")] || skyline;
    fn(c, w, h, mulberry32(parseInt(cv.getAttribute("data-seed"),10) || 7));
  });
}
```

It redraws on load, on resize (debounced 180 ms), on route change, on language change and after the
accordion opens. Shared helpers (`ground` gradient, `glow`, `hair` brass lines, `pale` light lines) keep
all seven in one visual language.

### Swapping in real photos
Each slot is a `.plate` wrapper that owns aspect ratio, crop and caption. Replace the `<canvas>` with an
`<img>`; no CSS change is needed.

---

## 13. Hash Router: Two Pages, One File

```js
function route(){
  var h = location.hash || "";
  var onContact = h.indexOf("#/contact") === 0;

  vHome.hidden = onContact;
  vContact.hidden = !onContact;
  navAnchors.forEach(function(a){
    a.classList.toggle("here", onContact && a.getAttribute("href") === "#/contact");
  });

  if (onContact){
    showAll(vContact);                         // no scroll reveals on a fresh page
    window.scrollTo(0,0);
  } else {
    var id = h.replace(/^#/, "");
    if (id && id.charAt(0) !== "/"){           // "#about" → scroll to the section
      var t = document.getElementById(id);
      if (t) requestAnimationFrame(function(){
        t.scrollIntoView({ behavior: reduce ? "auto" : "smooth", block: "start" });
      });
    } else if (h.indexOf("#/") === 0){
      window.scrollTo(0,0);
    }
  }
  requestAnimationFrame(drawPlates);
}
window.addEventListener("hashchange", route);
```

- `#/contact` shows the contact view.
- `#about`, `#history` and so on show home and scroll to that section, even when coming from the
  contact page.
- The `#/` prefix separates "routes" from "section anchors".

### Why a hash router?
GitHub Pages serves static files only. A path like `/contact` would 404, but a hash never reaches the
server, so it always works.

---

## 14. Contact Form Validation

Fields: name, email, enquiry topic (General, Commercial, Contracting & Services, Real Estate, Travel &
Tourism, Investment & partnerships, Supplier registration, …), message, consent checkbox.

```js
var checks = {
  name:    function(v){ return v.trim().length >= 2; },
  email:   function(v){ return /^[^\s@]+@[^\s@]+\.[^\s@]{2,}$/.test(v.trim()); },
  topic:   function(v){ return v !== ""; },
  message: function(v){ return v.trim().length >= 20; }
};
```

**When errors appear:** a field is marked "touched" on blur or change. After that it re-validates on
every keystroke. So no error appears while you type your first letters, but it clears as soon as you fix
it.

```js
function mark(name, bad){
  var f = cform.querySelector('[data-for="'+name+'"]');
  f.setAttribute("data-invalid", bad ? "true" : "false");          // CSS shows the message
  f.querySelector("input,select,textarea").setAttribute("aria-invalid", bad ? "true" : "false");
}
```

**On submit:** every field is checked, consent too. If anything fails, **focus moves to the first bad
field**. If all pass, the form hides and a success panel shows a reference like `REF AM-2026-4821`,
the desk it was "routed to", and the line *"Nothing was actually sent — this page is a design
concept."* "Send another" resets the form and focuses the name field.

---

## 15. English ⇄ Arabic with RTL

Every translatable element carries both languages:

```html
<h2 data-en="Latest from the group" data-ar="آخر الأخبار">Latest from the group</h2>
```

```js
langBtn.addEventListener("click", function(){
  isAR = !isAR;
  root.setAttribute("dir", isAR ? "rtl" : "ltr");
  root.setAttribute("lang", isAR ? "ar" : "en");
  langBtn.textContent = isAR ? "English" : "العربية";
  document.querySelectorAll("[data-en]").forEach(function(el){
    var v = el.getAttribute(isAR ? "data-ar" : "data-en");
    if (v) el.innerHTML = v;
  });
  requestAnimationFrame(drawPlates);
});
```

- `dir="rtl"` plus logical properties mirrors the layout.
- `lang="ar"` lets CSS switch to the Arabic font and helps screen readers pronounce it.
- The English is also the element's initial content, so the page works with no JavaScript.

---

## 16. Accessibility

- Visible **focus rings** on every interactive element.
- **`prefers-reduced-motion`**: no reveals, counters or smooth scrolling; all content visible at once.
- **`aria-expanded`** on the accordion and menu toggle; **`aria-invalid`** on bad fields; focus moved to
  the first error.
- **`lang` and `dir`** updated when switching language.
- **Works without JavaScript**: the `js` class guard, real numbers in the HTML, English text in place.
- Readable from **360 px** wide.

---

## 17. Sourcing Rules

These rules are the heart of the project's credibility:

1. **Never invent figures.** Every number on the page comes from the group's own About and Contact
   pages, Wikipedia (Juma Al Majid Holding Group), or Forbes Middle East's Top 100 Arab Family Businesses.
2. **Unknown values say "to confirm"**, for example `ext. — · to confirm` for department extensions and
   "Sun – Thu · hours to confirm" for working hours. A plausible-looking guess is worse than an honest gap.
3. **Never invent addresses or contact details.**
4. **Keep the disclaimer** in the README and on the page.

When pasting this into an AI chat to edit copy: tell it not to add any number, date, address or name
that isn't already on the page or in those sources.

---

## 18. Editing the Content

Everything is in `index.html`:
1. Find the section by its id (`id="about"` etc.).
2. Edit the English in **both** the element text and `data-en`.
3. Edit the Arabic in `data-ar`.
4. For a counter, change `data-to` **and** the number in the element text.
5. For a plate, change `data-seed` for a new variation, or `data-plate` for a different drawing.

---

## 19. Deployment

GitHub Pages serves the repo's default branch:

```bash
git add index.html
git commit -m "Update copy"
git push
```

Pages republishes in about a minute at https://keerthishree20.github.io/al-majid-concept/.

---

## 20. Troubleshooting

| Problem | Fix |
|---|---|
| plates are blank | the parent had zero size when drawn; resizing redraws. Check the console for a typo in `data-plate` |
| text didn't switch to Arabic | the element is missing `data-en`/`data-ar` |
| layout doesn't mirror in Arabic | a rule uses `left`/`right` instead of a logical property |
| nothing animates | reduced motion is on in the OS (intended) |
| `/contact` gives 404 | use `#/contact` |

---

## 21. Complete Feature Summary

### All Features Built

| # | Feature | Type | Where in `index.html` |
|---|---|---|---|
| 1 | Design tokens (colour, type, fluid spacing) | CSS | `:root` |
| 2 | Responsive layout with logical properties | CSS | media queries |
| 3 | Reveal on scroll + staggered hero | JS | "reveal on scroll" |
| 4 | Ease-out animated counters | JS | "ledger counters" |
| 5 | Five-sector accordion | JS | "sector index" |
| 6 | Mobile navigation | JS | "mobile nav" |
| 7 | Seven seeded canvas plates, DPR-aware | JS | "plates" |
| 8 | Hash router (home + contact) | JS | "router" |
| 9 | Contact form with accessible validation | JS | "contact form" |
| 10 | English ⇄ Arabic with RTL | JS + CSS | "EN / AR" |
| 11 | Reduced motion, no-JS fallback, focus rings | A11y | throughout |
| 12 | Sourced figures with "to confirm" gaps | Content | throughout |

### Data Flow Architecture

```
index.html loads
  ├─ <head> adds html.js ─► CSS may hide .rv elements
  ├─ route() ─► #/contact ? contact view : home view (+ scroll to #section)
  ├─ drawPlates() ─► each canvas[data-plate] ─► PLATES[name](ctx, w, h, mulberry32(seed))
  ├─ IntersectionObserver ─► .rv → .in   ·   .count → runCount()
  └─ listeners
       hashchange ─► route()            resize ─► drawPlates() (debounced)
       #lang ─► swap data-en/data-ar, dir, lang ─► drawPlates()
       .row-btn ─► accordion ─► drawPlates()
       #cform submit ─► checks ─► first error focus | success panel (nothing sent)
```

### Tech Stack at a Glance

```
Markup:    one HTML file, two views
Styling:   CSS custom properties, grid, clamp(), logical properties
Script:    vanilla JS (one IIFE), IntersectionObserver, Canvas 2D
Fonts:     Bodoni Moda · Archivo · IBM Plex Mono · IBM Plex Sans Arabic
Hosting:   GitHub Pages
```
