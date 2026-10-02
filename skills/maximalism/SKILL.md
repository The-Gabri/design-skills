---
name: maximalism
description: Maximalism — "more is more" web design: clashing saturated color, mixed CSS patterns, oversized stacked typography, sticker collages, rotated badges and layered compositions kept readable by a strict grid. Use for streetwear drops, music festivals, rave flyers, youth brands, and culture sites where energy beats calm.
---

# Maximalism

Also called *dopamine design* / *"more is more"*. Maximalism is the deliberate,
curated overload of color, pattern, type and imagery — a reaction against a
decade of flat minimal UI. Lineage: Victorian ornament → 1960s psychedelic
posters (Wes Wilson, Victor Moscoso) → Memphis Group → 1990s rave flyers →
today's brand-led e-commerce and culture sites. 🟡

The core paradox: **abundance in content, order in structure.** Density is the
aesthetic; the discipline is keeping one calm, readable voice inside the noise.
✅ (consistent across all cross-referenced sources)

## Verification legend

- ✅ = consistent across ≥2 independent sources.
- 🟡 = documented in one source + corroborated by observed real-world maximalist sites.
- ⚠️ = community recipe / useful convention, not documented dogma.

## Principles

1. **Joy and energy over calm.** The page should feel like a party invitation,
   not a dashboard. If an element can be louder, make it louder. ✅
2. **Curated chaos: a grid keeps it usable.** Overlapping collage, rotations and
   clashing colors sit on top of a rigid underlying grid. Rotations and
   overlaps are deliberate (stickers, badges), never the text the user must
   read. ✅
3. **One dominant idea per screen/section.** Hero is the loudest; supporting
   sections rank quieter. Exactly one element may break the grid per section.
   ✅ (agent-design-taste source)
4. **Layered planes, not scattered mess.** Background pattern → mid decorative
   layer → razor-sharp readable foreground. Pattern + color + type stack in
   deliberate depth planes. ✅
5. **Personality in every component.** Buttons, badges, cards and dividers all
   get a voice — chunky borders, hard offset shadows, stamped labels. 🟡
6. **Surprise on every scroll.** Sections change color, pattern and energy;
   tickers, starbursts and stickers reward continued scrolling. ✅

## Color

A loud, clashing set on warm paper, anchored by near-black outlines and text.
The canonical maximalist recipe (from the specimen/maximalism.md source, ✅):

| Token | Hex | Role |
|---|---|---|
| `paper` | `#FFF4D6` | background (warm cream, never stark white) ✅ |
| `ink` | `#140A1F` | text, outlines, borders ✅ |
| `pink` | `#FF2E88` | primary accent (hot pink) ✅ |
| `blue` | `#2B59FF` | secondary accent (electric blue) ✅ |
| `lime` | `#C6FF00` | highlight (acid lime) ✅ |
| `tang` | `#FF7A00` | highlight (tangerine) ✅ |

Recipes and rules:

- **Clash recipe:** 4+ saturated colors visible in one viewport — the "four or
  more" rule is the recognizability test. ✅
- **Anchoring rule:** every loud color must touch `ink` — via a 2–3px ink
  border, hard ink offset shadow, or ink text. The bold outline is what holds
  the chaos together. ✅
- **Palette cap:** base (`paper` + `ink`) + max 4 saturated accents. More hues
  than that reads as random, not curated. ⚠️
- **Contrast discipline:** body text and primary CTAs must hold WCAG AA (4.5:1
  for body text). Loudness never excuses unreadable text. ✅
- **Chaos mode recipe (alternate palette, for toggles):** swap `paper`→`#1A0B2E`
  (plum-black), keep the same 4 accents, swap `ink` text to `paper`. 🟡
- Section-background rotation: alternate full-bleed saturated color fields per
  section (`pink` → `blue` → `lime` → `tang`), with `paper` "breather" sections
  between the loudest ones. ⚠️

## Typography

Maximalism needs **one calm voice amid the noise**: one expressive display
face for headlines + one disciplined text face for body. Max 3 families, sharply
contrasted by classification. ✅

- **Display:** extra-bold condensed grotesques — free substitutes: `Archivo
  Black`, `Anton`, or the system stack `Impact, "Arial Black", sans-serif`
  (heavy weight is the point). Usage: headlines, marquee text, prices. 🟡
- **Body:** a neutral grotesque — `Archivo`, `Inter`, or system stack. Plain
  16–17px, generous line-height. This is the calm voice; never set paragraphs
  in the display face. ✅
