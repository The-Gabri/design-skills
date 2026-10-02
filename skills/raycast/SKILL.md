---
name: raycast
description: Dark, keyboard-first Raycast aesthetic — near-black canvas, one red accent, command-bar UI with macOS-native shadows. Use for launcher-style product pages, dev-tool marketing, and command-palette interfaces.
---

# Raycast — Dark Command-Bar Aesthetic

The design language of [raycast.com](https://www.raycast.com): a macOS launcher
and its marketing site built for people who live on the keyboard. Speed is the
brand — near-black blue-tinted surfaces, a single red accent used as
punctuation, and UI that reads like a native macOS overlay, not a website.

## Principles

1. **Keyboard first, mouse optional.** Every action shows its shortcut; nothing
   exists only behind hover. The `⌘K` action panel is the primary UI, not a
   secondary feature.
2. **Speed is visible.** Instant-feeling interactions, tiny motion budgets, and
   copy that talks about saving keystrokes. The interface never looks busy.
3. **Dark by identity, not by theme.** The canvas is near-black blue-tinted
   `#07080A` — never pure `#000000`. Translucent panels, blur, and inset
   highlights simulate real macOS window chrome.
4. **One accent, used as punctuation.** Raycast Red `#FF6363` appears sparingly:
   a hero stripe, a kicker tick, a flagged word. It is a signal, never a
   palette and almost never a button fill.
5. **Minimal marketing.** Short pages, quiet sections, product screenshots of
   the launcher itself instead of illustrations. Let the UI do the talking.
6. **Precision instrument, not playground.** 14px links, 12px labels, 8px/16px
   gaps, hairline borders. Dense but calm.

## Color

✅ official/documented · 🟡 cross-referenced across teardowns · ⚠️ community approximation

| Token | Hex | Role | Legend |
|---|---|---|---|
| Canvas | `#07080A` | Page background — near-black, blue-tinted, never pure black | 🟡 |
| Surface raised 1 | `#111214` | Launcher panel base, raised gradients | 🟡 |
| Surface raised 2 | `#1B1C1E` | Cards, popovers | 🟡 |
| Glass fill | `rgba(255,255,255,0.05)` | Ubiquitous translucent tile/row/input fill | 🟡 |
| Glass fill 2 | `rgba(255,255,255,0.10)` | Selected / raised glass row | 🟡 |
| Raycast Red | `#FF6363` | Brand accent — hero stripes, selection, brand mark | ✅ |
| Deep Crimson | `#D72A2A` | Dark end of the red hero gradient (`#FF6363 → #D72A2A`) | 🟡 |
| Soft Rose | `#ECA5A7` | Pale tone in conic light-sweep edges | 🟡 |
| Ink | `#F9F9F9` | Primary text (near-white, not pure white) | 🟡 |
| Ink secondary | `#9C9C9D` | Secondary text, muted labels | 🟡 |
| Ink dim | `#6A6B6C` | Disabled / low-emphasis text | 🟡 |
| Border hairline | `rgba(255,255,255,0.08)` | Standard containment border on dark | 🟡 |
| Border opaque | `#252829` | Opaque equivalent for dividers | 🟡 |
| Blue accent | `#56C2FF` | Links, focus states, info — interactive accent | 🟡 |
| Green | `#59D499` | Success states | 🟡 |
| Yellow | `#FFC531` | Warnings, highlights | 🟡 |
| Error | `#F83A3A` | Harder red so it never blurs into the coral brand accent | 🟡 |
| CTA surface | `#E6E6E6` | Off-white filled-button fill (primary CTA) | 🟡 |

Rules: blue is for interactive/info, red is the brand. White CTA inversion is
reserved for the Mac download action. Never `#000000` — the blue tint is what
separates this from a generic dark theme.

## Typography

- **Inter** everywhere — headings, body, buttons, captions. ✅ (raycast.com's
  typeface). OpenType features `calt, kern, liga, ss03` enabled globally; `ss02,
  ss08` on display text. 🟡
- Body text carries slight positive letter-spacing (`0.2px–0.4px`) — unusual
  for a dark UI, gives an airy feel. 🟡
- Default weight is `400`; UI chrome and controls use `500`/`600`. Headings
  `600`–`700`. Never lightweight body copy (no `300` for body). 🟡
- **GeistMono** (or `ui-monospace` fallback) for code elements and shortcuts
  readout. 🟡
- Scale: compact chrome — 14px links, 12px labels; display headlines scale
  up dramatically against the quiet surface.

```css
body {
  font-family: 'Inter', system-ui, -apple-system, sans-serif;
  font-feature-settings: "calt", "kern", "liga", "ss03";
  letter-spacing: 0.2px;
  color: #F9F9F9;
}
code { font-family: 'Geist Mono', ui-monospace, SFMono-Regular, Menlo, monospace; }
```

## Layout & spacing

- **Command-bar anatomy** — the signature unit: a 750px panel with (1) search
  input row on top, (2) filtered command list below, (3) footer hint bar
  (`↵ Open · ⌘K Actions · ⌘N/P Navigate`). 🟡
- Compact product UI: 14px links, 12px labels, 8px/16px gaps. Marketing sections
  stay quiet and narrow; the launcher screenshot is the hero. 🟡
- Radius: `6px`/`8px` for UI chrome, `12px` for cards and the launcher panel.
  Nothing rounder. 🟡
- Borders: hairline `rgba(255,255,255,0.08)` for containment, opaque `#252829`
  equivalents for dividers. Subtle inset top highlight
  (`inset 0 1px 0 rgba(255,255,255,0.06)`) on raised elements. 🟡
- Shadows: multi-layer macOS-style — stacked `box-shadows` with inset
  highlights that simulate pressed/raised glass. Deep soft ambient shadow
  under floating panels. 🟡
- Glass panels use `backdrop-filter: blur(40px) saturate(180%)` — blur plus
  saturation boost, always over a translucent `rgba()` background. 🟡
- Hero signature: diagonal red stripe pattern (the brand's iconic motif)
  behind the launcher, plus a soft red conic light-sweep. Red glow stays in
  hero/CTA contexts only. 🟡

## Components

### 1. Command bar (the core component)

```html
<div class="launcher">
  <div class="launcher-search">
    <svg class="icon"><!-- magnifier --></svg>
    <input type="text" placeholder="Search for apps and commands…" />
  </div>
  <div class="launcher-list">
    <div class="launcher-row selected">
      <span class="row-icon">📝</span>
      <span class="row-title">Create Issue</span>
      <span class="row-meta">Jira</span>
    </div>
    <div class="launcher-row">
      <span class="row-icon">🔍</span>
      <span class="row-title">Search Notion</span>
      <span class="row-meta">Notion</span>
    </div>
  </div>
  <div class="launcher-footer">
    <span><kbd>↵</kbd> Open</span>
    <span><kbd>⌘</kbd><kbd>K</kbd> Actions</span>
    <span><kbd>⌘</kbd><kbd>N</kbd><kbd>⌘</kbd><kbd>P</kbd> Navigate</span>
  </div>
</div>
```

```css
.launcher {
  width: 100%; max-width: 750px; margin: 0 auto;
  background: #111214;
  border: 1px solid rgba(255,255,255,0.08);
  border-radius: 12px;
  box-shadow:
    inset 0 1px 0 rgba(255,255,255,0.06),
    0 24px 80px rgba(0,0,0,0.6),
    0 4px 24px rgba(0,0,0,0.5);
  overflow: hidden;
  backdrop-filter: blur(40px) saturate(180%);
}
.launcher-search { display: flex; align-items: center; gap: 12px; padding: 16px; border-bottom: 1px solid rgba(255,255,255,0.08); }
.launcher-search input { flex: 1; background: none; border: none; outline: none; color: #F9F9F9; font-size: 16px; letter-spacing: 0.2px; }
.launcher-row { display: flex; align-items: center; gap: 12px; padding: 10px 16px; border-radius: 8px; margin: 2px 8px; }
.launcher-row.selected { background: rgba(255,255,255,0.10); }
.launcher-footer { display: flex; gap: 20px; padding: 12px 16px; border-top: 1px solid rgba(255,255,255,0.08); font-size: 12px; color: #9C9C9D; }
```

### 2. kbd keycaps

```html
<span class="kbd-row"><kbd>⌘</kbd><kbd>K</kbd></span>
```

```css
kbd {
  display: inline-flex; align-items: center; justify-content: center;
  min-width: 22px; height: 22px; padding: 0 6px;
  font-family: 'Geist Mono', ui-monospace, monospace; font-size: 12px; color: #F9F9F9;
  background: linear-gradient(180deg, #121212, #0D0D0D);
  border: 1px solid rgba(255,255,255,0.12); border-bottom-width: 2px;
  border-radius: 6px;
  box-shadow: 0 2px 6px rgba(0,0,0,0.5);
}
```

### 3. Action panel (⌘K menu)

```html
<div class="action-panel">
  <div class="launcher-row"><span class="row-title">Open in Browser</span><span class="row-meta"><kbd>↵</kbd></span></div>
  <div class="launcher-row"><span class="row-title">Copy Deep Link</span><span class="row-meta"><kbd>⌘</kbd><kbd>C</kbd></span></div>
  <div class="launcher-row destructive"><span class="row-title">Delete</span><span class="row-meta"><kbd>⌘</kbd><kbd>⌫</kbd></span></div>
</div>
```

```css
.action-panel { background: #1B1C1E; border: 1px solid rgba(255,255,255,0.08); border-radius: 8px; padding: 6px;
  box-shadow: 0 16px 48px rgba(0,0,0,0.6), inset 0 1px 0 rgba(255,255,255,0.06); }
.action-panel .destructive .row-title { color: #F83A3A; }
```

### 4. Extension store card

```html
<div class="ext-card">
  <div class="ext-icon" style="background:#FF6363">⇄</div>
  <h3>Google Translate</h3>
  <p>Translate text right from your launcher, powered by Google.</p>
  <div class="ext-foot"><span class="ext-author">raycast</span><span class="ext-count">842k installs</span><button class="btn-ghost">Install</button></div>
</div>
```

```css
.ext-card { background: #101111; border: 1px solid rgba(255,255,255,0.08); border-radius: 12px; padding: 20px;
  box-shadow: inset 0 1px 0 rgba(255,255,255,0.06); }
.ext-icon { width: 40px; height: 40px; border-radius: 10px; display: grid; place-items: center; color: #0D0D0D; font-weight: 700; }
.ext-foot { display: flex; align-items: center; gap: 12px; margin-top: 16px; font-size: 12px; color: #9C9C9D; }
.ext-count { margin-left: auto; }
```

### 5. Buttons — primary (off-white inversion) + ghost

```html
<a class="btn-primary" href="#">Download for Mac</a>
<a class="btn-ghost" href="#">Browse the Store</a>
```

```css
.btn-primary { display: inline-block; padding: 10px 20px; border-radius: 8px;
  background: #E6E6E6; color: #0D0D0D; font-weight: 600; font-size: 14px;
  box-shadow: inset 0 1px 0 rgba(255,255,255,0.4), 0 4px 16px rgba(0,0,0,0.4); }
.btn-ghost { display: inline-block; padding: 10px 20px; border-radius: 8px;
  background: rgba(255,255,255,0.05); color: #F9F9F9; font-weight: 500; font-size: 14px;
  border: 1px solid rgba(255,255,255,0.08); }
.btn-ghost:hover { background: rgba(255,255,255,0.10); }
```

### 6. Search input (standalone)

```html
<div class="search-box"><input type="text" placeholder="Search extensions…" /><kbd>⌘</kbd><kbd>F</kbd></div>
```

```css
.search-box { display: flex; align-items: center; gap: 8px; background: rgba(255,255,255,0.05);
  border: 1px solid rgba(255,255,255,0.08); border-radius: 8px; padding: 10px 14px; max-width: 420px; }
.search-box input { flex: 1; background: none; border: none; outline: none; color: #F9F9F9; font-size: 14px; }
.search-box:focus-within { border-color: #56C2FF; }
```

### 7. Toast

```html
<div class="toast"><span class="toast-dot"></span> Issue created in Jira</div>
```

```css
.toast { display: inline-flex; align-items: center; gap: 10px; background: #1B1C1E;
  border: 1px solid rgba(255,255,255,0.08); border-radius: 8px; padding: 12px 16px;
  font-size: 14px; box-shadow: 0 12px 32px rgba(0,0,0,0.5), inset 0 1px 0 rgba(255,255,255,0.06); }
.toast-dot { width: 8px; height: 8px; border-radius: 50%; background: #59D499; }
```

### 8. Section kicker + heading

```html
<p class="kicker"><span class="kicker-tick"></span>Extensions</p>
<h2 class="section-title">Extend everything.</h2>
```

```css
.kicker { display: flex; align-items: center; gap: 8px; font-size: 12px; font-weight: 600;
  letter-spacing: 0.8px; text-transform: uppercase; color: #9C9C9D; }
.kicker-tick { width: 8px; height: 16px; background: #FF6363; border-radius: 2px; } /* red punctuation */
.section-title { font-size: 32px; font-weight: 700; letter-spacing: -0.5px; color: #F9F9F9; }
```

### 9. Nav (frosted glass)

```html
<nav class="nav">
  <a class="logo" href="#"><span class="logo-mark"></span> Raycast</a>
  <a href="#">Store</a><a href="#">Pro</a><a href="#">Teams</a><a href="#">Changelog</a>
  <a class="btn-primary btn-sm" href="#">Download for Mac</a>
</nav>
```

```css
.nav { position: sticky; top: 0; display: flex; align-items: center; gap: 24px;
  padding: 12px 24px; background: rgba(7,8,10,0.72);
  backdrop-filter: blur(40px) saturate(180%);
  border-bottom: 1px solid rgba(255,255,255,0.08); font-size: 14px; }
.logo-mark { display: inline-block; width: 20px; height: 20px; border-radius: 5px;
  background: linear-gradient(135deg, #FF6363, #D72A2A); vertical-align: -4px; }
.nav a:not(.logo):not(.btn-primary) { color: #9C9C9D; }
.nav a:not(.logo):not(.btn-primary):hover { color: #F9F9F9; }
```

### 10. List row with accessories

```html
<div class="launcher-row selected">
  <span class="row-icon">📅</span>
  <div><div class="row-title">Schedule Meeting</div><div class="row-sub">Next: Design review, 10:00</div></div>
  <span class="tag">Calendar</span>
</div>
```

```css
.row-sub { font-size: 12px; color: #6A6B6C; }
.tag { font-size: 11px; font-weight: 500; color: #9C9C9D; background: rgba(255,255,255,0.05);
  border: 1px solid rgba(255,255,255,0.08); border-radius: 6px; padding: 2px 8px; }
```

## Motion

Fast and subtle — motion exists but stays under the perception threshold:
`120–200ms ease-out` for hovers/selections, `cubic-bezier(0.16, 1, 0.3, 1)` for
panel entrances. No parallax, no slow blobs, no springy overshoot. If in
doubt, make it instant. 🟡

## Do / Don't

- ✅ DO use `#07080A` as the page floor and build panels upward with
  `#111214` → `#1B1C1E`.
- ❌ DON'T leave the background pure white or pure black — the blue tint is
  the brand.
- ✅ DO use `#FF6363` as punctuation: hero stripes, the kicker tick, a
  selection accent — one red element per viewport.
- ❌ DON'T fill primary buttons with `#FF6363` — CTAs are off-white
  `#E6E6E6`; red buttons read as destructive.
- ✅ DO make every action keyboard-accessible and show the shortcut in a real
  keycap: `<kbd>⌘</kbd><kbd>K</kbd>`.
- ❌ DON'T use keycaps as decorative tags without a working action behind
  them.
- ✅ DO use hairline `rgba(255,255,255,0.08)` borders and macOS layered
  shadows (inset top highlight + soft ambient).
- ❌ DON'T use purple-blue gradients or glass cards floating on dark — Raycast
  glow is warm/red and stays in the hero.
- ✅ DO keep chrome compact (14px links, 12px labels) and radius at 6/8/12px.
- ❌ DON'T simplify brand red to `#FF0000` or muted gray text to Tailwind
  `#6B7280` — use `#FF6363` and `#9C9C9D`/`#78787C`.

## Copy voice

Terse, productive, confident. Verbs of speed; zero marketing fluff. Always
mention the shortcut.

- "Supercharge your productivity."
- "Say goodbye to window juggling. Press one hotkey and command your tools."
- "Search for apps, files and commands — your hands never leave the keyboard."
