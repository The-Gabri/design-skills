---
name: atlassian-ds
description: Build UI that looks and feels like Atlassian products (Jira, Confluence, Trello) — dense teamwork interfaces with status lozenges, avatar stacks, and honest, plain-spoken copy.
---

# Atlassian Design System (atlassian-ds)

The design language behind Jira, Confluence, Trello, and Bitbucket: dense, no-nonsense
teamwork software. Nothing decorative — every pixel exists so a team can move work forward.
When in doubt, it should look like it belongs next to a Jira board.

## Principles

1. **Don't make me think.** Interfaces should be immediately scannable: hierarchy, status,
   and the next action are obvious at a glance. (Stated Atlassian design principle.)
2. **Teams first.** The unit of design is a team doing work together — assignees, watchers,
   comments, shared boards. Collaboration chrome (avatars, mentions, activity) is core, not garnish.
3. **Clarity over decoration.** No marketing gloss inside the product. Color carries meaning
   (status, semantics), never just vibes.
4. **Consistent across the ecosystem.** Jira, Confluence, and Trello feel like one family:
   the same tokens, the same buttons, the same spacing. When you borrow the style, borrow
   the whole system — don't mix it with foreign patterns.
5. **Helpful, not clever.** Copy and UI explain themselves in plain language. If an empty
   state, error, or button needs interpretation, it's a design failure.

## Color

Legend: ✅ official/documented · 🟡 cross-referenced · ⚠️ community approximation.

Atlassian colors are semantic: choose the **role** (brand, information, success, warning,
danger, discovery, neutral, accent), then the emphasis. Accent colors must never carry
semantic meaning — swapping one accent for another must change nothing about the experience. ✅

Light theme, core tokens (hex values, light mode):

| Token / role | Hex | Use |
|---|---|---|
| Blue/700 — brand ✅ | `#0C66E4` | Primary buttons, links, active states |
| Blue/700 hover 🟡 | `#0055CC` | Primary button hover |
| Blue/700 pressed 🟡 | `#09326C` | Primary button pressed |
| Blue/100 🟡 | `#DEEBFF` | Information lozenge / banner backgrounds |
| Blue (text on light blue) 🟡 | `#0747A6` | Information lozenge text |
| Neutral/1100 — text ✅ | `#172B4D` | Default body text |
| Neutral/700 — text.subtle 🟡 | `#44546F` | Secondary text |
| Neutral/600 — text.subtlest 🟡 | `#626F86` | Hints, metadata, timestamps |
| Neutral/100 🟡 | `#F1F2F4` | Sunken surfaces, default button bg |
| Neutral/200 🟡 | `#DFE1E6` | Borders, neutral lozenge bg |
| Neutral/0 ✅ | `#FFFFFF` | Page/card surface |
| Green/700 🟡 | `#1F8455` | Success: done states, confirmations |
| Green/100 🟡 | `#E3FCEF` | Success lozenge/banner background |
| Green (text on light green) 🟡 | `#006644` | Success lozenge text |
| Red/700 🟡 | `#C9372C` | Danger: errors, destructive actions |
| Red/100 🟡 | `#FFEDEB` | Danger lozenge/banner background |
| Yellow/700 🟡 | `#946F00` | Warning: caution, at-risk |
| Yellow/100 🟡 | `#FFF7D6` | Warning lozenge/banner background |
| Purple/700 🟡 | `#6E5DC6` | Discovery: new, beta, onboarding |
| Purple/100 🟡 | `#F3F0FF` | Discovery lozenge/banner background |
| Blanket overlay 🟡 | `rgba(9, 30, 66, 0.54)` | Modal/dialog scrim |

Jira-style issue status pairings (🟡 cross-referenced):

| Status | Background | Text |
|---|---|---|
| To do | `#DFE1E6` | `#42526E` |
| In progress | `#DEEBFF` | `#0747A6` |
| In review | `#EAE6FF` | `#403294` |
| Done | `#E3FCEF` | `#006644` |
| Blocked | `#FFEBE6` | `#BF2600` |

Do: use the tinted background + dark text pairings above for status lozenges.
Don't: use pure saturated hues (e.g. `#FF0000`) or gradient backgrounds — Atlassian
status is always a soft tint with legible dark text.

