---
name: nothing-tech
description: Nothing (nothing.tech) design language — dot-matrix display typography (NDot), transparent-tech hardware aesthetic, strict black-and-white palette with one signal-red accent, and typewriter mono technical labels. Use for bold, playful consumer-tech pages that feel engineered, deadpan, and fun.
---

# Nothing Tech

## Principles

1. **Transparency as identity.** Hardware, layouts, and interfaces show their construction — transparent back panels, exposed grids, spec tables instead of marketing blurbs. Never hide how something is made.
2. **Dot-matrix is the logo.** A pixel-dot display face (NDot) carries product names and the wordmark; it reads like silkscreen ink printed on the inside of a transparent shell.
3. **Maximum contrast, minimum color.** The palette is near-monochrome. Color appears only as product photography or one red signal accent — used like a hardware recording light, never as decoration.
4. **Technical warmth.** Tiny uppercase mono labels make every UI element read like a firmware status readout or industrial packaging copy: precise, dry, slightly playful.
5. **Reduction with a wink.** Copy is terse and provocative ("Nothing to see here"). The playfulness lives in the words and the glyph lights, never in visual noise.

## Color

| Token | Hex | Role | Confidence |
|---|---|---|---|
| Ink black | `#000000` | Background (dark sections), text on light | ✅ |
| Paper white | `#FFFFFF` | Background (light sections), text on dark | ✅ |
| Signal red | `#D71921` | Sole accent — CTAs, recording dot, alerts | 🟡 |
| Worktop gray | `#F4F4F4` | Card fields, light surfaces | 🟡 |
| Spec gray | `#737373` | Secondary text, captions | 🟡 |
| Fine-print gray | `#A3A3A3` | Disabled, legal copy | 🟡 |
| Hairline (light) | `#E5E5E5` | 1px dividers on white | 🟡 |
| Hairline (dark) | `#2A2A2A` | 1px dividers on black | 🟡 |

✅ official/documented · 🟡 cross-referenced from independent site deconstructions · ⚠️ community approximation.
Black and white are the brand's documented core; the red is cross-referenced as the single accent across multiple independent analyses of nothing.tech.

## Typography

Three registers, never mixed:

- **Display / product names — NDot 55 / NDot 57** (Colophon Foundry). Dot-matrix face for the wordmark, product names, and nav. Brand rules (from Nothing's published quick guide ✅): used for product text and the logotype; leading at 90% of font size; **never change the tracking** (machine matrix spacing stays fixed); mainly uppercase; never combine with another face in the same headline block. NDot 57 is the tighter, more iconic cut.
- **Editorial display — NType 82** (Colophon Foundry). Condensed grotesque for large product statements, often set surprisingly light. 🟡
- **Technical voice — Lettera Mono LL** (Kobi Benezri / Lineto). Tiny uppercase mono for labels, buttons, metadata, timestamps, footnotes. 🟡

**Closest free substitutes** (NDot/NType/Lettera are proprietary):

| Register | Free substitute | Source |
|---|---|---|
| Dot-matrix display | **DotGothic16** — Google Fonts, pixel-dot construction closest to NDot | 🟡 documented Google Font; live font-API fetch failed during verification |
| Grotesque body/display | **Space Grotesk** or **Archivo** — geometric grotesk, Nothing's industrial register | 🟡 community recommendation |
| Technical mono | **Space Mono** or **IBM Plex Mono** — terminal-flavored uppercase labels | 🟡 community recommendation |

Fallback stack: `'DotGothic16', 'Space Mono', ui-monospace, monospace`.

**Product naming convention:** lowercase with spaced parentheses — `phone ( 3 )`, `ear ( 3a )`, `watch ( pro )`. This turns nomenclature into the brand's most recognizable graphic device. ✅

## Layout & spacing

- **Full-bleed sections** alternating pure black and white; the transparent-hardware photography supplies all texture. Pages feel like a teardown table in a clean lab: the device is the specimen, the grid is the measuring mat.
- **Technical grid:** 12-column grid with wide gutters (desktop ~80px); large empty space beats panels and cards.
- **Hairlines, not shadows.** 1px `#E5E5E5` / `#2A2A2A` dividers separate modules. No drop shadows, no elevation.
- **Radius: 0.** Square corners everywhere (product hardware may be rounded; UI chrome is not).
- **Mono label scale:** 11–12px uppercase mono, `letter-spacing: 0.08em` for UI chrome; 10px for legal copy.
- **Dot grids** as ambient texture: 1px dots on a 16–24px grid at very low contrast, never competing with content.

## Components

### 1. Dot-matrix headline
```html
<h1 class="nt-dot">ghost ( 1 )</h1>
```
```css
.nt-dot {
  font-family: 'DotGothic16', 'Space Mono', monospace;
  text-transform: uppercase;
  line-height: 0.9;          /* NDot brand rule: 90% leading */
  letter-spacing: 0;         /* never adjust tracking on dot-matrix faces */
  font-weight: 400;
}
```

### 2. Ambient dot grid
```css
.dot-grid {
  background-color: #000;
  background-image: radial-gradient(circle, #1a1a1a 1px, transparent 1px);
  background-size: 16px 16px;
}
```

### 3. Mono technical label
```html
<span class="nt-label">Glyph interface · 5 LED zones</span>
```
```css
.nt-label {
  font-family: 'Space Mono', ui-monospace, monospace;
  font-size: 11px;
  text-transform: uppercase;
  letter-spacing: 0.08em;
  color: #737373;
}
```

### 4. Product name tag (the spaced-parentheses convention)
```html
<p class="nt-dot nt-product">ear ( 3a )</p>
```
Always lowercase, single spaces inside the parentheses. Never `Ear (3a)` or `ear(3a)`.

### 5. Spec rows (firmware-style table)
```html
<dl class="nt-specs">
  <div><dt>Chipset</dt><dd>Snapdragon 8s Gen 4</dd></div>
  <div><dt>Glyph zones</dt><dd>5 · white LED</dd></div>
  <div><dt>Battery</dt><dd>5,150 mAh · 45 W</dd></div>
</dl>
```
```css
.nt-specs { font-family: 'Space Mono', monospace; font-size: 12px; }
.nt-specs div {
  display: flex; justify-content: space-between; gap: 2rem;
  padding: 14px 0; border-bottom: 1px solid #e5e5e5;
}
.nt-specs dt { text-transform: uppercase; letter-spacing: .08em; color: #737373; }
.nt-specs dd { margin: 0; text-align: right; }
```

### 6. Recording-dot status (red used like hardware)
```html
<span class="nt-live"><i></i>Live</span>
```
```css
.nt-live { font-family: 'Space Mono', monospace; font-size: 11px;
  text-transform: uppercase; letter-spacing: .08em;
  display: inline-flex; align-items: center; gap: 8px; }
.nt-live i { width: 8px; height: 8px; border-radius: 50%;
  background: #D71921; animation: blink 1.2s steps(2) infinite; }
@keyframes blink { 50% { opacity: 0.25; } }
```

### 7. Glyph LED motif (the light-strip language of Phone 1/2)
```html
<div class="nt-glyph" data-pattern="call">
  <span style="--i:0"></span><span style="--i:1"></span>
  <span style="--i:2"></span><span style="--i:3"></span>
  <span style="--i:4"></span>
</div>
```
```css
.nt-glyph { display: flex; gap: 6px; }
.nt-glyph span {
  width: 34px; height: 8px; background: #2a2a2a; border-radius: 4px;
  transition: background .25s;
}
.nt-glyph[data-pattern="call"] span { background: #fff; }
.nt-glyph[data-pattern="charge"] span:nth-child(-n+3) { background: #fff; }
```
Switch `data-pattern` (`call` / `message` / `charge`) to animate notification states — the functional heart of the Glyph interface. ⚠️ community approximation of the hardware language.

### 8. Transparent-tech product card
```html
<article class="nt-card">
  <p class="nt-label">01 · Teardown view</p>
  <div class="nt-xray"><!-- exploded SVG/CSS diagram of internals --></div>
  <p class="nt-dot">phone ( 3a )</p>
  <p class="nt-label">From $379 · In stock</p>
</article>
```
```css
.nt-card { background: #f4f4f4; padding: 24px; border: none; border-radius: 0; }
```

### 9. Mono CTA buttons (firmware labels, not pills)
```html
<a class="nt-btn" href="#">Buy now</a>
<a class="nt-btn nt-btn--alert" href="#">Notify me</a>
```
```css
.nt-btn {
  font-family: 'Space Mono', monospace; font-size: 12px;
  text-transform: uppercase; letter-spacing: .08em; text-decoration: none;
  color: #000; background: transparent;
  border: 1px solid #000; padding: 14px 28px; border-radius: 0;
  display: inline-block; transition: background .2s, color .2s;
}
.nt-btn:hover { background: #000; color: #fff; }
.nt-btn--alert { border-color: #D71921; color: #D71921; }
.nt-btn--alert:hover { background: #D71921; color: #fff; }
```
On dark sections, invert: `border-color: #fff; color: #fff;` with hover fill white/black text. Red is reserved for one alert/CTA per view.

### 10. Footer legal line
```html
<footer class="nt-foot">
  <p>© 2026 Nothing Technology Limited. London, UK.</p>
  <p>Made different. Tech is fun again.</p>
</footer>
```
```css
.nt-foot { font-family: 'Space Mono', monospace; font-size: 10px;
  letter-spacing: .04em; color: #a3a3a3;
  display: flex; justify-content: space-between;
  border-top: 1px solid #2a2a2a; padding: 24px; }
```

## Motion

Nothing publishes no motion language; keep it hardware-like — one line: LED-style blink/pulse sequences, instant snap state changes, and slow 600ms+ eases for section reveals. No bounces, no springs.

## Do / Don't

- **Do** set product names in dot-matrix as `phone ( 3 )` — lowercase with spaced parentheses. **Don't** write `Phone (3)`, `PHONE 3`, or mix the dot face with a grotesk in the same headline.
- **Do** use `#D71921` exactly once per view, like a recording light (one dot, one alert CTA). **Don't** tint backgrounds red or build red gradients — red is a signal, not a theme.
- **Do** write UI copy as tiny uppercase mono firmware labels (`Add to bag`, `Glyph interface`). **Don't** use rounded pill buttons, shadows, or glass blur cards.
- **Do** separate spec rows with 1px hairlines on generous whitespace. **Don't** put specs inside cards with backgrounds and icons — the table *is* the design.
- **Do** show the hardware's construction (transparent layers, screws, coils). **Don't** hide internals behind lifestyle photography — transparency is the product.

## Copy voice

Deadpan, terse, provocative. Short sentences. Tech is fun again. Product names are lowercase; claims are bold and unproven on purpose. Never corporate, never emoji.

- `Nothing to see here.`
- `We removed the noise. Literally.`
- `Tech is fun again.`
