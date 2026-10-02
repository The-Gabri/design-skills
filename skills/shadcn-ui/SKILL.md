---
name: shadcn-ui
description: The shadcn/ui dashboard aesthetic — semantic CSS variables, zinc monochrome, minimal borders, Radix-accessible components. Use for clean admin panels, dashboards, settings pages, and data-heavy SaaS UI.
---

# shadcn/ui

## Principles

1. **Not a component library.** Components are copy-pasted into your codebase and owned outright — `npx shadcn@latest add <component>`, then edit the files directly. You never fight a dependency's API to change a style; you change the source. ✅ official (docs: "This is not a component library. It's a collection of re-usable components that you can copy and paste into your apps.")
2. **Semantic tokens, never raw colors.** Components reference `--background`, `--foreground`, `--primary`, `--muted`, `--border`, `--ring` — never hex. Re-theming means editing variables in `:root`/`.dark`, not touching components. ✅ official (docs/theming)
3. **Engineered neutrality.** The default theme is achromatic zinc: near-black primary actions, hairline borders, muted gray text. It looks intentional before any brand decision is layered on, and brand color is added by changing *one token* (`--primary`), not by decorating every component. 🟡 cross-referenced
4. **Accessibility is inherited from Radix.** Every interactive primitive (Dialog, Dropdown Menu, Tabs, Popover) is built on Radix UI primitives — keyboard navigation, focus trapping, ARIA roles come free. The aesthetic keeps Radix's behavior untouched and only skins it. ✅ official
5. **composability over configuration.** Variants are exposed through `cva` (class-variance-authority) and merged with `cn()` (clsx + tailwind-merge). Adding a state is adding a class string, not learning a prop API. ✅ official
6. **Depth from borders, not shadows.** Surfaces are separated by 1px `--border` hairlines and single-step background shifts (`--card` vs `--muted`). Shadows are `shadow-xs`/`shadow-sm` at most. ✅ official theme defaults, 🟡 cross-referenced

## Color

Everything is a paired surface + `-foreground` token (foreground = the text/icon color on that surface). Light and dark values live in `:root` and `.dark`; dark mode flips the same variable names, no component logic changes. ✅ official (ui.shadcn.com/docs/theming, neutral base)

| Token | Light (oklch / ≈hex) | Dark (oklch / ≈hex) | Role |
|---|---|---|---|
| `--background` | `1 0 0` / `#ffffff` ✅ | `0.145 0 0` / `#0a0a0a` ✅ | page background |
| `--foreground` | `0.145 0 0` / `#0a0a0a` ✅ | `0.985 0 0` / `#fafafa` ✅ | default text |
| `--card` | `1 0 0` / `#ffffff` ✅ | `0.205 0 0` / `#18181b` ✅ | card surfaces |
| `--popover` | `1 0 0` / `#ffffff` ✅ | `0.205 0 0` / `#18181b` ✅ | dropdowns, popovers |
| `--primary` | `0.205 0 0` / `#18181b` 🟡 | `0.922 0 0` / `#fafafa` 🟡 | default Button, selected states |
| `--primary-foreground` | `0.985 0 0` / `#fafafa` ✅ | `0.205 0 0` / `#18181b` ✅ | text on primary |
| `--secondary` | `0.97 0 0` / `#f4f4f5` 🟡 | `0.269 0 0` / `#27272a` 🟡 | secondary fills |
| `--muted` | `0.97 0 0` / `#f4f4f5` 🟡 | `0.269 0 0` / `#27272a` 🟡 | subdued surfaces |
| `--muted-foreground` | `0.556 0 0` / `#71717a` 🟡 | `0.708 0 0` / `#a1a1aa` 🟡 | descriptions, placeholders, helper text |
| `--accent` | `0.97 0 0` / `#f4f4f5` 🟡 | `0.269 0 0` / `#27272a` 🟡 | hover/focus highlights (ghost buttons, menu rows) |
| `--destructive` | `0.577 0.245 27.3` / `#e11d48` 🟡 | `0.704 0.191 22.2` / `#ef4444` 🟡 | errors, destructive actions |
| `--border` | `0.922 0 0` / `#e4e4e7` 🟡 | `1 0 0 / 10%` / `rgba(255,255,255,.1)` ✅ | hairline borders |
| `--input` | `0.922 0 0` / `#e4e4e7` 🟡 | `1 0 0 / 15%` / `rgba(255,255,255,.15)` ✅ | form control borders |
| `--ring` | `0.708 0 0` / `#a1a1aa` 🟡 | `0.556 0 0` / `#71717a` 🟡 | focus rings |
| `--chart-1…5` | orange/teal/blue/amber/lime series ✅ | inverted series ✅ | data visualization |
| `--sidebar` | `0.985 0 0` / `#fafafa` ✅ | `0.205 0 0` / `#18181b` ✅ | sidebar surface |
| `--sidebar-accent` | `0.97 0 0` / `#f4f4f5` 🟡 | `0.269 0 0` / `#27272a` 🟡 | sidebar hover/selected row |

