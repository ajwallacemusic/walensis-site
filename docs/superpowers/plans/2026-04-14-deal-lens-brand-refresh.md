# Deal Lens Brand Refresh Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Transform the Deal Lens website from a minimal light-theme text site to a bold Indigo Night dark brand, and create three Chrome Web Store promotional image HTML templates.

**Architecture:** The site is a static Astro site with a single layout, one CSS file, and page-level `.astro` files. All changes are CSS variable swaps, HTML restructuring, and new standalone HTML files for promo screenshots. No JS, no build changes, no new dependencies.

**Tech Stack:** Astro 5, HTML, CSS (custom properties), SVG

**Spec:** `docs/superpowers/specs/2026-04-14-deal-lens-brand-refresh-design.md`

---

### Task 1: Update CSS custom properties and base styles for Indigo Night palette

**Files:**
- Modify: `src/styles/global.css:1-15` (CSS custom properties)
- Modify: `src/styles/global.css:21-28` (html element styles)
- Modify: `src/styles/global.css:45-66` (heading styles)
- Modify: `src/styles/global.css:72-80` (link styles)
- Modify: `src/styles/global.css:90-93` (strong tag)
- Modify: `src/styles/global.css:95-99` (hr)
- Modify: `src/styles/global.css:101-107` (code)

- [ ] **Step 1: Replace `:root` custom properties**

Replace the entire `:root` block in `src/styles/global.css`:

```css
:root {
  --color-bg: #1e1b4b;
  --color-surface: #312e81;
  --color-text: #ffffff;
  --color-text-muted: #c7d2fe;
  --color-text-tertiary: #a5b4fc;
  --color-border: rgba(255, 255, 255, 0.1);
  --color-accent: #6366f1;
  --color-accent-hover: #818cf8;

  --font-sans: -apple-system, BlinkMacSystemFont, "Segoe UI", "Helvetica Neue",
    Arial, sans-serif;
  --font-mono: ui-monospace, SFMono-Regular, Menlo, Monaco, Consolas, monospace;

  --max-width: 720px;
}
```

- [ ] **Step 2: Update base element styles that reference old palette**

In `src/styles/global.css`, update the `strong` rule to not override color (it was forcing dark text, now the inherited white is correct):

```css
strong {
  font-weight: 600;
}
```

Update the `code` rule background to use the surface color:

```css
code {
  font-family: var(--font-mono);
  font-size: 0.9em;
  background: var(--color-surface);
  padding: 0.1em 0.35em;
  border-radius: 3px;
}
```

- [ ] **Step 3: Run dev server and verify base styles**

Run: `npm run dev`

Open `http://localhost:4321/support` in a browser. Verify:
- Dark indigo background
- White heading text
- Muted blue body text
- Links are indigo accent color
- No white-on-white or invisible text anywhere

- [ ] **Step 4: Commit**

```bash
git add src/styles/global.css
git commit -m "feat: apply Indigo Night color palette to CSS custom properties"
```

---

### Task 2: Restyle header and footer for dark theme

**Files:**
- Modify: `src/styles/global.css:114-175` (header and footer styles)

- [ ] **Step 1: Update header styles**

Replace the header CSS block in `src/styles/global.css`:

```css
/* Header */
.site-header {
  border-bottom: 1px solid var(--color-border);
  background: var(--color-bg);
}

.site-header-inner {
  max-width: var(--max-width);
  margin: 0 auto;
  padding: 1.25rem 1.5rem;
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.site-logo {
  font-weight: 700;
  font-size: 1.25rem;
  color: var(--color-text);
}

.site-logo:hover {
  text-decoration: none;
  color: var(--color-accent);
}

.site-nav {
  display: flex;
  gap: 1.5rem;
}

.site-nav a {
  color: var(--color-text-tertiary);
  font-size: 0.95rem;
}

.site-nav a:hover {
  color: var(--color-accent);
  text-decoration: none;
}

.site-nav .nav-cta {
  color: var(--color-accent);
  font-weight: 600;
}
```

- [ ] **Step 2: Update footer styles**

Replace the footer CSS block in `src/styles/global.css`:

```css
/* Footer */
.site-footer {
  border-top: 1px solid var(--color-border);
  background: var(--color-bg);
  padding: 2rem 1.5rem;
  text-align: center;
  color: var(--color-text-tertiary);
  font-size: 0.9rem;
}

.site-footer-links {
  display: flex;
  gap: 1.5rem;
  justify-content: center;
  margin-bottom: 0.75rem;
}
```

- [ ] **Step 3: Verify in browser**

Open `http://localhost:4321` — verify header and footer blend into the dark background. Nav links should be light indigo, "Get Deal Lens" should be brighter accent. Footer text should be subtle.

Check `http://localhost:4321/support` to confirm inner pages also look correct.

- [ ] **Step 4: Commit**

```bash
git add src/styles/global.css
git commit -m "feat: restyle header and footer for dark theme"
```

---

### Task 3: Rebuild landing page hero section

**Files:**
- Modify: `src/pages/index.astro` (full rewrite of page content)
- Modify: `src/styles/global.css` (hero styles update)

- [ ] **Step 1: Rewrite index.astro with new hero structure**

Replace the entire content of `src/pages/index.astro`:

```astro
---
import Layout from '../layouts/Layout.astro';

const chromeWebStoreUrl = 'https://chromewebstore.google.com/detail/deal-lens/ndojllleemkjjelapmjdgapoeincbiol';
---

<Layout
  title="Deal Lens — Stop overpaying for used gear"
  description="AI-powered price analysis for enthusiast gear on Facebook Marketplace, eBay, and Reverb. Music, cameras, golf — know what it's worth before you buy."
>
  <section class="hero">
    <span class="badge">The deal checker for enthusiast gear</span>
    <h1>Stop overpaying<br>for used gear.</h1>
    <p class="hero-sub">
      AI-powered price analysis on Facebook Marketplace, eBay, and Reverb.
    </p>
    <a href={chromeWebStoreUrl} class="btn">Add to Chrome — Free</a>

    <div class="browser-mockup">
      <div class="browser-bar">
        <div class="browser-dots">
          <span></span><span></span><span></span>
        </div>
        <div class="browser-url">facebook.com/marketplace/item/...</div>
      </div>
      <div class="browser-body">
        <div class="listing-side">
          <div class="listing-image"></div>
          <div class="listing-title">Fender Jazz Bass MIJ 1994</div>
          <div class="listing-price">$680</div>
        </div>
        <div class="panel-side">
          <div class="panel-header">Deal Lens</div>
          <div class="panel-verdict verdict-good">Good Deal</div>
          <div class="panel-label">Estimated value</div>
          <div class="panel-value">$750 – $850</div>
          <div class="panel-label">Comparable sales</div>
          <div class="panel-comp">
            <span>Fender Jazz MIJ '93 — Reverb</span>
            <span>$810</span>
          </div>
          <div class="panel-comp">
            <span>Fender Jazz MIJ '95 — eBay</span>
            <span>$775</span>
          </div>
          <div class="panel-comp">
            <span>Fender Jazz Bass CIJ — Reverb</span>
            <span>$720</span>
          </div>
        </div>
      </div>
    </div>
  </section>

  <section class="stats-bar">
    <div class="stat">
      <div class="stat-value">3</div>
      <div class="stat-label">Platforms</div>
    </div>
    <div class="stat">
      <div class="stat-value">AI</div>
      <div class="stat-label">Powered</div>
    </div>
    <div class="stat">
      <div class="stat-value">Real</div>
      <div class="stat-label">Sold Comps</div>
    </div>
  </section>

  <section class="features">
    <div class="feature">
      <h3>Built for enthusiast gear</h3>
      <p>
        Music gear, cameras, golf clubs, vintage audio — anywhere specific
        model, year, and condition decide the price. Deal Lens reads the
        actual listing instead of averaging it away.
      </p>
    </div>
    <div class="feature">
      <h3>Real sold comps, not guesses</h3>
      <p>
        Pulls comparable listings from eBay and Reverb so every estimate is
        anchored to what items actually sold for — not a dealer's asking
        price.
      </p>
    </div>
    <div class="feature">
      <h3>Buy or flip, one verdict</h3>
      <p>
        Tells you whether something is a good buy at the asking price — and
        whether it's worth flipping for profit after fees.
      </p>
    </div>
    <div class="feature">
      <h3>Works where you shop</h3>
      <p>
        Facebook Marketplace, eBay, and Reverb supported today. More
        platforms coming.
      </p>
    </div>
  </section>
</Layout>
```

