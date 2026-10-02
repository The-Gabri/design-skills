---
name: memphis
description: Memphis Group postmodern pattern style — clashing pastels and neons, terrazzo and Bacterio squiggle patterns, playful geometric chaos. Use for party pages, creative brands, and anything that should feel joyfully loud.
---

# Memphis

The look of the Memphis Group (Memphis Milano, Ettore Sottsass, Milan, 1980–1987):
a postmodern rebellion against beige modernism that replaced "form follows
function" with emotion, kitsch, and deliberate visual noise. Furniture became
totems of plastic laminate printed with dense black squiggles; surfaces turned
into confetti fields of terrazzo chips, zigzags, and triangles in clashing
pastels and neons. On the web it reads as joyful maximalism — pattern is never
a texture under content, it IS the content.

## Principles

1. **Form follows fun.** Memphis openly rejected functionalism ("anti-functionalism"
   is the movement's documented core). A page should entertain first and behave
   second — decoration is a feature, not a crime.
2. **Pattern is the content.** Surfaces carry meaning: Bacterio's black
   squiggles (Sottsass, 1978, printed on Abet Laminati), terrazzo chip fields,
   geometric confetti. Never use a flat muted background where a printed
   pattern could be.
3. **Clash on purpose.** Pastels against neons, coral against mint, black
   against everything. Clashes must look intentional and saturated — a
   timid palette is the only real failure.
4. **Asymmetry is the grid.** Elements tilt (−3° to +3°), float, overlap, and
   refuse to line up. Centered, symmetrical layouts are the opposite of
   Memphis; compose like a collage, not a spreadsheet.
5. **Cheap materials, luxury attitude.** Memphis printed "distasteful" plastic
   laminate onto designer furniture to dismantle the material hierarchy. On the
   web: humble elements (borders, solid fills, hard shadows) used with total
   confidence beat expensive-looking glass and gradients.
6. **Kitsch between elegance.** The documented line: Memphis exists "between
   kitsch and elegance." Keep one foot in play (squiggles, sticker badges) and
   one in craft (crisp geometry, deliberate rhythm) — pure chaos tips into mess.

## Color

There is no official brand palette — Memphis was a furniture collective, not a
design system. The colors below are reconstructed from period photography and
the group's documented laminate/print vocabulary (coral reds, mints, mustards,
sky blues, black squiggles on white).

| Token | Hex | Role | Legend |
|---|---|---|---|
| Paper | `#FAF3E7` | Warm cream canvas, never pure white | ⚠️ |
| Ink | `#141414` | Black for squiggles, borders, text | ⚠️ |
| Bacterio black | `#111111` | Squiggle pattern ink (black squiggles documented) | ✅ |
| Coral | `#FF5A5A` | Primary loud accent | ⚠️ |
| Hot pink | `#F22E8A` | Neon clash accent | ⚠️ |
| Mustard | `#FFC62E` | Warm pop, stickers, chips | ⚠️ |
| Mint | `#6FDDB8` | Cool clash against coral | ⚠️ |
| Sky | `#4FA9E8` | Confetti blue | ⚠️ |
| Lilac | `#B08FE8` | Soft clash, chip fields | ⚠️ |
| Lime | `#C7E548` | Neon spark | ⚠️ |

Rules: pick 4–6 colors and let them collide in flat shapes — never blend them
into gradients (purple-blue gradients are the signature slop of every other
style; Memphis color sits in hard-edged shapes). Black 3px outlines and cream
paper hold the chaos together. ✅ = documented motif/fact; ⚠️ = reconstructed
from period sources, not official tokens.

## Typography

