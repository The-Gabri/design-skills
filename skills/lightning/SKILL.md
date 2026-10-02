---
name: lightning
description: Salesforce Lightning Design System (SLDS) — enterprise CRM UI language of blue brand buttons, page headers, dense data tables, and neutral grays; use for admin consoles, dashboards, and business apps.
---

# Salesforce Lightning Design System (SLDS)

## Principles

1. **Clarity** — every element earns its place; information hierarchy beats decoration. 🟡
2. **Efficiency** — dense, scannable layouts; users complete tasks fast, not admire chrome. 🟡
3. **Consistency** — one system across every Salesforce surface; components look and behave the same everywhere. 🟡
4. **Accessibility by default** — token values carry WCAG rationale (e.g. `$brand-accessible` exists precisely so white text on brand blue passes contrast). ✅

## Color

Official SLDS design tokens (new palette, lightningdesignsystem.com/design-tokens). Confidence legend: ✅ official/documented · 🟡 cross-referenced · ⚠️ approximation.

| Token | Hex | Role |
|---|---|---|
| `$brand-accessible` / `$color-brand-dark` ✅ | `#0176d3` | Brand blue — primary buttons, links-on-brand, selections |
| `$brand-accessible-active` ✅ | `#014486` | Brand blue hover/active |
| `$brand-primary` / `$color-brand` ✅ | `#1b96ff` | Brighter brand blue (decorative, not for text) |
| `$brand-text-link` ✅ | `#0b5cab` | Text links |
| `$brand-text-link-active` ✅ | `#014486` | Link hover |
| `$brand-background-primary` ✅ | `#eef4ff` | Light brand-blue page tint |
| `$palette-blue-20` ✅ | `#032d60` | Deep navy — app headers, dark chrome |
| `$color-text-default` ✅ | `#181818` | Body text (near-black) |
| `$color-text-weak` / `$color-text-label` ✅ | `#444444` | Secondary text, field labels |
| `$color-text-inverse` ✅ | `#ffffff` | Text on dark surfaces |
| `$color-text-error` ✅ | `#ea001e` | Errors, destructive |
| `$color-text-success` ✅ | `#2e844a` | Success text |
| `$color-text-warning-alt` ✅ | `#8c4b02` | Warning text on light bg |
| `$color-border` ✅ | `#e5e5e5` | Default borders |
| `$card-color-border` ✅ | `#c9c9c9` | Card & input borders |
| `$color-background-alt` / page-header bg ✅ | `#f3f3f3` | Page header background, light gray surfaces |
| Toast themes 🟡 | success `#2e844a` · error `#ea001e` · warning `#fe9339` · info `#014486` | Toast backgrounds (white text; dark text on warning) |

Styling hooks (customize per component, never override `.slds-*` classes directly — official guidance ✅):

```css
.my-scope {
  --slds-c-button-brand-color-background: #0176d3;       /* ✅ documented hook */
  --slds-c-button-brand-color-background-hover: #014486;
  --slds-c-button-brand-color-border: #0176d3;
}
```

## Typography

- Default font stack (`$font-family`) ✅: `-apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Helvetica, Arial, sans-serif, 'Apple Color Emoji', 'Segoe UI Emoji', 'Segoe UI Symbol'`
- Legacy brand face "Salesforce Sans" shipped as a webfont in older SLDS; current system is system-stack-first — use Salesforce Sans only as a fallback name if bundled. 🟡
- Monospace: `Consolas, Menlo, Monaco, Courier, monospace` ✅
- Type scale (font-size tokens, ✅): 0.625 / 0.75 / 0.8125 / 0.875 / 1 / 1.125 / 1.25 / 1.5 / 1.75 / 2 / 2.625 rem
- Line heights: text `1.5`, headings `1.25`, reset `1` ✅
- Rules: sentence case everywhere (no ALL CAPS except tiny uppercase table headers); labels 0.75rem in `#444444`; body 0.8125rem; page titles 1.25rem, weight 400 — never bold display type.

