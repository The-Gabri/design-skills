---
name: polaris
description: Shopify Polaris — the design system behind the Shopify admin: dense, merchant-first UIs with token-based surfaces, sentence-case plain-language copy, and data-heavy pages (Page, Card, ResourceList, Filters, Banner, EmptyState).
---

# Polaris (Shopify)

Shopify's design system for the Shopify admin and merchant-facing apps. Everything it does is optimized for one persona: **the merchant**, running their business in short bursts between real work. Polaris pages are dense, scannable, and calm — a neutral gray canvas, white cards, dark pill/rectangular buttons, and copy written in plain sentence case.

> Note on generations: Polaris React (v9–v12) was the token-based component library with the gray `#f1f1f1` admin canvas. In early 2026 Shopify archived Polaris React and moved to **Polaris web components** (`s-page`, `s-section`, …) loaded from the Shopify CDN with App Bridge. This skill documents the v12 token values (still the visual source of truth for the admin look) and flags the newest-admin differences inline.

## Principles

These are Shopify's own experience values that Polaris implements ("build apps that feel like Shopify"):

1. **Considerate** — Respect the merchant's device, language, geography, and accessibility needs. Never block them over something trivial; every modal asks whether it's really necessary.
2. **Empowering** — Optimize for the most important tasks by removing complexity, but keep advanced features reachable. Merchants range from first-time sellers to power users.
3. **Efficient** — Merchants should complete tasks quickly, accurately, and easily. 14px body text, dense lists, saved filter views, bulk actions — density is a feature.
4. **Trustworthy** — Be transparent about what the app can and cannot do. Destructive confirmations state the consequence and reversibility in plain words.
5. **Familiar** — Use patterns merchants already know from the admin (resource lists, index filters, contextual save bar) so they focus on the task, not the navigation.
6. **Crafted** — The system sweats micro-details: bevel highlights on buttons, 4px-grid spacing, and one dominant action per screen. Never loud or playful for its own sake.

## Color

Core v12 tokens with light-scheme hex values. Legend: ✅ official/documented · 🟡 cross-referenced · ⚠️ community approximation.

| Token | Hex | Role | Conf. |
|---|---|---|---|
| `--p-color-bg` | `#f1f1f1` | Page canvas (neutral gray) | ✅ |
| `--p-color-bg-surface` | `#ffffff` | Cards, popovers | ✅ |
| `--p-color-bg-surface-secondary` | `#f6f6f7` | Secondary surfaces | 🟡 |
| `--p-color-bg-fill-brand` | `#303030` | Primary buttons, brand fill | ✅ |
| `--p-color-bg-fill-brand-hover` | `#1a1a1a` | Primary hover | ✅ |
| `--p-color-bg-fill-brand-active` | `#1a1a1a` | Primary pressed | ✅ |
| `--p-color-bg-fill-critical` | `#d72c0d` | Destructive buttons/fills | 🟡 |
| `--p-color-text` | `#1a1a1a` | Default text | 🟡 |
| `--p-color-text-secondary` | `#616a75` | Subdued/metadata text | 🟡 |
| `--p-color-text-brand` | `#005c4b` | Brand-colored text (older gen) | ⚠️ |
| `--p-color-text-critical` | `#d72c0d` | Error text | 🟡 |
| `--p-color-border` | `#e3e5e7` | Default border | 🟡 |
| `--p-color-border-secondary` | `#ebebeb` | Hairline dividers | ⚠️ |
| `--p-color-bg-surface-success` | `#eafbea` | Success banner surface | ⚠️ |
| `--p-color-bg-surface-critical` | `#fbeae5` | Critical banner surface | ⚠️ |
| `--p-color-bg-surface-warning` | `#fcf1cd` | Warning banner surface | ⚠️ |
| `--p-color-bg-surface-info` | `#eaf4ff` | Info banner surface | ⚠️ |
| `--p-color-bg-fill-success` | `#2a7d3e` | Success fills/badges | 🟡 |
| `--p-color-text-link` / interactive | `#005bd3` | Links, plain buttons | 🟡 |
| focus ring | `#4680ff` | 2px focus outline | 🟡 |

