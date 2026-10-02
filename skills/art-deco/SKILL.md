---
name: art-deco
description: Art Deco — 1920s geometric glamour. Use for luxury hospitality, jazz clubs, galas, cocktail brands, and Gatsby-era marketing: gold on black, sunbursts, chevrons, stepped frames, tall elegant capitals.
---

# Art Deco

The look of the 1920s–30s Style Moderne: geometric ornament, strict
symmetry, and gold on black. Born after the *Exposition Internationale
des Arts Décoratifs* (Paris, 1925); built by the Chrysler Building
(William Van Alen, 1930), the ocean-liner posters of A. M. Cassandre,
and the skyscraper setbacks of 1916 New York zoning. Everything
ceremonial — the frame is the architecture, not an afterthought.

## Principles

1. **Axial symmetry is the governing law.** Every composition pivots on
   a strong central vertical axis, mirrored left and right, like a
   temple facade or the prow of an ocean liner seen head-on.
   Asymmetry reads as a mistake here.
2. **Ornament from pure geometry.** Decoration is never organic: only
   sunbursts, fans, chevrons, zigzags, fluting (parallel hairlines),
   and stepped "ziggurat" forms. Repeat them rhythmically like a
   frieze.
3. **Luxury materials, even in pixels.** Gold, lacquer, ivory, onyx.
   Ornament should feel metallic — thin gold hairlines on deep black —
   not flat. Gold gradients are rendered as flat brass + highlights,
   never purple-blue washes.
4. **Verticality and upward motion.** Forms rise and narrow: stepped
   crowns, rays ascending, tall capitals. The eye should travel up,
   toward the penthouse.
5. **Ceremony over convenience.** Borders enclose content like a proscenium
   frames a stage. Generous padding, double rules, corner crests — the
   page stages its content; it never just lists it.

## Color

Gold on black, ivory for text, one jewel tone at most.

| Token | Hex | Role | Legend |
|---|---|---|---|
| Onyx | `#0D0C0A` | Deep black ground | 🟡 |
| Lacquer | `#171310` | Raised surface, cards | ⚠️ |
| Ivory | `#F2EAD8` | Primary text on black | 🟡 |
| Champagne Gold | `#D4AF37` | Accent, ornament, rules | ✅ |
| Antique Brass | `#A98F4E` | Muted gold: borders, secondary lines | 🟡 |
| Faded Gold | `#5C4B22` | Deep border / inset shadow tone | ⚠️ |
| Emerald | `#0F4C3F` | Jewel tone — use once, for select panels | 🟡 |
| Wine | `#5E1F24` | Alternate jewel tone, never with emerald | ⚠️ |

Legend: ✅ documented in design-history sources (V&A, Wikipedia,
Britannica) · 🟡 cross-referenced across Deco analyses · ⚠️ community
approximation of my own tokens.

Contrast note: `#D4AF37` on `#0D0C0A` passes for large text and
graphics; body copy stays ivory-on-onyx at AA.

## Typography

Deco lettering is **upright, capitals-only, geometric, high-contrast** —
monument inscriptions and theater marquees. Cassandre used capitals
exclusively in his posters, believing them more legible at scale; the
Broadway face (Morris Fuller Benton, ATF, 1927/28 — ✅ documented) was
designed as a capitals-only display face with bold geometric lettering
and extreme thick/thin contrast.

- **Display:** `Cinzel` (✅ Google Font) or `Marcellus` — tall
  Roman-inspired capitals; the closest free substitutes for Deco
  display type. Cinzel for headlines, Marcellus for subheads. Both ⚠️
  as *period* accuracy goes: period faces were Broadway, Bifur (1929)
  and Peignot (1937). Never render headlines lowercase.
- **Tracking:** generous — `0.18em`–`0.35em` for small caps labels;
  `0.05em`–`0.12em` for large display.
- **Body:** a quiet serif for readability — `Cormorant Garamond` or
  `EB Garamond` at 15–17px, line-height 1.7. Ivory, not pure white.
- **Scale:** display jumps in big steps (e.g. 14 / 24 / 40 / 64 / 96px);
  nothing shouts mid-volume. Labels go small-caps with double letter
  spacing — the "brass plaque" effect.

## Layout & spacing

- **Centered axial layouts.** The symmetry axis is the composition;
  content columns mirror. Two-column layouts must balance visually
  left/right.