**Zinc base palette** (the tokens above are these, in oklch). ✅ official Tailwind scale:

`#fafafa` zinc-50 · `#f4f4f5` zinc-100 · `#e4e4e7` zinc-200 · `#d4d4d8` zinc-300 · `#a1a1aa` zinc-400 · `#71717a` zinc-500 · `#52525b` zinc-600 · `#3f3f46` zinc-700 · `#27272a` zinc-800 · `#18181b` zinc-900 · `#09090b` zinc-950

Key facts: the default theme has **no signature chromatic accent** — primary is near-black in light mode and near-white in dark mode. The only real color is `--destructive` red. Chart series is the one place saturated color lives.

## Typography

- **Default typeface: Geist** (Sans + Mono), current official style presets. 🟡 cross-referenced — older themes and many implementations use **Inter**; either reads as authentic, but do not mix them. (For a plain-CSS build, Inter is the free, safe pick.)
- **Mono (Geist Mono / ui-monospace) for identity chrome:** badges, kbd hints, IDs, slugs, code, timestamps, numeric metadata. ✅ documented convention
- Headings: `font-semibold` (600), `tracking-tight` (`-0.025em`); body at weight 400/500, sentence case everywhere — no all-caps eyebrows, hierarchy comes from size/weight not casing. 🟡
- Data tables: `font-variant-numeric: tabular-nums` on numeric columns. ✅ documented
- Scale: `text-sm` (14px) is the UI default body size; page titles `text-2xl`/`text-3xl`; `text-xs` for muted descriptions. 🟡

## Layout & spacing

- **Radius is one variable.** `--radius: 0.625rem` (10px) ✅ official, with derived scale: `rounded-sm` = radius×0.6, `rounded-md` = radius×0.8, `rounded-lg` = the base, `rounded-xl` = ×1.4, `rounded-2xl` = ×1.8. Change one token, reshape the whole system. In practice: buttons/inputs/badges = `rounded-md` (6–8px), cards/popovers/dialogs = `rounded-xl`/`rounded-lg`.
- **Page shell:** `mx-auto max-w-6xl` / `max-w-7xl`, `px-4 sm:px-6 lg:px-8`, section gaps `gap-6`/`gap-8`. 🟡
- **Sidebar app layout:** fixed left sidebar (~`w-64`, collapsible to icon rail), main content scrolls. Sidebar has its own tokens (`--sidebar`, `--sidebar-accent`, `--sidebar-border`). ✅ official sidebar tokens
- **Borders:** 1px solid `--border` everywhere — cards, tables, menus, separators, layout dividers. `--border` is near-invisible in light mode by design. ✅
- **Focus:** `:focus-visible { outline: 2px solid var(--ring); outline-offset: 2px; }` — focus rings are a visible, required part of the aesthetic. ✅
- **Shadows:** `shadow-xs` / `shadow-sm` only; dropdowns and dialogs may use `shadow-lg` for the overlay layer. 🟡
- **Dark mode:** `.dark` class on `<html>` flips every token. Never duplicate component markup for dark mode. ✅ official

## Components

All snippets assume the tokens above are defined. Plain HTML/CSS versions of the real primitives.

### Button — 6 variants ✅ official variants

```html
<button class="btn">Default</button>
<button class="btn btn-secondary">Secondary</button>
<button class="btn btn-outline">Outline</button>
<button class="btn btn-ghost">Ghost</button>
<button class="btn btn-destructive">Delete account</button>
<button class="btn btn-link">Cancel</button>
```

