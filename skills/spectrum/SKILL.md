---
name: spectrum
description: Adobe Spectrum design system — quiet gray surfaces, blue-600 accents, Adobe Clean typography and precise creative-tool components. Use when a UI should feel like a professional Adobe product: calm, accessible, and out of the content's way.
---

# Spectrum (Adobe)

Adobe's design system for 100+ Creative Cloud / Document Cloud products (Photoshop, Express, Acrobat, Lightroom). Spectrum is version-sensitive: Spectrum 1 tokens differ from Spectrum 2. This skill targets the canonical Spectrum look: light theme, medium scale.

## Principles

Spectrum's four documented principles — Adobe kept the original three (Rational, Human, Focused) and added a fourth, Collaborative, for Spectrum 2. ✅ ([s2.spectrum.adobe.com](https://s2.spectrum.adobe.com/), [adobe.design](https://adobe.design/ideas/designing-design-systems-how-to-lay-the-groundwork-that-drives-decision-making))

1. **Rational.** Every element earns its place. Layout is grid-driven, spacing is systematic, decoration is absent. "Spectrum places people's needs first" without ornament getting in the way.
2. **Human.** High accessibility bar, honest copy, respect for user attention. Interfaces adapt to people — not the reverse — across desktop, web, mobile.
3. **Focused.** One task, one hierarchy. Accent color is rationed: it marks the single most important action, never decoration.
4. **Collaborative.** Built by a community of designers, researchers and engineers across Adobe; components behave consistently so skills transfer between products.

