---
name: chakra-ui
description: Chakra UI component-library style — soft rounded cards, teal/blue accents, subtle alerts and badge pills. Use for friendly SaaS dashboards and admin pages.
---

# Chakra UI

Chakra UI is a React component library built on Panda CSS tokens. Its look is
friendly, neutral, and quietly rounded: gray surfaces, solid teal/blue primary
buttons, subtle status alerts, pill badges, and spacing on a strict 4px scale.

## Principles

- **Style props, not CSS files.** Every element gets spacing, color, and radius
  directly as props (`px="4"`, `colorPalette="teal"`), so layouts are built from
  tokens rather than ad-hoc values.
- **Semantic tokens first.** Use `bg`, `fg`, `border`, and `colorPalette.subtle`
  / `solid` so a design adapts to light/dark color mode automatically instead of
  hardcoding hex values.
- **Composable anatomy.** Complex components (Alert, Modal, Tabs) are built from
  small named parts (`Alert.Root`, `Alert.Indicator`, `Alert.Title`), each
  restyleable on its own.
- **Accessibility is a default, not a feature.** Focus rings, ARIA wiring,
  keyboard navigation for dialogs/tabs/menus, and color modes ship with the
  components rather than being bolted on later.
- **Constraints make it coherent.** 4px space scale, 11-step color palettes,
  named radius and shadow tokens — everything in the UI comes from the same
  small token set, which is why Chakra UIs look consistent.

## Color

Legend: ✅ official/documented · 🟡 cross-referenced · ⚠️ community approximation

Chakra v3 palettes are 11 steps (50–950). Key values, light mode:

### Gray ✅

| Token | Hex | Role |
|---|---|---|
| `gray.50` | `#fafafa` | page background (subtle) |
| `gray.100` | `#f4f4f5` | muted surfaces |
| `gray.200` | `#e4e4e7` | borders (`border`) |
| `gray.300` | `#d4d4d8` | emphasized borders |
| `gray.400` | `#a1a1aa` | subtle text |
| `gray.500` | `#71717a` | muted icons |
| `gray.600` | `#52525b` | secondary text |
| `gray.900` | `#18181b` | solid dark elements |
| `gray.950` | `#09090b` | dark-mode page bg |

### Accent palettes ✅

Primary actions default to **teal** (historically) or **blue** in most real apps.

| Token | Hex | Role |
|---|---|---|
| `teal.500` | `#14b8a6` | focus ring, accents |
| `teal.600` | `#0d9488` | solid button bg (`teal.solid`) |
| `teal.700` | `#0c5d56` | alert text (`teal.fg`) |
| `teal.100` | `#ccfbf1` | subtle alert/bg tint (`teal.subtle`) |
| `blue.500` | `#3b82f6` | links, focus ring alt |
| `blue.600` | `#2563eb` | solid button bg alt |
| `blue.100` | `#dbeafe` | info alert bg |
| `red.600` | `#dc2626` | error solid, danger buttons |
| `red.100` | `#fee2e2` | error alert bg |
| `green.600` | `#16a34a` | success solid |
| `green.100` | `#dcfce7` | success alert bg |
| `orange.600` | `#ea580c` | warning solid |
| `orange.100` | `#ffedd5` | warning alert bg |
| `yellow.300` | `#fde047` | warning solid (dark text `#422006` on it) |

### Semantic tokens ✅

- `bg` = white (light) / `#09090b` (dark); `bg.subtle` = `gray.50` / `gray.950`;
  `bg.muted` = `gray.100` / `gray.900`; `bg.panel` = white / `gray.950`
- `fg` = `#18181b` (light) / `gray.50` (dark); `fg.muted` = `gray.600` / `gray.400`
- `border` = `gray.200` (light) / `gray.800` (dark)
- Per palette: `contrast` (text on solid), `fg` (dark text on subtle), `subtle`
  (tinted bg), `muted` (deeper tint), `solid` (button bg), `focusRing`

## Typography

Chakra v3 default fonts ✅ — Inter first, system fallback, same for body and
heading. No display serif anywhere; the system is deliberately plain.

