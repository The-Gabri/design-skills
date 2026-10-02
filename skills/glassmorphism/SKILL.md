---
name: glassmorphism
description: Frosted-glass UI aesthetic — translucent panels with backdrop blur and saturate, bright hairline edges and soft shadows floating over vivid, colorful backgrounds. Use for dashboards, nav bars, modals, hero panels and overlays that should feel layered and luminous.
---

# Glassmorphism

The frosted-glass visual language of the early 2020s: translucent surfaces that
blur the world behind them, lit rims, and soft float shadows. The term was
coined in November 2020 by Michal Malewicz of the Hype4 design studio (🟡 —
widely documented in design press). The technique descends from Windows
Vista/7 Aero, iOS 7 blur, and macOS Big Sur's translucency (🟡).

> **Not the same as `apple-liquid-glass`.** That skill covers Apple's native
> Liquid Glass material system (two-layer model, regular/clear variants,
> system semantics). Glassmorphism is the generic, web-first frosted-glass
> aesthetic — it predates and outlives any single platform.

## Verification legend

- ✅ = documented behavior or rule confirmed in independent sources.
- 🟡 = widely cross-referenced community convention (consistent across ≥3
  implementations/guides), no single canonical spec.
- ⚠️ = approximation or guideline from a single source / community recipe —
  useful, not dogma.

## Principles

1. **Frost, don't tint.** The signature is real background blur via
   `backdrop-filter` (roughly 8–40px), not mere transparency. Below ~8px it
   reads as plain translucency; above ~40px it melts into opacity. 🟡
2. **Four ingredients, always together.** (a) Frost — `blur()` plus
   `saturate()` so the backdrop stays vivid; (b) translucency — a background
   fill with alpha, never fully opaque, never fully clear; (c) edge of glass —
   a hairline border *brighter* than the fill, ideally lit top-left → dim
   bottom-right; (d) depth — layered shadows plus an inset top highlight and
   bottom shade. A panel missing any one reads as a flat translucent box. 🟡
3. **Glass needs something to frost.** `backdrop-filter` only blurs content
   that sits behind the element. Over a flat background color it does nothing
   visible — the backdrop must be vivid: a colorful photo, video, or
   multi-stop mesh gradient. Glass without a busy backdrop is just a tinted
   div. ✅
4. **One level of glass.** Never stack glass on glass: frosted layers sample
   each other into mud, and stacked alphas compound. Separate overlapping
   glass panels with space or a solid layer between them. 🟡
5. **Legibility is the price of admission.** Choose text color from the
   backdrop's luminance (white text on dark glass, dark ink on light glass),
   back it with a subtle text-shadow, and verify contrast at the extremes of
   the background — not just the middle. 🟡
6. **Chrome, not content.** Glass is decoration for floating UI — nav bars,
   hero panels, modals, toasts, overlays. It should never carry a page's whole
   information architecture, and at most ~2 glass surfaces should share one
   view (typically the nav + one hero panel). 🟡

## Color

The glass tokens are near-universal; the page palette comes from the backdrop.

| Token | Value | Role | Confidence |
|---|---|---|---|
| `--glass-fill` | `rgba(255,255,255,0.08–0.18)` | Fill on dark/vivid backdrops | 🟡 |
| `--glass-fill-light` | `rgba(255,255,255,0.55–0.70)` | Frosted-white fill on light backdrops | 🟡 |
| `--glass-fill-darkmode` | `rgba(0,0,0,0.30)` | Dark glass variant | 🟡 |
| `--glass-edge` | `rgba(255,255,255,0.18–0.25)` | 1px hairline border, brighter than fill | 🟡 |
| `--glass-edge-lit` | `rgba(255,255,255,0.35)` | Inset top highlight (`inset 0 1px 0`) | 🟡 |
| `--glass-shade` | `rgba(0,0,0,0.12)` | Inset bottom shade (`inset 0 -1px 0`) | 🟡 |
| `--glass-shadow` | `rgba(0,0,0,0.20)` | Ambient float shadow (`0 8px 32px`) | 🟡 |
| `--glass-shadow-tint` | `rgba(31,38,135,0.37)` | Colored ambient shadow, classic recipe | 🟡 |

