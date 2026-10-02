---
name: audi-brand
description: Audi brand digital design language — progressive, precise, reduced; monochrome plus a single red accent, engineered for car model pages and premium tech.
---

# audi-brand

Audi's digital design language: progressive, precise, reduced. Everything on
audi.com and in Audi digital communications is engineered, not decorated —
generous whitespace, full-bleed imagery, hairline rules, and technical
typography. The slogan says it all: *Vorsprung durch Technik*
("Advancement through technology").

## Principles

1. **Reduced, never empty.** Strip everything that isn't load-bearing, then
   give what remains room to breathe. Whitespace is a brand asset.
2. **Technical precision.** Specs are set like instruments: tabular figures,
   consistent units, hairline dividers, no decorative noise.
3. **Monochrome discipline.** The page lives in black, white, and grays.
   Red appears exactly once or twice per view — badging, one CTA, a key figure.
4. **Progressive confidence.** Copy states facts and lets engineering speak.
   No exclamation marks, no hype adjectives, no superlatives.
5. **Full-bleed imagery.** The car is shown large, in motion or in
   architectural settings; UI chrome stays minimal and gets out of the way.

## Color

Audi's official palette is black, white, silver/gray, and a single
"progressive red" (Audi's own wording, via AudiWorld's brand overview).
Exact corporate values live behind Audi's brand portal; hexes below are marked
honestly.

| Token | Hex | Role | Confidence |
|---|---|---|---|
| `--audi-black` | `#000000` | Primary brand color; hero backgrounds, nav, footer | ✅ |
| `--audi-white` | `#FFFFFF` | Primary brand color; light sections, text on black | ✅ |
| `--audi-silver` | `#C0C0C0` | Signature silver (Pantone 877 C); accents, rules on dark | 🟡 |
| `--audi-red` | `#BB0A30` | "Progressive red"; single accent — RS badging, one key CTA | ⚠️ |
| `--ink` | `#0A0A0A` | Near-black page background (digital adaptation) | ⚠️ |
| `--surface` | `#161616` | Raised surface on dark | ⚠️ |
| `--hairline-dark` | `#2B2B2B` | 1px dividers on dark | ⚠️ |
| `--muted` | `#9A9A9A` | Secondary text on dark | ⚠️ |
| `--hairline-light` | `#E2E2E2` | 1px dividers on light | ⚠️ |
| `--paper` | `#F5F5F5` | Light section background | ⚠️ |

Rules: never pair red with blue; never set body text in red; never use
red for more than one focal element per viewport.

## Typography

- **Audi Type** — Audi's corporate typeface, designed by Paul van der Laan and
  Pieter van Rosmalen (Bold Monday, via MetaDesign), introduced 2009 for Audi's
  centenary, replacing the Univers-based Audi Sans. Design theme: "Pure and
  Clean". ✅ Proprietary — not available for public use.
- **Closest free substitute:** **Archivo** (Google Fonts), weights 300–600.
  Use the Expanded width axis for display headlines to approximate
  Audi Type Extended. 🟡
- Headlines: light/regular weight (300–400), sentence case, tight tracking,
  large sizes. Audi headlines are *quiet*, never bold-shouted.
- Specs and figures: `font-variant-numeric: tabular-nums`; units set small
  and gray (`km`, `kW`, `s`) next to large figures.
- Eyebrow labels: 11–12 px, uppercase, letter-spacing 0.18em, gray —
  the "technical drawing" voice of the page.
- Body: 16–18 px, regular, line-height 1.6, generous measure (max ~65ch).

## Layout & spacing

- 12-column grid, max content width 1280–1440 px; page gutters 24–48 px.
- Section rhythm: 120–180 px vertical padding between sections on desktop.
  Audi pages feel *slow* — one idea per screen.
- Hairline rules (1 px) separate spec rows and footer columns; no boxes,
  no cards-with-shadows on model pages.
- Border radius: 0–2 px for spec/table UI; CTAs are square or 2 px.
  Rounded "friendly" radii are off-brand.
- Full-bleed hero: 100vw × 90–100vh, headline anchored low-left with
  48–96 px clearance from the edge, not centered.
- Imagery: the car breaks the grid — full-bleed, edge to edge. Text blocks
  stay on the grid.

## Components

Shared tokens for every snippet below:

```css
:root {
  --audi-black: #000;
  --audi-white: #fff;
  --audi-silver: #C0C0C0;
  --audi-red: #BB0A30;
  --ink: #0A0A0A;
  --surface: #161616;
  --hairline-dark: #2B2B2B;
  --hairline-light: #E2E2E2;
  --muted: #9A9A9A;
  --paper: #F5F5F5;
  --font: "Archivo", "Helvetica Neue", Arial, sans-serif;
}
```

### 1. Rings mark (inspired, not the official logo)

Four interlinked rings, simplified — draw in SVG, never hotlink Audi assets.
The real mark has a precise interlace weave; this is an approximation.