```css
font-family: Inter, -apple-system, BlinkMacSystemFont, "Segoe UI",
  Helvetica, Arial, sans-serif, "Apple Color Emoji", "Segoe UI Emoji",
  "Segoe UI Symbol";
font-family-mono: SFMono-Regular, Menlo, Monaco, Consolas,
  "Liberation Mono", "Courier New", monospace;
```

Scale ✅ (rem, base 16px): `xs .75 · sm .875 · md 1 · lg 1.125 · xl 1.25 ·
2xl 1.5 · 3xl 1.875 · 4xl 2.25 · 5xl 3 · 6xl 3.75 · 7xl 4.5 · 8xl 6 · 9xl 8`

Weights ✅: `thin 100 · extralight 200 · light 300 · normal 400 · medium 500 ·
semibold 600 · bold 700 · extrabold 800 · black 900`. Headings are usually
`semibold`/`bold`; body is `normal`, secondary text often `medium`.

Letter-spacing ✅: `tighter -0.05em · tight -0.025em · wide 0.025em ·
wider 0.05em · widest 0.1em`. Labels and badges often `wide` uppercase.

## Layout & spacing

- **Space scale** ✅: 4px base — `0.5`=2px, `1`=4px, `2`=8px, `3`=12px,
  `4`=16px, `6`=24px, `8`=32px, `12`=48px, `16`=64px, `24`=96px.
  Everything (padding, gaps, margins) snaps to these.
- **Breakpoints** ✅: `sm 30em (480px) · md 48em (768px) · lg 62em (992px) ·
  xl 80em (1280px) · 2xl 96em (1536px)`. Content max-widths around `6xl`/`7xl`
  (72/80rem).
- **Radii** ✅: `2xs 1px · xs 2px · sm 4px · md 6px · lg 8px · xl 12px ·
  2xl 16px · 3xl 24px · full 9999px`. Cards typically `lg`/`xl`, buttons `md`,
  badges and avatars `full`.
- **Shadows** 🟡: `xs` 0 1px 2px rgb(0 0 0/.05); `sm` 0 1px 3px + 0 1px 2px-1px
  rgb(0 0 0/.1); `md` 0 4px 6px-1px + 0 2px 4px-2px rgb(0 0 0/.1); `lg`
  0 10px 15px-3px + 0 4px 6px-4px rgb(0 0 0/.1); `xl` 0 20px 25px-5px +
  0 8px 10px-6px rgb(0 0 0/.1); `2xl` 0 25px 50px-12px rgb(0 0 0/.25).
  Cards use `xs`/`sm`; dialogs and popovers use `lg`/`xl`.
- **Borders**: 1px `border` token on cards and inputs, rarely heavier. Depth
  comes from soft shadows, not thick rules.
- **Color mode**: `useColorMode` toggle; dark mode = near-black `#09090b` page,
  `gray.950` panels, text `gray.50`. Borders relax to `gray.800`.

## Components

Plain HTML/CSS approximations of the real Chakra parts, using the tokens
above. Copy, paste, and adapt.

### Button

Variants ✅: `solid · subtle · surface · outline · ghost · plain`.
Sizes: `2xs–2xl`, default `md` (h-10, px-4). Solid = palette.600 bg, white text;
subtle = palette.100 bg, palette.700 text; hover darkens ~10%.

```html
<button class="ck-btn ck-btn--solid-teal">Save changes</button>
<button class="ck-btn ck-btn--outline">Cancel</button>
<button class="ck-btn ck-btn--ghost">Skip</button>
<style>
  .ck-btn { display:inline-flex; align-items:center; justify-content:center;
    gap:.5rem; height:2.5rem; padding:0 1rem; font-size:.875rem; font-weight:600;
    border-radius:6px; border:1px solid transparent; cursor:pointer;
    transition:background .2s, box-shadow .2s; }
  .ck-btn:focus-visible { outline:none; box-shadow:0 0 0 3px #5eead4; }
  .ck-btn--solid-teal { background:#0d9488; color:#fff; }
  .ck-btn--solid-teal:hover { background:#0c5d56; }
  .ck-btn--outline { background:#fff; border-color:#e4e4e7; color:#18181b; }
  .ck-btn--outline:hover { background:#f4f4f5; }
  .ck-btn--ghost { background:transparent; color:#0c5d56; }
  .ck-btn--ghost:hover { background:#ccfbf1; }
</style>
```

