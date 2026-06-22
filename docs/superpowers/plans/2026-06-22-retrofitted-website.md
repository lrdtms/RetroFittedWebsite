# Retrofitted Website Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build a 6-page static HTML/CSS/JS website for Retrofitted with a dark stance-magazine editorial aesthetic.

**Architecture:** Flat vanilla files — one HTML file per page, a single shared `css/style.css`, and a single `js/main.js` for mobile nav and active-link logic. No build step, no framework. Open any HTML file directly in a browser to preview.

**Tech Stack:** HTML5, CSS3 (custom properties, Grid, Flexbox), Vanilla ES6 JS, Google Fonts (Bebas Neue + Inter via CSS @import)

## Global Constraints

- Background: `#111111`, Gold: `#F0C040`, White: `#FFFFFF`, Card: `#1C1C1C`, Divider: `#2A2A2A`
- Headlines: Bebas Neue. Body: Inter.
- Nav height: 60px (fixed). All pages get `padding-top: 60px` via `.page-wrapper`.
- No border-radius anywhere — sharp editorial aesthetic throughout.
- No images added yet — use `.img-placeholder` (grey `#2A2A2A` box with faint label).
- No form backend — contact form has no action attribute.

---

## File Map

| File | Responsibility |
|------|---------------|
| `css/style.css` | All styles: variables, reset, nav, footer, all page layouts, responsive |
| `js/main.js` | Mobile nav toggle + active link detection |
| `index.html` | Home — magazine cover (top bar, masthead, editorial grid) |
| `about.html` | About — brand story + image placeholder + culture section |
| `cars.html` | Cars — 3-column build card grid |
| `blog.html` | Vlog — horizontal video card list |
| `store.html` | Store — 4-column product card grid |
| `contact.html` | Contact — form + social links |
| `assets/` | Empty directory, ready for car images |

---

## Task 1: Scaffold, Global CSS, JS, and Home Page

**Files:**
- Create: `css/style.css`
- Create: `js/main.js`
- Create: `index.html`
- Create: `assets/.gitkeep`

**Interfaces:**
- Produces: All CSS custom properties, nav/footer HTML structure, `.page-wrapper`, `.img-placeholder`, `.editorial-link`, `.page-header` — used by every subsequent task.

---

- [ ] **Step 1: Create the directory structure**

```bash
mkdir -p css js assets
```

Verify `css/`, `js/`, `assets/` folders exist in the project root.

---

- [ ] **Step 2: Create `css/style.css` with the complete stylesheet**

