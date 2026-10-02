---
name: fluent-2
description: Microsoft Fluent 2 design system — calm layered depth, Segoe type, token-driven light/dark/high-contrast themes for productive software.
---

# Fluent 2

Microsoft's Fluent 2 design system — the visual language of Windows 11,
Microsoft 365, Teams, and Azure. Built for dense, productive,
information-heavy software: compact controls, a restrained neutral ramp, a
single 16-shade brand ramp, and depth expressed through a graduated shadow scale
plus Windows materials (Mica on window backgrounds, Acrylic on transient
surfaces). Nothing is styled by taste: every visual value is addressed through
named tokens, so light/dark/high-contrast theme swaps and customer rebrands
are mechanical.

Legend: ✅ official/documented · 🟡 cross-referenced from official token
sources · ⚠️ community approximation.

## Principles

1. **Open** — one coherent design language shared across web, desktop, and
   mobile; the same tokens and components speak every platform.
2. **Accessible** — contrast, keyboard operation, focus indicators, and screen
   reader semantics are part of the spec, not decoration; high-contrast theme
   is a first-class citizen, not an afterthought.
3. **Designed for everyone** — global products assume internationalization,
   RTL layouts, and diverse contexts from day one.
4. **Calm depth** — hierarchy comes from soft, layered shadows and surface
   value (Mica, Acrylic), not from loud color or ornament. Depth is quiet.
5. **Motion as meaning** — animation communicates cause and effect
   (ease-in = leaving, ease-out = entering); nothing moves decoratively.
6. **Productive, not spectacle** — layouts support work: compact controls,
   explicit states (rest, hover, pressed, selected, disabled), predictable
   component behavior across every surface.

## Color

Fluent uses **global tokens** (context-free ramps: `brand10…160`, neutral
ramp) and **alias tokens** (intent-named: `neutralForeground1`,
`neutralBackground2`, `neutralStroke1`, `colorBrandBackgroundHover`). In real
Fluent you address the alias, never the hex. `fluent2.microsoft.design`
publishes prose and images, not hex values — the hexes below are transcribed
from the official `microsoft/fluentui` token sources.

**Brand ramp (blue, default) — 16 shades** 🟡:

| Token | Hex | Token | Hex |
|---|---|---|---|
| `brand10` | `#F5FAFE` | `brand90` | `#115EA3` |
| `brand20` | `#EDF5FD` | `brand100` | `#0F548C` |
| `brand30` | `#DEEDFA` | `brand110` | `#0E4775` |
| `brand40` | `#C7E0F4` | `brand120` | `#0C3B5E` |
| `brand50` | `#ADCBED` | `brand130` | `#0A2E4A` |
| `brand60` | `#8AB4E6` | `brand140` | `#082338` |
| `brand70` | `#4F93C8` | `brand150` | `#071A29` |
| `brand80` | `#0F6CBD` | `brand160` | `#06101D` |

**Key semantic aliases (light theme)** ✅:

| Token | Hex | Role |
|---|---|---|
| `colorBrandBackground` | `#0F6CBD` | primary button rest |
| `colorBrandBackgroundHover` | `#115EA3` | primary button hover |
| `colorBrandBackgroundPressed` | `#0C3B5E` | primary button pressed |
| `colorBrandBackgroundSelected` | `#0F548C` | selected state |
| `colorBrandForeground1` | `#0F6CBD` | brand text / link |
| `colorNeutralForeground1` | `#242424` | primary text |
| `colorNeutralForeground2` | `#424242` | secondary text |
| `colorNeutralForeground3` | `#616161` | tertiary / captions |
| `colorNeutralForegroundDisabled` | `#BDBDBD` | disabled text |
| `colorNeutralBackground1` | `#FFFFFF` | app canvas / card |
| `colorNeutralBackground2` | `#FAFAFA` | grouped surface |
| `colorNeutralBackground3` | `#F5F5F5` | low-emphasis surface |
| `colorNeutralBackground4` | `#F0F0F0` | resting control fill |
| `colorNeutralStroke1` | `#D1D1D1` | control borders |
| `colorNeutralStroke2` | `#E0E0E0` | card hairlines |
| `colorNeutralStrokeAccessible` | `#616161` | strokes that must meet contrast |
| `colorStrokeFocus1` | `#0078D4` | inner focus ring |
| `colorStrokeFocus2` | `#000000` | outer focus ring |