- **Stamp/label:** a monospace or condensed uppercase face — `Space Mono`,
  `IBM Plex Mono`, or system `ui-monospace` — for kicker labels, badges,
  prices, dates. Uppercase, letterspaced. 🟡

Type-scaling rules:

- **Hero headline:** `clamp(3.5rem, 12vw, 11rem)`, weight 900, tight leading
  (0.9–1.0). ✅
- **Stacked multi-color lines:** split the headline across 2–4 lines; give each
  line a different accent color and/or background chip; outline or
  multi-shadow on top. Rotating one word (`-3deg`) is the classic trick. 🟡
- **Background mega-type:** `12rem`–`20rem`, single impactful word (WOW, YES,
  the brand name), `opacity: 0.12–0.2`, absolutely positioned and bleeding off
  an edge — adds depth without competing. 🟡
- **Multi-shadow headline treatment:** `text-shadow: 3px 3px 0 ink, 6px 6px 0
  accent` — layered, not blurred. 🟡
- **Line-length cap:** display type may break the grid; body copy stays on it
  (45–75 chars/line). ⚠️

## Layout & spacing

- **Strict grid underneath:** 12-column (or 6) grid; cards and text align to
  it. Rotated stickers and badges are absolutely positioned *over* the grid —
  they decorate, they don't lay out. ✅
- **Intentional overlap:** floating shapes/badges get higher `z-index` to sit
  above content edges; 60/40 asymmetric splits beat 50/50. 🟡
- **Density:** high, deliberately. Sections carry 5–10 decorative shapes each.
  But exactly **one grid-breaking element per section max**. ✅
- **Borders:** 2–3px solid `ink` everywhere (cards, images, buttons, inputs).
  Borders are structural glue. ✅
- **Shadows:** hard offset only — `4px 4px 0 ink` (hero elements up to
  `8px 8px 0 ink`). **Never soft blur shadows.** ✅
- **Radii — intentionally mixed:** stickers = pill/full round; cards = 0 or
  slight; starbursts = spiky. Mixed radii per layer is part of the language;
  within one component, stay consistent. 🟡
- **Dividers:** zigzag / torn-paper / thick stripe borders between sections
  (CSS: `repeating-linear-gradient` or SVG). 🟡

## Patterns (the texture layer)

Patterns are built with CSS (gradients/SVG data-URIs), never images. Every
section gets ≥1; hero gets ≥2 overlapping at low individual opacity. 🟡

```css
/* Checkerboard — the maximalist workhorse */
.pattern-checker {
  background-image:
    linear-gradient(45deg, rgba(20,10,31,.08) 25%, transparent 25%,
      transparent 75%, rgba(20,10,31,.08) 75%),
    linear-gradient(45deg, rgba(20,10,31,.08) 25%, transparent 25%,
      transparent 75%, rgba(20,10,31,.08) 75%);
  background-size: 32px 32px;
  background-position: 0 0, 16px 16px;
}

/* Halftone dots */
.pattern-dots {
  background-image: radial-gradient(rgba(20,10,31,.14) 2.5px, transparent 2.6px);
  background-size: 22px 22px;
}

/* Diagonal stripes */
.pattern-stripes {
  background-image: repeating-linear-gradient(-45deg,
    rgba(255,46,136,.16) 0 14px, transparent 14px 28px);
}
```

Rules: share one palette across patterns (recolored `ink` at low opacity);
keep pattern opacity low (0.05–0.16) under text; layer 2 patterns on the hero;
never put body text over a high-contrast pattern without an ink/paper chip
behind it. 🟡

## Components

### 1. Marquee ticker

```html
<div class="ticker" aria-hidden="true">
  <div class="ticker-track">
    <span>FREE SHIPPING OVER €80</span><span class="tick-star">★</span>
    <span>DROP 004 LIVE NOW</span><span class="tick-star">★</span>
    <!-- repeat the set twice for a seamless loop -->
  </div>
</div>
```

```css
.ticker { background: #140A1F; color: #FFF4D6; border-top: 3px solid #140A1F;
  border-bottom: 3px solid #140A1F; overflow: hidden; white-space: nowrap; }
.ticker-track { display: inline-block; padding: .6rem 0;
  font: 900 1.1rem "Archivo Black", Impact, sans-serif; letter-spacing: .04em;
  animation: tick 22s linear infinite; }
.ticker-track span { margin: 0 1.2rem; }
.tick-star { color: #C6FF00; }
@keyframes tick { to { transform: translateX(-50%); } }
.ticker:hover .ticker-track { animation-play-state: paused; }
@media (prefers-reduced-motion: reduce) { .ticker-track { animation: none; } }
```