## Layout & spacing

- Spacing scale (`$spacing-*`, ✅): `xxx-small 0.125rem` · `xx-small 0.25rem` · `x-small 0.5rem` · `small 0.75rem` · `medium 1rem` · `large 1.5rem` · `x-large 2rem` · `xx-large 3rem`. Utility classes: `slds-p-around_medium`, `slds-m-bottom_small`, `slds-var-p-horizontal_small`, etc. ✅
- Border radius (`$border-radius-*`, ✅): small `0.125rem`, **medium `0.25rem`** (the default — buttons, inputs, cards, page header), large `0.5rem`, circle `50%`.
- Grid: 12-column responsive grid — `slds-grid slds-wrap` + `slds-size_1-of-2`, `slds-medium-size_1-of-3` etc. ✅ Gutters use the spacing scale (`slds-gutters`).
- Cards sit on `#f3f3f3` (or white) canvas with 1px `#c9c9c9` borders and `.25rem` radius; page header is `#f3f3f3` with a `#c9c9c9` bottom border. ✅
- Density: tables and lists are compact — cell padding `0.25rem 0.5rem` (`$table-cell-spacing` ✅). Never airy marketing whitespace.

## Standard icon colors

Object icon tiles (`slds-icon-standard-*`) each have a fixed background with a white glyph — getting these right is what makes a page read as Salesforce at a glance. 🟡 cross-referenced from community icon references.

| Object | Tile bg |
|---|---|
| opportunity | `#fcb95b` (gold — the most recognizable one) |
| account | `#7f8de1` |
| contact | `#a094ed` |
| lead | `#f37837` |
| case | `#f2cf5b` |
| task | `#4bc076` |
| event | `#eb7092` |
| report | `#2ecbbe` |
| dashboard | `#ef6e64` |
| quote | `#88c651` |

## Components

Use the real `slds-*` classes when SLDS CSS is loaded; the CSS below mirrors token values for standalone use.

**1. Brand button**

```html
<button class="slds-button slds-button_brand">Save</button>
<button class="slds-button slds-button_neutral">Cancel</button>
<button class="slds-button slds-button_destructive">Delete</button>
```
```css
.slds-button{font-size:.8125rem;padding:0 1rem;line-height:1.875rem;min-height:2rem;
  border-radius:.25rem;border:1px solid transparent;cursor:pointer}
.slds-button_brand{background:#0176d3;border-color:#0176d3;color:#fff}
.slds-button_brand:hover{background:#014486;border-color:#014486}
.slds-button_neutral{background:#fff;border-color:#c9c9c9;color:#0176d3}
.slds-button_neutral:hover{background:#f3f3f3}
.slds-button_destructive{background:#ba0517;border-color:#ba0517;color:#fff}
```
✅ classes & behavior; hexes from official tokens.

**2. Page header (record home anatomy)** ✅ official class anatomy

```html
<div class="slds-page-header">
  <div class="slds-page-header__row">
    <div class="slds-page-header__col-title">
      <div class="slds-media">
        <div class="slds-media__figure">
          <span class="slds-icon_container slds-icon-standard-opportunity">
            <!-- object SVG icon -->
          </span>
        </div>
        <div class="slds-media__body">
          <div class="slds-page-header__name">
            <div class="slds-page-header__name-title">
              <h1><span class="slds-page-header__title">Acme — Enterprise Deal</span></h1>
            </div>
          </div>
          <p class="slds-page-header__name-meta">Opportunity • $250,000</p>
        </div>
      </div>
    </div>
    <div class="slds-page-header__col-actions">
      <div class="slds-page-header__controls">
        <div class="slds-page-header__control"><button class="slds-button slds-button_neutral">Log a Call</button></div>
        <div class="slds-page-header__control"><button class="slds-button slds-button_brand">New Opportunity</button></div>
      </div>
    </div>
  </div>
  <div class="slds-page-header__row slds-page-header__row_gutters">
    <div class="slds-page-header__col-details"><!-- detail blocks --></div>
  </div>
</div>
```

