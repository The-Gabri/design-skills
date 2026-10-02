---
name: arc-browser
description: Arc's playful, spatial browser aesthetic — sidebar-first chrome, per-space color themes, a Spotlight-style command bar, and warm, witty copy. Use for friendly productivity UIs and browser-chrome mockups.
---

# Arc Browser

The look of Arc (arc.net) by The Browser Company: the internet as a place,
not a tool. Warm, colorful, spatial — tabs live in a sidebar, every Space
has its own personality, and the browser tidies up after you.

## Principles

1. **Sidebar-first, no tab bar.** Arc deletes the horizontal tab strip
   entirely. Everything — favorites, pinned tabs, today's tabs — lives in
   a collapsible vertical sidebar on the left; the content owns the rest
   of the window.
2. **Space is a place.** Each Space is a separate sidebar with its own
   tabs, bookmarks, and theme color. Switching Spaces (click the icons
   at the bottom, or swipe) re-tints the whole window — the browser
   wears your context like a mood.
3. **The calm internet.** No clutter, no 47 open tabs. Unpinned tabs
   auto-archive out of the sidebar; favorites stay pinned at the top.
   The UI works to keep itself tidy so you don't have to.
4. **Color is a personality, not decoration.** A rainbow "Arc spectrum"
   runs through the brand, but each Space commits to one warm color.
   Gradients are used tastefully — as ambient washes, never as the whole
   identity.
5. **Command everything.** The address bar is a condensed site-name pill;
   clicking it (or pressing ⌘T / ⌘L) opens a centered, Spotlight-style
   command bar that searches tabs, actions, and the web from one input.
6. **Warm and witty copy.** The product talks like a friendly coworker:
   short, playful, a little cheeky, never corporate.

## Color

Cross-referenced from arc.net, documented Space themes, and reviews.

| Token | Hex | Role | Legend |
|---|---|---|---|
| Cream paper | `#FAF6EF` | Marketing/app canvas, warm off-white | 🟡 |
| Sidebar surface | `#F5EFE3` | Sidebar base under the Space wash | 🟡 |
| Content surface | `#FFFFFF` | Content panels, command bar body | 🟡 |
| Ink | `#231F1A` | Primary text — warm near-black | 🟡 |
| Ink soft | `#6E6459` | Secondary text, metadata | ⚠️ |
| Hairline | `rgba(35,31,26,0.10)` | Dividers, card borders | ⚠️ |
| Arc spectrum | `linear-gradient(135deg, #FF6B57, #FFB340, #7BC96F, #4D96FF, #9D7BFF)` | Brand rainbow — logo mark, one CTA at a time | ⚠️ |
| Focus coral | `#FF6B57` | Selection, active states, primary accent | 🟡 |
| Space: Coral | `#FF7A66` | Default-ish "Work" Space theme color | 🟡 |
| Space: Amber | `#FFC53D` | A bright "Personal" Space theme color | 🟡 |
| Space: Mint | `#3DDC97` | A fresh "Side project" Space theme color | 🟡 |
| Space: Sky | `#4D96FF` | A calm "Research" Space theme color | 🟡 |
| Space: Violet | `#9D7BFF` | A playful "Fun" Space theme color | 🟡 |

Rules: one Space, one color. The Space's color tints the sidebar as a
soft gradient wash (10–25% opacity over cream); text stays ink for
readability. The full rainbow spectrum appears only on brand surfaces
(logo, hero, primary CTA sheen) — never as a background flood.

## Typography

- **App chrome:** system fonts ✅ (Arc is native Swift/SwiftUI on macOS):
  `-apple-system, "SF Pro Text", "Segoe UI", system-ui, sans-serif`,
  13–15px body, 500–600 for labels. Closest web substitute is the system
  stack itself — don't force a custom face into the chrome.
- **Marketing / display:** no public brand typeface is documented ⚠️.
  The arc.net voice is a warm, rounded grotesque with personality —
  closest free substitutes: **Nunito** (rounded, friendly) or **Quicksand**.
  Headlines at 600–800, tight tracking (-0.02em), sentence case.
- **Scale:** Display 48–64px · H1 32px · H2 22–24px · Body 15–16px ·
  Caption 13px · Micro-label 11px, 600, uppercase, 0.08em tracking.
