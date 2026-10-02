---
name: geist
description: Vercel's Geist design language — minimal monochrome UI with hairline borders, Geist Sans/Mono, and restrained color. Use for developer tools, dashboards, and docs.
---

# Geist

Vercel's design language. A monochrome, developer-first system: black and white do the heavy lifting, a strict gray scale draws every hairline, and chroma is rationed to links, status, and code. Surfaces are flat, borders beat shadows, and type is set tight in Geist Sans with Geist Mono accents.

## Principles

1. **The ink is the brand.** Black (`#000`) is the primary action color — primary buttons, logo, strongest text. There is no second brand color. In dark mode the polarity flips: white text on pure black.
2. **Restraint over decoration.** Flat surfaces and 1px hairline borders first (`#eaeaea`); shadows only as multi-layer, near-invisible stacks. If it doesn't earn its pixels, remove it.
3. **Developer-first detail.** Tabular numbers, uppercase mono micro-labels, code blocks treated as first-class content, copy affordances on every snippet. The UI speaks the user's syntax.
4. **Chroma is functional.** Blue means links, green/red/amber mean status, and that's nearly it. Color is never decorative chrome.
5. **Speed is the aesthetic.** Transitions are 100–200ms; nothing bounces. The interface should feel as fast as the platform behind it.

## Color

Legend: ✅ documented from vercel.com production CSS / extracted token snapshots · 🟡 cross-referenced across community mirrors of Geist · ⚠️ approximation.

| Token | Hex | Role |
|---|---|---|
| `black` ✅ | `#000000` | Primary CTA, logo, dark text in dark mode (inverted) |
| `ink` ✅ | `#171717` | Body text on light surfaces (gray-900) |
| `white` ✅ | `#ffffff` | Page + card surface, text on black |
| `gray-50` ✅ | `#fafafa` | Default page background / soft surface |
| `gray-100` ✅ | `#f5f5f5` | Inset surfaces, hover fills, dropdown menus |
| `gray-200` ✅ | `#e5e5e5` | Borders (alt) |
| `gray-300` ✅ | `#d4d4d4` | Disabled / placeholder strokes |
| `gray-400` ✅ | `#a3a3a3` | Tertiary text |
| `gray-500` ✅ | `#737373` | Secondary text |
| `gray-600` ✅ | `#525252` | — |
| `gray-700` ✅ | `#404040` | — |
| `gray-800` ✅ | `#262626` | Borders in dark mode |
| `gray-900` ✅ | `#171717` | Text (light) / surface (dark) |
| `gray-950` ✅ | `#0a0a0a` | Dark surfaces |
| `hairline` ✅ | `#ebebeb` | 1px dividers, card borders, input borders |
| `link-blue` ✅ | `#0070f3` | Links and only links (also seen as `#0072f5` / `#0068d6` in different surfaces) 🟡 |
| `success` 🟡 | `#17c964` | Success states (classic Geist token) |
| `error` 🟡 | `#ee0000` | Error states (also `#ff3333` in some surfaces) |
| `warning` 🟡 | `#f5a623` | Warning states |
| `violet` 🟡 | `#7928ca` | Accent scale (console highlights, gradient stops) |
| `cyan` 🟡 | `#50e3c2` | Accent scale (brand gradient mint-cyan) |
| `preview-pink` 🟡 | `#de1d8d` | "Preview deployment" status |
| `ship-red` 🟡 | `#ff5b4f` | "Ship / production" accent |
| `develop-blue` 🟡 | `#0a72ef` | "Development" workflow accent |

Dark mode: background flips to pure `#000000`, text to `#ededed`/`#ffffff`, hairlines become `rgba(255,255,255,0.08)`. Everything else follows.

## Typography