**Frost tiers** — match blur to the panel's weight: 🟡

| Tier | Blur | Fill alpha | Use for |
|---|---|---|---|
| Light chrome | `blur(8–12px)` | 0.08–0.14 | nav bars, toolbars, tab bars |
| Standard | `blur(16–20px)` | 0.10–0.18 | cards, hero panels, toasts |
| Heavy | `blur(24–40px)` | 0.10–0.18 | modals, login sheets, scrims |

**Backdrop recipes** (vivid is mandatory): ⚠️ community recipes, cross-referenced.
- *Aurora mesh:* deep base (`#14102E` / `#0F172A`) with 3–5 large
  `radial-gradient` blobs (coral `#FF6B6B`, violet `#A855F7`, teal `#2DD4BF`,
  amber `#FBBF24`), each `filter: blur(60–100px)`. Pure CSS, no images.
- *Big Sur-style:* full-bleed colorful photo or abstract art, darkened ~20%
  for text safety (✅ — macOS Big Sur translucency sits over dynamic
  wallpaper).

**Text on glass:** dark glass → near-white `#FFFFFF`/`#F8FAFC`; light glass →
dark ink `#1E293B`. 🟡

## Typography

- **No canonical typeface.** Glassmorphism is a surface treatment, not a type
  movement — clean geometric/humanist sans (SF Pro, Segoe UI, system stack) is
  the norm. ⚠️
- **Rules:** text on glass is short and high-contrast — labels, numbers,
  headings. Keep body paragraphs on solid surfaces or behind fills of
  alpha ≥ 0.35. 🟡
- **Weights:** 500–700 for labels on glass; light weights (<400) dissolve
  into the blur. 🟡
- **Cheap legibility insurance:** `text-shadow: 0 1px 8px rgba(0,0,0,0.25)`
  on dark glass, `0 1px 2px rgba(255,255,255,0.5)` on light glass. ⚠️

## Layout & spacing

- **Radius:** 16–24px cards, 12–16px chips, full-round toggles/avatars. 🟡
- **Padding:** generous — 24–40px inside cards; glass needs air to read as
  floating. 🟡
- **Grid:** none canonical; most implementations use a centered container
  (max-width ~1200px) on a 12-col responsive grid. ⚠️
- **The 2-surface rule:** at most 2 glass surfaces per view. A third glass
  surface means the treatment should change, not stack. ⚠️ community
  guideline.

## Components

### 1. Base frosted panel (the whole recipe in one class)

```css
.glass {
  background: rgba(255, 255, 255, 0.12);       /* translucency */
  backdrop-filter: blur(16px) saturate(160%);  /* frost */
  -webkit-backdrop-filter: blur(16px) saturate(160%); /* Safari needs it */
  border: 1px solid rgba(255, 255, 255, 0.25);  /* edge brighter than fill */
  border-radius: 20px;
  box-shadow:
    0 8px 32px rgba(0, 0, 0, 0.20),            /* ambient float */
    inset 0 1px 0 rgba(255, 255, 255, 0.35),    /* top light catch */
    inset 0 -1px 0 rgba(0, 0, 0, 0.12);        /* bottom shade */
}

/* Fallback: no backdrop-filter → raise fill opacity so text stays readable */
@supports not ((backdrop-filter: blur(1px)) or (-webkit-backdrop-filter: blur(1px))) {
  .glass { background: rgba(20, 16, 46, 0.78); }
}
```

### 2. Specular edge ring (the "lit corner" upgrade)

A flat border is dead — draw a masked 1px ring whose top-left catches light:

```css
.glass-luxe { position: relative; }
.glass-luxe::before {
  content: ""; position: absolute; inset: 0; border-radius: inherit;
  padding: 1px; pointer-events: none;
  background: linear-gradient(135deg,
    rgba(255,255,255,0.65), rgba(255,255,255,0.12) 40%,
    rgba(255,255,255,0.05) 60%, rgba(255,255,255,0.35));
  -webkit-mask: linear-gradient(#fff 0 0) content-box, linear-gradient(#fff 0 0);
  -webkit-mask-composite: xor; mask-composite: exclude;
}
```

### 3. Frosted nav bar

```html
<header class="glass-nav">
  <a class="logo" href="#">Drift</a>
  <nav>
    <a href="#features">Features</a>
    <a href="#pricing">Pricing</a>
    <a href="#reviews">Reviews</a>
  </nav>
  <a class="btn-solid" href="#get-started">Get started</a>
</header>
```

```css
.glass-nav {
  position: sticky; top: 12px; z-index: 50;
  display: flex; align-items: center; justify-content: space-between;
  max-width: 1120px; margin: 12px auto; padding: 12px 20px;
  background: rgba(255,255,255,0.10);            /* light chrome tier */
  backdrop-filter: blur(12px) saturate(160%);
  -webkit-backdrop-filter: blur(12px) saturate(160%);
  border: 1px solid rgba(255,255,255,0.22);
  border-radius: 999px;                          /* pill nav = signature */
  box-shadow: 0 8px 24px rgba(0,0,0,0.18),
              inset 0 1px 0 rgba(255,255,255,0.30);
}
```

Deepen the frost on scroll (fill 0 → 0.12) via a `.scrolled` class toggle —
never animate `backdrop-filter` itself; swap classes instead.

### 4. Hero stat card

```html
<article class="glass glass-card">
  <p class="eyebrow">This week</p>
  <p class="stat">38<span>min</span></p>
  <p class="label">Average focus session, up 12% from last week</p>
  <div class="bar"><span style="width:72%"></span></div>
</article>
```

```css
.glass-card { padding: 28px; }
.eyebrow { font-size: 12px; letter-spacing: 0.14em; text-transform: uppercase;
           color: rgba(255,255,255,0.65); }
.stat { font-size: 56px; font-weight: 700; color: #fff;
        text-shadow: 0 2px 12px rgba(0,0,0,0.30); }
.stat span { font-size: 20px; font-weight: 500; opacity: 0.7; }
.bar { height: 8px; border-radius: 99px; background: rgba(255,255,255,0.15);
       overflow: hidden; }
.bar span { display: block; height: 100%; border-radius: inherit;
            background: linear-gradient(90deg, #2DD4BF, #A855F7); }
```

### 5. Glass modal + scrim

```html
<div class="scrim" id="signupModal" aria-hidden="true">
  <div class="glass glass-modal" role="dialog" aria-modal="true" aria-labelledby="modalTitle">
    <button class="modal-x" aria-label="Close">×</button>
    <h2 id="modalTitle">Start your clearest week</h2>
    <p>Free for 14 days. No card required.</p>
    <form>
      <input type="email" placeholder="you@studio.com" required>
      <button class="btn-solid" type="submit">Create free account</button>
    </form>
  </div>
</div>
```

```css
.scrim { position: fixed; inset: 0; display: grid; place-items: center;
         background: rgba(10, 8, 30, 0.45);
         backdrop-filter: blur(6px); -webkit-backdrop-filter: blur(6px); }
.glass-modal { max-width: 420px; width: calc(100% - 48px); padding: 36px;
               background: rgba(255,255,255,0.14);
               backdrop-filter: blur(28px) saturate(160%); /* heavy tier */
               -webkit-backdrop-filter: blur(28px) saturate(160%);
               border: 1px solid rgba(255,255,255,0.28);
               border-radius: 24px; }
.glass-modal input { width: 100%; padding: 14px 16px; border-radius: 14px;
  background: #fff; border: 1px solid rgba(0,0,0,0.08); color: #1e293b; }
/* Inputs stay SOLID — never translucent fields (contrast untestable). */
```