- **Numbers:** tabular figures for timestamps and counts
  (`font-variant-numeric: tabular-nums`). Monospace only for genuinely
  technical readouts (URLs in the command bar are fine in it).

## Layout & spacing

- **Base unit 8px**; steps 4 · 8 · 12 · 16 · 24 · 32 · 48 · 96.
- **The window:** fixed left sidebar 232–280px, content fluid to the
  right. No top tab bar — ever.
- **Sidebar order, top to bottom** (this order is the signature):
  1. Condensed site-name pill (opens the command bar)
  2. Favorites — a row of icon tiles pinned across Spaces
  3. Pinned tabs
  4. Today tabs (unpinned; they will auto-archive)
  5. Library: Media · Downloads · Easels & Notes · Boosts · Archived tabs
  6. Space switcher icons + "New space" — pinned at the very bottom
- **Radii are generous:** 12px buttons, 14–16px cards, 20px the command
  bar and big panels. Hairline `1px` separators instead of shadows.
- **Content breathing room:** page padding 24–32px; sidebar sections
  separated by 16–24px gaps, not boxes.
- **Responsive:** below ~768px the sidebar collapses to a hamburger /
  bottom-sheet drawer; Space icons stay visible as a horizontal strip.

## Components

Copy-pasteable HTML/CSS. Base context:
`body { background:#FAF6EF; color:#231F1A;
font-family:-apple-system,"SF Pro Text","Segoe UI",system-ui,sans-serif; }`

**1. App window with a Space-tinted sidebar**

```html
<div class="arc-window">
  <aside class="arc-sidebar" style="--space:#FF7A66">
    <div class="arc-urlpill">arc.new <span>⌘L</span></div>
    <!-- favorites, tabs… -->
  </aside>
  <main class="arc-content">…</main>
</div>
<style>
.arc-window{display:flex;height:640px;border-radius:20px;overflow:hidden;
  border:1px solid rgba(35,31,26,.1);box-shadow:0 24px 64px rgba(35,31,26,.12)}
.arc-sidebar{--space:#FF7A66;width:260px;flex:none;padding:14px 12px;
  background:linear-gradient(165deg,
    color-mix(in srgb, var(--space) 22%, #F5EFE3),
    color-mix(in srgb, var(--space) 8%, #F5EFE3));
  display:flex;flex-direction:column;gap:16px;overflow-y:auto}
.arc-content{flex:1;background:#fff;padding:32px;overflow-y:auto}
</style>
```

**2. Favorites row (pinned icon tiles)**

```html
<div class="arc-favs">
  <a class="fav" style="--c:#FF6B57">M</a>
  <a class="fav" style="--c:#4D96FF">C</a>
  <a class="fav" style="--c:#3DDC97">N</a>
  <a class="fav" style="--c:#FFC53D">Mu</a>
  <button class="fav fav-add">+</button>
</div>
<style>
.arc-favs{display:flex;gap:8px;flex-wrap:wrap}
.fav{width:40px;height:40px;border-radius:12px;display:grid;place-items:center;
  background:color-mix(in srgb, var(--c) 18%, #fff);color:#231F1A;
  font-weight:700;font-size:13px;text-decoration:none;
  border:1px solid rgba(35,31,26,.08);transition:transform .15s ease}
.fav:hover{transform:translateY(-2px) scale(1.04)}
.fav-add{background:transparent;border-style:dashed;color:#6E6459;font-size:18px;cursor:pointer}
</style>
```

**3. Tab list item (pinned + today tab)**

```html
<div class="arc-tab"><i class="dot" style="background:#FF6B57"></i><span>Trip to Lisbon — itinerary</span><button>×</button></div>
<div class="arc-tab today"><i class="dot" style="background:#4D96FF"></i><span>Sourdough starter guide</span><em>auto-archives tonight</em></div>
<style>
.arc-tab{display:flex;align-items:center;gap:10px;padding:9px 12px;border-radius:12px;
  background:rgba(255,255,255,.65);border:1px solid rgba(35,31,26,.06);
  font-size:13.5px;font-weight:500}
.arc-tab .dot{width:8px;height:8px;border-radius:50%;flex:none}
.arc-tab button{margin-left:auto;border:0;background:none;color:#6E6459;cursor:pointer;font-size:14px}
.arc-tab.today{background:transparent;border-color:transparent;font-weight:400;color:#6E6459}
.arc-tab.today em{margin-left:auto;font-style:normal;font-size:11px;color:#9a9187}
</style>
```

