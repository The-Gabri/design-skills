---
name: hyperos
description: Xiaomi HyperOS UI style — vivid wallpaper-forward phone UI, Soft Light Glass translucency, big rounded control-center tiles and fat sliders, MiSans type. Use for Xiaomi-flavored phone mockups, control centers, and settings pages.
---

# HyperOS (Xiaomi)

Xiaomi's system UI language, launched 2023 with the Xiaomi 14 as the
successor to MIUI (2010–2023). Evolved from MIUI's "clean, light, colorful"
look into **Life Aesthetics** — the HyperOS 4 (2026) design language built
around **Soft Light Glass**: translucent, layered, light-reactive surfaces —
frosted blur panels, depth through layering, and light that responds to
interaction and wallpaper. ✅ official/documented (hyperos.mi.com,
Xiaomi HyperOS 4 rollout notes 🟡 cross-referenced for details).

The signature surface is the **Control Center**: no tiny icons — big rounded
tiles that glow vivid blue when on, a music card, and fat vertical
brightness/volume sliders. Settings are minimal: white cards on light gray,
colorful squircle app icons, and the system font MiSans everywhere.

## Principles

1. **Light over heavy.** The whole interface is designed to feel weightless:
   frosted glass, soft blur, gentle translucency. Heavy panels, hard borders,
   and dark chrome are avoided — depth comes from layering, not shadow. ✅
2. **The wallpaper is the canvas.** UI floats above a vivid, often photographic
   wallpaper; glass panels tint and blur against it rather than covering it.
   The lock screen leads with a giant clock overlapping a "vivid" scene. 🟡
3. **Big, friendly geometry.** Large corner radii everywhere (cards ≈16–20dp,
   tiles ≈24dp), colorful gradient app icons, rounded pill sliders. Approachable
   and cheerful, never austere. 🟡
4. **Control, one swipe away.** The Control Center is the heart of HyperOS —
   big touch targets, obvious on/off states (vivid blue = on), fat sliders you
   can grab. Quick settings are felt as physical switches, not menu items. 🟡
5. **One font, one voice.** MiSans is the system typeface across every screen
   and 20+ writing systems — a uniform, humanist grotesque. No mixing families
   for hierarchy. ✅

## Color

HyperOS ships **light-first** (a full dark mode exists, but the canonical
HyperOS look is light and airy). Tokens below approximate the light look.

- `--hy-bg: #F1F1F4` — app/settings background (cool light gray) ⚠️ community approximation
- `--hy-card: #FFFFFF` — cards, tiles, sheets ⚠️
- `--hy-card-tint: #F6F6F9` — inset rows, slider tracks ⚠️
- `--hy-text: #191919` — primary text ⚠️
- `--hy-secondary: #8A8A8E` — secondary text, captions ⚠️
- `--hy-blue: #3482FF` — ACTIVE state: toggle tiles on, switch on, slider fill.
  HyperOS's signature vivid blue (tiles glow blue when enabled). ⚠️
- `--hy-tile-off: #E9E9EE` — inactive toggle tile fill ⚠️
- `--hy-green: #32C759` — battery/charging accents, success ⚠️
- `--hy-red: #FF3B30` — destructive, recording, DND badge ⚠️
- `--hy-yellow: #FFC107` — battery icon accent (HyperOS uses a yellow battery
  glyph in Settings) 🟡 cross-referenced
- `--hy-orange: #FF6900` — Xiaomi brand orange; use for brand moments only
  (logo, marketing), not system chrome ✅ official brand color
- Glass: panels use `background: color-mix(in srgb, #FFFFFF 62%, transparent)`
  + `backdrop-filter: blur(28px) saturate(1.4)` over the wallpaper. HyperOS 4's
  Soft Light Glass adds a subtle top highlight (light from above) and dynamic
  transparency that shifts with content behind it. 🟡

Dark mode (sketch, for completeness): bg `#0F0F12`, cards `#1C1C21`, text
`#F5F5F7`, active blue stays vivid `#4C8DFF`. ⚠️ community approximation

## Typography

**MiSans** — Xiaomi's own system font (free for commercial use,
hyperos.mi.com/font; iF Design Award 2023, HiiiBrand 2023). Variable font with
weights 100–900; HyperOS uses Regular 400 for body, Medium 500 for emphasis,
Semibold 600 sparingly for numbers. ✅ official/documented

