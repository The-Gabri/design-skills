---
name: solarpunk
description: Solarpunk — optimistic eco-futurism. Use for green tech, community energy, urban farming, climate-positive products, and anything that should feel sunlit, organic, and hopefully human: golden light, botanical motifs, art-nouveau curves, warm daylight palettes.
---

# Solarpunk

Solarpunk is a speculative-fiction movement (term coined 2008) imagining
positive futures driven by clean energy without scarcity — Wikipedia's
characterization: "the inverse of cyberpunk." The "solar" is solar energy
as a renewable source plus an optimistic vision that rejects environmental
pessimism; the "punk" is DIY, countercultural, post-capitalist,
community-led making. Visually: warm golden light, flowering vines over
architecture, Art Nouveau curves, hand-crafted textures, and a vibrant,
hopeful palette (cross-referenced across NightCafe's aesthetic survey,
the solarpunk primer on the Anarchist Library, and design press coverage,
incl. Figma CEO Dylan Field's "cyberpunk is out, solarpunk is in"
commentary). Aesthetically it borrows from Art Nouveau, upcycling, and
Asian and African artistic traditions. There is no official brand manual
— everything below that lacks a documentation source is marked ⚠️.

## Confidence legend
- ✅ = documented in a named, verifiable source.
- 🟡 = cross-referenced across ≥3 independent analyses/descriptions.
- ⚠️ = community approximation: consistent with the movement's look, not official.

## Principles

1. **Light is the medium, not the mood.** Cyberpunk is dark with neon;
   solarpunk is bright. Sunlight conveys cleanliness, abundance, and
   equity (✅ Wikipedia). Pages should feel mid-morning on a clear day —
   warm, legible, high-key. Darkness as a primary background is a style break.
2. **Nature and technology are one system.** Solar panels sit under
   green roofs; drones pollinate orchards. Never depict nature as
   decoration *on top of* gray tech — Andrewism-style critiques call
   that out as greenwashing: "it isn't slapping flowers and trees on
   concrete buildings" (✅ theanarchistlibrary.org primer). Every
   element should look like it *works* for the ecosystem it sits in.
3. **Organic geometry, not Euclidean boxes.** Curves, arches, whiplash
   tendrils, domes, spirals — Art Nouveau's flowing, plant-derived line
   work (🟡 cross-referenced: art-nouveau → solarpunk lineage appears in
   nearly every aesthetic survey). Corners are grown, not cut.
4. **Hand-made and community-scale.** Craft textures, hand-lettered
   warmth, visible joins, upcycled materials. The future here is built
   by neighbors, not corporations — "DIY projects to larger
   organization" (✅ theanarchistlibrary.org). UI copy speaks in first
   person plural: *we* built this.
5. **Diverse cultural roots, not one utopia.** Solarpunk "alludes to
   diverse cultural origins" and draws on Asian and African artistic
   styles alongside Art Nouveau (✅ Wikipedia; ✅ primer). Pattern
   language should borrow globally and never default to a single
   Eurocentric postcard.

## Color

Solarpunk has no official palette; the *hues* are 🟡 cross-referenced
(sun gold, leaf green, sky/clean-water blue appear in every description),
the specific hexes are ⚠️ community approximations chosen for WCAG-safe
pairings on warm daylight grounds.

| Token | Hex | Role |
|---|---|---|
| `--sun-gold` | `#E9A62B` ⚠️ | Primary accent: sun, CTA, keylines |
| `--sun-pale` | `#F7D774` ⚠️ | Highlights, rays, active states |
| `--leaf` | `#2E7D32` ⚠️ | Primary green: botanical fills, success |
| `--leaf-deep` | `#1B4D2E` ⚠️ | Text on light greens, footer deep tone |
| `--sky` | `#7FC8D6` ⚠️ | Clean-water blue: secondary accents |
| `--cream` | `#FFF8E7` ⚠️ | Page background — warm paper, never pure white |
| `--clay` | `#C96F3B` ⚠️ | Terracotta warmth: secondary buttons, earth |
| `--ink` | `#2B2A24` ⚠️ | Body text — warm near-black |
| `--petal` | `#E4573D` ⚠️ | Sparing: flowers, warnings, live status dots |

Ground rules:
- Backgrounds are warm (cream, pale sun, soft leaf tint) — dark sections
  only as a contrast accent, never the whole page (🟡).
- Green on cream: use `--leaf-deep` for text to stay legible; bright
  `--leaf` is for fills and icons, not body copy.
- No purple-blue gradients, no neon — those belong to the movement
  solarpunk defines itself *against* (🟡).
- Stained-glass moments: small panels where sun-gold, sky, leaf, and
  petal sit side by side separated by dark leading — a direct Art Nouveau
  nod (🟡).

## Typography

The movement prescribes no typefaces. These are ⚠️ substitutes chosen to
echo the style's dual roots (Nouveau poster + community noticeboard):