- **The panel is the unit:** content lives inside gold hairline frames
  (1–2px), often double-ruled (outer 2px `#A98F4E`, inner 1px
  `#5C4B22`, 4–6px gap). Corners may be stepped or carry a small
  chevron crest.
- **Rhythm of ornament:** chevron bands and fluted strips as section
  separators; sunburst as the single hero emblem. One sunburst per
  page — repetition dilutes it.
- **Spacing scale (8px base):** 16 · 24 · 40 · 64 · 96 · 160px. Sections
  separate with ceremony (64–96px); panel padding generous (32–48px).
- **Radii:** `0` to `2px` max. Deco corners are square or stepped —
  never pill, never glassy round. Stepped corners use `clip-path`.
- **No drop shadows.** Depth comes from inset hairlines and gold
  layering, not blur. If a shadow exists at all, it is a hard 1px
  brass offset — an engraving, not a float.

## Components

Copy-pasteable HTML/CSS. Base context: `body { background:#0D0C0A;
color:#F2EAD8; font-family:'Cormorant Garamond',Georgia,serif; }`,
display face `'Cinzel','Times New Roman',serif`.

**1. Sunburst emblem (the signature ornament, inline SVG)**

```html
<svg class="deco-sun" viewBox="0 0 200 200" width="200" height="200" aria-hidden="true">
  <g stroke="#D4AF37" stroke-width="2">
    <!-- generate rays in JS, or hardcode ~15 lines fanning 300°→60° upward -->
    <circle cx="100" cy="150" r="18" fill="none"/>
    <circle cx="100" cy="150" r="10" fill="#D4AF37"/>
    <path d="M70 150 h-40 M130 150 h40" />
  </g>
</svg>
<style>
.deco-sun{display:block;margin:0 auto}
</style>
```

Ray math (JS one-liner to fan rays upward from a hub): for
`a` in `[-75..-105°]`… simpler: emit 15 lines from `(100,150)` at
angles `200°..340°` excluding the bottom, length `90`. Fans read
"sunrise"; keep rays within the upper hemisphere.

**2. Gold-rule divider with center diamond**

```html
<div class="deco-divider" aria-hidden="true"><span></span><i></i><span></span></div>
<style>
.deco-divider{display:flex;align-items:center;gap:14px;max-width:560px;margin:40px auto}
.deco-divider span{flex:1;height:1px;background:linear-gradient(90deg,transparent,#A98F4E,transparent)}
.deco-divider i{width:9px;height:9px;background:#0D0C0A;border:2px solid #D4AF37;transform:rotate(45deg)}
</style>
```

**3. Double-ruled panel (frames hold content with ceremony)**

```html
<div class="deco-panel"><h3>Evening Program</h3><p>Dinner at eight. Dancing till two.</p></div>
<style>
.deco-panel{position:relative;border:2px solid #A98F4E;padding:36px 40px;background:#171310}
.deco-panel::before{content:"";position:absolute;inset:7px;border:1px solid #5C4B22;pointer-events:none}
.deco-panel h3{font-family:Cinzel,serif;letter-spacing:.28em;text-align:center;color:#D4AF37;margin:0 0 12px}
.deco-panel p{text-align:center;margin:0}
</style>
```

**4. Stepped (ziggurat) card crown**

```html
<div class="deco-step"><h3>The Chrysler Corner</h3></div>
<style>
.deco-step{background:#171310;border:1px solid #A98F4E;padding:28px;position:relative;
  clip-path:polygon(0 0,calc(100% - 24px) 0,100% 24px,100% 100%,0 100%,0 0)}
.deco-step::after{content:"";position:absolute;top:10px;right:10px;width:14px;height:14px;
  border-top:2px solid #D4AF37;border-right:2px solid #D4AF37}
.deco-step h3{font-family:Cinzel,serif;letter-spacing:.2em;color:#F2EAD8;margin:0}
</style>
```

**5. Monogram badge (circular crest)**

```html
<div class="deco-mono">M</div>
<style>
.deco-mono{width:72px;height:72px;border-radius:50%;border:2px solid #D4AF37;color:#D4AF37;
  display:flex;align-items:center;justify-content:center;font-family:Cinzel,serif;font-size:30px;
  box-shadow:inset 0 0 0 5px #0D0C0A,inset 0 0 0 6px #5C4B22;background:radial-gradient(circle,#1d1712 55%,#0D0C0A)}
</style>
```

**6. Primary button — gold on black**