- [ ] **Step 2: Update hero CSS and add new component styles**

Replace the hero CSS block and add new styles after it in `src/styles/global.css`. Remove the old `.hero`, `.hero h1`, `.hero p`, `.btn`, `.btn:hover`, `.features`, `.feature`, `.feature h3`, `.feature p` blocks (lines 177–232) and replace with:

```css
/* Hero (landing page) */
.hero {
  text-align: center;
  padding: 3rem 0 2rem;
}

.badge {
  display: inline-block;
  background: rgba(99, 102, 241, 0.2);
  color: var(--color-text-tertiary);
  padding: 0.35rem 1rem;
  border-radius: 99px;
  font-size: 0.85rem;
  font-weight: 500;
  margin-bottom: 1.5rem;
}

.hero h1 {
  font-size: 3.25rem;
  font-weight: 800;
  letter-spacing: -0.02em;
  margin-bottom: 1rem;
  line-height: 1.1;
}

.hero-sub {
  font-size: 1.15rem;
  color: var(--color-text-muted);
  max-width: 540px;
  margin: 0 auto 2rem;
}

.btn {
  display: inline-block;
  background: var(--color-accent);
  color: #fff;
  padding: 0.85rem 2rem;
  border-radius: 8px;
  font-weight: 600;
  font-size: 1.05rem;
  transition: background 0.15s;
}

.btn:hover {
  background: var(--color-accent-hover);
  color: #fff;
  text-decoration: none;
}

/* Browser mockup */
.browser-mockup {
  max-width: 600px;
  margin: 2.5rem auto 0;
  border-radius: 10px;
  overflow: hidden;
  border: 1px solid var(--color-border);
  background: #0f0e2a;
  text-align: left;
}

.browser-bar {
  display: flex;
  align-items: center;
  gap: 0.75rem;
  padding: 0.6rem 1rem;
  background: rgba(255, 255, 255, 0.05);
  border-bottom: 1px solid var(--color-border);
}

.browser-dots {
  display: flex;
  gap: 0.35rem;
}

.browser-dots span {
  width: 8px;
  height: 8px;
  border-radius: 50%;
  background: rgba(255, 255, 255, 0.15);
}

.browser-url {
  font-size: 0.7rem;
  color: var(--color-text-tertiary);
  background: rgba(255, 255, 255, 0.05);
  padding: 0.25rem 0.75rem;
  border-radius: 4px;
  flex: 1;
}

.browser-body {
  display: flex;
  min-height: 200px;
}

.listing-side {
  flex: 1;
  padding: 1rem;
  border-right: 1px solid var(--color-border);
}

.listing-image {
  width: 100%;
  height: 80px;
  background: rgba(255, 255, 255, 0.05);
  border-radius: 6px;
  margin-bottom: 0.75rem;
}

.listing-title {
  font-size: 0.8rem;
  font-weight: 600;
  color: var(--color-text);
  margin-bottom: 0.25rem;
}

.listing-price {
  font-size: 1.1rem;
  font-weight: 700;
  color: var(--color-text);
}

.panel-side {
  width: 200px;
  padding: 0.75rem;
  background: rgba(99, 102, 241, 0.08);
}

.panel-header {
  font-size: 0.7rem;
  font-weight: 700;
  color: var(--color-accent);
  text-transform: uppercase;
  letter-spacing: 0.05em;
  margin-bottom: 0.5rem;
}

.panel-verdict {
  display: inline-block;
  padding: 0.2rem 0.6rem;
  border-radius: 4px;
  font-size: 0.75rem;
  font-weight: 600;
  margin-bottom: 0.75rem;
}

.verdict-good {
  background: rgba(34, 197, 94, 0.2);
  color: #4ade80;
}

.panel-label {
  font-size: 0.6rem;
  color: var(--color-text-tertiary);
  text-transform: uppercase;
  letter-spacing: 0.04em;
  margin-bottom: 0.25rem;
  margin-top: 0.5rem;
}

.panel-value {
  font-size: 0.85rem;
  font-weight: 700;
  color: var(--color-text);
}

.panel-comp {
  display: flex;
  justify-content: space-between;
  font-size: 0.65rem;
  color: var(--color-text-muted);
  padding: 0.3rem 0;
  border-bottom: 1px solid rgba(255, 255, 255, 0.05);
}

/* Stats bar */
.stats-bar {
  display: flex;
  justify-content: center;
  gap: 3rem;
  padding: 2rem 0;
  border-top: 1px solid var(--color-border);
  border-bottom: 1px solid var(--color-border);
  margin-bottom: 2rem;
}

.stat {
  text-align: center;
}

.stat-value {
  font-size: 1.5rem;
  font-weight: 800;
  color: var(--color-accent-hover);
}

.stat-label {
  font-size: 0.8rem;
  color: var(--color-text-tertiary);
  margin-top: 0.15rem;
}

/* Feature cards */
.features {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 1.25rem;
}

.feature {
  padding: 1.25rem;
  background: var(--color-surface);
  border: 1px solid var(--color-border);
  border-radius: 8px;
}

.feature h3 {
  margin-top: 0;
  color: var(--color-text);
}

.feature p {
  margin-bottom: 0;
  color: var(--color-text-muted);
  font-size: 0.95rem;
}
```