- **Display:** a warm, organic serif with soft brackets — closest free
  substitute: **Fraunces** (Google Fonts). Fallback stack for offline
  pages: `Georgia, 'Times New Roman', serif`.
- **Body/UI:** a friendly humanist sans — closest free: **Nunito Sans**
  or **Karla**. Fallback: `system-ui`.
- **Hand accent (rare):** a hand-lettered script for marginalia
  ("grown with love", annotations) — **Caveat** sparingly, or skip.
- Scale: display headlines can be large and airy (`clamp(2.5rem, 6vw, 4.5rem)`);
  body 1–1.125rem; line-height ≥1.6 — text should breathe like open air.
- Rules: never all-caps headlines (shouting breaks the warmth); headlines
  in sentence case with a human verb ("Grow your power with your neighbors").

## Layout & spacing

- **Organic containers:** border-radius is generous and often asymmetric
  — arches (`border-radius: 50% 50% 12px 12px / 30% 30% 12px 12px`),
  blobs (`border-radius: 48% 52% 55% 45% / 52% 48% 52% 48%`). ⚠️
- **Spacing scale:** 8px base, generous whitespace; sections separated by
  organic SVG dividers (waves, leaf fringes, sun arches) rather than hard
  rules.
- **Shadows:** soft, warm, sun-cast — `0 12px 32px rgba(233,166,43,.18)`,
  never cold gray drop shadows. ⚠️
- **Cards** sit on cream with a thin sun-gold keyline or a leaf-tinted
  wash; corners ≥24px.
- **Grid:** 12-col max-width ~1120px, but hero and gallery sections may
  break the grid with overlapping botanical SVGs at the edges — asymmetry
  is welcome.
- **Borders as craft:** dashed "stitched" borders (like a sewn patch) or
  double hairlines with a leaf-diamond at joins evoke the handmade ethic.

## Components

### 1. Sun-mark logo badge

```html
<span class="sunmark" aria-hidden="true">
  <svg viewBox="0 0 48 48" width="40" height="40">
    <circle cx="24" cy="24" r="10" fill="#E9A62B"/>
    <g stroke="#E9A62B" stroke-width="3" stroke-linecap="round">
      <line x1="24" y1="4"  x2="24" y2="10"/>
      <line x1="24" y1="44" x2="24" y2="38"/>
      <line x1="4"  y1="24" x2="10" y2="24"/>
      <line x1="44" y1="24" x2="38" y2="24"/>
      <line x1="10" y1="10" x2="14" y2="14"/>
      <line x1="38" y1="10" x2="34" y2="14"/>
      <line x1="10" y1="38" x2="14" y2="34"/>
      <line x1="38" y1="38" x2="34" y2="34"/>
    </g>
  </svg>
</span>
```

### 2. Leaf-vine divider

```html
<div class="vine-divider" aria-hidden="true">
  <svg viewBox="0 0 600 40" preserveAspectRatio="xMidYMid meet">
    <path d="M0,28 C120,28 160,8 300,20 C440,32 480,8 600,20"
          fill="none" stroke="#2E7D32" stroke-width="2.5"/>
    <g fill="#2E7D32">
      <ellipse cx="150" cy="16" rx="14" ry="7" transform="rotate(-30 150 16)"/>
      <ellipse cx="300" cy="24" rx="14" ry="7" transform="rotate(20 300 24)"/>
      <ellipse cx="450" cy="12" rx="14" ry="7" transform="rotate(-25 450 12)"/>
    </g>
    <circle cx="600" cy="20" r="6" fill="#E9A62B"/>
  </svg>
</div>
```

### 3. Organic arch card

```css
.arch-card {
  background: #FFF8E7;
  border: 2px solid #E9A62B;
  border-radius: 120px 120px 24px 24px; /* sun-arch top */
  padding: 2.5rem 1.75rem 1.75rem;
  box-shadow: 0 12px 32px rgba(233,166,43,.18);
}
```

### 4. Stained-glass stat panel

```html
<div class="stained-stats">
  <div class="pane pane-gold"><strong>2.4 MWh</strong><span>solar shared this month</span></div>
  <div class="pane pane-leaf"><strong>312 kg</strong><span>food grown on roofs</span></div>
  <div class="pane pane-sky"><strong>48</strong><span>neighbors connected</span></div>
</div>
<style>
.stained-stats { display:grid; grid-template-columns:repeat(3,1fr); gap:6px;
  background:#2B2A24; padding:6px; border-radius:20px; }
.pane { border-radius:14px; padding:1.25rem; text-align:center; }
.pane-gold { background:#F7D774; } .pane-leaf { background:#9FD6A8; }
.pane-sky  { background:#BFE3EA; }
.pane strong { display:block; font-size:1.6rem; font-family:Georgia,serif; }
.pane span { font-size:.85rem; }
</style>
```