**4. Space switcher (bottom of sidebar)**

```html
<div class="arc-spaces">
  <button class="sp on" style="--c:#FF7A66" title="Work">W</button>
  <button class="sp" style="--c:#4D96FF" title="Research">R</button>
  <button class="sp" style="--c:#3DDC97" title="Fun">F</button>
  <button class="sp sp-new" title="New space">+</button>
</div>
<style>
.arc-spaces{margin-top:auto;display:flex;gap:8px;align-items:center;
  padding-top:12px;border-top:1px solid rgba(35,31,26,.1)}
.sp{width:38px;height:38px;border-radius:50%;border:2px solid transparent;
  background:var(--c);color:#fff;font-weight:700;font-size:13px;cursor:pointer;
  transition:transform .18s cubic-bezier(.34,1.56,.64,1)}
.sp:hover{transform:scale(1.1)}
.sp.on{border-color:#231F1A;box-shadow:0 0 0 2px rgba(255,255,255,.7)}
.sp-new{background:transparent;border:2px dashed rgba(35,31,26,.25);color:#6E6459}
</style>
```

**5. Command bar (Spotlight-style, centered)**

```html
<div class="arc-cmd">
  <input placeholder="Type a command or search…" />
  <div class="cmd-row on"><span>Go to tab — Trip to Lisbon</span><kbd>⏎</kbd></div>
  <div class="cmd-row"><span>New space</span><kbd>⌘⇧N</kbd></div>
  <div class="cmd-row"><span>Archive all today tabs</span><kbd>⌘⇧A</kbd></div>
</div>
<style>
.arc-cmd{width:min(560px,90vw);background:#fff;border-radius:20px;overflow:hidden;
  border:1px solid rgba(35,31,26,.1);box-shadow:0 32px 80px rgba(35,31,26,.22)}
.arc-cmd input{width:100%;border:0;border-bottom:1px solid rgba(35,31,26,.08);
  padding:18px 20px;font-size:16px;outline:none;background:transparent;color:#231F1A}
.cmd-row{display:flex;justify-content:space-between;align-items:center;
  padding:12px 20px;font-size:14px;color:#6E6459}
.cmd-row.on{background:color-mix(in srgb,#FF6B57 10%,#fff);color:#231F1A}
.cmd-row kbd{font:600 11px/1 system-ui;background:rgba(35,31,26,.07);
  padding:5px 8px;border-radius:6px}
</style>
```

**6. Library panel (Media · Downloads · Easels & Notes · Boosts · Archive)**

```html
<div class="arc-lib">
  <a><i style="background:#4D96FF"></i>Media<span>3</span></a>
  <a><i style="background:#3DDC97"></i>Downloads<span>2</span></a>
  <a><i style="background:#FFC53D"></i>Easels & Notes</a>
  <a><i style="background:#9D7BFF"></i>Boosts</a>
  <a><i style="background:#FF7A66"></i>Archived tabs<span>12</span></a>
</div>
<style>
.arc-lib{display:flex;flex-direction:column;gap:2px}
.arc-lib a{display:flex;align-items:center;gap:10px;padding:8px 10px;border-radius:10px;
  font-size:13px;font-weight:500;text-decoration:none;color:#231F1A}
.arc-lib a:hover{background:rgba(255,255,255,.7)}
.arc-lib i{width:22px;height:22px;border-radius:7px;flex:none}
.arc-lib span{margin-left:auto;font-size:11px;color:#9a9187;background:rgba(35,31,26,.06);
  padding:2px 7px;border-radius:999px}
</style>
```

**7. Primary CTA (tasteful spectrum)**

