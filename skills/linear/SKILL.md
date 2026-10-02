---
name: linear
description: Linear.app's dark, precise product aesthetic — use for sleek developer-tool marketing pages and dense keyboard-driven app UIs.
---

# Linear

The look of Linear.app (linear.app): a dark-mode-native, engineering-precise
design language. Craft over decoration. Every pixel feels machined.

## Principles

1. **Craft, not chrome.** The interface disappears so the work stands out.
   Nothing decorative exists without a functional reason.
2. **Speed is the aesthetic.** Dense layouts, instant-feeling 100–200ms
   transitions, and a keyboard-first culture (⌘K, single-letter shortcuts)
   make the product feel fast before you click anything.
3. **Dark by conviction.** Near-black is the native medium, not a theme
   toggle — depth is built from surface lightness steps, not drop shadows
   (shadows read poorly on dark).
4. **One accent, used sparingly.** A single indigo-violet carries brand,
   focus, and selection. Everything else is neutral.
5. **Opinionated defaults.** Linear picks the right behavior so the user
   doesn't configure it: cycles, triage, keyboard flows. The UI mirrors
   that confidence with terse copy and zero clutter.

## Color

Palette cross-referenced from Linear's marketing and app surfaces.

| Token | Hex | Role | Legend |
|---|---|---|---|
| Void black | `#08090a` | Marketing/app background, deepest canvas | ✅ |
| Panel | `#0f1011` | Sidebar, panels | 🟡 |
| Surface 2 | `#161718` | Elevated cards, dropdowns | 🟡 |
| Surface 3 | `#191a1b` | Cards, elevated areas | 🟡 |
| Surface 4 | `#28282c` | Hover states, lightest dark surface | 🟡 |
| Hairline | `rgba(255,255,255,0.05)`–`rgba(255,255,255,0.08)` | Ultra-thin borders, dividers (also observed as `#23252a`) | ✅ |
| Ink | `#f7f8f8` | Primary text — near-white, not pure white | ✅ |
| Ink muted | `#d0d6e0` | Secondary text | 🟡 |
| Ink dim | `#8a8f98` | Metadata, placeholders | 🟡 |
| Ink faint | `#62666d` | Timestamps, disabled states | 🟡 |
| Accent | `#5e6ad2` | The single chromatic color: brand, focus rings, select CTAs | ✅ |
| Accent bright | `#828fff` | Hover / bright accent state | 🟡 |
| Accent vivid | `#7170ff` | Secondary accent use | ⚠️ |
| Success | `#27a644` | Status indicators only, used narrowly | 🟡 |

Notes: contrast comes from light ink on near-black plus hairline borders —
not shadows. Chromatic color appears almost nowhere else; even semantic
colors are rare and narrow.

## Typography

- **Face:** Inter (✅ documented; Linear sets `"cv01", "ss03"` OpenType
  features for a cleaner geometric look). Closest free substitute is Inter
  itself.
- **Signature weight 510** (between regular and medium) for most UI text —
  one of Linear's most distinctive choices. Headings 500–700.
- **Tight tracking:** aggressive negative letter-spacing at display sizes
  (~-3px at 80px, ~-1px at 48px); body holds near -0.05px.
- **Hierarchy:** medium-weight section labels, small uppercase or muted
  captions for metadata. Timestamps and IDs de-emphasize to `#62666d`.
- **Mono:** a monospace face is reserved for code snippets and issue IDs in
  product contexts.

## Layout & spacing

- **Base unit 4px**; steps 4 · 8 · 12 · 16 · 24 · 32 · 48 · 96 (section gaps).
- **Dense but breathing:** component padding stays tight (8–14px) while
  marketing sections separate generously (~96px), creating clear "chapters."
- **Radii small and consistent:** 4 / 6 / 8 / 12px. Marketing panels and
  app screenshots sit in ~16px-radius frames.
- **Marketing rhythm:** centered hero with a short headline, one-line
  subhead, dual CTA, then a high-fidelity product screenshot framed in a
  hairline-bordered panel — the screenshot does the heavy lifting.
- **App rhythm:** dim sidebar + main list. Issue rows are ~48px, split into
  columns: status icon · ID + title · labels · priority · assignees ·
  date. View controls (tabs, filters) stay consistent across views.
