---
name: mid-century
description: Mid-century modern design (1945–1969) — warm woods, mustard/teal/burnt-orange palette, starburst motifs, clean grotesques with script accents. Use for optimistic, functionalist, 1950s-flavored pages.
---

# Mid-Century Modern

The design language of the post-war American living room: Charles and Ray Eames,
Eero Saarinen, George Nelson, Florence Knoll — and the 1950s graphic designers
who turned the Atomic Age into advertising. Clean lines, organic curves, honest
materials, and unapologetic optimism about the future.

## Principles

1. **Form follows function, happily.** Every curve and taper earns its place —
   like the molded plywood of an Eames lounge chair or a credenza's splayed legs.
   Nothing is ornamented; ornament comes from honest construction.
2. **Warmth over coldness.** Walnut and teak tones, wool and linen textures,
   warm cream paper — never cold sterile white. Technology is friendly here:
   chrome curves, smiling appliances, Sputnik as a toy.
3. **Optimistic functionalism.** The copy and the shapes both say the future is
   bright and you're invited. Boomerangs, starbursts, and orbit paths signal
   joy, not kitsch.
4. **Contrast of organic and geometric.** Kidney-shaped tables meet strict
   modular grids; amoeba coffee tables sit next to starburst clocks. Pair soft
   biomorphic shapes with hard geometry.
5. **Democratic design.** Mid-century pieces were made to be mass-produced and
   affordable. The web equivalent: layouts that work for everyone, generous
   whitespace, no gatekeeping flourishes.

## Color

Warm cream ground, period triad on top. Text in warm charcoal — never pure black.

| Token | Hex | Role | Legend |
|---|---|---|---|
| `--cream` | `#F5ECD7` | Page background; warm paper, never cold white | ✅ |
| `--mustard` | `#E5A535` | Primary accent; buttons, badges, starburst fills | ✅ |
| `--teal` | `#1FBFB8` | Secondary accent; links, highlights, orbit paths | ✅ |
| `--burnt-orange` | `#E8601C` | Energy accent; CTAs, prices, starburst cores | ✅ |
| `--charcoal` | `#3D3D3D` | Body text, outlines; always slightly warm | ✅ |
| `--walnut` | `#5E4633` | Wood tone; nav bars, footers, furniture in illustrations | ⚠️ |
| `--olive` | `#5E6B3A` | Tertiary accent; tags, details | 🟡 |
| `--avocado` | `#6B8F3C` | Soft green accent; nature motifs | 🟡 |
| `--brick` | `#B5403A` | Danger/error, sale badges, period red | 🟡 |

Period pairings: **Classic Atomic** (teal + burnt orange + mustard on cream),
**Harvest** (avocado + mustard + burnt orange on cream), **Diner**
(coral + mint + chrome + charcoal). Flat color fills — no gradients.

## Typography

Period-correct typefaces: **Helvetica** (1957), **Univers** (1957), **Futura**
(1927, the MCM advertising workhorse), Akzidenz-Grotesk for text. Script accents
for the friendly advertising voice — mid-century ads paired clean grotesques with
casual brush scripts for taglines and product names.

Closest free substitutes: `Archivo` or `Libre Franklin` for the grotesque;
`Caveat` or `Pacifico` for script accents. Headlines: grotesque, 600–800 weight,
tight-ish tracking, often ALL CAPS with wide letterspacing for section labels.
Body: 400, generous line-height (1.6+). Script: sparing — one tagline or product
name per view, never for body text.

Scale: display 40–64px / section titles 24–32px / body 16–18px. Section labels in
small caps with a starburst bullet before them.

## Layout & spacing

- **Strict modular grid**, 12 columns, max-width 1120–1280px. Mid-century loved
  order; whitespace is the luxury material.
- **Generous section padding**: 72–112px vertical, pages breathe like a
  well-proportioned living room.
- **Radius**: small — 2–6px. Sharp corners with rounded biomorphic accents; never
  fully pill-shaped.
- **Borders**: 2px solid charcoal rules separate sections; hairline rules inside
  spec rows. Shadows are flat offset (4px 4px 0 charcoal) — never soft blurred
  shadows, never glass.