### Card

`lg` radius (8–12px), 1px border, `sm` shadow, white panel. Header/title/body
anatomy: `Card.Root > Card.Header / Card.Body / Card.Footer`.

```html
<article class="ck-card">
  <div class="ck-card-head"><h3>Team activity</h3><span class="ck-badge ck-badge--green">Live</span></div>
  <p class="ck-muted">What your team shipped in the last 24 hours.</p>
</article>
<style>
  .ck-card { background:#fff; border:1px solid #e4e4e7; border-radius:12px;
    box-shadow:0 1px 3px rgb(0 0 0/.1), 0 1px 2px -1px rgb(0 0 0/.1);
    padding:1.25rem; }
  .ck-card-head { display:flex; align-items:center; justify-content:space-between; margin-bottom:.5rem; }
  .ck-card h3 { font-size:1.125rem; font-weight:600; }
  .ck-muted { color:#52525b; font-size:.875rem; }
</style>
```

### Dialog (Modal)

In v3 the component is named **Dialog** (v2 called it Modal) ✅. Anatomy:
`DialogBackdrop` (blackAlpha.600 ≈ rgba(0,0,0,.48), fade) >
`DialogContent` (rounded `lg`, `lg` shadow, max-w `md`/`lg`, scale-in).

```html
<div class="ck-backdrop" id="demoDialog" hidden>
  <div class="ck-dialog" role="dialog" aria-modal="true" aria-labelledby="dlgTitle">
    <header><h2 id="dlgTitle">Upgrade to Pro</h2>
      <button class="ck-iconbtn" aria-label="Close" onclick="document.getElementById('demoDialog').hidden=true">✕</button></header>
    <p class="ck-muted">Unlock unlimited projects and priority support for your whole team.</p>
    <footer>
      <button class="ck-btn ck-btn--ghost" onclick="document.getElementById('demoDialog').hidden=true">Not now</button>
      <button class="ck-btn ck-btn--solid-teal">Upgrade</button>
    </footer>
  </div>
</div>
<style>
  .ck-backdrop { position:fixed; inset:0; background:rgba(0,0,0,.48);
    display:flex; align-items:center; justify-content:center; padding:1rem; z-index:50; }
  .ck-backdrop[hidden] { display:none; }
  .ck-dialog { background:#fff; border-radius:8px; padding:1.5rem; width:100%; max-width:28rem;
    box-shadow:0 10px 15px -3px rgb(0 0 0/.1), 0 4px 6px -4px rgb(0 0 0/.1); }
  .ck-dialog header { display:flex; justify-content:space-between; align-items:center; margin-bottom:.75rem; }
  .ck-dialog h2 { font-size:1.25rem; font-weight:600; }
  .ck-dialog footer { display:flex; justify-content:flex-end; gap:.5rem; margin-top:1.5rem; }
  .ck-iconbtn { border:0; background:transparent; font-size:1rem; cursor:pointer; color:#71717a; border-radius:6px; padding:.25rem .5rem; }
  .ck-iconbtn:hover { background:#f4f4f5; }
</style>
```

### Table

Simple variant: thin `gray.200` row dividers, `sm` header text, numeric columns
right-aligned. No zebra striping by default.

```html
<table class="ck-table">
  <thead><tr><th>Customer</th><th>Status</th><th class="num">Amount</th></tr></thead>
  <tbody>
    <tr><td>Acme Corp</td><td><span class="ck-badge ck-badge--green">Paid</span></td><td class="num">$1,200</td></tr>
    <tr><td>Globex</td><td><span class="ck-badge ck-badge--orange">Pending</span></td><td class="num">$340</td></tr>
  </tbody>
</table>
<style>
  .ck-table { width:100%; border-collapse:collapse; font-size:.875rem; }
  .ck-table th { text-align:left; font-size:.75rem; font-weight:600; color:#71717a;
    text-transform:uppercase; letter-spacing:.05em; padding:.5rem .75rem; border-bottom:1px solid #e4e4e7; }
  .ck-table td { padding:.75rem; border-bottom:1px solid #e4e4e7; }
  .ck-table .num { text-align:right; font-variant-numeric:tabular-nums; }
</style>
```

