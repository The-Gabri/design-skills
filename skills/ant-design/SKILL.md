---
name: ant-design
description: Ant Design (Alibaba/Ant Group) enterprise design language — dense data UIs, certainty-first admin consoles, blue #1677ff primary, Tables/Forms/Steps.
---

# Ant Design

The design language and component system of Ant Group (Alibaba), built for
**enterprise-class products**: admin consoles, dashboards, ops tools, CRMs,
data-heavy back offices. Optimizes for information density, predictability and
efficiency — never for consumer flash. If it looks like a marketing landing
page, it's not Ant Design.

## Principles

1. **Natural** (自然) — interactions follow human intuition and OS/enterprise
   conventions; reduce unnecessary thinking. Prefer familiar patterns over
   novel inventions.
2. **Certain** (确定性) — users always know their state: hover, focus, active,
   loading, error and empty states are explicit and consistent everywhere.
3. **Meaningful** (意义感) — every element serves the user's mission; visual
   emphasis is reserved for action, and feedback is immediate. Remove
   decoration that does not communicate.
4. **Growing** (生长性) — the system scales from a small form to a dense table
   to a multi-tenant admin console without losing coherence (design tokens).
5. **Density is a feature.** Enterprise users scan tables with hundreds of
   rows: 12px cell padding and 14px base type keep data readable without
   wasting space.
6. **Color is scarce on purpose.** Most of the UI is neutral; status color
   (green/red/gold tags, alert banners) pops precisely because it is rare.

## Color

✅ official (docs/spec/colors, v5 token set) · 🟡 cross-referenced from theme
algorithms · ⚠️ community approximation.

| Token | Hex | Role |
|---|---|---|
| `colorPrimary` / Daybreak Blue ✅ | `#1677ff` | primary actions, links, active states |
| `colorLink` ✅ | `#1677ff` | links; hover `#69b1ff` 🟡, active `#0958d9` 🟡 |
| `colorSuccess` / Polar Green ✅ | `#52c41a` | success states, passed, "paid" |
| `colorWarning` / Calendar Gold ✅ | `#faad14` | warnings, pending, caution |
| `colorError` / Dust Red ✅ | `#ff4d4f` | errors, destructive, failed |
| `colorInfo` ✅ | `#1677ff` | informational (same as primary) |
| `colorText` / heading ✅ | `rgba(0,0,0,.85)` | headings, table headers |
| `colorText` / body ✅ | `rgba(0,0,0,.65)` | body text — default text color is NOT black |
| `colorTextSecondary` ✅ | `rgba(0,0,0,.45)` | descriptions, placeholders-as-labels |
| `colorTextDisabled` ✅ | `rgba(0,0,0,.25)` | disabled text |
| `colorBgContainer` ✅ | `#ffffff` | cards, tables, modals |
| `colorBgLayout` ✅ | `#f0f2f5` | page background (light grey-blue) |
| `colorBgElevated` ✅ | `#ffffff` | popovers, dropdowns |
| `colorBorder` ✅ | `#d9d9d9` | inputs, default borders |
| `colorBorderSecondary` / split ✅ | `#f0f0f0` | table row dividers, card dividers |
| `colorPrimaryBg` ✅ | `#e6f4ff` | primary-tinted surfaces (info alerts) |
| `colorSuccessBg` ✅ | `#f6ffed` | success alert backgrounds |
| `colorWarningBg` ✅ | `#fffbe6` | warning alert backgrounds |
| `colorErrorBg` ✅ | `#fff2f0` | error alert backgrounds |
| dark sider bg ✅ | `#001529` | classic left navigation in dark admin layouts |
| geekblue ⚠️ | `#2f54eb` | extended preset palette |
| purple ⚠️ | `#722ed1` | extended preset palette |
| cyan ⚠️ | `#13c2c2` | extended preset palette |
| volcano ⚠️ | `#fa541c` | extended preset palette |
| magenta ⚠️ | `#eb2f96` | extended preset palette |

Neutral greys (✅): `#ffffff #fafafa #f5f5f5 #f0f0f0 #d9d9d9 #bfbfbf #8c8c8c #595959 #434343 #262626 #1f1f1f #141414 #000000`.

