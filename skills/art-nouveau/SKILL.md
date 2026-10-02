---
name: art-nouveau
description: Art Nouveau in the Mucha idiom — whiplash curves, botanical ornament, halos, and muted golds — for posters, packaging, and editorial pages. Use when a design should feel like an 1890s Parisian lithograph.
---

# Art Nouveau / Mucha

Design in the language of Alphonse Mucha's 1890s Paris posters: organic line, botanical ornament, and decoration fused into structure. Art Nouveau (c. 1890–1910) reacted against industrial mass production and academic historicism by making nature the structure of design — the curve is not applied on top, it *is* the form. ✅

## Confidence legend

- ✅ = documented characteristic of Art Nouveau / Mucha's posters, confirmed in ≥2 independent sources.
- 🟡 = consistent across reference analyses and poster reproductions, no direct official spec.
- ⚠️ = community/web approximation of tones from aged lithographs (ink has faded for 130 years; exact "original" hexes are unknowable).

## Principles

1. **The line is alive.** Every contour flows: the *coup de fouet* (whiplash) curve — an asymmetrical S-curve that starts with a forceful stroke and tapers into a delicate tail — carries tension and release like a plant stem. Straight ruled lines are the enemy. ✅
2. **Ornament is structure, not garnish.** Borders, frames, and lettering grow out of the same botanical system as the imagery. Mucha integrated brand lettering into the decorative scheme so text reads as part of the artwork, never as an afterthought. ✅
3. **Flat, decorative space.** Shallow depth; figures and ornament live on one decorative plane. Volume is suggested with thin ink washes and fine hatching, never with photorealistic shading or drop shadows. ✅
4. **Nature, stylized — not illustrated.** Irises, lilies, poppies, thistles, vines, dragonflies, peacocks: chosen for long stems and expressive silhouettes, then reduced to rhythmic, syncopated patterns. The plant's "soul" matters more than its botany. ✅
5. **Muted, warm restraint.** Soft pastels, earthy tones, subtle gradations; ink colors were layered on limestone in 8–10 runs (flesh, ivory, gold, blues, siennas, bronze, black). The restraint lets the linework take center stage. ✅
6. **Asymmetry with balance.** Compositions are deliberately off-center, like growth — weight settles organically rather than mirroring. ✅

## Color

Palette sampled from Mucha poster reproductions (Gismonda, Biscuits Lefèvre-Utile, Bisquit Cognac, Soap Factory of Bagnolet). All hexes ⚠️ (aged-lithograph approximations), roles 🟡.