- **Display:** ultra-bold, playful, slightly wobbly. Closest free faces:
  **Shrikhand** (retro-curvy, the closest to Memphis's cartoon confidence),
  **Archivo Black**, **Titan One** (🟡 substitutes — Memphis had no house font).
- **Contrast voice:** pair the fat display face with a sharp grotesque for
  body: **Space Grotesk** or **Archivo** (🟡). One deliberate italic serif
  accent (e.g. Georgia italic) is allowed for kitsch quotes.
- **Memphis typographic moves:** mixed sizes in one headline (one word huge,
  one tiny), words rotated −2°, kicker labels in uppercase tracked-out
  small caps with black pill backgrounds, exclamation marks doing real work.
- **Scale:** display 56–120px, tight leading (0.95–1.0); body 16–18px with
  generous line-height (1.6) so the loud type stays readable.

## Layout & spacing

- **Pattern fields:** sections sit on full-bleed SVG patterns (terrazzo chips,
  squiggles, confetti) via inline `<pattern>` defs — never plain fills.
- **The collage grid:** 12-column grid is fine, but break it constantly —
  cards rotated ±2°, overlapping edges, elements hanging off section borders.
- **Borders & shadows:** 3px solid black borders; hard offset shadows
  (`box-shadow: 6px 6px 0 #141414`), zero blur. Radii are either 0 or full
  pill — nothing in between.
- **Spacing:** 8px base; section padding 64–96px; but let shapes bleed — a
  squiggle band can ignore padding entirely and run edge to edge.
- **Dividers:** squiggle/zigzag SVG bands between sections, not hairlines.

## Components

Base context: `body{background:#FAF3E7;color:#141414;font-family:'Space Grotesk',system-ui,sans-serif}`

**1. Bacterio squiggle band (the signature motif)**

Black squiggles on a colored band — documented Memphis print (Abet Laminati, ✅).

```html
<svg width="100%" height="72" aria-hidden="true">
  <defs>
    <pattern id="bacterio" width="120" height="36" patternUnits="userSpaceOnUse">
      <path d="M4 18 q6 -12 12 0 t12 0 t12 0" fill="none" stroke="#111" stroke-width="4" stroke-linecap="round"/>
      <path d="M30 8 q6 -8 12 0 t12 0" fill="none" stroke="#111" stroke-width="3" stroke-linecap="round"/>
      <path d="M70 28 q6 -10 12 0 t12 0" fill="none" stroke="#111" stroke-width="4" stroke-linecap="round"/>
    </pattern>
  </defs>
  <rect width="100%" height="72" fill="#FFC62E"/>
  <rect width="100%" height="72" fill="url(#bacterio)"/>
</svg>
```

**2. Terrazzo chip field (section background)**

```html
<svg width="100%" height="320" aria-hidden="true">
  <defs>
    <pattern id="terrazzo" width="140" height="140" patternUnits="userSpaceOnUse">
      <polygon points="20,14 34,30 18,36" fill="#FF5A5A"/>
      <polygon points="80,60 96,52 100,74 84,80" fill="#6FDDB8"/>
      <circle cx="52" cy="96" r="10" fill="#4FA9E8"/>
      <rect x="104" y="104" width="22" height="14" fill="#F22E8A" transform="rotate(24 115 111)"/>
      <polygon points="60,30 70,44 56,48" fill="#FFC62E"/>
      <circle cx="116" cy="24" r="7" fill="#B08FE8"/>
    </pattern>
  </defs>
  <rect width="100%" height="320" fill="#FAF3E7"/>
  <rect width="100%" height="320" fill="url(#terrazzo)"/>
</svg>
```

**3. Confetti card (tilted, hard shadow)**

```html
<article class="mem-card">
  <h3>Loud by design</h3>
  <p>Three clashing colors, one black border, zero apologies.</p>
</article>
<style>
.mem-card{background:#fff;border:3px solid #141414;border-radius:0;
  box-shadow:8px 8px 0 #141414;padding:24px;max-width:320px;
  transform:rotate(-2deg);position:relative}
.mem-card::before{content:"";position:absolute;top:-14px;right:-14px;
  width:44px;height:44px;background:#F22E8A;border:3px solid #141414;
  border-radius:50%}
.mem-card h3{font-family:Shrikhand,system-ui,sans-serif;font-size:28px;margin:0 0 8px}
.mem-card p{margin:0;line-height:1.6}
</style>
```

**4. Chunky tilted button**

```html
<a class="mem-btn" href="#">Get loud</a>
<style>
.mem-btn{display:inline-block;background:#FF5A5A;color:#141414;
  font:700 18px/1 'Space Grotesk',system-ui,sans-serif;text-transform:uppercase;
  letter-spacing:1px;text-decoration:none;padding:16px 32px;
  border:3px solid #141414;border-radius:999px;
  box-shadow:5px 5px 0 #141414;transform:rotate(-2deg);
  transition:transform .12s steps(2),box-shadow .12s steps(2)}
.mem-btn:hover{transform:rotate(1deg) translate(-2px,-2px);box-shadow:7px 7px 0 #141414}
.mem-btn:active{transform:translate(3px,3px);box-shadow:2px 2px 0 #141414}
</style>
```

**5. Sticker badge (rotated seal)**

```html
<span class="mem-sticker">100%<br>kitsch</span>
<style>
.mem-sticker{display:inline-flex;align-items:center;justify-content:center;
  width:110px;height:110px;background:#FFC62E;border:3px solid #141414;
  border-radius:50%;transform:rotate(12deg);text-align:center;
  font:700 15px/1.25 'Space Grotesk',system-ui,sans-serif;text-transform:uppercase}
</style>
```

**6. Marquee ticker**

```html
<div class="mem-ticker"><div class="mem-ticker-track">
  <span>No beige ★ Dress loud ★ Squiggles encouraged ★&nbsp;</span>
  <span>No beige ★ Dress loud ★ Squiggles encouraged ★&nbsp;</span>
</div></div>
<style>
.mem-ticker{background:#141414;color:#FAF3E7;overflow:hidden;white-space:nowrap;
  border-top:3px solid #141414;border-bottom:3px solid #141414;padding:10px 0;
  font:700 16px 'Space Grotesk',sans-serif;text-transform:uppercase;letter-spacing:2px}
.mem-ticker-track{display:inline-block;animation:mem-scroll 18s linear infinite}
@keyframes mem-scroll{to{transform:translateX(-50%)}}
</style>
```

**7. Ticket stub card**

```html
<div class="mem-ticket">
  <div><strong>General chaos</strong><span>$25 · door $35</span></div>
  <a class="mem-btn" href="#">Grab one</a>
</div>
<style>
.mem-ticket{display:flex;justify-content:space-between;align-items:center;gap:16px;
  background:#6FDDB8;border:3px dashed #141414;padding:20px 24px;
  transform:rotate(1.5deg);box-shadow:6px 6px 0 #141414;max-width:520px}
.mem-ticket strong{display:block;font-size:22px;text-transform:uppercase}
.mem-ticket span{font-size:15px}
</style>
```

**8. Confetti bullet list**

```html
<ul class="mem-list">
  <li>Squiggle-print dress code</li>
  <li>Terrazzo dance floor</li>
</ul>
<style>
.mem-list{list-style:none;padding:0;display:grid;gap:12px}
.mem-list li{position:relative;padding-left:34px;font-weight:600;font-size:17px}
.mem-list li::before{content:"";position:absolute;left:0;top:4px;width:18px;height:18px;
  background:#4FA9E8;border:3px solid #141414;transform:rotate(45deg)}
.mem-list li:nth-child(2n)::before{background:#FFC62E;border-radius:50%;transform:none}
.mem-list li:nth-child(3n)::before{background:#F22E8A;transform:rotate(-12deg)}
</style>
```

**9. Squiggle divider**

```html
<svg class="mem-zig" viewBox="0 0 1200 40" preserveAspectRatio="none" aria-hidden="true">
  <path d="M0 20 L30 4 L60 36 L90 4 L120 36 L150 4 L180 36 L210 4 L240 36 L270 4 L300 36 L330 4 L360 36 L390 4 L420 36 L450 4 L480 36 L510 4 L540 36 L570 4 L600 36 L630 4 L660 36 L690 4 L720 36 L750 4 L780 36 L810 4 L840 36 L870 4 L900 36 L930 4 L960 36 L990 4 L1020 36 L1050 4 L1080 36 L1110 4 L1140 36 L1170 4 L1200 20"
    fill="none" stroke="#141414" stroke-width="6"/>
</svg>
<style>.mem-zig{display:block;width:100%;height:36px}</style>
```

**10. Memphis footer strip**

Black bar, squiggle band on top, mixed-size type, loud sign-off — see demo.

## Motion

No motion language was ever defined — Memphis is furniture. On the web: keep
it playful and mechanical, never silky. Signature moves: `steps(2)` wobbles on
hover, 120–200ms pops, infinite marquee tickers, cards that straighten from
−2° to 0° on hover, confetti that drifts on a loop. No long fades, no
smooth `ease-in-out` choreography — bounce like plastic, don't glide like silk.

## Do / Don't

- **Do** let two patterns touch edge to edge (terrazzo card on a squiggle band).
  **Don't** blend colors into gradients or soft vignettes.
- **Do** tilt cards ±2° and overlap elements for collage energy.
  **Don't** center everything symmetrically with generous white space.
- **Do** clash coral against mint, mustard against hot pink.
  **Don't** pair colors timidly — beige, gray, and "tasteful neutrals" are banned.
- **Do** use 3px black borders with hard offset shadows (`6px 6px 0`, zero blur).
  **Don't** use blurred drop shadows or thin 1px hairlines.
- **Do** mix one fat display face with a sharp grotesque.
  **Don't** set everything in one neutral sans at one weight.
- **Do** decorate empty space with confetti, chips, and squiggles.
  **Don't** leave flat empty panels "for breathing room" — Memphis doesn't breathe, it shouts.

## Copy voice

Memphis copy is irreverent, anti-snob, and proud of it — a Milanese art prank
that got famous. Short declarative sentences, exclamation marks, mock-manifestos.

- "Minimalism is a rumor. Party starts at 9."
- "Dress code: louder than the carpet."
- "No beige. Ever."