Rules: primary actions get exactly one blue button per view; destructive
actions are `#ff4d4f` text or a red primary button — never both at once;
status is conveyed with a colored dot + tag, not by recoloring the whole row.

## Typography

System font stack (✅ official `fontFamily` token):
`-apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, 'Helvetica Neue', Arial,
'Noto Sans', sans-serif, 'Apple Color Emoji', 'Segoe UI Emoji', 'Segoe UI Symbol', 'Noto Color Emoji'`.
Code: `'SFMono-Regular', Consolas, 'Liberation Mono', Menlo, Courier, monospace`.

- Base size `14px`, line-height `1.5715` (22px). Body copy at 14px is a
  signature trait — don't "fix" it to 16px.
- Small/meta: `12px`; large: `16px`.
- Headings: `h5 16px · h4 20px · h3 24px · h2 30px · h1 38px`, weight `600`,
  color `rgba(0,0,0,.85)`. ✅
- Weights: only `400` and `600` in product UI; body text stays `400`.
- Links are always `#1677ff` with underline only on hover.

## Layout & spacing

- **4px base grid** (✅); layout gaps snap to **8px multiples**: 8 (tight/related),
  16 (standard), 24 (section separation). Page gutters are 24px.
- **24-column grid** for page layout; top-to-bottom single-column forms;
  complex groups go in cards, not in nested panels.
- **Border radius** (✅ v5 seed tokens): controls `6px`, small elements `4px`,
  surfaces/cards `8px`; pill radius reserved for avatars, badges, dots.
- **Borders first, shadows last** (✅ "flat-first"): 1px `#d9d9d9`/`#f0f0f0`
  carries hierarchy. Shadows are reserved for genuinely floating surfaces
  (modal, dropdown, popover): `0 6px 16px -8px rgba(0,0,0,.08)`.
- Component heights: default `32px`, small `24px`, large `40px`. Table rows
  54px default / 47px middle / 39px small. Pagination shows `Total N items`
  and a page-size select.
- Density modes: comfortable (default) and compact (`compactAlgorithm`) for
  data-heavy views.
- Left nav: 256px expanded / 80px collapsed; dark `#001529` or light white.
  Content header pattern: **breadcrumb → page title + actions → tabs/filter**.

## Components

Copy-pasteable HTML/CSS. Uses the tokens above; no external dependencies.

### 1. Primary button (32px, `#1677ff`)

```html
<button class="ant-btn-primary">Submit</button>
<style>
.ant-btn-primary {
  height: 32px; padding: 0 15px; font-size: 14px; border-radius: 6px;
  background: #1677ff; color: #fff; border: 1px solid #1677ff; cursor: pointer;
}
.ant-btn-primary:hover { background: #4096ff; border-color: #4096ff; }
.ant-btn-primary:active { background: #0958d9; border-color: #0958d9; }
.ant-btn-default {
  height: 32px; padding: 0 15px; font-size: 14px; border-radius: 6px;
  background: #fff; color: rgba(0,0,0,.88); border: 1px solid #d9d9d9;
}
</style>
```

### 2. Data table (dense, sortable, zebra-free)

```html
<table class="ant-table">
  <thead><tr><th>Vehicle <span class="sorter">▲▼</span></th><th>Status</th></tr></thead>
  <tbody><tr><td>Truck 104</td><td><span class="ant-tag-green">In service</span></td></tr></tbody>
</table>
<style>
.ant-table { width: 100%; border-collapse: separate; border-spacing: 0; font-size: 14px; }
.ant-table thead th {
  background: #fafafa; color: rgba(0,0,0,.88); font-weight: 600;
  padding: 12px 16px; text-align: left; border-bottom: 1px solid #f0f0f0;
}
.ant-table tbody td { padding: 12px 16px; border-bottom: 1px solid #f0f0f0; }
.ant-table tbody tr:hover td { background: #fafafa; }
.sorter { color: #bfbfbf; font-size: 11px; cursor: pointer; }
.sorter.on { color: #1677ff; }
</style>
```

### 3. Form item with validation states

