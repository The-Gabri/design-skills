---
name: bauhaus
description: Bauhaus design movement (1919–1933) — form follows function, geometric primitives, primary colors, lowercase geometric type. Use for posters, exhibition sites, design-school brands, and anything that should look constructed rather than decorated.
---

# Bauhaus

## Principles

1. **Form follows function.** Every element earns its place by doing a job — structure, hierarchy, or information. Ornament is a failure state. Nothing decorative that doesn't also communicate.
2. **Geometry is the whole vocabulary.** Circle, square, and triangle (Kandinsky's "Point and Line to Plane" primer forms) are the only decorative shapes. If it isn't one of these, it doesn't belong.
3. **Primaries only.** Red, yellow, and blue, used at full saturation as flat fills. Black and white do all the structural work. No tints, no gradients, no muddy intermediates.
4. **Asymmetric balance on a strict grid.** Composition is dynamic and off-center — never mirrored symmetry — but always anchored to a visible mathematical grid. Break the grid deliberately, never accidentally.
5. **Type is material.** Letters are physical objects set at scale: large, heavy, flush-left, lowercase. Typography composes with the shapes, not beside them.
6. **Honesty of construction.** Show the grid lines, the thick black rules, the flat color blocks. Joints are visible; nothing is hidden behind soft shadows or blur.

## Color

✅ **Paper** `#F7F4EC` — default background (warm unprinted paper, matches the school's institutional stock).  
✅ **Ink** `#1A1A1A` — near-black for type, rules, borders. Never use a "soft" black.  
✅ **White** `#FFFFFF` — reverse background / text on color fields.  

🟡 **Bauhaus red** `#D02020` — circle-associated; primary accent, energy, calls to action.  
🟡 **Bauhaus blue** `#1040C0` — square-associated; structure, information blocks, reason.  
🟡 **Bauhaus yellow** `#F0C020` — triangle-associated; highlights, warnings, movement.  

🟡 marks: exact hex values vary across print reproductions and scholarly sources; the trinity (red/yellow/blue + black/white) is canonical, the specific tints are cross-referenced from multiple Bauhaus digital revivals. Any fully saturated primary is defensible — consistency across a project matters more than the exact number.  
⚠️ Nothing else. No grays for "softness", no pastels, no gradients ever.

## Typography

The real thing: Herbert Bayer's **Universal alphabet** (1925, Dessau) — a geometric, lowercase-only sans-serif built from circles and straight lines, commissioned by Gropius for all Bauhaus publications. Digital revival: **Architype Bayer** (licensed). ⚠️ **ITC Bauhaus (1975)** is the commercialized, cliché derivative — avoid it unless you're being ironic.

Closest free substitutes (🟡), in order of authenticity:
1. **Jost** (Google Fonts) — free Futura revival; geometric, Bauhaus-era correct.
2. **Poppins** — pure geometric monolinear forms.
3. **Archivo** — grotesque with geometric bones; best body-text partner.

Rules:
- Headlines: lowercase always, weight 700–900, tight tracking (−1% to −2%), sizes 48–120px. This honors Bayer's rule: *"since speech reveals no difference between upper and lower case, why should written text?"*
- Body: sentence case is acceptable, 14–18px, line-height 1.5, geometric sans.
- Meta labels: small (11–13px), letter-spaced (10–15% em), and this is the ONLY place uppercase may appear — classification tags, section numbers.
- No italics. No serifs. Hierarchy comes from **scale and weight only**.

## Layout & spacing

- **Grid:** 12-column modular grid, visible or implied; thick black rules (3–4px) may be left visible as structural elements — they are composition, not decoration.
- **Spacing scale (base 8px):** `8 / 16 / 24 / 48 / 96`. Whitespace is active negative space, never filler.
- **Radius:** `0` on everything rectangular. Circles are circles; rectangles are rectangles.
- **Borders:** 3–4px solid ink `#1A1A1A` to frame blocks; thin 1–2px rules to separate rows. Borders are never "subtle".
- **Composition:** asymmetric, off-center. Place a red circle left, a blue square right, a yellow triangle breaking the column — then balance the whole with mass, not mirroring.
- **Depth:** flat. If layering is needed, use solid overlapping shapes or hard offset shadows (4–8px, no blur) — never drop shadows or glows.

## Components

All copy-pasteable. Base vars:

```css
:root {
  --paper: #F7F4EC;
  --ink: #1A1A1A;
  --white: #FFFFFF;
  --red: #D02020;
  --blue: #1040C0;
  --yellow: #F0C020;
  --rule: 3px solid var(--ink);
  --font: "Jost", "Archivo", "Futura", "Century Gothic", sans-serif;
}
```

### 1. Geometric hero

```html
<section class="hero">
  <h1>the shape<br>of function</h1>
  <div class="shapes">
    <span class="circle"></span>
    <span class="square"></span>
    <span class="triangle"></span>
  </div>
</section>
<style>
.hero { background: var(--paper); padding: 96px 48px; border-bottom: var(--rule); }
.hero h1 { font-family: var(--font); font-weight: 800; font-size: clamp(48px, 9vw, 120px);
           line-height: .92; letter-spacing: -.02em; text-transform: lowercase; margin: 0; }
.circle  { width: 72px; height: 72px; background: var(--red); border-radius: 50%; display: inline-block; }
.square  { width: 72px; height: 72px; background: var(--blue); display: inline-block; }
.triangle{ width: 0; height: 0; border-left: 40px solid transparent; border-right: 40px solid transparent;
           border-bottom: 72px solid var(--yellow); display: inline-block; }
</style>
```

### 2. Poster card (exhibition / event)

```html
<article class="poster">
  <div class="poster-bar"></div>
  <p class="poster-no">nº 03</p>
  <h2>geometry<br>workshop</h2>
  <p class="poster-meta">14 — 18 oct · hall a</p>
</article>
<style>
.poster { background: var(--white); border: var(--rule); padding: 24px; max-width: 320px; }
.poster-bar { height: 12px; background: var(--blue); margin-bottom: 24px; }
.poster-no { font: 700 12px/1 var(--font); letter-spacing: .12em; color: var(--red); text-transform: uppercase; }
.poster h2 { font: 800 40px/1 var(--font); letter-spacing: -.02em; text-transform: lowercase; margin: 16px 0; }
.poster-meta { font: 500 14px/1.4 var(--font); border-top: var(--rule); padding-top: 12px; }
</style>
```

### 3. Nav (top bar with shape mark)

```html
<nav class="nav">
  <span class="mark"><i class="c"></i><i class="s"></i><i class="t"></i></span>
  <span class="word">werkstatt</span>
  <span class="links"><a href="#">exhibitions</a><a href="#">workshops</a><a href="#">archive</a></span>
</nav>
<style>
.nav { display: flex; align-items: center; gap: 16px; padding: 16px 48px;
       background: var(--paper); border-bottom: var(--rule); font-family: var(--font); }
.mark i { display: inline-block; margin-right: -6px; }
.mark .c { width: 22px; height: 22px; background: var(--red); border-radius: 50%; }
.mark .s { width: 22px; height: 22px; background: var(--blue); }
.mark .t { width: 0; height: 0; border-left: 11px solid transparent;
           border-right: 11px solid transparent; border-bottom: 20px solid var(--yellow); }
.word { font-weight: 800; font-size: 20px; text-transform: lowercase; letter-spacing: -.01em; }
.links { margin-left: auto; display: flex; gap: 24px; }
.links a { color: var(--ink); text-decoration: none; font-weight: 600; font-size: 14px; }
.links a:hover { background: var(--yellow); }
</style>
```

### 4. Buttons as primitives

```html
<a class="btn btn-circle" href="#">enrol</a>
<a class="btn btn-square" href="#">programme</a>
<button class="btn btn-triangle" aria-label="tickets"><span>tickets</span></button>
<style>
.btn { font: 800 16px/1 var(--font); text-transform: lowercase; text-decoration: none;
       color: var(--white); display: inline-flex; align-items: center; justify-content: center;
       border: var(--rule); cursor: pointer; }
.btn-circle { width: 120px; height: 120px; border-radius: 50%; background: var(--red); }
.btn-square { width: 120px; height: 120px; background: var(--blue); }
.btn-triangle { background: none; border: none; position: relative; width: 140px; height: 122px; }
.btn-triangle::before { content: ""; position: absolute; inset: 0; background: var(--yellow);
       clip-path: polygon(50% 0, 100% 100%, 0 100%); }
.btn-triangle span { position: relative; color: var(--ink); }
.btn:hover { outline: var(--rule); outline-offset: 4px; }
</style>
```

### 5. Section label + number

```html
<div class="sec-head"><span class="sec-no">02</span><span class="sec-label">workshops</span></div>
<style>
.sec-head { display: flex; align-items: baseline; gap: 16px; border-bottom: var(--rule); padding-bottom: 12px; }
.sec-no { font: 800 40px/1 var(--font); color: var(--red); }
.sec-label { font: 700 13px/1 var(--font); letter-spacing: .14em; text-transform: uppercase; }
</style>
```

### 6. Solid color-block section

```html
<section class="block block-blue">
  <h2>art + technology:<br>a new unity</h2>
  <p>one sentence of purpose. nothing more.</p>
</section>
<style>
.block { padding: 96px 48px; color: var(--white); }
.block h2 { font: 800 clamp(40px, 6vw, 80px)/0.95 var(--font); text-transform: lowercase;
            letter-spacing: -.02em; margin: 0 0 24px; }
.block p { font: 400 18px/1.5 var(--font); max-width: 40ch; }
.block-blue { background: var(--blue); }
.block-red  { background: var(--red); }
</style>
```

### 7. Rule-separated list (programme / archive)

```html
<ul class="rows">
  <li><span class="dot"></span><strong>metal workshop</strong><em>moholy-nagy · 1923</em></li>
  <li><span class="dot"></span><strong>stage studies</strong><em>schlemmer · 1922</em></li>
</ul>
<style>
.rows { list-style: none; margin: 0; padding: 0; font-family: var(--font); }
.rows li { display: flex; align-items: center; gap: 16px; padding: 16px 0;
           border-bottom: 2px solid var(--ink); }
.rows .dot { width: 16px; height: 16px; background: var(--yellow); border-radius: 50%; flex: none; }
.rows strong { font-size: 20px; font-weight: 700; text-transform: lowercase; }
.rows em { margin-left: auto; font-style: normal; font-size: 14px; }
</style>
```

### 8. Footer

```html
<footer class="foot">
  <p><strong>werkstatt exhibition</strong> — hall a, dessau</p>
  <p class="foot-note">built with geometry. no decoration was harmed.</p>
</footer>
<style>
.foot { background: var(--ink); color: var(--paper); padding: 48px; font-family: var(--font); }
.foot p { margin: 0; text-transform: lowercase; }
.foot strong { font-weight: 800; }
.foot-note { font-size: 14px; margin-top: 8px !important; opacity: .7; }
</style>
```

## Motion

Bauhaus predates screen motion and defines none — when you must animate, move like a machine: linear easing, 200–300ms, whole-element translations and hard step cuts. Never bouncy, springy, or eased-in-out "delightful" motion.

## Do / Don't

- ✅ DO set headlines lowercase in heavy geometric sans. — ❌ DON'T use Title Case, serifs, or italic emphasis anywhere.
- ✅ DO use full-saturation primaries as flat fills (red circle, blue square, yellow triangle). — ❌ DON'T use gradients, tints, pastels, or drop shadows.
- ✅ DO make the grid and black rules visible. — ❌ DON'T hide structure behind rounded cards and soft containers.
- ✅ DO balance asymmetrically: offset composition, off-center placement. — ❌ DON'T center everything or mirror layouts symmetrically.
- ✅ DO set radius 0 on rectangles and use only circle/square/triangle primitives. — ❌ DON'T mix in stars, blobs, or decorative illustrations.
- ✅ DO let one color block carry a whole section (solid blue field with white type). — ❌ DON'T decorate color fields with patterns, noise, or texture.

## Copy voice

Bauhaus copy is functional and declarative: short sentences, no adjectives for sale, no exclamation marks. It states what something is and what to do.

- "the exhibition is open. come and see how things are made."
- "three shapes. three colours. one function."
- "enrolment ends friday. the workshop does not wait."
