---
name: one-ui
description: Samsung One UI design language — viewing/interaction split for one-handed use, giant collapsing titles, dark-first surfaces, Samsung Blue accent, and big rounded controls. Use for Samsung-style settings pages, Galaxy phone UI, and thumb-reachable mobile apps.
---

# One UI

Samsung's design system for Galaxy phones, tablets, watches and foldables
(developer.samsung.com/one-ui). Built for tall screens: the top of the screen
is for **viewing**, the bottom is for **touching**. Calm, rounded, dark-first,
with a single blue accent.

## Principles

1. **Focus on the task at hand.** Simple, intuitive designs that keep users on
   content and make the settings they need easy to find. ✅ official/documented
2. **Interact naturally — viewing area up, interaction area down.** The screen
   is split: a viewing area at the top and an interaction area below, so
   buttons stay within thumb reach even on tall devices. ✅ official/documented
3. **Be visibly comfortable.** Dark mode to reduce eye fatigue and glare, high
   contrast keyboard, variable font sizes and styles for accessibility.
   ✅ official/documented
4. **Make things responsive.** Layout adapts across phones, tablets, foldables
   and DeX; content and functions are added or removed to fit each form factor.
   ✅ official/documented
5. **Look, then act.** The viewing area holds only content users look at —
   titles, status, counts — no touch targets. Actionable components group at
   the bottom. Popups and dialogs anchor to the **bottom** of the screen, never
   the middle. ✅ official/documented (viewing-area rule); 🟡 cross-referenced
   (bottom popups, documented in One UI 2.0 notes)

## Color

One UI assigns **roles**, not raw hexes (Primary, Primary dark, Color control
activated, White, Black). ✅ official/documented (One UI design guide)

Light theme: ✅ official/documented
- `--oui-primary: #0381fe` — THE accent: switches, checkboxes, radio buttons,
  focused inputs, floating buttons, selected states
- `--oui-primary-dark: #0072de` — app-bar text, text buttons, dialog buttons
- `--oui-control-active: #3e91ff` — color of activated controls
- `--oui-white: #fafafa` — base surface
- `--oui-black: #000000` — darkest text