```css
/* ===== FONTS ===== */
@import url('https://fonts.googleapis.com/css2?family=Bebas+Neue&family=Inter:wght@400;500;600&display=swap');

/* ===== VARIABLES ===== */
:root {
  --bg:       #111111;
  --gold:     #F0C040;
  --white:    #FFFFFF;
  --card:     #1C1C1C;
  --divider:  #2A2A2A;
  --font-headline: 'Bebas Neue', cursive;
  --font-body:     'Inter', sans-serif;
  --nav-height: 60px;
}

/* ===== RESET ===== */
*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
html { scroll-behavior: smooth; }
body { background: var(--bg); color: var(--white); font-family: var(--font-body); line-height: 1.6; }
a { text-decoration: none; }
img { display: block; max-width: 100%; }
ul { list-style: none; }

/* ===== NAV ===== */
nav {
  position: fixed;
  top: 0; left: 0; right: 0;
  z-index: 100;
  background: var(--bg);
  border-bottom: 2px solid var(--gold);
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 0 2rem;
  height: var(--nav-height);
}

.nav-brand {
  font-family: var(--font-headline);
  font-size: 1.8rem;
  color: var(--gold);
  letter-spacing: 0.05em;
}

.nav-links {
  display: flex;
  gap: 2rem;
}

.nav-links a {
  color: var(--white);
  font-size: 0.78rem;
  font-weight: 600;
  letter-spacing: 0.12em;
  text-transform: uppercase;
  padding-bottom: 2px;
  transition: color 0.2s;
}

.nav-links a:hover,
.nav-links a.active {
  color: var(--gold);
  border-bottom: 2px solid var(--gold);
}

.nav-toggle {
  display: none;
  flex-direction: column;
  gap: 5px;
  cursor: pointer;
  background: none;
  border: none;
  padding: 4px;
}

.nav-toggle span {
  display: block;
  width: 24px;
  height: 2px;
  background: var(--white);
}

/* ===== PAGE WRAPPER ===== */
.page-wrapper {
  padding-top: var(--nav-height);
  min-height: calc(100vh - var(--nav-height));
}

/* ===== PAGE HEADER (inner pages) ===== */
.page-header {
  padding: 4rem 2rem 2rem;
  border-bottom: 1px solid var(--divider);
}

.page-header h1 {
  font-family: var(--font-headline);
  color: var(--gold);
  font-size: clamp(3rem, 8vw, 6rem);
  letter-spacing: 0.02em;
  line-height: 1;
}

.page-header-rule {
  width: 80px;
  height: 3px;
  background: var(--gold);
  margin-top: 0.75rem;
}

/* ===== FOOTER ===== */
footer {
  border-top: 2px solid var(--gold);
  padding: 1.5rem 2rem;
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-top: 4rem;
}

.footer-brand {
  font-family: var(--font-headline);
  color: var(--gold);
  font-size: 1.4rem;
  letter-spacing: 0.05em;
}

.footer-copy {
  font-size: 0.8rem;
  color: var(--white);
  opacity: 0.5;
}

/* ===== UTILITIES ===== */
.img-placeholder {
  background: var(--divider);
  display: flex;
  align-items: center;
  justify-content: center;
  color: rgba(255, 255, 255, 0.2);
  font-size: 0.6rem;
  letter-spacing: 0.2em;
  text-transform: uppercase;
  font-family: var(--font-body);
}

.editorial-label {
  font-size: 0.68rem;
  font-weight: 600;
  letter-spacing: 0.22em;
  text-transform: uppercase;
  color: var(--gold);
  display: block;
  margin-bottom: 0.5rem;
}

.editorial-link {
  display: inline-block;
  color: var(--gold);
  font-size: 0.8rem;
  font-weight: 600;
  letter-spacing: 0.12em;
  text-transform: uppercase;
  margin-top: 1rem;
  transition: opacity 0.2s;
}

.editorial-link:hover { opacity: 0.65; }

/* ===== HOME PAGE ===== */
.top-bar {
  background: var(--bg);
  border-bottom: 1px solid var(--divider);
  color: var(--gold);
  font-size: 0.62rem;
  letter-spacing: 0.22em;
  text-transform: uppercase;
  padding: 0.45rem 2rem;
  display: flex;
  justify-content: space-between;
  font-weight: 600;
}

.home-hero {
  padding: 5rem 2rem 4rem;
  text-align: center;
  border-bottom: 1px solid var(--divider);
}

.home-masthead {
  font-family: var(--font-headline);
  color: var(--gold);
  font-size: clamp(5rem, 18vw, 14rem);
  letter-spacing: 0.01em;
  line-height: 0.9;
}

.home-subtitle {
  font-size: clamp(0.6rem, 1.4vw, 0.8rem);
  letter-spacing: 0.45em;
  text-transform: uppercase;
  color: var(--white);
  margin-top: 1.5rem;
  opacity: 0.75;
}

.home-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  border-bottom: 1px solid var(--divider);
}

.home-grid-left {
  border-right: 1px solid var(--divider);
}

.home-editorial-block {
  padding: 2.5rem 2rem;
  border-bottom: 1px solid var(--divider);
}

.home-editorial-block:last-child { border-bottom: none; }

.editorial-headline {
  font-family: var(--font-headline);
  color: var(--white);
  font-size: clamp(1.8rem, 3vw, 2.6rem);
  letter-spacing: 0.02em;
  line-height: 1.1;
}

.home-grid-right {
  padding: 2.5rem 2rem;
  display: flex;
  flex-direction: column;
  justify-content: center;
}

.pull-quote-large {
  font-family: var(--font-headline);
  color: var(--white);
  font-size: clamp(2.5rem, 5vw, 4.5rem);
  letter-spacing: 0.02em;
  line-height: 1;
}

.pull-quote-small {
  font-size: clamp(0.65rem, 1.1vw, 0.8rem);
  letter-spacing: 0.2em;
  text-transform: uppercase;
  color: var(--gold);
  margin-top: 0.75rem;
  line-height: 1.8;
}

/* ===== ABOUT PAGE ===== */
.about-content {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 3rem;
  padding: 3rem 2rem;
  border-bottom: 1px solid var(--divider);
}

.about-text h2 {
  font-family: var(--font-headline);
  color: var(--gold);
  font-size: 2rem;
  letter-spacing: 0.05em;
  margin-bottom: 1rem;
}

.about-text p {
  color: rgba(255, 255, 255, 0.75);
  line-height: 1.9;
  font-size: 0.95rem;
}

.about-img {
  aspect-ratio: 4 / 3;
  width: 100%;
}

.about-culture {
  padding: 4rem 2rem;
  text-align: center;
}

.about-culture .pull-quote-large {
  color: var(--gold);
  font-size: clamp(1.5rem, 4vw, 3rem);
  letter-spacing: 0.18em;
}

.about-culture p {
  max-width: 580px;
  margin: 1.5rem auto 0;
  color: rgba(255, 255, 255, 0.7);
  line-height: 1.9;
  font-size: 0.95rem;
}

/* ===== CARS PAGE ===== */
.builds-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 1.5rem;
  padding: 3rem 2rem;
}

.build-card {
  background: var(--card);
  transition: transform 0.2s, box-shadow 0.2s;
  cursor: pointer;
}

.build-card:hover {
  transform: translateY(-4px);
  box-shadow: 0 0 0 2px var(--gold);
}

.build-card-img {
  aspect-ratio: 16 / 9;
  width: 100%;
}

.build-card-body { padding: 1rem 1.25rem 1.25rem; }

.build-card-name {
  font-family: var(--font-headline);
  color: var(--gold);
  font-size: 1.4rem;
  letter-spacing: 0.04em;
}

.build-card-meta {
  font-size: 0.7rem;
  letter-spacing: 0.12em;
  text-transform: uppercase;
  color: rgba(255, 255, 255, 0.45);
  margin-top: 0.3rem;
}

.build-card-tagline {
  font-size: 0.85rem;
  color: rgba(255, 255, 255, 0.7);
  font-style: italic;
  margin-top: 0.5rem;
}

/* ===== VLOG PAGE ===== */
.vlog-list {
  padding: 3rem 2rem;
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
}

.vlog-card {
  background: var(--card);
  display: grid;
  grid-template-columns: 320px 1fr;
}

.vlog-thumb {
  aspect-ratio: 16 / 9;
  position: relative;
}

.vlog-play {
  position: absolute;
  inset: 0;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 2.5rem;
  color: var(--gold);
}

.vlog-info {
  padding: 1.5rem 2rem;
  display: flex;
  flex-direction: column;
  justify-content: center;
}

.vlog-title {
  font-family: var(--font-headline);
  color: var(--gold);
  font-size: 1.6rem;
  letter-spacing: 0.03em;
  line-height: 1.1;
}

.vlog-desc {
  font-size: 0.88rem;
  color: rgba(255, 255, 255, 0.65);
  margin-top: 0.6rem;
  line-height: 1.75;
}

/* ===== STORE PAGE ===== */
.store-sub {
  display: block;
  font-size: 0.7rem;
  letter-spacing: 0.28em;
  text-transform: uppercase;
  color: rgba(255, 255, 255, 0.4);
  margin-top: 0.5rem;
}

.product-grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 1.25rem;
  padding: 3rem 2rem;
}

.product-card {
  background: var(--card);
  transition: transform 0.2s, box-shadow 0.2s;
  cursor: pointer;
}

.product-card:hover {
  transform: translateY(-4px);
  box-shadow: 0 0 0 2px var(--gold);
}

.product-card-img {
  aspect-ratio: 1 / 1;
  width: 100%;
}

.product-card-body { padding: 0.75rem 1rem 1rem; }

.product-card-name {
  font-size: 0.8rem;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 0.1em;
  color: var(--white);
}

.product-card-price {
  font-family: var(--font-headline);
  color: var(--gold);
  font-size: 1.1rem;
  margin-top: 0.3rem;
  letter-spacing: 0.05em;
}

/* ===== CONTACT PAGE ===== */
.contact-content {
  padding: 3rem 2rem;
  max-width: 640px;
  margin: 0 auto;
}

.contact-form {
  display: flex;
  flex-direction: column;
  gap: 1.25rem;
}

.form-group {
  display: flex;
  flex-direction: column;
  gap: 0.4rem;
}

.form-group label {
  font-size: 0.68rem;
  font-weight: 600;
  letter-spacing: 0.22em;
  text-transform: uppercase;
  color: rgba(255, 255, 255, 0.5);
}

.form-group input,
.form-group textarea {
  background: var(--card);
  border: 1px solid var(--divider);
  color: var(--white);
  font-family: var(--font-body);
  font-size: 0.95rem;
  padding: 0.75rem 1rem;
  outline: none;
  transition: border-color 0.2s;
  resize: vertical;
}

.form-group input:focus,
.form-group textarea:focus { border-color: var(--gold); }

.form-submit {
  background: var(--gold);
  color: var(--bg);
  font-family: var(--font-body);
  font-size: 0.82rem;
  font-weight: 700;
  letter-spacing: 0.18em;
  text-transform: uppercase;
  border: none;
  padding: 1rem;
  cursor: pointer;
  transition: opacity 0.2s;
  width: 100%;
  margin-top: 0.5rem;
}

.form-submit:hover { opacity: 0.8; }

.contact-social {
  margin-top: 3rem;
  padding-top: 2rem;
  border-top: 1px solid var(--divider);
  text-align: center;
}

.social-label {
  font-size: 0.65rem;
  letter-spacing: 0.28em;
  text-transform: uppercase;
  color: rgba(255, 255, 255, 0.35);
  margin-bottom: 1rem;
}

.social-links {
  display: flex;
  justify-content: center;
  gap: 2.5rem;
}

.social-links a {
  font-size: 0.75rem;
  font-weight: 600;
  letter-spacing: 0.18em;
  text-transform: uppercase;
  color: var(--gold);
  transition: opacity 0.2s;
}

.social-links a:hover { opacity: 0.65; }

/* ===== RESPONSIVE ===== */
@media (max-width: 900px) {
  .builds-grid    { grid-template-columns: repeat(2, 1fr); }
  .product-grid   { grid-template-columns: repeat(2, 1fr); }
  .vlog-card      { grid-template-columns: 240px 1fr; }
}

@media (max-width: 768px) {
  .nav-links {
    display: none;
    flex-direction: column;
    position: absolute;
    top: var(--nav-height);
    left: 0; right: 0;
    background: var(--bg);
    border-bottom: 2px solid var(--gold);
    padding: 1rem 2rem;
    gap: 1.25rem;
  }
  .nav-links.open  { display: flex; }
  .nav-toggle      { display: flex; }
  .home-grid       { grid-template-columns: 1fr; }
  .home-grid-left  { border-right: none; }
  .about-content   { grid-template-columns: 1fr; }
  .builds-grid     { grid-template-columns: 1fr; }
  .vlog-card       { grid-template-columns: 1fr; }
}

@media (max-width: 480px) {
  .product-grid { grid-template-columns: repeat(2, 1fr); }
}
```

