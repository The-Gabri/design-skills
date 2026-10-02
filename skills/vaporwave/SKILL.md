---
name: vaporwave
description: Vaporwave / synthwave retro-futurism — neon grid sunsets, chrome suns, palm silhouettes, VHS glitch. Use for music labels, arcade pages, event flyers, streaming overlays, anything addressing an audience that reads the 80s reference.
---

# Vaporwave / Synthwave Grid

Vaporwave and its earnest sibling synthwave are the visual language of a
retro-future that never happened: the perspective grid receding to a vanishing
point, a striped gradient sun setting on a digital horizon, chrome type,
palm silhouettes, scanlines and VHS tracking errors. Done well it reads as
cinematic and premium — *Drive* by way of *OutRun*. Done badly it reads as a
garish neon clip-art mess. The gap is **restraint**: one sun, one grid, one
sky, with glow rationed to the accents and deep night carrying the contrast.

Know the register you are designing in. The Aesthetics Wiki documents
synthwave as an **earnest celebration** of 1980s pop culture (action films,
arcade games, the night drive) while vaporwave is a **knowing, ironic**
revisit of late-80s/90s consumer culture (malls, Muzak, discarded tech) —
often "hauntological," a little sad. (✅ aesthetics.fandom.com/wiki/Synthwave.)
Wikipedia notes that "outrun" names the driving visual aesthetic of the genre:
magenta neon and gridlines. (✅ en.wikipedia.org/wiki/Vaporwave.) Pick one
register per page — ironic mall-memorial or sincere night-drive — and hold it.

## Principles

1. **One sun, one grid, one sky.** A single striped chrome sun on the horizon,
   a single one-point-perspective grid below it, a single vertical
   magenta-to-indigo sky. Repeating any of them reads as clip-art.
   (🟡 cross-referenced across documented synthwave design refs.)
2. **Loud hero, quiet product.** The grid, the sun, and the palms carry the
   register; the parts people actually use are set in ordinary type on an
   ordinary dark surface, with neon glow reserved for one or two accents.
   (✅ vocab.design term "vaporwave" — the workable interface pattern.)
3. **Glow is rationed, not sprayed.** Neon borders are 1px with a soft halo;
   filled gradients belong to buttons and the sun. Magenta text on cyan is
   unreadable at any size — never set body copy that way.
   (✅ vocab.design — readability is non-negotiable.)
4. **Degradation is period detail.** Scanlines, VHS tracking wobble,
   chromatic-aberration text splits, and full-width Ａ Ｅ Ｓ Ｔ Ｈ Ｅ Ｔ Ｉ Ｃ
   lettering are authentic artifacts of the era, not decoration on top.
   (✅ aesthetics wiki: compression artefacts and tracking errors as vocabulary.)
