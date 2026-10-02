---
name: japandi
description: Japandi minimalism for the web — wabi-sabi warmth meets Scandinavian function; muted earth tones, honest materials, low profiles, generous negative space. Use for calm, craft-led product and brand pages.
---

# Japandi

## Verification legend
- ✅ = documented in ≥3 independent design guides on the movement.
- 🟡 = cross-referenced in 2 sources, or standard community consensus.
- ⚠️ = approximation — my translation of an interior-design principle into a web token. Treat as a starting point, not canon.

## Principles
1. **Restraint as the feature.** Japandi is wabi-sabi (beauty in imperfection and ageing) fused with Scandinavian hygge (quiet warmth) and lagom (the right amount, neither too much nor too little). Every element must earn its place; what you remove is the design. ✅
2. **Honest, natural materials.** Light woods (oak, ash, birch) carry Scandinavian airiness; dark woods (walnut, teak, stained cedar) bring Japanese depth. Linen, cotton, wool, rattan, bamboo, stone, paper, handmade ceramics. Matte finishes; never gloss, never synthetic shine. ✅
3. **Muted earth palette, no sharp contrasts.** Warm off-whites, beige, oatmeal, stone, mushroom, taupe, greige. Depth comes from charcoal, deep brown, muted sage, terracotta — never from stark black-on-white or saturated color. ✅
4. **Ma — negative space is a material.** Empty space is not a problem to solve; it is part of the composition. Large quiet fields let few objects breathe. ✅
5. **Craft over decoration.** Visual interest comes from material quality and surface finish — visible grain, a handmade edge — not from added ornament. One considered craft object per composition beats a shelf of decor. ✅
6. **Low, grounded, functional.** Horizontal lines, low silhouettes, clean lines with gentle curves. Everything functional; clutter concealed. ✅

## Color
Base fields are warm; black is used sparingly (hairlines, small hardware), never as a dominant field. All hexes are my web translations of documented paint/material descriptions. ⚠️

| Token | Hex | Role |
|---|---|---|
| `--jpn-paper` | `#F6F2E9` | page background — warm rice-paper white ⚠️ |
| `--jpn-oat` | `#ECE5D3` | raised surface / card field ⚠️ |
| `--jpn-sand` | `#DCD2BB` | hairline borders, dividers ⚠️ |
| `--jpn-ink` | `#2B2620` | primary text — soft charcoal-brown, never pure black ⚠️ |
| `--jpn-clay` | `#6F6455` | secondary / muted text ⚠️ |
| `--jpn-oak` | `#C9A87E` | light-wood accent (Scandi airiness) ⚠️ |
| `--jpn-walnut` | `#5E4B3B` | dark-wood accent (Japanese depth) ⚠️ |
| `--jpn-sage` | `#8B9A7D` | muted green accent, sparing ⚠️ |
| `--jpn-terra` | `#B4714F` | terracotta accent, sparing — one per view max ⚠️ |
| `--jpn-char` | `#211D19` | near-black, reserved for slim frames and small UI hardware ⚠️ |

Rules: light tones dominate large surfaces; one dark accent (walnut/charcoal) per view for grounding. 🟡 No pure `#000`/`#fff` anywhere — they read as harsh against the palette. ⚠️

## Typography
Japandi has no official typeface; the web convention is a quiet editorial serif for display against a neutral humanist sans for text. 🟡

- **Display:** a warm serif with visible stroke contrast — closest free: *Fraunces* or *Cormorant Garamond*. Headlines in sentence case, never all-caps. ⚠️
- **Body/UI:** a neutral grotesque with open apertures — closest free: *Inter*, or the system stack. Small sizes (12–14px) with generous tracking (0.04–0.08em) for eyebrows and labels. ⚠️
- **Scale (1.333 ratio):** 13 / 16 / 21 / 28 / 37 / 50 / 67. Display at 50–67px with `line-height: 1.05` and `letter-spacing: -0.01em`. Body 16–17px, `line-height: 1.7`. ⚠️
- **Weight:** display in Light–Regular (300–400); body in Regular; Medium (500) reserved for tiny labels. No bold display type — emphasis comes from size and space, not weight. ⚠️
- Numerals for prices: tabular, same size as body, never oversized. ⚠️