Two corollaries Spectrum itself states: **the chrome recedes so the content shines** (the original gray palette was deliberately designed to step back — ✅ [Adobe Blog](https://blog.adobe.com/en/publish/2023/12/12/adobe-unveils-spectrum-2-design-system-reimagining-user-experience-over-100-adobe-applications)), and motion is **purposeful, intuitive, seamless** (🟡 *Animation in Design Systems*, Head).

## Color

Legend: ✅ official/documented · 🟡 cross-referenced · ⚠️ community approximation.

| Token | Hex | Role |
|---|---|---|
| `blue-600` | ✅ `#1473E6` | Signature accent — primary actions, selected states, focus |
| `blue-700` (S1) | 🟡 `#0D66D0` | Accent hover/down |
| S2 accent default | 🟡 `#0D80D8` (`blue-500`) | Spectrum 2 primary accent |
| S2 accent hover | 🟡 `#0265BB` (`blue-600`) | Spectrum 2 hover |
| `gray-50` | 🟡 `#FFFFFF` | Page background |
| `gray-75` | 🟡 `#FAFAFA` | Layered surface |
| `gray-100` | 🟡 `#F5F5F5` | Raised surface |
| `gray-300` | 🟡 `#E1E1E1` | Default border |
| `gray-400` | 🟡 `#CACACA` | Strong border / control border |
| `gray-700` | 🟡 `#6E6E6E` | Secondary text |
| `gray-800` | 🟡 `#4B4B4B` | Primary text |
| `gray-900` | 🟡 `#2C2C2C` | Emphasized text / toast surface |
| `red-600` (negative) | 🟡 `#D31010` | Errors, destructive |
| `orange-600` (notice) | 🟡 `#D66D00` | Warnings |
| `green-600` (positive) | 🟡 `#008400` | Success |
| `static-white` / `static-black` | ✅ `#FFFFFF` / `#000000` | Text on colored fills |
| Focus indicator | ✅ | 2px outline, 2px offset, accent blue |

Notes:
- Spectrum 1's accent scale: `blue-400 #2680EB`, `blue-500 #1473E6`, `blue-600 #0D66D0` (🟡). Spectrum 2 rebuilt the scale around Adobe brand blues. If precision matters, check the version you're targeting.
- Dark theme inverts the gray ramp (page `#252525`, surface `#2C2C2C`, text `#D5D5D5`) — components reference semantic roles, never raw hex. 🟡
- Blue is the *only* hue allowed to carry meaning like "selected" or "primary action." Status colors carry the rest. Never add a third decorative hue.

```css
:root {
  --spectrum-accent: #1473E6;
  --spectrum-accent-hover: #0D66D0;
  --spectrum-page: #FFFFFF;
  --spectrum-surface: #FAFAFA;
  --spectrum-raised: #F5F5F5;
  --spectrum-border: #E1E1E1;
  --spectrum-border-strong: #CACACA;
  --spectrum-text: #4B4B4B;
  --spectrum-text-strong: #2C2C2C;
  --spectrum-text-secondary: #6E6E6E;
  --spectrum-negative: #D31010;
  --spectrum-notice: #D66D00;
  --spectrum-positive: #008400;
  --spectrum-focus: #1473E6;
}
```

## Typography

- **Typeface:** Adobe Clean (Adobe's proprietary signature face). ✅ Web fallback stack, documented in Spectrum CSS: `adobe-clean, "Adobe Clean", "Source Sans Pro", -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif`. Closest free stand-in: **Source Sans 3**. Mono: Source Code Pro.
- **Scale:** desktop (medium scale) body is 13–14px; Spectrum ships *two* type scales — desktop and a mobile/large scale at **1.25×** the desktop sizes, because fingers are less precise than cursors. 🟡
- **Rules:** sentence case for labels and headings; weights 400 for body, 700 for headings and emphasis only; tabular numerals in data. Line height ~1.5 body, ~1.2 headings. Never letterspace body text.

```css
font-family: "Adobe Clean", "Source Sans 3", "Source Sans Pro",
  -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif;
```

## Layout & spacing

- **Spacing grid:** 4px base — `size-100` = 4px, `size-200` = 8px, `size-300` = 12px, continuing in 4px steps. ✅ (documented in React Spectrum token guidance)
- **Spectrum scale:** *medium* (desktop, 32px control height) and *large* (touch, ~40px, 1.25× sizing). 🟡 Border widths stay constant across scales.
- **Radius:** 4px on cards, fields, popovers; **fully rounded pills** on buttons (16px radius at 32px height). ⚠️
- **Elevation:** flat by default. 1px `gray-300` borders separate surfaces — reach for shadows only on overlays/popovers, and keep them soft and short.
- **Chrome pattern:** quiet variants everywhere — toolbars of borderless action buttons that only show backgrounds on hover; panels with hairline dividers, no boxes-in-boxes.

## Components

Signature components with copy-pasteable HTML/CSS. (Anatomy cross-referenced from Spectrum docs 🟡; CSS is a faithful recreation.)

### 1. ActionButton (quiet) — the most Spectrum control there is
Borderless until hovered. Used in every Adobe toolbar.

```html
<button class="sp-action-button" aria-pressed="false">
  <svg width="18" height="18" viewBox="0 0 18 18" fill="none" stroke="currentColor" stroke-width="1.5">
    <path d="M9 2v14M2 9h14"/>
  </svg>
  <span>Add</span>
</button>
```

```css
.sp-action-button {
  display: inline-flex; align-items: center; gap: 6px;
  height: 32px; padding: 0 12px;
  background: transparent; border: 1px solid transparent; border-radius: 4px;
  color: #4B4B4B; font: 400 14px "Source Sans 3", sans-serif; cursor: pointer;
  transition: background-color 130ms cubic-bezier(0,0,.40,1), border-color 130ms cubic-bezier(0,0,.40,1);
}
.sp-action-button:hover { background: #F5F5F5; border-color: #E1E1E1; }
.sp-action-button:active { background: #EAEAEA; }
.sp-action-button:focus-visible { outline: 2px solid #1473E6; outline-offset: 2px; }
.sp-action-button[aria-pressed="true"] { background: #E1E1E1; color: #2C2C2C; }
.sp-action-button:disabled { color: #CACACA; cursor: default; background: transparent; border-color: transparent; }
```

### 2. Button — accent (pill) and secondary
Spectrum buttons are pills, never rectangles.

```html
<button class="sp-button sp-button--accent">Export</button>
<button class="sp-button sp-button--secondary">Cancel</button>
```

```css
.sp-button {
  height: 32px; padding: 0 16px; border-radius: 16px;
  font: 700 14px "Source Sans 3", sans-serif; cursor: pointer;
  transition: background-color 130ms cubic-bezier(0,0,.40,1), border-color 130ms cubic-bezier(0,0,.40,1);
}
.sp-button--accent { background: #1473E6; border: 1px solid #1473E6; color: #fff; }
.sp-button--accent:hover { background: #0D66D0; border-color: #0D66D0; }
.sp-button--secondary { background: #fff; border: 1px solid #CACACA; color: #4B4B4B; }
.sp-button--secondary:hover { background: #F5F5F5; border-color: #B3B3B3; }
.sp-button:focus-visible { outline: 2px solid #1473E6; outline-offset: 2px; }
.sp-button:disabled { opacity: .5; cursor: default; }
```

### 3. Picker (dropdown)
```html
<button class="sp-picker" aria-haspopup="listbox">
  <span class="sp-picker-label">Format</span>
  <span class="sp-picker-value">PNG</span>
  <svg width="12" height="12" viewBox="0 0 12 12" fill="none" stroke="currentColor" stroke-width="1.5">
    <path d="M2 4l4 4 4-4"/>
  </svg>
</button>
```

```css
.sp-picker {
  display: inline-flex; align-items: center; gap: 8px;
  height: 32px; min-width: 160px; padding: 0 8px 0 12px;
  background: #fff; border: 1px solid #CACACA; border-radius: 4px;
  font: 400 14px "Source Sans 3", sans-serif; color: #2C2C2C; cursor: pointer;
  transition: border-color 130ms cubic-bezier(0,0,.40,1);
}
.sp-picker:hover { border-color: #B3B3B3; }
.sp-picker:focus-visible { outline: 2px solid #1473E6; outline-offset: 2px; }
.sp-picker-label { color: #6E6E6E; }
.sp-picker-value { font-weight: 700; }
.sp-picker svg { margin-left: auto; color: #6E6E6E; }
.sp-picker--quiet { border-color: transparent; background: transparent; }
.sp-picker--quiet:hover { background: #F5F5F5; border-color: #E1E1E1; }
```

### 4. Slider
Thin track, filled portion in accent blue, round handle. Value sits right of the label.

```html
<div class="sp-slider">
  <div class="sp-slider-row">
    <label for="quality">Quality</label>
    <output id="quality-val" for="quality">92</output>
  </div>
  <input type="range" id="quality" min="0" max="100" value="92">
</div>
```

```css
.sp-slider { width: 240px; }
.sp-slider-row { display: flex; justify-content: space-between; font-size: 14px; color: #4B4B4B; margin-bottom: 8px; }
.sp-slider-row output { font-weight: 700; color: #2C2C2C; }
.sp-slider input[type="range"] {
  -webkit-appearance: none; appearance: none; width: 100%; height: 16px; background: transparent; cursor: pointer;
}
.sp-slider input[type="range"]::-webkit-slider-runnable-track {
  height: 4px; border-radius: 2px;
  background: linear-gradient(to right, #1473E6 0 var(--fill, 92%), #E1E1E1 var(--fill, 92%) 100%);
}
.sp-slider input[type="range"]::-webkit-slider-thumb {
  -webkit-appearance: none; width: 12px; height: 12px; margin-top: -4px;
  border-radius: 50%; background: #fff; border: 2px solid #8E8E8E;
}
.sp-slider input[type="range"]:active::-webkit-slider-thumb { border-color: #1473E6; }
.sp-slider input[type="range"]::-moz-range-track { height: 4px; border-radius: 2px; background: #E1E1E1; }
.sp-slider input[type="range"]::-moz-range-progress { height: 4px; border-radius: 2px; background: #1473E6; }
.sp-slider input[type="range"]::-moz-range-thumb { width: 8px; height: 8px; border-radius: 50%; background: #fff; border: 2px solid #8E8E8E; }
.sp-slider input[type="range"]:focus-visible { outline: 2px solid #1473E6; outline-offset: 2px; }
```
JS: `input.addEventListener('input', e => { e.target.style.setProperty('--fill', e.target.value + '%'); output.textContent = e.target.value; })`

### 5. Meter
Read-only level bar (storage, health), thin and quiet.

```html
<div class="sp-meter" role="meter" aria-valuenow="21" aria-valuemin="0" aria-valuemax="100" aria-label="Cloud storage">
  <div class="sp-meter-label"><span>Cloud storage</span><span>2.1 of 10 GB</span></div>
  <div class="sp-meter-track"><div class="sp-meter-fill" style="width:21%"></div></div>
</div>
```

```css
.sp-meter { width: 240px; }
.sp-meter-label { display: flex; justify-content: space-between; font-size: 13px; color: #6E6E6E; margin-bottom: 6px; }
.sp-meter-track { height: 8px; border-radius: 4px; background: #EAEAEA; overflow: hidden; }
.sp-meter-fill { height: 100%; border-radius: 4px; background: #1473E6; }
.sp-meter--positive .sp-meter-fill { background: #008400; }
.sp-meter--notice .sp-meter-fill { background: #D66D00; }
.sp-meter--negative .sp-meter-fill { background: #D31010; }
```

### 6. ProgressBar
For determinate operations; label above, percentage right.

```html
<div class="sp-progress" role="progressbar" aria-valuenow="0" aria-valuemin="0" aria-valuemax="100">
  <div class="sp-progress-label"><span id="export-label">Ready to export</span><span id="export-pct"></span></div>
  <div class="sp-progress-track"><div class="sp-progress-fill" id="export-fill" style="width:0%"></div></div>
</div>
```

```css
.sp-progress { width: 280px; }
.sp-progress-label { display: flex; justify-content: space-between; font-size: 13px; color: #4B4B4B; margin-bottom: 6px; }
.sp-progress-track { height: 6px; border-radius: 3px; background: #E1E1E1; overflow: hidden; }
.sp-progress-fill { height: 100%; border-radius: 3px; background: #1473E6; transition: width 200ms cubic-bezier(0,0,.40,1); }
```

### 7. IllustratedMessage (empty state)
The signature Spectrum empty state: simple line illustration, heading, one or two sentences, one optional action.

```html
<div class="sp-illustrated-message">
  <svg width="96" height="72" viewBox="0 0 96 72" fill="none" stroke="#8E8E8E" stroke-width="2">
    <rect x="8" y="12" width="80" height="48" rx="4"/>
    <circle cx="34" cy="32" r="6"/>
    <path d="M14 52l16-14 10 8 12-12 18 18"/>
  </svg>
  <h3>No artboards yet</h3>
  <p>Create your first artboard to start laying out this project. You can add more at any time.</p>
  <button class="sp-button sp-button--accent">Create artboard</button>
</div>
```

```css
.sp-illustrated-message { text-align: center; padding: 48px 24px; max-width: 400px; margin: 0 auto; }
.sp-illustrated-message h3 { font: 700 18px "Source Sans 3", sans-serif; color: #2C2C2C; margin: 16px 0 8px; }
.sp-illustrated-message p { font-size: 14px; line-height: 1.5; color: #6E6E6E; margin: 0 0 20px; }
```

### 8. Tabs
Underline style. The selected tab gets a 2px accent underline — never a filled pill.

```html
<div class="sp-tabs" role="tablist">
  <button class="sp-tab is-selected" role="tab" aria-selected="true">Canvas</button>
  <button class="sp-tab" role="tab" aria-selected="false">Export</button>
  <button class="sp-tab" role="tab" aria-selected="false">Publish</button>
</div>
```

```css
.sp-tabs { display: flex; gap: 4px; border-bottom: 1px solid #E1E1E1; }
.sp-tab {
  height: 40px; padding: 0 16px; background: none; border: none; cursor: pointer;
  font: 400 14px "Source Sans 3", sans-serif; color: #6E6E6E; position: relative;
}
.sp-tab:hover { color: #2C2C2C; }
.sp-tab.is-selected { color: #2C2C2C; font-weight: 700; }
.sp-tab.is-selected::after {
  content: ""; position: absolute; left: 8px; right: 8px; bottom: -1px;
  height: 2px; background: #1473E6; border-radius: 1px;
}
.sp-tab:focus-visible { outline: 2px solid #1473E6; outline-offset: -2px; }
```

### 9. Toast
Dark, floating, bottom-center. Used for confirmations ("Export complete").

```html
<div class="sp-toast" role="status">
  <svg width="16" height="16" viewBox="0 0 16 16" fill="none" stroke="#fff" stroke-width="2">
    <path d="M2.5 8.5l3.5 3.5 7-8"/>
  </svg>
  <span>Export complete — saved to Downloads.</span>
  <button class="sp-toast-close" aria-label="Dismiss">✕</button>
</div>
```

```css
.sp-toast {
  position: fixed; left: 50%; bottom: 24px; transform: translateX(-50%);
  display: flex; align-items: center; gap: 10px;
  background: #2C2C2C; color: #fff; font-size: 14px;
  padding: 12px 16px; border-radius: 8px; box-shadow: 0 4px 16px rgba(0,0,0,.25);
  animation: sp-toast-in 250ms cubic-bezier(0,0,.40,1);
}
.sp-toast-close { background: none; border: none; color: #B3B3B3; cursor: pointer; font-size: 14px; }
.sp-toast-close:hover { color: #fff; }
@keyframes sp-toast-in { from { opacity: 0; transform: translate(-50%, 8px); } }
```

## Motion

✅ from Adobe's published Spectrum CSS (`--spectrum-global-animation-*`):

| Token | Value | Use |
|---|---|---|
| `duration-100` | 130ms | Hover, press, focus ring, toggle |
| `duration-200` | 160ms | Checkbox, small state |
| `duration-600` | 300ms | Popover, tab switch |
| `duration-1000` | 500ms | Largest UI transition |
| `ease-out` | `cubic-bezier(0, 0, 0.40, 1)` | **Default.** Entrances — the element arrives fast and settles |
| `ease-in` | `cubic-bezier(.50, 0, 1, 1)` | Exits only |
| `ease-in-out` | `cubic-bezier(.45, 0, .40, 1)` | Moving between two on-screen positions |
| `linear` | `cubic-bezier(0, 0, 1, 1)` | Spinners and progress only |

Rules: motion is purposeful, intuitive, seamless — never decorative (🟡). Nothing over 500ms for UI. Exits are faster than entrances.

## Do / Don't

- **Do** ration blue: one accent action per view, gray for everything else. **Don't** color-code decorative elements — a blue card header or blue illustration "for branding" is not Spectrum.
- **Do** use quiet action buttons for toolbars and icon rows. **Don't** put a pill button in a toolbar; pills belong to dialogs and single primary actions.
- **Do** separate panels with 1px `gray-300` hairlines. **Don't** wrap cards in drop shadows — Spectrum surfaces sit flat on the page.
- **Do** write labels in sentence case ("Create artboard", not "Create Artboard"). **Don't** use all-caps labels or marketing exclamation marks.
- **Do** show empty states as IllustratedMessage (illustration + heading + one sentence + one action). **Don't** leave a blank panel or a bare "No data" string.
- **Do** use the medium/large scale switch for touch vs. mouse contexts (1.25×). **Don't** just bump font-size and call it responsive.
- **Do** keep focus rings visible and blue. **Don't** remove outlines for aesthetics — Spectrum's accessibility bar is the point.
- **Do** name tokens by role (`accent`, `border`, `text-secondary`), not by value. **Don't** hardcode hex outside the token layer.

## Copy voice

Concise, respectful, task-first. Sentence case. Errors say what happened and what to do next, without blame: "Export failed. Check your connection and try again." / "No artboards yet — create your first artboard to get started." / "Saved. Your changes are up to date."

## Sources

- Official: [s2.spectrum.adobe.com](https://s2.spectrum.adobe.com/) · [spectrum.adobe.com](https://spectrum.adobe.com/) · [Spectrum 2 announcement, Adobe Blog](https://blog.adobe.com/en/publish/2023/12/12/adobe-unveils-spectrum-2-design-system-reimagining-user-experience-over-100-adobe-applications) · [adobe.design on Spectrum principles](https://adobe.design/ideas/designing-design-systems-how-to-lay-the-groundwork-that-drives-decision-making) · Adobe's published Spectrum CSS tokens (durations/easings/static colors)
- Cross-referenced: React Spectrum token prose (`@adobe/react-spectrum`) · community Spectrum design-token references on GitHub
