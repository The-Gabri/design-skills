---
name: vanilla-framework
description: Canonical's Vanilla framework style — the Ubuntu design system: white pages, Ubuntu orange CTAs, Canonical aubergine strips, Ubuntu font. Use for clean, accessible, "boring-on-purpose" corporate open-source pages.
---

# Vanilla Framework (Canonical / Ubuntu)

## Principles

1. **Predictable over clever.** Vanilla is "boring technology" for the web: standard components that behave the way users expect. Novelty is a bug, not a feature.
2. **Content first, decoration never.** Color is supportive, not decorative — the docs say most interfaces should be understandable in grayscale alone. If a flourish doesn't serve hierarchy or state, remove it.
3. **Accessible by default.** Minimum WCAG 2.2 Level AA contrast (4.5:1 for text/UI). Everything is keyboard-operable; Vanilla ships `prefers-reduced-motion` handling out of the box.
4. **Lightweight and composable.** Import the whole framework or just the parts you need. Ship CSS, not JS frameworks, wherever possible.
5. **Ubuntu brand voice.** Precise, reliable, free. Copy is plain-spoken and confident, never hypey — "Linux for human beings" energy.
6. **Baseline discipline.** All text sits on a strict `0.5rem` baseline grid; spacing is always a multiple of the 8px unit. The page feels calm because the math is strict.

## Color

Official tokens from Vanilla's `$settings_colors` (✅ = documented on vanillaframework.io):

| Token | Hex | Role |
|---|---|---|
| `$color-x-light` ✅ | `#ffffff` | Page background |
| `$color-light` ✅ | `#f7f7f7` | Subtle surfaces, alternating strips |
| `$color-mid-x-light` ✅ | `#e5e5e5` | Hairline borders, dividers |
| `$color-mid-light` ✅ | `#d9d9d9` | Disabled / stronger borders |
| `$color-mid-dark` ✅ | `#666666` | Muted / secondary text |
| `$color-dark` ✅ | `#111111` | Primary text |
| `$color-x-dark` ✅ | `#000000` | Code blocks, deepest contrast |
| `$color-brand` ✅ | `#e95420` | Ubuntu orange — primary CTAs only |
| `$color-link` ✅ | `#0066cc` | Links |
| `$color-negative` ✅ | `#c7162b` | Errors, destructive actions |
| `$color-caution` ✅ | `#f99b11` | Warnings |
| `$color-positive` ✅ | `#0e8420` | Success states |
| `$color-information` ✅ | `#24598f` | Info notifications |
| `$color-accent` ✅ | `#0f95a1` | Rare accent |
| Canonical aubergine 🟡 | `#772953` | Brand secondary — dark strips, footers, dark navigation (cross-referenced from the Canonical brand palette; ubuntu.com used it for nav/footer) |

Rules of use: body text is `#111` on `#fff`; orange appears only on CTAs and the logo mark — never as body text, never as decoration. Links are always `#06c` (not orange). Status colors only inside notifications, form validation, and badges.

## Typography

- **Primary:** the Ubuntu font family — `'Ubuntu', Arial, 'libra sans', sans-serif` ✅ (Google Fonts hosts it: family=Ubuntu). "All Ubuntu sites and applications should use the Ubuntu font."
- **Code:** `'Ubuntu Mono', Consolas, Monaco, Courier, monospace` ✅.
- Base size `1rem`, body line-height `1.5`, everything nudged onto the `0.5rem` baseline grid ✅.
- Weights are distinctive: display headings `100`, `h1`/`h3`/`h5` bold `550` (not 600/700), `h2` light `180`, `h4` `275`, `h6` regular `400` ✅. Headings are short, sentence-case, and unadorned — no letterspacing games, no gradient text.

## Layout & spacing

- **Grid:** 12-column responsive grid; content max-width ~75rem with generous gutters 🟡.
- **Spacing unit:** `$sp-unit: 8px` (`.5rem`) — all spacing is a multiple or fraction of it ✅.
- **Signature rhythm:** `$spv--strip-regular: 4rem` and `$spv--strip-deep: 6rem` vertical padding on strips — page sections breathe ✅. Horizontal: `$sph--large: 1rem`, `$sph--x-large: 1.5rem` ✅.
- **Radius:** `.125rem` (2px) on buttons and cards — effectively square; large rounded corners break the look 🟡.
- **Borders over shadows.** Hairline `1px #e5e5e5` rules separate things; drop shadows are near-absent.
- **Strips** (`.p-strip`) are the signature section device: alternate white / `#f7f7f7` / dark (`#111` or aubergine) full-width bands down the page ✅.