### Tabs

Variants ✅: `subtle · outline · plain` (plus `line` styling on the underline).
Underline style is the classic: `teal.600` indicator under the active tab.

```html
<div class="ck-tabs">
  <div role="tablist" aria-label="Reports">
    <button role="tab" aria-selected="true" class="ck-tab is-active">Overview</button>
    <button role="tab" aria-selected="false" class="ck-tab">Usage</button>
    <button role="tab" aria-selected="false" class="ck-tab">Team</button>
  </div>
</div>
<style>
  .ck-tabs [role=tablist] { display:flex; gap:.25rem; border-bottom:1px solid #e4e4e7; }
  .ck-tab { background:none; border:0; cursor:pointer; padding:.5rem 1rem;
    font-size:.875rem; font-weight:600; color:#52525b; border-bottom:2px solid transparent; margin-bottom:-1px; }
  .ck-tab:hover { color:#18181b; }
  .ck-tab.is-active { color:#0c5d56; border-bottom-color:#0d9488; }
</style>
```

### Badge

Sizes `xs–lg`; variants `subtle · solid · surface · outline` ✅. Subtle is the
signature look: tinted bg + dark text, `full` or `sm` radius, uppercase.

```html
<span class="ck-badge ck-badge--green">Paid</span>
<span class="ck-badge ck-badge--blue">New</span>
<span class="ck-badge ck-badge--red">Overdue</span>
<span class="ck-badge ck-badge--gray">Draft</span>
<style>
  .ck-badge { display:inline-flex; align-items:center; padding:.125rem .625rem;
    border-radius:9999px; font-size:.75rem; font-weight:600; letter-spacing:.025em;
    text-transform:uppercase; }
  .ck-badge--green { background:#dcfce7; color:#116932; }
  .ck-badge--blue { background:#dbeafe; color:#173da6; }
  .ck-badge--red { background:#fee2e2; color:#991919; }
  .ck-badge--orange { background:#ffedd5; color:#92310a; }
  .ck-badge--gray { background:#f4f4f5; color:#52525b; }
</style>
```

### Alert

Statuses ✅: `info · warning · success · error · neutral`. Variants ✅:
`subtle · surface · outline · solid`. Subtle is the default look: tinted
background, dark text, status icon in a circle at the left, optional close.

```html
<div class="ck-alert ck-alert--success" role="alert">
  <span class="ck-alert-icon" aria-hidden="true">✓</span>
  <div><strong>Payment received.</strong> Your invoice #1042 was paid — thanks!</div>
</div>
<style>
  .ck-alert { display:flex; gap:.75rem; align-items:flex-start; padding:.875rem 1rem;
    border-radius:8px; font-size:.875rem; }
  .ck-alert strong { font-weight:600; }
  .ck-alert-icon { display:inline-flex; align-items:center; justify-content:center;
    width:1.25rem; height:1.25rem; border-radius:9999px; font-size:.75rem; font-weight:700; flex:none; }
  .ck-alert--success { background:#f0fdf4; color:#116932; }
  .ck-alert--success .ck-alert-icon { background:#16a34a; color:#fff; }
  .ck-alert--info { background:#eff6ff; color:#173da6; }
  .ck-alert--info .ck-alert-icon { background:#2563eb; color:#fff; }
  .ck-alert--warning { background:#fff7ed; color:#92310a; }
  .ck-alert--warning .ck-alert-icon { background:#ea580c; color:#fff; }
  .ck-alert--error { background:#fef2f2; color:#991919; }
  .ck-alert--error .ck-alert-icon { background:#dc2626; color:#fff; }
</style>
```

### Form controls

`FormControl > FormLabel + Input + FormHelperText / FormErrorMessage`.
Inputs: h-10, `md` radius, 1px `gray.200`→`gray.300` border, teal focus ring
(`box-shadow: 0 0 0 1px teal.500 + 0 0 0 3px teal.100`-ish), error = `red.500`
border + message in `red.500`.

