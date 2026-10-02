---
name: neumorphism
description: Neumorphism (soft UI) — extruded and inset surfaces sculpted from a single background color with paired light/dark shadows. Use for calm, tactile interfaces: smart-home panels, music players, thermostats, calculators, settings screens.
---

# Neumorphism (Soft UI)

## Confidence legend
- ✅ = documented by the style's originators or consistently described in every independent analysis checked.
- 🟡 = cross-referenced community recipe: consistent across ≥3 independent sources, but not canon from a single authority.
- ⚠️ = community approximation: works well in practice, but is a judgment call, not doctrine.

## Principles
1. **One material everywhere.** Every surface shares the same base color as the background — elements don't float *above* it, they are *sculpted from* it. The self-test: card bg and page bg must be the same value. ✅
2. **The dual-shadow pair is the whole trick.** Each raised element carries two shadows at once: a dark shadow to the bottom-right (gravity) and a light shadow to the top-left (an implied light source). Remove one and the illusion dies. ✅
3. **Pressed = inverted shadows.** Interactive states flip the pair *inward* with `inset`: buttons sink, inputs become wells. The state change is shadow-only; color never changes. ✅
4. **Softness is the aesthetic.** Shadows are wide, blurred, and low-contrast. If the shadow edges look hard or the depth looks "cut out", increase blur — blur is the style. 🟡
5. **Restraint, or it turns to mush.** Neumorphism only reads with generous whitespace and a low element count. Stacked neumorphic cards on neumorphic cards collapse into an unreadable soft blob. 🟡
6. **Contrast must be borrowed.** The style is low-contrast by design and routinely fails WCAG. Never rely on it alone for critical actions: one filled accent CTA, dark body text, and visible focus rings are non-negotiable. 🟡

## Origin
Neumorphism ("new skeuomorphism") went viral in late 2019 / early 2020 from designer **Alexander Plyuto's** Dribbble shot of a banking-app concept — flat design's cleanliness with skeuomorphism's tactility. The term was coined by **Michał Malewicz** (Hype4) in 2019. Plyuto later published a free Neomorphism Guide for Figma/Adobe XD with light and dark variants. ✅

## Color
The palette is near-monochrome by definition; color arrives only through one accent.

| Token | Hex | Role | Confidence |
|---|---|---|---|
| `surface` (classic) | `#e0e5ec` | page bg AND every element bg | ✅ most-cited canonical base |
| `surface` (alt) | `#f0f0f3` | slightly brighter variant | 🟡 in Plyuto's guide + guides |
| `surface-dark` | `#2c313a` | dark-mode base | ⚠️ community standard |
| `shadow-dark` | `#a3b1c6` | bottom-right shadow (light mode) | 🟡 most-cited pairing with `#e0e5ec` |
| `shadow-light` | `#ffffff` | top-left highlight (light mode) | 🟡 |
| `shadow-dark` (alt) | `#b8bcc2` | warmer dark shadow | 🟡 alternate recipe |
| `shadow-dark-mode` | `#1a1e24` / highlight `#3d444f` | dark-mode shadow pair | ⚠️ |
| `text` | `#3f4756` | body text — ≥6:1 on `#e0e5ec` | ⚠️ accessibility-tuned pick |
| `text-muted` | `#6b7280` | secondary text — use only ≥18px or bold | ⚠️ min 4.5:1 |
| `accent` | `#e07b39` | the single saturated accent (CTA, active states) | ⚠️ pick any saturated accent; one only |

Rules: never put a gradient background behind neumorphic surfaces — the shadows stop matching and the illusion breaks 🟡. Background must be flat. ⚠️ For dark mode, reduce both shadow opacities (~60% of light-mode strength) or the relief looks carved too deep.

## Typography
Quiet, clean, medium-weight sans-serifs. The surfaces are the star — type stays out of the way. ✅/🟡

- **Closest free faces:** Nunito, Rubik, Poppins, DM Sans, Outfit (headings, 500–600); body in the same family at 400. System stack (`system-ui`) is always acceptable. 🟡
- **Avoid:** light/thin weights (they dissolve into the softness), black/900 weights, and serifs — they fight the plastic softness. ✅ (consistent in every analysis)
- **Scale:** comfortable and roomy; generous line-height (1.5+) because text must survive next to low-contrast surfaces. ⚠️