### 2. Sticker badge (die-cut, rotated)

```html
<span class="sticker" style="--rot:-6deg">NEW DROP</span>
```

```css
.sticker { display: inline-block; background: #C6FF00; color: #140A1F;
  font: 900 .85rem "Space Mono", ui-monospace, monospace; letter-spacing: .08em;
  padding: .55rem 1rem; border: 3px solid #140A1F; border-radius: 999px;
  box-shadow: 4px 4px 0 #140A1F; transform: rotate(var(--rot, -4deg));
  text-transform: uppercase; }
.sticker:hover { animation: wiggle .4s ease-in-out; }
@keyframes wiggle { 25%{transform:rotate(calc(var(--rot) - 4deg))}
  75%{transform:rotate(calc(var(--rot) + 4deg))} }
```

### 3. Starburst badge (SVG, no images)

```html
<div class="burst"><svg viewBox="0 0 120 120" aria-hidden="true">
  <polygon points="60,2 72,28 100,18 92,46 118,54 96,68 108,94 80,88 70,116
    60,90 48,116 40,88 12,94 24,68 2,54 28,46 20,18 48,28"/>
</svg><span>-30%</span></div>
```

```css
.burst { position: relative; width: 110px; height: 110px; }
.burst svg { width: 100%; height: 100%; fill: #FF2E88;
  stroke: #140A1F; stroke-width: 4; animation: spin-slow 14s linear infinite; }
.burst span { position: absolute; inset: 0; display: grid; place-items: center;
  font: 900 1.4rem Impact, "Arial Black", sans-serif; color: #FFF4D6;
  text-shadow: 2px 2px 0 #140A1F; }
@keyframes spin-slow { to { transform: rotate(360deg); } }
```

### 4. Stacked mega headline

```html
<h1 class="mega">
  <span class="line l1">WEAR</span>
  <span class="line l2">THE</span>
  <span class="line l3">NOISE</span>
</h1>
```

```css
.mega { font: 900 clamp(3.5rem, 13vw, 10rem)/0.92 Impact, "Arial Black", sans-serif; }
.mega .line { display: block; }
.l1 { color: #140A1F; text-shadow: 4px 4px 0 #FF2E88; }
.l2 { color: #FFF4D6; background: #2B59FF; display: inline-block;
  padding: 0 .25em; transform: rotate(-2deg);
  text-shadow: 4px 4px 0 #140A1F; }
.l3 { color: transparent; -webkit-text-stroke: 3px #140A1F; }
```

### 5. Chunky CTA button

```html
<a class="btn-loud" href="#">Shop the drop</a>
```

```css
.btn-loud { display: inline-block; background: #FF7A00; color: #140A1F;
  font: 900 1.1rem "Archivo Black", Impact, sans-serif; text-transform: uppercase;
  padding: 1rem 2rem; border: 3px solid #140A1F; box-shadow: 6px 6px 0 #140A1F;
  text-decoration: none; transition: transform .12s, box-shadow .12s; }
.btn-loud:hover { transform: translate(-2px,-2px); box-shadow: 8px 8px 0 #140A1F; }
.btn-loud:active { transform: translate(4px,4px); box-shadow: 0 0 0 #140A1F; }
```

### 6. Patterned product card

```html
<article class="pcard">
  <div class="pcard-img pattern-dots"><span class="sticker" style="--rot:5deg">HOT</span></div>
  <h3>Acid Rain Hoodie</h3>
  <p class="price">€89 <s>€120</s></p>
  <button class="btn-loud btn-small">Add to cart</button>
</article>
```

```css
.pcard { background: #FFF4D6; border: 3px solid #140A1F;
  box-shadow: 8px 8px 0 #140A1F; padding: 0; }
.pcard-img { height: 220px; background-color: #C6FF00; border-bottom: 3px solid #140A1F;
  position: relative; }
.pcard-img .sticker { position: absolute; top: 12px; right: 12px; }
.pcard h3 { font: 900 1.25rem Impact, "Arial Black", sans-serif;
  padding: .8rem 1rem 0; text-transform: uppercase; }
.pcard .price { font: 700 1rem "Space Mono", ui-monospace, monospace; padding: 0 1rem; }
.pcard .btn-small { margin: 0 1rem 1rem; padding: .7rem 1.2rem; font-size: .9rem; }
```

### 7. Chaos-mode toggle

