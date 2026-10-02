---
name: primer
description: GitHub's Primer design system — functional color tokens, system font stack, UnderlineNav, Labels, Blankslates, and dense developer-tool UI that is boring on purpose. Use for dashboards, repo pages, admin panels, and anything that should feel like github.com.
---

# Primer

The look of github.com, built from GitHub's open-source design system
(primer.style): functional color tokens (`fgColor` / `bgColor` /
`borderColor`), a 4px spacing grid, the system font stack, and components
that are deliberately unglamorous. Primer is infrastructure, not branding.

## Principles

1. **Accessible by default.** Primer enforces WCAG 2.1 AA at the token
   level — 4.5:1 text contrast, 3:1 link-vs-text — documented in the
   primitives contributor docs (✅). Never trade contrast for style.
2. **Functional, not decorative.** Color always carries meaning: `accent`
   = links/actions, `success` = open/good, `danger` = closed/bad,
   `attention` = warnings, `done` = purple. There is no "brand color"
   beyond meaning.
3. **Boring on purpose.** The chrome disappears so the work — code,
   issues, diffs — stands out. If your UI is exciting, you've strayed
   from Primer.
4. **Same tokens, every theme.** `fgColor.default` resolves to `#1f2328`
   in light, `#f0f6fc` in dark. Build with roles, never raw hex, and the
   UI survives light / dark / dark-dimmed / high-contrast.
5. **Dense but calm.** Developer tools show a lot of information: rows
   stay compact, borders stay 1px, shadows stay reserved for overlays,
   and hierarchy comes from type weight and muted text, not decoration.

## Color