```html
<a class="arc-cta" href="#">Get Arc</a>
<style>
.arc-cta{display:inline-flex;align-items:center;gap:8px;padding:13px 30px;
  border-radius:14px;font-weight:700;font-size:15px;color:#231F1A;text-decoration:none;
  background:linear-gradient(120deg,#FFB340,#FF7A66 45%,#FF6B57);
  box-shadow:0 6px 20px rgba(255,107,87,.35), inset 0 1px 0 rgba(255,255,255,.4);
  transition:transform .15s ease, box-shadow .15s ease}
.arc-cta:hover{transform:translateY(-2px);box-shadow:0 10px 28px rgba(255,107,87,.45)}
</style>
```

**8. Easel card (playful whiteboard)**

```html
<div class="arc-easel">
  <svg viewBox="0 0 200 90"><path d="M10 70 C 50 10, 90 90, 130 30 S 180 60, 195 20"
    fill="none" stroke="#FF6B57" stroke-width="5" stroke-linecap="round"/></svg>
  <p>Weekend trip ideas <span>edited 2h ago</span></p>
</div>
<style>
.arc-easel{background:#fff;border:1px solid rgba(35,31,26,.1);border-radius:16px;
  padding:14px;box-shadow:0 8px 24px rgba(35,31,26,.06)}
.arc-easel svg{width:100%;height:90px;background:#FAF6EF;border-radius:10px}
.arc-easel p{font-size:13.5px;font-weight:600;margin:10px 2px 0}
.arc-easel span{display:block;font-size:11.5px;font-weight:400;color:#9a9187}
</style>
```

**9. Download row**

```html
<div class="arc-dl"><i style="background:#4D96FF"></i>
  <div><b>lisbon-itinerary.pdf</b><span>2.4 MB · done</span></div><em>✓</em></div>
<style>
.arc-dl{display:flex;align-items:center;gap:12px;padding:10px 12px;border-radius:12px;
  background:rgba(255,255,255,.65);border:1px solid rgba(35,31,26,.06)}
.arc-dl i{width:34px;height:34px;border-radius:10px;flex:none}
.arc-dl b{display:block;font-size:13px;font-weight:600}
.arc-dl span{font-size:11.5px;color:#9a9187}
.arc-dl em{margin-left:auto;font-style:normal;color:#3DDC97;font-weight:700}
</style>
```

**10. Auto-archive notice (the calm-internet signature)**

```html
<p class="arc-tidy">4 tabs auto-archived today — your sidebar stays tidy.</p>
<style>
.arc-tidy{font-size:12.5px;color:#6E6459;background:rgba(61,220,151,.12);
  border:1px dashed rgba(61,220,151,.5);border-radius:12px;padding:10px 14px}
</style>
```

## Motion

No published spec ⚠️ — match the playful feel: gentle overshoot springs
(`cubic-bezier(.34,1.4,.4,1)`, 200–350ms) on Space switches, palette open,
and hover lifts; snappy 120ms `ease-out` on tabs and buttons. Motion
should feel bouncy and alive, never mechanical — like flipping between
rooms, not switching settings.

## Do / Don't

- **Do** put the Space switcher at the very bottom of the sidebar with
  one color per Space — **don't** center a generic settings icon there.
- **Do** tint the whole sidebar with the active Space's color wash —
  **don't** leave the sidebar neutral and only color a tiny dot.
- **Do** write the condensed address bar as a site-name pill that opens
  the command bar — **don't** draw a full Chrome-style URL omnibox.
- **Do** auto-archive unpinned tabs and say so proudly ("4 tabs archived
  today") — **don't** let tab lists grow into infinite clutter.
- **Do** use the rainbow spectrum sparingly (logo mark, one CTA sheen) —
  **don't** flood backgrounds with a full purple-to-blue gradient wash.
- **Do** keep corners round (12–20px) and dividers hairline-thin —
  **don't** use sharp corners or heavy drop shadows.
- **Do** copy Arc's voice: "Space for the different sides of you." —
  **don't** write "Leverage our revolutionary synergy platform."
- **Do** make the command bar float centered with big padding and
  visible shortcuts — **don't** anchor search to a corner.

## Copy voice

Warm, witty, a little cheeky — like a friend who keeps your desk clean.
Short sentences, sentence case, zero corporate filler.

- "Space for the different sides of you." ✅ (arc.net)
- "Tabs? Archived. Brain? Uncluttered."
- "This is the calm corner of your internet."
- Command bar empty state: "Type a command or search — your tabs are
  already tidy."
