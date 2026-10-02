---
name: pop-art
description: Pop Art design language (Lichtenstein / Warhol) — Ben-Day dots, thick black outlines, flat primaries, comic panels, silkscreen repetition, onomatopoeia bursts. Use for bold retro-pop marketing pages, posters, and product drops.
---

# Pop Art

## Confidence legend
- ✅ = documented in multiple independent analyses of the artists/works (primary visual facts).
- 🟡 = cross-referenced (consistent across 3+ sources, no single canonical citation).
- ⚠️ = community approximation (my best-practice recipe — useful, not dogma).

## Purpose
Produce designs in the visual language of 1960s Pop Art — Roy Lichtenstein's comic-strip panels and Andy Warhol's silkscreen serials. The core idea: borrow the look of cheap mass reproduction (newsprint dots, flat ink, misregistration) and blow it up to monumental scale. ✅

## Principles
1. **Flatness is the point.** Colors are unmodulated flat planes; shading comes from Ben-Day dot patterns, never from gradients or soft shadows. ✅
2. **Black does the drawing.** Thick, even-weight black outlines contain every shape. No hairlines, no feathery edges. ✅
3. **Primary colors, pushed hard.** Lichtenstein's signature triad is red, yellow, blue on flat backgrounds; Warhol swaps in unnatural hot pinks, acid yellows, and electric cyans. ✅
4. **Repetition is the message.** Warhol repeats the identical motif in a grid, changing only the colorway — the serial image comments on mass production. ✅
5. **Words become graphics.** Onomatopoeia ("WHAM!", "POW!"), speech balloons, and caption boxes are primary visual elements, set in heavy display type. 🟡
6. **Embrace the print flaw.** Deliberate misregistration (offset dot layers) and silkscreen grain read as authenticity in this language, not mistakes. 🟡

## Color
Paper-white base, ink-black structure, flat primaries and Warhol neons on top.

| Token | Hex | Role | Confidence |
|---|---|---|---|
| `ink` | `#111111` | Outlines, display type, gutters | ✅ |
| `paper` | `#FFFFFF` | Default surface | ✅ |
| `pop-red` | `#E8112D` | Primary accent (Lichtenstein red) | 🟡 |
| `pop-yellow` | `#FFD100` | Primary accent, caption boxes | 🟡 |
| `pop-blue` | `#0057B8` | Primary accent (Lichtenstein blue) | 🟡 |
| `warhol-pink` | `#F4007A` | Warhol neon colorway | ⚠️ |
| `warhol-cyan` | `#00B0E0` | Warhol neon colorway | ⚠️ |
| `acid-green` | `#7ABF00` | Warhol acidic colorway | ⚠️ |
| `cream` | `#F5EFE0` | Aged-paper alternative to pure white | ⚠️ |

Rules: backgrounds are flat — one color per plane. Black is for line and type, never for large fills (except the nav bar). Never mix a soft gradient into this palette; if a surface needs depth, cover it in dots instead. 🟡

### Ben-Day dot recipes (CSS `radial-gradient`) ⚠️
```css
/* coarse — big comic-print shading (Lichtenstein's blown-up halftone) */
.benday-coarse {
  background-color: #FFFFFF;
  background-image: radial-gradient(circle, #111111 2.2px, transparent 2.6px);
  background-size: 14px 14px;
}
/* mid — texture on panels, balloons, product shots */
.benday-mid {
  background-color: #FFD100;
  background-image: radial-gradient(circle, rgba(17,17,17,.55) 1.6px, transparent 2px);
  background-size: 10px 10px;
}
/* fine — subtle paper grain */
.benday-fine {
  background-color: #FFFFFF;
  background-image: radial-gradient(circle, rgba(17,17,17,.28) 1px, transparent 1.4px);
  background-size: 7px 7px;
}
/* misregistration — second dot layer nudged 3px, Warhol-style offset */
.misregister { position: relative; }
.misregister::after {
  content: ""; position: absolute; inset: 0; pointer-events: none;
  background-image: radial-gradient(circle, rgba(232,17,45,.5) 1.6px, transparent 2px);
  background-size: 10px 10px; background-position: 3px 3px;
}
```

## Typography
- **Display:** heavy condensed sans in all caps — primary free face: **Archivo Black** (Google Fonts, system fallback `Impact, "Arial Black", sans-serif`). Onomatopoeia ("POW!", "ZAP!") is set italic, often with `-webkit-text-stroke` outline and a hard offset shadow. 🟡
- **Comic lettering:** uppercase, bold, centered — for speech balloons, caption boxes, burst badges. Free substitute: bold `Arial/Helvetica`, letter-spacing 0.02em. ⚠️
- **Body:** plain bold-ish sans (`Helvetica, Arial, sans-serif`), left-aligned, short sentences. Comic captions traditionally start with a bolded lead-in ("MEANWHILE…"). 🟡
- **Scale:** display headlines at `clamp(3rem, 10vw, 8rem)`; never timid. Body 1rem/1.5, but paragraphs stay short — this language narrates in panels, not essays.