- **The glow:** a single subtle radial accent glow sits behind the hero
  product visual — never a full-bleed gradient wash.

## Components

Copy-pasteable HTML/CSS. Base context: `body { background:#08090a;
color:#f7f8f8; font-family:Inter,system-ui,sans-serif; }`.

**1. Primary button**

```html
<a class="lin-btn" href="#">Get started</a>
<style>
.lin-btn{display:inline-flex;align-items:center;gap:8px;background:#5e6ad2;
color:#fff;font-weight:500;font-size:14px;padding:10px 18px;border-radius:8px;
text-decoration:none;border:1px solid rgba(255,255,255,.08);
box-shadow:inset 0 1px 0 rgba(255,255,255,.12);transition:background .15s ease}
.lin-btn:hover{background:#828fff}
</style>
```

**2. Ghost / secondary button**

```html
<a class="lin-ghost" href="#">View the changelog</a>
<style>
.lin-ghost{display:inline-flex;align-items:center;background:rgba(255,255,255,.03);
color:#d0d6e0;font-size:14px;font-weight:500;padding:10px 18px;border-radius:8px;
text-decoration:none;border:1px solid rgba(255,255,255,.08);transition:background .15s ease}
.lin-ghost:hover{background:rgba(255,255,255,.07)}
</style>
```

**3. Keyboard shortcut (kbd)**

```html
<kbd class="lin-kbd">⌘</kbd><kbd class="lin-kbd">K</kbd>
<style>
.lin-kbd{display:inline-flex;align-items:center;justify-content:center;
min-width:22px;height:22px;padding:0 6px;font:500 11px/1 Inter,system-ui,sans-serif;
color:#d0d6e0;background:#28282c;border:1px solid rgba(255,255,255,.08);
border-bottom-width:2px;border-radius:4px}
</style>
```

**4. Command palette**

```html
<div class="lin-palette">
  <input placeholder="Type a command or search…" />
  <div class="lin-row"><span>Create issue</span><span><kbd class="lin-kbd">C</kbd></span></div>
  <div class="lin-row"><span>Go to issues</span><span><kbd class="lin-kbd">G</kbd> then <kbd class="lin-kbd">I</kbd></span></div>
</div>
<style>
.lin-palette{background:#161718;border:1px solid rgba(255,255,255,.08);
border-radius:12px;overflow:hidden;box-shadow:0 24px 64px rgba(0,0,0,.5)}
.lin-palette input{width:100%;background:transparent;border:0;border-bottom:1px solid rgba(255,255,255,.06);
color:#f7f8f8;font-size:14px;padding:14px 16px;outline:none}
.lin-row{display:flex;justify-content:space-between;align-items:center;
padding:10px 16px;font-size:13px;color:#d0d6e0;border-bottom:1px solid rgba(255,255,255,.04)}
.lin-row.active{background:rgba(94,106,210,.14);color:#f7f8f8}
</style>
```

**5. Issue row** (signature app element)

```html
<div class="lin-issue">
  <span class="st st-progress"></span>
  <span class="id">ENG-2298</span>
  <span class="title">Add granular project permissions</span>
  <span class="label">Access</span>
  <span class="avatars"><i style="background:#5e6ad2"></i><i style="background:#27a644"></i></span>
</div>
<style>
.lin-issue{display:flex;align-items:center;gap:12px;padding:11px 16px;
font-size:13.5px;border-bottom:1px solid rgba(255,255,255,.05)}
.lin-issue:hover{background:rgba(255,255,255,.025)}
.lin-issue .id{color:#62666d;font-family:ui-monospace,monospace;font-size:12px}
.lin-issue .title{color:#f7f8f8;font-weight:510}
.st{width:14px;height:14px;border-radius:50%;flex:none}
.st-progress{border:2px solid #5e6ad2;border-top-color:transparent;transform:rotate(45deg)}
.lin-issue .label{font-size:11.5px;color:#8a8f98;background:rgba(255,255,255,.04);
border:1px solid rgba(255,255,255,.06);padding:2px 8px;border-radius:999px}
.lin-issue .avatars{display:flex;margin-left:auto}
.lin-issue .avatars i{width:18px;height:18px;border-radius:50%;border:2px solid #0f1011;margin-left:-6px}
</style>
```

