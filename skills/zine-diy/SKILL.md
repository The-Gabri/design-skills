---
name: zine-diy
description: DIY punk zine / photocopy aesthetic — ransom-note type, cut-and-paste collage, high-contrast B/W, tape and staples. Use for show flyers, fanzines, protest ephemera, and anything that should look made at 2am on a borrowed copier.
---

# Zine DIY (Punk / Photocopy Aesthetic)

The look of the underground press: fanzines run off on a Xerox at the
library, hardcore show flyers wheat-pasted over each other, riot grrrl
cut-and-paste manifestos. The reference canon is **Sniffin' Glue**
(Mark P., 1976), **Ripped & Torn** (1976–79), **Chainsaw** (1977) —
stencil titles, newspaper cutouts collaged with band photos — and Jamie
Reid's cut-letter artwork for the Sex Pistols (1977). The aesthetic is
inseparable from its production process: photocopy degradation, visible
scissor marks, tape residue, torn edges are not decoration, they are the
medium.

## Legend

- ✅ = documented in historical zine scholarship or surviving artifacts,
  confirmed in ≥2 sources.
- 🟡 = cross-referenced across community zine references / design
  analyses, consistent but no single canonical source.
- ⚠️ = community approximation — useful, not dogma.

## Principles

1. **The copier is the designer.** High-contrast B/W reproduction, toner
   speckle, edge falloff, and overcopied blacks are the core texture.
   Simulate the machine, not "grunge". ✅ (black-and-white photocopying
   as the defining reproduction method of zine culture — Duncombe,
   *Notes from Underground*; Triggs, *Scissors and Glue*)