- **Starburst dividers** between major sections; section numbers in small caps
  ("Nº 3 — Seating").
- Wood-tone rails: dark walnut nav and footer anchor the cream page like
  furniture anchors a room.

## Components

### 1. Starburst hero (with SVG burst + script kicker)

```html
<section class="hero">
  <p class="kicker"><span class="script">New for</span> THE '59 COLLECTION</p>
  <h1>Furniture for the way<br>you live <em>now.</em></h1>
  <p class="lede">Solid walnut. Molded plywood. Zero clutter.</p>
  <a class="btn btn-primary" href="#">Browse the collection</a>
  <svg class="burst" viewBox="0 0 200 200" aria-hidden="true">
    <g fill="#E5A535">
      <!-- 12 tapered rays -->
      <polygon points="100,0 108,78 92,78"/>
      <polygon points="100,200 108,122 92,122"/>
      <polygon points="0,100 78,108 78,92"/>
      <polygon points="200,100 122,108 122,92"/>
      <polygon points="29,29 96,88 88,96"/>
      <polygon points="171,171 104,112 112,104"/>
      <polygon points="171,29 104,96 112,88"/>
      <polygon points="29,171 96,104 88,112"/>
      <polygon points="65,6 102,80 86,82"/>
      <polygon points="135,194 98,120 114,118"/>
      <polygon points="6,65 80,102 82,86"/>
      <polygon points="194,135 120,98 118,114"/>
    </g>
    <circle cx="100" cy="100" r="26" fill="#E8601C"/>
    <circle cx="100" cy="100" r="12" fill="#F5ECD7"/>
  </svg>
</section>
```

```css
.hero { background: #F5ECD7; padding: 96px 24px; position: relative; overflow: hidden; }
.hero h1 { font-family: "Archivo", sans-serif; font-weight: 800; font-size: clamp(40px, 6vw, 72px); color: #3D3D3D; letter-spacing: -0.01em; }
.hero h1 em { font-style: normal; color: #E8601C; }
.kicker { letter-spacing: 0.28em; font-size: 13px; font-weight: 700; color: #3D3D3D; }
.script { font-family: "Pacifico", "Brush Script MT", cursive; letter-spacing: 0; font-size: 1.35em; color: #E8601C; }
.lede { font-size: 19px; color: #3D3D3D; }
.burst { position: absolute; right: -40px; top: 50%; width: 340px; transform: translateY(-50%); opacity: .9; }
```

### 2. Atomic divider (starburst rule between sections)

```html
<div class="atomic-divider" aria-hidden="true">
  <span class="rule"></span>
  <svg viewBox="0 0 40 40" width="40" height="40">
    <g fill="#E5A535">
      <polygon points="20,0 23,15 17,15"/><polygon points="20,40 23,25 17,25"/>
      <polygon points="0,20 15,23 15,17"/><polygon points="40,20 25,23 25,17"/>
      <polygon points="6,6 19,17 17,19"/><polygon points="34,34 21,23 23,21"/>
      <polygon points="34,6 21,17 23,19"/><polygon points="6,34 19,23 17,21"/>
    </g>
    <circle cx="20" cy="20" r="6" fill="#E8601C"/>
  </svg>
  <span class="rule"></span>
</div>
```

```css
.atomic-divider { display: flex; align-items: center; gap: 16px; margin: 0 auto; max-width: 1120px; padding: 0 24px; }
.atomic-divider .rule { flex: 1; height: 2px; background: #3D3D3D; }
```

### 3. Product card (tapered legs, spec strip)

```html
<article class="card">
  <div class="card-art" style="--wood:#5E4633">
    <svg viewBox="0 0 160 120" aria-hidden="true">
      <rect x="30" y="30" width="100" height="44" rx="6" fill="var(--wood)"/>
      <polygon points="42,74 34,112 42,112 50,74" fill="#3D3D3D"/>
      <polygon points="118,74 110,112 118,112 126,74" fill="#3D3D3D"/>
    </svg>
  </div>
  <div class="card-body">
    <p class="card-no">Nº 402</p>
    <h3>The Astral Lounge Chair</h3>
    <p class="card-desc">Molded walnut shell, wool bouclé cushion, splayed brass-tipped legs.</p>
    <div class="card-row"><span class="price">$289</span><a class="btn btn-small" href="#">Add to cart</a></div>
  </div>
</article>
```