- [ ] **Step 3: Verify in browser**

Open `http://localhost:4321` and verify:
- Badge pill appears above headline
- "Stop overpaying for used gear." headline is large and bold
- CTA button says "Add to Chrome — Free"
- Browser mockup renders below CTA with listing + sidebar panel
- Stats bar shows three items with divider lines
- Feature cards in 2x2 grid
- No "A Walensis product." text
- No layout breaks on narrow viewport

- [ ] **Step 4: Commit**

```bash
git add src/pages/index.astro src/styles/global.css
git commit -m "feat: rebuild landing page with hero mockup, stats bar, and 2x2 features"
```

---

### Task 4: Update favicon to Indigo Night palette

**Files:**
- Modify: `public/favicon.svg`

- [ ] **Step 1: Replace teal color with indigo in favicon.svg**

Replace all instances of `#0f766e` with `#6366f1` in `public/favicon.svg`. The updated file:

```svg
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 128 128" fill="none">
  <!-- Handle -->
  <line x1="84" y1="84" x2="116" y2="116"
        stroke="#6366f1" stroke-width="14" stroke-linecap="round"/>

  <!-- Lens -->
  <circle cx="52" cy="52" r="44" fill="#ffffff" stroke="#6366f1" stroke-width="10"/>

  <!-- Bar chart inside lens -->
  <rect x="32" y="58" width="10" height="14" rx="1.5" fill="#6366f1"/>
  <rect x="47" y="48" width="10" height="24" rx="1.5" fill="#6366f1"/>
  <rect x="62" y="38" width="10" height="34" rx="1.5" fill="#6366f1"/>
</svg>
```

- [ ] **Step 2: Verify favicon in browser**

Hard-refresh `http://localhost:4321` and check the browser tab icon shows the indigo-colored lens.

- [ ] **Step 3: Commit**

```bash
git add public/favicon.svg
git commit -m "feat: update favicon from teal to indigo palette"
```

---

### Task 5: Create Chrome Web Store small tile (440x280)

**Files:**
- Create: `public/promo/small-tile.html`

- [ ] **Step 1: Create the promo directory**

```bash
mkdir -p public/promo
```

- [ ] **Step 2: Create small-tile.html**

Create `public/promo/small-tile.html` — a self-contained HTML file at exactly 440x280:

```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<style>
  * { margin: 0; padding: 0; box-sizing: border-box; }
  body {
    width: 440px;
    height: 280px;
    background: linear-gradient(135deg, #1e1b4b 0%, #312e81 40%, #6366f1 100%);
    font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", "Helvetica Neue", Arial, sans-serif;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    color: #ffffff;
    overflow: hidden;
  }
  .icon {
    width: 64px;
    height: 64px;
    margin-bottom: 1.25rem;
  }
  .name {
    font-size: 1.75rem;
    font-weight: 800;
    letter-spacing: -0.02em;
    margin-bottom: 0.5rem;
  }
  .tagline {
    font-size: 0.95rem;
    color: #c7d2fe;
    font-weight: 400;
  }
</style>
</head>
<body>
  <svg class="icon" viewBox="0 0 128 128" fill="none" xmlns="http://www.w3.org/2000/svg">
    <line x1="84" y1="84" x2="116" y2="116" stroke="#a5b4fc" stroke-width="14" stroke-linecap="round"/>
    <circle cx="52" cy="52" r="44" fill="rgba(255,255,255,0.15)" stroke="#a5b4fc" stroke-width="10"/>
    <rect x="32" y="58" width="10" height="14" rx="1.5" fill="#a5b4fc"/>
    <rect x="47" y="48" width="10" height="24" rx="1.5" fill="#a5b4fc"/>
    <rect x="62" y="38" width="10" height="34" rx="1.5" fill="#a5b4fc"/>
  </svg>
  <div class="name">Deal Lens</div>
  <div class="tagline">Stop overpaying for used gear.</div>
</body>
</html>
```

- [ ] **Step 3: Open in browser and verify**

Open `http://localhost:4321/promo/small-tile.html` in a browser. Verify:
- Gradient background renders
- Lens icon is centered and visible
- "Deal Lens" is bold and white
- Tagline is visible in muted text
- No scrollbars at 440x280

- [ ] **Step 4: Commit**

```bash
git add public/promo/small-tile.html
git commit -m "feat: add Chrome Web Store small tile promo template"
```

---

### Task 6: Create Chrome Web Store large tile (920x680)

**Files:**
- Create: `public/promo/large-tile.html`

- [ ] **Step 1: Create large-tile.html**

Create `public/promo/large-tile.html` — self-contained at 920x680:

```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<style>
  * { margin: 0; padding: 0; box-sizing: border-box; }
  body {
    width: 920px;
    height: 680px;
    background: linear-gradient(135deg, #1e1b4b 0%, #312e81 50%, #4f46e5 100%);
    font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", "Helvetica Neue", Arial, sans-serif;
    color: #ffffff;
    overflow: hidden;
    padding: 3.5rem;
    display: flex;
    flex-direction: column;
  }
  .top { flex: 1; }
  .headline {
    font-size: 2.75rem;
    font-weight: 800;
    letter-spacing: -0.02em;
    line-height: 1.1;
    margin-bottom: 0.75rem;
  }
  .subtext {
    font-size: 1.15rem;
    color: #c7d2fe;
    margin-bottom: 2rem;
  }
  .mockup {
    background: #0f0e2a;
    border-radius: 10px;
    overflow: hidden;
    border: 1px solid rgba(255,255,255,0.1);
    max-width: 700px;
  }
  .mock-bar {
    display: flex;
    align-items: center;
    gap: 0.75rem;
    padding: 0.5rem 0.75rem;
    background: rgba(255,255,255,0.05);
    border-bottom: 1px solid rgba(255,255,255,0.1);
  }
  .dots { display: flex; gap: 0.3rem; }
  .dots span {
    width: 7px; height: 7px;
    border-radius: 50%;
    background: rgba(255,255,255,0.15);
  }
  .mock-url {
    font-size: 0.65rem;
    color: #a5b4fc;
    background: rgba(255,255,255,0.05);
    padding: 0.2rem 0.6rem;
    border-radius: 3px;
    flex: 1;
  }
  .mock-body {
    display: flex;
    min-height: 220px;
  }
  .mock-listing {
    flex: 1;
    padding: 1rem;
    border-right: 1px solid rgba(255,255,255,0.1);
  }
  .mock-img {
    width: 100%;
    height: 100px;
    background: rgba(255,255,255,0.05);
    border-radius: 6px;
    margin-bottom: 0.6rem;
  }
  .mock-title {
    font-size: 0.8rem;
    font-weight: 600;
    margin-bottom: 0.2rem;
  }
  .mock-price {
    font-size: 1.1rem;
    font-weight: 700;
  }
  .mock-panel {
    width: 200px;
    padding: 0.75rem;
    background: rgba(99,102,241,0.08);
  }
  .mock-panel-hdr {
    font-size: 0.65rem;
    font-weight: 700;
    color: #6366f1;
    text-transform: uppercase;
    letter-spacing: 0.05em;
    margin-bottom: 0.4rem;
  }
  .mock-verdict {
    display: inline-block;
    padding: 0.15rem 0.5rem;
    border-radius: 4px;
    font-size: 0.7rem;
    font-weight: 600;
    background: rgba(34,197,94,0.2);
    color: #4ade80;
    margin-bottom: 0.6rem;
  }
  .mock-lbl {
    font-size: 0.55rem;
    color: #a5b4fc;
    text-transform: uppercase;
    letter-spacing: 0.04em;
    margin-bottom: 0.15rem;
    margin-top: 0.4rem;
  }
  .mock-val {
    font-size: 0.8rem;
    font-weight: 700;
  }
  .mock-comp {
    display: flex;
    justify-content: space-between;
    font-size: 0.6rem;
    color: #c7d2fe;
    padding: 0.25rem 0;
    border-bottom: 1px solid rgba(255,255,255,0.05);
  }
  .bottom {
    display: flex;
    align-items: center;
    gap: 1rem;
    margin-top: 1.5rem;
  }
  .pill {
    padding: 0.35rem 0.85rem;
    border-radius: 99px;
    font-size: 0.8rem;
    font-weight: 500;
  }
  .pill-platform {
    background: rgba(255,255,255,0.1);
    color: #c7d2fe;
  }
  .pill-category {
    background: rgba(99,102,241,0.2);
    color: #a5b4fc;
  }
</style>
</head>
<body>
  <div class="top">
    <div class="headline">Stop overpaying<br>for used gear.</div>
    <div class="subtext">AI-powered price analysis for enthusiast gear</div>
    <div class="mockup">
      <div class="mock-bar">
        <div class="dots"><span></span><span></span><span></span></div>
        <div class="mock-url">facebook.com/marketplace/item/...</div>
      </div>
      <div class="mock-body">
        <div class="mock-listing">
          <div class="mock-img"></div>
          <div class="mock-title">Fender Jazz Bass MIJ 1994</div>
          <div class="mock-price">$680</div>
        </div>
        <div class="mock-panel">
          <div class="mock-panel-hdr">Deal Lens</div>
          <div class="mock-verdict">Good Deal</div>
          <div class="mock-lbl">Estimated value</div>
          <div class="mock-val">$750 – $850</div>
          <div class="mock-lbl">Comparable sales</div>
          <div class="mock-comp"><span>Fender Jazz MIJ '93 — Reverb</span><span>$810</span></div>
          <div class="mock-comp"><span>Fender Jazz MIJ '95 — eBay</span><span>$775</span></div>
          <div class="mock-comp"><span>Fender Jazz CIJ — Reverb</span><span>$720</span></div>
        </div>
      </div>
    </div>
  </div>
  <div class="bottom">
    <span class="pill pill-platform">Facebook Marketplace</span>
    <span class="pill pill-platform">eBay</span>
    <span class="pill pill-platform">Reverb</span>
    <span class="pill pill-category">Music</span>
    <span class="pill pill-category">Cameras</span>
    <span class="pill pill-category">Golf</span>
  </div>
</body>
</html>
```

- [ ] **Step 2: Open in browser and verify**

Open `http://localhost:4321/promo/large-tile.html`. Verify:
- Headline top-left, subtext below
- Browser mockup with listing + sidebar panel
- Platform and category pills at bottom
- No scrollbars at 920x680

- [ ] **Step 3: Commit**