```css
.btn {
  display: inline-flex; align-items: center; justify-content: center; gap: .5rem;
  height: 2.25rem; padding: 0 1rem; border-radius: calc(var(--radius) - 2px);
  font-size: .875rem; font-weight: 500; line-height: 1;
  background: var(--primary); color: var(--primary-foreground); border: 1px solid transparent;
  cursor: pointer; transition: background-color .15s ease, color .15s ease;
  white-space: nowrap;
}
.btn:hover { background: color-mix(in srgb, var(--primary) 90%, transparent); }
.btn:focus-visible { outline: 2px solid var(--ring); outline-offset: 2px; }
.btn:disabled { opacity: .5; pointer-events: none; }
.btn-secondary { background: var(--secondary); color: var(--secondary-foreground); }
.btn-outline { background: transparent; color: var(--foreground); border-color: var(--border); }
.btn-outline:hover { background: var(--accent); color: var(--accent-foreground); }
.btn-ghost { background: transparent; color: var(--foreground); }
.btn-ghost:hover { background: var(--accent); }
.btn-destructive { background: var(--destructive); color: var(--primary-foreground); }
.btn-link { background: none; color: var(--primary); padding: 0; height: auto; text-decoration: none; }
.btn-link:hover { text-decoration: underline; }
.btn-sm { height: 2rem; padding: 0 .75rem; font-size: .75rem; }
.btn-lg { height: 2.5rem; padding: 0 2rem; }
.btn-icon { width: 2.25rem; padding: 0; }
```

### Badge

```html
<span class="badge">Default</span>
<span class="badge badge-secondary">Secondary</span>
<span class="badge badge-outline">Outline</span>
<span class="badge badge-destructive">Overdue</span>
```

```css
.badge {
  display: inline-flex; align-items: center; gap: .25rem;
  padding: .125rem .625rem; border-radius: 9999px;
  font-size: .75rem; font-weight: 600; line-height: 1.25rem;
  background: var(--primary); color: var(--primary-foreground);
  border: 1px solid transparent; white-space: nowrap;
}
.badge-secondary { background: var(--secondary); color: var(--secondary-foreground); }
.badge-outline { background: transparent; color: var(--foreground); border-color: var(--border); }
.badge-destructive { background: var(--destructive); color: var(--primary-foreground); }
```

### Card

```html
<article class="card">
  <div class="card-header">
    <div>
      <h3 class="card-title">Total revenue</h3>
      <p class="card-desc">Year-over-year growth</p>
    </div>
    <button class="badge badge-secondary">+12.4%</button>
  </div>
  <div class="card-content"><p class="stat">$128,400</p></div>
  <div class="card-footer"><p class="muted">Updated 2 minutes ago</p></div>
</article>
```

```css
.card {
  background: var(--card); color: var(--card-foreground);
  border: 1px solid var(--border); border-radius: var(--radius);
  padding: 1.5rem; box-shadow: 0 1px 2px rgb(0 0 0 / .05);
  display: flex; flex-direction: column; gap: 1rem;
}
.card-header { display: flex; justify-content: space-between; align-items: flex-start; }
.card-title { font-size: 1rem; font-weight: 600; letter-spacing: -0.01em; margin: 0; }
.card-desc { font-size: .875rem; color: var(--muted-foreground); margin: .25rem 0 0; }
.card-footer { border-top: 1px solid var(--border); padding-top: .75rem; }
.muted { color: var(--muted-foreground); font-size: .875rem; margin: 0; }
```

### Input (+ Label)

```html
<div class="field">
  <label class="label" for="team">Workspace name</label>
  <input class="input" id="team" type="text" placeholder="acme-inc" />
  <p class="hint">Used in URLs and billing receipts.</p>
</div>
```

```css
.field { display: flex; flex-direction: column; gap: .375rem; }
.label { font-size: .875rem; font-weight: 500; color: var(--foreground); }
.input {
  height: 2.25rem; padding: 0 .75rem; border-radius: calc(var(--radius) - 2px);
  border: 1px solid var(--input); background: transparent; color: var(--foreground);
  font-size: .875rem; width: 100%;
}
.input::placeholder { color: var(--muted-foreground); }
.input:focus-visible { outline: 2px solid var(--ring); outline-offset: 0; border-color: var(--ring); }
.hint { font-size: .75rem; color: var(--muted-foreground); margin: 0; }
```

### Table