```css
.card { background: #fff; border: 2px solid #3D3D3D; border-radius: 4px; overflow: hidden; }
.card-art { background: #1FBFB8; padding: 24px; display: grid; place-items: center; }
.card-body { padding: 20px 20px 24px; }
.card-no { font-size: 12px; letter-spacing: .22em; font-weight: 700; color: #E8601C; }
.card h3 { font-family: "Archivo", sans-serif; font-size: 22px; margin: 6px 0; color: #3D3D3D; }
.card-desc { font-size: 15px; color: #3D3D3D; line-height: 1.6; }
.card-row { display: flex; justify-content: space-between; align-items: center; margin-top: 16px; }
.price { font-size: 22px; font-weight: 800; color: #3D3D3D; }
```

### 4. Spec row (product details table)

```html
<dl class="specs">
  <div class="spec"><dt>Frame</dt><dd>Solid American walnut</dd></div>
  <div class="spec"><dt>Upholstery</dt><dd>Wool bouclé, mustard</dd></div>
  <div class="spec"><dt>Dimensions</dt><dd>28" W × 31" D × 29" H</dd></div>
  <div class="spec"><dt>Assembly</dt><dd>None — arrives ready</dd></div>
</dl>
```

```css
.specs { border-top: 2px solid #3D3D3D; }
.spec { display: grid; grid-template-columns: 160px 1fr; gap: 16px; padding: 14px 0; border-bottom: 1px solid #d8c9a8; }
.spec dt { font-size: 12px; letter-spacing: .2em; font-weight: 700; text-transform: uppercase; color: #5E6B3A; }
.spec dd { margin: 0; font-size: 16px; color: #3D3D3D; }
```

### 5. Buttons

```html
<a class="btn btn-primary" href="#">Shop the collection</a>
<a class="btn btn-outline" href="#">Our story</a>
```

```css
.btn { display: inline-block; font-family: "Archivo", sans-serif; font-weight: 700;
  font-size: 15px; letter-spacing: .08em; text-transform: uppercase; text-decoration: none;
  padding: 14px 28px; border: 2px solid #3D3D3D; border-radius: 3px; color: #3D3D3D; }
.btn-primary { background: #E5A535; box-shadow: 4px 4px 0 #3D3D3D; }
.btn-primary:hover { transform: translate(2px, 2px); box-shadow: 2px 2px 0 #3D3D3D; }
.btn-outline { background: transparent; }
.btn-outline:hover { background: #3D3D3D; color: #F5ECD7; }
```

### 6. Period badge ("New for '59")

```html
<span class="badge">New for '59</span>
```

```css
.badge { display: inline-block; background: #E8601C; color: #F5ECD7; font-size: 12px;
  font-weight: 800; letter-spacing: .18em; text-transform: uppercase; padding: 8px 14px;
  border: 2px solid #3D3D3D; border-radius: 3px; transform: rotate(-3deg); }
```

### 7. Collection filter tabs

```html
<div class="tabs" role="tablist">
  <button class="tab is-active" role="tab">All</button>
  <button class="tab" role="tab">Seating</button>
  <button class="tab" role="tab">Tables</button>
  <button class="tab" role="tab">Lighting</button>
</div>
```

```css
.tabs { display: flex; gap: 0; border: 2px solid #3D3D3D; border-radius: 3px; overflow: hidden; width: fit-content; }
.tab { font-family: "Archivo", sans-serif; font-weight: 700; font-size: 14px; letter-spacing: .06em;
  text-transform: uppercase; background: #F5ECD7; color: #3D3D3D; border: 0; border-right: 2px solid #3D3D3D;
  padding: 12px 24px; cursor: pointer; }
.tab:last-child { border-right: 0; }
.tab.is-active, .tab:hover { background: #1FBFB8; }
```

