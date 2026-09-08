# Al Majid — Group Site Concept

An unofficial redesign concept for a large Dubai holding group's corporate site, built as a
front-end design study.

**Live:** https://keerthishree20.github.io/al-majid-concept/

## Disclaimer

This is an independent design concept. It is **not affiliated with, commissioned by, or endorsed
by Juma Al Majid Holding Group**. Company names and trademarks belong to their respective owners
and appear here only to make the concept concrete. The contact form is a front-end demo — it sends
nothing and stores nothing.

## What's in it

One self-contained `index.html`. No build step, no dependencies beyond Google Fonts.

- **Two pages from one file** — a hash router (`#/contact`) with a working contact page
- **Bilingual EN ⇄ AR** with a real `dir="rtl"` flip, built on CSS logical properties throughout
- **Seven Canvas plates** — seeded generative illustrations (skyline, street map, MEP riser
  diagram, tower elevations, route network, capital allocation) in place of photography
- **Contact form** with inline validation, `aria-invalid` states, focus management and a
  success state
- Accessible focus rings, `prefers-reduced-motion` support, responsive from 360px up

### Design system

| Role | Face |
| --- | --- |
| Display | Bodoni Moda |
| Body | Archivo |
| Figures / labels | IBM Plex Mono |
| Arabic | IBM Plex Sans Arabic |

Palette: lacquer petrol-black `#0C1113`, limestone `#EFEDE6`, aged brass `#C4913F`. Deliberately
single-theme rather than a light/dark flip.

### Swapping in photography

Every image slot is a `.plate` wrapper that owns its aspect ratio, crop and caption. Replace the
`<canvas>` with an `<img>` and it drops straight in — no CSS changes needed.

## Sources

All figures are sourced, not invented; unknown values render as "to confirm" rather than filled
with plausible numbers.

- The group's own About and Contact pages
- Wikipedia — Juma Al Majid Holding Group
- Forbes Middle East, Top 100 Arab Family Businesses

## Running it

```bash
python3 -m http.server 8000
# open http://localhost:8000
```

Or just open `index.html` in a browser.

## Licence

Code is MIT. Referenced company names, marks and figures are not covered by that licence.