```html
<div class="table-wrap">
  <table class="table">
    <thead><tr><th>Name</th><th>Status</th><th class="num">MRR</th></tr></thead>
    <tbody>
      <tr><td class="strong">Acme Inc</td><td><span class="badge badge-secondary">Active</span></td><td class="num">$4,200</td></tr>
      <tr><td class="strong">Globex</td><td><span class="badge badge-destructive">Past due</span></td><td class="num">$860</td></tr>
    </tbody>
  </table>
</div>
```

```css
.table-wrap { border: 1px solid var(--border); border-radius: var(--radius); overflow: hidden; }
.table { width: 100%; border-collapse: collapse; font-size: .875rem; background: var(--card); }
.table th {
  text-align: left; padding: .75rem 1rem; font-weight: 500; font-size: .75rem;
  color: var(--muted-foreground); border-bottom: 1px solid var(--border);
  text-transform: none; letter-spacing: 0;
}
.table td { padding: .875rem 1rem; border-bottom: 1px solid var(--border); }
.table tr:last-child td { border-bottom: 0; }
.table tbody tr:hover { background: color-mix(in srgb, var(--muted) 50%, transparent); }
.table .num { text-align: right; font-variant-numeric: tabular-nums; }
.table .strong { font-weight: 500; }
```

### Tabs

```html
<div class="tabs" role="tablist">
  <button class="tab is-active" role="tab" aria-selected="true">Overview</button>
  <button class="tab" role="tab" aria-selected="false">Analytics</button>
  <button class="tab" role="tab" aria-selected="false">Reports</button>
</div>
```

```css
.tabs { display: inline-flex; gap: .25rem; background: var(--muted); padding: .25rem; border-radius: calc(var(--radius) - 2px); }
.tab {
  padding: .375rem .875rem; border: 0; background: transparent; cursor: pointer;
  font-size: .875rem; font-weight: 500; color: var(--muted-foreground);
  border-radius: calc(var(--radius) - 4px); transition: all .15s ease;
}
.tab:hover { color: var(--foreground); }
.tab.is-active { background: var(--background); color: var(--foreground); box-shadow: 0 1px 2px rgb(0 0 0 / .08); }
```

### Dropdown Menu

```html
<div class="menu-wrap">
  <button class="btn btn-outline btn-icon" id="menuBtn" aria-haspopup="menu" aria-expanded="false">
    <svg><!-- chevron-down icon --></svg>
  </button>
  <div class="menu" role="menu" hidden>
    <p class="menu-label">My account</p>
    <button class="menu-item" role="menuitem">Profile <kbd>⌘P</kbd></button>
    <button class="menu-item" role="menuitem">Billing <kbd>⌘B</kbd></button>
    <div class="menu-sep"></div>
    <button class="menu-item danger" role="menuitem">Log out</button>
  </div>
</div>
```

```css
.menu-wrap { position: relative; display: inline-block; }
.menu {
  position: absolute; right: 0; top: calc(100% + .5rem); min-width: 13rem; z-index: 50;
  background: var(--popover); color: var(--popover-foreground);
  border: 1px solid var(--border); border-radius: var(--radius);
  padding: .25rem; box-shadow: 0 10px 30px rgb(0 0 0 / .12);
}
.menu-label { font-size: .75rem; font-weight: 600; color: var(--muted-foreground); padding: .375rem .5rem; margin: 0; }
.menu-item {
  display: flex; align-items: center; justify-content: space-between; width: 100%;
  padding: .5rem; border: 0; background: transparent; cursor: pointer;
  font-size: .875rem; border-radius: calc(var(--radius) - 4px); color: inherit; gap: 1rem;
}
.menu-item:hover, .menu-item:focus-visible { background: var(--accent); color: var(--accent-foreground); outline: none; }
.menu-item.danger { color: var(--destructive); }
.menu-item kbd {
  font-family: ui-monospace, monospace; font-size: .6875rem; color: var(--muted-foreground);
  background: var(--muted); border-radius: .25rem; padding: .125rem .375rem;
}
.menu-sep { height: 1px; background: var(--border); margin: .25rem -.25rem; }
```

### Dialog