## Components

### 1. Navigation (dark)

```html
<nav class="p-navigation" aria-label="Main">
  <div class="p-navigation__row">
    <div class="p-navigation__banner">
      <a class="p-navigation__link" href="#" aria-label="Home">
        <svg width="32" height="32" viewBox="0 0 32 32" aria-hidden="true">
          <circle cx="16" cy="16" r="13" fill="none" stroke="#e95420" stroke-width="3"/>
          <circle cx="16" cy="16" r="4" fill="#e95420"/>
        </svg>
      </a>
    </div>
    <ul class="p-navigation__links">
      <li class="p-navigation__link"><a href="#">Products</a></li>
      <li class="p-navigation__link"><a href="#">Pricing</a></li>
      <li class="p-navigation__link"><a href="#">Docs</a></li>
    </ul>
  </div>
</nav>
```

```css
.p-navigation { background: #772953; color: #fff; }
.p-navigation__row { max-width: 75rem; margin: 0 auto; display: flex; align-items: center; gap: 2rem; padding: 0 1.5rem; }
.p-navigation__links { display: flex; gap: 1.5rem; list-style: none; margin: 0; padding: 0; }
.p-navigation__link a { color: #fff; text-decoration: none; font-size: .875rem; padding: 1rem 0; display: block; }
.p-navigation__link a:hover { color: #e95420; }
```

### 2. Buttons

```html
<button class="p-button--brand">Get started</button>
<button class="p-button--base">Read the docs</button>
<button class="p-button--negative">Delete</button>
```

```css
[class^="p-button"] { font-family: 'Ubuntu', sans-serif; font-size: 1rem; padding: .5rem 1.5rem; border: 1px solid transparent; border-radius: .125rem; cursor: pointer; }
.p-button--brand { background: #e95420; color: #fff; }
.p-button--brand:hover { background: #c7441a; }
.p-button--base { background: transparent; color: #111; border-color: #666; }
.p-button--base:hover { background: #f7f7f7; }
.p-button--negative { background: #c7162b; color: #fff; }
```

Buttons are rectangular with 2px radius; brand buttons are always solid orange with white text.

### 3. Strip / hero section

```html
<section class="p-strip">
  <div class="p-strip__row">
    <h1>Kubernetes at the edge, the Ubuntu way</h1>
    <p class="p-heading--5">One command to a production-ready cluster.</p>
    <a class="p-button--brand" href="#">Get started</a>
  </div>
</section>
```

```css
.p-strip { padding: 4rem 0; background: #fff; }
.p-strip--light { background: #f7f7f7; }
.p-strip--dark { background: #111; color: #fff; }
.p-strip--aubergine { background: #772953; color: #fff; }
.p-strip__row { max-width: 75rem; margin: 0 auto; padding: 0 1.5rem; }
.p-strip--deep { padding: 6rem 0; }
```

### 4. Cards

```html
<article class="p-card">
  <h3 class="p-card__title">Secure by default</h3>
  <p>Strict confinement and automatic security updates on every node.</p>
  <a href="#">Learn more &rsaquo;</a>
</article>
```

```css
.p-card { border-top: 3px solid #e95420; padding: 1rem 1.5rem 1.5rem; background: #fff; }
.p-card__title { font-weight: 550; margin: 0 0 .5rem; }
.p-card a { color: #06c; text-decoration: none; }
```

The colored top border on cards is a classic Vanilla detail — orange for default, or a status color.

### 5. Forms

Labels sit above inputs; validation messages use the status colors.

```html
<form>
  <label for="email">Work email</label>
  <input id="email" type="email" placeholder="you@company.com" required>
  <p class="p-form-validation__message is-error">Enter a valid email address.</p>
  <button class="p-button--brand" type="submit">Download</button>
</form>
```

