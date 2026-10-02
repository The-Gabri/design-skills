---
name: swiss-international
description: Swiss / International Typographic Style (1950s–60s Zurich & Basel schools) — mathematical grids, grotesque type as image, asymmetric layouts, black/white plus one red accent. Use for poster-like pages, editorial layouts, schedules, and anything that must communicate objectively and read at a glance.
---

# Swiss International

The International Typographic Style of 1950s–60s Switzerland: Zurich School of
Arts and Crafts (Ernst Keller, Josef Müller-Brockmann) and Basel School of
Design (Armin Hofmann, Emil Ruder). Max Miedinger's Helvetica (1957) and
Adrian Frutiger's Univers (1957) made the grotesque the voice of the style.
It spread as the global default for corporate identity, wayfinding, and
editorial design — and still underpins flat, grid-first UI design.

## Principles

1. **The grid is the design.** Every layout begins with a mathematical,
   modular grid — Müller-Brockmann called it "the most legible and harmonious
   means for structuring information." Margins, columns, baselines, and white
   space all derive from one module. If an element cannot sit on the grid, it
   does not exist.
2. **Objectivity over expression.** The designer is not an artist but a
   neutral conduit of information (Müller-Brockmann: design as a "socially
   useful and important activity"). No decoration, no illustration where
   objective photography or pure type will do. Serious, rational, clear.
3. **Typography is the image.** Headlines are set at poster scale and carry
   the whole composition — letterforms *are* the visual material. Type is
   never decorated; it is sized, spaced, and placed with intent.
4. **Asymmetric balance.** Compositions are deliberately off-center —
   weight is distributed across the grid, never mirrored. Asymmetry on a
   strict grid reads dynamic but stays orderly.
5. **Clarity is universal.** One typeface family, one accent color, flush-left
   ragged-right text that never breaks into decoration. The style was built
   to communicate across Switzerland's four languages without ambiguity.
6. **White space is active material.** Blank grid cells are compositional
   decisions, not leftovers (Ruder, *Typographie*, 1967). Crowding is a
   failure of hierarchy.

## Color

Black, white, and a single red. Grays exist only as photographic halftones,
never as UI tones.

| Token | Hex | Role | Legend |
|---|---|---|---|
| `--paper` | `#FFFFFF` | Page background | ✅ |
| `--ink` | `#000000` | Text, type-as-image, rules | ✅ |
| `--red` | `#FF0000` | The single accent: rules, blocks, numerals | 🟡 |
| `--red-deep` | `#EE1C25` | Print-substitute for `--red` on dense ink areas | ⚠️ |
| `--hairline` | `#111111` | 1px rules and dividers (on paper, reads as hairline) | 🟡 |

Notes: the Swiss formula is documented as "black and white with
occasional red" (designhistory.org, Wikipedia). There is no official hex —
pure poster red is the convention; `#EE1C25` approximates how that red prints.
Never add a second accent. Never tint surfaces gray.

## Typography

- **Faces (documented):** Helvetica (Miedinger, 1957) ✅, Akzidenz-Grotesk
  (Berthold, 1896) ✅, Univers (Frutiger, 1957) ✅. One grotesque per
  composition — never mix two.
- **Free substitutes (author's recommendation):** "Inter Tight" for
  headlines (its tightened construction sits closest to Helvetica Bold) and
  "Archivo" for body — both Google Fonts. ⚠️
- **Alignment:** flush left, ragged right — always. Centered and justified
  type violate the style. ✅
- **Scale:** poster headlines at 8–20× body size; hierarchy comes from size
  and position, not from color or italics.
- **Leading:** display 0.85–1.0, body 1.35–1.5, captions 1.4.
- **Weights:** 400 (text), 500/700 (headlines), 900 (oversized numerals and
  poster words). No light weights for body, no italics for emphasis.
- **Case:** sentence case for text; oversized lowercase is a legitimate
  poster device (Müller-Brockmann's Beethoven poster, 1955).

## Layout & spacing

- **Grid:** 8- or 12-column modular grid. Desktop: content starts on an
  inner column (e.g. column 3 of 8) for asymmetry; one oversized element
  crosses columns.
- **Spacing scale:** multiples of a single base unit — `8px` (`--u`).
  Margins, gutters, and type sizes are multiples of `--u` (8, 16, 24, 32, 64,
  128…). 16px/24px gutters, 64px+ section rhythm on desktop.
- **Radius:** `0` everywhere. Corners are never rounded.
- **Rules:** 1px hairlines (`--ink` at 1px) separate rows, sections, and
  table cells. A single 8–16px red rule or red block marks the one accent
  moment per view.
- **Imagery:** objective photography (documentary, un-stylized) or no image
  at all. Cropping follows the grid; images never bleed past their module.

## Components

All snippets assume these tokens and drop straight into a page:

```css
:root{
  --paper:#FFFFFF; --ink:#000000; --red:#FF0000;
  --u:8px; --gutter:24px;
  --font:"Inter Tight","Archivo","Helvetica Neue",Helvetica,Arial,sans-serif;
}
*{box-sizing:border-box;margin:0}
body{font-family:var(--font);background:var(--paper);color:var(--ink)}
.swiss-grid{max-width:1200px;margin:0 auto;padding:0 var(--gutter);
  display:grid;grid-template-columns:repeat(12,1fr);gap:var(--gutter)}
```

**1 — Poster header (masthead + edition line)**

```html
<header class="swiss-grid" style="padding-top:64px;padding-bottom:64px">
  <div style="grid-column:1/9">
    <p class="kicker">International symposium on typographic design</p>
    <h1 class="poster">Rastersysteme<br>2027</h1>
  </div>
  <div style="grid-column:9/13;text-align:left">
    <p class="edition">No. 09</p>
    <div class="red-rule"></div>
    <p class="meta">Zürich<br>14–16 May 2027</p>
  </div>
</header>
```

```css
.kicker{font-size:13px;font-weight:700;letter-spacing:.12em;text-transform:uppercase}
.poster{font-size:clamp(64px,11vw,168px);font-weight:900;line-height:.86;
  letter-spacing:-.02em;text-transform:lowercase}
.edition{font-size:64px;font-weight:900;line-height:1;color:var(--red)}
.red-rule{height:12px;background:var(--red);margin:16px 0}
.meta{font-size:15px;line-height:1.4}
```

**2 — Grid hero (asymmetric, type as image)**

```html
<section class="swiss-grid" style="padding:96px 24px">
  <h2 style="grid-column:3/11" class="hero-line">Typography<br>is image.</h2>
  <p style="grid-column:3/7" class="lede">Three days on grids, grotesques,
  and the discipline of the objective poster.</p>
</section>
```

```css
.hero-line{font-size:clamp(48px,8vw,120px);font-weight:900;line-height:.9;
  letter-spacing:-.02em}
.lede{font-size:20px;line-height:1.4;margin-top:32px;max-width:34ch}
```

**3 — Nav (tabular index row)**

```html
<nav class="swiss-grid swiss-nav">
  <a href="#" style="grid-column:1/3">Raster&shy;systeme</a>
  <a href="#" style="grid-column:4/6">Programme</a>
  <a href="#" style="grid-column:6/8">Speakers</a>
  <a href="#" style="grid-column:8/10">Tickets</a>
  <a href="#" style="grid-column:11/13">Zürich ↗</a>
</nav>
```

```css
.swiss-nav{border-top:1px solid var(--ink);border-bottom:1px solid var(--ink);
  padding-top:12px;padding-bottom:12px}
.swiss-nav a{color:var(--ink);text-decoration:none;font-size:14px;font-weight:700}
.swiss-nav a:hover{color:var(--red)}
```

**4 — Timetable table (the Swiss signature)**

```html
<table class="timetable">
  <thead><tr><th>Time</th><th>Session</th><th>Room</th></tr></thead>
  <tbody>
    <tr><td class="tnum">09:00</td><td>Opening: the grid as contract</td><td>A</td></tr>
    <tr><td class="tnum">10:30</td><td>Akzidenz-Grotesk at 125</td><td>A</td></tr>
  </tbody>
</table>
```

```css
.timetable{width:100%;border-collapse:collapse;font-size:15px}
.timetable th{font-size:12px;text-transform:uppercase;letter-spacing:.1em;
  text-align:left;border-bottom:2px solid var(--ink);padding:8px 12px 8px 0}
.timetable td{border-bottom:1px solid var(--ink);padding:14px 12px 14px 0;
  vertical-align:top}
.tnum{font-weight:900;font-variant-numeric:tabular-nums;white-space:nowrap}
```

**5 — Oversized numeral block**

```html
<div class="swiss-grid" style="padding:64px 24px">
  <div style="grid-column:1/5"><span class="bignum">03</span></div>
  <div style="grid-column:5/11"><h3>Days. One grid.</h3>
    <p>Every session, meal, and poster is set on the same 12-column module.</p></div>
</div>
```

```css
.bignum{font-size:clamp(96px,14vw,220px);font-weight:900;line-height:.8;
  letter-spacing:-.03em}
.bignum.red{color:var(--red)}
```

**6 — Caption block (photo, objective)**

```html
<figure class="swiss-grid" style="padding:0 24px">
  <img src="poster-hall.jpg" alt="Turbinenhalle during the 2026 edition"
       style="grid-column:1/13;width:100%;display:block">
  <figcaption style="grid-column:1/6" class="caption">Turbinenhalle, Zürich.
    1,400 seats. Photograph, unretouched.</figcaption>
</figure>
```

```css
.caption{font-size:13px;line-height:1.4;margin-top:12px;max-width:32ch}
```

**7 — CTA button (square, black)**

```html
<a class="swiss-btn" href="#">Get tickets — CHF 240</a>
<a class="swiss-btn red" href="#">Student — CHF 90</a>
```

```css
.swiss-btn{display:inline-block;background:var(--ink);color:var(--paper);
  font-weight:700;font-size:15px;padding:16px 32px;text-decoration:none}
.swiss-btn.red{background:var(--red)}
.swiss-btn:hover{background:var(--ink);color:var(--red)}
.swiss-btn.red:hover{color:var(--paper)}
```

**8 — Hairline list (index of names)**

```html
<ul class="index">
  <li><span class="idx">01</span>Josef Müller-Brockmann <span class="tag">Grid systems</span></li>
  <li><span class="idx">02</span>Armin Hofmann <span class="tag">Poster as sign</span></li>
</ul>
```

```css
.index{list-style:none;padding:0}
.index li{border-top:1px solid var(--ink);padding:16px 0;font-size:20px;
  font-weight:700;display:flex;gap:24px;align-items:baseline}
.index li:last-child{border-bottom:1px solid var(--ink)}
.idx{color:var(--red);font-weight:900;font-size:14px;min-width:32px}
.tag{margin-left:auto;font-size:13px;font-weight:400}
```

**9 — Red accent panel**

```html
<aside class="red-panel">
  <p>Registrations close<br>30 April 2027.</p>
</aside>
```

```css
.red-panel{background:var(--red);color:var(--paper);padding:48px;
  font-size:32px;font-weight:900;line-height:1.1;max-width:420px}
```

**10 — Colophon footer**

```html
<footer class="swiss-grid" style="padding:64px 24px 32px">
  <p style="grid-column:1/5" class="colophon">Set in Inter Tight.<br>
  Grid: 12 columns, 24 px gutter.<br>Printed in black and red.</p>
  <p style="grid-column:9/13" class="colophon">Rastersysteme 2027<br>
  Geroldstrasse 5, 8005 Zürich</p>
</footer>
```

```css
.colophon{font-size:13px;line-height:1.5}
```

## Motion

Swiss print has no motion language — on screen, use near-instant cuts
(≤150 ms, no easing flourish) or nothing at all.

## Do / Don't

- **Do** start every composition with the grid; align type, images, and
  rules to the same columns.
  **Don't** eyeball placement or let two elements sit "almost" aligned.
- **Do** set headlines at poster scale — type is the image.
  **Don't** shrink the headline and add a decorative hero illustration.
- **Do** align text flush left, ragged right.
  **Don't** center headlines or justify body copy — both violate the style.
- **Do** use one red block or rule as the single chromatic event.
  **Don't** introduce a second accent color, tinted surfaces, or gray text.
- **Do** separate information with 1px hairlines (timetables, indexes).
  **Don't** use cards, rounded corners, or drop shadows.
- **Do** write captions and labels as flat statements of fact.
  **Don't** add marketing adjectives — "objective" means objective.
- **Do** leave whole grid modules empty.
  **Don't** fill white space because it feels bare — it is doing work.

## Copy voice

Objective, terse, present tense. Facts, not persuasion. Prices and times
are part of the copy, not footnotes.

- "Typography is image. Three days on grids, grotesques, and the discipline of the objective poster."
- "Doors 20:00. Concert 21:00. Admission CHF 25. No reservations."
- "Registrations close 30 April. The programme is final."
