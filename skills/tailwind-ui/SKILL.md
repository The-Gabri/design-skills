---
name: tailwind-ui
description: Build pages and app UIs in the Tailwind UI / Catalyst style — refined, utility-first interfaces with Inter, zinc neutrals, ring-based hairlines, and one restrained accent. Use for dev-tool marketing sites and React-style admin/app shells.
---

# Tailwind UI / Catalyst

Tailwind UI (now Tailwind Plus) is the component library and template collection
by the Tailwind CSS team; **Catalyst** is its React UI kit for application
interfaces. The style covers two modes: crisp **marketing pages** (big tight
type, grid-pattern backgrounds, code snippets) and refined **app UIs**
(monochrome chrome, ringed cards, dense tables). Both share the same tokens.

## Principles

1. **Utility-first thinking.** Design with composable primitives — spacing,
   color, and ring scales — rather than bespoke one-off CSS. If a value isn't
   on the scale, it probably shouldn't exist.
2. **Refined restraint.** One neutral ramp (zinc or slate), one accent hue.
   Depth comes from hairline rings and spacing, not from shadows, gradients,
   or decoration.
3. **Rings, not borders.** Hairlines are `ring-1 ring-inset` (or low-opacity
   borders) so edges stay crisp on any background without shifting layout.
4. **Design in the browser.** Real data in tables, real copy in marketing
   sections, real code in snippets. Components are judged at real content
   density, not in idealized mockups.
5. **Content-first density.** App UI is compact (`text-sm`, tight rows,
   `divide-y` hairlines); marketing is airy (`py-24`, `max-w-7xl`) but never
   empty — every section earns its space with concrete proof (code, stats,
   screenshots).
6. **Dark mode is a first-class citizen.** Every surface, ring, and badge has
   a deliberate `dark:` counterpart; dark isn't an inverted afterthought.

## Color

Neutrals carry the design; a single accent does the talking. 🟡 = cross-
referenced from Catalyst kit sources and documented Tailwind UI examples;
✅ = documented in the official Tailwind CSS palette.

| Token | Hex | Role | Legend |
|---|---|---|---|
| `zinc-50` | `#fafafa` ✅ | app/page background (light) | ✅ |
| `white` | `#ffffff` ✅ | raised surfaces, cards | ✅ |
| `zinc-950` | `#09090b` ✅ | primary text (light), app bg (dark), dark sidebar | ✅ |
| `zinc-900` | `#18181b` ✅ | dark surfaces, monochrome primary button | ✅ |
| `zinc-800` | `#27272a` ✅ | dark elevated surface | ✅ |
| `zinc-600` | `#52525b` ✅ | secondary text (light) | ✅ |
| `zinc-500` | `#71717a` ✅ | muted text, placeholders | ✅ |
| `zinc-200` | `#e4e4e7` ✅ | strong hairlines (light) | ✅ |
| `zinc-950/10` ring | `rgba(9,9,11,.08)` 🟡 | default hairline ring (light) | 🟡 |
| `white/10` ring | `rgba(255,255,255,.10)` 🟡 | default hairline ring (dark) | 🟡 |
| `blue-600` | `#2563eb` ✅ | primary accent, links, eyebrows | ✅ |
| `blue-700` | `#1d4ed8` ✅ | accent hover / emphasis text | ✅ |
| `blue-50` | `#eff6ff` ✅ | accent tint backgrounds | ✅ |
| `emerald-600/700` | `#059669` / `#047857` ✅ | success badges, checks | ✅ |
| `amber-700` | `#b45309` ✅ | warning badges | ✅ |
| `red-600/700` | `#dc2626` / `#b91c1c` ✅ | danger badges, errors | ✅ |

Dark-mode strategy 🟡: use the `dark:` variant (class strategy). Dark app
background is `zinc-950`, surfaces step up the ladder `zinc-950 → zinc-900 →
zinc-800` for depth *without shadows*, and hairlines become
`ring-white/10`. Primary text flips to `white`, secondary to `zinc-400`.

## Typography

- **Typeface:** Inter ✅ (the official Tailwind typeface; tailwindcss.com and
  all Tailwind UI templates ship it). System fallback:
  `ui-sans-serif, system-ui, sans-serif`.
- **Code:** `ui-monospace, SFMono-Regular, Menlo, monospace` ✅.
- **Headings:** `font-semibold` with `tracking-tight` (`-0.025em`) 🟡 — the
  signature Tailwind UI marketing headline. Never bold-black display type.
- **Type scale** 🟡: hero `text-5xl sm:text-6xl`/`text-7xl`; section titles
  `text-3xl sm:text-4xl`; body `text-base`/`text-lg` in `zinc-600`;
  eyebrows `text-sm font-semibold uppercase tracking-wide` in accent color.