Web substitute ladder: MiSans → `Inter` → system-ui. (MiSans is a humanist
neo-grotesque; Inter is the closest Google Font.) Download MiSans TTFs from
hyperos.mi.com/font and `@font-face` them for full fidelity. 🟡

Type scale (HyperOS conventions, px): ⚠️ community approximation
- Clock (lock screen): 96–120 / 600 — giant, the wallpaper hero
- Display title (Settings headers): 28 / 600
- Section title: 20 / 600
- Card title: 17 / 500
- Body / list row: 16 / 400
- Caption / status: 13 / 400, secondary color
- Numeric readouts (time, battery %): 15 / 600, tabular figures

Rules: sentence case everywhere; Settings headers are large and bold on first
screen, then collapse. Never use serif or condensed faces.

## Layout & spacing

- **Radius is the signature.** Settings cards 16–20px; control-center tiles
  24–28px; sliders and switches fully pill (9999px); app icons are squircles
  ≈ 22–26% radius; sheets 24px top corners. ⚠️
- **Spacing:** 8px base; screen margins 16px; card padding 16–20px; control
  center tile gap 10–12px; list rows 56–64px tall. ⚠️
- **Cards float on gray.** Content lives in white rounded cards on the light
  gray page bg — flat, borderless (no outline strokes), with only a very soft
  shadow `0 2px 12px rgb(0 0 0 / .06)` or none at all. Separation is color and
  radius, not borders. 🟡
- **Control Center grid:** 2×2 large tiles (Wi-Fi, Bluetooth, Mobile data,
  Flashlight — with labels under the big tiles), then a 4-across row of small
  circular/rounded toggles, then the tall sliders side by side. Brightness and
  volume sliders are **tall vertical pills**, ~2× the height of a tile. 🟡
- **Settings list:** grouped rows with icon-in-rounded-square on the left
  (each icon its own pastel/gradient color), title + subtitle, chevron right.
  Section headers are small caps-ish gray labels. 🟡

## Components

Copy-pasteable HTML/CSS. Assumes the tokens above and MiSans (or Inter)
loaded.

### 1. Control-center toggle tile (large)

```html
<button class="cc-tile on" aria-pressed="true">
  <span class="cc-icon">◉</span><span class="cc-label">Wi-Fi</span>
</button>
```
```css
.cc-tile{width:100%;aspect-ratio:1.6;border:0;border-radius:26px;cursor:pointer;
  background:var(--hy-tile-off);color:var(--hy-text);
  display:flex;flex-direction:column;align-items:flex-start;justify-content:space-between;
  padding:14px;font:500 13px/18px MiSans,Inter,system-ui;transition:background .25s}
.cc-tile .cc-icon{width:34px;height:34px;border-radius:50%;display:grid;place-items:center;
  background:rgb(0 0 0/.08);font-size:17px}
.cc-tile.on{background:var(--hy-blue);color:#fff}
.cc-tile.on .cc-icon{background:rgb(255 255 255/.25)}
```
On = vivid blue fill, white glyph. Off = light gray fill, dark glyph. In
HyperOS 1+ the big tiles carry labels; the small-row toggles below are
icon-only circles. 🟡

### 2. Brightness / volume slider (tall vertical pill)

```html
<div class="cc-slider" role="slider" aria-valuenow="70" tabindex="0">
  <div class="fill" style="height:70%"></div><span class="glyph">☀</span>
</div>
```
```css
.cc-slider{position:relative;width:76px;height:190px;border-radius:9999px;cursor:pointer;
  background:var(--hy-tile-off);overflow:hidden}
.cc-slider .fill{position:absolute;bottom:0;left:0;right:0;background:#fff;
  border-radius:9999px;transition:height .15s}
.cc-slider .glyph{position:absolute;bottom:12px;left:50%;translate:-50%;font-size:18px;color:var(--hy-secondary)}
/* active fill is white-on-blue when "full control" style, or blue fill on gray track: */
.cc-slider.loud .fill{background:var(--hy-blue)}
```
MIUI/HyperOS sliders are chunky pills you drag with a thumb; the filled
portion is bright (white on colored track, or blue fill on gray). 🟡

### 3. Music playback card