```html
<svg class="rings" width="76" height="24" viewBox="0 0 76 24" aria-label="Four rings">
  <g fill="none" stroke="currentColor" stroke-width="2.6">
    <circle cx="14" cy="12" r="10.5"/>
    <circle cx="32.6" cy="12" r="10.5"/>
    <circle cx="51.2" cy="12" r="10.5"/>
    <circle cx="69.8" cy="12" r="10.5"/>
  </g>
</svg>
```

Use in monochrome only: white on black, black on white.

### 2. Header / nav

Black bar, rings left, quiet uppercase links, one restrained CTA.

```html
<header class="audi-nav">
  <a class="brand" href="#">
    <svg class="rings" width="68" height="22" viewBox="0 0 76 24" aria-label="Four rings">
      <g fill="none" stroke="#fff" stroke-width="2.6">
        <circle cx="14" cy="12" r="10.5"/><circle cx="32.6" cy="12" r="10.5"/>
        <circle cx="51.2" cy="12" r="10.5"/><circle cx="69.8" cy="12" r="10.5"/>
      </g>
    </svg>
  </a>
  <nav>
    <a href="#">Models</a><a href="#">Electric</a>
    <a href="#">Technology</a><a href="#">Company</a>
  </nav>
  <a class="cta-quiet" href="#">Book a test drive</a>
</header>
```

```css
.audi-nav {
  display: flex; align-items: center; justify-content: space-between;
  padding: 0 48px; height: 72px; background: var(--audi-black); color: #fff;
}
.audi-nav nav { display: flex; gap: 40px; }
.audi-nav nav a {
  color: #fff; text-decoration: none; font-size: 13px;
  letter-spacing: .14em; text-transform: uppercase;
}
.audi-nav nav a:hover { color: var(--audi-silver); }
.cta-quiet {
  color: #fff; text-decoration: none; font-size: 13px; letter-spacing: .14em;
  text-transform: uppercase; border: 1px solid #fff; padding: 12px 24px;
}
.cta-quiet:hover { background: #fff; color: #000; }
```

### 3. Full-bleed hero

Dark, edge-to-edge, headline low-left. No centered pill buttons.

```html
<section class="hero">
  <div class="hero-media"><!-- full-bleed car image or CSS/SVG art --></div>
  <div class="hero-copy">
    <p class="eyebrow">The new Audi A9 e-tron</p>
    <h1>Vorsprung<br>durch Technik.</h1>
    <div class="hero-links">
      <a class="link-arrow" href="#">Explore the A9 e-tron</a>
      <a class="link-arrow" href="#">Book a test drive</a>
    </div>
  </div>
</section>
```

```css
.hero { position: relative; height: 100vh; min-height: 640px; background: var(--ink); color: #fff; }
.hero-media { position: absolute; inset: 0; }
.hero-media img { width: 100%; height: 100%; object-fit: cover; }
.hero-copy { position: absolute; left: 48px; bottom: 96px; max-width: 640px; }
.eyebrow { font-size: 12px; letter-spacing: .18em; text-transform: uppercase; color: var(--audi-silver); margin: 0 0 24px; }
.hero h1 { font-weight: 300; font-size: clamp(48px, 7vw, 110px); line-height: 1.02; letter-spacing: -.01em; margin: 0 0 40px; }
.link-arrow { color: #fff; text-decoration: none; font-size: 15px; margin-right: 40px; }
.link-arrow::after { content: " →"; }
.link-arrow:hover { color: var(--audi-red); }
```

### 4. Stat strip (technical figures)

```html
<div class="stats">
  <div class="stat"><p class="eyebrow">0–100 km/h</p><p class="figure">3.1 <span>s</span></p></div>
  <div class="stat"><p class="eyebrow">Range (WLTP)</p><p class="figure">625 <span>km</span></p></div>
  <div class="stat"><p class="eyebrow">Power</p><p class="figure">500 <span>kW</span></p></div>
  <div class="stat"><p class="eyebrow">Charging</p><p class="figure">320 <span>kW</span></p></div>
</div>
```

```css
.stats { display: grid; grid-template-columns: repeat(4, 1fr); background: var(--audi-black); color: #fff; }
.stat { padding: 56px 48px; border-left: 1px solid var(--hairline-dark); }
.stat:first-child { border-left: none; }
.figure { font-weight: 300; font-size: 56px; margin: 16px 0 0; font-variant-numeric: tabular-nums; }
.figure span { font-size: 18px; color: var(--muted); }
```

### 5. Spec table

```html
<table class="specs">
  <tbody>
    <tr><th>Battery (usable)</th><td>105 kWh</td></tr>
    <tr><th>Power</th><td>500 kW (680 hp)</td></tr>
    <tr><th>0–100 km/h</th><td>3.1 s</td></tr>
    <tr><th>Range (WLTP)</th><td>625 km</td></tr>
    <tr><th>Top speed</th><td>250 km/h</td></tr>
    <tr><th>DC charging</th><td>320 kW · 10–80% in 18 min</td></tr>
  </tbody>
</table>
```

