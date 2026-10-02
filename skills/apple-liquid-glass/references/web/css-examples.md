# Apple-style CSS examples (apple.com / Liquid Glass era)

Snippets copy-pasteable as-is for Apple-style websites. All code comments in English. Each snippet carries its verification mark and a "when to use it".

**Legend:** ✅ standard verified technique · 🟡 consistently documented · ⚠️ irregular or unverified support.

## 0. Shared base: web tokens ✅

**When to use it:** at the start of any Apple-style page. Defines the system font stack, the light/dark semantic colors, and the base radius. Everything else hangs off it.

```css
:root {
  /* ✅ color-scheme tells the browser the active mode: adapts forms,
     scrollbars, and makes light-dark() work */
  color-scheme: light dark;

  /* 🟡 system font stack (from references/system/tokens.md):
     on Apple devices it resolves to San Francisco */
  --font: -apple-system, BlinkMacSystemFont, "SF Pro Text", "SF Pro Display",
           "Helvetica Neue", system-ui, sans-serif;

  /* ✅ semantic colors with light-dark(): one value serves both modes */
  --blue:      light-dark(#007AFF, #0A84FF); /* systemBlue: primary action */
  --bg:        light-dark(#FFFFFF, #000000); /* systemBackground */
  --bg-2:      light-dark(#F5F5F7, #1C1C1E); /* apple.com-style section gray */
  --text:      light-dark(#1D1D1F, #F5F5F7); /* label */
  --text-2:    light-dark(#6E6E73, #98989D); /* secondaryLabel */
  --separator: light-dark(rgba(60,60,67,.29), rgba(84,84,88,.6));

  --radius: 24px; /* generous Apple-style card radius */
}

body {
  font-family: var(--font);
  background: var(--bg);
  color: var(--text);
  margin: 0;
  -webkit-font-smoothing: antialiased; /* crisp text on macOS/iOS */
}
```

## 1. Full-screen hero, apple.com style ✅

**When to use it:** product or launch page. One product, one message, total attention: huge name + tagline + CTAs + centered product photo. Nothing else.

```html
<header class="hero hero--dark">
  <div class="hero-content">
    <h1 class="hero-title">iPhone Air</h1>
    <p class="hero-tagline">The thinnest iPhone ever.<br>Power on another level.</p>
    <div class="hero-ctas">
      <a class="cta-solid" href="#">Buy</a>
      <a class="cta-text" href="#">Learn more ›</a>
    </div>
  </div>
  <!-- Real product photo in full color: the scene's protagonist.
       width/height prevent layout jumps; the path is your final file. -->
  <img class="hero-product"
       src="./img/iphone-air.png"
       alt="iPhone Air in profile, sky blue"
       width="1200" height="800"
       decoding="async" fetchpriority="high">
</header>
```

```css
.hero {
  /* ✅ 100svh discounts the browser bar on mobile;
     with 100vh part of the hero would be covered on iOS/Android */
  min-height: 100svh;
  display: grid;
  place-items: center;
  align-content: center;
  gap: clamp(1.5rem, 4vw, 3rem);
  /* leaves room above for the fixed nav (48px) + air */
  padding: calc(48px + 3rem) 1.5rem 4rem;
  text-align: center;
}

.hero--dark { background: #000; color: #F5F5F7; }
.hero--dark .hero-tagline { color: #A1A1A6; }

.hero-title {
  margin: 0;
  font-size: clamp(3rem, 1.75rem + 5.5vw, 6rem); /* 48px → 96px, fluid */
  font-weight: 700;
  letter-spacing: -0.02em;  /* negative tracking in display only */
  line-height: 1.05;        /* tight leading */
  text-wrap: balance;       /* ✅ spreads the headline over balanced lines */
}

.hero-tagline {
  margin: 0;
  font-size: clamp(1.3125rem, 1.125rem + 0.9vw, 1.75rem); /* 21px → 28px */
  line-height: 1.35;
  color: var(--text-2);
}

.hero-ctas {
  display: flex;
  gap: 1.75rem;
  justify-content: center;
  align-items: center;
  flex-wrap: wrap;
  margin-top: 0.5rem;
}

/* Solid CTA: the screen's only accent color */
.cta-solid {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  min-height: 44px;          /* ✅ minimum touch target */
  padding: 0 1.75rem;
  border-radius: 999px;      /* pill */
  background: var(--blue);
  color: #fff;
  font-size: 1.0625rem;
  font-weight: 600;
  text-decoration: none;
}
.cta-solid:hover { filter: brightness(1.08); }

/* apple.com-style text CTA: "Buy ›" without a loud button */
.cta-text {
  color: var(--blue);
  font-size: 1.0625rem;
  text-decoration: none;
}
.cta-text:hover { text-decoration: underline; }

.hero-product {
  width: min(100%, 900px);
  height: auto;
  margin-top: 1rem;
}
```