2. **Cut, don't set.** Display type is physically cut from other
   publications and pasted down: mismatched faces, sizes, weights, and
   baselines inside a single word. ✅ (ransom-note / cut-n-paste
   typography documented across Sniffin' Glue, Chainsaw, Ripped & Torn)
3. **One hand made all of this.** The chaos is coherent: at most 3
   display faces per composition, rotation capped at ±8°, baselines
   nudged but never randomized per render. The maker's hand is visible
   and consistent. 🟡
4. **Reading copy stays boring on purpose.** Body text, dates, prices,
   addresses are dead level, one plain face, zero rotation. The chaos
   never touches anything longer than ~8 words or anything that must be
   read at a glance. 🟡
5. **Marks of making are load-bearing.** Tape strips, staples, scissor
   cuts, hand-drawn underlines, margin scribbles, stamps — these are the
   shadows and borders of this style. A zine page without them is just
   ugly; with them it's a zine. 🟡
6. **Constraint is the aggression.** Black + white + exactly one accent.
   No four-color process, no gradients, no soft shadows — punk was made
   on photocopiers and with found materials. You get what the machine
   gives you. ✅

## Color

Photocopiers print black on paper. Everything else is either the paper
showing through or a single found accent (one highlighter, one stamp
pad, one red pen).

| Token | Hex | Role | Confidence |
|---|---|---|---|
| `ink` | `#111111` | Text, cut letters, rules. Never pure `#000` — toner blooms. | 🟡 cross-referenced |
| `ink-deep` | `#0A0A0A` | Overcopied blacks, solid fills, stamp ink | 🟡 cross-referenced |
| `paper` | `#F4F1E8` | Aged copy paper / newsprint base | ⚠️ community approximation |
| `paper-fresh` | `#FFFFFF` | Fresh-cut pasted scraps (slightly brighter than the base page) | ⚠️ community approximation |
| `copier-gray` | `#808080` | Incidental midtone: photocopier gray, degraded photo fills | 🟡 cross-referenced |
| `toner-fade` | `#6E6E6E` | Faded type, 10th-generation copy text | ⚠️ community approximation |
| `accent-red` | `#CC0000` | Blood red — the classic single accent (stamp pad, marker) | 🟡 cross-referenced |
| `accent-pink` | `#FF1493` | Hot pink — riot grrrl / flyer accent alternative | 🟡 cross-referenced |
| `accent-yellow` | `#F5FF3D` | Safety yellow — highlighter marker pass | 🟡 cross-referenced |
| `tape` | `rgba(244,240,210,0.55)` | Masking-tape strips over pasted scraps | ⚠️ community approximation |

**Rules:** pick ONE accent per composition and commit. Black text on the
accent; white or paper text on black blocks. The accent appears in at
most ~3 places per spread (stamp, one underline, one headline word).
Never two accents — that's a rave flyer, not a zine.

## Typography

### The type-mixing rules (ransom-note system)

- **Max 3 display faces per composition:** one heavy block face, one
  scrawled marker face, one typewriter/stencil face. Never a fourth.
  🟡
- **Wrap each *word* (never each letter)** in its own span, cycling
  faces across the 3, varying size ±20%. Letters-from-different-
  magazines reads as ransom note; letters-each-different-font reads as
  broken. ✅ (cut-letter words in Jamie Reid's Pistols artwork are
  word-assembled from mixed sources)
- **Rotation and baseline offset must be deterministic** — derived from
  word index, capped at ±8°, never re-randomized per render. A jittering
  headline breaks the "one hand cut all of this" cohesion. 🟡
- **The ransom treatment never touches a run longer than ~8 words.**
  Past that it's a broken layout wearing a costume. 🟡
- **Marker highlighter pass:** a semi-transparent skewed rect behind
  1–2 key words per headline only
  (`background: #F5FF3D; mix-blend-mode: multiply; transform:
  skew(-3deg) rotate(-1deg)`). Behind every word it reads as a filter,
  not a choice. 🟡

### Faces

| Role | Face (free) | Stands in for | Confidence |
|---|---|---|---|
| Heavy block | `Anton`, `Archivo Black` (fallback: `Arial Black`, `Impact`) | Grotesque poster faces, hand-cut headlines | 🟡 cross-referenced |
| Marker scrawl | `Permanent Marker`, `Caveat` (fallback: `cursive`) | Hand annotations, corrections, arrows | 🟡 cross-referenced |
| Typewriter / stencil | `Special Elite`, `Courier New` | Stamps, dates, datelines, classifieds | 🟡 cross-referenced |
| Reading body | System humanist sans (`-apple-system, "Segoe UI", Roboto, …`), 400, `line-height 1.55–1.65` | The legibility anchor — deliberately unstyled | 🟡 community convention |
| Metadata | Typewriter face, uppercase, letterspaced, small, **never rotated** | Timestamps, prices, issue numbers | 🟡 |

Headline case: mixed — ransom words keep their found case. Body:
sentence case. Stamps and datelines: ALL CAPS.

## Layout & spacing

- **The page is a pasteboard.** One slightly-rotated paper sheet on a
  darker desk/background surface, with cut scraps pasted on top —
  overlapping, some rotated ±2–6°, edges torn or scissor-cut. Nothing is
  "aligned to grid"; everything is *placed*. 🟡
- **Density is the point.** Zine pages are packed: narrow gutters
  (8–16px), stacked gig listings, margin notes colonizing whitespace.
  Generous whitespace reads as unfinished, not elegant. ✅ (cluttered,
  overlapping layouts as a documented trait — Ripped & Torn analyses)
- **Radius is 0 everywhere.** Paper doesn't have rounded corners unless
  someone cut them. Tape strips are axis-aligned rectangles. 🟡
- **Cut-paper edge treatments:** torn edges via jagged `clip-path`
  polygons (7–11 points per edge, irregular depths 4–14px); scissor-cut
  edges dead straight but slightly rotated. ⚠️ community technique
- **Overlap order tells the story:** headline scraps on top, tape over
  scrap corners, stamps last (a stamp is pressed *onto* the finished
  collage). Scribbles live in margins and over gutters, never over body
  text they would obscure.
- **One spread, one idea.** A zine page is a single dense composition,
  not a scrolling landing page. Sections are separated by torn strips
  or thick hand-drawn rules, not cards with padding.

## Paper / ink treatments

- **Photocopy grain recipe:** an `feTurbulence`-based SVG noise layer
  over the whole page at low opacity (`0.05–0.09`) with
  `mix-blend-mode: multiply`, plus a global `filter:
  contrast(1.08) brightness(0.99)` on the page to crush midtones the way
  a copier does. ⚠️ community technique
- **Overcopied toggle:** `filter: contrast(1.6) brightness(0.92)`
  blows out midtones into solid blacks (the "too dark" copy); `filter:
  contrast(0.75) brightness(1.12) grayscale(0.2)` gives the washed-out
  "toner low" copy. Both are authentic machine states, not filters.
  ⚠️
- **Degraded photos:** any photo/halftone block gets `filter:
  grayscale(1) contrast(1.8)` — photocopiers only ever saw black and
  white. ✅
- **Tape:** semi-transparent warm beige, 24–36px wide strips at
  ±30–45° across scrap corners, with a 1px darker edge and slight
  `opacity` variance. Real tape yellows: never pure white. ⚠️
- **Staples:** two small metallic-gray rectangles (`#9a9a9a` with a
  darker center line) bridging a scrap edge — the cheapest binding in
  history. ⚠️

## Components

All examples are plain HTML/CSS, copy-pasteable. Assumes tokens as CSS
custom properties (`--ink`, `--paper`, `--accent`, `--tape`).

**1. Ransom-note headline**

```html
<h2 class="zn-ransom" aria-label="Copy this. Burn the original.">
  <span style="--i:0">COPY</span> <span style="--i:1">THIS.</span>
  <span style="--i:2">BURN</span> <span style="--i:3">THE</span>
  <span style="--i:4">ORIGINAL.</span>
</h2>
```

```css
.zn-ransom { font-size: clamp(2.2rem, 6vw, 4.5rem); line-height: 1.02; margin: 0; }
.zn-ransom span {
  display: inline-block;
  padding: 0.04em 0.12em;
  background: var(--paper-fresh, #fff);          /* each word = a cut scrap */
  box-shadow: 1px 2px 0 rgba(0,0,0,0.18);        /* paste shadow, hard */
  transform: rotate(calc((var(--i, 0) % 5 - 2) * 3deg))
             translateY(calc((var(--i, 0) % 3 - 1) * 3px));
}
.zn-ransom span:nth-child(3n)   { font-family: Anton, "Arial Black", Impact, sans-serif; }
.zn-ransom span:nth-child(3n+1) { font-family: "Permanent Marker", cursive; font-size: 0.88em; }
.zn-ransom span:nth-child(3n+2) { font-family: "Special Elite", "Courier New", monospace; font-size: 0.92em; }
.zn-ransom .hl { background: var(--accent, #F5FF3D); } /* 1-2 words max */
```

**2. Photocopy grain overlay**

```html
<svg width="0" height="0" aria-hidden="true">
  <filter id="zn-grain">
    <feTurbulence type="fractalNoise" baseFrequency="0.9" numOctaves="2" stitchTiles="stitch"/>
    <feColorMatrix type="matrix" values="0 0 0 0 0  0 0 0 0 0  0 0 0 0 0  0.6 0.6 0.6 0 0"/>
  </filter>
</svg>
<div class="zn-grain" aria-hidden="true"></div>
```

```css
.zn-grain {
  position: fixed; inset: 0; pointer-events: none; z-index: 60;
  filter: url(#zn-grain);
  opacity: 0.07; mix-blend-mode: multiply;
}
.zn-copied { filter: contrast(1.08) brightness(0.99); } /* the machine's default crush */
```

**3. Torn paper edge**

```html
<article class="zn-torn">
  <p>Manifesto text goes here…</p>
</article>
```

```css
.zn-torn {
  background: var(--paper-fresh, #fff);
  padding: 28px 26px;
  /* jagged tear: irregular points, 4-14px bite depth */
  clip-path: polygon(0% 3%, 4% 0%, 11% 2%, 19% 0%, 27% 3%, 36% 1%, 45% 3%,
    55% 0%, 64% 2%, 73% 0%, 82% 3%, 91% 1%, 98% 3%, 100% 8%, 99% 20%,
    100% 35%, 98% 50%, 100% 66%, 99% 80%, 100% 94%, 93% 100%, 84% 98%,
    74% 100%, 63% 97%, 52% 100%, 41% 98%, 30% 100%, 20% 97%, 10% 100%,
    2% 97%, 0% 90%, 1% 75%, 0% 60%, 2% 45%, 0% 30%, 1% 15%);
  transform: rotate(-1.2deg);
}
```

**4. Masking-tape strip**

```html
<div class="zn-taped">
  <span class="zn-tape tl"></span><span class="zn-tape tr"></span>
  <p>Pasted-down flyer content…</p>
</div>
```

```css
.zn-taped { position: relative; background: var(--paper-fresh, #fff); padding: 24px; }
.zn-tape {
  position: absolute; top: -14px; width: 92px; height: 30px;
  background: var(--tape, rgba(244,240,210,0.55));
  border-left: 1px dashed rgba(0,0,0,0.18);
  border-right: 1px dashed rgba(0,0,0,0.18);
  box-shadow: 0 1px 2px rgba(0,0,0,0.12);
}
.zn-tape.tl { left: 18px; transform: rotate(-38deg); }
.zn-tape.tr { right: 18px; transform: rotate(38deg); }
```

**5. Hand-drawn underline + circle (marker pass)**

```html
<p>We are <span class="zn-u">not asking</span> for permission.</p>
<p>The <span class="zn-circ">third night</span> sold out.</p>
```

```css
.zn-u {
  background: linear-gradient(transparent 62%, var(--accent, #F5FF3D) 62% 92%, transparent 92%);
}
.zn-circ { position: relative; white-space: nowrap; }
.zn-circ::after {
  content: ""; position: absolute; inset: -0.35em -0.5em;
  border: 3px solid var(--accent-red, #CC0000); border-radius: 48% 52% 55% 45% / 55% 48% 52% 45%;
  transform: rotate(-3deg); pointer-events: none;
}
```

**6. Rubber stamp**

```html
<span class="zn-stamp">ALL AGES</span>
<span class="zn-stamp zn-stamp-red">SOLD OUT</span>
```

```css
.zn-stamp {
  display: inline-block; font-family: "Special Elite", "Courier New", monospace;
  font-weight: 700; letter-spacing: 0.12em; text-transform: uppercase;
  color: var(--ink, #111); border: 3px double var(--ink, #111);
  border-radius: 4px; padding: 6px 14px; transform: rotate(-7deg);
  opacity: 0.88; /* stamp ink never lands perfectly */
  mask-image: url("data:image/svg+xml,..."); /* optional: distress via feTurbulence mask */
}
.zn-stamp-red { color: var(--accent-red, #CC0000); border-color: var(--accent-red, #CC0000); }
```

**7. Gig listing (show flyer block)**

```html
<section class="zn-gig">
  <p class="zn-date">FRI OCT 9</p>
  <h3 class="zn-bands">RANSOM NOTE <span>w/</span> COPYCAT KILL</h3>
  <p class="zn-meta">THE BASEMENT · 214 KELLER ST · DOORS 7PM · $8 · <span class="zn-stamp zn-stamp-sm">ALL AGES</span></p>
</section>
```

```css
.zn-gig { border-top: 3px solid var(--ink, #111); padding: 14px 4px 18px; }
.zn-date { font-family: "Special Elite", "Courier New", monospace; font-weight: 700; letter-spacing: 0.08em; margin: 0 0 6px; }
.zn-bands { font-family: Anton, "Arial Black", Impact, sans-serif; font-size: 1.6rem; margin: 0 0 6px; text-transform: uppercase; }
.zn-bands span { font-family: "Permanent Marker", cursive; font-size: 0.7em; text-transform: none; }
.zn-meta { font-family: "Special Elite", "Courier New", monospace; font-size: 0.85rem; margin: 0; }
```

**8. Margin scribble (hand annotation)**

```html
<aside class="zn-note">bring earplugs!! <span>— M.</span></aside>
```

```css
.zn-note {
  font-family: "Permanent Marker", "Segoe Print", cursive;
  color: var(--accent-red, #CC0000);
  transform: rotate(-4deg);
  font-size: 1.05rem; line-height: 1.3; max-width: 180px;
}
.zn-note span { display: block; font-size: 0.8em; color: var(--ink, #111); }
```

**9. Staple**

```html
<div class="zn-stapled"><i class="zn-staple"></i><p>Setlist, night two…</p></div>
```

```css
.zn-stapled { position: relative; background: var(--paper-fresh, #fff); padding: 24px; }
.zn-staple {
  position: absolute; top: 10px; left: 50%; width: 26px; height: 7px;
  background: linear-gradient(#b5b5b5, #8f8f8f);
  border-radius: 2px; transform: translateX(-50%) rotate(2deg);
  box-shadow: 0 1px 1px rgba(0,0,0,0.3);
}
```

## Motion

The photocopier has no motion language. State changes are hard cuts:
`transition: none` on content; interactive states swap instantly
(invert, contrast flip, stamp slam). If anything must move, keep it
mechanical — a linear ticker strip like a cut-paste slogan, `12s linear
infinite`, no easing. `prefers-reduced-motion` changes nothing because
nothing moves.

## Do / Don't

- **Do** build display type from per-word spans cycling ≤3 faces with
  deterministic rotation (word-index math, ±8° cap).
- **Don't** randomize per render (`Math.random()` in the transform
  jitters on every re-render and destroys the handmade cohesion).