```html
<div class="ant-form-item has-error">
  <label class="ant-form-label">Work order title</label>
  <input class="ant-input" placeholder="e.g. Brake inspection — Truck 104">
  <div class="ant-form-explain">Please enter a title.</div>
</div>
<style>
.ant-form-label { display: block; font-size: 14px; margin-bottom: 4px; }
.ant-input {
  width: 100%; height: 32px; padding: 4px 11px; font-size: 14px;
  border: 1px solid #d9d9d9; border-radius: 6px; color: rgba(0,0,0,.88);
}
.ant-input:focus { border-color: #4096ff; outline: 0; box-shadow: 0 0 0 2px rgba(5,145,255,.1); }
.has-error .ant-input { border-color: #ff4d4f; }
.has-error .ant-input:focus { box-shadow: 0 0 0 2px rgba(255,77,79,.1); }
.has-warning .ant-input { border-color: #faad14; }
.ant-form-explain { font-size: 14px; color: #ff4d4f; margin-top: 4px; }
.has-warning .ant-form-explain { color: #faad14; }
</style>
```

### 4. Steps (wizard)

```html
<div class="ant-steps">
  <div class="ant-step done"><span class="dot">✓</span><span class="label">Select vehicle</span></div>
  <div class="ant-step current"><span class="dot">2</span><span class="label">Describe issue</span></div>
  <div class="ant-step todo"><span class="dot">3</span><span class="label">Review</span></div>
</div>
<style>
.ant-steps { display: flex; align-items: center; gap: 8px; }
.ant-step { display: flex; align-items: center; gap: 8px; }
.ant-step .dot {
  width: 32px; height: 32px; border-radius: 50%; display: grid; place-items: center;
  font-size: 14px; border: 1px solid #d9d9d9; color: rgba(0,0,0,.25); background: #fff;
}
.ant-step .label { font-size: 14px; color: rgba(0,0,0,.45); }
.ant-step.done .dot { background: #1677ff; border-color: #1677ff; color: #fff; }
.ant-step.done .label { color: rgba(0,0,0,.88); }
.ant-step.current .dot { border-color: #1677ff; color: #1677ff; }
.ant-step.current .label { color: rgba(0,0,0,.88); font-weight: 600; }
.ant-step + .ant-step::before { content: ""; width: 48px; height: 1px; background: #f0f0f0; margin-right: 8px; }
</style>
```

### 5. Alert banners

```html
<div class="ant-alert ant-alert-info">ℹ 3 vehicles are due for inspection this week.</div>
<style>
.ant-alert { padding: 8px 12px; border-radius: 8px; font-size: 14px; border: 1px solid; }
.ant-alert-info    { background: #e6f4ff; border-color: #91caff; color: rgba(0,0,0,.88); }
.ant-alert-success { background: #f6ffed; border-color: #b7eb8f; color: rgba(0,0,0,.88); }
.ant-alert-warning { background: #fffbe6; border-color: #ffe58f; color: rgba(0,0,0,.88); }
.ant-alert-error   { background: #fff2f0; border-color: #ffccc7; color: rgba(0,0,0,.88); }
</style>
```

### 6. Tabs

```html
<div class="ant-tabs"><button class="on">All</button><button>Scheduled</button><button>In progress</button></div>
<style>
.ant-tabs { display: flex; gap: 24px; border-bottom: 1px solid #f0f0f0; }
.ant-tabs button {
  background: none; border: none; font-size: 14px; color: rgba(0,0,0,.65);
  padding: 12px 0; cursor: pointer; position: relative;
}
.ant-tabs button.on { color: #1677ff; }
.ant-tabs button.on::after {
  content: ""; position: absolute; left: 0; right: 0; bottom: -1px; height: 2px; background: #1677ff;
}
</style>
```

### 7. Tags & badges

```html
<span class="ant-tag ant-tag-green">In service</span>
<span class="ant-badge"><span class="dot-red"></span>2 critical</span>
<style>
.ant-tag { font-size: 12px; padding: 1px 8px; border-radius: 4px; border: 1px solid; }
.ant-tag-green { background: #f6ffed; border-color: #b7eb8f; color: #389e0d; }
.ant-tag-gold  { background: #fffbe6; border-color: #ffe58f; color: #d48806; }
.ant-tag-red   { background: #fff2f0; border-color: #ffccc7; color: #cf1322; }
.ant-tag-blue  { background: #e6f4ff; border-color: #91caff; color: #0958d9; }
.ant-badge .dot-red { display: inline-block; width: 6px; height: 6px; border-radius: 50%; background: #ff4d4f; margin-right: 8px; }
</style>
```