## Typography

Legend: ✅ official/documented · 🟡 cross-referenced · ⚠️ community approximation.

App font: **Atlassian Sans** ✅ (marketing/brand uses Charlie Sans; in-app is always
Atlassian Sans or Atlassian Mono for code). Where Atlassian Sans isn't licensed for the
web, fall back to the official stack: ✅

```css
font-family: "Atlassian Sans", -apple-system, BlinkMacSystemFont, "Segoe UI",
  "Roboto", "Helvetica Neue", Arial, sans-serif;
```

Type scale (official tokens, ✅):

| Token | Size | Line height | Weight | Use |
|---|---|---|---|---|
| `font.heading.xxlarge` | 32px | 36px | Bold | Marketing-size headings |
| `font.heading.xlarge` | 28px | 32px | Bold | — |
| `font.heading.large` | 24px | 28px | Bold | Page titles (forms, dialogs) |
| `font.heading.medium` | 20px | 24px | Bold | Modal titles, large component titles |
| `font.heading.small` | 16px | 20px | Bold | Card titles, section heads |
| `font.heading.xsmall` | 14px | 20px | Bold | Small component titles |
| `font.heading.xxsmall` | 12px | 16px | Bold | Fine print headings |
| `font.body.large` | 16px | 24px | Regular | Long-form reading (Confluence) |
| `font.body` | 14px | 20px | Regular | **Default UI text — most of Jira lives here** |
| `font.body.small` | 12px | 16px | Regular | Metadata, timestamps, fine print |
| `font.code` | 12px | 20px | Regular | Code blocks (Atlassian Mono) |

Weights: Regular 400 for prose, Medium 500 for text that sits beside icons and for
button labels, Bold 700 for headings — and **only** headings and lozenge text. ✅

Rules: one `<h1>` per page (usually the page title); never skip heading levels (no
h2 → h4); prefer a real heading style over just bolding body text. ✅

## Layout & spacing

Legend: ✅ official/documented · 🟡 cross-referenced.

- **Base unit is 8px.** Every space token is a percentage of it: `space.100` = 8px,
  `space.200` = 16px, `space.150` = 12px, `space.300` = 24px, `space.400` = 32px,
  `space.600` = 48px. Suffix = percent of base. ✅
- **Radius:** `border.radius.050` = 2px (lozenges, chips) · `border.radius.100` = 3px
  (buttons, inputs) · `border.radius.200` = 8px (cards, panels) · `border.radius.300` =
  12px (modals) · `border.radius.circle` = 50% (avatars). 🟡
- **Borders:** 1px solid Neutral/200 (`#DFE1E6`) for card/field outlines; no heavy
  borders anywhere. Jira cards are flat white with a 1px border, not big shadows. 🟡
- **Elevation (shadows), subtle by default** 🟡:
  - Raised (cards, dropdown triggers): `0 1px 1px rgba(9,30,66,.25), 0 0 1px rgba(9,30,66,.31)`
  - Overflow (menus, tooltips): `0 4px 8px rgba(9,30,66,.08), 0 0 1px rgba(9,30,66,.31)`
  - Overlay (modals, dialogs): `0 8px 12px rgba(9,30,66,.15), 0 0 1px rgba(9,30,66,.31)`
- **Density:** app chrome is compact — 14px body text, 32px default buttons, 24px
  compact buttons, table rows ~40px. Group related items close (8px), separate groups
  wider (16–24px): proximity carries meaning. ✅

## Components

### 1. Button

Appearances: `primary` → `default` → `subtle` → `link` → `danger`. 🟡
Height 32px default, 24px compact; radius 3px; 14px / 500 label.

```html
<button class="ads-btn ads-btn-primary">Create</button>
<button class="ads-btn ads-btn-default">Cancel</button>
<button class="ads-btn ads-btn-subtle">Learn more</button>
<button class="ads-btn ads-btn-link">View details</button>
<button class="ads-btn ads-btn-danger">Delete</button>
<button class="ads-btn ads-btn-primary ads-btn-compact">Filter</button>
```

