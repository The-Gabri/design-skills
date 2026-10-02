---
name: mantine
description: Mantine's clean, feature-rich React UI style — use for admin dashboards, app chrome, and data-dense web apps with blue #228be6 primary.
---

# Mantine

The look of Mantine (mantine.dev): a pragmatic, developer-first React component
library. Clean light surfaces, hairline dividers, a calm blue primary, and
dense app chrome (AppShell + NavLinks) rather than marketing flair. Components
ship with sensible defaults so interfaces look assembled, not decorated.

## Principles

1. **Feature-rich, opinionated defaults.** Every component arrives with the
   right answer (radius `md`, blue filled buttons, labeled inputs) so a page
   reads as finished with zero customization.
2. **App chrome first.** The signature layout is an application shell — header,
   sidebar, main — not a hero banner. Mantine pages look like tools, not ads.
3. **Color as function.** Color variants (`filled`, `light`, `outline`,
   `subtle`) encode hierarchy and state; each theme color ships as a 10-shade
   palette (0 light → 9 dark) so any hue resolves to background, tint, and text.
4. **Calm density.** Data-dense tables, tabs, and accordions with generous
   whitespace between groups; hairline borders and soft shadows create depth,
   never heavy panels.
5. **Accessible by default.** `:focus-visible` rings in the primary color,
   labeled inputs with error states, and `prefers-reduced-motion` respected.

## Color

Mantine's default theme uses open-color (plus additions) — 10 shades per
color, index 0 (lightest) → 9 (darkest). `primaryColor` is `blue`,
`primaryShade` is `{ light: 6, dark: 8 }`, so the default primary is blue.6.

| Token | Hex | Role | Legend |
|---|---|---|---|
| Blue 0 | `#e7f5ff` | Lightest tint — light-variant backgrounds | ✅ |
| Blue 1 | `#d0ebff` | Light-variant badge/tag backgrounds | ✅ |
| Blue 2 | `#a5d8ff` | | ✅ |
| Blue 3 | `#74c0fc` | | ✅ |
| Blue 4 | `#4dabf7` | | ✅ |
| Blue 5 | `#339af0` | | ✅ |
| Blue 6 | `#228be6` | **Default primary** — filled buttons, links, focus rings | ✅ |
| Blue 7 | `#1c7ed6` | Primary hover | ✅ |
| Blue 8 | `#1971c2` | Primary in dark color scheme | ✅ |
| Blue 9 | `#1864ab` | Darkest blue | ✅ |
| Gray 0 | `#f8f9fa` | App background tint, striped table rows | ✅ |
| Gray 1 | `#f1f3f5` | Navbar/sidebar background | ✅ |
| Gray 2 | `#e9ecef` | Hairline borders, dividers | ✅ |
| Gray 4 | `#ced4da` | Input borders | ✅ |
| Gray 6 | `#868e96` | Placeholder, dimmed text | ✅ |
| Gray 7 | `#495057` | Secondary text | ✅ |
| Gray 9 | `#212529` | Body text (near-black) | ✅ |
| Red 6 | `#fa5252` | Error, destructive actions | ✅ |
| Green 6 | `#37b24d` | Success | ✅ |
| Yellow 6 | `#f59f00` | Warning | ✅ |
| Pink 6 | `#d6336c` | Accent alternative | ✅ |
| Grape 6 | `#be4bdb` | Accent alternative | ✅ |
| Violet 6 | `#7950f2` | Accent alternative | ✅ |
| Indigo 6 | `#4c6ef5` | Accent alternative | ✅ |
| Cyan 6 | `#1098ad` | Accent alternative | ✅ |
| Teal 6 | `#0ca678` | Accent alternative | ✅ |
| Lime 6 | `#74b816` | Accent alternative | ✅ |
| Orange 6 | `#f76707` | Accent alternative | ✅ |
| Body | `#ffffff` | Light-mode canvas | ✅ |
| Text | `#212529` | Default body text on white | ✅ |
| Dark body | `#1a1b1e` | Dark-mode canvas (dark.8) | 🟡 |

