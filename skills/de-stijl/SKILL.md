---
name: de-stijl
description: De Stijl / Mondrian neoplasticism — the primary-only palette, black orthogonal grid, and asymmetric rectangles of the 1917–1931 movement; use for museum, gallery, manifesto, editorial, or print-style pages that need absolute geometric discipline.
---

# De Stijl (Neoplasticism)

## Verification legend
- ✅ = documented in ≥2 independent sources (encyclopedias, movement histories, artist archives).
- 🟡 = cross-referenced across ≥3 design-literature sources; no direct period citation in hand.
- ⚠️ = community approximation — works, but treat as convention, not doctrine.

## Purpose
Produce designs (web pages, posters, exhibition sites, editorial layouts) in the visual language of De Stijl (Dutch for "The Style", founded 1917, dissolved around 1931 after Theo van Doesburg's death), the Dutch movement whose painting theory — Neoplasticism — was codified by Piet Mondrian and propagated through Van Doesburg's journal *De Stijl*. The discipline is total: only the three primary colors plus black, white and grey; only horizontal and vertical black lines; only rectangles; compositions balanced asymmetrically, never mirrored.

## Principles
1. **Reduction to the essential.** Neoplasticism strips form to its minimum: straight lines, right angles, and flat planes of pure color. Nothing decorative, nothing expressive, nothing subjective survives the cut. ✅
2. **Universal palette.** Only red, blue and yellow — the primaries — plus the "non-colors" black, white and grey. Colors are never mixed, tinted, shaded or textured; each occupies its own flat, matte plane. ✅
3. **Orthogonality is absolute.** Only horizontal and vertical lines. No diagonals, no curves, no circles, no triangles. Van Doesburg's 1924 "Elementarism" introduced the 45° diagonal — and it fractured the movement; Mondrian left over it. ✅
4. **Asymmetric balance.** Compositions are deliberately off-center. Equilibrium is achieved by counterweighting large white planes against small, dense color blocks — never by mirroring. ✅
5. **White is structural, not background.** White planes are active elements: they hold color blocks apart, carry compositional weight, and are drawn with the same intention as red or blue. ✅/🟡
6. **Flatness is honesty.** No gradients, no shadows, no texture, no simulated material, no glass. The plane is the texture; the surface is always unadorned. 🟡

## Color
Real palette: the primaries plus non-colors. Exact hex values were never published by Mondrian — the values below are the community-standard reproduction sampling (consistent across design-literature palettes); treat the *rule* as ✅ and the *numbers* as 🟡.

| Token | Hex | Role |
|---|---|---|
| `--dst-red` | `#E01F26` 🟡 | Dominant accent. One large red plane per composition, rarely two. Never pure `#FF0000`. |
| `--dst-blue` | `#225095` 🟡 | Secondary accent. Deep, muted navy-blue, never bright. |
| `--dst-yellow` | `#FAC901` 🟡 | Tertiary accent. Used sparingly — small dense blocks carry the most weight. |
| `--dst-black` | `#1A1A1A` 🟡 | Grid lines, rules, body text, fills for small planes. |
| `--dst-white` | `#FFFFFF` ✅ | Background and structural planes — white is white. |
| `--dst-grey` | `#C0C0C0` 🟡 | Neutral planes and secondary surfaces; a cool mid-grey. |

Usage rules (🟡/⚠️ community conventions):
- Max **3 color blocks per composition**. One primary dominates; the others counterweight.
- Never place two primaries adjacent without a black line or white plane between them.
- Never place grey adjacent to white without a black separator — the contrast collapses.
- Text on primaries: white on red/blue, black on yellow, for legibility.

## Typography
- **Display:** bold geometric sans, all caps — **Archivo Black** or **Jost** (700) as free stand-ins for Van Doesburg's 1919 geometric alphabet and the heavy grotesques Piet Zwart used in De Stijl-inflected commercial typography. 🟡
- **Body:** the same family at regular weight, 16–18px, short paragraphs, left-aligned with a ragged right edge. Never centered, never justified into even blocks that fight the asymmetry. 🟡
- **Scale (⚠️ community convention):** display 48–96px desktop; eyebrow labels 12–14px, uppercase, letter-spacing `0.2–0.3em`; captions 12–14px regular.
- **Type is always set horizontally, in strict rectangular blocks.** Letterforms are treated as rectangular units in the grid — never italic, never rotated, never set on a curve or diagonal. ✅ (orthogonality rule applied to type, documented in movement analyses)

## Layout & spacing
- **Grid:** 12-column asymmetric grid. Content spans uneven column groups (7/5, 5/4/3, 8/4) — hero text left-aligned hard against a black rule, never centered. 🟡
- **The Mondrian construction:** `display: grid` on a black background with a fixed `gap` and a matching outer `border` — the gaps *become* the black lines. This is the canonical CSS translation of the paintings. ⚠️
- **Line weight:** 6–10px desktop, 4–6px mobile; one constant weight per composition. Mondrian's lines vary across paintings, but within a single composition they hold — don't mix hairlines and bars in one panel. 🟡
- **Radius:** 0 everywhere. **Shadows:** none. **Borders:** black, never grey. ✅
- **Spacing:** rectangles sit flush to the grid; color blocks carry no internal padding except text blocks (24–48px). Sections are separated by full-bleed black rules, not by soft whitespace alone. 🟡
- **Asymmetry check:** if a layout is mirrorable left-to-right, re-balance it — shift one block off axis until the mirror breaks. ⚠️

## Components

### 1. Composition panel (the core block)
The whole page is built from these. Black background + gap = black grid lines; children are the color planes.

```html
<div class="dst-composition">
  <div class="dst-plane dst-white" style="grid-column: 1 / 8; grid-row: 1 / 4;">
    <p class="dst-eyebrow">Museum of Neoplastic Art</p>
    <h2>Composition 25</h2>
  </div>
  <div class="dst-plane dst-red" style="grid-column: 8 / 13; grid-row: 1 / 3;"></div>
  <div class="dst-plane dst-blue" style="grid-column: 10 / 13; grid-row: 3 / 5;"></div>
  <div class="dst-plane dst-yellow" style="grid-column: 1 / 5; grid-row: 4 / 5;"></div>
  <div class="dst-plane dst-white" style="grid-column: 5 / 10; grid-row: 3 / 5;"></div>
</div>

<style>
.dst-composition {
  display: grid;
  grid-template-columns: repeat(12, 1fr);
  grid-auto-rows: minmax(72px, auto);
  gap: 8px;                    /* the gap IS the black grid line */
  background: #1A1A1A;
  border: 8px solid #1A1A1A;   /* same weight as the internal lines */
}
.dst-plane { padding: 32px; }
.dst-red { background: #E01F26; } .dst-blue { background: #225095; }
.dst-yellow { background: #FAC901; } .dst-white { background: #FFFFFF; }
.dst-black { background: #1A1A1A; } .dst-grey { background: #C0C0C0; }
</style>
```

### 2. Primary CTA button
A solid primary-color block with bold uppercase type. Square corners, no hover glow — the hover state is a hard swap to black.

```html
<a class="dst-btn dst-btn-red" href="#tickets">Book tickets</a>

<style>
.dst-btn {
  display: inline-block; padding: 18px 36px;
  font: 900 14px/1 'Archivo Black', 'Arial Black', sans-serif;
  text-transform: uppercase; letter-spacing: .18em;
  color: #FFFFFF; background: #E01F26;
  text-decoration: none; border: none; border-radius: 0; cursor: pointer;
}
.dst-btn:hover { background: #1A1A1A; }   /* hard cut, no transition */
.dst-btn-blue { background: #225095; }
.dst-btn-yellow { background: #FAC901; color: #1A1A1A; }
.dst-btn-yellow:hover { background: #1A1A1A; color: #FFFFFF; }
</style>
```

### 3. Rule divider with color segment
Sections are separated by a full-bleed black rule carrying one primary segment — the De Stijl equivalent of a section break.

```html
<div class="dst-rule"><span class="dst-rule-seg"></span></div>

<style>
.dst-rule { height: 10px; background: #1A1A1A; position: relative; }
.dst-rule-seg {
  position: absolute; top: 0; bottom: 0; left: 12%;
  width: 22%; background: #E01F26;
}
/* variant: place a second segment off-axis for asymmetry */
</style>
```

### 4. Block tabs
Tabs are solid blocks, not underlines. The active tab is a primary color; inactive tabs are white with a black border.

```html
<div class="dst-tabs" role="tablist">
  <button class="dst-tab is-active" data-tab="hours" role="tab">Hours</button>
  <button class="dst-tab" data-tab="tickets" role="tab">Tickets</button>
  <button class="dst-tab" data-tab="visit" role="tab">Getting here</button>
</div>

<style>
.dst-tabs { display: flex; gap: 8px; background: #1A1A1A; padding: 8px; }
.dst-tab {
  flex: 1; padding: 16px; border: 3px solid #1A1A1A; background: #FFFFFF;
  font: 900 13px/1 'Archivo Black', sans-serif; text-transform: uppercase;
  letter-spacing: .15em; cursor: pointer; border-radius: 0;
}
.dst-tab.is-active { background: #E01F26; color: #FFFFFF; border-color: #1A1A1A; }
</style>
```

### 5. Artwork card
A mini Mondrian composition on top, a black caption bar below. The composition is the image — no photographs required.

```html
<figure class="dst-card">
  <div class="dst-card-art">
    <div style="grid-column:1/5;grid-row:1/3;background:#E01F26"></div>
    <div style="grid-column:5/9;grid-row:1/4;background:#FFFFFF"></div>
    <div style="grid-column:1/5;grid-row:3/4;background:#225095"></div>
    <div style="grid-column:5/9;grid-row:4/5;background:#FAC901"></div>
  </div>
  <figcaption>
    <strong>Composition with Red, Blue and Yellow</strong>
    <span>Piet Mondrian · 1930 · Oil on canvas</span>
  </figcaption>
</figure>

<style>
.dst-card { margin: 0; border: 6px solid #1A1A1A; background: #FFFFFF; }
.dst-card-art {
  display: grid; grid-template-columns: repeat(8, 1fr);
  grid-auto-rows: 56px; gap: 5px; background: #1A1A1A;
}
.dst-card figcaption { background: #1A1A1A; color: #FFFFFF; padding: 14px 16px; }
.dst-card figcaption strong { display: block; font: 900 14px/1.3 'Archivo Black', sans-serif; text-transform: uppercase; }
.dst-card figcaption span { font: 400 13px/1.5 Arial, sans-serif; color: #C0C0C0; }
</style>
```

### 6. Schedule table
Black header row, alternating white/grey body rows, one primary date block per row.

```html
<table class="dst-table">
  <thead><tr><th>Date</th><th>Event</th><th>Hall</th></tr></thead>
  <tbody>
    <tr><td class="dst-date">12 Oct</td><td>Curator walkthrough: The Grid Years</td><td>Hall A</td></tr>
    <tr><td class="dst-date">26 Oct</td><td>Family workshop: Build a composition</td><td>Atelier</td></tr>
  </tbody>
</table>

<style>
.dst-table { width: 100%; border-collapse: collapse; border: 6px solid #1A1A1A; }
.dst-table th { background: #1A1A1A; color: #FFFFFF; text-align: left;
  font: 900 12px/1 'Archivo Black', sans-serif; text-transform: uppercase;
  letter-spacing: .15em; padding: 14px 16px; }
.dst-table td { padding: 14px 16px; border-top: 3px solid #1A1A1A; font: 400 15px/1.4 Arial, sans-serif; }
.dst-table tbody tr:nth-child(even) { background: #C0C0C0; }
.dst-table .dst-date { background: #225095; color: #FFFFFF; font-weight: 700; white-space: nowrap; }
</style>
```

## Motion
None. Static equilibrium is the point — the tension lives *between* the rectangles, not in transitions between states. State changes (tabs, filters, hovers) must be instant hard cuts with no easing; a fade or slide breaks the style's stillness. Respect `prefers-reduced-motion` trivially: there is nothing to reduce. 🟡

## Do / Don't

| ✅ Do | 🚫 Don't |
|---|---|
| Build black lines from grid gaps and borders — the container's black background showing through | Draw lines as separate decorative elements floating over content |
| Use at most 3 primary color blocks per view, one dominant | Add a fourth "harmonizing" color to soften the palette |
| Set type in horizontal rectangular blocks, bold geometric sans | Italicize, rotate, curve, or angle any text |
| Let white planes carry compositional weight — they are structure | Treat white as leftover background to be filled |
| Keep every corner perfectly square, every edge flush to the grid | Round a corner or add a shadow "to soften it" |
| Balance asymmetrically — counterweight a large white plane with a small dense color block | Center the composition or mirror it left-to-right |
| Change states with an instant hard cut | Animate with fades, slides, or eased transitions |
| Separate sections with full-bleed black rules | Use soft spacing or hairline grey dividers |

The hard rule, in one line: **no diagonals.** The 45° line split the movement in 1924 — it will split your design too.

## Copy voice
Declarative and manifesto-brief. Short sentences. Imperatives. Numbers as facts. No adjectives of feeling, no marketing warmth, no exclamation marks.

Example strings:
- "Line. Plane. Colour. Nothing else."
- "Red, blue, yellow. Black, white, grey. No more, no less."
- "The white rectangle is not empty. It holds the others apart."

## Sources consulted
- De Stijl Movement Explained: Mondrian & Neoplasticism: https://stoneandgray.co.za/blogs/news/what-is-de-stijl-neoplasticism
- De Stijl — Aesthetics Wiki (rules of Neoplasticism, the Elementarism schism): https://aesthetics.fandom.com/wiki/De_Stijl
- De Stijl — Cornell University design history archive (functionalism, rectilinearity, primary-only palette): http://char.txa.cornell.edu/ART/DECART/DESTIJL/decstijl.htm
- de-stijl.md — aesthetic-frontend-skills (sampled hex palette, geometric-sans typography, flat matte surface, static equilibrium): https://github.com/hongquandev/aesthetic-frontend-skills/blob/HEAD/skills/aesthetic-literacy/aesthetics/de-stijl.md
- Architype van der Leck — Wikipedia (Bart van der Leck's geometric typeface for a De Stijl journal; Van Doesburg's 1919 geometric alphabet): https://en.wikipedia.org/wiki/Architype_van_der_Leck
- Typography and Religion in the De Stijl Movement — CareTypography: https://www.caretypography.com/typography-and-religion-in-the-de-stijl-movement