---

- [ ] **Step 3: Create `js/main.js`**

```javascript
const toggle = document.querySelector('.nav-toggle');
const navLinks = document.querySelector('.nav-links');

if (toggle && navLinks) {
  toggle.addEventListener('click', () => navLinks.classList.toggle('open'));
}

const currentFile = window.location.pathname.split('/').pop() || 'index.html';
document.querySelectorAll('.nav-links a').forEach(link => {
  if (link.getAttribute('href') === currentFile) link.classList.add('active');
});
```

---

- [ ] **Step 4: Create `index.html` (Home page)**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Retrofitted</title>
  <link rel="stylesheet" href="css/style.css">
</head>
<body>

  <nav>
    <a href="index.html" class="nav-brand">RETROFITTED</a>
    <button class="nav-toggle" aria-label="Toggle navigation">
      <span></span><span></span><span></span>
    </button>
    <ul class="nav-links">
      <li><a href="about.html">About</a></li>
      <li><a href="cars.html">Cars</a></li>
      <li><a href="blog.html">Blog</a></li>
      <li><a href="store.html">Store</a></li>
      <li><a href="contact.html">Contact</a></li>
    </ul>
  </nav>

  <div class="page-wrapper">

    <div class="top-bar">
      <span>Camber &bull; Fitment &bull; Style</span>
      <span>Issue #01</span>
    </div>

    <section class="home-hero">
      <h1 class="home-masthead">RETROFITTED</h1>
      <p class="home-subtitle">The Ultimate Authority on Stance</p>
    </section>

    <section class="home-grid">
      <div class="home-grid-left">
        <div class="home-editorial-block">
          <span class="editorial-label">Featured:</span>
          <h2 class="editorial-headline">Build of<br>the Month</h2>
          <a href="cars.html" class="editorial-link">&rarr; Explore the Cars</a>
        </div>
        <div class="home-editorial-block">
          <span class="editorial-label small">Camber &bull; Fitment &bull; Style</span>
        </div>
      </div>
      <div class="home-grid-right">
        <h2 class="pull-quote-large">Old School<br>Cool</h2>
        <p class="pull-quote-small">Timeless Style<br>Never Fades</p>
        <a href="cars.html" class="editorial-link">&rarr; View the Builds</a>
      </div>
    </section>

  </div>

  <footer>
    <span class="footer-brand">RETROFITTED</span>
    <span class="footer-copy">&copy; 2026</span>
  </footer>

  <script src="js/main.js"></script>