**Status colors** 🟡:

| Token | Hex | Role |
|---|---|---|
| `colorStatusSuccessForeground1` | `#107C10` | success |
| `colorStatusWarningForeground1` | `#BC4B09` | warning |
| `colorStatusDangerForeground1` | `#D13438` | error / destructive |
| `colorStatusDangerBackground1` | `#FDECEA` | error message bar fill |
| `colorStatusSevereForeground1` | `#C50F1F` | severe error |

**Neutral global ramp** 🟡: `#FAFAFA` · `#F5F5F5` · `#F0F0F0` · `#E0E0E0` ·
`#D1D1D1` · `#BDBDBD` · `#A6A6A6` · `#8A8A8A` · `#616161` · `#424242` ·
`#242424`.

**Dark theme** ✅: backgrounds invert to near-black ramps
(`#292929` canvas … `#11100F`), foregrounds to `#FFFFFF`/`#E6E6E6`, brand
ramp shifts lighter (`colorBrandBackground` stays `#0F6CBD`, hover becomes
`#4F93C8`). **High-contrast theme** ✅: 8 Windows system colors, brand color
intentionally removed, hard 1px borders on every control, no shadows.

## Typography

✅ official/documented. Typeface: **Segoe UI Variable** (Windows 11) falling
back to **Segoe UI**, then the platform system font. Fluent System Icons
accompany labels — icons never replace text labels.

Web type ramp (size / line-height / weight):

| Token | Size | Line | Weight | Use for |
|---|---|---|---|---|
| `Caption2` | 10px | 12px | regular | meta microcopy |
| `Caption1` | 12px | 16px | regular | captions, message bars |
| `Body1` | 14px | 20px | regular | default UI text |
| `Body1Strong` | 14px | 20px | semibold | control labels |
| `Body2` | 16px | 22px | regular | long-form content |
| `Subtitle1` | 16px | 22px | semibold | section headers |
| `Subtitle2` | 20px | 28px | semibold | panel titles |
| `Title1` | 24px | 32px | regular | page titles |
| `Title2` | 28px | 36px | semibold | page titles, larger |
| `Title3` | 40px | 52px | semibold | hero / landing |
| `Display` | 68px | 76px | semibold | marketing display |

Rules: functional, readable text over expressive editorial treatment;
semibold is for headers and primary control labels, never for whole
paragraphs; keep tables and forms typographically compact but not cramped.

Closest free substitutes when Segoe is unavailable: `Segoe UI Variable`,
`Segoe UI`, `-apple-system`, `system-ui` — or Inter as a neutral stand-in
(mark ⚠️).

## Layout & spacing

✅ official/documented (values from `microsoft/fluentui` token sources).

- **Base grid**: 4px. Spacing tokens snap to 4/8/12/16/20/24/32px
  (`spacingHorizontalS` 8, `M` 12, `L` 16, `XL` 20, `XXL` 24; vertical adds
  `XXXL` 32).
- **Corner radius**: `borderRadiusNone` 0, `Small` 2px, `Medium` 4px (default
  for buttons, inputs, controls), `Large` 6px, `XLarge` 8px (cards, dialogs),
  `Circular` 50% (avatars, pills).
- **Stroke width**: `strokeWidthThin` 1px (all control borders), `strokeWidthThick`
  2px (focus accents, drag handles).
- **Depth**: the shadow scale below — shadows map to interaction depth, never
  to taste 🟡:

| Token | box-shadow | Used for |
|---|---|---|
| `shadow2` | `0 1px 2px rgba(0,0,0,.14), 0 0 2px rgba(0,0,0,.12)` | card rest, tooltip |
| `shadow4` | `0 2px 4px rgba(0,0,0,.14), 0 0 2px rgba(0,0,0,.12)` | menu, card hover, popover |
| `shadow8` | `0 4px 8px rgba(0,0,0,.14), 0 0 2px rgba(0,0,0,.12)` | teaching callout, panel |
| `shadow16` | `0 8px 16px rgba(0,0,0,.14), 0 0 2px rgba(0,0,0,.12)` | dialog |
| `shadow28` | `0 14px 28px rgba(0,0,0,.24), 0 0 8px rgba(0,0,0,.2)` | large dialog |
| `shadow64` | `0 32px 64px rgba(0,0,0,.24), 0 0 8px rgba(0,0,0,.2)` | full-screen overlay |

- **Materials** ✅: Mica on window backgrounds (opaque, desktop-only
  backdrop), Acrylic on transient surfaces (flyouts, tooltips — semi-opaque
  blur of what is behind). On the web, approximate Acrylic with a light
  backdrop blur and a translucent neutral fill.
- **Layout patterns** ✅: left-side app navigation, command surfaces as
  toolbars/ribbons at the top, breadcrumbs for deep hierarchies, dense
  32px-high controls, 8/12px gutters, content in cards on a canvas.

## Components

All CSS is copy-pasteable. Swap hexes for CSS variables in real projects.

### 1. Buttons (Primary / Secondary / Subtle)

Fluent appearances: `primary | outline | subtle | transparent`. 32px tall,
4px radius, 14px semibold label. Primary darkens through states — never grows
a shadow.

```html
<button class="f-btn f-btn-primary">Save changes</button>
<button class="f-btn">Cancel</button>
<button class="f-btn f-btn-subtle">Show details</button>
```

```css
.f-btn {
  height: 32px; padding: 0 12px; border-radius: 4px;
  font: 600 14px/20px "Segoe UI Variable","Segoe UI",system-ui,sans-serif;
  border: 1px solid #D1D1D1; background: #FFFFFF; color: #242424;
  cursor: pointer; display: inline-flex; align-items: center; gap: 8px;
}
.f-btn:hover { background: #F5F5F5; }
.f-btn:active { background: #E0E0E0; }
.f-btn-primary { background: #0F6CBD; border-color: transparent; color: #FFF; }
.f-btn-primary:hover { background: #115EA3; }
.f-btn-primary:active { background: #0C3B5E; }
.f-btn-subtle { border-color: transparent; background: transparent; }
.f-btn-subtle:hover { background: #F5F5F5; }
.f-btn:focus-visible {
  outline: 2px solid #000; outline-offset: 2px; box-shadow: 0 0 0 3px #0078D4;
}
.f-btn:disabled { background: #F0F0F0; color: #BDBDBD; border-color: transparent; cursor: not-allowed; }
```

### 2. Command bar

The top toolbar of a productive surface: grouped actions, overflow chevron.
Icons + labels; dividers between groups.

```html
<div class="f-commandbar" role="toolbar" aria-label="Document commands">
  <button class="f-btn f-btn-primary">New</button>
  <span class="f-sep"></span>
  <button class="f-btn f-btn-subtle">Share</button>
  <button class="f-btn f-btn-subtle">Export</button>
  <span class="f-sep"></span>
  <button class="f-btn f-btn-subtle" aria-label="More commands">···</button>
</div>
```

```css
.f-commandbar {
  display: flex; align-items: center; gap: 4px; padding: 8px 12px;
  background: #FAFAFA; border-bottom: 1px solid #E0E0E0;
}
.f-sep { width: 1px; height: 24px; background: #E0E0E0; margin: 0 4px; }
```

### 3. Message bar

Inline, calm status — preferred over modal interruption. Tinted background,
icon, text, optional actions and dismiss.