```css
.ads-btn {
  font: 500 14px/1 -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif;
  height: 32px; padding: 0 12px; border-radius: 3px; border: 0; cursor: pointer;
  transition: background 50ms cubic-bezier(0.4, 1, 0.6, 1);
}
.ads-btn-primary { background: #0C66E4; color: #fff; }
.ads-btn-primary:hover { background: #0055CC; }
.ads-btn-primary:active { background: #09326C; }
.ads-btn-default { background: #F1F2F4; color: #172B4D; }
.ads-btn-default:hover { background: #E9EBF0; }
.ads-btn-subtle { background: transparent; color: #172B4D; }
.ads-btn-subtle:hover { background: #F1F2F4; }
.ads-btn-link { background: transparent; color: #0C66E4; height: auto; padding: 0; }
.ads-btn-link:hover { text-decoration: underline; }
.ads-btn-danger { background: #CA3521; color: #fff; }
.ads-btn-danger:hover { background: #AE2E24; }
.ads-btn-compact { height: 24px; padding: 0 8px; font-size: 12px; }
.ads-btn:disabled { background: #F1F2F4; color: #8590A2; cursor: not-allowed; }
```

### 2. Lozenge (status badge)

The single most recognizable Atlassian element. Uppercase, 11px, weight 700,
radius 3px (2–3px), default height ~24px (spacious: 32px). 🟡
Appearances: `neutral`, `information`, `success`, `warning`, `danger`, `discovery`,
plus accent colors for non-semantic labels (gray, red, orange, yellow, lime, green,
teal, blue, purple, magenta). Max width 200px; truncate with ellipsis, don't wrap.

```html
<span class="ads-lozenge ads-loz-information">In progress</span>
<span class="ads-lozenge ads-loz-success">Done</span>
<span class="ads-lozenge ads-loz-warning">At risk</span>
<span class="ads-lozenge ads-loz-danger">Blocked</span>
<span class="ads-lozenge ads-loz-discovery">New</span>
<span class="ads-lozenge ads-loz-neutral">Draft</span>
```

```css
.ads-lozenge {
  display: inline-block; max-width: 200px; overflow: hidden; white-space: nowrap;
  text-overflow: ellipsis; text-transform: uppercase;
  font: 700 11px/1 -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif;
  padding: 6px 8px; border-radius: 3px;
}
.ads-loz-neutral     { background: #F1F2F4; color: #44546F; }
.ads-loz-information { background: #DEEBFF; color: #0747A6; }
.ads-loz-success     { background: #E3FCEF; color: #006644; }
.ads-loz-warning     { background: #FFF7D6; color: #946F00; }
.ads-loz-danger      { background: #FFEDEB; color: #C9372C; }
.ads-loz-discovery   { background: #F3F0FF; color: #6E5DC6; }
```

### 3. Section message

Full-width informational banner with icon, bold title, and body text. Icon color
matches the role. Background is the role's lightest tint. ✅ (usage), 🟡 (exact hex)

```html
<div class="ads-section-msg ads-sm-info" role="status">
  <svg class="ads-sm-icon" viewBox="0 0 16 16" width="24" height="24" aria-hidden="true">
    <circle cx="8" cy="8" r="7" fill="none" stroke="currentColor" stroke-width="2"/>
    <path d="M8 7v4" stroke="currentColor" stroke-width="2" stroke-linecap="round"/>
    <circle cx="8" cy="4.5" r="1.2" fill="currentColor"/>
  </svg>
  <div>
    <p class="ads-sm-title">Board filters have moved</p>
    <p class="ads-sm-body">You can now save filter combinations as views and share them with your team.</p>
  </div>
</div>
```

```css
.ads-section-msg { display: flex; gap: 12px; align-items: flex-start;
  padding: 16px; border-radius: 8px; }
.ads-sm-title { font: 600 16px/20px -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif;
  margin: 0 0 4px; color: #172B4D; }
.ads-sm-body { font: 400 14px/20px -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif;
  margin: 0; color: #44546F; }
.ads-sm-icon { flex: none; margin-top: 2px; }
.ads-sm-info { background: #DEEBFF; } .ads-sm-info .ads-sm-icon { color: #0C66E4; }
.ads-sm-success { background: #DFFCF0; } .ads-sm-success .ads-sm-icon { color: #1F8455; }
.ads-sm-warning { background: #FFF7D6; } .ads-sm-warning .ads-sm-icon { color: #946F00; }
.ads-sm-error { background: #FFEDEB; } .ads-sm-error .ads-sm-icon { color: #C9372C; }
```

