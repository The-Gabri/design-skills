---
name: flat-design
description: Flat 2.0 (semi-flat): bold solid-color blocks, crisp geometry and simple iconography, with long shadows and subtle tinted depth only where something is interactive or layered. Use for clean, friendly marketing pages, dashboards and mobile-first UIs.
---

# Flat 2.0

## Confidence legend
- ✅ = stated in the style's canonical documentation (or Wikipedia's sourced account of it), confirmed in ≥2 independent sources.
- 🟡 = widely documented in design writing about the style, consistent across ≥3 sources, no single canonical quote.
- ⚠️ = community approximation or this skill's own curation — useful, not dogma.

## Principles
1. **Color does the work of depth.** Surfaces are distinguished by solid fills, not by floating above each other. If you can delete an effect and the hierarchy survives on color, type and spacing alone, delete the effect. ✅ (core flat principle; designbrief flat-design.md: "layering through color")
2. **Almost flat, not flat-flat.** Pure flat (zero shadows, zero gradients) lost affordances — users couldn't tell what was tappable. Flat 2.0 keeps the 2D aesthetic but adds back *subtle hints of physics* to communicate interactability. 🟡 ("Flat aesthetics, but with subtle hints of physics to communicate interactability" — design-it flat-design-2)
3. **Shadows are reserved for the interactive and the layered.** Elevation appears only on things you can press (buttons, FABs) or things that float (modals, popovers, cards). Low opacity, high blur, tinted with the surface/background color — never pure black. 🟡
4. **The long shadow is the signature graphic device.** A hard diagonal shadow in a darker tint of the surface color, used on icons, numerals and headline tiles to add punch without breaking flatness. It is decorative, not an elevation cue. 🟡 (widely documented Flat 2.0 technique, e.g. webdesignerdepot's Flat Design 2.0 roundup)
5. **Content before chrome.** Interfaces are built from typography, geometric shapes and bold color fields; decorative frames, borders and ornament are stripped out. ✅ (Microsoft Metro: "content before chrome", typography-first)
6. **Crisp geometry, honest materials.** Basic rectangles, circles and tiles; single-color icons (outline or filled, never mixed on one page); no textures, no noise, no photo-realism. Micro-gradients (a 2–4% lightness shift to keep a large surface from feeling dead) are the only acceptable gradient, and even those are optional. 🟡

## Color
Material Design's 2014 palette and Microsoft's Metro accent are the canonical flat-era references; the tokens below are documented values, not this skill's invention.

| Token | Hex | Role | Confidence |
|---|---|---|---|
| `--flat-blue` | `#2196F3` | primary accent / links | ✅ (Material Blue 500) |
| `--flat-indigo` | `#3F51B5` | deep accent / nav bars | ✅ (Material Indigo 500) |
| `--flat-teal` | `#009688` | success / brand bands | ✅ (Material Teal 500) |
| `--flat-green` | `#4CAF50` | success states | ✅ (Material Green 500) |
| `--flat-amber` | `#FFC107` | highlights, badges | ✅ (Material Amber 500) |
| `--flat-orange` | `#FF5722` | CTAs, warnings | ✅ (Material Deep Orange 500) |
| `--flat-red` | `#F44336` | destructive / errors | ✅ (Material Red 500) |
| `--flat-pink` | `#E91E63` | playful accent | ✅ (Material Pink 500) |
| `--flat-metro` | `#0078D7` | alternate primary (Windows-era) | ✅ (Microsoft accent blue, Windows 10) |
| `--flat-ink` | `#212121` | primary text | ✅ (Material text primary) |
| `--flat-ink-2` | `#757575` | secondary text / icons | ✅ (Material text secondary) |
| `--flat-line` | `#BDBDBD` | hairline dividers (rare) | ✅ (Material divider) |
| `--flat-paper` | `#FFFFFF` | surfaces | ✅ |
| `--flat-canvas` | `#FAFAFA` | page background | ✅ (Material background grey) |

Palette rules:
- **3–5 confident colors max per page.** Each color is used at full strength; no washed-out variants except tints for long shadows. 🟡
- **Long-shadow tint:** darken the surface color by ~12–15% (e.g. on `#FF5722`, use `#D84315`) or use `rgba(0,0,0,0.12)` stepped stacks. ⚠️
- **Elevation shadow tint:** `rgba(<surface-rgb>, 0.08–0.14)` — tinted with the background, never pure black. 🟡

## Typography
- **Canonical faces:** Segoe UI (Metro — "large lower case typography" ✅), Roboto (Material — ✅). Closest free substitutes: Open Sans, Lato, or a system sans stack. 🟡
- **Scale (web, ⚠️):** display 48–64px / H1 36–48 / H2 24–32 / body 16–18 / caption 12–14. Hierarchy comes from size and weight steps, since depth is gone.
- **Rules:** bold (600–800) weight carries emphasis, not color; generous line-height (1.5–1.6) on body; lowercase headings are a legitimate Metro nod ("wide tiles, lowercase headings" ✅); tight letter-spacing (-0.01em) on large display type only.

## Layout & spacing
- **8pt/dp baseline grid** for spacing and sizing ✅ (Material). Rhythm: 16 / 24 / 32 / 48 / 64.
- **Radius:** 2–4px on cards and buttons, or fully square. Flat does not do large pill radii everywhere — reserve pill for the single primary CTA at most. 🟡
- **Borders:** none, or 1px solid `--flat-line` at most. A card is distinguished from its background by a *different solid fill*, not by an outline. ✅ (designbrief: "layering through color")
- **Shadows:** content elements get none. Interactive/layered elements get one soft tinted shadow: e.g. `0 10px 30px rgba(33,33,33,0.10)`; press/hover deepens slightly and lifts `translateY(-2px)`. 🟡
- **Long shadows:** diagonal, bottom-right, hard-edged steps of the darkened surface tint; length 24–64px on icons/tiles, up to ~120px on display numerals. Decorative — never on body text or inputs. ⚠️

## Components

### 1. Long-shadow icon tile (the Flat 2.0 signature)
```html
<div class="ls-tile" aria-hidden="true">
  <!-- single-color SVG icon -->
  <svg width="32" height="32" viewBox="0 0 24 24" fill="none" stroke="#fff" stroke-width="2"><path d="M4 12l5 5L20 7"/></svg>
</div>
<style>
.ls-tile{
  width:72px;height:72px;border-radius:6px;background:#FF5722;
  display:grid;place-items:center;position:relative;
  /* stepped long shadow in a darker tint of the surface (#D84315) */
  box-shadow:6px 6px 0 #D84315,12px 12px 0 #D84315,18px 18px 0 #D84315,
             24px 24px 0 #D84315,30px 30px 0 rgba(0,0,0,.05);
}
</style>
```

### 2. Primary CTA button (solid, pressable, long-shadow on hover)
```html
<button class="btn-flat">Start free</button>
<style>
.btn-flat{
  background:#FF5722;color:#fff;border:0;border-radius:4px;
  padding:14px 28px;font:700 16px/1 "Segoe UI",system-ui,sans-serif;
  cursor:pointer;transition:transform .18s ease-out, box-shadow .18s ease-out;
  box-shadow:0 4px 12px rgba(216,67,21,.35); /* tinted with the button color */
}
.btn-flat:hover{ transform:translateY(-2px); box-shadow:0 8px 20px rgba(216,67,21,.40); }
.btn-flat:active{ transform:translateY(1px); box-shadow:0 2px 6px rgba(216,67,21,.35); }
</style>
```

### 3. Flat card with tinted elevation (content cards stay flat; only raised ones get this)
```html
<article class="flat-card">
  <h3>Instant payouts</h3>
  <p>Money lands in your account the day the invoice clears.</p>
</article>
<style>
.flat-card{
  background:#fff;border-radius:4px;padding:28px;
  box-shadow:0 10px 30px rgba(33,33,33,.08); /* tinted, not black */
}
</style>
```

### 4. Solid color-band section
```html
<section class="band">
  <h2>Get paid on time, every time.</h2>
  <button class="btn-flat btn-on-band">Try Kite free</button>
</section>
<style>
.band{ background:#009688; color:#fff; padding:72px 24px; text-align:center; }
.band .btn-flat{ background:#FF5722; }
</style>
```

### 5. Single-color icon badge
```html
<span class="icon-badge" aria-hidden="true">
  <svg width="20" height="20" viewBox="0 0 24 24" fill="currentColor"><path d="M13 2 4 14h6l-1 8 9-12h-6l1-8z"/></svg>
</span>
<style>
.icon-badge{ display:inline-grid; place-items:center; width:40px; height:40px;
  border-radius:50%; background:#2196F3; color:#fff; }
</style>
```

### 6. Flat tab bar (color state, no indicator underline gimmicks)
```html
<div class="tabs" role="tablist">
  <button class="tab is-active" role="tab" aria-selected="true">Send</button>
  <button class="tab" role="tab" aria-selected="false">Track</button>
  <button class="tab" role="tab" aria-selected="false">Get paid</button>
</div>
<style>
.tabs{ display:inline-flex; background:#fff; border-radius:4px; padding:4px;
  box-shadow:0 4px 14px rgba(33,33,33,.08); }
.tab{ border:0; background:transparent; padding:10px 22px; border-radius:3px;
  font:600 14px/1 "Segoe UI",system-ui,sans-serif; color:#757575; cursor:pointer; }
.tab.is-active{ background:#2196F3; color:#fff; }
</style>
```

### 7. Monthly/yearly pricing toggle
```html
<label class="switch">
  <span>Monthly</span>
  <input type="checkbox" id="billing-toggle">
  <span class="track" aria-hidden="true"><span class="knob"></span></span>
  <span>Yearly <em>−25%</em></span>
</label>
<style>
.switch{ display:inline-flex; align-items:center; gap:12px; font:600 14px "Segoe UI",system-ui,sans-serif; color:#212121; cursor:pointer; }
.switch input{ position:absolute; opacity:0; }
.track{ width:52px; height:28px; border-radius:4px; background:#BDBDBD; position:relative; transition:background .2s; }
.knob{ position:absolute; top:4px; left:4px; width:20px; height:20px; border-radius:3px; background:#fff; transition:left .2s; }
.switch input:checked + .track{ background:#009688; }
.switch input:checked + .track .knob{ left:28px; }
.switch em{ font-style:normal; color:#009688; }
</style>
```

### 8. Flat notice bar
```html
<p class="notice"><strong>Heads up:</strong> payouts pause on public holidays — plan invoices a day early.</p>
<style>
.notice{ background:#FFC107; color:#212121; padding:14px 18px; border-radius:4px;
  font:400 15px/1.5 "Segoe UI",system-ui,sans-serif; }
</style>
```

### 9. Flat input (bottom hairline, focus = color)
```html
<label class="field">Work email
  <input type="email" placeholder="you@studio.com">
</label>
<style>
.field{ display:block; font:600 13px "Segoe UI",system-ui,sans-serif; color:#757575; }
.field input{ display:block; width:100%; margin-top:6px; padding:12px 4px;
  border:0; border-bottom:2px solid #BDBDBD; background:transparent;
  font:400 16px "Segoe UI",system-ui,sans-serif; color:#212121; }
.field input:focus{ outline:none; border-bottom-color:#2196F3; }
</style>
```

## Motion
Flat 2.0 has no canonical motion language of its own; keep motion minimal and physical: 150–250ms `ease-out`, hover lifts of `translateY(-2px)`, shadow deepening on press. 🟡

## Do / Don't
- ✅ **Do** separate a card from its background with a different solid fill (white card on `#FAFAFA`). ❌ Don't add a black drop shadow to a static content card — shadows are reserved for interactive or floating layers.
- ✅ **Do** use the long shadow on icons, numerals and headline tiles in a darker tint of the surface. ❌ Don't put long shadows on body text, inputs or paragraphs — it kills legibility.
- ✅ **Do** tint elevation shadows with the background/surface color (`rgba(33,33,33,.10)`), low opacity and high blur. ❌ Don't use pure-black or hard `0 2px 4px #000` shadows.
- ✅ **Do** signal the primary action with the single boldest color on the page. ❌ Don't give two different CTAs the same orange — one color, one meaning.
- ✅ **Do** keep icons single-color (all outline or all filled) with consistent stroke width. ❌ Don't mix outline icons, filled icons and emoji on the same screen.
- ✅ **Do** let typography carry hierarchy: display size + bold weight + color. ❌ Don't fake emphasis with bevels, inner glows or skeuomorphic textures.

## Copy voice
Plain, confident, verb-driven. Short sentences, no jargon, no exclamation spam. The product does the talking.
- "Send an invoice. Get paid by Friday."
- "No accounting degree required."
- "Your money, on time — every time."

## Sources consulted
- Flat design — Wikipedia (Swiss/Bauhaus influence; Metro/Zune history; Material "Holo" era): https://en.wikipedia.org/wiki/Flat_design
- Metro (design language) — Wikipedia (typography-first, "content before chrome", lowercase headings, tiles; Segoe): https://en.wikipedia.org/wiki/Metro_(design_language)
- "Design trends: Flat Design 2.0" — Webdesigner Depot (Dropbox Guide, Tolia, Google Santa Tracker as 2.0 examples; subtle raised effects): https://webdesignerdepot.com/design-trends-flat-design-2-0/
- "Web Design Trends: Flat Design vs Flat Design 2.0" — articlesfactory.com (2.0 named with Material Design 2014; long shadow as signature technique): https://www.articlesfactory.com/articles/web-design/web-design-trends-flat-design-vs-flat-design-20.html
- Flat Design 2.0 (Semi-Flat) skill — design-it (core principles: mostly flat; subtle elevation tinted with background; micro-gradients): https://github.com/dxrk777/dxrk-ai/blob/HEAD/./agent/skills/design-it/flat-design-2/SKILL.md
- Flat Design — heiberg-industries/designbrief (zero-depth non-negotiables; layering through color): https://github.com/heiberg-industries/designbrief/blob/HEAD/styles/flat-design.md
