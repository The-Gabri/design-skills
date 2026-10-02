---
name: apple-marketing
description: Design marketing pages like apple.com — full-bleed product scenes, huge tightly-tracked SF type, one idea per scroll scene, bento grids, and footnote-dense legal copy.
---

# Apple Marketing (apple.com style)

Use for fictional-product marketing pages that read like apple.com: a cinematic
scroll through full-bleed scenes where the product is the hero, typography does
the selling, and the UI gets out of the way. Research base: apple.com homepage
and product pages (observed directly) plus multiple published design teardowns
cross-referenced for tokens.

## Principles

1. **One idea per scene.** Each full-bleed section makes exactly one claim
   ("A battery you can't outrun."). If a section needs a bullet list, it has
   too many ideas.
2. **The product is the hero; the UI recedes.** Photography (or a large render)
   carries the color and the interest. No decorative chrome, no borders, no
   competing visuals.
3. **Restraint as a budget.** One accent color, spent only on interactive
   elements. One background change per scene. Every element must justify its
   existence.
4. **Scroll is the story.** Scenes alternate light / dark / product-stage gray,
   and the background change itself is the section divider. Pacing is
   cinematic: tight, quiet text blocks surrounded by vast whitespace.
5. **Confidence, not hype.** Copy is short, declarative, and punctuated.
   Let the claim land, then stop talking.

## Color

Confidence legend: ✅ observed on apple.com itself · 🟡 cross-referenced across
published teardowns · ⚠️ community approximation.

| Token | Hex | Role | Confidence |
|---|---|---|---|
| White | `#ffffff` | Page canvas, bento tile surface | ✅ |
| Apple gray | `#f5f5f7` | Product-stage section background | ✅ |
| Soft white | `#fbfbfd` | Alternate hero background | 🟡 |
| Ink | `#1d1d1f` | Primary text, dark-scene background | 🟡 |
| Secondary gray | `#86868b` | Taglines, secondary copy | 🟡 |
| Separator gray | `#d2d2d7` | Hairline dividers, spec table rules | 🟡 |
| Apple blue (link) | `#0066cc` | Inline text links, "Learn more >" | 🟡 |
| Apple blue (fill) | `#0071e3` | Primary pill button fill | 🟡 |
| Apple blue (on dark) | `#2997ff` | Links/buttons on dark scenes | 🟡 |
| Black | `#000000` | Dark drama scenes | ✅ |
| Single product accent | — | The product's own color (one finish at a time); the UI never invents a second accent | ✅ |

Rules: white ↔ `#f5f5f7` ↔ black is the entire section palette. The accent is
**one** blue, reserved for interactive elements. Product photography supplies
all other color. Never put gradients, textures, or patterns on backgrounds.

## Typography

- **Typeface:** SF Pro Display (20px and up) / SF Pro Text (below 20px). SF is
  not on Google Fonts; ship the system stack so real SF renders on Apple
  devices, with a neutral fallback elsewhere:
  ```css
  font-family: "SF Pro Display", "SF Pro Text", -apple-system,
    BlinkMacSystemFont, "Segoe UI", "Helvetica Neue", Arial, sans-serif;
  ```
- **Headlines:** weight 600 (semibold, never 800/900), negative letter-spacing
  that tightens with size, compressed line-height 1.04–1.10.

| Element | Size | Weight | Tracking | Line-height |
|---|---|---|---|---|
| Hero display | 80–104px (`clamp(3.5rem, 8vw, 6.5rem)`) | 600 | `-0.022em` | 1.05 |
| Scene headline | 48–64px | 600 | `-0.02em` | 1.08 |
| Section title | 32–40px | 600 | `-0.015em` | 1.12 |
| Tagline | 21–28px | 400 | `-0.01em` | 1.3 |
| Body | 17px | 400 | `-0.01em` | 1.47 |
| Footnote legal | 12px | 400 | 0 | 1.33 |