## Layout & spacing
- **Comic grid:** panels separated by thick black gutters (8–12px of solid `ink`, or 4px borders on a black page background). One panel = one beat of the story. 🟡
- **Borders:** every card, button, and panel gets a `3px–5px solid #111` border. Small UI chrome (tags, inputs): 3px. Big cards/panels: 4–5px. ⚠️
- **Radius:** `0`. Pop Art is rectilinear; rounded corners read as a different decade. ⚠️
- **Shadows:** hard offset only — `box-shadow: 6px 6px 0 #111`. No blur, no spread. 🟡
- **Warhol grid:** 2×2 (or 4×1) of the identical motif, each tile a different colorway, tiles flush against each other. ✅
- **Caption boxes:** yellow `#FFD100` box with 3px black border, top-left inside a panel, uppercase comic lettering. 🟡
- **Density:** maximalist. Fill the page — dots, bursts, ticker strips. White space is suspicion.

## Components
Copy-pasteable HTML/CSS. All radii 0, all shadows hard-offset.

### 1. Chunky CTA button
```html
<a class="pop-btn" href="#buy">GRAB A 6-PACK!</a>
```
```css
.pop-btn {
  display: inline-block; font-family: Impact, "Arial Black", sans-serif;
  font-size: 1.25rem; letter-spacing: .03em; text-transform: uppercase;
  color: #111; background: #FFD100; border: 4px solid #111;
  padding: .8em 1.6em; box-shadow: 6px 6px 0 #111; text-decoration: none;
  transition: transform .08s steps(2), box-shadow .08s steps(2);
}
.pop-btn:hover { transform: translate(-2px,-2px); box-shadow: 8px 8px 0 #111; }
.pop-btn:active { transform: translate(4px,4px); box-shadow: 2px 2px 0 #111; }
```

### 2. Comic panel with caption box
```html
<figure class="panel">
  <figcaption class="caption">MEANWHILE, AT ZOOM LABS…</figcaption>
  <div class="panel-art benday-mid"><!-- art / SVG here --></div>
</figure>
```
```css
.panel { border: 5px solid #111; background: #fff; margin: 0; position: relative; }
.panel-art { min-height: 220px; }
.caption {
  position: absolute; top: 0; left: 0; z-index: 2;
  font: 700 .85rem Arial, Helvetica, sans-serif; letter-spacing: .04em;
  background: #FFD100; border: 3px solid #111; border-top: 0; border-left: 0;
  padding: .45em .8em; text-transform: uppercase;
}
```

### 3. Starburst badge (SVG, JS-generated points)
```html
<span class="burst" data-text="NEW!"></span>
```
```css
.burst { display: inline-block; width: 120px; height: 120px; }
.burst svg { width: 100%; height: 100%; overflow: visible; }
.burst-shape { fill: #E8112D; stroke: #111; stroke-width: 5; }
.burst-text {
  font-family: Impact, "Arial Black", sans-serif; font-size: 30px; fill: #fff;
  stroke: #111; stroke-width: 1.5; paint-order: stroke; letter-spacing: 1px;
}
```
```js
// 16-point jagged starburst — the POW!/ZAP! shape
function burstPoints(cx, cy, spikes, r1, r2) {
  const pts = [];
  for (let i = 0; i < spikes * 2; i++) {
    const r = i % 2 === 0 ? r1 : r2;
    const a = (Math.PI * i) / spikes - Math.PI / 2;
    pts.push((cx + r * Math.cos(a)).toFixed(1) + "," + (cy + r * Math.sin(a)).toFixed(1));
  }
  return pts.join(" ");
}
document.querySelectorAll(".burst").forEach(el => {
  const NS = "http://www.w3.org/2000/svg";
  const svg = document.createElementNS(NS, "svg");
  svg.setAttribute("viewBox", "0 0 200 200");
  const poly = document.createElementNS(NS, "polygon");
  poly.setAttribute("points", burstPoints(100, 100, 16, 98, 72));
  poly.setAttribute("class", "burst-shape");
  svg.appendChild(poly);
  const t = document.createElementNS(NS, "text");
  t.setAttribute("x", "100"); t.setAttribute("y", "112");
  t.setAttribute("text-anchor", "middle"); t.setAttribute("class", "burst-text");
  t.textContent = el.dataset.text || "POW!";
  svg.appendChild(t);
  el.appendChild(svg);
});
```

### 4. Speech bubble (with tail)
```html
<blockquote class="bubble">Tastes like a comic book feels.</blockquote>
```
```css
.bubble {
  position: relative; display: inline-block; background: #fff;
  border: 3px solid #111; padding: 1em 1.2em; max-width: 26ch;
  font: 700 1rem Arial, Helvetica, sans-serif;
}
.bubble::after { /* the tail */
  content: ""; position: absolute; left: 28px; bottom: -11px;
  width: 16px; height: 16px; background: #fff;
  border-right: 3px solid #111; border-bottom: 3px solid #111;
  transform: rotate(45deg) skew(12deg, 12deg);
}
```