- **App UI:** `text-sm` base, table headers `text-xs font-medium uppercase
  tracking-wider text-zinc-500` 🟡; numbers in tables use `tabular-nums` ✅.

## Layout & spacing

- **Container:** `mx-auto max-w-7xl px-4 sm:px-6 lg:px-8` ✅ — the canonical
  Tailwind UI page container. Narrower prose: `max-w-2xl/3xl`.
- **Section rhythm:** `py-24 sm:py-32` for marketing sections 🟡; app content
  `px-4 py-8 sm:px-6 lg:px-8`.
- **Spacing scale:** the default Tailwind scale (4px base: `4, 8, 12, 16,
  20, 24, 32, 48, 64, 96`) ✅. Gaps: `gap-4`–`gap-8` in grids.
- **Radius:** `rounded-lg` for buttons/inputs/cards, `rounded-xl`/`rounded-2xl`
  for large panels, `rounded-full` for pills/avatars 🟡 (Catalyst's two workhorse
  radii are `lg` and `full`).
- **Borders/shadows:** hairline `ring-1 ring-zinc-950/10` (light) /
  `ring-white/10` (dark) instead of `border` where crispness matters 🟡;
  shadows stay subtle — `shadow-sm` on cards, `shadow-lg` reserved for
  dropdowns/modals ✅.
- **Marketing backgrounds:** faint CSS grid or dot patterns
  (`linear-gradient` 1px lines at low opacity, or `radial-gradient` dots) behind
  heroes, plus *one* sparing radial accent glow 🟡 (a documented Tailwind CSS
  docs recipe widely used across Tailwind UI templates).
- **App shell (Catalyst sidebar layout)** 🟡: full-height dark sidebar
  (`zinc-950`/`zinc-900`), nav grouped under small section headings; main
  content sits in a rounded, ringed container on desktop
  (`lg:rounded-lg lg:bg-white lg:shadow-xs lg:ring-1 lg:ring-zinc-950/10`).

## Components

Copy-pasteable Tailwind utility snippets (v3/v4 class names). Pair with
`dark:` variants for dark mode.

### 1. Button

Catalyst's default primary action is **monochrome**, not colored 🟡.

```html
<!-- Primary (monochrome, Catalyst default) -->
<button class="inline-flex items-center gap-2 rounded-lg bg-zinc-950 px-4 py-2 text-sm font-semibold text-white shadow-sm hover:bg-zinc-800 focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-blue-600 dark:bg-white dark:text-zinc-950 dark:hover:bg-zinc-200">
  Get started
</button>

<!-- Accent (marketing CTAs) -->
<button class="inline-flex items-center gap-2 rounded-lg bg-blue-600 px-4 py-2 text-sm font-semibold text-white shadow-sm hover:bg-blue-500 focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-blue-600">
  Start deploying
</button>

<!-- Secondary -->
<button class="inline-flex items-center gap-2 rounded-lg bg-white px-4 py-2 text-sm font-semibold text-zinc-900 ring-1 ring-inset ring-zinc-950/10 hover:bg-zinc-50 dark:bg-white/10 dark:text-white dark:ring-white/10 dark:hover:bg-white/20">
  Read the docs
</button>
```

### 2. Badge

The signature `ring-1 ring-inset` status pill 🟡 (from Tailwind UI's documented
badge examples).

```html
<span class="inline-flex items-center gap-x-1.5 rounded-md bg-emerald-50 px-2 py-1 text-xs font-medium text-emerald-700 ring-1 ring-inset ring-emerald-600/20 dark:bg-emerald-500/10 dark:text-emerald-400 dark:ring-emerald-500/20">
  <span class="size-1.5 rounded-full bg-emerald-500"></span> Live
</span>
<span class="inline-flex items-center rounded-md bg-amber-50 px-2 py-1 text-xs font-medium text-amber-700 ring-1 ring-inset ring-amber-600/20">Building</span>
<span class="inline-flex items-center rounded-md bg-red-50 px-2 py-1 text-xs font-medium text-red-700 ring-1 ring-inset ring-red-600/20">Failed</span>
<span class="inline-flex items-center rounded-md bg-zinc-50 px-2 py-1 text-xs font-medium text-zinc-600 ring-1 ring-inset ring-zinc-500/10">Queued</span>
```

### 3. Card

Ringed, barely-there shadow — never a heavy drop shadow 🟡.

```html
<div class="rounded-xl bg-white p-6 shadow-sm ring-1 ring-zinc-950/10 dark:bg-zinc-900 dark:ring-white/10">
  <h3 class="text-base font-semibold text-zinc-950 dark:text-white">Card title</h3>
  <p class="mt-2 text-sm text-zinc-600 dark:text-zinc-400">Supporting copy in secondary text.</p>
</div>
```

