# Retrofitted Website — Design Spec
**Date:** 2026-06-22  
**Status:** Approved

---

## Overview

A multi-page static website for **Retrofitted**, a stance car culture company. The aesthetic is directly inspired by stance magazine editorial design — dark backgrounds, bold gold typography, high contrast, and grid-based layouts. Built with flat vanilla HTML, CSS, and JS (no framework, no build step).

---

## Pages

1. `index.html` — Home (magazine cover style)
2. `about.html` — About
3. `cars.html` — Cars / The Builds
4. `blog.html` — The Vlog
5. `store.html` — The Store
6. `contact.html` — Contact Us

---

## File Structure

```
RetroFittedWebsite/
├── index.html
├── about.html
├── cars.html
├── blog.html
├── store.html
├── contact.html
├── css/
│   └── style.css
├── js/
│   └── main.js
└── assets/           ← empty, ready for car images later
```

---

## Global Design System

### Color Palette
| Token       | Value     | Usage                          |
|-------------|-----------|-------------------------------|
| Background  | `#111111` | Page background               |
| Gold        | `#F0C040` | Headlines, accents, borders   |
| White       | `#FFFFFF` | Body text                     |
| Card surface| `#1C1C1C` | Cards, inner panels           |
| Divider     | `#2A2A2A` | Subtle separators             |

### Typography
- **Headlines:** Bebas Neue (Google Font) — chunky condensed, matches magazine masthead style
- **Body:** Inter (Google Font) — clean, readable on dark backgrounds

### Navigation (shared, all pages)
- Fixed top bar, `#111111` background, gold bottom border (`2px solid #F0C040`)
- Left: "RETROFITTED" in gold Bebas Neue
- Right: `ABOUT | CARS | BLOG | STORE | CONTACT` in white, active page underlined in gold
- Mobile: hamburger icon toggles a dropdown nav (handled in `main.js`)

### Footer (shared, all pages)
- Dark single row, gold top border
- Left: "RETROFITTED"
- Right: "© 2026"

---

## Page Designs

### Home — `index.html`

Magazine cover layout.

1. **Top bar:** Full-width thin strip — `CAMBER • FITMENT • STYLE` left, `ISSUE #01` right. Gold text on dark background.
2. **Nav:** Standard shared nav below top bar.
3. **Masthead hero:** Full-width section. `RETROFITTED` in very large Bebas Neue gold text spanning the width. Below it: `THE ULTIMATE AUTHORITY ON STANCE` in white spaced small-caps (`letter-spacing: 0.3em`).
4. **Editorial grid:** Two-column section below the masthead.
   - Left column: Gold `FEATURED:` label, placeholder headline (e.g. "Build of the Month"), gold arrow link to `cars.html`
   - Left column second block: `CAMBER • FITMENT • STYLE` in small gold caps
   - Right column: Pull-quote style text (`OLD SCHOOL COOL` large, `TIMELESS STYLE NEVER FADES` smaller), gold arrow link to `cars.html`
5. **Footer:** Standard shared footer.

No images on the home page — pure typographic layout.

---

### About — `about.html`

1. **Page header:** Full-width dark section. `ABOUT` in large gold Bebas Neue, thin gold underline below.
2. **Two-column section:**
   - Left: `THE STORY` heading + placeholder brand story text
   - Right: Placeholder image box (grey `#2A2A2A` fill, aspect ratio preserved, ready for a photo)
3. **Culture section:** Full-width. Gold pull-quote `CAMBER. FITMENT. STYLE.` centred. Short paragraph about brand ethos below.
4. **Footer.**

---

### Cars — `cars.html`

1. **Page header:** `THE BUILDS` in gold Bebas Neue.
2. **Build grid:** 3-column CSS grid of build cards.
   - Each card: `#1C1C1C` background, placeholder image box (16:9), car name in gold Bebas Neue, `Year · Make · Model` in small white text, italic tagline in white.
   - 6 placeholder cards by default (2 rows of 3).
   - Card hover: gold border appears, slight lift (`transform: translateY(-4px)`).
3. **Footer.**

Car images will be added later — placeholder boxes use `#2A2A2A` background with a centred "PHOTO COMING SOON" label.

---

### Blog / Vlog — `blog.html`

1. **Page header:** `THE VLOG` in gold Bebas Neue.
2. **Video list:** Vertical stack of horizontal video cards.
   - Each card: `#1C1C1C` background, two columns.
   - Left: 16:9 thumbnail placeholder box with a centred gold play icon (`▶`).
   - Right: Episode title in gold Bebas Neue, short description in white Inter, `→ Watch` link in gold.
   - 4 placeholder video cards.
3. **Footer.**

---

### Store — `store.html`

1. **Page header:** `THE STORE` in gold Bebas Neue. Subheading: `APPAREL & ACCESSORIES` in white small-caps.
2. **Product grid:** 4-column CSS grid.
   - Each product card: `#1C1C1C` background, square placeholder image box, item name in white, price as `$--` in gold.
   - 8 placeholder cards by default (2 rows of 4).
   - Card hover: gold border, slight lift.
3. **Footer.**

---

### Contact — `contact.html`

1. **Page header:** `CONTACT` in gold Bebas Neue.
2. **Form:** Centred, max-width ~600px.
   - Fields: Name, Email, Message (textarea).
   - All inputs: dark background `#1C1C1C`, gold border, white text, no border-radius (sharp editorial feel).
   - Submit: gold background button, dark text, `SEND IT →` label, full width.
3. **Social row:** Thin divider, then `FOLLOW US` label + icon links for Instagram, YouTube, TikTok (placeholder `#` hrefs).
4. **Footer.**

---

## Behaviour (main.js)

- Mobile hamburger toggle: adds/removes `.nav-open` class on `<body>`, nav links slide down.
- Active nav link: on page load, compares `window.location.pathname` to each nav link's `href`, adds `.active` class to the matching link.
- No other JS required for the layout phase.

---

## Out of Scope (this phase)

- Real car images (added later via `assets/`)
- Real product listings or e-commerce functionality
- Real video embeds (YouTube iframes added when vlog content is ready)
- Real contact form submission (backend/API)
- Real social media links