### 5. Warhol colorway grid (same motif, 4 colorways)
```html
<div class="warhol-grid">
  <button class="warhol-tile" style="--c1:#E8112D;--c2:#FFD100" data-flavor="Classic Cola">…motif…</button>
  <button class="warhol-tile" style="--c1:#FFD100;--c2:#0057B8" data-flavor="Lemon Zing">…motif…</button>
  <button class="warhol-tile" style="--c1:#0057B8;--c2:#FFFFFF" data-flavor="Blue Bolt">…motif…</button>
  <button class="warhol-tile" style="--c1:#F4007A;--c2:#00B0E0" data-flavor="Pink Zowie">…motif…</button>
</div>
```
```css
.warhol-grid { display: grid; grid-template-columns: repeat(4, 1fr); gap: 0;
  border: 5px solid #111; }
.warhol-tile { border: 0; border-right: 5px solid #111; cursor: pointer;
  background: var(--c1); padding: 1.5rem; }
.warhol-tile:last-child { border-right: 0; }
.warhol-tile .motif { background: var(--c2); border: 3px solid #111; }
```

### 6. Onomatopoeia ticker (marquee strip)
```html
<div class="ticker" aria-hidden="true"><div class="ticker-track">
  <span>ICE-COLD ★ SUPER FIZZY ★ 100% ZOWIE ★ ZERO BORING SIPS ★ </span><span>…repeat…</span>
</div></div>
```
```css
.ticker { background: #111; color: #FFD100; border-top: 4px solid #111;
  border-bottom: 4px solid #111; overflow: hidden; white-space: nowrap; }
.ticker-track { display: inline-block; padding: .6em 0;
  font: 1.1rem Impact, "Arial Black", sans-serif; letter-spacing: .06em;
  animation: tick 18s linear infinite; }
@keyframes tick { to { transform: translateX(-50%); } }
```

### 7. Display headline with ink outline
```html
<h1 class="pop-display">TASTE<br>THE BANG!</h1>
```
```css
.pop-display {
  font-family: Impact, "Arial Black", sans-serif;
  font-size: clamp(3.5rem, 11vw, 8.5rem); line-height: .9; margin: 0;
  color: #E8112D; text-transform: uppercase;
  -webkit-text-stroke: 3px #111; paint-order: stroke fill;
  text-shadow: 6px 6px 0 #111;
}
```

## Motion
Pop Art has no native motion language — movement is print. On the web: hard cuts only. Use `steps()` or sub-100ms transitions for presses/pops; no fades, no blurs, no parallax. Comic panels may SLAM in on scroll (IntersectionObserver + `steps(4)` keyframes: drop in rotated/offset, snap to rest). Marquee tickers run `linear infinite` at ~16s. Respect `prefers-reduced-motion` (freeze the ticker, skip pops and slams).

## Do / Don't
- ✅ DO shade with Ben-Day dots on a flat color. ❌ DON'T use a soft linear-gradient to fake depth — gradients are the sworn enemy of this style.
- ✅ DO outline every card/button/panel with 4px+ solid black and a hard offset shadow. ❌ DON'T use 1px hairlines, rounded corners, or blurred drop shadows.
- ✅ DO repeat the identical product image in a 2×2 grid with a different colorway per tile. ❌ DON'T show one "lifestyle photo" — the serial grid IS the product shot.
- ✅ DO make headlines heavy condensed caps ("TASTE THE BANG!") with onomatopoeia in italic. ❌ DON'T set the hero in a polite geometric sans at regular weight.
- ✅ DO use speech balloons, caption boxes ("MEANWHILE…"), and starburst badges for calls to action. ❌ DON'T use pill buttons with subtle elevation.
- ✅ DO keep copy loud, short, and exclamatory. ❌ DON'T write long explanatory paragraphs — if it needs three sentences, it needs three panels.

## Copy voice
Loud retro-ad copy: exclamations, onomatopoeia, short punchy sentences, comic captions. Think 1960s soda ad meets comic-book narrator.
- "STEP INTO THE POW! New 'WHAM' runners — air-pop cushion, Ben-Day everything, 500 numbered pairs!"
- "MEANWHILE, AT POW! LABS… Dr. Fizz adds the secret third bubble. KABOOM!"
- "4 COLORWAYS! 0 RESTOCK! Pick your print — the shoe alone deserves a museum wall."

## Sources consulted
- "Roy Lichtenstein and the Rise of Pop Art" — loughercontemporary.com (Ben-Day dots via stencils, primaries red/yellow/blue, thick black outlines on flat grounds)
- "The Language of Ben-Day Dots and Bold Lines" — ArtsDot / wahooart artist analyses (dots as mass-production commentary, enlarged comic panels, *Whaam!*, *Drowning Girl*)
- "Andy Warhol Pop Art Style" — backlot.aths.org (flat saturated color planes, serial repetition, silkscreen as mass-production method; *Marilyn Diptych*, *Campbell's Soup Cans*)
- "How was Andy Warhol's Campbell Soup made" — ansoup.com (projected outline + silkscreened ink layers, 32-canvas serial uniformity)