## Layout & spacing
- **Grid:** 12-column max-width 1200px, but compositions are deliberately asymmetric — a 7/5 split beats a centered stack. Content often sits off-center to leave a breathing field. ⚠️
- **Spacing scale (Ma rhythm):** `8 · 16 · 24 · 48 · 96 · 160`. Sections separated by 96–160px; related elements by 16–24px. Whitespace is the loudest element on the page. ⚠️
- **Radius:** 2–6px on cards and buttons; pills only for tiny tags. Nothing fully rounded except material swatches (circles). ⚠️
- **Borders:** 1px hairlines in `--jpn-sand`. No heavy outlines, no neon. ⚠️
- **Shadows:** one soft, warm-tinted shadow for lifted product: `0 24px 48px -24px rgba(43,38,32,.22)`. No stacked or dark shadows. ⚠️
- **Texture:** suggest wood grain / linen / paper with layered CSS gradients at ≤6% opacity — matte suggestion, never photoreal noise. ⚠️

## Components
Copy-pasteable HTML/CSS. Assumes the tokens above are defined on `:root`.

### 1. Quiet nav
Hairline divider, wordmark left, few links, one quiet action. No sticky blur theatrics — a plain paper bar.
```html
<header class="jpn-nav">
  <a class="jpn-wordmark" href="#">Kanso</a>
  <nav>
    <a href="#">Collection</a><a href="#">Craft</a><a href="#">Journal</a><a href="#">Atelier</a>
  </nav>
  <button class="jpn-btn-quiet">Visit the atelier</button>
</header>
```
```css
.jpn-nav{display:flex;align-items:center;justify-content:space-between;
  padding:20px 48px;border-bottom:1px solid var(--jpn-sand);background:var(--jpn-paper);}
.jpn-wordmark{font-family:Georgia,serif;font-size:24px;letter-spacing:.02em;color:var(--jpn-ink);text-decoration:none;}
.jpn-nav nav{display:flex;gap:32px;}
.jpn-nav nav a{font-size:14px;letter-spacing:.04em;color:var(--jpn-clay);text-decoration:none;}
.jpn-nav nav a:hover{color:var(--jpn-ink);}
```

### 2. Editorial hero (asymmetric)
One idea, off-center, breathing room around it. Eyebrow in tracked caps, serif headline, short paragraph, two quiet buttons.
```html
<section class="jpn-hero">
  <div class="jpn-hero-copy">
    <p class="jpn-eyebrow">Oak · Linen · Stone — Est. 2019</p>
    <h1>Furniture for<br>slower mornings.</h1>
    <p class="jpn-lede">Low profiles, honest materials, nothing you don't need. Built in small batches to be kept for decades, not seasons.</p>
    <div class="jpn-hero-actions">
      <button class="jpn-btn">Browse the collection</button>
      <a class="jpn-link" href="#">Our craft →</a>
    </div>
  </div>
  <div class="jpn-hero-field" aria-hidden="true"></div>
</section>
```
```css
.jpn-hero{display:grid;grid-template-columns:7fr 5fr;gap:48px;max-width:1200px;
  margin:0 auto;padding:120px 48px 96px;align-items:end;}
.jpn-eyebrow{font-size:12px;letter-spacing:.14em;text-transform:uppercase;color:var(--jpn-clay);}
.jpn-hero h1{font-family:Georgia,serif;font-weight:400;font-size:64px;line-height:1.05;
  letter-spacing:-.01em;color:var(--jpn-ink);margin:24px 0;}
.jpn-lede{font-size:17px;line-height:1.7;color:var(--jpn-clay);max-width:42ch;}
.jpn-hero-field{min-height:420px;background:var(--jpn-oat);border:1px solid var(--jpn-sand);border-radius:4px;}
.jpn-btn{background:var(--jpn-ink);color:var(--jpn-paper);border:none;border-radius:4px;
  padding:14px 28px;font-size:15px;letter-spacing:.03em;cursor:pointer;transition:background .4s ease;}
.jpn-btn:hover{background:var(--jpn-walnut);}
.jpn-btn-quiet{background:transparent;border:1px solid var(--jpn-sand);border-radius:4px;
  padding:12px 24px;font-size:14px;color:var(--jpn-ink);cursor:pointer;transition:border-color .4s ease;}
.jpn-btn-quiet:hover{border-color:var(--jpn-clay);}
.jpn-link{font-size:15px;color:var(--jpn-ink);text-decoration:none;border-bottom:1px solid var(--jpn-sand);padding-bottom:2px;}
```