## 2. Fluid type scale with `clamp()` ✅

**When to use it:** define the headline sizes for the whole page/landing at once. Display scales fluidly with the viewport; body barely (like apple.com).

```css
:root {
  /* Headlines: display grows a lot, lower levels barely move.
     Formula: clamp(min, base + viewport-scale, max). */
  --text-display:  clamp(3rem, 1.75rem + 5.5vw, 6rem);      /* 48 → 96px: hero */
  --text-title:   clamp(2rem, 1.5rem + 2.5vw, 3.5rem);     /* 32 → 56px: sections */
  --text-title-2: clamp(1.5rem, 1.25rem + 1.25vw, 2.125rem);/* 24 → 34px: subsections */
  --text-lead:clamp(1.3125rem, 1.125rem + 0.9vw, 1.75rem); /* 21 → 28px: taglines */
  --text-body:   clamp(1rem, 0.95rem + 0.25vw, 1.0625rem); /* 16 → 17px: paragraphs */

  --leading-tight: 1.05;  /* display */
  --leading-title: 1.15;  /* section titles */
  --leading-body: 1.5;   /* paragraphs: air to read */
}

/* Ready-to-use utility classes */
.display   { font-size: var(--text-display);   font-weight: 700;
              letter-spacing: -0.02em; line-height: var(--leading-tight);
              text-wrap: balance; }
.title     { font-size: var(--text-title);    font-weight: 700;
              letter-spacing: -0.015em; line-height: var(--leading-title);
              text-wrap: balance; }
.title-2   { font-size: var(--text-title-2);  font-weight: 600;
              letter-spacing: -0.01em;  line-height: var(--leading-title); }
.lead      { font-size: var(--text-lead); line-height: 1.35;
              color: var(--text-2); }
.body      { font-size: var(--text-body);    line-height: var(--leading-body); }

/* ✅ No breakpoints: one fluid value replaces 3 media queries.
   Skill rule: text styles, not loose fixed sizes. */
```

## 3. Basic scroll storytelling ✅

**When to use it:** launch page with "one idea per screen": full-viewport sections that succeed each other on scroll, with alternating color blocks (black / `#F5F5F7` / white). Never hijack the user's scroll.

### 3A. Viewport scenes with scroll-snap (pure CSS) ✅

```html
<main class="scenes">
  <section class="scene scene--dark">
    <h2 class="title">Design.<br>Aerospace-grade titanium.</h2>
    <p class="lead">The thinnest iPhone we've ever made.</p>
  </section>
  <section class="scene scene--light">
    <h2 class="title">Camera.<br>48 MP that sees in the dark.</h2>
    <p class="lead">Sharp photos even when there's no light.</p>
  </section>
  <section class="scene">
    <h2 class="title">A19 Pro chip.<br>Power without breaking a sweat.</h2>
    <p class="lead">Twice the performance at half the power.</p>
  </section>
</main>
```

```css
html {
  /* ✅ proximity instead of mandatory: suggests the snap without hijacking scroll.
     mandatory = scroll-jacking, forbidden by the skill. */
  scroll-snap-type: y proximity;
}

.scene {
  scroll-snap-align: start;   /* each scene snaps to the viewport top */
  min-height: 100svh;
  display: grid;
  place-items: center;
  align-content: center;
  gap: 1rem;
  padding: 4rem 1.5rem;
  text-align: center;
}

/* Each color change = a new scene (apple.com pattern) */
.scene--dark { background: #000; color: #F5F5F7; }
.scene--dark .lead { color: #A1A1A6; }
.scene--light  { background: var(--bg-2); }
```

### 3B. Sections revealed on entering the viewport ✅

```html
<section class="reveal">
  <h2 class="title">All-day battery.</h2>
  <p class="body">Up to 27 hours of video on a single charge.</p>
</section>
```

```css
.reveal {
  opacity: 0;
  translate: 0 24px;  /* ✅ small offset: subtle, not theatrical */
  transition: opacity 0.7s ease, translate 0.7s ease;
}
.reveal.visible { opacity: 1; translate: 0 0; }

/* ✅ Respects users who asked for reduced motion: no animation, visible content */
@media (prefers-reduced-motion: reduce) {
  .reveal { opacity: 1; translate: none; transition: none; }
}
```