```html
<div class="ck-field">
  <label for="fEmail">Work email</label>
  <input id="fEmail" type="email" placeholder="you@company.com" aria-describedby="fEmailHelp">
  <p id="fEmailHelp" class="ck-help">We will never share your email.</p>
</div>
<div class="ck-field is-invalid">
  <label for="fName">Team name</label>
  <input id="fName" aria-invalid="true" aria-describedby="fNameErr" value="">
  <p id="fNameErr" class="ck-error">Team name is required.</p>
</div>
<style>
  .ck-field { display:flex; flex-direction:column; gap:.375rem; margin-bottom:1rem; }
  .ck-field label { font-size:.875rem; font-weight:500; }
  .ck-field input { height:2.5rem; padding:0 .75rem; font-size:1rem;
    border:1px solid #d4d4d8; border-radius:6px; background:#fff; }
  .ck-field input:focus { outline:none; border-color:#14b8a6;
    box-shadow:0 0 0 3px rgba(20,184,166,.25); }
  .ck-field input::placeholder { color:#a1a1aa; }
  .ck-help { font-size:.75rem; color:#71717a; }
  .ck-field.is-invalid input { border-color:#ef4444; }
  .ck-field.is-invalid input:focus { box-shadow:0 0 0 3px rgba(239,68,68,.2); }
  .ck-error { font-size:.875rem; color:#dc2626; }
</style>
```

### Stat

Anatomy ✅: `Stat > StatLabel · StatNumber · StatHelpText · StatArrow`.
Label = small muted uppercase-ish; number = `2xl`–`3xl` semibold; help text
carries an up/down arrow in green/red.

```html
<dl class="ck-stat">
  <dt>Monthly revenue</dt>
  <dd class="ck-stat-num">$48,290</dd>
  <dd class="ck-stat-help"><span class="up">▲ 12.4%</span> vs last month</dd>
</dl>
<style>
  .ck-stat dt { font-size:.875rem; font-weight:500; color:#52525b; }
  .ck-stat-num { font-size:1.875rem; font-weight:600; letter-spacing:-.025em; margin:.25rem 0; }
  .ck-stat-help { font-size:.875rem; color:#71717a; }
  .ck-stat-help .up { color:#16a34a; font-weight:600; }
  .ck-stat-help .down { color:#dc2626; font-weight:600; }
</style>
```

## Motion

Chakra does not define a signature motion language; transitions are simple
state changes. Durations 🟡: `faster .1s · fast .15s · normal .2s · slow .3s ·
slower .4s`. Easing is the platform default (`ease-out`-style). Dialogs scale
from ~0.95 and fade the backdrop; drawers/slide-overs translate on the X axis.

## Do / Don't

- **Do** put all spacing on the 4px scale (`p="6"`, `gap="4"`); **don't** invent
  7px paddings or 13px margins — off-scale values are the fastest way to break
  the Chakra look.
- **Do** use `subtle` variants for badges and alerts (tinted bg + dark text);
  **don't** use `solid` red/green pills for status — solid is reserved for
  primary buttons and strong calls to action.
- **Do** keep radius modest: buttons `md` (6px), cards `lg`–`xl` (8–12px),
  badges `full`; **don't** round everything into giant pills — Chakra is soft,
  not bubbly.
- **Do** give the primary action `teal` or `blue` and leave everything else
  `gray`/`outline`/`ghost`; **don't** color every button a different hue.
- **Do** support both color modes with semantic tokens (`bg`, `fg`, `border`);
  **don't** hardcode `#fff` page backgrounds if the design must work in dark mode.
- **Do** name things after anatomy (`Card.Header`, `Alert.Title`) when composing;
  **don't** flatten compound components into single divs with magic classes —
  you lose the composability the system is built for.

## Copy voice

Plain, friendly, and direct — short sentences, no marketing fluff. Example
strings: "Your invoice #1042 was paid — thanks!", "We couldn't save your
changes. Try again.", "Invite your team to get started."