### 3. Product card (quiet)
Matte field, generous padding, material note in small type, price in tabular numerals. Hover: the visual lifts slightly — the card itself barely moves.
```html
<article class="jpn-card">
  <div class="jpn-card-visual jpn-oak-grain"></div>
  <h3>Ari low bench</h3>
  <p class="jpn-card-material">Solid white oak · soap finish</p>
  <div class="jpn-card-row"><span class="jpn-price">€480</span><button class="jpn-btn-quiet">Add to bag</button></div>
</article>
```
```css
.jpn-card{background:var(--jpn-oat);border:1px solid var(--jpn-sand);border-radius:6px;padding:24px;}
.jpn-card-visual{height:220px;border-radius:4px;background:var(--jpn-sand);margin-bottom:24px;
  transition:transform .6s cubic-bezier(.22,1,.36,1), box-shadow .6s ease;}
.jpn-card:hover .jpn-card-visual{transform:translateY(-6px);box-shadow:0 24px 48px -24px rgba(43,38,32,.22);}
.jpn-card h3{font-family:Georgia,serif;font-weight:400;font-size:21px;margin:0 0 6px;color:var(--jpn-ink);}
.jpn-card-material{font-size:13px;letter-spacing:.05em;color:var(--jpn-clay);margin:0 0 20px;}
.jpn-card-row{display:flex;justify-content:space-between;align-items:center;}
.jpn-price{font-variant-numeric:tabular-nums;font-size:16px;color:var(--jpn-ink);}
```

### 4. Material tabs
Switching a finish is the signature interaction — quiet segmented control, hairline container.
```html
<div class="jpn-tabs" role="tablist" aria-label="Finish">
  <button role="tab" aria-selected="true" class="jpn-tab is-active">White oak</button>
  <button role="tab" aria-selected="false" class="jpn-tab">Smoked walnut</button>
  <button role="tab" aria-selected="false" class="jpn-tab">Rattan</button>
</div>
```
```css
.jpn-tabs{display:inline-flex;border:1px solid var(--jpn-sand);border-radius:6px;padding:4px;gap:4px;background:var(--jpn-paper);}
.jpn-tab{border:none;background:transparent;padding:10px 20px;font-size:14px;letter-spacing:.03em;
  color:var(--jpn-clay);border-radius:4px;cursor:pointer;transition:all .35s ease;}
.jpn-tab.is-active{background:var(--jpn-ink);color:var(--jpn-paper);}
```