Primer Primitives: every color is a **functional token**
`{fgColor|bgColor|borderColor|shadow|control|button}-…` resolving to base
scales (`blue.0–9`, `gray.0–9`, …). Light values verified on
[primer.style/foundations/color](https://primer.style/foundations/color/);
dark/dimmed cross-referenced from the `primer/primitives` themes.

Legend: ✅ official/documented · 🟡 cross-referenced · ⚠️ community approximation

**Light theme** (✅)

| Token | Hex | Role |
|---|---|---|
| `--fgColor-default` | `#1f2328` | Primary text — near-black, never pure black |
| `--fgColor-muted` | `#59636e` | Secondary text, timestamps, metadata |
| `--fgColor-accent` | `#0969da` | Links, selected nav, accent text |
| `--fgColor-success` | `#1a7f37` | Open/good states (green text) |
| `--fgColor-danger` | `#d1242f` | Closed/bad states, errors |
| `--fgColor-attention` | `#9a6700` | Warnings, degraded states |
| `--fgColor-done` | `#8250df` | Purple: merged, sponsors, "done" |
| `--bgColor-default` | `#ffffff` | Page canvas |
| `--bgColor-muted` | `#f6f8fa` | Subtle surfaces, row hover, wells |
| `--bgColor-inset` | `#f6f8fa` | Inset inputs, code blocks |
| `--borderColor-default` | `#d1d9e0` | Standard 1px borders and dividers |
| `--borderColor-muted` | `#d1d9e0b3` | Subtle dividers |
| `--focus-outlineColor` | `#0969da` | 2px focus ring |
| `--button-primary-bgColor-rest` | `#1f883d` | Primary CTA (green, not blue — GitHub's signature) |
| `--bgColor-accent-muted` | `#ddf4ff` | Tint behind info content |

**Dark theme** (🟡)

| Token | Hex | Role |
|---|---|---|
| `--fgColor-default` | `#f0f6fc` | Primary text |
| `--fgColor-muted` | `#9198a1` | Secondary text |
| `--fgColor-accent` | `#4493f8` | Links, accent |
| `--fgColor-success` | `#3fb950` | Open/good |
| `--fgColor-danger` | `#f85149` | Closed/bad |
| `--fgColor-attention` | `#d29922` | Warnings |
| `--fgColor-done` | `#ab7df8` | Purple |
| `--bgColor-default` | `#0d1117` | Page canvas |
| `--bgColor-muted` | `#151b23` | Subtle surfaces |
| `--bgColor-inset` | `#010409` | Deepest inset (near-black) |
| `--borderColor-default` | `#3d444d` | Standard borders |
| `--bgColor-accent-emphasis` | `#1f6feb` | Filled accent elements |
| `--bgColor-success-emphasis` | `#238636` | Filled green elements |

**Dark-dimmed theme** (🟡 — GitHub's third real theme)

| Token | Hex |
|---|---|
| `--bgColor-default` | `#1c2128` |
| `--bgColor-muted` | `#22272e` |
| `--fgColor-default` | `#adbac7` |
| `--fgColor-muted` | `#768390` |
| `--fgColor-accent` | `#539bf5` |
| `--borderColor-default` | `#444c56` |

**Rules of use**

- Text = `fgColor-*`, surfaces = `bgColor-*`, lines = `borderColor-*`.
  Never pick a raw scale color for UI chrome; scales are for data viz.
- Semantic colors map to workflow states: open = `success` green,
  closed = `danger` red, merged = `done` purple, draft = `neutral` gray.
- The primary action button is **green** (`#1f883d`), links are
  **blue** (`#0969da`) — GitHub's most copied quirk.

## Typography

- **Face:** the system stack, always — ✅ documented:
  `-apple-system, BlinkMacSystemFont, "Segoe UI", "Noto Sans", Helvetica,
  Arial, sans-serif, "Apple Color Emoji", "Segoe UI Emoji"`.
  No webfont is ever loaded. That's the Primer look.
- **Mono** (code, SHAs, counts): `ui-monospace, SFMono-Regular, "SF Mono",
  Menlo, Consolas, "Liberation Mono", monospace` (🟡).
- **Scale** — Primer Primitives functional type tokens (🟡):

| Token | Size / line-height | Weight |
|---|---|---|
| `display` | 2.75rem / 2.75rem | 500 |
| `title-large` | 2rem / 2.5rem | 600 |
| `title-medium` | 1.25rem / 1.875rem | 600 |
| `title-small` | 1rem / 1.5rem | 600 |
| `subtitle` | 1.25rem / 1.875rem | 400 |
| `body-large` | 1rem / 1.5rem | 400 |
| `body-medium` | 0.875rem / 1.25rem | 400 |
| `body-small` / `caption` | 0.75rem / 1rem | 400 |

- **Rules:** body UI text is 14px (`body-medium`); 12px is reserved for
  metadata, labels, and table headers. Headings are semibold (600), never
  light — Primer has no thin aesthetic. Line heights sit on the 4px grid.

## Layout & spacing

- **Base unit 4px** (✅ documented: "line height values … align to the 4px
  grid"). Spacing scale: 0 · 4 · 8 · 16 · 24 · 32 · 40 · 48 · 64 · 80 ·
  96 · 112 · 128px — every value a multiple of 4 (🟡 Primer CSS).
- **Borders:** 1px `borderColor-default` everywhere. Cards are flat
  bordered boxes (`bgColor-default`), not shadowed — shadows are
  **reserved for floating elements** (dialogs, dropdowns, tooltips):
  `shadow-floating-small`, `shadow-floating-medium` (✅ token names from
  primer.style).
- **Radii:** 4 / 6 / 8 / 12px + full pill (🟡 Primer radius scale).
- **PageLayout:** GitHub-style two-column app layout — main column plus
  optional sidebar pane, max-width ~1280px container, generous top
  whitespace. Repo header pattern: org avatar + `org / repo` name, Public
  label, action buttons right-aligned, UnderlineNav below the divider.

## Components

Copy-pasteable HTML/CSS using Primer token names. Base context:

```css
:root{
  --fgColor-default:#1f2328; --fgColor-muted:#59636e; --fgColor-accent:#0969da;
  --bgColor-default:#fff; --bgColor-muted:#f6f8fa;
  --borderColor-default:#d1d9e0;
  --button-primary-bgColor-rest:#1f883d;
}
body{font-family:-apple-system,BlinkMacSystemFont,"Segoe UI","Noto Sans",
  Helvetica,Arial,sans-serif,"Apple Color Emoji","Segoe UI Emoji";
  font-size:14px; line-height:1.5; color:var(--fgColor-default);}
```

**1. Buttons** — 32px medium (28px small), 6px radius, weight 500,
subtle 1px border. Primary is green.

```html
<button class="btn">Default</button>
<button class="btn btn-primary">New pull request</button>
<button class="btn btn-danger">Delete</button>
<button class="btn btn-invisible">Cancel</button>
<style>
.btn{appearance:none;display:inline-flex;align-items:center;gap:6px;
  height:32px;padding:0 12px;font:500 14px/1 system-ui,-apple-system,"Segoe UI",sans-serif;
  color:#25292e;background:#f6f8fa;border:1px solid #d1d9e0;border-radius:6px;
  box-shadow:0 1px 0 0 #1f23280a;cursor:pointer;transition:background .08s}
.btn:hover{background:#eff2f5}
.btn-primary{background:#1f883d;border-color:#1f232826;color:#fff}
.btn-primary:hover{background:#1c8139}
.btn-danger{color:#d1242f}
.btn-danger:hover{background:#cf222e;border-color:#1f232826;color:#fff}
.btn-invisible{background:transparent;border-color:transparent;box-shadow:none;color:#0969da}
.btn-invisible:hover{background:#818b981a;color:#0969da}
</style>
```

**2. Banner** — full-width status strip: icon + bold title + description,
optional dismiss. Variants: info (blue), success (green), warning
(yellow), critical (red), upsell (purple).

```html
<div class="banner banner-warning" role="alert">
  <svg width="16" height="16" viewBox="0 0 16 16" fill="currentColor"><path d="M8 1.5a6.5 6.5 0 1 0 0 13 6.5 6.5 0 0 0 0-13ZM7 4h2v5H7V4Zm0 6h2v2H7v-2Z"/></svg>
  <div><strong>2 Dependabot alerts need your attention.</strong>
  Review them to keep dependencies secure.</div>
  <button aria-label="Dismiss">✕</button>
</div>
<style>
.banner{display:flex;gap:8px;align-items:flex-start;padding:12px 16px;
  font-size:14px;border:1px solid;border-radius:6px;color:#1f2328}
.banner svg{flex:none;margin-top:2px}
.banner div{flex:1}
.banner button{background:none;border:0;color:inherit;cursor:pointer;font-size:14px}
.banner-info{background:#ddf4ff;border-color:#54aeff66;color:#1f2328}
.banner-warning{background:#fff8c5;border-color:#d4a72c66}
.banner-critical{background:#ffebe9;border-color:#ff818266}
.banner-success{background:#dafbe1;border-color:#4ac26b66}
</style>
```

**3. Dialog** — 440px panel, 12px radius, backdrop `#c8d1da66`,
header / body / footer with right-aligned buttons.

```html
<div class="overlay"><div class="dialog" role="dialog" aria-modal="true">
  <header><h2>Delete branch?</h2><button aria-label="Close">✕</button></header>
  <div class="dialog-body"><p>The <code>feature/csv-export</code> branch will be
  permanently deleted. This cannot be undone.</p></div>
  <footer><button class="btn btn-invisible">Cancel</button>
  <button class="btn btn-danger">Delete branch</button></footer>
</div></div>
<style>
.overlay{position:fixed;inset:0;background:#c8d1da66;display:flex;
  align-items:center;justify-content:center;z-index:100}
.dialog{width:440px;max-width:calc(100vw - 32px);background:#fff;border-radius:12px;
  box-shadow:0 0 0 1px #d1d9e080,0 24px 48px -12px #25292e14}
.dialog header{display:flex;justify-content:space-between;align-items:center;
  padding:16px;border-bottom:1px solid #d1d9e0}
.dialog header h2{font-size:16px;font-weight:600;margin:0}
.dialog header button{background:none;border:0;cursor:pointer;color:#59636e}
.dialog-body{padding:16px;font-size:14px}
.dialog footer{display:flex;justify-content:flex-end;gap:8px;padding:16px;
  border-top:1px solid #d1d9e0}
code{font-family:ui-monospace,SFMono-Regular,Menlo,Consolas,monospace;
  font-size:12px;background:#eff1f3;padding:2px 4px;border-radius:4px}
</style>
```

**4. DataTable** — 12px muted uppercase-ish header, 1px row dividers,
sortable headers, row hover.

```html
<table class="dtable">
  <thead><tr><th>Title</th><th>Status</th><th class="num">+ lines</th></tr></thead>
  <tbody>
    <tr><td><a href="#">Fix off-by-one in balance rounding</a></td>
        <td><span class="lbl lbl-open">Open</span></td><td class="num">+42</td></tr>
  </tbody>
</table>
<style>
.dtable{width:100%;border-collapse:collapse;font-size:14px}
.dtable th{font-size:12px;font-weight:600;color:#59636e;text-align:left;
  padding:8px 16px;border-bottom:1px solid #d1d9e0;background:#f6f8fa}
.dtable td{padding:12px 16px;border-bottom:1px solid #d1d9e0b3;vertical-align:middle}
.dtable tbody tr:hover{background:#f6f8fa}
.dtable .num{text-align:right;font-family:ui-monospace,Menlo,monospace;font-size:12px}
.dtable a{color:#0969da;text-decoration:none;font-weight:600}
.dtable a:hover{text-decoration:underline}
</style>
```

**5. Blankslate** — centered empty state: large muted icon, title,
short description, one action. Max-width ~480px.

```html
<div class="blankslate">
  <svg width="32" height="32" viewBox="0 0 16 16" fill="#59636e"><path d="M8 0a8 8 0 1 0 0 16A8 8 0 0 0 8 0Zm.93 11.58-2.29.28.34-2.77.82-.06-1.06-1.92 3.04-.37.34 1.36-1.4 1.4 1.31 1.08Z"/></svg>
  <h3>No workflows yet</h3>
  <p>Automate your build, test, and deployment with GitHub Actions.
  Start with a starter workflow or write your own YAML.</p>
  <button class="btn btn-primary">Set up a workflow yourself</button>
</div>
<style>
.blankslate{max-width:480px;margin:48px auto;padding:32px;text-align:center;
  border:1px solid #d1d9e0;border-radius:6px;background:#fff}
.blankslate h3{font-size:20px;font-weight:600;margin:16px 0 4px}
.blankslate p{color:#59636e;font-size:14px;margin:0 0 16px}
</style>
```

**6. Timeline** — vertical connector line, icon badges per event,
condensed entries (commits, comments, merges).

```html
<div class="timeline">
  <div class="tl-item">
    <span class="tl-badge tl-green"><svg width="12" height="12" viewBox="0 0 16 16" fill="#fff"><path d="M8 1.5l2.3 2.3 3.2-.5-.5 3.2L15.3 8l-2.3 1.5.5 3.2-3.2-.5L8 14.5l-2.3-2.3-3.2.5.5-3.2L.7 8l2.3-1.5-.5-3.2 3.2.5z"/></svg></span>
    <div><strong>priya</strong> merged commit <code>a3f9c1d</code> into
    <code>main</code> <span class="muted">· 2 hours ago</span></div>
  </div>
  <div class="tl-item">
    <span class="tl-badge tl-gray"></span>
    <div><strong>marcus</strong> requested changes
    <span class="muted">· yesterday</span></div>
  </div>
</div>
<style>
.timeline{position:relative;padding-left:8px}
.tl-item{position:relative;display:flex;gap:12px;padding:12px 0 12px 24px}
.tl-item::before{content:"";position:absolute;left:13px;top:0;bottom:0;
  width:2px;background:#d1d9e0}
.tl-item:first-child::before{top:20px}
.tl-badge{position:absolute;left:0;top:12px;width:28px;height:28px;border-radius:50%;
  background:#59636e;border:2px solid #fff;display:flex;align-items:center;justify-content:center}
.tl-green{background:#1f883d}
.muted{color:#59636e;font-size:12px}
</style>
```

**7. UnderlineNav** — the signature GitHub tab bar: muted items,
2px accent underline on selected, counter pills.

```html
<nav class="unav" aria-label="Repository">
  <a href="#">Code</a>
  <a href="#" class="sel">Pull requests <span class="counter">3</span></a>
  <a href="#">Issues <span class="counter">12</span></a>
  <a href="#">Actions</a>
</nav>
<style>
.unav{display:flex;gap:8px;border-bottom:1px solid #d1d9e0;overflow-x:auto}
.unav a{display:inline-flex;align-items:center;gap:6px;padding:8px 12px;
  font-size:14px;color:#1f2328;text-decoration:none;white-space:nowrap;
  border-bottom:2px solid transparent;margin-bottom:-1px}
.unav a:hover{border-bottom-color:#d1d9e0}
.unav a.sel{font-weight:600;border-bottom-color:#fd8c73}
.counter{font-size:12px;font-weight:500;min-width:20px;text-align:center;
  padding:0 6px;line-height:20px;border-radius:999px;
  background:#818b981f;border:1px solid #d1d9e0b3}
</style>
```

Selected underline is orange-red (`#fd8c73`): GitHub's real UnderlineNav
selection color — one of Primer's most recognizable details.

**8. Label** — pill badges for categorization. Outline style on white,
filled muted bg in lists.

```html
<span class="lbl">documentation</span>
<span class="lbl lbl-bug">bug</span>
<span class="lbl lbl-open">Open</span>
<style>
.lbl{display:inline-block;font-size:12px;font-weight:500;line-height:20px;
  padding:0 10px;border-radius:999px;border:1px solid #d1d9e0;
  background:#fff;color:#1f2328;white-space:nowrap}
.lbl-bug{border-color:#ff818266;background:#ffebe9;color:#d1242f}
.lbl-open{background:#1f883d;border-color:#1f232826;color:#fff}
</style>
```

Issue-label convention: `bug` = red tint, `enhancement` = teal/green
tint, `documentation` = blue tint, `good first issue` = purple tint —
always tinted backgrounds, never saturated fills, with a matching
`*-muted` border.

**9. Avatar stack + state icons** — overlapping 20px avatars, octicon-style
status dots.

```html
<span class="avatars"><i style="background:#0969da">P</i><i style="background:#8250df">M</i><i style="background:#1f883d">J</i></span>
<span class="state state-open">● Open</span>
<style>
.avatars{display:inline-flex}
.avatars i{width:20px;height:20px;border-radius:50%;border:2px solid #fff;
  margin-left:-8px;color:#fff;font:600 10px/16px system-ui;font-style:normal;
  display:inline-flex;align-items:center;justify-content:center}
.avatars i:first-child{margin-left:0}
.state{font-size:12px;font-weight:600}
.state-open{color:#1a7f37}
</style>
```

## Motion

Primer has no signature motion language: interactive states use fast,
subtle transitions (~80ms background/border-color) and that is it.
One line: keep motion invisible — hover fills, focus rings, and dialog
fade-ins under 150ms; no springs, no page choreography.

## Do / Don't

- **Do** reach for `bgColor-muted` + 1px `borderColor-default` boxes for
  cards and panels — **don't** add drop shadows to static content;
  shadows are for dialogs, dropdowns, and tooltips only.
- **Do** make the primary button green (`#1f883d`) and links blue
  (`#0969da`) — **don't** "fix" them to a single brand color; the
  green-CTA/blue-link split is the GitHub signature.
- **Do** use UnderlineNav with the orange `#fd8c73` selection underline
  for switching views — **don't** build pill tabs or segmented controls
  for primary navigation.
- **Do** show empty states as Blankslate (icon + title + one action) —
  **don't** leave blank pages or write "No data found" in plain text.
- **Do** tint labels (`#ffebe9` bg + `#ff818266` border for bug) —
  **don't** use saturated solid-color badges; Primer labels are always
  soft tints.
- **Do** write headings semibold at 16–20px with the system stack —
  **don't** load a display webfont; the system stack IS the personality.
- **Do** use `fgColor-muted` (`#59636e`) for timestamps and metadata —
  **don't** invent a lighter gray that breaks the 4.5:1 contrast rule.
- **Do** keep tables dense: 12px padded rows, 12px muted headers —
  **don't** add zebra striping; hover highlight is enough.

## Copy voice

Plain, direct, developer-to-developer. Short declarative sentences,
helpful verbs, no hype, no exclamation marks.

- "You're all caught up." — empty state confirmation.
- "Pull requests let you tell others about changes you've pushed to a
  branch in a repository."
- "2 Dependabot alerts need your attention."
- "This branch has no conflicts with the base branch."