```bash
git add public/promo/large-tile.html
git commit -m "feat: add Chrome Web Store large tile promo template"
```

---

### Task 7: Create Chrome Web Store marquee (1400x560)

**Files:**
- Create: `public/promo/marquee.html`

- [ ] **Step 1: Create marquee.html**

Create `public/promo/marquee.html` — self-contained at 1400x560:

```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<style>
  * { margin: 0; padding: 0; box-sizing: border-box; }
  body {
    width: 1400px;
    height: 560px;
    background: linear-gradient(135deg, #1e1b4b 0%, #312e81 40%, #4f46e5 100%);
    font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", "Helvetica Neue", Arial, sans-serif;
    color: #ffffff;
    overflow: hidden;
    display: flex;
    align-items: center;
    padding: 0 5rem;
    gap: 4rem;
  }
  .left {
    flex: 1;
  }
  .headline {
    font-size: 3rem;
    font-weight: 800;
    letter-spacing: -0.02em;
    line-height: 1.1;
    margin-bottom: 1rem;
  }
  .subtext {
    font-size: 1.2rem;
    color: #c7d2fe;
    margin-bottom: 1.75rem;
  }
  .cta {
    display: inline-block;
    background: #6366f1;
    color: #fff;
    padding: 0.75rem 1.75rem;
    border-radius: 8px;
    font-weight: 600;
    font-size: 1rem;
    margin-bottom: 1.5rem;
  }
  .pills {
    display: flex;
    gap: 0.6rem;
  }
  .pill {
    padding: 0.3rem 0.75rem;
    border-radius: 99px;
    font-size: 0.8rem;
    font-weight: 500;
    background: rgba(99,102,241,0.2);
    color: #a5b4fc;
  }
  .right {
    flex: 0 0 520px;
  }
  .mockup {
    background: #0f0e2a;
    border-radius: 10px;
    overflow: hidden;
    border: 1px solid rgba(255,255,255,0.1);
    box-shadow: 0 25px 50px rgba(0,0,0,0.3);
  }
  .mock-bar {
    display: flex;
    align-items: center;
    gap: 0.75rem;
    padding: 0.5rem 0.75rem;
    background: rgba(255,255,255,0.05);
    border-bottom: 1px solid rgba(255,255,255,0.1);
  }
  .dots { display: flex; gap: 0.3rem; }
  .dots span {
    width: 7px; height: 7px;
    border-radius: 50%;
    background: rgba(255,255,255,0.15);
  }
  .mock-url {
    font-size: 0.65rem;
    color: #a5b4fc;
    background: rgba(255,255,255,0.05);
    padding: 0.2rem 0.6rem;
    border-radius: 3px;
    flex: 1;
  }
  .mock-body {
    display: flex;
    min-height: 280px;
  }
  .mock-listing {
    flex: 1;
    padding: 1rem;
    border-right: 1px solid rgba(255,255,255,0.1);
  }
  .mock-img {
    width: 100%;
    height: 130px;
    background: rgba(255,255,255,0.05);
    border-radius: 6px;
    margin-bottom: 0.6rem;
  }
  .mock-title {
    font-size: 0.85rem;
    font-weight: 600;
    margin-bottom: 0.2rem;
  }
  .mock-price {
    font-size: 1.15rem;
    font-weight: 700;
  }
  .mock-panel {
    width: 210px;
    padding: 0.75rem;
    background: rgba(99,102,241,0.08);
  }
  .mock-panel-hdr {
    font-size: 0.65rem;
    font-weight: 700;
    color: #6366f1;
    text-transform: uppercase;
    letter-spacing: 0.05em;
    margin-bottom: 0.4rem;
  }
  .mock-verdict {
    display: inline-block;
    padding: 0.15rem 0.5rem;
    border-radius: 4px;
    font-size: 0.7rem;
    font-weight: 600;
    background: rgba(34,197,94,0.2);
    color: #4ade80;
    margin-bottom: 0.6rem;
  }
  .mock-lbl {
    font-size: 0.55rem;
    color: #a5b4fc;
    text-transform: uppercase;
    letter-spacing: 0.04em;
    margin-bottom: 0.15rem;
    margin-top: 0.4rem;
  }
  .mock-val {
    font-size: 0.85rem;
    font-weight: 700;
  }
  .mock-comp {
    display: flex;
    justify-content: space-between;
    font-size: 0.6rem;
    color: #c7d2fe;
    padding: 0.25rem 0;
    border-bottom: 1px solid rgba(255,255,255,0.05);
  }
</style>
</head>
<body>
  <div class="left">
    <div class="headline">Stop overpaying<br>for used gear.</div>
    <div class="subtext">AI-powered price analysis on Facebook Marketplace, eBay, and Reverb.</div>
    <div class="cta">Add to Chrome — Free</div>
    <div class="pills">
      <span class="pill">Music</span>
      <span class="pill">Cameras</span>
      <span class="pill">Golf</span>
    </div>
  </div>
  <div class="right">
    <div class="mockup">
      <div class="mock-bar">
        <div class="dots"><span></span><span></span><span></span></div>
        <div class="mock-url">facebook.com/marketplace/item/...</div>
      </div>
      <div class="mock-body">
        <div class="mock-listing">
          <div class="mock-img"></div>
          <div class="mock-title">Fender Jazz Bass MIJ 1994</div>
          <div class="mock-price">$680</div>
        </div>
        <div class="mock-panel">
          <div class="mock-panel-hdr">Deal Lens</div>
          <div class="mock-verdict">Good Deal</div>
          <div class="mock-lbl">Estimated value</div>
          <div class="mock-val">$750 – $850</div>
          <div class="mock-lbl">Comparable sales</div>
          <div class="mock-comp"><span>Fender Jazz MIJ '93 — Reverb</span><span>$810</span></div>
          <div class="mock-comp"><span>Fender Jazz MIJ '95 — eBay</span><span>$775</span></div>
          <div class="mock-comp"><span>Fender Jazz CIJ — Reverb</span><span>$720</span></div>
        </div>
      </div>
    </div>
  </div>
</body>
</html>
```