### 4. Avatar stack

Overlapping 24px (or 32px) circles, 2px white ring, overflow shown as "+N" gray
circle. Always represents people — assignees, watchers, commenters.

```html
<div class="ads-avatars">
  <span class="ads-avatar" style="--c:#6E5DC6" title="Maya Chen">MC</span>
  <span class="ads-avatar" style="--c:#1F8455" title="Jonas Berg">JB</span>
  <span class="ads-avatar" style="--c:#C9372C" title="Aisha Khan">AK</span>
  <span class="ads-avatar ads-avatar-more">+4</span>
</div>
```

```css
.ads-avatars { display: inline-flex; }
.ads-avatar {
  width: 24px; height: 24px; border-radius: 50%; flex: none;
  display: inline-flex; align-items: center; justify-content: center;
  font: 700 10px/1 -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif;
  background: var(--c, #626F86); color: #fff;
  border: 2px solid #fff; margin-left: -6px;
}
.ads-avatar:first-child { margin-left: 0; }
.ads-avatar-more { background: #DFE1E6; color: #42526E; }
```

### 5. Breadcrumbs

Chevron-separated, 14px, links are Blue/700 with underline on hover only; the
current page is plain dark text, not a link. ✅ (behavior), 🟡 (exact metrics)

```html
<nav class="ads-crumbs" aria-label="Breadcrumb">
  <a href="#">Projects</a><span aria-hidden="true">›</span>
  <a href="#">Sunrise (SUN)</a><span aria-hidden="true">›</span>
  <span aria-current="page">Board</span>
</nav>
```

```css
.ads-crumbs { display: flex; align-items: center; gap: 8px; font-size: 14px; }
.ads-crumbs a { color: #0C66E4; text-decoration: none; }
.ads-crumbs a:hover { text-decoration: underline; }
.ads-crumbs span[aria-hidden] { color: #626F86; }
.ads-crumbs [aria-current] { color: #172B4D; }
```

### 6. Inline dialog

A small popover card anchored to a trigger: white surface, 8px radius, overlay
shadow, optional heading + body + actions. 🟡

```html
<button class="ads-btn ads-btn-subtle" id="dlg-trigger">Why is this blocked?</button>
<div class="ads-inline-dialog" id="dlg" role="dialog" aria-label="Blocked reason">
  <p class="ads-inline-dialog-title">Blocked by SUN-1042</p>
  <p class="ads-inline-dialog-body">Waiting on the API contract from the platform team. Expected Thursday.</p>
  <div class="ads-inline-dialog-actions">
    <button class="ads-btn ads-btn-primary ads-btn-compact">View issue</button>
    <button class="ads-btn ads-btn-subtle ads-btn-compact">Dismiss</button>
  </div>
</div>
```

```css
.ads-inline-dialog {
  background: #fff; border-radius: 8px; padding: 16px; width: 280px;
  box-shadow: 0 8px 12px rgba(9,30,66,.15), 0 0 1px rgba(9,30,66,.31);
  animation: ads-pop 200ms cubic-bezier(0.4, 1, 0.6, 1);
}
.ads-inline-dialog-title { font: 600 14px/20px -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif; margin: 0 0 4px; }
.ads-inline-dialog-body { font-size: 14px; line-height: 20px; color: #44546F; margin: 0 0 12px; }
.ads-inline-dialog-actions { display: flex; gap: 8px; }
@keyframes ads-pop { from { opacity: 0; transform: translateY(4px); } }
```

### 7. Empty state

Centered illustration spot + heading (16px bold) + one explanatory sentence +
one primary action. Honest, no mascot jokes. 🟡 (pattern), ✅ (tone)