</body>
</html>
```

---

- [ ] **Step 5: Create `assets/.gitkeep`**

Create an empty file at `assets/.gitkeep` so the folder is tracked by git.

---

- [ ] **Step 6: Verify in browser**

Open `index.html` in a browser. Check:
- Fixed dark nav with gold bottom border and "RETROFITTED" in gold on the left
- Nav links right-aligned in white
- Thin top-bar strip below nav with "CAMBER • FITMENT • STYLE" and "ISSUE #01"
- Massive gold "RETROFITTED" masthead filling the width
- "THE ULTIMATE AUTHORITY ON STANCE" subtitle in small white caps below
- Two-column editorial grid: left has "FEATURED:" label + headline + gold arrow link; right has pull quotes + link
- Gold footer with brand name left and copyright right
- Hamburger appears on mobile (resize browser to < 768px) and clicking it opens the nav links

---

- [ ] **Step 7: Commit**

```bash
git add css/style.css js/main.js index.html assets/.gitkeep
git commit -m "feat: scaffold global CSS, JS, and home page"
```

---

## Task 2: About Page

**Files:**
- Create: `about.html`

**Interfaces:**
- Consumes: `.page-wrapper`, `.page-header`, `.page-header-rule`, `.img-placeholder`, `.pull-quote-large`, `nav`, `footer` from Task 1
- Produces: `about.html` (no new shared interfaces)

---

- [ ] **Step 1: Create `about.html`**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>About — Retrofitted</title>
  <link rel="stylesheet" href="css/style.css">
</head>
<body>

  <nav>
    <a href="index.html" class="nav-brand">RETROFITTED</a>
    <button class="nav-toggle" aria-label="Toggle navigation">
      <span></span><span></span><span></span>
    </button>
    <ul class="nav-links">
      <li><a href="about.html">About</a></li>
      <li><a href="cars.html">Cars</a></li>
      <li><a href="blog.html">Blog</a></li>
      <li><a href="store.html">Store</a></li>
      <li><a href="contact.html">Contact</a></li>
    </ul>
  </nav>

  <div class="page-wrapper">

    <div class="page-header">
      <h1>About</h1>
      <div class="page-header-rule"></div>
    </div>

    <div class="about-content">
      <div class="about-text">
        <h2>The Story</h2>
        <p>
          Retrofitted was born from a simple belief: that the cars we drive should
          reflect the people we are. Founded on a passion for fitment, camber, and
          the art of stance, we exist at the intersection of old-school culture and
          modern craftsmanship.
        </p>
        <p style="margin-top: 1rem;">
          Every build tells a story. Every stance is a statement. We are Retrofitted —
          and this is our culture.
        </p>
      </div>
      <div class="about-img img-placeholder">Photo Coming Soon</div>
    </div>

    <div class="about-culture">
      <h2 class="pull-quote-large">Camber. Fitment. Style.</h2>
      <p>
        We don't just build cars — we build identities. Retrofitted is a community
        of drivers, builders, and dreamers who believe that how low you go says
        everything about who you are. Culture. Passion. Dedication.
      </p>
    </div>

  </div>

  <footer>
    <span class="footer-brand">RETROFITTED</span>
    <span class="footer-copy">&copy; 2026</span>
  </footer>

  <script src="js/main.js"></script>
</body>
</html>
```