### 4. Table

Dense, refined: uppercase micro-headers, hairline dividers, no zebra striping 🟡.

```html
<div class="overflow-hidden rounded-xl bg-white shadow-sm ring-1 ring-zinc-950/10 dark:bg-zinc-900 dark:ring-white/10">
  <table class="min-w-full divide-y divide-zinc-950/10 dark:divide-white/10">
    <thead>
      <tr>
        <th scope="col" class="px-6 py-3 text-left text-xs font-medium uppercase tracking-wider text-zinc-500">Preview</th>
        <th scope="col" class="px-6 py-3 text-left text-xs font-medium uppercase tracking-wider text-zinc-500">Status</th>
        <th scope="col" class="px-6 py-3 text-right text-xs font-medium uppercase tracking-wider text-zinc-500">Duration</th>
      </tr>
    </thead>
    <tbody class="divide-y divide-zinc-950/5 dark:divide-white/5">
      <tr class="hover:bg-zinc-50 dark:hover:bg-white/5">
        <td class="whitespace-nowrap px-6 py-4 text-sm font-medium text-zinc-950 dark:text-white">pr-482 · add-checkout-flow</td>
        <td class="whitespace-nowrap px-6 py-4"><!-- badge here --></td>
        <td class="whitespace-nowrap px-6 py-4 text-right text-sm tabular-nums text-zinc-500">38s</td>
      </tr>
    </tbody>
  </table>
</div>
```

### 5. Dropdown menu

White panel, ringed, `shadow-lg`; items highlight on hover/focus; selected item
gets a check icon 🟡.

```html
<div class="relative">
  <button class="...trigger...">Filter: All</button>
  <div class="absolute right-0 z-10 mt-2 w-48 origin-top-right rounded-xl bg-white p-1 shadow-lg ring-1 ring-zinc-950/10 focus:outline-none dark:bg-zinc-900 dark:ring-white/10">
    <a href="#" class="flex items-center justify-between rounded-lg px-3 py-2 text-sm text-zinc-950 hover:bg-zinc-100 dark:text-white dark:hover:bg-white/10">
      All statuses
      <svg class="size-4 text-blue-600" viewBox="0 0 20 20" fill="currentColor"><path fill-rule="evenodd" d="M16.7 5.3a1 1 0 010 1.4l-8 8a1 1 0 01-1.4 0l-4-4a1 1 0 011.4-1.4L8 12.6l7.3-7.3a1 1 0 011.4 0z" clip-rule="evenodd"/></svg>
    </a>
    <a href="#" class="block rounded-lg px-3 py-2 text-sm text-zinc-600 hover:bg-zinc-100 dark:text-zinc-300 dark:hover:bg-white/10">Live</a>
  </div>
</div>
```

### 6. Modal / Dialog

Centered panel on a dimmed backdrop; panel is ringed with `sm:rounded-2xl` 🟡.

```html
<div class="fixed inset-0 z-50 flex items-center justify-center bg-zinc-950/50 p-4">
  <div class="w-full max-w-md rounded-2xl bg-white p-6 shadow-xl ring-1 ring-zinc-950/10 dark:bg-zinc-900 dark:ring-white/10">
    <h2 class="text-base font-semibold text-zinc-950 dark:text-white">Delete preview?</h2>
    <p class="mt-2 text-sm text-zinc-600 dark:text-zinc-400">This will permanently remove pr-482 and its database.</p>
    <div class="mt-6 flex justify-end gap-3">
      <button class="rounded-lg px-4 py-2 text-sm font-semibold text-zinc-900 ring-1 ring-inset ring-zinc-950/10 hover:bg-zinc-50">Cancel</button>
      <button class="rounded-lg bg-red-600 px-4 py-2 text-sm font-semibold text-white hover:bg-red-500">Delete</button>
    </div>
  </div>
</div>
```

### 7. Tabs

Underline style for page sections; selected tab gets accent text + accent
2px underline 🟡.

```html
<div class="border-b border-zinc-950/10 dark:border-white/10">
  <nav class="-mb-px flex gap-6" aria-label="Tabs">
    <a href="#" class="border-b-2 border-blue-600 px-1 py-3 text-sm font-semibold text-blue-600">Overview</a>
    <a href="#" class="border-b-2 border-transparent px-1 py-3 text-sm font-medium text-zinc-500 hover:border-zinc-300 hover:text-zinc-700">Activity</a>
    <a href="#" class="border-b-2 border-transparent px-1 py-3 text-sm font-medium text-zinc-500 hover:border-zinc-300 hover:text-zinc-700">Settings</a>
  </nav>
</div>
```

### 8. Form inputs