```css
.specs { width: 100%; border-collapse: collapse; font-size: 16px; }
.specs tr { border-bottom: 1px solid var(--hairline-dark); }
.specs th { text-align: left; font-weight: 400; color: var(--muted); padding: 20px 0; width: 55%; }
.specs td { text-align: right; font-variant-numeric: tabular-nums; padding: 20px 0; }
```

### 6. Trim selector (tabs)

Underline tabs, no pill shapes; active tab gets a 2 px white underline.

```html
<div class="trims" role="tablist">
  <button class="trim is-active" role="tab" aria-selected="true">A9 e-tron</button>
  <button class="trim" role="tab" aria-selected="false">A9 e-tron performance</button>
  <button class="trim" role="tab" aria-selected="false">A9 e-tron RS</button>
</div>
```

```css
.trims { display: flex; gap: 48px; border-bottom: 1px solid var(--hairline-dark); }
.trim {
  background: none; border: none; color: var(--muted); cursor: pointer;
  font: 400 15px/1 var(--font); letter-spacing: .1em; text-transform: uppercase;
  padding: 0 0 20px;
}
.trim.is-active { color: #fff; box-shadow: inset 0 -2px 0 #fff; }
.trim:hover { color: #fff; }
```

### 7. Model card (lineup grid)

Image, name in light type, one-line fact, arrow link. No shadow, no rounded
corners.

```html
<article class="model-card">
  <img src="a9.jpg" alt="Audi A9 e-tron side profile">
  <h3>Audi A9 e-tron</h3>
  <p>625 km range. From €84,900.</p>
  <a class="link-arrow" href="#">Configure</a>
</article>
```

```css
.model-card img { width: 100%; aspect-ratio: 16/9; object-fit: cover; display: block; }
.model-card h3 { font-weight: 300; font-size: 32px; margin: 28px 0 8px; }
.model-card p { color: var(--muted); margin: 0 0 20px; }
```

### 8. Footer

Dark, thin top border, columns of quiet links, legal line in small gray.

```html
<footer class="audi-footer">
  <div class="foot-grid">
    <div><p class="eyebrow">Models</p><a href="#">A9 e-tron</a><a href="#">Q6 e-tron</a></div>
    <div><p class="eyebrow">Services</p><a href="#">Test drive</a><a href="#">Find a dealer</a></div>
    <div><p class="eyebrow">Company</p><a href="#">About Audi</a><a href="#">Careers</a></div>
  </div>
  <p class="legal">© 2026 Audi-inspired demo. Built from the audi-brand skill · design-skills</p>
</footer>
```

```css
.audi-footer { background: var(--audi-black); color: #fff; padding: 96px 48px 48px; border-top: 1px solid var(--hairline-dark); }
.foot-grid { display: grid; grid-template-columns: repeat(3, 1fr); gap: 48px; margin-bottom: 80px; }
.audi-footer a { display: block; color: var(--muted); text-decoration: none; font-size: 15px; margin-top: 16px; }
.audi-footer a:hover { color: #fff; }
.legal { font-size: 12px; color: #666; border-top: 1px solid var(--hairline-dark); padding-top: 32px; }
```

## Motion

No signature motion language is publicly documented — keep it restrained:
200–300 ms `ease-out` fades and 8–16 px vertical drifts on scroll-in; instant,
precise hover states (color/underline only, no bounce, no scale tricks). ⚠️

## Do / Don't

- **Do** set headlines in light weight (300–400), sentence case, large and
  left-aligned. **Don't** use bold, uppercase, or centered shout-headlines.
- **Do** reserve Audi Red for exactly one focal point per view (e.g. the RS
  badge or the "Reserve" link). **Don't** scatter red across buttons, icons,
  and dividers.
- **Do** build spec tables with 1 px hairlines, tabular figures, and units in
  small gray type. **Don't** put specs in chunky cards with shadows.
- **Do** give sections 120 px+ of vertical air. **Don't** fill whitespace
  with filler graphics or icon rows.
- **Do** render the rings in solid monochrome (white on black / black on
  white). **Don't** recolor, gradient-fill, or 3-D-ify the rings.
- **Do** write CTAs as quiet text links with arrows (`Explore the A9 e-tron →`)
  or thin-bordered rectangles. **Don't** use pill-shaped gradient buttons.
- **Do** show the car full-bleed in motion or architectural settings.
  **Don't** float product shots on decorative gradient backgrounds.

## Copy voice (for brand styles)

Confident, technical, minimal. Facts first, adjectives rare, never an
exclamation mark. Short declarative sentences; the engineering is the message.

- "Vorsprung durch Technik."
- "625 kilometers. One charge. Zero compromise."
- "Book a test drive. The numbers speak quietly."