---

- [ ] **Step 2: Verify in browser**

Open `about.html`. Check:
- "ABOUT" link in nav is gold and underlined (active state)
- Gold page title "About" with gold rule beneath
- Two-column layout: text left, grey placeholder image right
- On mobile (< 768px): columns stack vertically
- Culture section centred with gold pull quote
- Footer visible

---

- [ ] **Step 3: Commit**

```bash
git add about.html
git commit -m "feat: add about page"
```

---

## Task 3: Cars Page

**Files:**
- Create: `cars.html`

**Interfaces:**
- Consumes: `.page-wrapper`, `.page-header`, `.page-header-rule`, `.img-placeholder`, `nav`, `footer` from Task 1
- Produces: `cars.html` (no new shared interfaces)

---

- [ ] **Step 1: Create `cars.html`**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Cars — Retrofitted</title>
  <link rel="stylesheet" href="css/style.css">
</head>
<body>

  <nav>
    <a href="index.html" class="nav-brand">RETROFITTED</a>
    <button class="nav-toggle" aria-label="Toggle navigation">
      <span></span><span></span><span></span>
    </button>
    <ul class="nav-links">
      <li><a href="about.html">About</a></li>
      <li><a href="cars.html">Cars</a></li>
      <li><a href="blog.html">Blog</a></li>
      <li><a href="store.html">Store</a></li>
      <li><a href="contact.html">Contact</a></li>
    </ul>
  </nav>

  <div class="page-wrapper">

    <div class="page-header">
      <h1>The Builds</h1>
      <div class="page-header-rule"></div>
    </div>

    <div class="builds-grid">

      <div class="build-card">
        <div class="build-card-img img-placeholder">Photo Coming Soon</div>
        <div class="build-card-body">
          <div class="build-card-name">Build 01</div>
          <div class="build-card-meta">1990 &middot; Nissan &middot; 240SX</div>
          <div class="build-card-tagline">"Slammed and sorted."</div>
        </div>
      </div>

      <div class="build-card">
        <div class="build-card-img img-placeholder">Photo Coming Soon</div>
        <div class="build-card-body">
          <div class="build-card-name">Build 02</div>
          <div class="build-card-meta">1995 &middot; Toyota &middot; Chaser</div>
          <div class="build-card-tagline">"Old school cool, new school fit."</div>
        </div>
      </div>

      <div class="build-card">
        <div class="build-card-img img-placeholder">Photo Coming Soon</div>
        <div class="build-card-body">
          <div class="build-card-name">Build 03</div>
          <div class="build-card-meta">2002 &middot; Honda &middot; Civic</div>
          <div class="build-card-tagline">"Fitment is everything."</div>
        </div>
      </div>

      <div class="build-card">
        <div class="build-card-img img-placeholder">Photo Coming Soon</div>
        <div class="build-card-body">
          <div class="build-card-name">Build 04</div>
          <div class="build-card-meta">1988 &middot; BMW &middot; E30</div>
          <div class="build-card-tagline">"Timeless iron."</div>
        </div>
      </div>

      <div class="build-card">
        <div class="build-card-img img-placeholder">Photo Coming Soon</div>
        <div class="build-card-body">
          <div class="build-card-name">Build 05</div>
          <div class="build-card-meta">1997 &middot; Mazda &middot; RX-7</div>
          <div class="build-card-tagline">"Rotary culture runs deep."</div>
        </div>
      </div>

      <div class="build-card">
        <div class="build-card-img img-placeholder">Photo Coming Soon</div>
        <div class="build-card-body">
          <div class="build-card-name">Build 06</div>
          <div class="build-card-meta">1993 &middot; Mitsubishi &middot; Galant VR-4</div>
          <div class="build-card-tagline">"Built different."</div>
        </div>
      </div>

    </div>

  </div>

  <footer>
    <span class="footer-brand">RETROFITTED</span>
    <span class="footer-copy">&copy; 2026</span>
  </footer>

  <script src="js/main.js"></script>