```css
label { display: block; font-weight: 550; margin-bottom: .25rem; }
input[type="email"], input[type="text"], textarea {
  width: 100%; max-width: 24rem; padding: .5rem; font: inherit;
  border: 1px solid #666; border-radius: .125rem;
}
input:focus { outline: 2px solid #06c; outline-offset: 1px; }
.p-form-validation__message.is-error { color: #c7162b; font-size: .875rem; }
```

### 6. Code block

```html
<pre class="p-code-snippet"><code>sudo snap install lattice --classic
lattice init --ha</code></pre>
```

```css
.p-code-snippet { background: #111; color: #fff; font-family: 'Ubuntu Mono', monospace; padding: 1rem 1.5rem; border-radius: .125rem; overflow-x: auto; }
```

### 7. Tabs

```html
<div class="p-tabs" role="tablist" aria-label="Setup steps">
  <button class="p-tabs__item" role="tab" aria-selected="true">Install</button>
  <button class="p-tabs__item" role="tab" aria-selected="false">Configure</button>
  <button class="p-tabs__item" role="tab" aria-selected="false">Scale</button>
</div>
```

```css
.p-tabs { display: flex; border-bottom: 1px solid #e5e5e5; }
.p-tabs__item { background: none; border: 0; font: inherit; padding: .5rem 1rem; cursor: pointer; color: #666; border-bottom: 3px solid transparent; margin-bottom: -1px; }
.p-tabs__item[aria-selected="true"] { color: #111; border-bottom-color: #e95420; font-weight: 550; }
```

Active tab = orange 3px underline, no pills, no background fill.

### 8. Notifications

```html
<div class="p-notification--information">
  <p class="p-notification__content">Ubuntu 24.04.3 LTS is now available.</p>
</div>
<div class="p-notification--positive">
  <p class="p-notification__content">Deployment succeeded on 3 nodes.</p>
</div>
```

```css
[class^="p-notification"] { border: 1px solid #e5e5e5; border-left: 4px solid; padding: .75rem 1rem; margin-bottom: 1rem; background: #fff; }
.p-notification--information { border-left-color: #24598f; }
.p-notification--positive { border-left-color: #0e8420; }
.p-notification--caution { border-left-color: #f99b11; }
.p-notification--negative { border-left-color: #c7162b; }
```

### 9. Footer strip

```html
<footer class="p-strip--dark">
  <div class="p-strip__row p-footer">
    <p>&copy; 2026 Canonical Ltd. Ubuntu and Canonical are registered trademarks.</p>
  </div>
</footer>
```

Footer is always dark (`#111` or aubergine), with muted `#cdcdcd`-ish link columns and a plain copyright line.

## Motion

Vanilla barely moves — animation is functional, never decorative. Official settings ✅: durations `snap .1s`, `fast .165s`, `brisk .333s`, `slow .5s`, `sleepy 1s`; easing `out: cubic-bezier(.215, .61, .355, 1)` and `in: cubic-bezier(.55, .055, .675, .19)`. Buttons get a `fast` background-color transition on hover; accordions/tabs use `brisk`. `prefers-reduced-motion` disables everything.

## Do / Don't

- **Do** keep pages overwhelmingly white with `#111` text; let orange and aubergine carry all the brand weight.
- **Don't** use gradients, glassmorphism, or drop shadows — Vanilla pages are flat and proud of it.
- **Do** give sections 4–6rem of vertical strip padding; whitespace is the main luxury.
- **Don't** round corners beyond 2px — chunky rounded cards read as a different framework.
- **Do** mark the active tab/nav item with the 3px orange underline, not a filled pill.
- **Don't** color body text orange or use orange for links — links are `#06c`, orange is for CTAs.
- **Do** left-align hero content; centered heroes with floating badges are not the Vanilla way.
- **Don't** add emoji as icons; Vanilla uses simple geometric SVGs or text.
- **Do** write short, sentence-case headings with no trailing punctuation.

## Copy voice (for brand styles)

Canonical's tone is plain, confident, and technical without jargon: "precise, reliable and free." Short declarative sentences. Features are stated as facts, not promises. No exclamation marks in product copy, no "revolutionary."

Example strings:

- "One command to a production-ready Kubernetes cluster. No YAML required."
- "Free for personal and small-scale commercial use. Always will be."
- "Security updates for 12 years, on every architecture you ship."