| Token | Hex | Role |
|---|---|---|
| `--nouv-parchment` | `#F3E7CB` | Page background — aged paper |
| `--nouv-cream` | `#FBF4E2` | Panels, cards, figure skin highlights |
| `--nouv-gold` | `#C9962E` | Accent — metallic bronze/gold leaf, rules, lettering |
| `--nouv-gold-soft` | `#D9B45C` | Halo glows, highlights on gold |
| `--nouv-ochre` | `#B26A2E` | Warm secondary accent (terracotta/amber) |
| `--nouv-olive` | `#7A7444` | Botanical green — stems, leaves |
| `--nouv-sage` | `#9AA46B` | Pale leaf green, background washes |
| `--nouv-rose` | `#C98A7D` | Faded rose — blossoms, figure warmth |
| `--nouv-cobalt` | `#2F4B7C` | Deep blue for mosaic halos and lettering grounds (Gismonda's title) |
| `--nouv-ink` | `#33291F` | Linework, body text — warm black |
| `--nouv-brown` | `#6B4A2F` | Secondary ink, shading washes |

Rules: warm paper backgrounds always (never pure white); gold used as *ink*, not gradient — flat metallic tone or fine hatching, never a CSS metallic gradient; one deep tone (`--nouv-ink` or `--nouv-cobalt`) for legibility anchors; pastels sit on top of dark, never inverted. 🟡

## Typography

- **Display lettering:** Mucha drew bespoke hand-lettering per commission — tall, narrow capitals with curvilinear terminals, often set on a gently arcing band or integrated into mosaic tile fields. Closest free substitutes (named, not loaded): **Cormorant Garamond** (light, tall), **Cinzel Decorative** (inscribed-cap feel), **Marcellus**. Always all-caps with generous letter-spacing (`0.18–0.3em`), often arched or set inside the ornament band. 🟡
- **Body:** a quiet old-style serif for readability — **EB Garamond / Georgia** — regular weight, `1.05–1.15` line-height, never a geometric or grotesque sans. ⚠️
- **Scale:** Mucha posters are strongly hierarchical — one large title (often ~1/6 of poster height), a graceful subhead, then small, meticulously organized text blocks. Translate to web: display `clamp(2.5rem, 6vw, 4.5rem)`, subhead `1.25rem` italic, body `1rem`, captions `0.8rem` tracked caps. ⚠️

## Layout & spacing

- **The Mucha composition** (poster formula, ✅): central arched or circular panel (the "halo" — sun, moon, or floral wreath) behind the subject; vertical botanical borders flanking left/right; title integrated into a decorated base band at the bottom.
- **Arches everywhere:** panels and image frames are round-topped (semicircular or pointed arch), often double-ruled. Rectangular cards must earn their corners with ornament — plain `border-radius: 8px` boxes read as modern UI, not Nouveau.
- **Radius:** architectural — arches are semicircles (`border-radius: 50% 50% 0 0 / 100% 100% 0 0` on a tall panel), small details use 0–2px. Shadows: none, or a single flat offset "print misregistration" shadow in a muted tone — never blurred black shadows. ⚠️
- **Spacing scale:** generous air, 8-based grid is fine but *rhythm* matters more than math — let ornament breathe. Content column ≤ 720px centered inside wider ornamental margins.

## Components

All snippets assume the palette tokens above and an inline-SVG ornament approach (no external assets).

### 1. Ornamental page frame (double-ruled with corner flourishes)

```html
<div class="nouveau-frame">
  <svg class="corner tl" viewBox="0 0 80 80" aria-hidden="true">
    <path d="M4 76 V28 Q4 4 28 4 H76" fill="none" stroke="#C9962E" stroke-width="2.5"/>
    <path d="M12 76 V34 Q12 12 34 12 H76" fill="none" stroke="#C9962E" stroke-width="1"/>
    <circle cx="28" cy="28" r="5" fill="none" stroke="#C9962E" stroke-width="1.5"/>
    <path d="M28 23 q10 -12 22 -14 q-12 4 -14 16 q6 -8 16 -9 q-10 3 -12 12 Z" fill="#7A7444"/>
  </svg>
  <!-- repeat .tr .bl .br with rotate transforms -->
  <div class="nouveau-frame-inner">
    <!-- page content -->
  </div>
</div>
```

```css
.nouveau-frame { border: 3px double #C9962E; padding: 10px; background: #F3E7CB; }
.nouveau-frame-inner { border: 1px solid #C9962E; padding: clamp(1.5rem, 4vw, 3rem); position: relative; }
.corner { position: absolute; width: 64px; height: 64px; }
.corner.tl { top: 14px; left: 14px; }
.corner.tr { top: 14px; right: 14px; transform: scaleX(-1); }
.corner.bl { bottom: 14px; left: 14px; transform: scaleY(-1); }
.corner.br { bottom: 14px; right: 14px; transform: scale(-1); }
```

### 2. Arch panel (Mucha's signature round-topped frame)

```html
<figure class="arch-panel">
  <svg viewBox="0 0 200 260" aria-hidden="true"><!-- halo + figure art --></svg>
  <figcaption>Eau de Parfum · 50 ml</figcaption>
</figure>
```

```css
.arch-panel {
  border: 2px solid #33291F; outline: 1px solid #C9962E; outline-offset: 6px;
  border-radius: 999px 999px 0 0; overflow: hidden; background: #FBF4E2;
  max-width: 320px;
}
.arch-panel figcaption {
  text-align: center; font-family: Georgia, serif; letter-spacing: .22em;
  text-transform: uppercase; font-size: .75rem; padding: .9rem; color: #33291F;
  border-top: 1px solid #C9962E;
}
```

### 3. Halo medallion (ornamental nimbus behind a subject)

```html
<div class="halo">
  <svg viewBox="0 0 200 200" aria-hidden="true">
    <circle cx="100" cy="100" r="92" fill="none" stroke="#C9962E" stroke-width="2"/>
    <circle cx="100" cy="100" r="82" fill="none" stroke="#C9962E" stroke-width="1" stroke-dasharray="3 5"/>
    <!-- sunburst rays -->
    <g stroke="#D9B45C" stroke-width="1.5">
      <line x1="100" y1="8" x2="100" y2="26"/><line x1="100" y1="174" x2="100" y2="192"/>
      <line x1="8" y1="100" x2="26" y2="100"/><line x1="174" y1="100" x2="192" y2="100"/>
    </g>
    <circle cx="100" cy="100" r="60" fill="#FBF4E2"/>
  </svg>
  <span class="halo-label">Est. 1897</span>
</div>
```

### 4. Whiplash divider (coup de fouet rule between sections)

```html
<div class="whiplash" role="separator" aria-hidden="true">
  <svg viewBox="0 0 600 60" preserveAspectRatio="none">
    <path d="M10 40 C 120 40, 160 10, 260 22 S 420 52, 590 28"
          fill="none" stroke="#7A7444" stroke-width="3" stroke-linecap="round"/>
    <path d="M10 40 C 120 40, 160 10, 260 22 S 420 52, 590 28"
          fill="none" stroke="#33291F" stroke-width="1" stroke-dasharray="1 0" opacity="0.35"
          transform="translate(0,4)"/>
    <!-- tapering leaf at the tail -->
    <path d="M560 30 q 30 -10 34 -26 q -18 6 -24 22 q 8 -4 18 -4 q -12 2 -16 12 Z" fill="#7A7444"/>
    <circle cx="10" cy="40" r="4" fill="#C9962E"/>
  </svg>
</div>
```

### 5. Botanical side border (vertical ornament strip)

```html
<aside class="vine-border" aria-hidden="true">
  <svg viewBox="0 0 60 600" preserveAspectRatio="xMidYMin slice">
    <path d="M30 0 C 10 120, 50 240, 30 360 C 12 470, 48 540, 30 600"
          fill="none" stroke="#7A7444" stroke-width="2.5"/>
    <g fill="#9AA46B">
      <ellipse cx="22" cy="90" rx="10" ry="4" transform="rotate(-30 22 90)"/>
      <ellipse cx="38" cy="180" rx="10" ry="4" transform="rotate(30 38 180)"/>
      <ellipse cx="22" cy="270" rx="10" ry="4" transform="rotate(-30 22 270)"/>
      <ellipse cx="38" cy="360" rx="10" ry="4" transform="rotate(30 38 360)"/>
      <ellipse cx="22" cy="450" rx="10" ry="4" transform="rotate(-30 22 450)"/>
    </g>
    <g fill="#C98A7D">
      <circle cx="30" cy="135" r="7"/><circle cx="30" cy="315" r="7"/><circle cx="30" cy="495" r="7"/>
    </g>
  </svg>
</aside>
```

### 6. Arch tab (section navigation shaped like a niche)

```html
<nav class="arch-tabs" role="tablist" aria-label="Collections">
  <button class="arch-tab is-active" role="tab" aria-selected="true">Floral</button>
  <button class="arch-tab" role="tab" aria-selected="false">Oriental</button>
  <button class="arch-tab" role="tab" aria-selected="false">Citrus</button>
</nav>
```

```css
.arch-tab {
  font-family: Georgia, serif; text-transform: uppercase; letter-spacing: .18em;
  font-size: .8rem; color: #33291F; background: transparent;
  border: 1.5px solid #7A7444; border-bottom: none;
  border-radius: 999px 999px 0 0; padding: .8rem 1.6rem .7rem; cursor: pointer;
}
.arch-tab.is-active { background: #33291F; color: #F3E7CB; border-color: #33291F; }
.arch-tab:hover:not(.is-active) { background: #D9B45C33; }
```

### 7. Ornamental button (oval, double-ruled)

```html
<a class="nouv-btn" href="#atelier">Discover the Atelier</a>
```

```css
.nouv-btn {
  display: inline-block; font-family: Georgia, serif; text-transform: uppercase;
  letter-spacing: .22em; font-size: .8rem; text-decoration: none; color: #F3E7CB;
  background: #33291F; padding: 1rem 2.4rem; border-radius: 999px;
  outline: 1px solid #C9962E; outline-offset: 4px;
  transition: background .35s ease, outline-color .35s ease;
}
.nouv-btn:hover { background: #6B4A2F; outline-color: #D9B45C; }
.nouv-btn--ghost { background: transparent; color: #33291F; border: 1.5px solid #33291F; }
```

### 8. Price vignette (product card as a small framed panel)

```html
<article class="vignette">
  <div class="vignette-arch">
    <!-- product illustration (inline SVG) -->
  </div>
  <h3>Nuit d'Iris</h3>
  <p class="vignette-notes">Iris · violet leaf · blond woods</p>
  <p class="vignette-price">€ 88 <span>· 50 ml</span></p>
</article>
```

```css
.vignette { text-align: center; max-width: 260px; }
.vignette-arch {
  border: 1.5px solid #33291F; border-radius: 999px 999px 0 0;
  background: #FBF4E2; aspect-ratio: 3/4; overflow: hidden;
}
.vignette h3 { font-family: Georgia, serif; font-weight: 400; letter-spacing: .14em;
  text-transform: uppercase; margin: 1rem 0 .3rem; }
.vignette-notes { font-style: italic; color: #6B4A2F; font-size: .9rem; margin: 0; }
.vignette-price { letter-spacing: .1em; margin: .6rem 0 0; }
.vignette-price span { color: #6B4A2F; font-size: .8rem; }
```

## Motion

Art Nouveau is a print-first style with no defined motion language — state it plainly rather than inventing one. On screens, translate its spirit as *slow growth*: transitions of 500–800 ms with gentle ease (`cubic-bezier(.22,.61,.36,1)`), elements that bloom/scale from 0.96 rather than slide, and `prefers-reduced-motion` collapsing everything to an instant crossfade. Nothing may bounce, pop, or snap. ⚠️

## Do / Don't

- ✅ **Do** let borders, frames, and lettering grow from the same botanical line system — a rule that turns into a vine at its ends reads as Nouveau; a plain `<hr>` does not.
- ❌ **Don't** use sharp, unornamented rectangles for primary panels — arch the tops or frame them doubly in gold.
- ✅ **Do** keep the palette muted and warm: parchment grounds, olive/sage greens, gold as flat ink, one deep anchor tone.
- ❌ **Don't** reach for neon, saturated brights, or blue-purple gradients — Mucha's inks were earth, pastel, and bronze.
- ✅ **Do** set display type in tracked-out capitals, arched or banded, as part of the ornament (like Gismonda's mosaic title).
- ❌ **Don't** set body copy in a geometric sans or center every line — the style's hierarchy is one large title, a graceful subhead, then quiet organized columns.
- ✅ **Do** compose asymmetrically: an off-center arch, a vine that climbs one side, weight that settles like growth.
- ❌ **Don't** use blurred drop shadows, glassmorphism, or photorealistic textures — depth comes from fine hatching and layered flat washes.

## Copy voice (for brand styles)

Language is lyrical but precise, Belle Époque commercial poetry: product names in French, descriptions in flowing English, nature metaphors for craft. It promises *artistry*, never speed or disruption.

- "Distilled by hand, adorned by nature — our iris rests twelve weeks in oak before it ever meets the flacon."
- "The Autumn Collection: four eaux de parfum, pressed like flowers between the pages of the year."
- "Visit the atelier on Rue des Lilas — Saturdays we decant the week's pressing while the copper stills are warm."

## Sources consulted

- classicalcanvas.org — analyses of Mucha's "Gismonda", "Whitman's Chocolates", "Soap Factory of Bagnolet" (composition, mosaic typography, palette, whiplash hair)
- en.wikipedia.org — "Whiplash (decorative art)": coup de fouet, Obrist's Cyclamen, motif vocabulary
- vectree.io — Art Nouveau map: whiplash curve structure, botanical vitalism
- aesthetics.fandom.com — Art Nouveau: palette description (olive, brown, pale pink, gold), motif lists
- github.com/0xzgbot/hermes-media-skill-pack — Art Nouveau specialist summary: the Mucha composition formula
