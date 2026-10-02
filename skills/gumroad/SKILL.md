---
name: gumroad
description: Gumroad's lo-fi, neo-brutalist creator commerce style — pink #FF90E8, thick black borders, hard offset shadows. Use for creator storefronts, digital-product pages, and playful anti-corporate commerce UIs.
---

# Gumroad

The look of [gumroad.com](https://gumroad.com/) since its 2021 redesign under
Sahil Lavingia: the internet's garage sale. Lo-fi, hand-drawn, deliberately
unpolished — thick black outlines, flat candy colors, and hard offset shadows
that make every element feel like a sticker slapped onto a creator's notebook.
The design does brand PR: *we're not a polished corporation. We're creators,
like you.*

## Principles

1. **Creator-first, corporate-never.** The aesthetic rejects SaaS polish on
   purpose. Every border, shadow, and doodle says: a person made this, and
   you could too. Rawness is the positioning, not a budget constraint.
2. **Sticker-book geometry.** Everything is a flat shape with a 2px black
   outline and a solid, unblurred shadow kicked 4–6px down-right. Cards,
   buttons, badges, and illustrations all share the same outline weight so
   the whole page reads as one collage.
3. **Flat color only — no gradients, no blur.** Gumroad's signature is candy
   flat color: pink `#FF90E8` hero sections, cream canvases, sunny yellow and
   mint accents. A gradient is the fastest way to break the illusion.
4. **Hand-drawn beats pixel-perfect.** Squiggly arrows, doodled stars,
   slightly wobbly illustrations, and rotated stickers give the page its
   zine energy. Keep them sparse and intentional — one arrow per section is
   plenty; a page full of doodles reads as noise.
5. **Oversized, honest commerce.** Prices are big and plain, ratings are
   plain stars with a count, CTAs say "Buy now" and mean it. No dark
   patterns, no fake scarcity timers, no countdown clocks.

## Color

Palette cross-referenced from gumroad.com, Gumroad's brand assets, and
documented teardowns (Medium/designstudiouiux neo-brutalism analysis,
Aesthetics Wiki, Figma community kits).

| Token | Hex | Role | Legend |
|---|---|---|---|
| Gumroad pink | `#FF90E8` | Primary brand color: CTAs, hero sections, highlights | ✅ |
| Pink deep | `#F56BB1` | Hover/pressed state for pink surfaces | 🟡 |
| Ink black | `#000000` | All outlines, body text, hard shadows, footer | ✅ |
| Cream | `#FFF9F2` | Page canvas, card backgrounds (softened to feel printed) | 🟡 |
| Paper white | `#FFFFFF` | Card interiors, input fields | ✅ |
| Sunny yellow | `#FFD02F` | Badges, star ratings, highlight blocks | 🟡 |
| Mint | `#90E8A3` | Secondary accent: tags, success states | 🟡 |
| Sky | `#90C9E8` | Tertiary accent: category chips, info blocks | 🟡 |
| Ink soft | `#2B2B2B` | Secondary body text (use sparingly; black is the default) | ⚠️ |
| Grey paper | `#EDE6DA` | Dividers, disabled fills, placeholder blocks | ⚠️ |

Notes: black is the only neutral. There is no grey text scale — secondary
information gets smaller size or a yellow highlight, not a lighter grey. Use
pink for action, yellow for delight, cream for rest.

## Typography

- **Face:** Mabry (✅ documented as Gumroad's brand typeface, designed by
  Colophon). No free license exists, so substitute freely: **Space Grotesk**
  (closest in quirk and proportion, 🟡 community-recommended substitute),
  **Archivo**, or **DM Sans** as second choice. System fallback:
  `system-ui, -apple-system, sans-serif`.
- **Voice in type:** headings are bold, sentence case or lowercase, tight
  leading (1.0–1.1), often paired with an underline or a yellow
  highlighter swipe. Body is regular weight, comfortable line height
  (1.5–1.6), never justified.
- **Scale (web):** Display 64–96px / H1 40–56px / H2 28–32px / H3 20–24px /
  body 16–18px / small 14px. Display headlines are sentence case with
  periods allowed ("Go from zero to $1.").
- **Rules:** never letterspace uppercase headings; never use light weights
  for display type; price tags and ratings always bold; keep one typeface
  across the whole page — mixing a second face breaks the lo-fi spell.

## Layout & spacing

- **Border:** `2px solid #000` on everything interactive — cards, buttons,
  inputs, badges. Never 1px hairlines, never `border: none`.
- **Shadow:** hard offset, zero blur: `box-shadow: 4px 4px 0 #000`. Large
  hero cards can push to `6px 6px 0 #000`. Never `rgba` soft shadows.
- **Radius:** mostly square with small `6–10px` radius on cards and buttons;
  pills reserved for tags and badges (`border-radius: 999px`).
- **Press effect:** primary buttons "press down" on `:active` —
  `transform: translate(2px, 2px)` with shadow shrinking to `2px 2px 0 #000`.
  This is the signature Gumroad interaction.
- **Spacing scale:** 8 / 16 / 24 / 32 / 48 / 64 / 96px. Generous whitespace
  between sections; content blocks themselves sit snug inside their bordered
  cards.
- **Backgrounds:** full-bleed pink section alternating with cream; never
  more than two background colors on screen at once.
- **Slight rotations:** `rotate(-1.5deg)` / `rotate(1deg)` on sticker badges
  and testimonial cards only — the grid stays straight, the stickers tilt.

## Components

### 1. Buy button (signature)

```html
<a class="btn-buy" href="#">Buy now — $24</a>
```
```css
.btn-buy {
  display: inline-block;
  background: #FF90E8;
  color: #000;
  font-weight: 700;
  font-size: 18px;
  padding: 14px 28px;
  border: 2px solid #000;
  border-radius: 8px;
  box-shadow: 4px 4px 0 #000;
  text-decoration: none;
  transition: transform 0.08s ease, box-shadow 0.08s ease;
}
.btn-buy:hover { background: #F56BB1; }
.btn-buy:active {
  transform: translate(4px, 4px);
  box-shadow: 0 0 0 #000;
}
```

### 2. Product card

```html
<article class="product-card">
  <img src="cover.jpg" alt="Lo-fi Beat Tape Vol. 3 cover" class="product-card__cover">
  <div class="product-card__body">
    <h3>Lo-fi Beat Tape Vol. 3</h3>
    <p class="product-card__creator">by Maya Reyes</p>
    <p class="product-card__rating">★★★★★ <span>4.9 (312)</span></p>
    <div class="product-card__row">
      <span class="price">$18</span>
      <a class="btn-buy btn-buy--sm" href="#">Buy</a>
    </div>
  </div>
</article>
```
```css
.product-card {
  background: #FFFFFF;
  border: 2px solid #000;
  border-radius: 10px;
  box-shadow: 6px 6px 0 #000;
  overflow: hidden;
  max-width: 320px;
}
.product-card__cover { display: block; width: 100%; border-bottom: 2px solid #000; }
.product-card__body { padding: 16px; }
.product-card__body h3 { margin: 0 0 4px; font-size: 20px; }
.product-card__creator { margin: 0; font-size: 14px; }
.product-card__rating { color: #000; font-weight: 700; }
.product-card__rating span { font-weight: 400; font-size: 14px; }
.product-card__row {
  display: flex; justify-content: space-between; align-items: center;
  margin-top: 12px;
}
.price { font-size: 24px; font-weight: 800; }
.btn-buy--sm { font-size: 15px; padding: 8px 18px; }
```

### 3. Creator profile chip

```html
<div class="creator-chip">
  <img src="avatar.jpg" alt="Portrait of Maya Reyes" class="creator-chip__avatar">
  <div>
    <strong>Maya Reyes</strong>
    <span>12k followers · 48 products</span>
  </div>
  <a class="btn-outline" href="#">Follow</a>
</div>
```
```css
.creator-chip {
  display: inline-flex; align-items: center; gap: 12px;
  background: #FFFFFF; border: 2px solid #000; border-radius: 12px;
  box-shadow: 4px 4px 0 #000; padding: 10px 16px 10px 10px;
}
.creator-chip__avatar {
  width: 48px; height: 48px; border-radius: 50%;
  border: 2px solid #000; object-fit: cover;
}
.creator-chip div { display: flex; flex-direction: column; }
.creator-chip span { font-size: 13px; }
```

### 4. Star rating row

```html
<p class="rating"><span aria-hidden="true">★★★★★</span> 4.9 · 312 ratings</p>
```
```css
.rating { font-size: 15px; font-weight: 700; }
.rating [aria-hidden] { color: #000; letter-spacing: 2px; }
```
Gumroad ratings are monochrome stars — no gold coloring, no gradient fill.

### 5. Checkout row (cart line item)

```html
<div class="checkout-row">
  <img src="cover.jpg" alt="">
  <div class="checkout-row__info">
    <strong>Lo-fi Beat Tape Vol. 3</strong>
    <span>Digital download · 212 MB</span>
  </div>
  <span class="price">$18</span>
  <button class="btn-remove" aria-label="Remove from cart">✕</button>
</div>
```
```css
.checkout-row {
  display: flex; align-items: center; gap: 16px;
  background: #FFFFFF; border: 2px solid #000; border-radius: 10px;
  box-shadow: 4px 4px 0 #000; padding: 12px 16px;
}
.checkout-row img { width: 56px; height: 56px; border: 2px solid #000; border-radius: 6px; }
.checkout-row__info { flex: 1; display: flex; flex-direction: column; }
.checkout-row__info span { font-size: 13px; }
.btn-remove {
  background: #FFF9F2; border: 2px solid #000; border-radius: 6px;
  width: 32px; height: 32px; font-weight: 700; cursor: pointer;
}
.btn-remove:hover { background: #FF90E8; }
```

### 6. Nav

```html
<header class="nav">
  <a class="nav__logo" href="#">gumroad</a>
  <nav>
    <a href="#">Discover</a><a href="#">Sell</a><a href="#">Pricing</a>
  </nav>
  <div class="nav__actions">
    <a href="#">Log in</a>
    <a class="btn-buy btn-buy--sm" href="#">Start selling</a>
  </div>
</header>
```
```css
.nav {
  display: flex; align-items: center; justify-content: space-between;
  padding: 16px 24px; background: #FFF9F2;
  border-bottom: 2px solid #000;
}
.nav__logo { font-size: 26px; font-weight: 800; color: #000; text-decoration: none; }
.nav nav { display: flex; gap: 24px; }
.nav nav a, .nav__actions a { color: #000; text-decoration: none; font-weight: 600; }
.nav__actions { display: flex; gap: 16px; align-items: center; }
```

### 7. Highlight swash (hand-drawn underline)

```html
<h2>Make your own <span class="hl">road</span>.</h2>
```
```css
.hl {
  background: #FFD02F;
  padding: 0 6px;
  border: 2px solid #000;
  border-radius: 4px;
  box-shadow: 2px 2px 0 #000;
  white-space: nowrap;
}
```

### 8. Sticker badge (rotated)

```html
<span class="sticker">Bestseller ★</span>
```
```css
.sticker {
  display: inline-block;
  background: #FFD02F; color: #000; font-weight: 800; font-size: 13px;
  border: 2px solid #000; border-radius: 999px; padding: 6px 14px;
  box-shadow: 3px 3px 0 #000;
  transform: rotate(-3deg);
}
```

### 9. Marquee ticker

```html
<div class="ticker" aria-hidden="true">
  <div class="ticker__track">
    <span>Sell anything ★ Go from zero to $1 ★ Keep 90% of every sale ★</span>
    <span>Sell anything ★ Go from zero to $1 ★ Keep 90% of every sale ★</span>
  </div>
</div>
```
```css
.ticker { background: #000; color: #FF90E8; overflow: hidden;
  border-top: 2px solid #000; border-bottom: 2px solid #000; padding: 10px 0; }
.ticker__track { display: inline-flex; gap: 0; white-space: nowrap;
  animation: ticker 18s linear infinite; font-weight: 700; }
.ticker__track span { padding-right: 24px; }
@keyframes ticker { to { transform: translateX(-50%); } }
```

### 10. Testimonial card

```html
<figure class="quote-card">
  <blockquote>"I uploaded a file, set a price, and made my first $50 before lunch."</blockquote>
  <figcaption>— Priya N., sells Notion templates</figcaption>
</figure>
```
```css
.quote-card {
  background: #FFFFFF; border: 2px solid #000; border-radius: 10px;
  box-shadow: 6px 6px 0 #000; padding: 24px; max-width: 340px;
  transform: rotate(1deg);
}
.quote-card blockquote { margin: 0 0 12px; font-size: 18px; font-weight: 600; }
.quote-card figcaption { font-size: 14px; }
```

## Motion

Minimal. One signature interaction and one ambient loop:

- **Button press** (the core motion language): on click, the element
  translates 4px down-right and its shadow collapses —
  `transition: transform 0.08s ease, box-shadow 0.08s ease`. Everything else
  should feel instant, like paper.
- **Marquee ticker** at a slow, steady `linear` pace — the only ambient
  animation. Pause it under `prefers-reduced-motion`.

No scroll-triggered reveals, no parallax, no spring physics, no gradient
animation. If it doesn't feel like a sticker, don't animate it.

## Do / Don't

- **Do** use exactly `2px solid #000` outlines at every size — **don't**
  drop to 1px hairlines on mobile to "look cleaner".
- **Do** kick hard shadows 4–6px down-right with zero blur — **don't**
  soften them with `rgba` blur shadows.
- **Do** write prices as plain bold numbers ($18, not $17.99) — **don't**
  use charm pricing; Gumroad creators price honestly.
- **Do** make every CTA a pink `#FF90E8` slab with a press-down effect —
  **don't** use ghost buttons or text links for the primary action.
- **Do** keep one doodle per section (squiggle, star, arrow) — **don't**
  fill the page with hand-drawn clip art.
- **Do** rotate only stickers and quote cards (±1–3°) — **don't** tilt the
  grid, nav, or product cards.
- **Do** write ratings as `4.9 (312)` with monochrome stars — **don't**
  color the stars gold or add review-badge chrome.
- **Don't** add gradients, glass blur, or soft drop shadows — Gumroad's
  flatness is load-bearing, not laziness.

## Copy voice (for brand styles)

Gumroad's copy is direct, creator-side, and allergic to startup jargon.
Short sentences. Second person. Money talk without the hustle-bro stink.

- "Go from zero to $1." (the brand's mission, stated as a nudge, not a slogan)
- "Sell anything. Video lessons. Monthly subscriptions. Whatever!"
- "I uploaded a file, set a price, and I was selling on the internet before
  lunch."
- "Start small. Get better together. Learn quickly." — the "Gumroad Way"
  trio; plain verbs, no adjectives.

Avoid: "leverage", "ecosystem", "synergy", "disrupt", growth-hacker
superlatives, and any promise that sounds like a get-rich scheme. Gumroad
sells the *first dollar*, not the lambo.