```js
// Reveals each .reveal when it enters the viewport, then stops observing it.
// ✅ IntersectionObserver: standard API, no dependencies.
const observer = new IntersectionObserver((entries) => {
  for (const entry of entries) {
    if (entry.isIntersecting) {
      entry.target.classList.add("visible");
      observer.unobserve(entry.target);
    }
  }
}, { threshold: 0.15 }); // fires at 15% visibility

document.querySelectorAll(".reveal").forEach((el) => observer.observe(el));
```

## 4. Apple-style product card ✅

**When to use it:** product grid, comparator, or feature bento. Light background, generous radius, subtle shadow: the card doesn't compete with the product.

```html
<div class="product-grid">
  <article class="product-card">
    <img src="./img/iphone-air-blue.png" alt="iPhone Air in sky blue"
         width="600" height="600" loading="lazy" decoding="async">
    <h3 class="card-name">iPhone Air</h3>
    <p class="card-tagline">Thin. Powerful. Pro.</p>
    <p class="card-price">From $999</p>
    <div class="card-ctas">
      <a class="cta-solid cta-solid--small" href="#">Buy</a>
      <a class="cta-text" href="#">Learn more ›</a>
    </div>
  </article>
  <!-- repeat <article> per product -->
</div>
```

```css
.product-grid {
  display: grid;
  /* ✅ self-adapting columns: 1 on mobile, 2–3 on desktop */
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 1.5rem;
  max-width: 980px;   /* apple.com-style centered container */
  margin: 0 auto;
  padding: 4rem 1.5rem;
}

.product-card {
  background: var(--bg-2);
  border-radius: var(--radius);          /* 24px: generous radius */
  padding: 2.5rem 2rem 2rem;
  display: grid;
  gap: 0.75rem;
  justify-items: center;
  text-align: center;
  /* subtle shadow: ambient and diffuse, never hard */
  box-shadow: 0 4px 16px rgba(0, 0, 0, 0.06);
  transition: translate 0.3s ease, box-shadow 0.3s ease; /* ✅ transform/shadow only */
}
.product-card:hover {
  translate: 0 -4px;
  box-shadow: 0 12px 32px rgba(0, 0, 0, 0.10);
}

.product-card img {
  width: min(100%, 320px);
  height: auto;
}

.card-name     { margin: 0; font-size: 1.5rem; font-weight: 700;
                 letter-spacing: -0.01em; }
.card-tagline  { margin: 0; color: var(--text-2); font-size: 1.0625rem; }
.card-price    { margin: 0.25rem 0 0; font-weight: 600; }
.card-ctas     { display: flex; gap: 1.25rem; align-items: center;
                 margin-top: 0.5rem; flex-wrap: wrap; justify-content: center; }

.cta-solid--small { min-height: 40px; padding: 0 1.25rem; font-size: 0.9375rem; }
```

## 5. Translucent top nav ⚠️

**When to use it:** it's the **only** translucent element allowed on the page (floating functional chrome). Minimal ~48px nav, pinned to the top, with content passing underneath.

> ⚠️ **MANDATORY WARNING:** this is a **visual approximation**, not real Liquid Glass. `backdrop-filter` imitates the veil + blur without refraction or dynamic sampling of the system material. Never call it "Liquid Glass" in the UI or in user-facing documentation.

```html
<nav class="nav" aria-label="Primary">
  <div class="nav-inner">
    <a class="nav-logo" href="#" aria-label="Home"></a>
    <a href="#">Store</a>
    <a href="#">Mac</a>
    <a href="#">iPad</a>
    <a href="#">iPhone</a>
    <a href="#">Watch</a>
    <a href="#">Support</a>
  </div>
</nav>
```