```html
<div class="ads-empty">
  <div class="ads-empty-art" aria-hidden="true">▦</div>
  <p class="ads-empty-title">This sprint is empty</p>
  <p class="ads-empty-body">Drag issues from the backlog, or create one to get the team moving.</p>
  <button class="ads-btn ads-btn-primary">Create issue</button>
</div>
```

```css
.ads-empty { text-align: center; padding: 48px 24px; }
.ads-empty-art { font-size: 48px; color: #DFE1E6; margin-bottom: 16px; }
.ads-empty-title { font: 700 16px/20px -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif; margin: 0 0 8px; }
.ads-empty-body { font-size: 14px; color: #44546F; margin: 0 0 16px; }
```

### 8. Tabs

Text tabs with a 2px Blue/700 indicator under the active tab; inactive tabs are
Neutral/700 text, hover gets a subtle neutral background. No pill backgrounds. 🟡

```html
<div class="ads-tabs" role="tablist">
  <button class="ads-tab is-active" role="tab" aria-selected="true">Board</button>
  <button class="ads-tab" role="tab" aria-selected="false">Backlog</button>
  <button class="ads-tab" role="tab" aria-selected="false">Reports</button>
</div>
```

```css
.ads-tabs { display: flex; gap: 4px; border-bottom: 1px solid #DFE1E6; }
.ads-tab { background: none; border: 0; cursor: pointer; padding: 8px 12px;
  font: 500 14px/20px -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif;
  color: #44546F; border-bottom: 2px solid transparent; margin-bottom: -1px; }
.ads-tab:hover { background: #F1F2F4; border-radius: 3px 3px 0 0; color: #172B4D; }
.ads-tab.is-active { color: #0C66E4; border-bottom-color: #0C66E4; }
```

## Motion

Atlassian's motion system (early access, ✅ documented): motion is a clarifying
layer, not decoration. Keep everyday UI fast and subtle; reserve expression for
brand moments; honor `prefers-reduced-motion` (motion off when active).

- Hover/press feedback: near-instant — list-item hover is **50ms**; keep
  high-frequency interactions **under 150ms**. ✅
- Elements entering/exiting/moving (modals, panels, popups): longer so users can
  track spatial changes; exits are **faster than entrances**. ✅
- Official easing curves ✅:
  - Ease-out bold: `cubic-bezier(0, 0.4, 0, 1)` — panels/flags entering
  - Ease-in-out bold: `cubic-bezier(0.4, 0, 0, 1)` — scaling modals, repositioning
  - Ease-in practical: `cubic-bezier(0.6, 0, 0.8, 0.6)` — exits, getting out of the way
  - Ease-out practical: `cubic-bezier(0.4, 1, 0.6, 1)` — everyday entrances, hover fades
- Before adding motion ask: *if I remove this, does the user lose information?*
  If not, remove it. ✅

## Do / Don't

- **Do** use lozenges for every status; **don't** invent your own status hues — the
  six semantic appearances (neutral, information, success, warning, danger, discovery)
  are the vocabulary. ✅
- **Do** keep button labels as verbs ("Create", "Save", "Cancel"); **don't** label a
  button "Submit" or "OK". ✅ (Atlassian voice guidance)
- **Do** put the primary action on the right in dialog footers; **don't** stack two
  primary buttons in one dialog.
- **Do** use accent lozenge colors only for non-semantic labels (teams, tags);
  **don't** use a red accent to mean "error" — use the danger role instead. ✅
- **Do** show one `<h1>` per page and descend heading levels in order; **don't**
  fake hierarchy with bolded body text. ✅
- **Do** make hover feedback near-instant (≤150ms); **don't** animate list items
  in on load — Atlassian lists just appear. ✅
- **Do** truncate long lozenge text at 200px with an ellipsis; **don't** let badges
  wrap or stretch the layout. ✅

## Copy voice

Straightforward, helpful, team-aware. Short sentences. No marketing adjectives, no
exclamation marks in the product UI.

- Empty sprint: "This sprint is empty. Drag issues from the backlog, or create one
  to get the team moving." (action + who benefits)
- Confirmation flag: "Saved. Everyone watching this issue can see the update."
- Error: "We couldn't load the board. Check your connection and try again."
  (plain cause, plain next step — never "Something went wrong" alone)