```html
<div class="f-msg f-msg-info" role="status">
  <strong>Your draft was saved.</strong>
  <span>Autosave is on for this workspace.</span>
  <button class="f-btn f-btn-subtle">Undo</button>
  <button class="f-btn f-btn-subtle" aria-label="Dismiss">✕</button>
</div>
```

```css
.f-msg {
  display: flex; align-items: center; gap: 8px; padding: 8px 12px;
  border-radius: 4px; font: 400 12px/16px "Segoe UI Variable","Segoe UI",sans-serif;
  color: #242424; border: 1px solid transparent;
}
.f-msg-info    { background: #EBF3FC; }
.f-msg-success { background: #DFF6DD; }
.f-msg-warning { background: #FFF4CE; }
.f-msg-error   { background: #FDECEA; border-color: #D13438; }
.f-msg strong { font-weight: 600; }
.f-msg .f-btn { height: 24px; padding: 0 8px; font-size: 12px; }
```

### 4. Teaching callout

A focused coach mark: 8px radius, `shadow8`, beak pointing at the target,
dismiss button, one clear action.

```html
<div class="f-teaching" role="dialog" aria-label="New feature">
  <div class="f-teaching-beak"></div>
  <h3 class="f-teaching-title">Try Copilot summaries</h3>
  <p class="f-teaching-body">Get a two-sentence brief of any long thread before you read it.</p>
  <div class="f-teaching-actions">
    <button class="f-btn f-btn-primary">Try it</button>
    <button class="f-btn">Not now</button>
  </div>
</div>
```

```css
.f-teaching {
  position: relative; width: 320px; padding: 20px; border-radius: 8px;
  background: #FFF; box-shadow: 0 4px 8px rgba(0,0,0,.14), 0 0 2px rgba(0,0,0,.12);
  font: 400 14px/20px "Segoe UI Variable","Segoe UI",sans-serif; color: #242424;
}
.f-teaching-title { font: 600 16px/22px "Segoe UI Variable","Segoe UI",sans-serif; margin: 0 0 4px; }
.f-teaching-body { margin: 0 0 16px; color: #424242; }
.f-teaching-actions { display: flex; gap: 8px; }
.f-teaching-beak {
  position: absolute; top: -7px; left: 32px; width: 14px; height: 14px;
  background: #FFF; transform: rotate(45deg); border-left: 1px solid #E0E0E0; border-top: 1px solid #E0E0E0;
}
```

### 5. Persona / avatar

Circular, initials or photo, presence badge ring. Overlap stacks in lists.

```html
<div class="f-persona">
  <span class="f-avatar f-avatar--36" style="background:#4F93C8">AK</span>
  <span class="f-persona-text">
    <span class="f-persona-name">Aiko Tanaka</span>
    <span class="f-persona-sub">Available · Designer</span>
  </span>
</div>
```

```css
.f-persona { display: flex; align-items: center; gap: 12px; }
.f-avatar {
  border-radius: 50%; display: inline-flex; align-items: center; justify-content: center;
  color: #FFF; font: 600 14px/20px "Segoe UI Variable","Segoe UI",sans-serif; flex: none;
}
.f-avatar--36 { width: 36px; height: 36px; }
.f-persona-name { display: block; font: 600 14px/20px "Segoe UI Variable","Segoe UI",sans-serif; color: #242424; }
.f-persona-sub { display: block; font: 400 12px/16px "Segoe UI Variable","Segoe UI",sans-serif; color: #616161; }
```

### 6. Nav (left rail)

App shell pattern: icon + label rows, selected row gets a tinted fill and a
2px brand-colored indicator bar at its left edge.

```html
<nav class="f-nav" aria-label="Primary">
  <button class="f-nav-item is-selected"><span class="f-nav-icon">▦</span> Home</button>
  <button class="f-nav-item"><span class="f-nav-icon">✉</span> Mail</button>
  <button class="f-nav-item"><span class="f-nav-icon">▤</span> Files</button>
</nav>
```