```css
.nav {
  position: fixed;
  inset: 0 0 auto 0;   /* pinned to the top, full width */
  z-index: 50;
  height: 48px;        /* apple.com-style nav height */

  /* ⚠️ approximation recipe (from ../materials/glass-css-web.md):
     blur + saturate (blur alone "kills" color), translucent veil,
     hairline below. Needs content behind it to show. */
  background: light-dark(rgba(251,251,253,0.72), rgba(22,22,23,0.72));
  -webkit-backdrop-filter: blur(12px) saturate(160%); /* ⚠️ mandatory prefix on Safari/iOS */
  backdrop-filter: blur(12px) saturate(160%);
  border-bottom: 1px solid light-dark(rgba(0,0,0,0.08), rgba(255,255,255,0.12));
}

.nav-inner {
  height: 100%;
  max-width: 1024px;
  margin: 0 auto;
  padding: 0 1.5rem;
  display: flex;
  align-items: center;
  justify-content: space-between;
  font-size: 0.75rem;              /* small, discreet nav like apple.com */
}

.nav-inner a {
  color: var(--text-2);
  text-decoration: none;
  padding: 0.5rem;                 /* comfortable touch area without growing the bar */
}
.nav-inner a:hover { color: var(--text); }

.nav-logo::before {
  content: "";                   /* logo: replace with your SVG or symbol */
  display: block;
  width: 14px; height: 14px;
  background: currentColor;
  /* trick: mask with your logo; with no external image there's no broken placeholder */
  -webkit-mask: url("./img/logo.svg") center / contain no-repeat;
  mask: url("./img/logo.svg") center / contain no-repeat;
}

/* Page content passes UNDERNEATH the nav (floating functional layer) */
body { padding-top: 0; } /* don't push the layout: the hero already reserves the space */

/* 🟡 Fallback 1: no backdrop-filter support → opaque, legible bar */
@supports not ((backdrop-filter: blur(1px)) or (-webkit-backdrop-filter: blur(1px))) {
  .nav { background: var(--bg); }
}

/* ⚠️ Fallback 2: user asked for reduced transparency → solid bar.
   prefers-reduced-transparency is only understood by WebKit/Safari; the @supports
   above still covers the other browsers. */
@media (prefers-reduced-transparency: reduce) {
  .nav {
    background: var(--bg);
    -webkit-backdrop-filter: none;
    backdrop-filter: none;
  }
}
```

**Performance rules** (from `../materials/glass-css-web.md`, 🟡): `backdrop-filter` is one of CSS's most expensive effects — it re-samples the background every frame. Limits: 1–3 blurred surfaces at once (the fixed nav is cheap once composed); **never animate `backdrop-filter` itself**; animate only `transform` and `opacity` on elements with glass.

## Do / don't pairs

1. **Glass: just one, and only in the nav**
   - ✅ **DO:** a single translucent surface per page — the pinned top nav. It's functional chrome floating over content, the same two-layer rule as the skill.
   - ❌ **DON'T:** content cards, section backgrounds, or paragraphs with `backdrop-filter`. Glass in the content layer competes with content for attention and breaks the model.

2. **Fluid type, not fixed sizes**
   - ✅ **DO:** headlines with `clamp()` scaling from mobile (48px) to desktop (96px) without breakpoints. Body barely scales: 16 → 17px.
   - ❌ **DON'T:** fixed `font-size: 96px` that overflows on mobile, or hand-made media queries per headline when a `clamp()` solves it.

3. **One accent color per screen**
   - ✅ **DO:** blue (`#007AFF` / `#0A84FF` in dark) only for the primary action. Everything else, text.
   - ❌ **DON'T:** CTAs in several competing colors (blue + green + orange). One color, one meaning.

4. **Every translucency carries a fallback**
   - ✅ **DO:** `@supports not (backdrop-filter)` → opaque background; `prefers-reduced-transparency` → solid variant. The design survives without blur.
   - ❌ **DON'T:** assume blur exists and leave text unreadable over a loud background in unsupported browsers.

5. **Subtle, respectful motion**
   - ✅ **DO:** reveals of `opacity` + 24px `translate`, disabled with `prefers-reduced-motion`. `scroll-snap-type: y proximity` that suggests without forcing.
   - ❌ **DON'T:** scroll-jacking (aggressive `mandatory`), strong parallax, or animating the `backdrop-filter` radius — GPU-expensive and nauseating.

6. **The product, in real full-color photography**
   - ✅ **DO:** product photography as protagonist over a near-monochrome palette (black / `#F5F5F7` / white). One idea per screen.
   - ❌ **DON'T:** abstract blobs, generic icons, or stock illustrations as the main image. The abstract decorates; the product sells.

7. **`100svh`, not `100vh`, in the hero**
   - ✅ **DO:** `min-height: 100svh` — discounts the browser bar on iOS/Android and the hero takes exactly the visible screen.
   - ❌ **DON'T:** `100vh`, which leaves part of the hero covered by the browser bar on mobile and breaks "one idea per screen".

8. **Measured contrast over the nav**
   - ✅ **DO:** measure nav text against the worst background passing underneath; if contrast collapses, raise the veil's opacity.
   - ❌ **DON'T:** long paragraphs or small text over translucent surfaces. Glass is for minimal chrome, not for reading.

See also: `apple-web-style.md`, `../materials/glass-css-web.md`, `../system/tokens.md`, `../system/motion.md`.
