---
name: material-3
description: Google Material Design 3 / Material You — tonal color roles, type/shape/elevation tokens, and M3 components. Use for Android-first products, settings pages, and dynamic-color theming.
---

# Material 3 (M3 / Material You)

Google's open design system (m3.material.io), third generation. Material You adds
**dynamic color**: a whole tonal scheme generated from one seed color, so the UI
feels personal on every device. Expressive, rounded, optimistic — the look of
modern Android (Pixel UI, Google apps).

## Principles

1. **Color is semantic, never literal.** Components reference roles (`primary`,
   `surfaceContainerHigh`), not hex values. One seed color generates ~40
   coordinated roles via tonal palettes (TonalSpot/HCT), so light/dark mode and
   re-theming are free. ✅ official/documented
2. **Elevation is tone, not shadow.** Raised surfaces get lighter/darker in
   light/dark mode (the `surfaceContainer` family) instead of drop shadows.
   Shadows are subtle and secondary. ✅ official/documented
3. **Everything is a container of tone.** Buttons, chips, FABs, nav indicators,
   dialogs — all express hierarchy through filled tonal containers and pill
   shapes, not borders. ✅ official/documented
4. **State layers carry feedback.** Hover/press/focus paint a translucent layer
   of the "on" color over the component (hover ≈ 8%, focus ≈ 12%, pressed ≈ 12%,
   dragged ≈ 16% of on-surface). 🟡 cross-referenced
5. **One typeface, many roles.** A single family (Roboto) in a 15-style scale;
   hierarchy comes from size/weight/role, not from mixing fonts. ✅
   official/documented
6. **Delight through motion.** Transitions use emphasized easing for important
   moves; M3 Expressive extends this with springy, bouncy, personality-rich
   motion. ✅ official/documented

## Color

M3 assigns **roles**, not hexes. Below is the official **baseline scheme** (the
purple scheme m3.material.io ships with, seed `#6750A4`) — use it as an example,
or generate your own from a seed.

Light scheme (baseline): ✅ official/documented
- `--md-primary: #6750A4` — key actions, filled buttons, FAB, active states
- `--md-on-primary: #FFFFFF` — text/icons on primary
- `--md-primary-container: #EADDFF` — softer primary surfaces (tonal buttons, selected chips)
- `--md-on-primary-container: #21005D` — text on primary-container
- `--md-secondary: #625B71`, `--md-on-secondary: #FFFFFF`, `--md-secondary-container: #E8DEF8`, `--md-on-secondary-container: #1D192B`
- `--md-tertiary: #7D5260` — contrasting accent (often used for FAB), `--md-tertiary-container: #FFD8E4`
- `--md-surface: #FEF7FF` — page/app background (never pure white)
- `--md-surface-dim: #DED8E1`, `--md-surface-bright: #FEF7FF`
- `--md-surface-container-lowest: #FFFFFF`, `--md-surface-container-low: #F7F2FA`, `--md-surface-container: #F3EDF7`, `--md-surface-container-high: #ECE6F0`, `--md-surface-container-highest: #E6E0E9` — tonal depth ladder; pick by elevation
- `--md-on-surface: #1C1B1F` — body text; `--md-on-surface-variant: #49454F` — secondary text/icons
- `--md-outline: #79747E` (borders), `--md-outline-variant: #CAC4D0` (dividers)
- `--md-error: #B3261E`, `--md-on-error: #FFFFFF`, `--md-error-container: #F9DEDC`

Dark scheme (baseline): 🟡 cross-referenced (values from M3 baseline dark scheme)
- `--md-primary: #D0BCFF`, `--md-on-primary: #381E72`, `--md-primary-container: #4F378B`, `--md-on-primary-container: #EADDFF`
- `--md-surface: #141218`, `--md-surface-container-lowest: #0F0D13`, `--md-surface-container-low: #1D1B20`, `--md-surface-container: #211F26`, `--md-surface-container-high: #2B2930`, `--md-surface-container-highest: #36343B`
- `--md-on-surface: #E6E0E9`, `--md-on-surface-variant: #CAC4D0`, `--md-outline: #938F99`, `--md-outline-variant: #49454F`
- `--md-error: #F2B8B5`, `--md-on-error: #601410`, `--md-error-container: #8C1D18`

**Dynamic color / TonalSpot** (Material You): ✅ official/documented concept
- One **seed color** → 5 tonal palettes (primary, secondary, tertiary, neutral,
  neutral-variant), each tones 0–100 in HCT color space.