### 5. Craft statement (philosophy block)
Numbered principles, generous measure, one dark accent panel per view.
```html
<section class="jpn-craft">
  <p class="jpn-eyebrow">Our craft</p>
  <h2>Perfection is a finish.<br>We prefer the grain.</h2>
  <ol class="jpn-principles">
    <li><span>01</span><div><h3>Restraint</h3><p>Fewer objects, made better. If it doesn't serve the room, it doesn't ship.</p></div></li>
    <li><span>02</span><div><h3>Honest materials</h3><p>Oak, linen, stone — finished matte, left to age gracefully.</p></div></li>
    <li><span>03</span><div><h3>The beauty of wear</h3><p>A softened edge, a darkened handle. Time is part of the design.</p></div></li>
  </ol>
</section>
```
```css
.jpn-craft{max-width:1200px;margin:0 auto;padding:96px 48px;}
.jpn-craft h2{font-family:Georgia,serif;font-weight:400;font-size:44px;line-height:1.15;color:var(--jpn-ink);margin:24px 0 64px;}
.jpn-principles{list-style:none;margin:0;padding:0;display:grid;gap:0;}
.jpn-principles li{display:grid;grid-template-columns:80px 1fr;gap:24px;padding:32px 0;border-top:1px solid var(--jpn-sand);}
.jpn-principles span{font-family:Georgia,serif;font-size:15px;color:var(--jpn-oak);letter-spacing:.06em;}
.jpn-principles h3{font-family:Georgia,serif;font-weight:400;font-size:21px;margin:0 0 8px;color:var(--jpn-ink);}
.jpn-principles p{font-size:16px;line-height:1.7;color:var(--jpn-clay);margin:0;max-width:52ch;}
```

### 6. Materials & care accordion
Quiet Q&A; plus/minus drawn with CSS, not emoji.
```html
<div class="jpn-acc">
  <button class="jpn-acc-head" aria-expanded="false">How do I care for oiled oak?<span class="jpn-acc-icon"></span></button>
  <div class="jpn-acc-body"><p>Wipe with a dry linen cloth. Re-oil once a year with the soap flakes included in every order — the wood darkens gently, which is the point.</p></div>
</div>
```
```css
.jpn-acc{border-top:1px solid var(--jpn-sand);}
.jpn-acc:last-child{border-bottom:1px solid var(--jpn-sand);}
.jpn-acc-head{width:100%;display:flex;justify-content:space-between;align-items:center;background:none;border:none;
  padding:22px 4px;font-family:Georgia,serif;font-size:19px;color:var(--jpn-ink);cursor:pointer;text-align:left;}
.jpn-acc-icon{position:relative;width:14px;height:14px;flex:none;}
.jpn-acc-icon::before,.jpn-acc-icon::after{content:"";position:absolute;background:var(--jpn-clay);transition:transform .4s ease;}
.jpn-acc-icon::before{left:0;top:6px;width:14px;height:2px;}
.jpn-acc-icon::after{left:6px;top:0;width:2px;height:14px;}
.jpn-acc.open .jpn-acc-icon::after{transform:rotate(90deg) scaleY(0);}
.jpn-acc-body{max-height:0;overflow:hidden;transition:max-height .5s cubic-bezier(.22,1,.36,1);}
.jpn-acc-body p{font-size:15px;line-height:1.7;color:var(--jpn-clay);margin:0;padding:0 4px 24px;max-width:60ch;}
```

### 7. Newsletter footer
Understated signup; the footer is a quiet colophon, not a sitemap wall.
```html
<footer class="jpn-footer">
  <div class="jpn-news">
    <h3>Letters, twice a year.</h3>
    <p>New pieces, workshop notes, nothing else.</p>
    <form class="jpn-form"><input type="email" placeholder="your@email.com" required><button class="jpn-btn" type="submit">Subscribe</button></form>
  </div>
  <p class="jpn-colophon">Kanso — furniture for slower mornings. Built from the japandi skill · design-skills</p>
</footer>
```
```css
.jpn-footer{background:var(--jpn-ink);color:var(--jpn-paper);padding:96px 48px 40px;}
.jpn-footer h3{font-family:Georgia,serif;font-weight:400;font-size:32px;margin:0 0 8px;}
.jpn-footer p{color:#B9AF9F;font-size:15px;line-height:1.7;}
.jpn-form{display:flex;gap:12px;margin-top:24px;max-width:440px;}
.jpn-form input{flex:1;background:transparent;border:1px solid #4A443C;border-radius:4px;
  padding:14px 18px;color:var(--jpn-paper);font-size:15px;}
.jpn-form input::placeholder{color:#8A8177;}
.jpn-footer .jpn-btn{background:var(--jpn-paper);color:var(--jpn-ink);}
.jpn-colophon{margin-top:80px;padding-top:24px;border-top:1px solid #4A443C;font-size:13px;color:#8A8177;}
```