```html
<div class="dialog-overlay" id="dialogOverlay" hidden>
  <div class="dialog" role="dialog" aria-modal="true" aria-labelledby="dialogTitle">
    <h2 class="dialog-title" id="dialogTitle">Invite team member</h2>
    <p class="dialog-desc">They'll get an email with access to this workspace.</p>
    <div class="field">
      <label class="label" for="email">Email</label>
      <input class="input" id="email" type="email" placeholder="teammate@acme.com" />
    </div>
    <div class="dialog-footer">
      <button class="btn btn-outline">Cancel</button>
      <button class="btn">Send invite</button>
    </div>
  </div>
</div>
```

```css
.dialog-overlay {
  position: fixed; inset: 0; z-index: 100; display: grid; place-items: center; padding: 1rem;
  background: rgb(0 0 0 / .5);
}
.dialog {
  width: 100%; max-width: 28rem; background: var(--background); color: var(--foreground);
  border: 1px solid var(--border); border-radius: var(--radius);
  padding: 1.5rem; box-shadow: 0 25px 60px rgb(0 0 0 / .25);
  display: flex; flex-direction: column; gap: 1rem;
}
.dialog-title { font-size: 1.125rem; font-weight: 600; letter-spacing: -.015em; margin: 0; }
.dialog-desc { font-size: .875rem; color: var(--muted-foreground); margin: -.5rem 0 0; }
.dialog-footer { display: flex; justify-content: flex-end; gap: .5rem; }
```

### Sidebar navigation

```html
<aside class="sidebar">
  <p class="sidebar-group">Workspace</p>
  <nav>
    <a class="side-item is-active" href="#"><svg><!-- icon --></svg>Overview</a>
    <a class="side-item" href="#"><svg><!-- icon --></svg>Customers</a>
    <a class="side-item" href="#"><svg><!-- icon --></svg>Billing</a>
  </nav>
</aside>
```

```css
.sidebar { width: 16rem; background: var(--sidebar); border-right: 1px solid var(--sidebar-border); padding: 1rem .75rem; }
.sidebar-group { font-size: .75rem; font-weight: 500; color: var(--muted-foreground); padding: 0 .75rem; margin: 0 0 .5rem; }
.side-item {
  display: flex; align-items: center; gap: .75rem; padding: .5rem .75rem;
  border-radius: calc(var(--radius) - 2px); font-size: .875rem; font-weight: 500;
  color: var(--sidebar-foreground); text-decoration: none;
}
.side-item svg { width: 1rem; height: 1rem; opacity: .7; }
.side-item:hover { background: var(--sidebar-accent); }
.side-item.is-active { background: var(--sidebar-accent); color: var(--sidebar-accent-foreground); }
```

### Separator

```html
<div class="separator" role="separator"></div>
```

```css
.separator { height: 1px; background: var(--border); margin: 1rem 0; }
```

## Motion

Minimal by design: 150ms ease color transitions on hover (buttons, rows, menu items); dialogs/dropdowns use a short fade + slight scale/zoom-in on mount (the library ships `animate-in fade-in-0 zoom-in-95` semantics). No signature easing curve or choreography — if in doubt, do less. ✅ behavior per Radix primitives, 🟡 timing values

## Do / Don't

- **Do** re-theme by editing `--primary` / `--background` / `--radius` in `:root` and `.dark` — the whole app follows.
  **Don't** fork component files to change colors; you fork them to change structure or behavior.
- **Do** use `text-muted-foreground` for descriptions, placeholders, table headers, helper text.
  **Don't** invent a third gray for "subtle text" — muted-foreground is the only one.
- **Do** keep the near-black (light) / near-white (dark) default button as the single primary CTA per view.
  **Don't** color the primary button with a brand color and also keep it black somewhere else — pick one `--primary` per theme.
- **Do** put the destructive red only on irreversible actions ("Delete account", "Remove member") and their confirmation dialogs.
  **Don't** use red for warnings, highlights, or marketing emphasis.
- **Do** give every focusable element a visible ring (`outline: 2px solid var(--ring)` on `:focus-visible`).
  **Don't** strip focus rings "because they look noisy" — they're part of the look.
- **Do** separate surfaces with 1px `--border` hairlines and one background step.
  **Don't** stack shadows for depth — the system reads "flat with hairlines", not "elevated cards".

## Copy voice

Terse product-UI voice, sentence case, no marketing adjectives: "Invite team member", "Updated 2 minutes ago", "No results found." — the interface describes itself and gets out of the way.