```html
<a class="deco-btn" href="#">Reserve a Table</a>
<style>
.deco-btn{display:inline-block;font-family:Cinzel,serif;font-size:13px;letter-spacing:.3em;
  text-transform:uppercase;color:#0D0C0A;background:#D4AF37;padding:16px 38px 14px;
  text-decoration:none;border:1px solid #A98F4E;transition:all .35s ease}
.deco-btn:hover{background:#0D0C0A;color:#D4AF37;box-shadow:inset 0 0 0 1px #D4AF37}
</style>
```

**7. Chevron band (CSS-only frieze)**

```html
<div class="deco-chevron" aria-hidden="true"></div>
<style>
.deco-chevron{height:14px;
  background:repeating-linear-gradient(135deg,#A98F4E 0 2px,transparent 2px 12px),
             repeating-linear-gradient(45deg,#A98F4E 0 2px,transparent 2px 12px)}
</style>
```

**8. Fluted strip (parallel gold hairlines)**

```html
<div class="deco-flute" aria-hidden="true"></div>
<style>
.deco-flute{height:28px;background:repeating-linear-gradient(90deg,#5C4B22 0 1px,transparent 1px 14px)}
</style>
```

**9. Marquee marquee strip (ticket band)**

```html
<div class="deco-ticket"><span>Tonight</span><b>Paul Whiteman &amp; His Orchestra</b><span>9 O'Clock Sharp</span></div>
<style>
.deco-ticket{display:flex;justify-content:space-between;align-items:center;gap:16px;
  border-top:1px solid #A98F4E;border-bottom:1px solid #A98F4E;padding:14px 24px;
  font-family:Cinzel,serif;letter-spacing:.18em;font-size:12px;color:#F2EAD8}
.deco-ticket b{color:#D4AF37;font-size:14px}
.deco-ticket span{color:#A98F4E}
</style>
```

**10. Corner-crested frame**

```html
<div class="deco-frame"><p>Champagne is served from six.</p></div>
<style>
.deco-frame{position:relative;padding:30px;border:1px solid #A98F4E}
.deco-frame i{position:absolute;width:22px;height:22px;border-color:#D4AF37;border-style:solid}
.deco-frame i.tl{top:-2px;left:-2px;border-width:3px 0 0 3px}
.deco-frame i.tr{top:-2px;right:-2px;border-width:3px 3px 0 0}
.deco-frame i.bl{bottom:-2px;left:-2px;border-width:0 0 3px 3px}
.deco-frame i.br{bottom:-2px;right:-2px;border-width:0 3px 3px 0}
</style>
```

## Motion

Stately, never playful: 300–500ms `ease-out` on fades and reveals;
1px gold line-draws may grow from center outward (400–700ms). No
bounces, no springs, no parallax playfulness. Ornament enters with
dignity — fade and rise 12px, once. If in doubt, one line: *motion is
ceremonial and slow.*

## Do / Don't

- **Do** anchor every composition on a central vertical axis and mirror
  left/right — **don't** scatter elements in an asymmetric grid.
- **Do** draw ornament as thin gold hairlines (`#D4AF37`/`#A98F4E`)
  on onyx — **don't** use thick neon strokes or glows.
- **Do** keep headlines in spaced capitals (`letter-spacing:.2em+`) —
  **don't** set display type in lowercase or sentence case.
- **Do** use one jewel tone (emerald OR wine), sparingly, against
  black and gold — **don't** mix emerald, wine, and gold into a
  rainbow.
- **Do** frame content with double rules and stepped corners —
  **don't** use rounded pills, glass cards, or soft drop shadows.
- **Do** ration the sunburst: one hero emblem per page — **don't**
  stamp a fan on every card and button.
- **Do** keep body copy a quiet ivory serif — **don't** typeset
  paragraphs in Cinzel (it is a display face, not a reading face).
- **Do** let gold be flat with engraved hairline layering —
  **don't** reach for purple-blue gradients or metallic bevel CSS
  tricks.

## Copy voice

Elegant, grand, ceremonial — announcements from a master of
ceremonies, never slang, never exclamation-point hype. Short
declarative lines with a touch of occasion.

- "An Evening Above the Clouds — Dinner, Dancing, and the Finest
  Orchestra in Town."
- "Table Twelve, Nine O'Clock Sharp. Your Evening Awaits."
- "Champagne is served from six. The orchestra tunes at eight."