Rules that make it Polaris, not just gray-and-white:

- **The gray canvas is the identity.** `--p-color-bg` (`#f1f1f1`) behind white cards is non-negotiable. Never white-on-white floating cards.
- **Primary buttons are near-black (`#303030`), not green.** Shopify green (`#008060`-family) is reserved for success states, active badges, and positive indicators. A green CTA is wrong.
- **Color appears only as semantic tone.** Badges, banners, icons carry tone color; chrome and buttons stay monochrome.
- Newest admin (web-component era) shift: near-black `#101010` primary buttons, white page with floating panels. Mark generation if it matters.

## Typography

Polaris uses **system fonts, not a brand face** — Inter (variable, weights 450/550/650) when available, falling back to the OS stack.

```css
font-family: Inter, -apple-system, BlinkMacSystemFont, "San Francisco",
  "Segoe UI", Roboto, "Helvetica Neue", sans-serif;
```

- **Body default is 14px/20px** (`--p-font-size-300: 14px` ✅ scale), not 16px. Polaris optimizes for information-dense admin UIs. Use 16px (`bodyLg`) only for prominent descriptions.
- **Non-standard weights**: regular **450**, medium **550**, semibold **650**, bold **700**. Using 400/500/600 gives subtly wrong rendering against real Polaris. ✅
- Type scale (`--p-font-size-*`): `275: 11px`, `300: 14px`, `325: 15px`, `350: 16px`, `400: 20px`, `500: 24px`, `600: 28px`, `700: 32px`, `800: 40px` 🟡.
- Component variants: `bodySm` / `bodyMd` (default) / `bodyLg`, `headingXs`–`heading4xl`. Page titles are restrained (never 48px display type).
- **Sentence case everywhere.** Headings, buttons, table columns, tabs. "Create order", not "Create Order". ✅

## Layout & spacing

- **4px base grid.** Spacing scale ✅: `--p-space-050: 2px`, `100: 4px`, `200: 8px`, `300: 12px`, `400: 16px`, `500: 20px`, `600: 24px`, `800: 32px`, `1000: 40px`, `1200: 48px`, `1600: 64px`, `3200: 128px`. Nothing is 6px or 15px.
- **Border radius** 🟡: `--p-border-radius-100: 4px` (checkboxes, badges), `-200: 8px` (buttons, inputs), `-300: 12px` (cards), `-400: 16px`, `-500: 20px`, `-full: 9999px` (pills/avatars).
- **Shadows are minimal and precise**, never generic blurs. Card elevation: `0 0 0 1px rgba(63,63,68,.05), 0 1px 3px 0 rgba(63,63,68,.15)` 🟡. Newer card shadow: `--p-shadow-100: 0 1px 0 0 rgba(26,26,26,.07)` 🟡.
- **Buttons carry a tactile bevel**, not a flat fill: over the `#303030` fill, a top-to-bottom gradient overlay `linear-gradient(180deg, rgba(48,48,48,0) 63.53%, hsla(0,0%,100%,.15))` plus inset highlights `inset 0 -1px 0 rgba(0,0,0,.2), inset 0 1px 0 rgba(255,255,255,.04)` ✅ (reverse-engineered from the actual button CSS).
- **Layout primitives**: `Page` (max-width content column, title top-left, primary action top-right), `Card` (white, 12px radius, 16px padding), `Layout` sections (full-width + one-third aside). Headings sit *above* cards, not inside them.
- Borders: `--p-border-width-0165: 1px` (inputs, pagination), `--p-border-width-025: 2px` ✅ naming.

## Components

Copy-pasteable HTML/CSS approximations using the real tokens. (Polaris React: `import {Page, Card, ResourceList, Filters, Banner, EmptyState, Modal, Button, Badge} from '@shopify/polaris'`; web components: `<s-page>`, `<s-section>`, …)