```css
.f-nav { width: 220px; background: #FAFAFA; padding: 8px; display: grid; gap: 2px; }
.f-nav-item {
  position: relative; display: flex; align-items: center; gap: 12px;
  height: 36px; padding: 0 12px; border: 0; border-radius: 4px; background: transparent;
  font: 400 14px/20px "Segoe UI Variable","Segoe UI",sans-serif; color: #242424; cursor: pointer;
  text-align: left; width: 100%;
}
.f-nav-item:hover { background: #F0F0F0; }
.f-nav-item.is-selected { background: #EBF3FC; font-weight: 600; }
.f-nav-item.is-selected::before {
  content: ""; position: absolute; left: 0; top: 10px; bottom: 10px;
  width: 2px; border-radius: 2px; background: #0F6CBD;
}
.f-nav-icon { width: 20px; text-align: center; color: #616161; }
```

### 7. Switch (toggle)

On = brand fill, knob white, 40×20px. Labels sit to the left.

```html
<label class="f-switch">
  <span class="f-switch-text">Autosave <span class="f-switch-sub">Apply changes immediately</span></span>
  <button role="switch" aria-checked="true" class="f-switch-control"></button>
</label>
```

```css
.f-switch { display: flex; align-items: center; justify-content: space-between; gap: 16px; }
.f-switch-text { font: 600 14px/20px "Segoe UI Variable","Segoe UI",sans-serif; color: #242424; }
.f-switch-sub { display: block; font: 400 12px/16px "Segoe UI Variable","Segoe UI",sans-serif; color: #616161; font-weight: 400; }
.f-switch-control {
  position: relative; width: 40px; height: 20px; border-radius: 20px;
  background: #E0E0E0; border: 1px solid #BDBDBD; cursor: pointer; padding: 0;
}
.f-switch-control::after {
  content: ""; position: absolute; top: 2px; left: 2px; width: 14px; height: 14px;
  border-radius: 50%; background: #616161; transition: transform .1s, background .1s;
}
.f-switch-control[aria-checked="true"] { background: #0F6CBD; border-color: #0F6CBD; }
.f-switch-control[aria-checked="true"]::after { transform: translateX(20px); background: #FFF; }
```

### 8. Checkbox / radio

Compact 20px boxes, brand check, 4px radius.

```css
.f-check { display: inline-flex; align-items: center; gap: 8px;
  font: 400 14px/20px "Segoe UI Variable","Segoe UI",sans-serif; color: #242424; }
.f-check input { width: 20px; height: 20px; accent-color: #0F6CBD; margin: 0; }
```

### 9. Text field

1px `neutralStroke1` border, 4px radius, focus = brand border + double focus
ring (`#0078D4` inner, `#000` outer per `strokeFocus1/2`). Label above, helper
text below, error text in danger red.

```css
.f-field { display: grid; gap: 4px; max-width: 400px; }
.f-field label { font: 600 14px/20px "Segoe UI Variable","Segoe UI",sans-serif; color: #242424; }
.f-field input {
  height: 32px; padding: 0 12px; border-radius: 4px; border: 1px solid #D1D1D1;
  font: 400 14px/20px "Segoe UI Variable","Segoe UI",sans-serif; color: #242424; background: #FFF;
}
.f-field input:focus { outline: none; border-color: #0078D4; box-shadow: 0 0 0 1px #0078D4; }
.f-field .f-hint { font: 400 12px/16px "Segoe UI Variable","Segoe UI",sans-serif; color: #616161; }
.f-field .f-error { font: 400 12px/16px "Segoe UI Variable","Segoe UI",sans-serif; color: #D13438; }
```

### 10. Card + compound button (tile)

`shadow2`, hairline border, 8px radius. Compound buttons are big clickable
tiles with title + description.