- **Taglines are gray and quiet** (`#86868b`, weight 400) — the "Now
  supercharged by M5." line under the hero name.
- **Headlines center; body copy left-aligns.** Footnotes are dense 12px blocks.
- Apply `font-feature-settings: "numr"` on spec/numeric content for tabular
  figures. 🟡

## Layout & spacing

- **Full-bleed scenes, 0 gap.** Sections stack edge to edge; the background
  color change is the only divider. Each product scene gets roughly one
  viewport of height and ≥64px of air above its headline.
- **Text column ≈ 980px** centered for headline/tagline blocks; bento grids
  and galleries can run wider (up to ~1400px).
- **Bento grids:** 2–3 large rounded tiles, 20–24px gutters, tile radius
  18–28px (🟡), alternating `#ffffff` / `#f5f5f7` surfaces — no borders, no
  shadows on tiles.
- **Pills:** CTA buttons and link pills use `border-radius: 980px`.
- **Radius continuity:** rectangular elements are rounded (cards 18–28px);
  nothing on the page has a 4px corner.
- Base unit 8px; section vertical padding ~80px; product imagery keeps ≥40px
  clearance from any text.

## Components

### 1. Global nav (frosted dark)

```html
<nav class="anav">
  <a href="#" class="anav-wordmark">nimbus</a>
  <a href="#">Overview</a><a href="#">Tech Specs</a>
  <a href="#">Compare</a><a href="#">Support</a>
</nav>
<style>
.anav{
  position:sticky;top:0;z-index:50;
  display:flex;gap:28px;justify-content:center;align-items:center;
  height:48px;font-size:12px;color:#f5f5f7;
  background:rgba(22,22,23,.8);          /* 🟡 cross-referenced */
  backdrop-filter:saturate(180%) blur(20px);
  -webkit-backdrop-filter:saturate(180%) blur(20px);
}
.anav a{color:#f5f5f7;text-decoration:none;opacity:.8}
.anav a:hover{opacity:1}
.anav-wordmark{font-weight:600;opacity:1!important}
</style>
```

### 2. Product sub-nav (sticky buy bar)

```html
<div class="asubnav">
  <span class="asubnav-name">Nimbus One</span>
  <a href="#" class="apill">Buy</a>
</div>
<style>
.asubnav{
  position:sticky;top:48px;z-index:40;
  display:flex;justify-content:space-between;align-items:center;
  padding:12px 24px;
  background:rgba(251,251,253,.72);
  backdrop-filter:saturate(180%) blur(20px);
  border-bottom:1px solid #d2d2d7;
}
.asubnav-name{font-size:21px;font-weight:600;letter-spacing:-.01em}
</style>
```

### 3. Hero (huge type, centered)

```html
<section class="ahero">
  <h1>Nimbus One</h1>
  <p class="tagline">Hear everything. Miss nothing.</p>
  <div class="cta-row">
    <a href="#" class="apill">Buy</a>
    <a href="#" class="alearn">Learn more <span aria-hidden="true">&gt;</span></a>
  </div>
</section>
<style>
.ahero{background:#fbfbfd;text-align:center;padding:96px 24px 64px}
.ahero h1{
  font-size:clamp(3.5rem,8vw,6.5rem);   /* 56px → 104px */
  font-weight:600;letter-spacing:-.022em;line-height:1.05;
  margin:0;color:#1d1d1f;
}
.tagline{font-size:28px;color:#86868b;margin:12px 0 28px;letter-spacing:-.01em}
.cta-row{display:flex;gap:28px;justify-content:center;align-items:center}
</style>
```

### 4. CTA link pair (the signature)