### 1. Button

```html
<button class="p-btn p-btn-primary">Create order</button>
<button class="p-btn p-btn-secondary">Discard</button>
<button class="p-btn p-btn-destructive">Delete products</button>
```
```css
.p-btn {
  font-size: 14px; font-weight: 550; line-height: 20px;
  border-radius: 8px; padding: 6px 16px; min-height: 36px;
  border: 1px solid transparent; cursor: pointer;
}
.p-btn-primary {
  color: #fff; background: #303030;
  background-image: linear-gradient(180deg, rgba(48,48,48,0) 63.53%, hsla(0,0%,100%,.15));
  box-shadow: inset 0 -1px 0 rgba(0,0,0,.2), inset 0 1px 0 rgba(255,255,255,.04);
}
.p-btn-primary:hover { background-color: #1a1a1a; }
.p-btn-secondary {
  color: #1a1a1a; background: #fff; border-color: #c9cccf;
  box-shadow: inset 0 -1px 0 rgba(0,0,0,.06), inset 0 1px 0 rgba(255,255,255,.04);
}
.p-btn-destructive { color: #fff; background: #d72c0d; }
.p-btn:disabled { background: #ebebeb; color: #a1a8b3; box-shadow: none; cursor: default; }
```

### 2. Card

```html
<section class="p-card">
  <h2 class="p-heading-md">Order timeline</h2>
  <p class="p-body">…</p>
</section>
```
```css
.p-card {
  background: #fff; border-radius: 12px; padding: 16px;
  box-shadow: 0 0 0 1px rgba(63,63,68,.05), 0 1px 3px 0 rgba(63,63,68,.15);
}
```

### 3. Page header

```html
<header class="p-page-header">
  <div>
    <h1 class="p-page-title">Orders</h1>
    <p class="p-body p-subdued">Review and fulfill recent orders.</p>
  </div>
  <div class="p-actions">
    <button class="p-btn p-btn-secondary">Export</button>
    <button class="p-btn p-btn-primary">Create order</button>
  </div>
</header>
```
```css
.p-page-header { display: flex; justify-content: space-between; align-items: flex-start; gap: 16px; margin-bottom: 16px; }
.p-page-title { font-size: 24px; line-height: 32px; font-weight: 650; letter-spacing: -.01em; margin: 0; }
.p-actions { display: flex; gap: 8px; }
```

### 4. ResourceList (rows, not a table)

Use when merchants read rows and click into one (thumbnail + lines of metadata). For selectable/bulk/sortable data, use an IndexTable instead.

```html
<ul class="p-resource-list">
  <li class="p-resource-item">
    <input type="checkbox" aria-label="Select order 1042">
    <div class="p-item-media"><span class="p-thumb">#1042</span></div>
    <div class="p-item-body">
      <a href="#">#1042 · Ana Beltrán</a>
      <span class="p-subdued">2 items · $84.50 · Paid</span>
    </div>
    <span class="p-badge p-badge-success">Fulfilled</span>
  </li>
</ul>
```
```css
.p-resource-list { list-style: none; margin: 0; padding: 0; }
.p-resource-item {
  display: flex; align-items: center; gap: 12px;
  padding: 12px 16px; border-top: 1px solid #ebebeb; font-size: 14px;
}
.p-resource-item:first-child { border-top: 0; }
.p-resource-item:hover { background: #f6f6f7; }
```

### 5. Filters (tabs + search + pills)