```html
<div class="cc-music">
  <div class="art"></div>
  <div class="meta"><p class="song">Midnight City</p><p class="artist">M83</p></div>
  <div class="ctrl"><button>⏮</button><button class="play">⏸</button><button>⏭</button></div>
</div>
```
```css
.cc-music{display:flex;align-items:center;gap:12px;background:var(--hy-card);
  border-radius:22px;padding:12px 16px}
.cc-music .art{width:48px;height:48px;border-radius:14px;
  background:linear-gradient(135deg,#f6d365,#fda085)} /* album art */
.cc-music .song{font:600 15px/20px MiSans,Inter,system-ui}
.cc-music .artist{font:400 13px/18px MiSans,Inter,system-ui;color:var(--hy-secondary)}
.cc-music .ctrl{margin-left:auto;display:flex;gap:4px}
.cc-music button{border:0;background:transparent;font-size:18px;cursor:pointer;color:var(--hy-text)}
```
In HyperOS the music widget lives inside Control Center with transport
controls inline — not a notification. 🟡

### 4. Settings group card

```html
<section class="set-card">
  <a class="row" href="#"><span class="ric" style="--c:#3482FF">✈</span>
    <span class="rt"><b>Wi-Fi</b><small>HomeNet_5G</small></span><i>›</i></a>
  <a class="row" href="#"><span class="ric" style="--c:#32C759">◉</span>
    <span class="rt"><b>Bluetooth</b><small>On · 2 devices</small></span><i>›</i></a>
</section>
```
```css
.set-card{background:var(--hy-card);border-radius:20px;overflow:hidden}
.set-card .row{display:flex;align-items:center;gap:14px;padding:6px 16px;min-height:60px;
  text-decoration:none;color:inherit;border-bottom:1px solid var(--hy-card-tint)}
.set-card .row:last-child{border-bottom:0}
.ric{width:34px;height:34px;border-radius:10px;background:var(--c);color:#fff;
  display:grid;place-items:center;font-size:17px;flex:none}
.rt{flex:1;display:flex;flex-direction:column}
.rt b{font:500 16px/22px MiSans,Inter,system-ui}
.rt small{font:400 13px/18px MiSans,Inter,system-ui;color:var(--hy-secondary)}
.set-card i{font-style:normal;color:#C7C7CC;font-size:20px}
```
Every Settings row gets its own colored squircle icon — the MIUI trademark. 🟡

### 5. Switch (MIUI style)

```html
<button class="mi-switch on" role="switch" aria-checked="true"><span></span></button>
```
```css
.mi-switch{width:52px;height:32px;border-radius:9999px;border:0;cursor:pointer;
  background:#D9D9DE;position:relative;transition:background .25s}
.mi-switch span{position:absolute;top:3px;left:3px;width:26px;height:26px;border-radius:50%;
  background:#fff;box-shadow:0 2px 6px rgb(0 0 0/.25);transition:left .25s}
.mi-switch.on{background:var(--hy-blue)}
.mi-switch.on span{left:23px}
```
iOS-like pill switch, vivid blue when on. 🟡

### 6. App icon (squircle, gradient)

```html
<div class="appicon" style="--g1:#4facfe;--g2:#00f2fe"><span>✉</span></div>
```
```css
.appicon{width:60px;height:60px;border-radius:16px;display:grid;place-items:center;
  background:linear-gradient(145deg,var(--g1),var(--g2));color:#fff;font-size:26px;
  box-shadow:0 4px 12px rgb(0 0 0/.12)}
```
MIUI/HyperOS icons: rounded squircles with cheerful gradients; the launcher
masks third-party icons into the same shape. 🟡

### 7. Notification card (grouped)

```html
<div class="notif">
  <div class="nh"><span class="appicon mini" style="--g1:#f6d365;--g2:#fda085">♪</span>
    <b>Music</b><time>now</time></div>
  <p>Now playing — Midnight City</p>
</div>
```
```css
.notif{background:color-mix(in srgb,#fff 78%,transparent);backdrop-filter:blur(24px);
  border-radius:20px;padding:12px 16px;margin:8px 0}
.notif .nh{display:flex;align-items:center;gap:8px;font:500 13px/18px MiSans,Inter,system-ui;
  color:var(--hy-secondary)}
.notif time{margin-left:auto;font-weight:400}
.notif p{font:400 15px/21px MiSans,Inter,system-ui;margin-top:6px}
.appicon.mini{width:24px;height:24px;border-radius:7px;font-size:13px}
```
Notifications stack as frosted cards; HyperOS 4 groups them vertically. 🟡