```html
<a href="#" class="apill">Buy</a>
<a href="#" class="alearn">Learn more <span aria-hidden="true">&gt;</span></a>
<style>
.apill{
  display:inline-block;background:#0071e3;color:#fff!important;
  font-size:15px;padding:8px 22px;border-radius:980px;text-decoration:none;
}
.apill:hover{background:#0077ed}
.alearn{color:#0066cc;font-size:17px;text-decoration:none}
.alearn:hover{text-decoration:underline}
.alearn span{font-size:.85em}
</style>
```

### 5. Sticky-scroll scene

```html
<section class="ascene" style="background:#000;color:#f5f5f7">
  <div class="ascene-pin">
    <img src="product-dark.jpg" alt="Nimbus One in Midnight">
    <div class="ascene-copy">
      <h2 class="ascene-h">Silence,<br>engineered.</h2>
      <p>Dual-driver adaptive noise cancellation samples your world
         48,000 times a second.</p>
    </div>
  </div>
</section>
<style>
.ascene{min-height:300vh;position:relative}
.ascene-pin{position:sticky;top:0;height:100vh;
  display:grid;place-items:center;overflow:hidden}
.ascene-h{font-size:clamp(2.5rem,6vw,4rem);font-weight:600;
  letter-spacing:-.02em;line-height:1.08;text-align:center}
.ascene-copy{position:absolute;bottom:12vh;max-width:640px;
  padding:0 24px;text-align:center}
.ascene-copy p{font-size:21px;color:#86868b}
</style>
```
Swap `.ascene-copy` text per scroll third with a tiny JS fade (see Motion), or
stack two pins — one claim per pin, never two.

### 6. Bento grid

```html
<section class="abento">
  <div class="atile tile-a">
    <h3>40-hour battery.</h3>
    <p>One charge. A week of commutes.</p>
  </div>
  <div class="atile tile-b">
    <h3>Studio drivers.</h3>
    <p>Custom 40&nbsp;mm beryllium.</p>
  </div>
  <div class="atile tile-c">
    <h3>Feather frame.</h3>
    <p>218&nbsp;grams. All day.</p>
  </div>
</section>
<style>
.abento{display:grid;gap:20px;max-width:1200px;margin:0 auto;
  padding:80px 24px;
  grid-template-columns:repeat(6,1fr)}
.atile{border-radius:28px;padding:48px;background:#fff}
.atile:nth-child(even){background:#f5f5f7}
.atile h3{font-size:32px;font-weight:600;letter-spacing:-.015em;
  line-height:1.12;margin:0 0 8px}
.atile p{font-size:17px;color:#86868b;margin:0}
.tile-a{grid-column:span 4}.tile-b{grid-column:span 2}
.tile-c{grid-column:span 6}
</style>
```

### 7. Spec table

```html
<table class="aspecs">
  <tr><th>Driver</th><td>40&nbsp;mm dynamic, beryllium-coated</td></tr>
  <tr><th>Battery</th><td>Up to 40 hours (ANC on)<sup>1</sup></td></tr>
  <tr><th>Weight</th><td>218&nbsp;g</td></tr>
</table>
<style>
.aspecs{width:100%;max-width:980px;margin:0 auto;border-collapse:collapse}
.aspecs th,.aspecs td{text-align:left;padding:18px 8px;
  border-bottom:1px solid #d2d2d7;font-size:17px;vertical-align:top}
.aspecs th{font-weight:600;width:32%}
.aspecs td{color:#1d1d1f}
</style>
```

### 8. Finish picker (segmented swatches)

```html
<div class="apicker" role="radiogroup" aria-label="Finish">
  <button class="aswatch is-on" style="--sw:#2e2e33" aria-label="Midnight"></button>
  <button class="aswatch" style="--sw:#e3e4e6" aria-label="Silver"></button>
  <button class="aswatch" style="--sw:#a7c1d9" aria-label="Sky"></button>
</div>
<p class="apicker-name">Midnight</p>
<style>
.apicker{display:flex;gap:12px;justify-content:center}
.aswatch{width:32px;height:32px;border-radius:50%;border:none;
  background:var(--sw);cursor:pointer;
  box-shadow:inset 0 0 0 1px rgba(0,0,0,.12)}
.aswatch.is-on{box-shadow:0 0 0 2px #fff,0 0 0 4px #0071e3}
.apicker-name{font-size:14px;color:#86868b;text-align:center}
</style>
```