```html
<div class="p-filters">
  <nav class="p-tabs" role="tablist">
    <button class="p-tab p-tab-active" role="tab" aria-selected="true">All</button>
    <button class="p-tab" role="tab" aria-selected="false">Unfulfilled <span class="p-tab-count">4</span></button>
    <button class="p-tab" role="tab" aria-selected="false">Unpaid</button>
  </nav>
  <div class="p-filter-bar">
    <input class="p-search" type="search" placeholder="Search orders" aria-label="Search orders">
    <span class="p-pill">Fulfillment: Unfulfilled <button aria-label="Remove filter">×</button></span>
    <button class="p-btn p-btn-secondary">More filters</button>
  </div>
</div>
```
```css
.p-tab { background: none; border: 0; font-size: 14px; font-weight: 550; color: #616a75; padding: 8px 12px; border-bottom: 2px solid transparent; cursor: pointer; }
.p-tab-active { color: #1a1a1a; border-bottom-color: #303030; }
.p-tab-count { background: #ebebeb; border-radius: 9999px; padding: 1px 8px; font-size: 11px; }
.p-search { height: 36px; border: 1px solid #c9cccf; border-radius: 8px; padding: 0 12px 0 32px; font-size: 14px; background: #fff; }
.p-pill { display: inline-flex; align-items: center; gap: 6px; background: #ebebeb; border-radius: 9999px; padding: 4px 6px 4px 12px; font-size: 13px; }
```

### 6. Banner (loud, persistent, tone-colored)

Banner is the loud persistent message; Badge is quiet status; Toast is transient success; Modal is a blocking decision.

```html
<div class="p-banner p-banner-info" role="status">
  <div class="p-banner-icon" aria-hidden="true">i</div>
  <div>
    <p class="p-banner-title">Payouts are on hold</p>
    <p class="p-body">Update your bank details to receive payouts again.</p>
  </div>
  <button class="p-banner-dismiss" aria-label="Dismiss">×</button>
</div>
```
```css
.p-banner { display: flex; gap: 12px; align-items: flex-start; border-radius: 12px; padding: 16px; margin-bottom: 16px; }
.p-banner-info { background: #eaf4ff; }      /* ⚠️ approximated surface */
.p-banner-success { background: #eafbea; }
.p-banner-warning { background: #fcf1cd; }
.p-banner-critical { background: #fbeae5; }
.p-banner-title { font-size: 14px; font-weight: 650; margin: 0 0 4px; }
```

### 7. EmptyState (invitation, not apology)

```html
<div class="p-empty">
  <h2 class="p-heading-md">Add products to your store</h2>
  <p class="p-body p-subdued">Start selling by adding your first product. You can add descriptions, images, and pricing.</p>
  <button class="p-btn p-btn-primary">Add product</button>
</div>
```
```css
.p-empty { text-align: center; padding: 48px 32px; max-width: 520px; margin: 0 auto; }
.p-empty .p-btn { margin-top: 16px; }
```

### 8. Badge

```html
<span class="p-badge p-badge-success">Paid</span>
<span class="p-badge p-badge-attention">Unfulfilled</span>
<span class="p-badge">Draft</span>
```
```css
.p-badge { display: inline-flex; align-items: center; border-radius: 9999px; padding: 3px 8px; font-size: 12px; font-weight: 550; background: #ebebeb; color: #1a1a1a; }
.p-badge-success { background: #a4e8b4; color: #0c3d1c; }   /* 🟡 */
.p-badge-attention { background: #ffe9a8; color: #573b00; } /* 🟡 */
.p-badge-critical { background: #fead9a; color: #61130a; }  /* 🟡 */
```

### 9. Modal

```html
<div class="p-modal-backdrop">
  <div class="p-modal" role="dialog" aria-modal="true" aria-labelledby="m-title">
    <h2 id="m-title" class="p-heading-md">Delete 12 products?</h2>
    <p class="p-body">This can't be undone.</p>
    <div class="p-modal-footer">
      <button class="p-btn p-btn-secondary">Cancel</button>
      <button class="p-btn p-btn-destructive">Delete products</button>
    </div>
  </div>
</div>
```
```css
.p-modal-backdrop { position: fixed; inset: 0; background: rgba(26,26,26,.5); display: grid; place-items: center; }
.p-modal { background: #fff; border-radius: 12px; padding: 20px; width: min(480px, calc(100vw - 64px)); }
.p-modal-footer { display: flex; justify-content: flex-end; gap: 8px; margin-top: 20px; }
```