```css
.f-card {
  background: #FFF; border: 1px solid #E0E0E0; border-radius: 8px;
  box-shadow: 0 1px 2px rgba(0,0,0,.14), 0 0 2px rgba(0,0,0,.12);
  padding: 16px;
}
.f-compound {
  display: grid; gap: 4px; text-align: left; cursor: pointer;
  background: #FFF; border: 1px solid #E0E0E0; border-radius: 8px;
  box-shadow: 0 1px 2px rgba(0,0,0,.14), 0 0 2px rgba(0,0,0,.12);
  padding: 16px;
}
.f-compound:hover { box-shadow: 0 2px 4px rgba(0,0,0,.14), 0 0 2px rgba(0,0,0,.12); }
.f-compound strong { font: 600 14px/20px "Segoe UI Variable","Segoe UI",sans-serif; color: #242424; }
.f-compound span { font: 400 12px/16px "Segoe UI Variable","Segoe UI",sans-serif; color: #616161; }
```

## Motion

✅ official/documented. Motion communicates — never decorates. Two
families: **ease-in** (`accelerate*`) for elements leaving/dismissing,
**ease-out** (`decelerate*`) for elements entering; `easyEase*` for
in-place state changes.

**Durations:** `durationUltraFast` 50ms · `durationFaster` 100ms ·
`durationFast` 150ms · `durationNormal` 200ms · `durationGentle` 250ms ·
`durationSlow` 300ms · `durationSlower` 400ms · `durationUltraSlow` 500ms.

**Curves:** `accelerateMax` cubic-bezier(1, 0, 1, 1) ·
`accelerateMid` cubic-bezier(.7, 0, 1, .5) ·
`decelerateMax` cubic-bezier(0, 0, 0, 1) ·
`decelerateMid` cubic-bezier(.1, .9, .2, 1) ·
`easyEaseMax` cubic-bezier(0, 0, 0, 1) ·
`easyEaseMid` cubic-bezier(.8, 0, .2, 1) ·
`easyEaseSlow` cubic-bezier(.8, 0, 0, 1) ·
`linear` cubic-bezier(0, 0, 1, 1).

CSS:

```css
/* dialog enters */
.f-dialog { transition: opacity 200ms cubic-bezier(.1,.9,.2,1), transform 200ms cubic-bezier(.1,.9,.2,1); }
/* dismissing */
.f-dialog.is-leaving { transition: opacity 150ms cubic-bezier(.7,0,1,.5); }
/* reduced motion always wins */
@media (prefers-reduced-motion: reduce) { * { transition: none !important; animation: none !important; } }
```

## Do / Don't

- **Do** address semantic alias tokens (`neutralForeground1`, `brandBackgroundHover`).
  **Don't** hardcode `#0F6CBD` as "the blue" in product code — the ramp exists so themes and rebrands change one value.
- **Do** show explicit states: rest, hover, pressed, selected, disabled, focus ring.
  **Don't** rely on hover alone to reveal meaning — keyboard users must see it too.
- **Do** use `shadow2` for resting cards and step up the scale for menus/dialogs.
  **Don't** add shadows for visual interest; if it doesn't float, it doesn't cast.
- **Do** keep controls 32px tall with 4px radii in dense layouts.
  **Don't** round everything to 12px pills "to look modern" — that's a different system.
- **Do** use the message bar for calm, inline status.
  **Don't** throw a modal dialog for something an inline message could carry.
- **Do** write the teaching callout with one clear next action.
  **Don't** stack two calls out on the same screen — one coach mark at a time.
- **Do** test in high contrast: borders replace shadows, brand color disappears.
  **Don't** assume the light-theme ramp survives — design the layout to work in black and white.
- **Do** pair icons with visible text labels.
  **Don't** turn ordinary commands into icon-only buttons without a tooltip and label.

## Copy voice

Direct, task-oriented, plain-spoken: "Your draft was saved." · "Share this
with your team?" · "Something didn't work. Try again."