### 9. Footnote block (dense legal)

```html
<section class="afootnotes">
  <ol>
    <li>Battery life varies by use and configuration. Testing conducted by
    Nimbus Labs in August 2026 using preproduction Nimbus One units with
    ANC enabled at 50% volume…</li>
  </ol>
  <p>Copyright © 2026 Nimbus Audio Inc. All rights reserved. Or call
  1-800-555-0199.</p>
</section>
<style>
.afootnotes{max-width:980px;margin:0 auto;padding:32px 24px;
  font-size:12px;line-height:1.33;color:#6e6e73}
.afootnotes ol{padding-left:18px;margin:0 0 12px}
</style>
```

### 10. Footer (dense link columns)

```html
<footer class="afooter">
  <div class="acols">
    <div><h4>Shop</h4><a href="#">Nimbus One</a><a href="#">Accessories</a></div>
    <div><h4>Support</h4><a href="#">Manuals</a><a href="#">Warranty</a></div>
  </div>
  <p class="alegal">Copyright © 2026 Nimbus Audio Inc. All rights reserved. |
  <a href="#">Privacy</a> | <a href="#">Terms</a></p>
</footer>
<style>
.afooter{background:#f5f5f7;padding:32px 24px 48px}
.acols{max-width:980px;margin:0 auto 24px;display:grid;
  grid-template-columns:repeat(auto-fit,minmax(140px,1fr));gap:24px}
.acols h4{font-size:12px;font-weight:600;margin:0 0 8px;color:#1d1d1f}
.acols a{display:block;font-size:12px;color:#424245;text-decoration:none;
  margin-bottom:8px}
.alegal{max-width:980px;margin:0 auto;font-size:12px;color:#6e6e73;
  border-top:1px solid #d2d2d7;padding-top:16px}
</style>
```

## Motion

Restrained and slow — fade-up scroll reveals (opacity + gentle translateY,
~0.8–1s, decelerating ease ⚠️), sticky pins that crossfade one claim at a
time, press = `scale(.96)`. No bounce, no spin, no parallax speed runs.
Always honor `prefers-reduced-motion`.

## Do / Don't

- **Do** alternate full-bleed scenes white → `#f5f5f7` → black with 0 gap; the
  color change is the divider. **Don't** add borders, rules, or gradient bands
  between sections.
- **Do** set hero headlines at 80–104px, weight 600, tracking `-0.022em`.
  **Don't** use weight 800/900 or zero tracking at display sizes — it breaks
  the carved-headline feel.
- **Do** spend the blue only on interactive elements (pill CTAs, "Learn more
  >" links). **Don't** use blue for decoration, icons, or section headers.
- **Do** keep taglines short, gray, weight 400 ("A battery you can't
  outrun."). **Don't** stack three adjectives in a headline.
- **Do** give every product scene one claim and one visual. **Don't** put a
  feature-grid inside a hero.
- **Do** write dense 12px footnotes with numbered claims and a support line.
  **Don't** ship marketing claims without footnote numbers.
- **Do** use pill CTAs (`border-radius: 980px`) and chevron text links.
  **Don't** use sharp-cornered or ghost-outline buttons.
- **Do** let product imagery carry the color on flat gray fields. **Don't**
  add shadows, glows, or gradient washes behind type.

## Copy voice

Confident. Short. Punctuated. Declarative fragments with periods that force a
pause — never exclamation marks, never superlative-stuffed paragraphs.

Examples:
- "Nimbus One. Sound, distilled."
- "40 hours. One charge. Zero compromises."¹
- "Pro drivers. Pro silence. Pro battery."