5. **Deep night, never pure black.** Grounds are near-black shifted toward
   purple (#0D0221 family) so the neon has something to glow *against*;
   the horizon line is the brightest line on the page.
   (🟡 cross-referenced; "never pure black" is community convention.)
6. **Symmetry and depth.** Centered, mirrored compositions; foreground
   silhouettes (palms, mountains) framing the sun; layered planes receding to
   the vanishing point. (🟡 documented synthwave composition.)

## Color

Neon gradients ARE the style here — keep them vaporwave-accurate (hot
pink/purple/cyan sunset on deep night), never generic purple-blue.

| Token | Hex | Role | Legend |
|---|---|---|---|
| `sunset-pink` | `#FF71CE` | hot pink neon — primary accent, sun band, primary buttons | 🟡 cross-referenced (canon neon trio) |
| `violet` | `#B967FF` | purple — secondary accent, sky midtone, card borders | 🟡 cross-referenced (canon neon trio) |
| `neon-cyan` | `#01CDFE` | electric cyan — grid lines, HUD outlines, data accents | 🟡 cross-referenced (canon neon trio) |
| `night` | `#0D0221` | page background — near-black with purple undertone | 🟡 documented retro-futurism refs |
| `deep-ground` | `#1A0033` | surfaces, panels, card grounds | ⚠️ community approximation |
| `sun-yellow` | `#FFD700` | top band of the chrome sun, price/label highlights | 🟡 canonical banded sun (yellow→pink) |
| `laser-orange` | `#FF6B00` | sun mid-band accent, warning/REC accents | 🟡 cross-referenced |
| `chrome-silver` | `#C0C0C0` | chrome type highlights | ⚠️ community approximation |
| `silhouette` | `#08010F` | palms, mountains, foreground cut-outs | ⚠️ community approximation |
| `white` | `#FFFFFF` | body text (with subtle glow) | ✅ document practice |

**Documented combinations** (🟡 cross-referenced synthwave refs):
- **Classic sunset:** hot pink + electric cyan + deep violet ground + chrome-yellow sun — the canonical grid hero.
- **Miami night:** magenta + teal + deep navy, laser-orange accents — neon signs on wet asphalt.
- **Outrun:** hot pink/orange gradient sun + purple sky + cyan grid — the driving-game register.

## Typography

- **Display (hero, signage):** `Orbitron` (Google Fonts, 500–900) for chrome
  lettering and headlines; `Monoton` (Google Fonts, 400 only, ALL CAPS,
  letterspaced) for neon-sign accents — used sparingly, one per page.
  ⚠️ community convention — the accepted free proxies for 80s chrome type.
- **Body/UI:** a quiet neutral grotesk or system stack (`system-ui`), 15–17px,
  regular weight, `#FFFFFF` at 85% opacity. The style's personality lives in
  the display type; body copy must stay legible. ⚠️ community practice.
- **Period accents:** full-width Ａ Ｅ Ｓ Ｔ Ｈ Ｅ Ｔ Ｉ Ｃ unicode lettering
  for kickers; katakana (e.g. ミッドナイト) as marginalia. Use as spice, never
  as body text. (🟡 documented vaporwave vocabulary.)
- **Rules:** display type is always ALL CAPS or Title Case with wide
  letterspacing (`0.15–0.35em`); italic skew (`skewX(-8deg)`) on hero
  lettering nods to the tilted outrun logotype; never set chrome gradient
  text below 24px — it has no measurable contrast. (✅ vocab.design.)

## Layout & spacing

- **Hero-dominant:** full-viewport (100vh) sunset scene — sky (top ~60%),
  horizon line, grid floor (bottom ~40%), sun centered on the horizon,
  silhouettes flanking. Content floats above in layered planes.
  (🟡 documented composition.)
- **The visible grid:** a one-point-perspective cyan wireframe grid occupies
  the lower third, glowing at the horizon line. Only one grid per page;
  the vanishing point sits at horizontal center.
  (✅ aesthetics wiki "neon-grid landscapes".)
- **VHS framing:** a thin global scanline overlay (`repeating-linear-gradient`
  2–3px stripes, ~20% opacity) plus corner HUD labels (PLAY, SP timecode,
  blinking REC) frames the whole page as a tape. (🟡 documented vocabulary.)
- **Spacing:** generous — cinematic sections (`clamp(4rem, 10vh, 8rem)`
  vertical), content `max-width: 72ch` for text, cards in 3-up grids that
  collapse to 1-up. Let the decorative elements breathe.
- **Separators:** glowing 1px horizontal rules or diamond/lozenge dividers
  (`◆`) between letterspaced subtitles; tape tickers (marquee strips) between
  major sections. (🟡 documented decoration motifs.)
- **Radius:** `0–4px` (angular) for cards, full pill for buttons only.
- **Shadows:** never dark drop-shadows — elements *emit light*: `box-shadow`
  glows in the accent color. (🟡 documented borders/shadows.)

## Components

Copy-pasteable HTML/CSS. Assumes tokens: `--pink:#FF71CE; --violet:#B967FF;
--cyan:#01CDFE; --night:#0D0221; --ground:#1A0033;`.

### 1. Neon grid hero (perspective grid)

```html
<div class="hero">
  <div class="sky"></div>
  <div class="sun"></div>
  <div class="grid-floor"></div>
  <h1 class="chrome-text">MIDNIGHT MALL</h1>
</div>
```
```css
.hero{position:relative;min-height:100vh;overflow:hidden;background:linear-gradient(180deg,#2D0052 0%,#8a2be2 35%,#FF71CE 62%,var(--night) 100%);}
.grid-floor{position:absolute;left:-25%;right:-25%;bottom:-2%;height:42%;
  background:
    repeating-linear-gradient(180deg,transparent 0 42px,rgba(1,205,254,.6) 42px 44px),
    repeating-linear-gradient(90deg,transparent 0 62px,rgba(1,205,254,.6) 62px 64px);
  transform:perspective(420px) rotateX(58deg);transform-origin:top center;
  -webkit-mask-image:linear-gradient(180deg,transparent,#000 32%);mask-image:linear-gradient(180deg,transparent,#000 32%);
  animation:grid-drift 6s linear infinite;}
@keyframes grid-drift{to{background-position:0 44px,0 0;}}
```

### 2. Chrome sun (banded, sliced)

```html
<div class="sun" aria-hidden="true"></div>
```
```css
.sun{width:min(38vw,340px);aspect-ratio:1;border-radius:50%;position:relative;overflow:hidden;
  background:linear-gradient(180deg,#FFD700 0%,#FF6B00 34%,#FF2D95 68%,var(--violet) 100%);
  box-shadow:0 0 60px rgba(255,113,206,.55),0 0 140px rgba(255,113,206,.25);}
.sun::after{content:"";position:absolute;inset:0;
  background:repeating-linear-gradient(180deg,transparent 0 12px,var(--night) 12px 15px);
  -webkit-mask-image:linear-gradient(180deg,transparent 42%,#000 85%);mask-image:linear-gradient(180deg,transparent 42%,#000 85%);}
```

### 3. Glitch headline

```html
<h1 class="glitch" data-text="THE GRID REMEMBERS">THE GRID REMEMBERS</h1>
```
```css
.glitch{position:relative;color:#fff;font-family:Orbitron,sans-serif;}
.glitch::before,.glitch::after{content:attr(data-text);position:absolute;inset:0;overflow:hidden;}
.glitch::before{color:var(--pink);transform:translate(-3px,-2px);animation:gl-a 2.6s infinite steps(2);}
.glitch::after{color:var(--cyan);transform:translate(3px,2px);animation:gl-b 3.4s infinite steps(2);}
@keyframes gl-a{0%,90%{clip-path:inset(18% 0 62% 0);}92%{clip-path:inset(4% 0 82% 0);}95%{clip-path:inset(48% 0 38% 0);}98%,100%{clip-path:inset(18% 0 62% 0);}}
@keyframes gl-b{0%,88%{clip-path:inset(64% 0 16% 0);}90%{clip-path:inset(80% 0 4% 0);}94%{clip-path:inset(30% 0 58% 0);}97%,100%{clip-path:inset(64% 0 16% 0);}}
```

### 4. Chrome text

```html
<h2 class="chrome-text">CHROME BOULEVARD</h2>
```
```css
.chrome-text{
  background:linear-gradient(180deg,#fff 0%,#cfe9ff 26%,#5a6b8c 48%,#eef7ff 52%,#8fb7d8 74%,#ffffff 100%);
  -webkit-background-clip:text;background-clip:text;color:transparent;
  font-family:Orbitron,sans-serif;font-style:italic;transform:skewX(-6deg);}
```

### 5. Cassette card

```html
<article class="cassette">
  <div class="cassette-window" aria-hidden="true"><span class="reel"></span><span class="reel"></span></div>
  <h3>Midnight Food Court</h3>
  <p class="artist">DJ Escalator · 1987</p>
  <ol class="tracks"><li>Escalator Dreams</li><li>Aisle Seven Romance</li></ol>
  <button class="btn-ghost">ADD TO CRATE · $9</button>
</article>
```
```css
.cassette{background:var(--ground);border:1px solid rgba(1,205,254,.55);border-radius:6px;
  padding:1.25rem;box-shadow:0 0 14px rgba(1,205,254,.28);}
.cassette-window{display:flex;justify-content:space-around;background:#0D0221;border:1px solid #2a1a4d;
  border-radius:4px;padding:.8rem;margin-bottom:1rem;}
.reel{width:34px;height:34px;border-radius:50%;border:3px solid #e8e8e8;position:relative;
  background:conic-gradient(#e8e8e8 0 25%,transparent 0 50%,#e8e8e8 0 75%,transparent 0);}
.cassette:hover .reel{animation:spin 1.6s linear infinite;}
@keyframes spin{to{transform:rotate(360deg);}}
.tracks{font-size:.85rem;color:rgba(255,255,255,.65);padding-left:1.2rem;}
```

### 6. HUD outline card (corner ticks)

```html
<section class="hud"><h3>Arcade Night</h3><p>Every Friday, 21:00.</p></section>
```
```css
.hud{position:relative;border:1px solid rgba(1,205,254,.55);background:rgba(26,0,51,.78);padding:1.5rem;
  box-shadow:0 0 12px rgba(1,205,254,.18),inset 0 0 24px rgba(1,205,254,.06);}
.hud::before,.hud::after{content:"";position:absolute;width:14px;height:14px;border:2px solid var(--pink);}
.hud::before{top:-2px;left:-2px;border-right:0;border-bottom:0;}
.hud::after{bottom:-2px;right:-2px;border-left:0;border-top:0;}
```

### 7. Neon buttons

```html
<button class="btn-neon">BROWSE THE CATALOG</button>
<button class="btn-ghost">INSERT COIN</button>
```
```css
.btn-neon{font-family:Orbitron,system-ui,sans-serif;letter-spacing:.18em;font-weight:700;
  background:linear-gradient(90deg,var(--pink),var(--violet));color:var(--night);
  border:0;border-radius:999px;padding:.9rem 2.2rem;cursor:pointer;
  box-shadow:0 0 18px rgba(255,113,206,.7),0 0 48px rgba(255,113,206,.3);transition:transform .15s;}
.btn-neon:hover{transform:translateY(-2px);}
.btn-ghost{font-family:Orbitron,system-ui,sans-serif;letter-spacing:.18em;font-weight:500;
  background:transparent;color:var(--cyan);border:1px solid var(--cyan);border-radius:999px;
  padding:.9rem 2.2rem;cursor:pointer;
  box-shadow:0 0 12px rgba(1,205,254,.5),inset 0 0 12px rgba(1,205,254,.12);}
```

### 8. VHS scanline overlay (whole-page framing)

```html
<body class="vhs">…</body>
```
```css
.vhs::after{content:"";position:fixed;inset:0;pointer-events:none;z-index:999;
  background:repeating-linear-gradient(0deg,rgba(0,0,0,.22) 0 1px,transparent 1px 3px);}
.rec{color:#ff3b3b;font-family:Orbitron,monospace;animation:blink 1.2s steps(2) infinite;}
@keyframes blink{50%{opacity:0;}}
```

### 9. Equalizer (audio-less)

```html
<div class="eq" aria-hidden="true"><span style="animation-delay:0s"></span><span style="animation-delay:.15s"></span><span style="animation-delay:.3s"></span><span style="animation-delay:.45s"></span><span style="animation-delay:.6s"></span><span style="animation-delay:.75s"></span></div>
```
```css
.eq{display:flex;gap:5px;align-items:flex-end;height:36px;}
.eq span{width:7px;background:linear-gradient(180deg,var(--pink),var(--cyan));animation:eq .7s ease-in-out infinite alternate;}
@keyframes eq{from{height:18%;}to{height:100%;}}
```

### 10. Tape ticker + diamond divider

```html
<div class="tape" aria-hidden="true"><p>SIDE A ◆ 45 RPM ◆ CHROME POSITION ◆&nbsp;</p><p>SIDE A ◆ 45 RPM ◆ CHROME POSITION ◆&nbsp;</p></div>
<p class="dia">FEATURED RELEASES</p>
```
```css
.tape{overflow:hidden;white-space:nowrap;border-top:1px solid rgba(255,113,206,.5);border-bottom:1px solid rgba(255,113,206,.5);
  color:var(--pink);font-family:Orbitron,monospace;letter-spacing:.3em;padding:.6rem 0;}
.tape p{display:inline-block;margin:0;animation:tape 20s linear infinite;}
@keyframes tape{to{transform:translateX(-100%);}}
.dia{letter-spacing:.35em;font-family:Orbitron,monospace;color:var(--cyan);}
.dia::before,.dia::after{content:"◆";margin:0 .75em;font-size:.7em;color:var(--pink);}
```

## Motion

Signature motion is analog-degradation motion, not app motion:

- **Glitch flicker:** RGB-split clones with `steps(2)` clip-path jumps every
  2.6–3.4s (see component 3). On hover, force the displaced state for 400ms.
- **Grid drift:** the perspective grid's horizontal lines scroll toward the
  viewer (`6s linear infinite`) — the endless night drive.
- **Scanline shimmer:** optional 8s slow vertical tracking bar across the
  overlay; keep opacity ≤ 12%.
- **Reels:** cassette reels `spin 1.6s linear infinite` only while hovered.
- **Reduced motion:** honor it — `@media (prefers-reduced-motion: reduce){
  *{animation:none!important;transition:none!important;}}`. The endless grid
  is exactly the background motion that needs a path out. (✅ vocab.design.)

## Do / Don't

- **Do** give the page exactly one sun and one grid, then set everything
  usable in quiet type on a dark ground. / **Don't** wallpaper the page with
  three suns, two grids, and a gradient behind every paragraph — that is the
  clip-art failure mode.
- **Do** use 1px neon outlines with soft glows on cards and inputs.
  / **Don't** spray `text-shadow` glow on body copy — magenta-on-cyan text is
  unreadable at any size, and chrome text has no single color to measure
  contrast against.
- **Do** run a thin scanline overlay across the whole frame at ~20% opacity.
  / **Don't** make it heavy enough to fight the text — it is a VHS patina,
  not a filter.
- **Do** animate the grid drifting toward the viewer with a
  `prefers-reduced-motion` kill switch. / **Don't** autoplay endless motion
  with no off-ramp.
- **Do** pick one register — earnest outrun (cars, night drives, chrome) or
  ironic vaporwave (malls, busts, 90s pop-ups) — and hold it.
  / **Don't** mix a Roman bust, a DeLorean, and a Windows 95 dialog on the
  same hero; the two halves of the canon satirize each other.
- **Do** use full-width Ａ Ｅ Ｓ Ｔ Ｈ Ｅ Ｔ Ｉ Ｃ and katakana as marginalia.
  / **Don't** set whole paragraphs in them — they are seasoning, not prose.

## Copy voice (for brand styles)

Vaporwave copy is **nostalgic and lightly ironic**: it mourns a future that
never happened while winking at the mall that sold it. Synthwave copy is the
earnest twin: cinematic, night-drive romantic. Write in short, declarative
fragments; name obsolete formats like relics; never explain the joke.

- "The mall never closed. It just changed frequency."
- "Remember a future that never happened? Neither do we. Press play anyway."
- "All tapes rewound by hand. Side B is where the feelings live."

## Sources

- Aesthetics Wiki — Synthwave (neon-grid landscapes, chrome lettering,
  sunsets in magenta/cyan/violet; earnest synthwave vs. ironic vaporwave):
  https://aesthetics.fandom.com/wiki/Synthwave
- Wikipedia — Vaporwave (outrun as the driving visual aesthetic: magenta
  neon, gridlines, VHS tracking artifacts):
  https://en.wikipedia.org/wiki/Vaporwave
- vocab.design — "vaporwave" term (perspective grid + statue as giveaways;
  loud hero + quiet product; glow rationed; reduced-motion path):
  https://github.com/gkurt/vocab.design/blob/HEAD/src/content/terms/vaporwave.mdx