- **Geist Sans** ✅ — primary typeface. Fallback stack: `Geist, Inter, ui-sans-serif, system-ui, -apple-system, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif` (Inter is the endorsed substitute when Geist isn't licensed). Enable `font-feature-settings: "liga"` globally.
- **Geist Mono** ✅ — code, metrics, terminal, tabular data, uppercase micro-labels. Fallbacks: `"Geist Mono", ui-monospace, SFMono-Regular, "Roboto Mono", Menlo, Monaco, Consolas, monospace`. Use `font-variant-numeric: tabular-nums` / `"tnum"` for numbers in tables and badges.
- **Scale & rules** 🟡: display caps at weight 600 (never heavier for voice); tight tracking — `-0.04em` on display, `-0.02em` on headings; body 14–16px, `line-height: 1.5`; secondary text `#737373` / `#666`; micro-labels 12px mono uppercase. Sentence case everywhere — no title case.

## Layout & spacing

- **Spacing**: 4px base ladder — 4 / 8 / 12 / 16 / 24 / 32 / 40 / 48 / 64 / 96 / 128px. Generous section air (64px+ on marketing heroes). ✅ (documented scale)
- **Radius** 🟡: 6px default compact UI radius; 8px softer marketing surfaces; 9999px pills reserved for badges and marketing CTAs only — never pill-shaped product buttons.
- **Borders & shadows** ✅: hairline borders do the structural work where other systems would use shadow or tinted panels. When depth is needed, stack hairline ring + ultra-subtle shadows, e.g. `0 0 0 1px rgba(0,0,0,.08), 0 2px 2px rgba(0,0,0,.04)`. Never a heavy drop shadow (opacity ≤ 0.1).
- **Page width** 🟡: 1200px product / 1400px marketing containers. Grid columns separated by collapsed 1px hairlines ("crosshair" intersections) on data-dense surfaces.

## Components

8 signature components, copy-pasteable. Light mode shown; flip polarity for dark.

### 1. Button

Primary = black fill, white text. Secondary = hairline border. Tertiary = ghost. Heights sm 32 / md 40 / lg 48; radius 6px; 14px/500.

```html
<button class="geist-btn geist-btn--primary">Deploy</button>
<button class="geist-btn geist-btn--secondary">Cancel</button>
<button class="geist-btn geist-btn--error">Delete</button>
```
```css
.geist-btn { display:inline-flex; align-items:center; justify-content:center;
  height:40px; padding:0 16px; border-radius:6px; font:500 14px/1 Inter,system-ui,sans-serif;
  cursor:pointer; transition:background .15s, color .15s, border-color .15s; }
.geist-btn--primary { background:#000; color:#fff; border:1px solid #000; }
.geist-btn--primary:hover { background:#333; }
.geist-btn--secondary { background:#fff; color:#171717; border:1px solid #eaeaea; }
.geist-btn--secondary:hover { border-color:#a3a3a3; }
.geist-btn--error { background:#ee0000; color:#fff; border:1px solid #ee0000; }
```

### 2. Badge

Status pill: height 24px, 12px/500, `tabular-nums`. Tone maps to a tinted background + dark text of the same scale (e.g. blue: `#ebf5ff` bg, `#0068d6` text).

```html
<span class="geist-badge geist-badge--blue">● Ready</span>
<span class="geist-badge geist-badge--gray">Queued</span>
<span class="geist-badge geist-badge--red">● Failed</span>
```
```css
.geist-badge { display:inline-flex; align-items:center; gap:6px; height:24px;
  padding:0 10px; border-radius:999px; font:500 12px/1 Inter,system-ui,sans-serif;
  font-variant-numeric:tabular-nums; }
.geist-badge--blue  { background:#ebf5ff; color:#0068d6; }
.geist-badge--gray  { background:#f5f5f5; color:#525252; }
.geist-badge--red   { background:#fdeeee; color:#ee0000; }
.geist-badge--green { background:#e8f8ee; color:#17a34a; }
```

### 3. Snippet / Code block

Mono text in a hairline box with a copy affordance on the right — the signature Geist developer detail. Optional language tag in the header.

```html
<div class="geist-snippet">
  <span class="geist-snippet__tag">Terminal</span>
  <code>npm i -g vercel</code>
  <button class="geist-snippet__copy" aria-label="Copy">⧉</button>
</div>
```
```css
.geist-snippet { display:flex; align-items:center; gap:12px; padding:12px 16px;
  background:#fafafa; border:1px solid #eaeaea; border-radius:6px;
  font:400 13px/1.5 "Geist Mono",ui-monospace,SFMono-Regular,Menlo,monospace; }
.geist-snippet__tag { font-size:11px; text-transform:uppercase; letter-spacing:.06em; color:#737373; }
.geist-snippet code { flex:1; overflow-x:auto; white-space:pre; }
.geist-snippet__copy { border:1px solid #eaeaea; background:#fff; border-radius:6px;
  padding:6px 10px; cursor:pointer; font-size:13px; }
.geist-snippet__copy:hover { border-color:#a3a3a3; }
```
(Replace `⧉` with a real copy SVG icon in production.)

### 4. Note

One-line callout: colored left treatment or tinted variant, 14px text, 6px radius. Types: secondary, success, error, warning, violet, cyan.

```html
<div class="geist-note geist-note--warning">
  <strong>Note:</strong> Preview deployments are kept for 30 days on the Hobby plan.
</div>
```
```css
.geist-note { padding:12px 16px; border-radius:6px; font:400 14px/1.6 Inter,system-ui,sans-serif;
  border:1px solid #eaeaea; background:#fafafa; color:#171717; }
.geist-note--warning { background:#fff8ec; border-color:#f5a623; }
.geist-note--error   { background:#fdeeee; border-color:#ee0000; }
.geist-note--success { background:#e8f8ee; border-color:#17c964; }
```

### 5. Card

Border first, no shadow; title 16px/600 with tight tracking, description `#666` 14px.

```html
<div class="geist-card">
  <h3>Analytics</h3>
  <p>Real-time insights for every deployment, edge request included.</p>
</div>
```
```css
.geist-card { background:#fff; border:1px solid #eaeaea; border-radius:8px; padding:24px; }
.geist-card h3 { font:600 16px/24px Inter,system-ui,sans-serif; letter-spacing:-.02em; color:#171717; }
.geist-card p { margin-top:8px; font:400 14px/20px Inter,system-ui,sans-serif; color:#666; }
.geist-card:hover { border-color:#d4d4d4; }
```

### 6. Input

Hairline border at rest, two-layer blue focus ring (`box-shadow` ring + border-color), 6px radius.

```html
<input class="geist-input" type="text" placeholder="my-project" />
```
```css
.geist-input { height:40px; padding:0 12px; border:1px solid #eaeaea; border-radius:6px;
  font:400 14px/1 Inter,system-ui,sans-serif; color:#171717; background:#fff; outline:none;
  transition:border-color .15s, box-shadow .15s; }
.geist-input::placeholder { color:#a3a3a3; }
.geist-input:focus { border-color:#0070f3; box-shadow:0 0 0 1px #0070f3; }
```

### 7. Tabs

Underline indicator, mono-ish small labels, no pill background.

```html
<div class="geist-tabs">
  <button class="geist-tab is-active">Deployments</button>
  <button class="geist-tab">Analytics</button>
  <button class="geist-tab">Settings</button>
</div>
```
```css
.geist-tabs { display:flex; gap:4px; border-bottom:1px solid #eaeaea; }
.geist-tab { padding:10px 12px; font:500 13px/1 Inter,system-ui,sans-serif; color:#737373;
  background:none; border:none; border-bottom:2px solid transparent; margin-bottom:-1px; cursor:pointer; }
.geist-tab:hover { color:#171717; }
.geist-tab.is-active { color:#171717; border-bottom-color:#000; }
```

### 8. Tooltip

Small, dark, mono-friendly: black bubble, white text, 12px, minimal padding, no arrow decoration needed.

```html
<button class="geist-has-tip" data-tip="Copied to clipboard">Copy</button>
```
```css
.geist-has-tip { position:relative; }
.geist-has-tip::after { content:attr(data-tip); position:absolute; bottom:calc(100% + 8px);
  left:50%; transform:translateX(-50%); background:#000; color:#fff;
  font:500 12px/1.5 "Geist Mono",ui-monospace,monospace; padding:4px 8px;
  border-radius:6px; white-space:nowrap; opacity:0; pointer-events:none; transition:opacity .15s; }
.geist-has-tip:hover::after { opacity:1; }
```

## Motion

Geist has no motion language to show off — the rule is near-invisibility: 100–200ms `ease` transitions on color/border/opacity, loading states use a segmented-opacity spinner rather than a rotating loader. Nothing springs, bounces, or parallaxes.

## Do / Don't

- **Do** use `#000` for the primary CTA and reserve blue strictly for links — a black button and a blue link side by side is the canonical Geist pairing.
- **Don't** give product buttons a pill radius; pills are for badges and marketing CTAs only (product buttons are 6px).
- **Do** draw structure with 1px `#ebebeb` hairlines — table rows, cards, inputs — before reaching for shadows or tinted panels.
- **Don't** use weight 700 to create voice; drop to 600 and tighten tracking instead (`-0.04em` display, `-0.02em` headings).
- **Do** put a copy affordance on every snippet and code block, with "Copied" feedback.
- **Don't** introduce warm colors (orange, yellow, green) into chrome — chroma is status-only; keep the frame monochrome.
- **Do** use uppercase 12px Geist Mono micro-labels with wide tracking for eyebrows and section tags.
- **Don't** center-align everything into a marketing hero when building product UI; Geist dashboards are left-aligned, dense, and hairline-ruled.

## Copy voice

Plain, technical, confident. Short sentences, sentence case, no exclamation marks, no marketing adjectives. The docs talk like an engineer explaining to an engineer.

- "Deployments are immutable. Roll back in one click."
- "Preview URLs are generated for every push."
- "Usage resets on the 1st of every month."
