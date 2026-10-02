# Apple.com-style web 🟡

Actionable principles consistently observed in teardowns and reconstructions of apple.com. Not Apple's spec; patterns, not literal copy.

For the copy-pasteable CSS of each pattern: `css-examples.md`. The translucency recipe: `../materials/glass-css-web.md`.

## 1. Minimal, translucent top nav ✅

Slim global sticky bar **(~44–48px)** ✅, translucent with backdrop blur; content scrolls underneath ✅. Slims/adapts on scroll. It's the page's **only** glass.

Minimal structure example ✅:

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

> ⚠️ `backdrop-filter` imitates the veil + blur, **it is not real Liquid Glass** (no refraction or dynamic sampling of the system material). Never call it "Liquid Glass" in the UI or in user-facing docs. Full recipe with fallbacks in `css-examples.md` §5.

## 2. Full-screen hero ✅

One product, one message, total attention: product name + tagline + CTA row with the hero centered full-screen ✅. The asymmetric split hero is rejected: **symmetric lockup** (name + tagline + CTAs) with the product render/image bleeding full-bleed. One idea per section ✅.

- ✅ Enormous type: hero headlines **80–104px** on desktop; hierarchy in big jumps (hero 80–104 → section 40–56px → eyebrow 12–14px uppercase → body 17px); SF Pro Display >20px / SF Pro Text <20px; very tight tracking in display (−0.02 to −0.04em), body ≈ −0.016em.
- ✅ Text CTAs ("Buy ›", "Learn more ›") — no loud buttons. Double grammar: blue text links and **small blue pills** (`border-radius` ~980px, thin); rarely more than one elevated CTA per section.

Lockup example ✅:

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
  <img class="hero-product" src="./img/iphone-air.png"
       alt="iPhone Air in profile, sky blue"
       width="1200" height="800" decoding="async" fetchpriority="high">
</header>
```

Full CSS with `clamp()` and `100svh` in `css-examples.md` §1–§2.

## 3. One idea per screen ✅

Full-viewport sections separated by **alternating color blocks** (black, `#F5F5F7`/`#FAFAFC`, white) more than by spacing ✅. Every color change = a new scene. Page rhythm: hero → alternating full-bleed feature sections → bento → tech specs → fat multi-column footer (max density in the footer) ✅.

- ✅ **Bento once, where it earns it**: 2–3 column feature grid inside a centered container (~980px); not as default decoration. On the home page, sections separated by ~12px gutters.
- ✅ **Elevation**: no shadows on cards/chrome; a single shadow reserved for product-on-surface (`rgba(0,0,0,0.22) 3px 5px 30px`); depth from photography (light, DOF) and scroll parallax.

## 4. Scroll storytelling ✅

The product rotates/zooms/advances with scroll: video with scrubbed `currentTime` (video-first on flagship pages, with a static-frame fallback and reduced-motion → static), image sequence on canvas, or transforms tied to scroll progress with damping ✅. One continuous cinematic scene per flagship page; **never scroll-jacking** (damped smoothing, not hijack).

Light, safe version (full pattern in `css-examples.md` §3):

- Viewport scenes with `scroll-snap-type: y proximity` ✅ (proximity suggests the snap; aggressive `mandatory` = scroll-jacking, forbidden).
- Sections revealed on entering the viewport with `IntersectionObserver`: `opacity` + 24px `translate`, disabled after `prefers-reduced-motion` ✅.

## 5. Product photography as protagonist ✅

Near-monochrome palette + full-color photo ✅. Show the real product, not abstract blobs: the palette is white `#FFFFFF`, pearl `#F5F5F7`, near-black ink `#1D1D1F` for text, one blue (`#0071E3` on the web) for everything interactive; **the color comes from the product photography, not the chrome**. Hairline borders `#D2D2D7` very rare. Low density in the hero (lots of air, one focal object) growing band by band.

## 6. Giant type as a graphic element 🟡

Fluid headlines with `clamp()` (display scales fluidly, body barely) 🟡. Compression inside the block (negative tracking, tight leading) and **vast air** around. Scale in `../system/tokens.md`; ready-to-use fluid scale in `css-examples.md` §2.

## 7. Engineering 🟡

Progressive (not a heavy SPA): `<picture>`/`srcset`, `loading="lazy"`, immutably-hashed assets, deferred JS 🟡. All motion behind `prefers-reduced-motion` ✅. Centered content width **~1024–1240px**, generous vertical rhythm (96–192px sections) 🟡. On the web with notch/Dynamic Island: `viewport-fit=cover` + `env(safe-area-inset-*)` on header/hero ✅.

## 8. The razor test 🟡

For every effect ask: *"if I remove it, does the design lose meaning or just decoration?"* If just decoration → cut. (Restraint principle, consistent in ≥3 sources.)

### Do / don't pairs — apple.com style

1. **One idea per screen**
   - ✅ **DO:** full-viewport centered hero with one focal object; sections separated by color blocks (black / pearl / white).
   - ❌ **DON'T:** asymmetric split hero with three messages at once, or sections separated only by spacing that melt into each other.

2. **CTAs**
   - ✅ **DO:** "Buy ›" / "Learn more ›" as blue text; at most one pill CTA per section (`border-radius` ~980px, thin).
   - ❌ **DON'T:** loud buttons in several colors or two competing pills.

3. **Color**
   - ✅ **DO:** near-monochrome palette + full-color product photo as protagonist; one blue for everything interactive.
   - ❌ **DON'T:** decorative gradients, abstract blobs as the main image, or borders/shadows on the chrome.

4. **Scroll**
   - ✅ **DO:** scroll storytelling with scrubbed video or damped transforms; `scroll-snap: y proximity`; motion disabled after `prefers-reduced-motion`.
   - ❌ **DON'T:** scroll-jacking (aggressive `mandatory`), strong parallax, or autoplay without a static alternative.

See also: `css-examples.md`, `../materials/glass-css-web.md`, `../system/tokens.md`, `../system/motion.md`.