### 10. Toast (transient feedback)

```html
<div class="p-toast" role="status">Product saved</div>
```
```css
.p-toast {
  position: fixed; bottom: 32px; left: 50%; transform: translateX(-50%);
  background: #1a1a1a; color: #fff; font-size: 14px; font-weight: 550;
  border-radius: 9999px; padding: 10px 20px; box-shadow: 0 4px 12px rgba(0,0,0,.25);
}
```

## Motion

Polaris is deliberately restrained: motion exists for feedback, not decoration.

- Duration tokens 🟡: `--p-motion-duration-100: 100ms`, `-150: 150ms`, `-200: 200ms`, `-300: 300ms`, `-500: 500ms`.
- Easing 🟡: `--p-motion-ease: cubic-bezier(0.32, 0.72, 0, 1)`; `--p-motion-linear: cubic-bezier(0, 0, 1, 1)`.
- Rules: animate state changes under 200ms (hovers, row highlights, checkbox ticks); 300–500ms only for popover/modal entrances and toast slide-ins. No entrance animations on page load, no parallax, no decorative reveals. Skeleton screens pulse (`opacity 1 ↔ .4`, 1.5s ease-in-out infinite) while loading.

## Do / Don't

- **Do** put the page title top-left and the primary action top-right ("Create order", "Add product"). **Don't** center the header or float the CTA.
- **Do** use dark `#303030` for primary buttons and reserve green for success. **Don't** make the primary CTA green "because Shopify".
- **Do** keep body text at 14px with 20px line-height in admin UIs. **Don't** bump everything to 16px — the density is the design.
- **Do** pick the list component by behavior: IndexTable for selectable/bulk/sort rows, ResourceList for clickable rows with rich metadata, DataTable for comparing numbers. **Don't** use a fancy card grid for data the merchant needs to scan.
- **Do** design the empty state, loading state, and "1 item" state for every list. **Don't** ship a list that only looks good when full.
- **Do** use a Banner for "payouts on hold" (persistent, needs attention) and a Toast for "Product saved" (transient, no action needed). **Don't** use a modal to say "saved successfully".
- **Do** use the contextual save bar pattern for dirty forms: pinned top bar with "Save" / "Discard" that blocks navigation until resolved. **Don't** rely on the merchant remembering to scroll back to a save button.
- **Do** pair every tone color with an icon and text label (badges, banners). **Don't** communicate status through color alone.
- **Do** label destructive buttons with the actual outcome: "Delete products", never "Confirm" or "OK". **Don't** make the merchant guess what a generic button does.

## Copy voice (for brand styles)

Voice: plain, direct, confident — a knowledgeable colleague, not a mascot and not a lawyer. Write like merchants talk (7th-grade reading level, contractions welcome).

Mechanics: sentence case everywhere; active voice, verb-first buttons; no terminal punctuation on labels, headings, or buttons (body copy gets periods); numerals for numbers ("3 products"); no "click here", no jargon, no branded feature names for ordinary things.

Example strings:

- EmptyState heading: **"Add a layer of security to your store"** — body: "Create custom filters to help you prevent fraud." — action: "Add a filter". (Name what goes here, one line of why, one action. Never "No data.")
- Destructive modal: heading **"Delete 12 products?"** — body: "This can't be undone." — buttons: "Cancel" / "Delete products".
- Inline error (next to the field, never "Error:" prefix): **"Enter a price using numbers only."** ✅ (official Polaris content guidance; voice summary cross-referenced from Polaris Fundamentals content docs)

Sources: polaris.shopify.com tokens reference (✅ via token-source snippets in the wild: `--p-color-bg-fill-brand: #303030`, button gradient), Shopify partner blog summarizing Polaris experience values (✅ Considerate/Empowering/Crafted/Efficient/Trustworthy/Familiar), polaris-react.shopify.com Fundamentals content docs (✅ plain-language, sentence case, contractions), plus cross-referenced community rebuilds of the admin for spacing/radius/motion values.