**3. Data table** ✅

```html
<table class="slds-table slds-table_cell-buffer slds-table_bordered">
  <thead><tr class="slds-line-height_reset">
    <th scope="col"><div class="slds-truncate">Opportunity Name</div></th>
    <th scope="col"><div class="slds-truncate">Amount</div></th>
  </tr></thead>
  <tbody>
    <tr class="slds-hint-parent">
      <th scope="row"><a href="#">Acme — Enterprise Deal</a></th>
      <td>$250,000</td>
    </tr>
  </tbody>
</table>
```
Rules: header labels small `#444444`, row hover `#f3f3f3`, selected row `#f3f3f3` background with 2px inset `#0176d3` left edge (`$color-background-row-selected` / `$color-border-row-selected` ✅), row actions in a trailing cell.

**4. Badge**

```html
<span class="slds-badge">Prospecting</span>
```
```css
.slds-badge{background:#f3f3f3;border:1px solid #e5e5e5;color:#181818;
  border-radius:15rem;font-size:.75rem;padding:.125rem .5rem}
```
✅. Stage-colored variants: tint backgrounds with `#2e844a`/`#ea001e`/`#0b5cab` text — 🟡 convention.

**5. Pill (selected filter / multi-select value)** ✅

```html
<span class="slds-pill">
  <span class="slds-pill__label">Stage: Negotiation</span>
  <button class="slds-pill__remove" aria-label="Remove">×</button>
</span>
```
```css
.slds-pill{display:inline-flex;align-items:center;background:#fff;
  border:1px solid #c9c9c9;border-radius:15rem;padding:.125rem .125rem .125rem .75rem;font-size:.8125rem}
.slds-pill__remove{border:none;background:transparent;color:#444444;cursor:pointer;
  border-radius:50%;width:1.25rem;height:1.25rem}
.slds-pill__remove:hover{background:#eef4ff;color:#014486}
```

**6. Modal** ✅ official class anatomy

```html
<div class="slds-modal slds-fade-in-open">
  <div class="slds-modal__container">
    <header class="slds-modal__header"><h2 class="slds-modal__title">New Opportunity</h2></header>
    <div class="slds-modal__content slds-p-around_medium"><!-- form --></div>
    <footer class="slds-modal__footer">
      <button class="slds-button slds-button_neutral">Cancel</button>
      <button class="slds-button slds-button_brand">Save</button>
    </footer>
  </div>
</div>
<div class="slds-backdrop slds-backdrop_open"></div>
```
Rules: header has bottom border `#e5e5e5`, footer top border, actions right-aligned, brand button last.

**7. Toast** ✅ classes (`slds-notify slds-notify_toast`); theme hexes 🟡/⚠️

```html
<div class="slds-notify_container">
  <div class="slds-notify slds-notify_toast slds-theme_success" role="status">
    <span class="slds-notify__content">
      <h2 class="slds-text-heading_small">Opportunity saved</h2>
      <p>Acme — Enterprise Deal was updated.</p>
    </span>
  </div>
</div>
```
```css
.slds-notify_toast{border-radius:.25rem;padding:.75rem 1rem;color:#fff;min-width:20rem}
.slds-theme_success{background:#2e844a}.slds-theme_error{background:#ea001e}
.slds-theme_warning{background:#fe9339;color:#181818}.slds-theme_info{background:#014486}
```

**8. Tabs**

```html
<div class="slds-tabs_default">
  <ul class="slds-tabs_default__nav">
    <li class="slds-tabs_default__item slds-is-active"><a class="slds-tabs_default__link" href="#">Activity</a></li>
    <li class="slds-tabs_default__item"><a class="slds-tabs_default__link" href="#">Details</a></li>
  </ul>
  <div class="slds-tabs_default__content">…</div>
</div>
```
Active tab: `#181818` text with `#0176d3` bottom border; inactive `#444444`, hover `#0b5cab`. 🟡