### 8. Empty state

```html
<div class="ant-empty">
  <div class="ant-empty-img">▢</div>
  <p>No work orders found</p>
  <button class="ant-btn-primary">Create now</button>
</div>
<style>
.ant-empty { text-align: center; padding: 48px 0; color: rgba(0,0,0,.45); font-size: 14px; }
.ant-empty-img { font-size: 64px; color: #d9d9d9; margin-bottom: 8px; }
</style>
```
(Real antd uses its own line-art illustration; the gray geometric placeholder
above keeps the same reserved tone.)

### 9. Result (success page)

```html
<div class="ant-result">
  <div class="ant-result-icon ok">✓</div>
  <h3 class="ant-result-title">Work order created successfully</h3>
  <p class="ant-result-sub">WO-2026-1042 has been assigned to Bay 3. The driver was notified.</p>
  <button class="ant-btn-primary">View order</button>
  <button class="ant-btn-default">Create another</button>
</div>
<style>
.ant-result { text-align: center; padding: 48px 24px; }
.ant-result-icon { width: 72px; height: 72px; border-radius: 50%; display: inline-grid; place-items: center; font-size: 36px; color: #fff; }
.ant-result-icon.ok { background: #52c41a; }
.ant-result-title { font-size: 24px; font-weight: 600; color: rgba(0,0,0,.88); margin: 24px 0 8px; }
.ant-result-sub { font-size: 14px; color: rgba(0,0,0,.45); margin-bottom: 24px; }
.ant-result button + button { margin-left: 8px; }
</style>
```

### 10. Pagination

```html
<div class="ant-pagination">
  <span class="total">Total 48 items</span>
  <button>‹</button><button class="on">1</button><button>2</button><button>3</button><button>›</button>
</div>
<style>
.ant-pagination { display: flex; align-items: center; gap: 8px; font-size: 14px; }
.ant-pagination .total { color: rgba(0,0,0,.45); margin-right: 8px; }
.ant-pagination button {
  min-width: 32px; height: 32px; border: 1px solid #d9d9d9; border-radius: 6px;
  background: #fff; cursor: pointer;
}
.ant-pagination button.on { border-color: #1677ff; color: #1677ff; font-weight: 600; }
</style>
```

## Motion

Three official motion principles: **Natural, Performant, Concise** ✅. Micro
interactions ~100ms, component transitions 200–300ms, page-level 400–1000ms;
enter uses `cubic-bezier(0.215, 0.61, 0.355, 1)` (ease-out), leave uses
`cubic-bezier(0.55, 0.055, 0.675, 0.19)` (ease-in) 🟡. Modals/dropdowns slide-up
+ fade. Never animate for decoration — motion only communicates state change.

## Do / Don't

- **Do** keep one primary blue button per view; secondary actions are default/ghost.
  **Don't** make every CTA blue — a page of blue buttons is a warning sign.
- **Do** express status with a colored Tag (green "In service", gold "Pending",
  red "Failed"). **Don't** recolor whole table rows or cards by status.
- **Do** show explicit empty, loading and error states on every data view.
  **Don't** leave a blank panel when a query returns nothing.
- **Do** put form labels above inputs, single column, with inline validation
  text under the field. **Don't** use placeholder-only labels.
- **Do** use 14px body text, 12px meta, `rgba(0,0,0,.45)` secondary text.
  **Don't** bump body copy to 16px for "readability".
- **Do** use 1px borders (`#f0f0f0` dividers) for hierarchy in lists and cards.
  **Don't** add soft shadows to things that don't float.
- **Do** number wizard steps and mark completed steps blue with a check.
  **Don't** build a multi-step flow without a visible step indicator.
- **Do** keep the dark `#001529` sider menu with white text when you want the
  classic admin look. **Don't** restyle the sider into a pastel sidebar.

## Copy voice

Functional, direct, no marketing adjectives. Labels are nouns, actions are
verbs. Examples: "Are you sure you want to delete this record?" · "3 vehicles
are due for inspection this week." · "Work order created successfully."