## Layout & spacing
- **Radius:** nothing sharp — "edges are almost rounded". 🟡 Small controls 12–16px, cards 20–30px, toggles/dials pill or full circle.
- **Shadow math:** offset : blur ≈ 1 : 2 (e.g. `8px 8px 16px`). Inset (pressed) shadows run at roughly **half** that magnitude (`inset 4px 4px 8px`). Hover states widen slightly (`10px 10px 20px`). 🟡
- **Spacing:** 8pt-friendly scale but biased loose — whitespace is load-bearing here. Keep raised elements ≥24px apart. ⚠️
- **Borders:** none. No divider lines, no strokes; shape comes only from the shadow pair. ✅ One exception: a visible `:focus-visible` ring on interactive elements (accessibility, see Do/Don't).

### The three shadow recipes (copy-paste)

```css
:root {
  --neu-bg: #e0e5ec;      /* page AND element background */
  --neu-dark: #a3b1c6;    /* bottom-right shadow */
  --neu-light: #ffffff;   /* top-left highlight */
  --neu-text: #3f4756;
  --neu-accent: #e07b39;
}

/* RAISED — cards, buttons at rest, toggles' knobs */
.neu-raised {
  background: var(--neu-bg);
  border-radius: 20px;
  box-shadow:
    8px 8px 16px var(--neu-dark),
    -8px -8px 16px var(--neu-light);
}

/* INSET / PRESSED — active buttons, input wells, slider tracks */
.neu-inset {
  background: var(--neu-bg);
  border-radius: 20px;
  box-shadow:
    inset 4px 4px 8px var(--neu-dark),
    inset -4px -4px 8px var(--neu-light);
}

/* FLAT — plain labels on the surface */
.neu-flat { background: var(--neu-bg); }
```
🟡 Recipes cross-referenced across Plyuto's guide derivatives, neumorphism.io-era generators, and 4+ independent write-ups.

## Components

### 1. Pressable button (raised → inset on active)
```html
<button class="neu-btn">Save changes</button>
```
```css
.neu-btn {
  background: #e0e5ec;
  color: #3f4756;
  border: none;
  border-radius: 14px;
  padding: 14px 28px;
  font-weight: 600;
  box-shadow: 6px 6px 12px #a3b1c6, -6px -6px 12px #ffffff;
  transition: box-shadow 0.18s ease-out;
  cursor: pointer;
}
.neu-btn:hover  { box-shadow: 8px 8px 18px #a3b1c6, -8px -8px 18px #ffffff; }
.neu-btn:active { box-shadow: inset 4px 4px 8px #a3b1c6, inset -4px -4px 8px #ffffff; }
.neu-btn:focus-visible { outline: 3px solid #e07b39; outline-offset: 3px; }
```

### 2. Extruded card
```html
<article class="neu-card">
  <h3>Living room</h3>
  <p>21.5°C · Humidity 42%</p>
</article>
```
```css
.neu-card {
  background: #e0e5ec;
  border-radius: 24px;
  padding: 28px;
  box-shadow: 10px 10px 20px #a3b1c6, -10px -10px 20px #ffffff;
}
```

### 3. Toggle switch (inset track, raised knob)
```html
<button class="neu-toggle" role="switch" aria-checked="false" aria-label="Away mode">
  <span class="neu-knob"></span>
</button>
```
```css
.neu-toggle {
  width: 64px; height: 34px; border: none; border-radius: 999px;
  background: #e0e5ec; cursor: pointer; position: relative;
  box-shadow: inset 4px 4px 8px #a3b1c6, inset -4px -4px 8px #ffffff;
  transition: box-shadow 0.2s ease-out;
}
.neu-knob {
  position: absolute; top: 4px; left: 4px; width: 26px; height: 26px;
  border-radius: 50%; background: #e0e5ec;
  box-shadow: 3px 3px 6px #a3b1c6, -3px -3px 6px #ffffff;
  transition: transform 0.2s ease-out, background 0.2s ease-out;
}
.neu-toggle[aria-checked="true"] .neu-knob { transform: translateX(30px); background: #e07b39; }
.neu-toggle:focus-visible { outline: 3px solid #e07b39; outline-offset: 3px; }
```

### 4. Slider (inset track, raised thumb)
```html
<label class="neu-slider-label" for="brightness">Brightness <output id="brightness-val">60%</output></label>
<input class="neu-slider" id="brightness" type="range" min="0" max="100" value="60">
```
```css
.neu-slider { -webkit-appearance: none; appearance: none; width: 100%; height: 12px;
  border-radius: 999px; background: #e0e5ec; outline-offset: 4px;
  box-shadow: inset 3px 3px 6px #a3b1c6, inset -3px -3px 6px #ffffff; }
.neu-slider::-webkit-slider-thumb { -webkit-appearance: none; width: 28px; height: 28px;
  border-radius: 50%; background: #e0e5ec; border: none; cursor: pointer;
  box-shadow: 4px 4px 8px #a3b1c6, -4px -4px 8px #ffffff; }
.neu-slider::-moz-range-thumb { width: 28px; height: 28px; border-radius: 50%;
  background: #e0e5ec; border: none; cursor: pointer;
  box-shadow: 4px 4px 8px #a3b1c6, -4px -4px 8px #ffffff; }
.neu-slider::-moz-range-track { height: 12px; border-radius: 999px; background: #e0e5ec;
  box-shadow: inset 3px 3px 6px #a3b1c6, inset -3px -3px 6px #ffffff; }
```

### 5. Input well
```html
<input class="neu-input" type="text" placeholder="Device name" aria-label="Device name">
```
```css
.neu-input {
  background: #e0e5ec; border: none; border-radius: 14px;
  padding: 14px 18px; color: #3f4756; width: 100%;
  box-shadow: inset 4px 4px 8px #a3b1c6, inset -4px -4px 8px #ffffff;
}
.neu-input::placeholder { color: #6b7280; }
.neu-input:focus { outline: 3px solid #e07b39; outline-offset: 2px; }
```

### 6. Segmented tabs
```html
<div class="neu-segmented" role="tablist" aria-label="Mode">
  <button role="tab" aria-selected="true" class="is-active">Heat</button>
  <button role="tab" aria-selected="false">Cool</button>
  <button role="tab" aria-selected="false">Auto</button>
</div>
```
```css
.neu-segmented { display: inline-flex; gap: 6px; padding: 6px; border-radius: 999px;
  background: #e0e5ec;
  box-shadow: inset 4px 4px 8px #a3b1c6, inset -4px -4px 8px #ffffff; }
.neu-segmented button { border: none; background: transparent; color: #6b7280;
  border-radius: 999px; padding: 10px 22px; font-weight: 600; cursor: pointer; }
.neu-segmented button.is-active { color: #3f4756; background: #e0e5ec;
  box-shadow: 4px 4px 8px #a3b1c6, -4px -4px 8px #ffffff; }
```

### 7. Icon well (inset socket for an SVG glyph)
```html
<span class="neu-iconwell" aria-hidden="true">
  <!-- inline SVG icon here, stroke #3f4756 -->
</span>
```
```css
.neu-iconwell { display: inline-grid; place-items: center; width: 56px; height: 56px;
  border-radius: 18px; background: #e0e5ec;
  box-shadow: inset 4px 4px 8px #a3b1c6, inset -4px -4px 8px #ffffff; }
```

## Motion
Neumorphism has no canonical motion language — the style is a surface treatment, not a system. Keep it minimal: 150–250ms `ease-out` transitions on shadow flips (raised ↔ inset), knob slides, and thumb drags; no springs, no bounce. ⚠️ Respect `prefers-reduced-motion` (state changes become instant).

## Do / Don't
- ✅ DO match surface color to the page background exactly — one flat color, no gradients behind the relief.
- ❌ DON'T put neumorphic surfaces over gradient or photo backgrounds; the shadow pair stops matching and elements look like stickers.
- ✅ DO use inset for anything that receives input: text fields, slider tracks, toggle tracks, active tabs.
- ❌ DON'T mark a primary CTA with soft shadows alone — pair the key action with a filled accent button so it reads at a glance.
- ✅ DO keep labels and body text at ≥4.5:1 contrast (`#3f4756` on `#e0e5ec` passes comfortably); reserve muted gray for large/bold text only.
- ❌ DON'T set small gray text on the surface (the classic neumorphism failure: ~1.6:1 ghost labels nobody can read).
- ✅ DO add a visible `:focus-visible` ring (accent outline) on every interactive element.
- ❌ DON'T stack neumorphic cards inside neumorphic cards — relief on relief reads as mush.
- ✅ DO keep the element count low: 4–6 extruded tiles per screen max, with real whitespace between them.
- ❌ DON'T use hard, tight shadows or sharp corners — if it doesn't look squeezable, it's not neumorphism.

## Copy voice
Neumorphism is a product style, not a brand voice: copy stays calm, plain, and functional — short labels, no exclamation marks, no hype. Let the tactility carry the delight.

- "Living room · 21.5°"
- "Hold to confirm — the dial clicks when it's set."
- "Away mode is on. We'll keep it at 17° until you're back."

## Sources
- Alexander Plyuto's Neomorphism Guide freebie (light + dark variants, via freebieflux) — origin and canonical recipes.
- Michał Malewicz / Hype4 — coined "neumorphism" (new + skeuomorphism), 2019.
- Cross-checked recipes: neumorphism.io-era CSS generators, dev.to soft-UI walkthrough, heiberg-industries designbrief, trixsec frontend-skills, aievolutionpl agent-design-taste, mmrahmanbappi 100-css-designs (accessible smart-home template), pitayacore + soupz-stall + physalia neumorphism skill notes.