### 8. Testimonial / quote card

```html
<figure class="quote">
  <blockquote>"The Astral chair is the best seat in our house. Guests fight over it."</blockquote>
  <figcaption>— Mrs. D. Calloway, Palm Springs</figcaption>
</figure>
```

```css
.quote { background: #5E4633; color: #F5ECD7; border: 2px solid #3D3D3D; border-radius: 4px; padding: 32px; }
.quote blockquote { font-family: "Pacifico", "Brush Script MT", cursive; font-size: 24px; margin: 0 0 12px; }
.quote figcaption { font-size: 13px; letter-spacing: .18em; text-transform: uppercase; color: #E5A535; }
```

### 9. Walnut nav with script wordmark

```html
<nav class="topnav">
  <a class="wordmark" href="#">Hartwell <span>&amp; Rowe</span></a>
  <div class="navlinks"><a href="#">Collection</a><a href="#">Showrooms</a><a href="#">Catalog</a></div>
  <a class="btn btn-primary btn-nav" href="#">Order the catalog</a>
</nav>
```

```css
.topnav { background: #5E4633; color: #F5ECD7; display: flex; align-items: center; gap: 32px; padding: 16px 32px; }
.wordmark { font-family: "Pacifico", "Brush Script MT", cursive; font-size: 28px; color: #F5ECD7; text-decoration: none; }
.wordmark span { font-family: "Archivo", sans-serif; font-size: 13px; letter-spacing: .24em; text-transform: uppercase; }
.navlinks a { color: #F5ECD7; text-decoration: none; font-size: 14px; font-weight: 700; letter-spacing: .1em; text-transform: uppercase; margin-right: 24px; }
.navlinks a:hover { color: #E5A535; }
.btn-nav { padding: 10px 18px; margin-left: auto; box-shadow: 3px 3px 0 #3D3D3D; }
```

### 10. Footer with starburst mark

```html
<footer class="sitefoot">
  <svg class="footburst" viewBox="0 0 40 40" width="48" height="48" aria-hidden="true">…</svg>
  <p class="footline">Hartwell &amp; Rowe Furniture Co. — Grand Rapids, Michigan</p>
  <p class="footsub">Crafted since 1954 · Free delivery on orders over $99</p>
</footer>
```

```css
.sitefoot { background: #3D3D3D; color: #F5ECD7; text-align: center; padding: 56px 24px; }
.footline { font-size: 14px; letter-spacing: .2em; text-transform: uppercase; font-weight: 700; color: #E5A535; }
.footsub { font-size: 14px; color: #F5ECD7; opacity: .8; }
```

## Motion

Mid-century is a print-native movement: it has no motion language. One rule —
keep movement mechanical and cheerful: 160–240ms `ease-out`, flat translations
and fades only. No blur, no spring, no parallax, no slow cinematic easing.

## Do / Don't

- **Do** pair a clean grotesque headline with ONE script accent per view —
  **don't** set whole sentences in script.
- **Do** use warm cream grounds with flat period color blocks —
  **don't** use cold white or purple-blue gradients anywhere.
- **Do** draw starbursts, boomerangs, and orbit paths as simple flat SVG shapes —
  **don't** use drop shadows or 3D renders of them.
- **Do** show furniture on tapered, splayed legs with visible wood grain —
  **don't** show chunky blocky furniture or floating-with-soft-shadow cards.
- **Do** write prices, dimensions, and materials like a catalog —
  **don't** hide specs behind vague lifestyle copy.
- **Do** use small-caps section labels ("Nº 2 — Lighting") with a starburst
  bullet — **don't** use generic "Features" headings.

## Copy voice

Mid-century copy is optimistic, assured, and concrete — the 1959 catalog voice.
It states facts like compliments and promises a brighter everyday life.

- "Solid walnut, wool bouclé, and absolutely zero clutter. This is the way the modern home was meant to look."
- "New for '59: the Astral lounge chair. Sit down once — you'll understand."
- "Built in Grand Rapids. Guaranteed for a lifetime of Tuesday evenings."
