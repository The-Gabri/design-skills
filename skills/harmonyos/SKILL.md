---
name: harmonyos
description: Huawei HarmonyOS design language — "Harmonious" aesthetics, service cards, atomic services, vivid-yet-restrained color, rounded card grids.
---

# HarmonyOS

Huawei's native design language for HarmonyOS / HarmonyOS NEXT ("Harmonious aesthetics"):
immersive full-screen surfaces, service cards instead of plain icons, atomic services that
start from a card with one tap, and a spatial sense of depth built from stacked
material layers — not from borders.

## Principles

1. **Human-centered clarity.** Every screen should feel instantly readable and
   intuitive; remove a control before decorating it. (Official design concepts:
   clarity and intuition first.)
2. **Balanced visual and interaction language.** One balanced vocabulary across the
   system — vivid accents on restrained neutrals, never chaos. "Harmonious
   aesthetics."
3. **Depth through layers, not chrome.** Card materials are one layer, shadows
   another, the background depth-of-field another — a 2D plane that still reads
   as spatial. (Quoted from Huawei UX designer Dafu's design walkthrough.)
4. **Atomic services.** A service is a self-contained card: install-free,
   startable from a tap, pinnable to the home screen. Design for the card, not
   the app chrome.
5. **One language, every device.** Phones, tablets, wearables, cars share the same
   visual DNA with per-device differentiation — the same palette and radius
   rhythm, scaled.
6. **Vivid yet restrained.** High-saturation accents are allowed to sing on a
   calm, near-neutral ground. Color is never the hierarchy — size and weight are.

## Color

Tokens are semantic and theme-mapped; the table gives light-theme values.

| Token | Hex | Role |
|---|---|---|
| `--hos-bg` | `#FFFFFF` 🟡 | Snowy white — light background ("snowy white" is Huawei's own word) |
| `--hos-bg-secondary` | `#F1F3F5` 🟡 | Secondary surfaces in light mode |
| `--hos-starry` | `#131316` ⚠️ | Starry sky gray — dark background, deliberately *not* pure black (Huawei's own word) |
| `--hos-surface` | `#FFFFFF` 🟡 | Card material, light mode (near-white on starry gray in dark mode) |
| `--hos-text-primary` | `#182431` 🟡 | Primary text, light mode |
| `--hos-text-secondary` | `rgba(24,36,49,0.6)` ⚠️ | Secondary text |
| `--hos-accent` | `#0A59F7` 🟡 | Celestial blue — system accent, filled buttons, switches, links |
| `--hos-success` | `#00B578` ⚠️ | Success / connected states |
| `--hos-warning` | `#FF8A00` ⚠️ | Warnings |
| `--hos-danger` | `#FA2A2D` ⚠️ | Destructive actions |

Legend: ✅ official/documented · 🟡 cross-referenced · ⚠️ community approximation.

Rules: one accent per screen; cards stay neutral while accents carry status.
Dark mode keeps the *same* accent hue at slightly higher lightness, never a
different hue.

## Typography

- **Typeface:** HarmonyOS Sans (✅ — designed for the OS around three goals:
  *easy to read, unique, universal*; balances modern letterforms with rounded,
  calligraphic stroke details). Latin fallback stack:
  `"HarmonyOS Sans", -apple-system, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif`.
  The webfont is not on Google Fonts — reference it by name and let the system
  stack take over.
- **Units:** type is measured in `fp` (font-pixels, scales with the user's
  system font size); geometry in `vp`. Honor large-font accessibility modes —
  HarmonyOS users expect them.
- **Scale (phone, fp):** page title `26` / section `22` / card title `18` /
  writing content `17` / body `15` / caption `13` 🟡 (community-distilled from
  ArkUI component libraries against the official guide).
- **Weights:** 400 body, 500 emphasis, 700 titles. No italics in UI.
- Titles sit top-left, large and confident; body text keeps generous line
  height (≥ 1.5 for paragraphs).

## Layout & spacing

- **8vp grid.** Small alignments may use 4vp. Rhythm: `8vp` between closely
  related controls, `12vp` between cards, `16vp` between groups; screen margins
  `16vp` (phone), `24vp` (foldable), `32vp` (tablet) 🟡.
- **Radius grows with size** 🟡: chips `8` · buttons/inputs `12` ·
  standard cards `16` · large cards, sheets, dialogs `24` · pills full-round.
  Nothing in HarmonyOS is sharp-cornered.
- **Cards float, never box.** Card surfaces have no borders; separation comes
  from soft, short shadows (y 2–4, blur 8–16, low alpha) over a blurred
  background layer.
- **Immersive light.** Full-bleed headers where the content scrolls *under* a
  blurred system bar; the status area blends into the page instead of framing it.
- **Service-card grid:** cards come in multiple footprints (e.g. 1×2, 2×2,
  2×4, 4×4 icon-cells) and can stack; mixed sizes on one screen are the norm,
  not an exception.

## Components

### 1. Service card (the signature)

```html
<!-- Service card: live content, rounded, soft shadow, tap-to-open atomic service -->
<article class="hos-card" style="--card-radius:24px">
  <header class="hos-card__top">
    <span class="hos-card__title">Morning run</span>
    <span class="hos-card__more">•••</span>
  </header>
  <p class="hos-card__metric">8,432 <small>steps</small></p>
  <div class="hos-card__bar"><i style="width:68%"></i></div>
  <footer class="hos-card__foot">Goal 12,000 · 70% there</footer>
</article>

<style>
.hos-card{
  background:#fff; border-radius:var(--card-radius,16px);
  padding:16px; box-shadow:0 2px 8px rgba(20,30,45,.06), 0 12px 32px rgba(20,30,45,.08);
  transition:transform .18s ease;
}
.hos-card:active{ transform:scale(.97); }
.hos-card__metric{ font-size:26px; font-weight:700; margin:8px 0; }
.hos-card__metric small{ font-size:13px; font-weight:400; color:#666; }
.hos-card__bar{ height:6px; border-radius:999px; background:#eef1f4; }
.hos-card__bar i{ display:block; height:100%; border-radius:inherit; background:#0A59F7; }
.hos-card__foot{ font-size:13px; color:#666; margin-top:8px; }
</style>
```

### 2. App icon grid + dock

Squircle icons (~22% continuous corner), vivid flat glyphs on calm labels.

```html
<div class="hos-grid">
  <a class="hos-app" href="#"><span class="hos-icon" style="background:linear-gradient(135deg,#0A59F7,#00A0FF)">✉</span>Mail</a>
  <a class="hos-app" href="#"><span class="hos-icon" style="background:linear-gradient(135deg,#FF6A00,#FFB300)">♪</span>Music</a>
  <a class="hos-app" href="#"><span class="hos-icon" style="background:linear-gradient(135deg,#00B578,#00E0A0)">✚</span>Health</a>
  <a class="hos-app" href="#"><span class="hos-icon" style="background:linear-gradient(135deg,#7A5CFF,#B388FF)">◍</span>Photos</a>
</div>
<style>
.hos-grid{ display:grid; grid-template-columns:repeat(4,1fr); gap:16px; }
.hos-app{ display:flex; flex-direction:column; align-items:center; gap:6px;
  font-size:12px; color:#182431; text-decoration:none; }
.hos-icon{ width:56px; height:56px; border-radius:16px; display:grid;
  place-items:center; color:#fff; font-size:24px;
  box-shadow:0 4px 12px rgba(20,30,45,.12); }
</style>
```

### 3. Bottom sheet (panel)

```html
<div class="hos-scrim" hidden></div>
<section class="hos-sheet" aria-modal="true">
  <span class="hos-sheet__grabber"></span>
  <h2>Now playing</h2>
  <!-- sheet content -->
</section>
<style>
.hos-scrim{ position:fixed; inset:0; background:rgba(10,15,25,.35); backdrop-filter:blur(4px); }
.hos-sheet{ position:fixed; left:0; right:0; bottom:0; background:#fff;
  border-radius:24px 24px 0 0; padding:8px 20px 28px;
  box-shadow:0 -8px 32px rgba(10,15,25,.15); }
.hos-sheet__grabber{ display:block; width:40px; height:4px; border-radius:999px;
  background:#dfe4ea; margin:8px auto 16px; }
</style>
```
Slides up with a spring; dismisses by dragging the grabber down or tapping the scrim.

### 4. Alert dialog

```html
<div class="hos-dialog" role="alertdialog" aria-labelledby="d-title">
  <h3 id="d-title">Delete this note?</h3>
  <p>Deleted notes stay in Recently deleted for 30 days.</p>
  <div class="hos-dialog__actions">
    <button class="hos-btn hos-btn--text">Cancel</button>
    <button class="hos-btn hos-btn--text hos-btn--danger">Delete</button>
  </div>
</div>
<style>
.hos-dialog{ background:#fff; border-radius:24px; padding:24px; max-width:320px;
  box-shadow:0 16px 48px rgba(10,15,25,.18); text-align:center; }
.hos-dialog__actions{ display:flex; margin-top:16px; }
.hos-dialog__actions .hos-btn{ flex:1; }
.hos-btn--text{ background:none; border:0; color:#0A59F7; font-size:16px; padding:12px; }
.hos-btn--danger{ color:#FA2A2D; }
</style>
```

### 5. Switch

```html
<button class="hos-switch" role="switch" aria-checked="true"><span></span></button>
<style>
.hos-switch{ width:52px; height:32px; border-radius:999px; border:0;
  background:#0A59F7; position:relative; transition:background .2s; }
.hos-switch span{ position:absolute; top:3px; left:3px; width:26px; height:26px;
  border-radius:50%; background:#fff; box-shadow:0 2px 6px rgba(0,0,0,.2);
  transition:left .2s; }
.hos-switch[aria-checked="false"]{ background:#c9d1da; }
.hos-switch[aria-checked="false"] span{ left:23px; }
</style>
```

### 6. List row

```html
<li class="hos-row">
  <span class="hos-row__icon">◍</span>
  <div><strong>FreeBuds Pro 3</strong><small>Connected · 82% battery</small></div>
  <span class="hos-row__chev">›</span>
</li>
<style>
.hos-row{ display:flex; align-items:center; gap:12px; padding:14px 16px;
  background:#fff; border-radius:16px; list-style:none; }
.hos-row small{ display:block; color:#666; font-size:13px; }
.hos-row__icon{ width:40px; height:40px; border-radius:12px; background:#eef4ff;
  display:grid; place-items:center; color:#0A59F7; }
.hos-row__chev{ margin-left:auto; color:#9aa5b1; font-size:20px; }
</style>
```

### 7. Search bar

```html
<label class="hos-search">
  <svg width="16" height="16" viewBox="0 0 16 16"><circle cx="7" cy="7" r="5" fill="none" stroke="currentColor" stroke-width="2"/><path d="M11 11l3 3" stroke="currentColor" stroke-width="2" stroke-linecap="round"/></svg>
  <input type="search" placeholder="Search apps and services">
</label>
<style>
.hos-search{ display:flex; align-items:center; gap:8px; background:#eef1f4;
  border-radius:999px; padding:10px 16px; color:#666; }
.hos-search input{ border:0; background:none; outline:0; width:100%; font-size:15px; }
</style>
```

### 8. Segmented control / tabs

```html
<div class="hos-seg" role="tablist">
  <button role="tab" aria-selected="true">Today</button>
  <button role="tab" aria-selected="false">Week</button>
  <button role="tab" aria-selected="false">Month</button>
</div>
<style>
.hos-seg{ display:inline-flex; background:#eef1f4; border-radius:999px; padding:3px; }
.hos-seg button{ border:0; background:none; padding:8px 20px; border-radius:999px;
  font-size:14px; font-weight:500; color:#666; }
.hos-seg [aria-selected="true"]{ background:#fff; color:#182431;
  box-shadow:0 2px 6px rgba(20,30,45,.12); }
</style>
```

### 9. Status bar (phone chrome)

Left: time in medium weight. Right: signal / Wi-Fi / battery as thin outline
glyphs, no fills. Content scrolls underneath it — never a solid bar.

### 10. Progress ring (health/atomic fitness card)

```html
<svg class="hos-ring" width="96" height="96" viewBox="0 0 96 96">
  <circle cx="48" cy="48" r="40" fill="none" stroke="#eef1f4" stroke-width="10"/>
  <circle cx="48" cy="48" r="40" fill="none" stroke="#00B578" stroke-width="10"
    stroke-linecap="round" stroke-dasharray="251.3" stroke-dashoffset="80"
    transform="rotate(-90 48 48)"/>
</svg>
```

## Motion

HarmonyOS ships a full animation spec (one-line summary here): panels and
cards move with short, soft springs — enter ~200–300ms, press feedback is a
scale to ~0.97 with no bounce, and opening a service card uses a shared-element
zoom from the card into the sheet so the card *becomes* the destination. Avoid
long or elastic motion; nothing takes longer than ~400ms.

## Do / Don't

- ✅ Lead with a service card showing live content (next train, now playing,
  today's steps). ❌ Don't make the home surface a wall of identical app icons
  with no live information.
- ✅ Mix card footprints (2×2 weather next to 1×2 music and a 2×4 notes strip).
  ❌ Don't force every card into one uniform size.
- ✅ Use the starry-sky-gray dark theme as a real mode, with the same accent
  hue. ❌ Don't ship "dark mode" as pure-black background with blue text.
- ✅ Let content scroll under a blurred status area. ❌ Don't box the top with
  a solid header bar.
- ✅ Radius scales with the component: bigger element, bigger radius.
  ❌ Don't use one 8px radius everywhere.
- ✅ One vivid accent per screen; calm neutrals elsewhere. ❌ Don't rainbow
  the UI — vivid accents on vivid cards reads as noise, not "vivid".
- ✅ Honor the user's font-size setting; layout must survive large text.
  ❌ Don't fix text to pixel sizes that break at 130% scale.
- ✅ Confirm destructive actions in a centered 24-radius dialog with text
  buttons. ❌ Don't bury delete behind a toast.

## Copy voice

Concise, human, service-first — the copy sounds like a helpful concierge, not
a manual. Examples: "Your day, at a glance." / "One tap, and the music follows
you to the car." / "Everything connected. Nothing to set up."

---

Sources: Huawei developer design portal (design concepts, immersive light,
color, font, typography, radius guides); designer walkthrough "Color, Space,
Font" (starry sky gray / snowy white / layered depth / HarmonyOS Sans goals);
community ArkUI component libraries (spacing/radius/type scales distilled from
the official guides).
