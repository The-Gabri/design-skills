---
name: figma
description: Recreate Figma's brand language — playful, colorful, vector-first marketing with black-and-white chrome, bold color blocks, named multiplayer cursors, and tight grotesque type. Use for collaborative product landing pages that feel fun and design-nerdy.
---

# Figma

Figma's brand is a party trick: a strictly black-and-white interface layer, and
color reserved for the five logo shapes and big saturated blocks. It reads as
playful without being childish, technical without being dry — the visual
language of "we made this together," drawn with vector shapes.

## Principles

1. **Chrome is monochrome, joy is chromatic.** On figma.com the interface
   layer — nav, body text, buttons — is strictly black on white. Saturated
   color appears only in product visuals, color-block sections, and the five
   logo shapes. Color is always a decision, never wallpaper.
2. **Vector-first and playful.** Marketing illustration is flat, geometric,
   drawn-like-a-shape-tool art: the five "cube" colors as abstract playful
   forms, dashed selection outlines, Config-era boldness. It should look like
   it was made *in* Figma.
3. **Collaboration is the headline.** Multiplayer cursors with people's names
   are the brand's most distinctive motif — the visual proof of designing
   together. Name your cursors; they are characters, not chrome.
4. **Confident grotesque type.** Huge, tight, negatively tracked headlines in
   a grotesque (Whyte / the custom figmaSans) carry the message. Body copy is
   short, and hierarchy comes from weight, not gray.
5. **Rhythm through alternation.** White canvas sections alternate with
   full-bleed saturated color blocks, paced so at most one loud color block
   sits in the viewport at a time. White space is the separator, not hairlines.
6. **Design-nerd warmth.** Copy speaks the tribe's language — cursors, frames,
   components, Dev Mode — with friendly confidence and zero gatekeeping.

## Color

The five logo shapes (documented on figma.com/brand):