### 6. Glass notification toast

```html
<div class="glass glass-toast" role="status">
  <span class="dot"></span>
  <p><strong>Session saved.</strong> 42 minutes of deep focus logged.</p>
</div>
```

```css
.glass-toast { display: flex; gap: 12px; align-items: center;
  padding: 14px 18px; border-radius: 16px; max-width: 380px;
  background: rgba(255,255,255,0.12);
  backdrop-filter: blur(18px) saturate(160%);
  -webkit-backdrop-filter: blur(18px) saturate(160%);
  border: 1px solid rgba(255,255,255,0.25);
  box-shadow: 0 12px 40px rgba(0,0,0,0.30),
              inset 0 1px 0 rgba(255,255,255,0.35);
  transform: translateY(16px); opacity: 0; transition: .3s ease-out; }
.glass-toast.show { transform: none; opacity: 1; }
.dot { width: 10px; height: 10px; border-radius: 50%; background: #2DD4BF;
       box-shadow: 0 0 12px #2DD4BF; flex: none; }
```

### 7. Segmented control (glass tabs)

```html
<div class="glass-tabs" role="tablist">
  <button role="tab" aria-selected="true">Timer</button>
  <button role="tab" aria-selected="false">Soundscapes</button>
  <button role="tab" aria-selected="false">Team rooms</button>
</div>
```

```css
.glass-tabs { display: inline-flex; padding: 6px; gap: 4px; border-radius: 999px;
  background: rgba(255,255,255,0.10);
  backdrop-filter: blur(12px) saturate(160%);
  -webkit-backdrop-filter: blur(12px) saturate(160%);
  border: 1px solid rgba(255,255,255,0.22); }
.glass-tabs button { border: 0; background: transparent; color: rgba(255,255,255,0.75);
  padding: 10px 22px; border-radius: 999px; font-weight: 600; cursor: pointer; }
.glass-tabs button[aria-selected="true"] { background: rgba(255,255,255,0.22);
  color: #fff; box-shadow: inset 0 1px 0 rgba(255,255,255,0.35); }
```

### 8. Aurora mesh background (pure CSS, zero images)

```css
.backdrop { position: fixed; inset: 0; z-index: -2; background: #14102E; }
.backdrop::before { content: ""; position: absolute; inset: -10%;
  background:
    radial-gradient(42% 38% at 18% 22%, rgba(255,107,107,0.85), transparent 70%),
    radial-gradient(38% 42% at 82% 18%, rgba(168,85,247,0.80), transparent 70%),
    radial-gradient(46% 40% at 72% 78%, rgba(45,212,191,0.75), transparent 70%),
    radial-gradient(30% 30% at 30% 82%, rgba(251,191,36,0.60), transparent 70%);
  filter: blur(70px); }
/* Anti-banding grain: kills stepped contours under heavy blur */
.backdrop::after { content: ""; position: absolute; inset: 0; opacity: 0.05;
  background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='160' height='160'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='2'/%3E%3C/filter%3E%3Crect width='160' height='160' filter='url(%23n)'/%3E%3C/svg%3E"); }
```

## Motion

- **Signature:** hover → frost deepens slightly, highlight brightens, panel
  lifts `translateY(-4px)`; 200–300ms `ease-out`. 🟡
- **Nav:** frosts in on scroll (transparent → fill 0.12) via class swap. ⚠️
- **Entrances:** panels rise + fade in (`translateY(24px)` → 0, opacity 0 →
  1), staggered 60–80ms. ⚠️
- **Never transition `backdrop-filter` itself** — it forces expensive repaints.
  Swap between pre-baked classes or animate opacity/transform only. 🟡
- **Reduced motion:** `prefers-reduced-motion` → instant crossfade, no drift,
  no float loops. ✅ (platform guideline, applied here.)

## Do / Don't

