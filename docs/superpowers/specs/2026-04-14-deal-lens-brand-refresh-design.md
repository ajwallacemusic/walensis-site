# Deal Lens Brand Refresh & Chrome Web Store Assets

**Date:** 2026-04-14
**Status:** Approved

## Overview

Refresh the Deal Lens website from a minimal light-theme text site to a bold, dark Indigo Night brand, and create three Chrome Web Store promotional image assets. The goal is to make the site and store listing feel like a product enthusiasts get excited about — matching the energy of the deal-hunting audience.

## Brand System

### Color Palette (Indigo Night)

| Token | Value | Usage |
|-------|-------|-------|
| `--color-bg` | `#1e1b4b` | Page background |
| `--color-surface` | `#312e81` | Cards, panels |
| `--color-accent` | `#6366f1` | Buttons, primary highlights |
| `--color-accent-hover` | `#818cf8` | Button hover, stats emphasis |
| `--color-text` | `#ffffff` | Primary text |
| `--color-text-muted` | `#c7d2fe` | Body text on dark bg |
| `--color-text-tertiary` | `#a5b4fc` | Labels, subtle text |
| `--color-border` | `rgba(255, 255, 255, 0.1)` | Card borders, dividers |

### Gradient

Hero and promo backgrounds use:
```
linear-gradient(135deg, #1e1b4b 0%, #312e81 40%, #6366f1 100%)
```

### Typography

- System font stack unchanged: `-apple-system, BlinkMacSystemFont, "Segoe UI", "Helvetica Neue", Arial, sans-serif`
- Hero headline: 3rem+, font-weight 800, letter-spacing -0.02em
- Body: 1.1rem, weight 400, `#c7d2fe`
- No custom fonts — zero external dependencies

### Logo

- Text-based "Walensis" — white on dark background
- No image logo needed

### Favicon

- Update existing `favicon.svg` stroke color from `#0f766e` (teal) to `#6366f1` (indigo) to match new palette

## Landing Page

### Structure (top to bottom)

#### 1. Header
- Dark background (`--color-bg`)
- "Walensis" logo left (white, bold)
- Nav right: "Get Deal Lens" CTA link (indigo accent, bold) + Privacy, Terms, Support (muted text)

#### 2. Hero Section
- **Category badge**: pill-shaped, semi-transparent indigo bg, text "The deal checker for enthusiast gear"
- **Headline**: "Stop overpaying for used gear." — 3rem+, weight 800, white
- **Subheadline**: "AI-powered price analysis on Facebook Marketplace, eBay, and Reverb." — muted text
- **CTA button**: "Add to Chrome — Free" — `#6366f1` bg, white text, rounded, links to Chrome Web Store
- **Browser mockup**: below the CTA, a stylized representation of a browser window with the Deal Lens extension sidebar visible, analyzing a listing. Built in pure HTML/CSS (not an image).

#### 3. Stats Bar
Horizontal strip with three items, subtle dividers:
- "3 Platforms"
- "AI Powered"
- "Real Sold Comps"

#### 4. Feature Cards
2x2 grid, same four features with same copy as current site:
1. Built for enthusiast gear
2. Real sold comps, not guesses
3. Buy or flip, one verdict
4. Works where you shop

Restyled: dark card bg (`--color-surface`), subtle border (`rgba(255,255,255,0.1)`), rounded corners. Feature titles in white, descriptions in muted text.

#### 5. Footer
- Same links: Privacy, Terms, Support
- Same copyright line
- Restyled for dark background: muted text, subtle top border

### Copy Changes
- Headline: "Deal Lens" → "Stop overpaying for used gear."
- Badge (new): "The deal checker for enthusiast gear"
- CTA: "Get Deal Lens for Chrome" → "Add to Chrome — Free"
- "A Walensis product." line removed (logo in header is sufficient)

## Chrome Web Store Promotional Images

All built as standalone HTML pages, screenshotted at the required pixel dimensions. Same Indigo Night palette.

### Small Tile (440x280)
- Centered layout
- Deal Lens name in bold white
- Magnifying lens icon (from favicon, scaled up, recolored to indigo palette)
- Tagline: "Stop overpaying for used gear."
- Gradient background

### Large Tile (920x680)
- Headline top-left: "Stop overpaying for used gear."
- Subtext: "AI-powered price analysis for enthusiast gear"
- Right/lower area: browser mockup showing extension sidebar analyzing a listing
- Bottom strip: platform pills (Facebook Marketplace, eBay, Reverb)
- Category accent pills: Music, Cameras, Golf

### Marquee (1400x560)
- Wide cinematic layout
- Left half: headline + subtext + decorative "Add to Chrome" button
- Right half: browser mockup with extension panel
- Category pills as accent badges
- Gradient background sweeping left to right

### Browser Mockup (shared component)
Used in the landing page hero and the promo images. A stylized HTML/CSS representation of:
- A browser chrome bar (simplified URL bar, window controls)
- A listing page body (product image placeholder, title, price)
- The Deal Lens sidebar panel showing: product name, estimated value, verdict badge ("Good Deal"), 2-3 comp listings

Readable at small sizes, consistent with brand. Not a real screenshot — a designed representation.

## Files Changed

| File | Change |
|------|--------|
| `src/styles/global.css` | Full restyle: Indigo Night palette, dark theme for all components |
| `src/layouts/Layout.astro` | Header/footer restyled for dark bg |
| `src/pages/index.astro` | New hero structure: badge, headline, mockup, stats bar, feature grid |
| `public/favicon.svg` | Stroke color `#0f766e` → `#6366f1` |

## New Files

| File | Purpose |
|------|---------|
| `public/promo/small-tile.html` | Chrome Web Store small promo (440x280) — screenshot source |
| `public/promo/large-tile.html` | Chrome Web Store large promo (920x680) — screenshot source |
| `public/promo/marquee.html` | Chrome Web Store marquee (1400x560) — screenshot source |

## Out of Scope

- No new pages — support, privacy, terms inherit dark theme from layout
- No custom fonts or external asset dependencies
- No JavaScript additions
- No welcome page changes beyond inherited layout restyle
- No actual extension screenshots in promo images — stylized mockups only
- No logo redesign — stays text-based