**9. Card**

```html
<article class="slds-card">
  <div class="slds-card__header slds-grid">
    <header class="slds-media slds-media_center">
      <div class="slds-media__body"><h2 class="slds-card__header-title">Key Metrics</h2></div>
    </header>
  </div>
  <div class="slds-card__body slds-card__body_inner">…</div>
  <footer class="slds-card__footer"><a href="#">View All</a></footer>
</article>
```
Card: white, 1px `#c9c9c9`, radius `.25rem`; footer link centered, `#0b5cab`. ✅

**10. Sales Path (the signature chevron stage bar)** ✅ official token values, verified against the design-token set

Real path colors (not blue-on-blue — this is the detail most rebuilds get wrong):

| State | Background | Text |
|---|---|---|
| `slds-is-complete` | `#3ba755` (`$color-background-path-complete`) · hover `#2e844a` | white + white checkmark |
| `slds-is-current` | white (`$color-background-path-current`) with 2px `#014486` border (`$color-border-path-current`, `$width-path-border-current`) | `#014486` bold (`$color-text-path-current`) |
| `slds-is-incomplete` | `#f3f3f3` · hover `#c9c9c9` | `#444444` |
| `slds-is-won` | `#2e844a` | white |
| `slds-is-lost` | `#ea001e` | white |

Chevrons are separated by 2px white dividers (`$color-border-path-divider`), height `2rem` (`$height-sales-path`). Below the bar sits the Guidance for Success panel: stage guidance text, key fields, a brand "Mark Stage as Complete" button and a "Mark as Closed Lost" link.

```css
/* chevron geometry (one polygon per position; current stage gets the
   2px border via a padded outer cell in $color-border-path-current) */
.path-cell.pos-first .path-item{clip-path:polygon(0 0,calc(100% - .75rem) 0,100% 50%,calc(100% - .75rem) 100%,0 100%)}
.path-cell.pos-mid .path-item{clip-path:polygon(0 0,calc(100% - .75rem) 0,100% 50%,calc(100% - .75rem) 100%,0 100%,.75rem 50%)}
.path-cell.pos-last .path-item{clip-path:polygon(0 0,100% 0,100% 100%,0 100%,.75rem 50%)}
.path-cell.is-complete .path-item{background:#3ba755;color:#fff}
.path-cell.is-current{background:#014486;padding:2px}
.path-cell.is-current .path-item{background:#fff;color:#014486;font-weight:700}
```

## Motion

SLDS defines no signature choreography — keep it minimal: short linear/ease fades (~100ms) for dropdowns, modals, and toasts; no bouncy easing, no parallax, no page transitions. 🟡

## Do / Don't

- **Do** use `#0176d3` for the single primary action per view; secondary actions stay `slds-button_neutral` (white, blue text).
  **Don't** make every button brand blue — in SLDS, one blue button per screen is the rule. 🟡
- **Do** put the page header at the top of every record/list view with icon tile + object label + record name + actions.
  **Don't** invent a custom hero banner — CRM pages open with the page header, not a marketing hero.
- **Do** left-align dense tables with `0.25rem 0.5rem` cell padding and hover highlighting.
  **Don't** add zebra striping or rounded "card" rows — SLDS tables are flat with hairline `#e5e5e5` rules. 🟡
- **Do** write sentence case, e.g. "New opportunity", and end toast titles without periods.
  **Don't** use ALL CAPS for headings — SLDS voice is sentence case. 🟡
- **Do** customize via `--slds-c-*` / `--slds-g-*` styling hooks scoped to your component.
  **Don't** override `.slds-*` classes directly — internals change between releases and overrides break. ✅ (official guidance)
- **Do** show record state with badges/pills (stage, status, owner).
  **Don't** invent gradient status chips — flat tints only. 🟡

## Copy voice

Direct, task-oriented, no marketing fluff. Examples: "Opportunity saved." / "12 records • Updated 2 minutes ago" / "Save and New".