| Token | Hex | Role | Confidence |
|---|---|---|---|
| `shape-red` | `#F24E1E` | Logo shape, brand accents, collaborator color | ✅ |
| `shape-orange` | `#FF7262` | Logo shape, brand accents, collaborator color | ✅ |
| `shape-purple` | `#A259FF` | Logo shape, brand accents, collaborator color | ✅ |
| `shape-blue` | `#1ABCFE` | Logo shape, brand accents, collaborator color | ✅ |
| `shape-green` | `#0ACF83` | Logo shape, brand accents, collaborator color | ✅ |
| `action-blue` | `#0D99FF` | Product CTA color (Figma's editor blue) — not the shape blue | ✅ |
| `blurple` | `#5551FF` | FigJam / Slides / plan-upgrade accents | ✅ |
| `ink` | `#000000` | All text, all solid buttons, borders — the only "color" of the chrome | 🟡 |
| `canvas` | `#FFFFFF` | Page background, white buttons, text on dark surfaces | 🟡 |
| `dark-canvas` | `#1E1E1E` | Dark editor canvas / dark sections | 🟡 |

Rules that make the palette read as Figma:

- **The five shapes are brand accents, never primary CTAs.** Assign them to
  cursors, avatars, illustrations, and color blocks.
- **Color-block sections use one solid brand color** (green, orange, purple,
  blue — or black) with black or white type on top. No shadows, no borders on
  color blocks; the color is the depth device.
- **No mid-gray text.** Body hierarchy comes from type weight, never from
  gray or reduced opacity.

## Typography

- **Headlines:** Whyte (Dinamo) 🟡 — Figma's marketing grotesque; the current
  figma.com ships a custom variable font, `figmaSans`, in its place. Closest
  free substitutes: **Space Grotesk** (display — closest to Whyte's quirks) or
  **Inter** (the product's own workhorse UI typeface).
- **Labels / taxonomy:** a monospace — `figmaMono`, or SF Mono / JetBrains
  Mono — for **uppercase technical labels with wide letter-spacing**, never
  for body copy 🟡.
- **Scale:** display-xl headlines run ~86px desktop, collapsing to ~48px on
  mobile 🟡. Body 16–18px. Everything set with **negative letter-spacing**
  (`-0.02em` on headlines, `-0.01em` to `-0.02em` even on body) and tight
  line-height on headlines (`1.05–1.1`).
- **Weight is the hierarchy.** Bold headline → regular body, both near-black.
  Never gray out secondary text.

```css
font-family: 'Space Grotesk', 'Inter', system-ui, sans-serif;
h1 { font-size: clamp(3rem, 8vw, 5.5rem); font-weight: 700;
     letter-spacing: -0.03em; line-height: 1.02; }
.eyebrow { font-family: ui-monospace, 'SF Mono', monospace;
           text-transform: uppercase; letter-spacing: 0.14em; font-size: 12px; }
```

## Layout & spacing

- **Grid:** max content width 1280px, gutters expanding beyond; sections
  alternate white canvas with full-bleed color blocks 🟡.
- **Radius:** pill (`border-radius: 50px`) CTAs and circular (`50%`) icon
  buttons are the brand signature — never square buttons 🟡. Cards ~12–16px.
- **Borders:** 1px black hairlines on white surfaces; none on color blocks.
- **Dashed outlines** echo the editor's selection handles — use `2px dashed`
  for decorative frames and focus rings 🟡.
- **Shadows:** none on color-block sections; soft small shadows only on white
  cards.
- **Tap targets:** pill CTAs keep 44px minimum height across viewports 🟡;
  mobile CTAs may go full-width.

## Components

### 1. Five-shape motif (SVG)

The logo's five shapes as a decorative cluster — circle, rounded rects, and
the signature "wrench-ish" green wedge, in the five brand colors.

```html
<svg viewBox="0 0 160 60" width="160" height="60" aria-hidden="true">
  <rect x="4"  y="4"  width="24" height="24" rx="12" fill="#F24E1E"/>
  <rect x="32" y="4"  width="24" height="24" rx="12" fill="#FF7262"/>
  <rect x="60" y="4"  width="24" height="52" rx="12" fill="#A259FF"/>
  <rect x="88" y="4"  width="24" height="24" rx="12" fill="#1ABCFE"/>
  <path d="M116 4h12a12 12 0 0 1 12 12v12a12 12 0 0 1-12 12h-12a12 12 0 0 1-12-12V16a12 12 0 0 1 12-12z" fill="#0ACF83"/>
</svg>
```

### 2. Black + white button pair

The brand's signature CTA pattern: solid black pill + white pill with black
border, used together when a section needs both a primary and secondary action.

```html
<a class="btn btn-black" href="#">Get started</a>
<a class="btn btn-white" href="#">Watch the film</a>

<style>
.btn { display: inline-block; border-radius: 50px; padding: 14px 32px;
       font-weight: 600; letter-spacing: -0.01em; min-height: 44px; }
.btn-black { background: #000; color: #fff; }
.btn-white { background: #fff; color: #000; border: 1px solid #000; }
.btn-black:hover { background: #222; }
.btn-white:hover { background: #f4f4f4; }
</style>
```

### 3. Multiplayer cursors

Named cursor chips drifting over a mock canvas — the collaboration signature.
Give each a brand shape color and a person's name.

```html
<div class="cursor-chip" style="--c:#A259FF">
  <svg width="18" height="18" viewBox="0 0 18 18"><path d="M3 2l12 6-7 2-3 7z" fill="var(--c)" stroke="#000" stroke-width="1.5"/></svg>
  <span>Ana</span>
</div>

<style>
.cursor-chip { display: inline-flex; align-items: center; gap: 6px;
  background: var(--c); color: #fff; font-weight: 600; font-size: 13px;
  padding: 5px 10px; border-radius: 20px; border: 1.5px solid #000; }
</style>
```

### 4. Color-block hero

Full-bleed solid brand color, giant tight headline in black or white, and the
black + white button pair. One loud block per viewport.

```html
<section style="background:#0ACF83; color:#000; padding:96px 24px; text-align:center;">
  <h1 style="font-size:clamp(3rem,8vw,5.5rem); letter-spacing:-0.03em; line-height:1.02;">
    Design together,<br>ship faster.
  </h1>
  <p>One canvas. Everyone invited.</p>
  <a class="btn btn-black" href="#">Get started for free</a>
  <a class="btn btn-white" href="#">See what's new</a>
</section>
```

### 5. Feature cards with playful illustration

White cards, each topped with a flat vector illustration block in brand
colors — geometric, shape-tool-looking — then a bold headline and one-liner.

```html
<div class="feat-card">
  <svg viewBox="0 0 120 72" aria-hidden="true"> <!-- flat vector doodle -->
    <rect x="8" y="8" width="40" height="40" rx="8" fill="#1ABCFE"/>
    <circle cx="84" cy="36" r="20" fill="#FF7262"/>
    <rect x="40" y="40" width="40" height="12" rx="6" fill="#A259FF"/>
  </svg>
  <h3>Multiplayer editing</h3>
  <p>Everyone's cursor on one canvas. No "final_v2_FINAL" ever again.</p>
</div>
```

### 6. Testimonial quote card

Oversized quote in the grotesque, author chip with a brand-color initial
avatar.

```html
<blockquote class="t-card" style="background:#FF7262; color:#000;">
  <p>"We killed the handoff deck. Designers and engineers live in the same file now."</p>
  <footer><span class="avatar" style="background:#A259FF">M</span>
    Maya Chen — Design Lead, Paperplane</footer>
</blockquote>
```

### 7. Pricing with pill tab toggle

Three tiers (Starter free / Professional / Organization); a pill tab group
toggles monthly vs yearly, with "selected = black fill" as the brand pattern.

```html
<div class="tabs" role="tablist">
  <button class="tab selected" role="tab" aria-selected="true">Monthly</button>
  <button class="tab" role="tab" aria-selected="false">Yearly</button>
</div>
<style>
.tabs { display:inline-flex; border:1px solid #000; border-radius:50px; padding:4px; }
.tab { border:0; background:none; border-radius:50px; padding:10px 24px; font-weight:600; }
.tab.selected { background:#000; color:#fff; }
</style>
```

### 8. Mono eyebrow label

Uppercase wide-tracked mono kicker above section headlines — the taxonomy
voice of the brand.

```html
<p class="eyebrow">Config 2026 · What's new</p>
```

### 9. Color-block CTA

A final loud block — black or brand color — with a short punchy headline and
a white pill CTA. One line of copy, one button.

```html
<section style="background:#000; color:#fff; padding:96px 24px; text-align:center;">
  <h2 style="font-size:clamp(2.5rem,6vw,4rem); letter-spacing:-0.03em;">Your next file is a team sport.</h2>
  <a class="btn" style="background:#fff; color:#000;" href="#">Start designing free</a>
</section>
```

### 10. Marquee ribbon

A ticker strip of design-nerd terms separated by the five shapes — pure
Config energy.

```html
<div class="marquee" style="background:#1ABCFE; color:#000; overflow:hidden;">
  <div class="track">AUTO LAYOUT ✳ MULTIPLAYER ✳ DEV MODE ✳ VARIABLES ✳ PROTOTYPING ✳ </div>
</div>
```

## Motion

Figma's marketing has no heavy motion language — keep it light: 150–250ms
`ease-out` hovers, looping marquee ribbons, and gently drifting multiplayer
cursors. Playful, never physics-showy.

## Do / Don't

- **Do** pair a black pill CTA with a white pill CTA; **don't** make CTAs in
  brand colors — the five shapes are accents, not buttons.
- **Do** keep nav, text, and chrome black-on-white; **don't** tint the
  interface chrome with brand colors.
- **Do** use named cursors with brand colors to signal collaboration;
  **don't** scatter anonymous cursors as decoration.
- **Do** alternate white sections with one full-bleed color block at a time;
  **don't** stack two loud blocks back-to-back — white canvas must separate
  them.
- **Do** write hierarchy with weight (bold → regular); **don't** use mid-gray
  body text or reduced-opacity labels.
- **Do** round CTAs to pills and icon buttons to circles; **don't** square off
  buttons.
- **Do** reserve the mono uppercase style for labels and kickers; **don't**
  set body copy in monospace.
- **Do** use dashed outlines to echo selection handles; **don't** add drop
  shadows to color-block sections.

## Copy voice (for brand styles)

Friendly, confident, design-nerdy. Second person, short sentences, insider
vocabulary (cursors, frames, components, Dev Mode) with zero gatekeeping.
Exclamation-free enthusiasm — the product is the excitement.

- "Design, prototype, and ship — all in one file, with everyone you know."
- "Your cursor is never alone."
- "Auto layout handled it."

Sources: figma.com/brand (five logo colors #F24E1E #FF7262 #A259FF #1ABCFE
#0ACF83); documented brand teardowns of figma.com — monochrome chrome with
color only in product content and color blocks, custom variable figmaSans with
negative letter-spacing, figmaMono uppercase labels, 50px pill / 50% circular
button geometry, 1280px max content width, "selected = black fill" pricing
tabs, dashed selection-handle motifs, #0D99FF editor action blue, #5551FF
blurple for FigJam, #1E1E1E dark canvas. Whyte (Dinamo) as marketing grotesque
per typeface analyses; Space Grotesk / Inter recommended as free substitutes.