Status variants: `.st-todo{border:2px dashed #62666d}` · `.st-done{background:#27a644;border:0}`.

**6. Cycle progress**

```html
<div class="lin-cycle"><span>Cycle 32</span><div class="bar"><i style="width:64%"></i></div><span class="dim">14 of 22</span></div>
<style>
.lin-cycle{display:flex;align-items:center;gap:10px;font-size:12.5px;color:#d0d6e0}
.lin-cycle .bar{flex:1;height:4px;border-radius:999px;background:#28282c;overflow:hidden}
.lin-cycle .bar i{display:block;height:100%;background:#5e6ad2;border-radius:999px}
.lin-cycle .dim{color:#62666d}
</style>
```

**7. View tabs with counts**

```html
<nav class="lin-tabs"><a class="on">Active <b>18</b></a><a>Backlog <b>41</b></a><a>Done</a></nav>
<style>
.lin-tabs{display:flex;gap:4px;border-bottom:1px solid rgba(255,255,255,.06)}
.lin-tabs a{padding:8px 12px;font-size:13px;color:#8a8f98;text-decoration:none;border-bottom:2px solid transparent;margin-bottom:-1px}
.lin-tabs a.on{color:#f7f8f8;border-bottom-color:#5e6ad2}
.lin-tabs b{font-weight:500;font-size:11px;background:rgba(255,255,255,.06);padding:1px 6px;border-radius:999px;margin-left:4px}
</style>
```

**8. Feature card**

```html
<div class="lin-card"><h3>Cycles</h3><p>Fixed-length sprints, handled for you.</p></div>
<style>
.lin-card{background:#0f1011;border:1px solid rgba(255,255,255,.06);border-radius:12px;padding:20px}
.lin-card h3{font-size:15px;font-weight:600;letter-spacing:-.01em;margin:0 0 6px}
.lin-card p{font-size:13.5px;color:#8a8f98;margin:0;line-height:1.55}
</style>
```

**9. Hairline divider + section label**

```html
<p class="lin-label">WHY LINEAR</p><hr class="lin-hr">
<style>
.lin-label{font-size:11.5px;font-weight:600;letter-spacing:.12em;color:#8a8f98;text-transform:uppercase}
.lin-hr{border:0;border-top:1px solid rgba(255,255,255,.06);margin:16px 0}
</style>
```

## Motion

Fast and barely noticeable: 100–200ms `ease-out` (or a soft
`cubic-bezier(.16,1,.3,1)`) on hovers, palette open, and row highlights.
No springy overshoot, no page-level animation choreography. The product
feels instant; motion just confirms the action.

## Do / Don't

- **Do** build depth with surface steps (`#08090a` → `#0f1011` → `#161718`)
  plus 1px hairline borders — **don't** reach for drop shadows on dark.
- **Do** use the accent `#5e6ad2` once per screen (brand mark, one CTA,
  focus) — **don't** paint everything lavender; restraint is the brand.
- **Do** show keyboard shortcuts as visible `kbd` chips next to actions —
  **don't** hide them in a docs page.
- **Do** lead marketing pages with a real product screenshot in a
  hairline-bordered panel — **don't** lead with abstract illustration or a
  full-bleed gradient wash.
- **Do** keep copy terse: short headlines, one-line subheads, verbs not
  adjectives — **don't** write "leverage our revolutionary AI-powered
  synergy platform."
- **Do** use the signature 510 weight and tight tracking on headlines —
  **don't** default to bold 700 with loose spacing.
- **Do** keep the glow subtle: one radial accent wash behind the hero
  visual — **don't** flood the page with a purple-to-blue gradient.
- **Do** dim the sidebar so the main content leads — **don't** give every
  column equal visual weight.

## Copy voice

Confident, terse, engineering-honest. Short declarative sentences.
No exclamation marks, no hype words.

- "Move faster. Break nothing." — hero-style headline pair.
- "Cycles keep the team in rhythm. No setup, no ceremony."
- Changelog entry: "Fixed an edge case where large attachments failed to
  upload on slow connections."