## Motion
Japandi web motion is slow and barely-there: fades and 8–16px rises over 400–700ms with `cubic-bezier(.22,1,.36,1)`; no springs, no bounce, no parallax showboating. ⚠️ Honor `prefers-reduced-motion` (disable transforms, keep opacity crossfades). One animated element per viewport; the page should feel still. ⚠️

## Do / Don't
- ✅ **Do** pair light oak tones with exactly one dark walnut/charcoal accent per view — that light/dark wood contrast is the signature. / ❌ **Don't** build a dark-mode-everything page or a stark black-on-white page; both kill the warmth.
- ✅ **Do** use 1px hairlines and matte surfaces; let texture come from layered low-opacity gradients. / ❌ **Don't** use gloss, glassmorphism, heavy drop shadows, or gradients with saturated color.
- ✅ **Do** leave large empty fields — one product floating in paper-colored space is the hero composition. / ❌ **Don't** fill every pixel: no badge walls, no promo carousels, no "3 feature cards with icons" grids.
- ✅ **Do** write headlines in sentence case with short, sensory lines ("Oak, linen, and time."). / ❌ **Don't** use all-caps hype, exclamation marks, or urgency copy ("SALE ENDS SOON!!!").
- ✅ **Do** include one imperfect, handmade detail per composition — an uneven edge, a visible grain, an asymmetric offset. / ❌ **Don't** enforce pixel-perfect symmetry everywhere; sterile symmetry reads as Scandinavian, not Japandi.
- ✅ **Do** keep forms and CTAs quiet: single ink button, ghost secondary. / ❌ **Don't** use pill buttons with gradients, floating action buttons, or sticky promo bars.
- ✅ **Do** show joinery and craft in product copy ("dovetail joints, no screws visible"). / ❌ **Don't** describe products with tech-spec energy ("AERODYNAMIC 3000").

## Copy voice (for brand styles)
Unhurried, sensory, and plain-spoken. Short declarative lines; verbs of slowness — gather, linger, settle, keep. Prices and practicalities stated plainly, never hyped. Nature words used sparingly and literally (oak, linen, morning light), never as decoration.

Example strings:
- "Made to be kept."
- "Oak, linen, and time. Nothing else on the shelf."
- "It will darken where your hands rest. That's the design."

## Sources consulted
- PRDT Interiors — "Japandi Interior Design for HDB Flats in Singapore" (2026): palette (warm off-white/oat base, black used sparingly), materials, matte finishes, low horizontal lines.
- Style Curator — "What is Japandi interior design?" : wabi-sabi + hygge synthesis, muted palette, low grounded furniture, "perfectly imperfect" finishes.
- Emilamerica magazine — "Japandi Style interior design: ideas, rules": lagom as guiding principle, craft over decoration, harmony through negative space.
- Illustrarch — "Japandi Style Guide": light/dark wood contrast, clean lines with gentle curves.
- Homeg.org — "Japandi Style Homes": wabi-sabi & imperfection, connection to nature, single statement craft object per room.
- IndochinaLight — "Wabi-Sabi vs. Japandi": warm neutral hex ranges (sand #D2B48C to clay #967969), warm lighting 2700–3500K.
- vectree.io — "Japandi": hygge comfort, wabi-sabi zen, Ma (negative space), natural textures.