Dark theme: ✅ official/documented
- `--oui-primary: #0381fe` — same blue, unchanged
- `--oui-primary-dark: #3e91ff` — text buttons and dialog buttons lighten
- `--oui-control-active: #3e91ff`
- `--oui-black: #080808` — app background (near-black, not pure #000)

Meaning colors: RED = warning/danger/prohibition · GREEN = safety/peace ·
BLUE = efficiency/intelligence/tranquility. ✅ official/documented

Brand note: Samsung Blue (brand) is Pantone 286 C. 🟡 cross-referenced
(brand-guideline summaries; approximate sRGB #0039A6)

Dark-mode surfaces (sampled from One UI Settings screenshots):
⚠️ community approximation — official docs only define the roles above
- `--oui-surface-raised: #1e1e1e` — cards and grouped list containers on dark
- `--oui-text-primary: #ffffff`, `--oui-text-secondary: #9a9a9a`
- Light theme keeps surfaces at #fafafa/#ffffff with text #000000 / secondary #6b6b6b

## Typography

- **One UI Sans** — the default system typeface since One UI 6.0 (Android 14),
  a variable grotesque sans (system name `One UI Sans APP VF` on Galaxy
  devices). Fallback stack: `"One UI Sans APP VF", "One UI Sans", Roboto,
  system-ui, sans-serif`. 🟡 cross-referenced (multiple device/font reports)
- Older One UI ships Roboto as the default font. ✅ official/documented (design
  guide lists Roboto as the default family)
- **Title Case rule:** capitalize the first letter of every word in component
  titles, tabs and text-only buttons ("App Bar", "Dialog Button", "Main Tab"),
  everything else lowercase. ✅ official/documented
- The signature type moment is the **giant screen title** in the viewing area:
  very large (roughly 30–34sp), bold, center-aligned, shrinking into a small
  toolbar title on scroll. 🟡 cross-referenced (design guide + shipping apps;
  exact sizes are platform defaults, not documented constants)
- Viewing-area text is **center-aligned** for visual stability; the
  interaction area below stays left-aligned. ✅ official/documented

## Layout & spacing

- **Viewing area (top ~1/3+):** wide margins, open space, center-aligned title
  and glanceable info. No touch targets here. When an image sits here, separate
  it from the interaction area with a **straight cut**, never a curve.
  ✅ official/documented
- **Interaction area (bottom):** actionable components grouped in logical
  order with clear margins between groups. ✅ official/documented
- 8dp baseline grid; generous touch targets (≥48dp). 🟡 cross-referenced
  (Android convention adopted by One UI)
- **Corner radii:** cards and dialogs use very large radii (observed ~26–28px
  on cards, ~28px+ on dialogs); quick toggles and switch tracks are fully
  round. ⚠️ approximation from screenshots — official docs are thin here
- Elevation is quiet: dark mode leans on tonal steps (#080808 → #1e1e1e),
  light mode on soft shadows. ⚠️ approximation
- Settings rows are full-bleed icon + label + trailing control (switch/chevron),
  separated by hairline dividers. 🟡 cross-referenced

## Components

Copy-pasteable HTML/CSS. Assumes the CSS variables from **Color** and the font
stack from **Typography**. Dark-first: the tokens below assume the dark theme.

### 1. Big collapsible header (viewing area → toolbar)

```html
<header class="oui-headerview">
  <h1 class="oui-bigtitle">Settings</h1>
  <p class="oui-viewinfo">Galaxy Nova · One UI 8</p>
</header>
<div class="oui-toolbar"><span>Settings</span></div>
```
```css
.oui-headerview{text-align:center;padding:56px 24px 24px;background:var(--oui-black);color:#fff}
.oui-bigtitle{font-size:34px;font-weight:700;letter-spacing:-.3px;margin:0 0 6px}
.oui-viewinfo{font-size:14px;color:#9a9a9a;margin:0}
/* on scroll: collapse .oui-bigtitle (fade/scale), reveal .oui-toolbar */
.oui-toolbar{position:sticky;top:0;display:none;background:var(--oui-black);
  color:#fff;font-size:17px;font-weight:600;text-align:center;padding:14px}
body.scrolled .oui-toolbar{display:block}
body.scrolled .oui-bigtitle{opacity:0;transform:scale(.6)}
.oui-bigtitle{transition:opacity .25s,transform .25s}
```
Big title lives in the viewing area and shrinks into the toolbar as content
scrolls up — the single most recognizable One UI behavior.

### 2. Settings list row (interaction area)

```html
<div class="oui-row">
  <span class="oui-rowicon">◉</span>
  <div class="oui-rowtxt"><b>Dark Mode</b><span>Reduce eye strain at night</span></div>
  <button class="oui-switch" role="switch" aria-checked="true"><span></span></button>
</div>
```
```css
.oui-row{display:flex;align-items:center;gap:14px;padding:16px 20px;background:#080808;color:#fff;cursor:pointer}
.oui-row+.oui-row{border-top:1px solid #232323}
.oui-rowicon{width:40px;height:40px;border-radius:50%;background:#1e1e1e;display:grid;place-items:center;flex:none}
.oui-rowtxt{flex:1}.oui-rowtxt b{display:block;font-size:16px;font-weight:400}
.oui-rowtxt span{font-size:13px;color:#9a9a9a}
```

### 3. Switch — big, round, blue when on

```html
<button class="oui-switch" role="switch" aria-checked="true" aria-label="Dark mode"><span></span></button>
```
```css
.oui-switch{width:56px;height:32px;border-radius:9999px;border:0;background:#3a3a3a;
  position:relative;cursor:pointer;flex:none;transition:background .2s}
.oui-switch span{position:absolute;top:3px;left:3px;width:26px;height:26px;border-radius:50%;
  background:#fff;transition:left .2s}
.oui-switch[aria-checked="true"]{background:var(--oui-primary)}
.oui-switch[aria-checked="true"] span{left:27px}
```

### 4. Card — 26px+ radius, tonal lift

```html
<div class="oui-card"><h3>Storage</h3><p>78 GB of 128 GB used</p></div>
```
```css
.oui-card{background:#1e1e1e;border-radius:28px;padding:22px;color:#fff}
.oui-card h3{font-size:17px;font-weight:600;margin:0 0 6px}
.oui-card p{font-size:14px;color:#9a9a9a;margin:0}
```

### 5. Bottom navigation

```html
<nav class="oui-bottomnav">
  <a class="active" href="#"><i>⌂</i>Home</a>
  <a href="#"><i>▦</i>Devices</a>
  <a href="#"><i>◐</i>Routines</a>
</nav>
```
```css
.oui-bottomnav{position:fixed;left:0;right:0;bottom:0;display:flex;background:#101010;
  padding:8px 8px calc(10px + env(safe-area-inset-bottom))}
.oui-bottomnav a{flex:1;display:flex;flex-direction:column;align-items:center;gap:2px;
  color:#9a9a9a;text-decoration:none;font-size:11px;padding:6px}
.oui-bottomnav a.active{color:#fff}
.oui-bottomnav i{font-style:normal;font-size:22px}
```

### 6. Bottom dialog (action sheet)

```html
<div class="oui-scrim open"><div class="oui-sheet" role="dialog">
  <h2>Screen Timeout</h2>
  <button>15 seconds</button><button>30 seconds</button><button class="sel">1 minute</button>
</div></div>
```
```css
.oui-scrim{position:fixed;inset:0;background:rgba(0,0,0,.55);display:none;align-items:flex-end}
.oui-scrim.open{display:flex}
.oui-sheet{width:100%;background:#1e1e1e;border-radius:28px 28px 0 0;padding:20px 20px 32px;color:#fff}
.oui-sheet h2{font-size:20px;font-weight:600;text-align:center;margin:0 0 12px}
.oui-sheet button{display:block;width:100%;background:none;border:0;color:#fff;
  font-size:16px;padding:14px;cursor:pointer;border-radius:14px;text-align:center}
.oui-sheet button.sel{color:var(--oui-primary);font-weight:600}
```
Dialogs sit at the **bottom** (thumb reach), never centered mid-screen.

### 7. Quick toggles — big round buttons

```html
<button class="oui-qtoggle on" aria-pressed="true"><i>◉</i><span>Wi-Fi</span></button>
```
```css
.oui-qtoggle{width:76px;border:0;background:none;color:#9a9a9a;cursor:pointer;
  display:flex;flex-direction:column;align-items:center;gap:6px;font-size:12px}
.oui-qtoggle i{font-style:normal;width:56px;height:56px;border-radius:50%;background:#1e1e1e;
  display:grid;place-items:center;font-size:24px;color:#9a9a9a}
.oui-qtoggle.on i{background:var(--oui-primary);color:#fff}
.oui-qtoggle.on{color:#fff}
```

### 8. Linear progress

```html
<div class="oui-progress" role="progressbar" aria-valuenow="61"><i style="width:61%"></i></div>
```
```css
.oui-progress{height:6px;border-radius:9999px;background:#2a2a2a;overflow:hidden}
.oui-progress i{display:block;height:100%;border-radius:9999px;background:var(--oui-primary)}
```

### 9. Buttons — contained + text-only

```html
<button class="oui-btn">Turn On</button>
<button class="oui-btn text">Learn More</button>
```
```css
.oui-btn{background:var(--oui-primary);color:#fff;border:0;border-radius:9999px;
  height:48px;padding:0 32px;font-size:15px;font-weight:600;cursor:pointer}
.oui-btn.text{background:none;color:var(--oui-primary-dark)}
```
One UI buttons are pill-shaped; text buttons use the primary-dark blue.

### 10. Search field

```html
<label class="oui-search"><input placeholder="Search Settings"></label>
```
```css
.oui-search{display:block;background:#1e1e1e;border-radius:9999px;padding:0 20px}
.oui-search input{width:100%;height:48px;background:none;border:0;color:#fff;font-size:15px;outline:none}
.oui-search input::placeholder{color:#9a9a9a}
```
Fully round, tonal gray fill — sits at the top of the interaction area.

## Motion

No published motion spec as detailed as M3's — keep it fast and natural:
state changes (switch, toggle) ~200ms ease-out; the big-title collapse tracks
the scroll with a quick fade/scale (~250ms). 🟡 cross-referenced from shipping
app behavior.

## Do / Don't

- ✅ Do put the big title and glanceable info in the top viewing area, and
  every tappable control in the bottom interaction area.
  ❌ Don't place buttons, tabs or switches at the top of the screen.
- ✅ Do collapse the giant title into a small centered toolbar title on scroll.
  ❌ Don't keep a static 34px header while the user scrolls.
- ✅ Do use the single blue accent `#0381fe` for switches, radios, focused
  inputs and selected states.
  ❌ Don't mix accent colors — One UI has one blue, not a rainbow.
- ✅ Do round cards and sheets hard (26–28px+ radii).
  ❌ Don't use 4–8px corners or sharp rectangles — that's not One UI.
- ✅ Do anchor dialogs and popups to the bottom of the screen.
  ❌ Don't center modal dialogs mid-screen.
- ✅ Do write titles and tab labels in Title Case ("Screen Timeout").
  ❌ Don't use ALL CAPS or sentence case for component titles.
- ✅ Do design dark-first (#080808 background, #1e1e1e raised surfaces).
  ❌ Don't ship a bright white settings page as the default One UI look.
- ✅ Do make quick toggles big, round and thumb-sized (56px+).
  ❌ Don't shrink toggles to dainty 40px circles.

## Copy voice

One UI is a system, not a brand — in-product copy is plain, direct and
action-led, in Title Case for labels. Examples: "Screen Timeout", "Protect
Battery", "Your phone will restart to apply the update."