- [ ] **Step 2: Open in browser and verify**

Open `http://localhost:4321/promo/marquee.html`. Verify:
- Left half: headline, subtext, CTA button, category pills
- Right half: browser mockup with listing + sidebar
- Gradient sweeps across
- No scrollbars at 1400x560

- [ ] **Step 3: Commit**

```bash
git add public/promo/marquee.html
git commit -m "feat: add Chrome Web Store marquee promo template"
```

---

### Task 8: Add .superpowers/ to .gitignore

**Files:**
- Modify: `.gitignore`

- [ ] **Step 1: Add .superpowers/ to .gitignore**

Add to the end of `.gitignore`:

```
# superpowers brainstorm artifacts
.superpowers/
```

- [ ] **Step 2: Commit**

```bash
git add .gitignore
git commit -m "chore: add .superpowers/ to gitignore"
```

---

### Task 9: Final verification

- [ ] **Step 1: Run dev server and check all pages**

Run: `npm run dev`

Check each page in the browser:
- `http://localhost:4321` — full landing page with hero, mockup, stats, features
- `http://localhost:4321/support` — dark theme inherited, text readable
- `http://localhost:4321/privacy` — dark theme inherited
- `http://localhost:4321/terms` — dark theme inherited
- `http://localhost:4321/deal-lens/welcome` — dark theme inherited
- `http://localhost:4321/deal-lens/privacy` — dark theme inherited
- `http://localhost:4321/deal-lens/terms` — dark theme inherited

Verify no white-on-white text, no broken layouts, all links visible.

- [ ] **Step 2: Check promo templates**

- `http://localhost:4321/promo/small-tile.html` — 440x280, no scrollbars
- `http://localhost:4321/promo/large-tile.html` — 920x680, no scrollbars
- `http://localhost:4321/promo/marquee.html` — 1400x560, no scrollbars

- [ ] **Step 3: Verify favicon**

Check browser tab shows indigo-colored lens icon.

- [ ] **Step 4: Run build to confirm no errors**

```bash
npm run build
```

Expected: clean build with no errors.