### 8. Horizontal slider (Settings style)

```html
<input type="range" class="mi-range" min="0" max="100" value="60">
```
```css
.mi-range{-webkit-appearance:none;width:100%;height:28px;background:transparent}
.mi-range::-webkit-slider-runnable-track{height:8px;border-radius:9999px;background:var(--hy-tile-off)}
.mi-range::-webkit-slider-thumb{-webkit-appearance:none;width:28px;height:28px;border-radius:50%;
  background:#fff;margin-top:-10px;box-shadow:0 2px 8px rgb(0 0 0/.25);cursor:pointer}
/* fill: paint the track with a linear-gradient sized by JS, or use accent-color fallback */
```
Fat track, big white thumb with soft shadow — the MIUI volume/brightness feel. ⚠️

### 9. Bottom sheet

```html
<div class="scrim"></div>
<div class="sheet"><div class="grabber"></div><h3>Display modes</h3>
  <button class="sheet-opt sel">Vivid <span>✓</span></button>
  <button class="sheet-opt">Natural</button></div>
```
```css
.scrim{position:fixed;inset:0;background:rgb(0 0 0/.35)}
.sheet{position:fixed;left:0;right:0;bottom:0;background:var(--hy-card);
  border-radius:24px 24px 0 0;padding:12px 20px 28px;max-width:480px;margin:0 auto}
.grabber{width:40px;height:5px;border-radius:9999px;background:#D9D9DE;margin:0 auto 16px}
.sheet h3{font:600 18px/24px MiSans,Inter,system-ui;margin-bottom:12px}
.sheet-opt{display:flex;width:100%;justify-content:space-between;align-items:center;border:0;
  background:transparent;padding:14px 4px;font:400 16px/22px MiSans,Inter,system-ui;cursor:pointer}
.sheet-opt.sel{color:var(--hy-blue);font-weight:500}
```
Grabber pill + top-rounded sheet, used for pickers and quick options. ⚠️

### 10. Search field (Settings)

```html
<label class="mi-search"><span>⌕</span><input placeholder="Search settings"></label>
```
```css
.mi-search{display:flex;align-items:center;gap:10px;background:var(--hy-card-tint);
  border-radius:16px;padding:12px 16px;color:var(--hy-secondary)}
.mi-search input{border:0;background:transparent;outline:none;flex:1;
  font:400 16px/22px MiSans,Inter,system-ui;color:var(--hy-text)}
```
Settings opens with a gray rounded search bar, not a stark white one. ⚠️

## Motion

HyperOS motion is fluid and bouncy — "smooth like water". Documented
characteristics, no official token sheet found:
- App open/close and tile presses use springy overshoot rather than linear
  fades (community-measured ≈ `cubic-bezier(.3,1.4,.4,1)` for playful pops,
  250–350ms). ⚠️ community approximation
- Control Center slides down with a blur-fade (~200ms ease-out). ⚠️
- Charging and fingerprint animations are the signature showpieces — expanding
  rings and light sweeps. 🟡

## Do / Don't

- ✅ Do make active states VIVID blue tiles/sliders — "on" should glow.
  ❌ Don't use muted gray-blue or outline-only active states.
- ✅ Do float white, borderless, large-radius cards on a light gray page.
  ❌ Don't add hairline borders or card outlines — MIUI separates with color and radius.
- ✅ Do give every settings row its own colorful squircle icon.
  ❌ Don't use monochrome icon lists — that's not MIUI.
- ✅ Do put a grabber pill and 24px top corners on bottom sheets.
  ❌ Don't use square-cornered modals with X buttons.
- ✅ Do keep the wallpaper visible: frosted, translucent panels over it.
  ❌ Don't paste opaque white panels edge-to-edge over imagery.
- ✅ Do use sentence case, friendly plain copy ("You're all set").
  ❌ Don't use ALL-CAPS labels or technical jargon in consumer surfaces.

## Copy voice

HyperOS is a system, not a brand — microcopy is short, warm, and plain:
"You're all set", "Battery saver is on", "2 devices connected".