```html
<button id="chaosBtn" class="sticker" aria-pressed="false">CHAOS: OFF</button>
```

```css
body.chaos { --paper: #1A0B2E; --ink: #FFF4D6; }
body.chaos .ticker { background: #FF2E88; color: #140A1F; }
```

```js
document.getElementById('chaosBtn').addEventListener('click', e => {
  const on = document.body.classList.toggle('chaos');
  e.currentTarget.textContent = on ? 'CHAOS: ON' : 'CHAOS: OFF';
  e.currentTarget.setAttribute('aria-pressed', on);
});
```

## Motion

Maximalism has no official motion spec — the conventions below are community
practice. ⚠️

- **Marquee tickers:** `linear infinite`, 18–30s per loop, pause on hover.
- **Wiggle / float:** stickers wiggle on hover (`.4s`); decorative shapes
  float slowly (`6s ease-in-out infinite alternate`, ±8px). 🟡
- **Spin-slow:** starbursts rotate `12–16s linear infinite`.
- **Easing for UI:** chunky `cubic-bezier(.2,.9,.3,1.2)` overshoot on presses;
  no fades — elements pop.
- **Always include** a `prefers-reduced-motion` reset that kills tickers,
  wiggles, spins and floats (static layout must still look intentional). ✅
  (accessibility expectation, not style dogma)

## Do / Don't

- ✅ **Do:** give every section ONE dominant idea, rank loudness (hero >
  manifesto > footer).
  ⚠️ **Don't:** make every section scream at full volume — ranked noise reads
  as designed; uniform noise reads as a bug.
- ✅ **Do:** set body copy in the calm text face at 16–17px on `paper` chips.
  ⚠️ **Don't:** set paragraphs in the display font or over a loud pattern —
  the noise is for headlines, not for reading.
- ✅ **Do:** clash *within* the shared palette (max 4 saturated + ink + paper)
  and anchor each accent with an ink border/shadow.
  ⚠️ **Don't:** introduce random off-palette colors — curated clashing vs.
  accidental clashing is the whole game.
- ✅ **Do:** use hard offset shadows (`4px 4px 0 ink`) to separate the three
  depth planes.
  ⚠️ **Don't:** use soft blur shadows or glassmorphism — maximalism is tactile
  and flat-stacked, never frosted.
- ✅ **Do:** rotate stickers/badges ±2–6°, break the grid once per section.
  ⚠️ **Don't:** rotate body text, buttons or form labels — readable content
  never tilts.
- ✅ **Do:** keep individual pattern opacity at 0.05–0.16 under text; layer
  for cumulative effect. 🟡
  ⚠️ **Don't:** put a high-contrast checker behind a paragraph — readability
  dies before the joke lands.
- ✅ **Do:** cap type at 3 families, contrasted by classification
  (display / text / stamp).
  ⚠️ **Don't:** add a fourth "fun" font for one heading.
- ✅ **Do:** write copy like a hype-person with a megaphone (see below).

## Copy voice

Loud, exclamatory, conspiratorial hype — a friend dragging you to the best
party. Short punchy lines. CAPS for emphasis, never whole paragraphs. Playful
imperatives ("grab it", "don't sleep on this"), insider slang, starbursts for
urgency ("SELLING FAST"). Zero corporate polish; zero lorem ipsum.

Examples:

- "DROP 004 IS LIVE. 200 hoodies. When they're gone, they're gone — no restocks, no mercy."
- "WEAR THE NOISE. Our loudest collection yet: acid colors, zero apologies."
- "Join 40,000 loud humans. First dibs, secret drops, 10% off — straight to your inbox."

## When NOT to use

Finance, healthcare, legal, government services, or anything where trust =
calm and a misread costs money or health. Maximalism buys attention with
readability risk — spend that budget only where the product wants energy.
🟡

## Sources

- ujjwal-gowda/specimen — `public/design-md/maximalism.md`: palette
  (cream #FFF4D6, ink #140A1F, hot pink #FF2E88, electric blue #2B59FF, acid
  lime #C6FF00, tangerine #FF7A00), lineage, recognizability rules.
- aievolutionpl/agent-design-taste — `styles/12-maximalism/`: layered planes,
  strict grid, one dominant idea per screen, hard offset shadows,
  prefers-reduced-motion reset, max 3 type families.
- shekhsahebali/ux-ux-skills — `maximalism/SKILL.md`: use-cases and
  anti-use-cases, "more is more" philosophy.
- Observed consensus across maximalist brand/festival sites (sticker badges,
  tickers, starbursts, mega background type): community convention.