### 5. Sunburst CTA button

```css
.btn-sun {
  background:#E9A62B; color:#2B2A24; font-weight:700;
  border-radius:999px; padding:.9rem 2rem; border:none; cursor:pointer;
  box-shadow: 0 6px 0 #b97f1d, 0 12px 24px rgba(233,166,43,.35);
  transition: transform .15s ease-out, box-shadow .15s ease-out;
}
.btn-sun:hover  { transform: translateY(-2px); }
.btn-sun:active { transform: translateY(4px); box-shadow: 0 2px 0 #b97f1d; }
```

### 6. Grove tab switcher (rounded segment control)

```html
<div class="grove-tabs" role="tablist" aria-label="Projects">
  <button role="tab" aria-selected="true"  class="grove-tab active">Solar</button>
  <button role="tab" aria-selected="false" class="grove-tab">Rooftop farm</button>
  <button role="tab" aria-selected="false" class="grove-tab">Shared battery</button>
</div>
<style>
.grove-tabs { display:inline-flex; gap:4px; background:#F3E8CF;
  border-radius:999px; padding:6px; }
.grove-tab { border:none; background:transparent; border-radius:999px;
  padding:.6rem 1.25rem; cursor:pointer; font-weight:600; color:#2B2A24; }
.grove-tab.active { background:#fff; box-shadow:0 2px 8px rgba(43,42,36,.12); }
</style>
```

### 7. Impact counter chip

```html
<p class="impact-chip">
  <svg viewBox="0 0 24 24" width="20" height="20" aria-hidden="true">
    <path d="M12 3C7 8 5 12 5 15a7 7 0 0 0 14 0c0-3-2-7-7-12z" fill="#2E7D32"/>
  </svg>
  <strong id="co2-saved">0</strong> kg of CO₂ kept out of the sky this year
</p>
```
*(Animate the number with JS on scroll into view.)*

## Motion

Solarpunk has no codified motion language — one line: motion should feel
like *growth*, not like machinery: slow, organic ease-outs (e.g.
`cubic-bezier(.22,1,.36,1)`), 300–600ms, elements that bloom, drift, or
unfurl (scale + slight rise) rather than snap or slide mechanically. ⚠️
Respect `prefers-reduced-motion`: replace drift/ambient animation with
static states.

## Do / Don't

- ✅ **Do** draw nature and tech as one working system — a solar canopy
  that also shades a herb garden, a rain barrel feeding a living wall.
- ❌ **Don't** greenwash: never slap leaves onto a gray concrete box and
  call it done. That is the movement's defining anti-pattern (✅ primer).
- ✅ **Do** let sunlight be the hero: warm key light, long soft shadows,
  pages that feel like morning.
- ❌ **Don't** use dark cyberpunk backgrounds, neon, or purple-blue
  gradients — that is the aesthetic solarpunk was written against (🟡).
- ✅ **Do** grow your corners: arches, blobs, whiplash curves, stitched
  dashed borders, hand-drawn-feeling SVG.
- ❌ **Don't** use sharp corporate rectangles, glassmorphism on dark bg,
  or cold gray shadows — they read as the old world.
- ✅ **Do** write copy in the communal "we": neighbors, groves,
  harvests, shared yields. Numbers that count *collective* impact.
- ❌ **Don't** write dystopian or scarcity copy ("fight", "survive",
  "the last...") — optimism is structural here, not decoration (🟡).

## Copy voice

Warm, practical, communal. Present tense, active verbs, invitations not
demands. Talk about abundance and shared work, never guilt. Short
sentences; botanical or solar metaphors where natural, never forced.

Examples:
- "Your roof is already a power station. Let's plug the street into it."
- "This week your block grew 14 kg of tomatoes and banked 320 kWh. Nice work, neighbors."
- "Repairs welcome here — bring your broken kettle on Saturday and we'll fix it together."

## Sources
- Solarpunk — Wikipedia (characteristics: bright greens/blues, light as
  motif of cleanliness/abundance/equability, diverse cultural origins):
  https://en.wikipedia.org/wiki/Solarpunk
- "What is Solarpunk?" primer — theanarchistlibrary.org (art nouveau,
  upcycling, Asian/African styles, DIY organization, anti-greenwashing):
  https://Theanarchistlibrary.org/library/saint-andrew-what-is-solarpunk.a4.pdf
- NightCafe solarpunk aesthetic survey (warm golden light, flowering
  vines, art-nouveau curves, hand-crafted textures, hopeful palette):
  https://Creator.Nightcafe.studio/tools/solarpunk-aesthetic-generator
- Dylan Field on the solarpunk turn in design (curves, blended into
  environment, humanist vs cyberpunk hard edges):
  https://techiemag.co.uk/cyberpunk-is-out-and-solarpunk-is-in-according-to-figmas-ceo/