Variant color rules (documented): `filled` = shade 6 background + white text;
`light` = light tint background + dark text of the same hue; `outline` =
colored border + colored text on transparent; hover on filled darkens the
background ~10% (e.g. `#228be6` → `#1c7ed6`).

**Dark color scheme** 🟡: body `#1a1b1e` (dark.8), surfaces dark.6
(`#25262b`), hairlines dark.4 (`#373a40`), text dark.0 (`#c1c2c5`).
`primaryShade` flips to 8 in dark mode, so filled buttons render blue.8
(`#1971c2`). `light`-variant tints become translucent overlays with a
lighter shade for text (e.g. blue → `rgba(34,139,230,.16)` background with
blue.3 `#74c0fc` text).

## Typography

- **Face:** system stack — `-apple-system, BlinkMacSystemFont, "Segoe UI",
  Roboto, Helvetica, Arial, sans-serif, "Apple Color Emoji",
  "Segoe UI Emoji"` ✅ (Mantine's documented default `fontFamily`).
- **Monospace:** `"JetBrains Mono", "SFMono-Regular", Menlo, Consolas,
  "Liberation Mono", "Courier New", monospace` 🟡.
- **Weights:** regular 400, medium 600, bold 700 ✅ (`theme.fontWeights`);
  headings default to bold. (In Mantine v8 the medium default changed to
  500 🟡; the skill uses the long-stable v7 values.)
- **Scale:** body text 14–16px; `Title` order 1–6 for headings (h1 ~34px,
  h2 ~26px, h3 ~22px), `Text` component with `size` xs–xl for everything
  else. Badges and table headers run small and uppercase.
- **Rules:** left-aligned, terse UI labels; sentence case for buttons
  ("Save changes", not "SAVE CHANGES") except badges, which are uppercase.

## Layout & spacing

- **AppShell anatomy** ✅: fixed `Header` (height 60px) + `Navbar`
  (width 300px, collapses below the `sm` breakpoint) + `Main` content with
  `padding="md"`. Optional `Aside` (right) and `Footer` (height 60px).
- **Breakpoints** ✅ (Bootstrap-derived): xs 576px · sm 768px · md 992px ·
  lg 1200px · xl 1408px.
- **Spacing scale** ✅ (px, rem-converted): xs 10 · sm 12 · md 16 · lg 20 ·
  xl 32.
- **Radius scale** ✅: xs 2px · sm 4px · md 8px · lg 16px · xl 32px;
  `defaultRadius` is `md` (8px) — inputs, buttons, cards, and modals are
  rounded-8 by default, never pill-shaped. Exception: `Badge` defaults to
  `radius="xl"` (fully pill-shaped).
- **Borders:** 1px hairlines in gray.2 (`#e9ecef`); `withBorder` adds the
  same line around cards and tables. 🟡
- **Shadows:** soft multi-layer, scale xs–xl; e.g. modal/dropdown level is a
  diffuse gray shadow, never a hard offset. 🟡
- **Focus ring:** `:focus-visible` 2px solid outline in the primary color
  with 2px offset. 🟡

## Components

Tokens used below: `--blue-6: #228be6; --blue-7: #1c7ed6; --blue-0: #e7f5ff;
--blue-9: #1864ab; --gray-0..2: #f8f9fa/#f1f3f5/#e9ecef; --gray-4: #ced4da;
--gray-6: #868e96; --gray-9: #212529; --red-6: #fa5252; --green-6: #37b24d.`

### 1. Button

Default: `variant="filled"`, `size="sm"` (36px tall), `radius="md"`,
font-weight 600. Other variants: `light`, `outline`, `default`, `subtle`,
`white`, `transparent`, `gradient` ✅ (variant list documented).

```html
<button class="mt-btn">Save changes</button>
<button class="mt-btn mt-btn-light">Cancel</button>
<button class="mt-btn mt-btn-outline">Export</button>

<style>
.mt-btn {
  height: 36px; padding: 0 18px; border: 0; border-radius: 8px;
  background: #228be6; color: #fff;
  font: 600 14px/1 -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif;
  cursor: pointer; transition: background 120ms ease;
}
.mt-btn:hover { background: #1c7ed6; }
.mt-btn:focus-visible { outline: 2px solid #228be6; outline-offset: 2px; }
.mt-btn-light { background: #e7f5ff; color: #1864ab; }
.mt-btn-light:hover { background: #d0ebff; }
.mt-btn-outline { background: transparent; color: #228be6; border: 1px solid #228be6; }
.mt-btn-outline:hover { background: #e7f5ff; }
</style>
```

### 2. AppShell

Header 60px, Navbar 300px, Main padded. The classic Mantine application
chrome ✅ (structure from official docs examples).

```html
<div class="mt-shell">
  <header class="mt-header">
    <button class="mt-burger" aria-label="Toggle navigation"><span></span><span></span><span></span></button>
    <strong>Relay</strong>
  </header>
  <aside class="mt-navbar">
    <a class="mt-navlink is-active" href="#">Dashboard</a>
    <a class="mt-navlink" href="#">Projects</a>
    <a class="mt-navlink" href="#">Team</a>
    <a class="mt-navlink" href="#">Settings</a>
  </aside>
  <main class="mt-main"><!-- page content --></main>
</div>

<style>
.mt-shell { display: grid; grid-template-columns: 300px 1fr;
  grid-template-rows: 60px 1fr; grid-template-areas: "header header" "navbar main";
  min-height: 100vh; }
.mt-header { grid-area: header; display: flex; align-items: center; gap: 12px;
  padding: 0 16px; border-bottom: 1px solid #e9ecef; background: #fff;
  position: sticky; top: 0; z-index: 10; }
.mt-navbar { grid-area: navbar; background: #f8f9fa; padding: 16px 12px;
  border-right: 1px solid #e9ecef; }
.mt-main { grid-area: main; padding: 16px 24px; }
.mt-navlink { display: block; padding: 8px 12px; border-radius: 8px;
  color: #495057; font-size: 14px; font-weight: 500; text-decoration: none; }
.mt-navlink:hover { background: #f1f3f5; }
.mt-navlink.is-active { background: #e7f5ff; color: #1864ab; font-weight: 600; }
.mt-burger { display: none; background: none; border: 0; cursor: pointer; }
@media (max-width: 768px) {
  .mt-shell { grid-template-columns: 1fr; grid-template-areas: "header" "main"; }
  .mt-navbar { display: none; }
  .mt-burger { display: block; }
}
</style>
```

### 3. Table

No vertical borders; horizontal hairline row dividers; `striped` tints even
rows gray.0; `highlightOnHover` deepens hover rows. Small semibold header.

```html
<table class="mt-table mt-table-striped mt-table-hover">
  <thead><tr><th>Name</th><th>Status</th><th>Owner</th></tr></thead>
  <tbody>
    <tr><td>Website redesign</td><td><span class="mt-badge">In progress</span></td><td>Mara</td></tr>
    <tr><td>Mobile app</td><td><span class="mt-badge mt-badge-green">Done</span></td><td>Dev</td></tr>
  </tbody>
</table>

<style>
.mt-table { width: 100%; border-collapse: collapse; font-size: 14px; }
.mt-table th { text-align: left; font-size: 12px; font-weight: 700; color: #495057;
  padding: 8px 12px; border-bottom: 1px solid #e9ecef; }
.mt-table td { padding: 12px; border-bottom: 1px solid #e9ecef; color: #212529; }
.mt-table-striped tbody tr:nth-child(even) { background: #f8f9fa; }
.mt-table-hover tbody tr:hover { background: #f1f3f5; }
</style>
```

### 4. Modal

Centered card, radius `md`, large soft shadow, dimmed overlay
(`rgba(0,0,0,.55)`), header with title + close X. 🟡

```html
<div class="mt-modal-overlay" hidden>
  <div class="mt-modal" role="dialog" aria-modal="true">
    <div class="mt-modal-head"><h3>New project</h3><button class="mt-modal-x" aria-label="Close">✕</button></div>
    <div class="mt-modal-body"><!-- form --></div>
  </div>
</div>

<style>
.mt-modal-overlay { position: fixed; inset: 0; background: rgba(0,0,0,.55);
  display: flex; align-items: center; justify-content: center; padding: 16px; z-index: 100; }
.mt-modal { background: #fff; border-radius: 8px; width: 480px; max-width: 100%;
  box-shadow: 0 12px 40px rgba(0,0,0,.18); padding: 24px;
  animation: mt-pop 180ms ease; }
.mt-modal-head { display: flex; justify-content: space-between; align-items: center; margin-bottom: 16px; }
.mt-modal-head h3 { margin: 0; font-size: 18px; font-weight: 700; }
.mt-modal-x { background: none; border: 0; color: #868e96; font-size: 16px; cursor: pointer;
  border-radius: 4px; padding: 4px 8px; }
.mt-modal-x:hover { background: #f1f3f5; color: #212529; }
@keyframes mt-pop { from { transform: scale(.96); opacity: 0; } }
</style>
```

### 5. Notifications

Stack anchored bottom-right (default position 🟡). Each notification: white
card, radius md, colored icon chip, bold title + message, close button,
auto-dismiss. Triggered imperatively (`notifications.show({ title, message,
color })`).

```html
<div class="mt-notifs">
  <div class="mt-notif">
    <span class="mt-notif-icon" style="background:#e7f5ff;color:#228be6">i</span>
    <div><strong>Deploy finished</strong><p>relay-web v2.4.1 is live.</p></div>
    <button aria-label="Dismiss">✕</button>
  </div>
</div>

<style>
.mt-notifs { position: fixed; right: 16px; bottom: 16px; display: flex;
  flex-direction: column; gap: 8px; z-index: 200; max-width: 360px; }
.mt-notif { display: flex; gap: 12px; align-items: flex-start; background: #fff;
  border: 1px solid #e9ecef; border-radius: 8px; padding: 12px 16px;
  box-shadow: 0 8px 24px rgba(0,0,0,.12); animation: mt-slide 160ms ease; }
.mt-notif-icon { width: 28px; height: 28px; border-radius: 50%; flex: none;
  display: grid; place-items: center; font-weight: 700; font-size: 14px; }
.mt-notif strong { display: block; font-size: 14px; }
.mt-notif p { margin: 2px 0 0; font-size: 13px; color: #495057; }
.mt-notif button { margin-left: auto; background: none; border: 0; color: #868e96; cursor: pointer; }
@keyframes mt-slide { from { transform: translateY(8px); opacity: 0; } }
</style>
```

### 6. Tabs

Default variant: tab list over a bottom hairline; active tab gets a 2px
primary underline and primary text. `pills` variant is the common
alternative. 🟡

```html
<div class="mt-tabs">
  <div class="mt-tablist" role="tablist">
    <button class="mt-tab is-active" role="tab">Active</button>
    <button class="mt-tab" role="tab">Archived</button>
    <button class="mt-tab" role="tab">Templates</button>
  </div>
</div>

<style>
.mt-tablist { display: flex; gap: 4px; border-bottom: 1px solid #e9ecef; }
.mt-tab { background: none; border: 0; border-bottom: 2px solid transparent;
  margin-bottom: -1px; padding: 10px 14px; font-size: 14px; font-weight: 500;
  color: #495057; cursor: pointer; }
.mt-tab:hover { color: #212529; }
.mt-tab.is-active { color: #228be6; border-bottom-color: #228be6; font-weight: 600; }
</style>
```

### 7. Accordion

Default variant: items separated by top hairlines, label left, chevron right
that rotates 180° when open. `separated`/`contained` variants box each item. 🟡

```html
<div class="mt-acc">
  <div class="mt-acc-item">
    <button class="mt-acc-control" aria-expanded="false">
      How do I invite teammates?
      <svg class="mt-acc-chev" width="16" height="16" viewBox="0 0 16 16"><path d="M4 6l4 4 4-4" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round"/></svg>
    </button>
    <div class="mt-acc-panel" hidden>Open Settings → Members and send an invite link…</div>
  </div>
</div>

<style>
.mt-acc-item { border-top: 1px solid #e9ecef; }
.mt-acc-item:last-child { border-bottom: 1px solid #e9ecef; }
.mt-acc-control { width: 100%; display: flex; justify-content: space-between; align-items: center;
  background: none; border: 0; padding: 14px 8px; font-size: 15px; font-weight: 500;
  color: #212529; cursor: pointer; text-align: left; }
.mt-acc-control:hover { background: #f8f9fa; }
.mt-acc-chev { color: #868e96; transition: transform 200ms ease; }
.mt-acc-control[aria-expanded="true"] .mt-acc-chev { transform: rotate(180deg); color: #228be6; }
.mt-acc-panel { padding: 0 8px 16px; font-size: 14px; color: #495057; }
</style>
```

### 8. Badge

Uppercase, letterspaced, small. Default variant is `light` (tint background,
dark text of the same hue); `filled` for high emphasis. 🟡

```html
<span class="mt-badge">In progress</span>
<span class="mt-badge mt-badge-green">Deployed</span>
<span class="mt-badge mt-badge-red">Overdue</span>
<span class="mt-badge mt-badge-gray">Template</span>

<style>
.mt-badge { display: inline-block; font-size: 11px; font-weight: 700;
  text-transform: uppercase; letter-spacing: .06em; padding: 4px 10px;
  border-radius: 999px; background: #e7f5ff; color: #1864ab; }
.mt-badge-green { background: #ebfbee; color: #2b8a3e; }
.mt-badge-red { background: #ffe3e3; color: #c92a2a; }
.mt-badge-gray { background: #f1f3f5; color: #495057; }
</style>
```

Note: `Badge` is the one component whose default radius is `xl` (pill),
not `md` — square badges read as a different library.

### 9. Input (TextInput)

Label above (14px, weight 500), input 36px tall, 1px gray.4 border, radius
`md`; focus swaps border to primary with the focus ring; error state turns
border/message red. 🟡

```html
<label class="mt-field">
  <span class="mt-label">Project name</span>
  <input class="mt-input" type="text" placeholder="e.g. Website redesign">
  <span class="mt-error" hidden>Name is required</span>
</label>

<style>
.mt-label { display: block; font-size: 14px; font-weight: 500; margin-bottom: 4px; color: #212529; }
.mt-input { width: 100%; height: 36px; padding: 0 12px; font-size: 14px;
  border: 1px solid #ced4da; border-radius: 8px; color: #212529; }
.mt-input::placeholder { color: #868e96; }
.mt-input:focus { outline: none; border-color: #228be6;
  box-shadow: 0 0 0 2px rgba(34,139,230,.25); }
.mt-field.has-error .mt-input { border-color: #fa5252; }
.mt-error { display: block; font-size: 12px; color: #fa5252; margin-top: 4px; }
</style>
```

## Motion

Mantine defines no branded motion language — one line: transitions are
short and functional (100–200ms `ease`; modal/popover enter with a subtle
scale .96→1 + fade 🟡), and `respectReducedMotion` defaults to `true`,
honoring `prefers-reduced-motion` ✅.

## Do / Don't

- **Do** lead with a blue.6 (`#228be6`) filled button as the single primary
  action; secondary actions get `light` or `outline` variants.
- **Do** build pages as AppShell chrome — header + 300px navbar with
  light-tint active NavLinks — not as centered marketing heroes.
- **Do** uppercase badges and keep them small; pair `light`-variant status
  badges with `striped` + `highlightOnHover` tables.
- **Do** put notifications bottom-right with a title, a message, and a
  severity color; dismiss them automatically.
- **Don't** reach for gradients or glow — Mantine's only sanctioned gradient
  is the explicit `variant="gradient"` button, and it is rarely used.
- **Don't** make buttons or inputs pill-shaped; the default radius is 8px
  (`md`), and fully-rounded controls read as a different library.
- **Don't** invent palette values — every color must come from a 10-shade
  scale (0 light → 9 dark); if you only have one hex, generate the scale
  first (mantine.dev/colors-generator).
- **Don't** drop the focus ring; keyboard-visible `:focus-visible` outlines
  in the primary color are part of the look, not an afterthought.

## Copy voice

Pragmatic developer docs voice: terse, imperative, code-first. State what
the thing does, then show it.

- "Notifications are used to display ephemeral messages. They are
  positioned in the bottom right corner by default."
- "Use `striped` and `highlightOnHover` to make dense tables scannable."
- "The `color` prop supports any key of `theme.colors`, for example
  `blue` or `blue.6`."