- Tertiary hue is offset **+60°** from the primary hue.
- Neutral palettes inherit the seed hue at very low chroma (this is why M3
  surfaces look "tinted", never pure gray).
- Light roles pull from tones 40/90/10/98…, dark roles from 80/30/90/6…
  (primary 40 light / 80 dark; primaryContainer 90 light / 30 dark; surface 98
  light / 6 dark; surfaceContainer 94/12, …).
- `on*` roles are guaranteed readable on their parent role — always pair
  `X` with `onX` for text/icons. ✅ official/documented
- ⚠️ Community approximation: web demos (including this skill's demo) typically
  approximate HCT with OKLCH/HSL tonal interpolation — close in spirit, not the
  exact TonalSpot output.

## Typography

Roboto (Google Fonts), or system-ui fallback. M3 uses exactly one family for the
whole product. ✅ official/documented

M3 type scale (size / weight / line-height / tracking): ✅ official/documented
- Display L 57/400/64/−0.25 · M 45/400/52/0 · S 36/400/44/0 — hero, huge numerals
- Headline L 32/400/40/0 · M 28/400/36/0 · S 24/400/32/0 — page/section titles
- Title L 22/400/28/0 · M 16/500/24/+0.15 · S 14/500/20/+0.1 — top-app-bar, card titles
- Body L 16/400/24/+0.5 · M 14/400/20/+0.25 · S 12/400/16/+0.4 — reading text
- Label L 14/500/20/+0.1 · M 12/500/16/+0.5 · S 11/500/16/+0.5 — buttons, badges, captions

Rules: buttons use **Label Large** (14/500); display/headlines stay Regular 400 —
M3 never bolds hero text; body tracking is positive (+0.25–0.5), never tight.

## Layout & spacing

- **8dp baseline grid**; spacing steps 4, 8, 12, 16, 24, 32, 48. 16dp screen
  margins on phone; touch targets ≥ 48dp. ✅ official/documented
- **Shape scale** (closed — use only these): ✅ official/documented
  none 0 · extraSmall 4 · small 8 · medium 12 · large 16 · extraLarge 28 ·
  full = pill (9999px). M3 Expressive adds largeIncreased 20 / extraLargeIncreased 32.
- Common mapping: buttons → full pill; FAB → large (16); cards → medium (12);
  dialogs/sheets → extraLarge (28); chips → small (8); text fields → extraSmall (4).
- **Elevation** levels (dp): Level0 0 · Level1 1 · Level2 3 · Level3 6 · Level4 8 ·
  Level5 12. ✅ official/documented. In M3, prefer expressing elevation with the
  `surfaceContainer*` tonal ladder over shadows.

## Components

Copy-pasteable HTML/CSS. Assumes the CSS variables from **Color** above and
Roboto loaded. All interactive components get a state layer: a translucent `on-*`
overlay on hover (8%) / focus (12%) / pressed (12%).

Icons: use **inline SVGs** (Material Symbols paths are Apache-licensed), never an
icon font — a failed font or ligature silently drops icons. 24px viewBox,
`fill: currentColor`:
```html
<svg viewBox="0 0 24 24" width="24" height="24" fill="currentColor" aria-hidden="true">
  <path d="M9 16.17L4.83 12l-1.42 1.41L9 19 21 7l-1.41-1.41z"/><!-- check -->
</svg>
```
Selected switches also show the check glyph inside the thumb (16px, in the
primary color), per the M3 spec.

### 1. Buttons — filled, tonal, outlined, text, elevated

```html
<button class="m3-btn filled">Label</button>
<button class="m3-btn tonal">Label</button>
<button class="m3-btn outlined">Label</button>
<button class="m3-btn textbtn">Label</button>
```
```css
.m3-btn{font:500 14px/20px Roboto,system-ui,sans-serif;letter-spacing:.1px;
  height:40px;padding:0 24px;border-radius:9999px;border:0;cursor:pointer;
  position:relative;overflow:hidden;transition:box-shadow .2s}
.m3-btn::after{content:"";position:absolute;inset:0;background:transparent;transition:background .15s}
.m3-btn:hover::after{background:color-mix(in srgb,currentColor 8%,transparent)}
.filled{background:var(--md-primary);color:var(--md-on-primary);box-shadow:0 1px 2px rgb(0 0 0/.3)}
.filled:hover{box-shadow:0 1px 3px 1px rgb(0 0 0/.15),0 1px 2px rgb(0 0 0/.3)}
.tonal{background:var(--md-secondary-container);color:var(--md-on-secondary-container)}
.outlined{background:transparent;color:var(--md-primary);border:1px solid var(--md-outline)}
.textbtn{background:transparent;color:var(--md-primary);padding:0 12px}
.m3-btn:disabled{background:color-mix(in srgb,var(--md-on-surface) 12%,transparent);
  color:color-mix(in srgb,var(--md-on-surface) 38%,transparent);box-shadow:none;cursor:default}
```

### 2. FAB (floating action button)

```html
<button class="m3-fab" aria-label="Create">+</button>
```
```css
.m3-fab{width:56px;height:56px;border-radius:16px;border:0;cursor:pointer;
  background:var(--md-primary-container);color:var(--md-on-primary-container);
  font:400 24px/1 Roboto,system-ui;box-shadow:0 4px 8px 3px rgb(0 0 0/.15),0 1px 3px rgb(0 0 0/.3)}
```
Use tertiary-container for the classic accent FAB; extended FAB adds a Label
Large caption next to the icon.

### 3. Cards — elevated, filled, outlined

```html
<div class="m3-card filled"><h3 class="t-title-l">Card title</h3><p class="t-body-m">Supporting text.</p></div>
```
```css
.m3-card{border-radius:12px;padding:16px;max-width:340px}
.m3-card.elevated{background:var(--md-surface-container-low);box-shadow:0 1px 2px rgb(0 0 0/.3),0 1px 3px 1px rgb(0 0 0/.15)}
.m3-card.filled{background:var(--md-surface-container-highest)}
.m3-card.outlined{background:var(--md-surface);border:1px solid var(--md-outline-variant)}
```

### 4. Navigation bar (bottom) with pill indicator

```html
<nav class="m3-navbar">
  <a class="active" href="#"><span class="pill">●</span>Home</a>
  <a href="#"><span class="pill">●</span>Search</a>
  <a href="#"><span class="pill">●</span>Library</a>
</nav>
```
```css
.m3-navbar{display:flex;background:var(--md-surface-container);padding:8px}
.m3-navbar a{flex:1;display:flex;flex-direction:column;align-items:center;gap:4px;
  font:500 12px/16px Roboto,system-ui;color:var(--md-on-surface-variant);text-decoration:none;padding:4px}
.m3-navbar .pill{width:64px;height:32px;border-radius:9999px;display:grid;place-items:center}
.m3-navbar a.active{color:var(--md-on-surface)}
.m3-navbar a.active .pill{background:var(--md-secondary-container);color:var(--md-on-secondary-container)}
```

### 5. Chips — assist, filter, input, suggestion

```html
<button class="m3-chip">Assist</button>
<button class="m3-chip selected">Filter ✓</button>
```
```css
.m3-chip{height:32px;padding:0 16px;border-radius:8px;border:1px solid var(--md-outline);
  background:transparent;color:var(--md-on-surface-variant);font:500 14px/20px Roboto,system-ui;cursor:pointer}
.m3-chip.selected{background:var(--md-secondary-container);border-color:transparent;color:var(--md-on-secondary-container)}
```

### 6. Switch

```html
<button class="m3-switch" role="switch" aria-checked="true"><span class="thumb"></span></button>
```
```css
.m3-switch{width:52px;height:32px;border-radius:9999px;border:2px solid var(--md-outline);
  background:var(--md-surface-container-highest);position:relative;cursor:pointer;transition:all .2s}
.m3-switch .thumb{position:absolute;top:50%;left:4px;translate:0 -50%;width:16px;height:16px;
  border-radius:50%;background:var(--md-outline);transition:all .2s}
.m3-switch[aria-checked="true"]{background:var(--md-primary);border-color:var(--md-primary)}
.m3-switch[aria-checked="true"] .thumb{left:26px;width:24px;height:24px;background:var(--md-on-primary)}
```

### 7. Dialog

```html
<div class="m3-dialog" role="dialog" aria-modal="true">
  <h2 class="t-title-l">Delete this list?</h2>
  <p class="t-body-m">This will permanently remove the list and its items.</p>
  <div class="actions"><button class="m3-btn textbtn">Cancel</button><button class="m3-btn textbtn">Delete</button></div>
</div>
```
```css
.m3-dialog{background:var(--md-surface-container-high);border-radius:28px;padding:24px;
  max-width:320px;box-shadow:0 6px 10px 4px rgb(0 0 0/.15),0 2px 3px rgb(0 0 0/.3)}
.m3-dialog .actions{display:flex;justify-content:flex-end;gap:8px;margin-top:16px}
```

### 8. Text field (outlined)

```html
<label class="m3-field"><input placeholder=" " required><span>Label</span></label>
```
```css
.m3-field{position:relative;display:block}
.m3-field input{width:100%;height:56px;border:1px solid var(--md-outline);border-radius:4px;
  background:transparent;padding:0 16px;font:400 16px/24px Roboto,system-ui;color:var(--md-on-surface)}
.m3-field span{position:absolute;left:12px;top:16px;padding:0 4px;background:var(--md-surface);
  color:var(--md-on-surface-variant);font:400 16px/24px Roboto,system-ui;transition:all .15s;pointer-events:none}
.m3-field input:focus{border:2px solid var(--md-primary);outline:none}
.m3-field input:focus+span,.m3-field input:not(:placeholder-shown)+span{top:-10px;font-size:12px;color:var(--md-primary)}
```

### 9. Segmented buttons

```html
<div class="m3-segmented" role="group">
  <button class="active">Day</button><button>Week</button><button>Month</button>
</div>
```
```css
.m3-segmented{display:inline-flex;border:1px solid var(--md-outline);border-radius:9999px;overflow:hidden}
.m3-segmented button{border:0;background:transparent;color:var(--md-on-surface);
  font:500 14px/20px Roboto,system-ui;height:40px;padding:0 20px;cursor:pointer;border-left:1px solid var(--md-outline)}
.m3-segmented button:first-child{border-left:0}
.m3-segmented button.active{background:var(--md-secondary-container);color:var(--md-on-secondary-container)}
```

### 10. Progress (linear) & slider

```css
/* Linear progress: 4dp track, pill, primary on surface-container-highest */
.m3-progress{height:4px;border-radius:9999px;background:var(--md-surface-container-highest);overflow:hidden}
.m3-progress>i{display:block;height:100%;width:40%;border-radius:9999px;background:var(--md-primary)}
```

## Motion

Easing tokens (CSS): ✅ official/documented (md.sys.motion.easing.*)
- `--ease-standard: cubic-bezier(0.2, 0, 0, 1)` — default for most UI motion
- `--ease-standard-decelerate: cubic-bezier(0, 0, 0, 1)` — entering
- `--ease-standard-accelerate: cubic-bezier(0.3, 0, 1, 1)` — exiting
- `--ease-emphasized: cubic-bezier(0.05, 0.7, 0.1, 1)` — emphasized decelerate,
  the signature M3 Expressive curve; accelerate variant: `cubic-bezier(0.3, 0, 0.8, 0.15)`

Duration tokens: short 50/100/150/200ms · medium 250/300/350/400ms · long
450/500/550/600ms · extra-long up to 1000ms. ✅ official/documented

Guidance: enters use emphasized-decelerate at ~400–500ms (FAB morphing into a
sheet is the canonical example); exits use emphasized-accelerate at ~200ms;
state changes (switch, ripple) use standard at 100–200ms. Container transform
(dialog/card → full screen) is the signature M3 transition. M3 Expressive
(2025) replaces some duration+easing pairs with spring physics for bouncy,
personality-rich motion. 🟡 cross-referenced for spring specifics.

## Do / Don't

- ✅ Do pair every colored surface with its `on*` role for text (`onPrimary` on
  `primary`, never `onSurface`).
  ❌ Don't put body text in `onSurfaceVariant` gray on a `primaryContainer` — use `onPrimaryContainer`.
- ✅ Do express elevation with the tonal `surfaceContainer*` ladder
  (lowest → highest) in light mode.
  ❌ Don't stack heavy drop shadows — M3 elevation is mostly tone.
- ✅ Do use pill shapes (full radius) for buttons, chips-with-icons, and the
  nav-bar active indicator.
  ❌ Don't give buttons 4dp or 8dp corners — that's M2.
- ✅ Do keep one font family; hierarchy via the 15-style scale.
  ❌ Don't bold display headlines — Display stays Regular 400.
- ✅ Do let users re-seed the theme (Material You) and persist light/dark.
  ❌ Don't hardcode the baseline purple as "the M3 look" — it's just the example seed.
- ✅ Do use state layers (8% hover / 12% pressed overlays) for feedback.
  ❌ Don't invent custom ripple colors — the layer is always the `on*` color of the surface.

## Copy voice

Material 3 is a system, not a brand — it has no marketing voice. In-product
microcopy in Google's M3 apps is plain, friendly, and action-led: "Delete this
list?", "Turn on notifications", "Try again".