- **Do** keep body copy, dates, prices, and addresses dead level in one
  plain face — the legibility anchor.
- **Don't** apply the ransom treatment to anything longer than ~8
  words, or to navigation, forms, or buttons.
- **Do** use exactly one accent per composition (red *or* pink *or*
  yellow), in ≤3 places.
- **Don't** use gradients, soft shadows, or rounded corners — paper has
  none of these.
- **Do** show the marks of making: tape on scrap corners, staples on
  bound edges, stamps pressed on last, scribbles in margins.
- **Don't** fake it with a "grunge texture pack" look — no stock
  coffee stains, no lens dirt. The only texture is the machine:
  toner grain, high contrast, torn edges.
- **Do** degrade photos to `grayscale(1) contrast(1.8)` — the copier
  only ever saw black and white.
- **Don't** center a hero with a pill button and three feature cards.
  A zine page is one dense pasteboard, not a landing page.

## Copy voice

Angry-tender, first-person plural, direct address. Short sentences.
Practical details up front (price, address, time). Calls to action, not
calls to engagement. Price lines are poetry ("50¢ OR TRADE").

- "COPY THIS. BURN THE ORIGINAL. If the cops ask, you never saw page 3."
- "Three nights. Eight bucks. No barrier, no backstage, no excuses —
  bring earplugs and a friend who owes you money."
- "BASSIST WANTED. Must own van. Must hate van. Call after 6, never
  before noon."

## Sources consulted

- Teal Triggs, "Scissors and Glue: Punk Fanzines and the Creation of a
  DIY Aesthetic" — cut-n-paste / ransom-note typography, hand of the
  maker, Sniffin' Glue / Chainsaw / Ripped & Torn case studies.
- Stephen Duncombe, *Notes from Underground* (ch. 4, aesthetics and
  ethics of zine culture) — B/W photocopying as defining method,
  intentional imperfection, appropriation ethics.
- Community zine references cross-checked (2 independent aesthetic
  skill docs): B/W + single-accent palette, 3-face ransom system,
  deterministic rotation, feTurbulence grain recipe, highlighter marker
  pass — all tagged 🟡/⚠️ above accordingly.