</body>
</html>
```

---

- [ ] **Step 2: Verify in browser**

Open `cars.html`. Check:
- "CARS" nav link is active (gold + underline)
- "THE BUILDS" page header in gold
- 6 cards in a 3-column grid, each with grey 16:9 placeholder image, gold car name, faint meta text, italic tagline
- Hover a card: it lifts 4px and gets a 2px gold border
- At 900px wide: grid collapses to 2 columns
- At 768px wide: grid collapses to 1 column

---

- [ ] **Step 3: Commit**

```bash
git add cars.html
git commit -m "feat: add cars / builds page"
```

---

## Task 4: Vlog Page

**Files:**
- Create: `blog.html`

**Interfaces:**
- Consumes: `.page-wrapper`, `.page-header`, `.page-header-rule`, `.img-placeholder`, `.editorial-link`, `nav`, `footer` from Task 1
- Produces: `blog.html` (no new shared interfaces)

---

- [ ] **Step 1: Create `blog.html`**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>The Vlog — Retrofitted</title>
  <link rel="stylesheet" href="css/style.css">
</head>
<body>

  <nav>
    <a href="index.html" class="nav-brand">RETROFITTED</a>
    <button class="nav-toggle" aria-label="Toggle navigation">
      <span></span><span></span><span></span>
    </button>
    <ul class="nav-links">
      <li><a href="about.html">About</a></li>
      <li><a href="cars.html">Cars</a></li>
      <li><a href="blog.html">Blog</a></li>
      <li><a href="store.html">Store</a></li>
      <li><a href="contact.html">Contact</a></li>
    </ul>
  </nav>

  <div class="page-wrapper">

    <div class="page-header">
      <h1>The Vlog</h1>
      <div class="page-header-rule"></div>
    </div>

    <div class="vlog-list">

      <div class="vlog-card">
        <div class="vlog-thumb img-placeholder">
          <span class="vlog-play">&#9654;</span>
        </div>
        <div class="vlog-info">
          <div class="vlog-title">Episode 01 — The Beginning</div>
          <p class="vlog-desc">How it all started. We take you behind the scenes of the first Retrofitted build and what inspired the whole company.</p>
          <a href="#" class="editorial-link">&rarr; Watch</a>
        </div>
      </div>

      <div class="vlog-card">
        <div class="vlog-thumb img-placeholder">
          <span class="vlog-play">&#9654;</span>
        </div>
        <div class="vlog-info">
          <div class="vlog-title">Episode 02 — Fitment Day</div>
          <p class="vlog-desc">Wheel fitment is an art. Watch us dial in the perfect offset and stance on the 240SX build from start to finish.</p>
          <a href="#" class="editorial-link">&rarr; Watch</a>
        </div>
      </div>

      <div class="vlog-card">
        <div class="vlog-thumb img-placeholder">
          <span class="vlog-play">&#9654;</span>
        </div>
        <div class="vlog-info">
          <div class="vlog-title">Episode 03 — Show Day</div>
          <p class="vlog-desc">We hit a local meet and show you what the stance scene looks like on the ground. Builds, culture, and good vibes.</p>
          <a href="#" class="editorial-link">&rarr; Watch</a>
        </div>
      </div>

      <div class="vlog-card">
        <div class="vlog-thumb img-placeholder">
          <span class="vlog-play">&#9654;</span>
        </div>
        <div class="vlog-info">
          <div class="vlog-title">Episode 04 — Parts Run</div>
          <p class="vlog-desc">Tracking down hard-to-find JDM parts. A day in the life of sourcing the pieces that make a build truly unique.</p>
          <a href="#" class="editorial-link">&rarr; Watch</a>
        </div>
      </div>

    </div>

  </div>

  <footer>
    <span class="footer-brand">RETROFITTED</span>
    <span class="footer-copy">&copy; 2026</span>
  </footer>

  <script src="js/main.js"></script>
</body>
</html>
```