Rounded, ringed, subtle inner shadow; focus swaps the ring to the accent 🟡.

```html
<label class="block text-sm font-medium text-zinc-950 dark:text-white">Email</label>
<input type="email" placeholder="you@example.com"
  class="mt-2 block w-full rounded-lg bg-white px-3.5 py-2.5 text-sm text-zinc-950 shadow-sm ring-1 ring-inset ring-zinc-950/10 placeholder:text-zinc-400 focus:outline-none focus:ring-2 focus:ring-inset focus:ring-blue-600 dark:bg-white/5 dark:text-white dark:ring-white/10" />
```

### 9. Sidebar (Catalyst app shell)

Dark sidebar, grouped nav with section headings, active item subtly highlighted 🟡.

```html
<div class="flex min-h-screen bg-zinc-950">
  <aside class="hidden w-64 flex-col bg-zinc-950 lg:flex">
    <div class="flex h-16 items-center px-6"><!-- logo --></div>
    <nav class="flex-1 space-y-8 px-4 py-4">
      <div>
        <p class="px-3 text-xs font-semibold uppercase tracking-wider text-zinc-500">Overview</p>
        <a href="#" class="mt-2 flex items-center gap-3 rounded-lg bg-white/10 px-3 py-2 text-sm font-medium text-white">Dashboard</a>
        <a href="#" class="mt-1 flex items-center gap-3 rounded-lg px-3 py-2 text-sm text-zinc-400 hover:bg-white/5 hover:text-white">Previews</a>
      </div>
      <div>
        <p class="px-3 text-xs font-semibold uppercase tracking-wider text-zinc-500">Settings</p>
        <a href="#" class="mt-1 flex items-center gap-3 rounded-lg px-3 py-2 text-sm text-zinc-400 hover:bg-white/5 hover:text-white">Team</a>
      </div>
    </nav>
    <div class="border-t border-white/10 p-4"><!-- user row --></div>
  </aside>
  <main class="flex-1 lg:p-2">
    <div class="min-h-full bg-white lg:rounded-lg lg:shadow-xs lg:ring-1 lg:ring-zinc-950/10 dark:bg-zinc-900">
      <!-- page content -->
    </div>
  </main>
</div>
```

### 10. Alert

Subtle tinted panel with ring — informative, never shouty 🟡.

```html
<div class="flex gap-3 rounded-xl bg-blue-50 p-4 ring-1 ring-inset ring-blue-600/20 dark:bg-blue-500/10 dark:ring-blue-500/20">
  <svg class="size-5 shrink-0 text-blue-600" viewBox="0 0 20 20" fill="currentColor"><path fill-rule="evenodd" d="M18 10a8 8 0 11-16 0 8 8 0 0116 0zm-7-4a1 1 0 11-2 0 1 1 0 012 0zM9 9a1 1 0 000 2v3a1 1 0 001 1h1a1 1 0 100-2v-3a1 1 0 00-1-1H9z" clip-rule="evenodd"/></svg>
  <p class="text-sm text-blue-800 dark:text-blue-200">Preview environments are torn down automatically 24 hours after merge.</p>
</div>
```

## Motion

No signature animation language — keep it subtle and functional: `transition-colors`
(150–200ms, `ease-out`) on hovers; dropdowns/modals fade + scale from 95%
over ~100–200ms (Headless UI style) ⚠️. Respect
`prefers-reduced-motion`.

## Do / Don't

- **Do** use `ring-1 ring-inset` hairlines (`ring-zinc-950/10` light,
  `ring-white/10` dark). **Don't** frame cards with `border-2` or heavy
  `shadow-xl` — depth comes from rings and spacing.
- **Do** keep one accent (blue/indigo) plus semantic hues only where meaning
  demands it (badges, charts). **Don't** rainbow the interface.
- **Do** make app-chrome primary actions monochrome (`zinc-950`/`white`,
  Catalyst default). **Don't** paint every button the accent color inside app UI.
- **Do** write table headers as `text-xs uppercase tracking-wider
  text-zinc-500` with `divide-y` hairlines. **Don't** use zebra-striped rows.
- **Do** lay marketing heroes out asymmetrically (copy + product visual over a
  grid pattern). **Don't** default to centered headline + pill + three cards.
- **Do** put real code, real numbers, and real UI in screenshots and snippets.
  **Don't** ship lorem ipsum or empty state illustrations as content.
- **Do** use the `dark:` variant on every surface, ring, and text color.
  **Don't** ship a light-only page and call it done.

## Copy voice

Direct, developer-to-developer, concrete over clever. Lead with what it does
and a number that proves it.

- "Beautifully designed components, expertly crafted."
- "Production-ready, not prototype-ready."
- "Spin up a full-stack preview in 38 seconds. Tear it down on merge."