| ✅ Do | ❌ Don't |
|---|---|
| Give every glass panel a vivid, busy backdrop (mesh gradient, photo, video) — the frost has to blur *something*. | Put glass over a flat solid color: `backdrop-filter` goes invisible and you ship a muddy translucent box. |
| Pick text color from backdrop luminance, add `text-shadow`, and check contrast at the background's brightest *and* darkest spots. | Set long paragraphs (200+ words) on low-alpha glass — body copy belongs on solid surfaces or behind fill alpha ≥ 0.35. |
| Keep primary CTAs **solid and opaque** — white or brand fill, full contrast. | Make the main CTA glass: its contrast is untestable across backdrops, and it never pops. |
| Pair every glass panel with the 1px edge brighter than the fill plus the inset top highlight. | Rely on fill alone — without the lit rim it reads as plastic wrap, not glass. |
| Vary frost by weight: 8–12px chrome, 16–20px cards, 24–40px modals. | Use one blur value everywhere — uniform frost flattens the depth hierarchy. |
| Add `saturate(140–180%)` so the backdrop stays vivid through the blur. | Blur without saturate at high radii — it desaturates into gray milk. |
| Cap at ~5–8 glass elements per page; `transform: translateZ(0)` on animated ones. | `backdrop-filter` an entire scrolling list or grid — it tanks mobile GPUs. |
| Ship `-webkit-backdrop-filter` alongside the standard property (Safari), plus an `@supports` fallback with raised fill opacity. ✅ | Assume `backdrop-filter` works everywhere — older browsers get an unreadable ghost. |

## Copy voice

Glassmorphism is a movement, not a brand — but its canonical copy shares a
register: short, luminous, and calm. UI text is terse; marketing copy leans on
light/clarity metaphors (clear, glow, drift, focus, through). Headings carry
the poetry, body copy stays plain.

- "Blur the noise. Keep the signal."
- "Your next focus session, already glowing."
- "See everything through it. Miss nothing behind it."

## Performance notes

`backdrop-filter` is GPU-heavy: each frosted element repaints its backdrop on
scroll. Budget ~5–8 glass surfaces per view, prefer `transform`/`opacity`
animations, and test on a mid-range phone before shipping. 🟡

## Sources consulted

- Canonical community recipe (cross-referenced in 4+ guides): `background:
  rgba(255,255,255,0.07–0.25)`, `backdrop-filter: blur(10–20px)`,
  `border: 1px solid rgba(255,255,255,0.18–0.30)`, `border-radius: 16–20px`,
  `box-shadow: 0 8px 32px rgba(0,0,0,0.2)`. Sources:
  https://www.thatsoftwaredude.com/content/14160/how-to-implement-glassmorphism-design-on-your-website,
  https://medium.com/@wilfredcy/how-to-create-a-glassmorphism-effect-with-css-39f1b12a5347,
  https://github.com/NikolaPopovic71/glass-morphism-buttons,
  https://dev.to/omeal/glassmorphism-upcoming-ui-trend-44fk 🟡
- Four-ingredient model, frost tiers, specular edge, anti-banding grain,
  masked-border recipe: https://github.com/danilodoamarall/compound-labs-design/blob/HEAD/content/skills/iart-ai__glassmorphism.md 🟡
- 2-surface rule, solid-CTA rule, light-glass recipe, state guidance:
  https://github.com/aievolutionpl/agent-design-taste/blob/HEAD/styles/02-glassmorphism/README.md ⚠️ (single-source community guideline)
- Pure-CSS backdrop + accessibility notes:
  https://github.com/mmrahmanbappi/100-css-designs/blob/HEAD/01-soft-tactile-ui/001-glassmorphism/README.md 🟡
- MDN `backdrop-filter` (Safari `-webkit-` prefix; Firefox 103+ support) — noted
  via cross-referenced guides. ✅
- Term coined by Michal Malewicz (Hype4), Nov 2020 — documented in design
  press, cross-referenced. 🟡