---

- [ ] **Step 2: Verify in browser**

Open `blog.html`. Check:
- "BLOG" nav link is active
- "THE VLOG" page header in gold
- 4 horizontal video cards, each with grey 16:9 placeholder left and gold play triangle centred on it
- Right side: gold title, grey description, gold "→ Watch" link
- At 768px: vlog card stacks vertically (thumbnail on top, info below)

---

- [ ] **Step 3: Commit**

```bash
git add blog.html
git commit -m "feat: add vlog page"
```

---

## Task 5: Store Page

**Files:**
- Create: `store.html`

**Interfaces:**
- Consumes: `.page-wrapper`, `.page-header`, `.page-header-rule`, `.img-placeholder`, `nav`, `footer` from Task 1
- Produces: `store.html` (no new shared interfaces)

---

- [ ] **Step 1: Create `store.html`**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Store — Retrofitted</title>
  <link rel="stylesheet" href="css/style.css">
</head>
<body>

  <nav>
    <a href="index.html" class="nav-brand">RETROFITTED</a>
    <button class="nav-toggle" aria-label="Toggle navigation">
      <span></span><span></span><span></span>
    </button>
    <ul class="nav-links">
      <li><a href="about.html">About</a></li>
      <li><a href="cars.html">Cars</a></li>
      <li><a href="blog.html">Blog</a></li>
      <li><a href="store.html">Store</a></li>
      <li><a href="contact.html">Contact</a></li>
    </ul>
  </nav>

  <div class="page-wrapper">

    <div class="page-header">
      <h1>The Store</h1>
      <span class="store-sub">Apparel &amp; Accessories</span>
      <div class="page-header-rule"></div>
    </div>

    <div class="product-grid">

      <div class="product-card">
        <div class="product-card-img img-placeholder">Photo Coming Soon</div>
        <div class="product-card-body">
          <div class="product-card-name">Retrofitted Tee</div>
          <div class="product-card-price">$--</div>
        </div>
      </div>

      <div class="product-card">
        <div class="product-card-img img-placeholder">Photo Coming Soon</div>
        <div class="product-card-body">
          <div class="product-card-name">Stance Cap</div>
          <div class="product-card-price">$--</div>
        </div>
      </div>

      <div class="product-card">
        <div class="product-card-img img-placeholder">Photo Coming Soon</div>
        <div class="product-card-body">
          <div class="product-card-name">Camber Hoodie</div>
          <div class="product-card-price">$--</div>
        </div>
      </div>

      <div class="product-card">
        <div class="product-card-img img-placeholder">Photo Coming Soon</div>
        <div class="product-card-body">
          <div class="product-card-name">Fitment Sticker Pack</div>
          <div class="product-card-price">$--</div>
        </div>
      </div>

      <div class="product-card">
        <div class="product-card-img img-placeholder">Photo Coming Soon</div>
        <div class="product-card-body">
          <div class="product-card-name">Low Life Tee</div>
          <div class="product-card-price">$--</div>
        </div>
      </div>

      <div class="product-card">
        <div class="product-card-img img-placeholder">Photo Coming Soon</div>
        <div class="product-card-body">
          <div class="product-card-name">Retrofitted Keychain</div>
          <div class="product-card-price">$--</div>
        </div>
      </div>

      <div class="product-card">
        <div class="product-card-img img-placeholder">Photo Coming Soon</div>
        <div class="product-card-body">
          <div class="product-card-name">Old School Longsleeve</div>
          <div class="product-card-price">$--</div>
        </div>
      </div>

      <div class="product-card">
        <div class="product-card-img img-placeholder">Photo Coming Soon</div>
        <div class="product-card-body">
          <div class="product-card-name">Air Ride Patch</div>
          <div class="product-card-price">$--</div>
        </div>
      </div>

    </div>

  </div>

  <footer>
    <span class="footer-brand">RETROFITTED</span>
    <span class="footer-copy">&copy; 2026</span>
  </footer>

  <script src="js/main.js"></script>
