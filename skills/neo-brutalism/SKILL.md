---
name: neo-brutalism
description: Chunky Gumroad-style neo-brutalism — thick black borders, hard offset shadows, loud flat colors. Use for playful, high-energy landing pages, indie SaaS, and creator-economy brands that want to be impossible to ignore.
---

# Neo-Brutalism

Neubrutalism: brutalism after a design system got hold of it. Born with
[Gumroad's 2021 redesign](https://gumroad.com), popularized by Figma community
kits and [neobrutalism.dev](https://www.neobrutalism.dev) component libraries
(neobrutalism-components, BoldKit, etc.). It keeps brutalism's rawness — thick
outlines, flat fills, hard shadows — as deliberate, orderly decoration:
one typeface, a fixed palette, a strict grid, and nothing accidental.

## Principles

1. **The border is the design.** Every interactive surface gets a thick
   (2–4px) solid black outline. The border is the primary styling device —
   it carries the visual weight, not backgrounds or gradients.
2. **Depth is physical, not atmospheric.** Shadows are hard, offset, solid
   black blocks with zero blur (`4px 4px 0 #000`), never soft glows.
   Elements feel like paper stickers pressed onto a surface.
3. **Color is loud and flat.** Saturated un-tinted fills on a warm
   cream/paper canvas. Max 3–4 block colors per page. No gradients, no mesh,
   no aurora — ever.
4. **Interaction is a button you can feel.** Hover lifts the element and
   grows its shadow; pressing translates it *into* its own shadow until the
   shadow disappears. ~80ms, linear.
5. **Loud AND aligned.** The energy is comic-book; the grid underneath is
   rigorous. No random rotation on structural elements, no rainbow soup.
6. **Honest structure.** Boxes look like boxes. The skeleton of the layout
   stays visible — thick dividers, obvious grid, density without clutter.

## Color

Background is warm cream, never pure white (looks cold). Pick 1 primary +
1–2 accents from the block set; text and borders are always near-black ink.

| Token | Hex | Role | Confidence |
|---|---|---|---|
| `ink` | `#0A0A0A` | Borders, shadows, text | ✅ documented (border/shadow color in neubrutalist component specs) |
| `paper` | `#FFF9E6` | Page background, warm cream | 🟡 cross-referenced (documented as the neo-brutalist canvas) |
| `yell` | `#FFD803` | Primary — the "Gumroad yellow" | ✅ documented (Gumroad's signature yellow) |
| `pink` | `#FF6B9D` | Accent block | 🟡 cross-referenced (documented accent) |
| `cyan` | `#00E5FC` | Accent block | 🟡 cross-referenced (documented accent) |
| `lime` | `#A6FF4D` | Accent block | 🟡 cross-referenced (documented accent) |
| `coral` | `#FF7B7B` | Accent block (hsl 0 84% 71%) | 🟡 cross-referenced (BoldKit neubrutalism theme tokens) |
| `mustard` | `#FFD66B` | Accent block (hsl 49 100% 71%) | 🟡 cross-referenced (BoldKit neubrutalism theme tokens) |
| `teal` | `#47C2B0` | Accent block (hsl 174 62% 56%) | 🟡 cross-referenced (BoldKit neubrutalism theme tokens) |
| `white` | `#FFFFFF` | Text on dark blocks, stamp text | ⚠️ community approximation |

Rules: solid fills only — gradients, mesh, and blur are forbidden. Black text
on yellow/pink/cyan/lime; white text on black blocks. Dark variant:
`ink` background, accents go neon — rarely needed, use sparingly.

## Typography

- **Display:** heavy grotesque — `Archivo Black` (closest free match to the
  genre; 🟡 cross-referenced). All-caps, tight leading, oversized.
  Gumroad itself used ABC Favorit (✅ documented) — not free; Archivo Black
  or Anton are the standard free stand-ins.
- **Body:** `Space Grotesk` 400/500/700 (🟡 cross-referenced), generous size
  (16–18px), never light weights.
- **Labels/stamps:** monospace uppercase with letterspacing
  (`Space Mono` or `IBM Plex Mono`, ⚠️ community convention) for badges,
  eyebrows, and "stamp" stickers.
- One typeface per role; never mix display faces. Headline case: ALL-CAPS.

## Layout & spacing

- **Grid:** 12-col or simple block grid, one repeated gap value (24–32px).
  Axis-aligned only — no rotated structural blocks (rotation is reserved for
  stickers/stamps).
- **Radius:** `0` (pure) or a small consistent radius (`4–8px`) for the
  friendlier variant. The border + shadow matter more than the corner.
- **Borders:** `2px solid #0A0A0A` on inputs/badges; `3px` on cards;
  `4px` on hero blocks and primary CTAs. Never 1px, never colored borders.
- **Shadows (zero blur, always):** small `4px 4px 0`, standard `6px 6px 0`,
  hero `8px 8px 0` — solid black block, no blur, no spread.
- **Spacing:** generous, chunky padding (16/24/32/48px). Elements must feel
  substantial and unapologetic.
- **Signature decoration:** a scrolling marquee strip, a tilted "stamp"
  badge (`rotate(-8deg)`, bordered, all-caps), and a halftone/dot or grid
  background pattern — pick at most two per page.

## Components

All examples below are plain HTML/CSS, copy-pasteable. Assumes the color
tokens as CSS custom properties (`--ink`, `--paper`, `--yell`, ...).

**1. Chunky button (the signature)**

```html
<button class="nb-btn">GET STARTED</button>
```
```css
.nb-btn {
  font-family: "Archivo Black", "Arial Black", sans-serif;
  font-size: 1rem; letter-spacing: 0.04em;
  background: var(--yell, #FFD803); color: #0A0A0A;
  border: 3px solid #0A0A0A; border-radius: 6px;
  box-shadow: 4px 4px 0 #0A0A0A;
  padding: 14px 28px; cursor: pointer;
  transition: transform 80ms linear, box-shadow 80ms linear;
}
.nb-btn:hover { transform: translate(-2px, -2px); box-shadow: 6px 6px 0 #0A0A0A; }
.nb-btn:active { transform: translate(4px, 4px); box-shadow: 0 0 0 #0A0A0A; }
```

**2. Card**

```html
<div class="nb-card">
  <h3>LOUD FEATURE</h3>
  <p>One plain sentence about what it does.</p>
</div>
```
```css
.nb-card {
  background: #FFF9E6; border: 3px solid #0A0A0A; border-radius: 8px;
  box-shadow: 6px 6px 0 #0A0A0A; padding: 28px;
}
.nb-card h3 { font-family: "Archivo Black", sans-serif; margin: 0 0 12px; }
```

**3. Marquee strip**

```html
<div class="nb-marquee"><div class="nb-marquee-track">
  <span>NO GRADIENTS</span><span>NO BLUR</span><span>NO SUBTLETY</span>
  <span>NO GRADIENTS</span><span>NO BLUR</span><span>NO SUBTLETY</span>
</div></div>
```
```css
.nb-marquee {
  background: #0A0A0A; color: #FFD803; overflow: hidden;
  border-top: 3px solid #0A0A0A; border-bottom: 3px solid #0A0A0A;
  padding: 12px 0; white-space: nowrap;
}
.nb-marquee-track { display: inline-block; animation: nb-scroll 18s linear infinite; }
.nb-marquee-track span {
  font-family: "Archivo Black", sans-serif; font-size: 1.25rem;
  padding: 0 28px;
}
@keyframes nb-scroll { to { transform: translateX(-50%); } }
```

**4. Badge / stamp**

```html
<span class="nb-badge">NEW</span>
<span class="nb-stamp">NO REFUNDS ON STYLE</span>
```
```css
.nb-badge {
  display: inline-block; background: #FF6B9D; color: #0A0A0A;
  font: 700 0.8rem "Space Mono", monospace; letter-spacing: 0.08em;
  border: 2px solid #0A0A0A; border-radius: 999px; padding: 6px 14px;
  box-shadow: 3px 3px 0 #0A0A0A;
}
.nb-stamp {
  display: inline-block; background: #FFF9E6; color: #0A0A0A;
  font-family: "Archivo Black", sans-serif; font-size: 0.95rem;
  border: 3px solid #0A0A0A; padding: 10px 18px;
  transform: rotate(-8deg); box-shadow: 4px 4px 0 #0A0A0A;
}
```

**5. Nav bar**

```html
<nav class="nb-nav">
  <a class="nb-logo" href="#">YELL&reg;</a>
  <div class="nb-links"><a href="#">Pricing</a><a href="#">Manifesto</a></div>
  <button class="nb-btn nb-btn-sm">SIGN UP</button>
</nav>
```
```css
.nb-nav {
  display: flex; align-items: center; gap: 24px;
  background: #FFF9E6; border-bottom: 3px solid #0A0A0A; padding: 14px 28px;
}
.nb-logo { font-family: "Archivo Black", sans-serif; font-size: 1.5rem; color: #0A0A0A; text-decoration: none; }
.nb-links { display: flex; gap: 20px; margin-left: auto; }
.nb-links a { color: #0A0A0A; font-weight: 700; text-decoration: none; }
.nb-links a:hover { text-decoration: underline; text-decoration-thickness: 3px; text-underline-offset: 4px; }
.nb-btn-sm { padding: 8px 18px; font-size: 0.85rem; }
```

**6. Forms (input + label)**

```html
<label class="nb-label" for="nb-email">EMAIL</label>
<input class="nb-input" id="nb-email" type="email" placeholder="you@loud.com">
```
```css
.nb-label { display: block; font: 700 0.8rem "Space Mono", monospace; letter-spacing: 0.08em; margin-bottom: 8px; }
.nb-input {
  width: 100%; font: 500 1rem "Space Grotesk", sans-serif;
  background: #fff; border: 3px solid #0A0A0A; border-radius: 6px;
  padding: 14px 16px; box-shadow: 4px 4px 0 #0A0A0A; outline: none;
}
.nb-input:focus { transform: translate(-2px, -2px); box-shadow: 6px 6px 0 #0A0A0A; }
```

**7. Pricing block**

```html
<div class="nb-card nb-price">
  <span class="nb-badge">MOST LOUD</span>
  <p class="nb-plan">PRO</p>
  <p class="nb-amount">$19<span>/mo</span></p>
  <ul><li>Unlimited everything</li><li>Zero subtlety</li></ul>
  <button class="nb-btn">GO PRO</button>
</div>
```
```css
.nb-price { background: #FFD803; text-align: left; }
.nb-plan { font: 700 0.85rem "Space Mono", monospace; letter-spacing: 0.1em; margin: 16px 0 4px; }
.nb-amount { font-family: "Archivo Black", sans-serif; font-size: 3rem; margin: 0 0 16px; }
.nb-amount span { font: 700 1rem "Space Grotesk", sans-serif; }
.nb-price ul { list-style: none; padding: 0; margin: 0 0 20px; font-weight: 700; }
.nb-price li::before { content: "\2713\0020"; font-weight: 900; }
```

**8. Alert / callout**

```html
<div class="nb-alert"><strong>HEADS UP:</strong> This offer ends when the marquee stops.</div>
```
```css
.nb-alert {
  background: #00E5FC; border: 3px solid #0A0A0A; border-radius: 6px;
  box-shadow: 5px 5px 0 #0A0A0A; padding: 16px 20px; font-weight: 700;
}
```

**9. Accordion (FAQ)**

```html
<details class="nb-acc"><summary>Is this too loud?</summary><p>No. The inbox is louder.</p></details>
```
```css
.nb-acc { background: #FFF9E6; border: 3px solid #0A0A0A; border-radius: 6px; box-shadow: 4px 4px 0 #0A0A0A; margin-bottom: 16px; }
.nb-acc summary { font-family: "Archivo Black", sans-serif; padding: 16px 20px; cursor: pointer; list-style: none; }
.nb-acc summary::after { content: "+"; float: right; font-size: 1.4rem; }
.nb-acc[open] summary::after { content: "\2013"; }
.nb-acc p { padding: 0 20px 18px; margin: 0; font-weight: 500; }
```

## Motion

Short, physical, linear: `80ms linear` for press/hover (translate + shadow
change). Marquee: `18s linear infinite`. Nothing else — no eased fades,
no scale-ups, no opacity tricks (opacity fades instantly break the style).

## Do / Don't

- **Do** put a 3–4px black border on every card, button, input, and badge —
  the border is the primary styling device.
- **Don't** use a single blurred or translucent shadow anywhere
  (`box-shadow: 0 8px 24px rgba(...)` kills the style on contact).
- **Do** use flat saturated blocks with a cream canvas and max 3–4 block
  colors per page.
- **Don't** add any gradient, mesh, or glow — solid fills only, no exceptions.
- **Do** press buttons into their own shadow on `:active`
  (`translate(4px,4px)` + `box-shadow: 0 0 0`).
- **Don't** use 1px hairlines, gray borders, or light-weight body fonts —
  everything must read at a glance.
- **Do** keep blocks axis-aligned on a strict grid; reserve rotation for
  stickers and stamps only.
- **Don't** let decoration become rainbow soup — one yellow, one or two
  accents, that's the whole party.

## Copy voice

Loud, direct, allergic to corporate hedging. Short sentences. Verbs that
shove. Exclamation marks are load-bearing.

- "YOUR INBOX CALLED. IT WANTS YOUR ATTENTION BACK."
- "Send the email. Take the credit. We handle the boring parts."
- "Free to start. Loud forever. Cancel whenever — we won't cry (much)."