</body>
</html>
```

---

- [ ] **Step 2: Verify in browser**

Open `store.html`. Check:
- "STORE" nav link is active
- "THE STORE" title in gold, "APPAREL & ACCESSORIES" subtitle below in faint white
- 8 product cards in a 4-column grid, each with square grey placeholder, white item name, gold `$--` price
- Hover a card: lifts 4px, 2px gold border appears
- At 900px: 2-column grid
- At 480px: 2-column grid (still 2 on smallest screens)

---

- [ ] **Step 3: Commit**

```bash
git add store.html
git commit -m "feat: add store page"
```

---

## Task 6: Contact Page

**Files:**
- Create: `contact.html`

**Interfaces:**
- Consumes: `.page-wrapper`, `.page-header`, `.page-header-rule`, `nav`, `footer` from Task 1
- Produces: `contact.html` (no new shared interfaces)

---

- [ ] **Step 1: Create `contact.html`**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Contact — Retrofitted</title>
  <link rel="stylesheet" href="css/style.css">
</head>
<body>

  <nav>
    <a href="index.html" class="nav-brand">RETROFITTED</a>
    <button class="nav-toggle" aria-label="Toggle navigation">
      <span></span><span></span><span></span>
    </button>
    <ul class="nav-links">
      <li><a href="about.html">About</a></li>
      <li><a href="cars.html">Cars</a></li>
      <li><a href="blog.html">Blog</a></li>
      <li><a href="store.html">Store</a></li>
      <li><a href="contact.html">Contact</a></li>
    </ul>
  </nav>

  <div class="page-wrapper">

    <div class="page-header">
      <h1>Contact</h1>
      <div class="page-header-rule"></div>
    </div>

    <div class="contact-content">

      <form class="contact-form">
        <div class="form-group">
          <label for="name">Name</label>
          <input type="text" id="name" name="name" placeholder="Your name" autocomplete="name">
        </div>
        <div class="form-group">
          <label for="email">Email</label>
          <input type="email" id="email" name="email" placeholder="your@email.com" autocomplete="email">
        </div>
        <div class="form-group">
          <label for="message">Message</label>
          <textarea id="message" name="message" rows="6" placeholder="What's on your mind?"></textarea>
        </div>
        <button type="submit" class="form-submit">Send It &rarr;</button>
      </form>

      <div class="contact-social">
        <p class="social-label">Follow Us</p>
        <div class="social-links">
          <a href="#">Instagram</a>
          <a href="#">YouTube</a>
          <a href="#">TikTok</a>
        </div>
      </div>

    </div>

  </div>

  <footer>
    <span class="footer-brand">RETROFITTED</span>
    <span class="footer-copy">&copy; 2026</span>
  </footer>

  <script src="js/main.js"></script>
</body>
</html>
```

---

- [ ] **Step 2: Verify in browser**

Open `contact.html`. Check:
- "CONTACT" nav link is active
- "CONTACT" page header in gold with gold rule
- Form centred, max ~640px width
- Dark card-coloured input fields with divider border, gold border on focus
- "SEND IT →" button is full-width, gold background, dark text
- Social row below a divider: "FOLLOW US" faint label then Instagram / YouTube / TikTok links in gold
- Footer at bottom

---

- [ ] **Step 3: Final cross-page check**

Click through every nav link from every page and verify:
- The active link is always correct (gold + underline)
- The nav hamburger works on mobile for every page
- Footer is consistent across all pages
- No page shows a white flash on load (all backgrounds are dark)

---

- [ ] **Step 4: Commit**

```bash
git add contact.html
git commit -m "feat: add contact page"
```
