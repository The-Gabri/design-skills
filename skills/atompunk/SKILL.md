---
name: atompunk
description: 1950s atomic-age retro-futurism (Googie, pulp sci-fi, fallout-shelter signage): starbursts, tailfins, boomerangs, teal/chrome palettes and exclamatory ad copy for "World of Tomorrow" pages.
---

# Atompunk — 1950s Atomic-Age Retro-Futurism

## Legend
- ✅ documented in ≥2 independent sources (aesthetics/encyclopedia references, museum/architectural sources)
- 🟡 cross-referenced in ≥3 sources without a single canonical spec
- ⚠️ community approximation — useful but not dogma

**Scope note:** this is a category-D *editorial/niche* skill: use it to theme
pages, posters, expo sites and pulp-flavored content — not for full product
design systems. Mid-century (the earnest furniture/interior style) is a
different skill; atompunk is the *pulpy retro-futurist sci-fi fantasy* of the
atomic age.

## Principles
1. **The future was friendly — and atomic.** Atompunk renders 1945–1969
   (pre-Vietnam) American optimism about technology: bombs become household
   helpers, rockets become tailfins, physics becomes diner signage. Everything
   radiates confidence that tomorrow will be shinier than today. ✅
2. **Designed to be read at 40 mph.** Googie roadside architecture (John
   Lautner's Googies coffee shop, 1949; named by critic Douglas Haskell in
   1952) was built for motorists: exaggerated silhouettes, neon signs, and
   upswept rooflines that read at highway speed. On the web this means
   oversized display type, high-contrast shapes, and one dominant message per
   screen. ✅
3. **Physics as ornament.** The atom diagram, the boomerang, the starburst,
   the flying saucer, the parabola — scientific diagrams are treated as pure
   decoration, repeated until they become pattern. ✅
4. **The exclamation mark is a load-bearing structure.** Mid-century atomic
   advertising copy (Coca-Cola, Westinghouse, GE ~1955–62) is hyperbolic,
   direct-address, and punctuated: "See the Atomic Kitchen!", "Thrill to the
   Space Highway!" Copy sells the future as a ticket you can buy today. 🟡
5. **Shine = progress.** Chrome, neon, polished steel, polished Formica:
   reflective surfaces signal technological triumph. Matte is for the past;
   the future gleams. ✅
6. **One cheerful universe.** Unlike cyberpunk's neon dystopia, atompunk's
   signature dialects (Googie/Tomorrowland, atomic-advertising, pulp covers)
   share one optimistic register. A darker Fallout-style "bunker CRT"
   sub-dialect exists but mixing the two registers on one page breaks the
   spell — pick one and commit. 🟡

## Color
The canonical atompunk register is the Googie/atomic-advertising palette —
butter-cream grounds, teal + coral-red + mustard accents, chrome highlights:

| Token | Hex | Role | Conf. |
|---|---|---|---|
| `--ap-cream` | `#FFF6DE` | page background, the butter-cream of 1955 print ads | 🟡 |
| `--ap-paper` | `#FBEECB` | card/surface background | 🟡 |
| `--ap-teal` | `#1E9A96` | primary accent — Tomorrowland teal | 🟡 |
| `--ap-teal-deep` | `#0F6E6B` | teal shadow/darker gradient stop | 🟡 |
| `--ap-rocket` | `#E63B2A` | secondary accent — atomic-ad red (Coca-Cola-atomic register) | 🟡 |
| `--ap-mustard` | `#F2B234` | tertiary accent — starburst gold / Formica yellow | 🟡 |
| `--ap-chrome` | `#C7CDD4` | chrome silver (fins, sign borders, rules) | 🟡 |
| `--ap-ink` | `#22303A` | body text — warm charcoal, never pure black | ⚠️ |
| `--ap-navy` | `#152B3C` | night-sky/dark section background | ⚠️ |
| `--ap-neon` | `#FF5C39` | neon sign glow (red neon on teal or navy) | 🟡 |
| `--ap-phosphor` | `#7DFF9E` | CRT/bunker green — only for fallout-shelter and terminal notes | ⚠️ |

Rules: cream ground + exactly two of {teal, rocket-red, mustard} as the
working accents per screen; chrome as metal edges, never as a fill for large
areas. Phosphor green is a *quotation* color for shelter signage — it is not
a page accent. ⚠️

## Typography
- **Display (pulp poster):** `Bungee` (Google Fonts) — closest free face to
  the heavy, exclamatory 1950s poster hand-lettering. 🟡
- **Script accent (diner signage):** `Racing Sans One` — for "World of
  Tomorrow"-style script flourishes on signs and tickets. Use sparingly,
  one per screen max. 🟡
- **Mono/technical (shelter signage, data readouts):** `Space Mono` — for
  fallout-shelter plates, capacity numbers, countdown digits. 🟡
- **Body:** `Archivo` (regular 400 / medium 500) — a clean neo-grotesque
  standing in for mid-century ad gothics. 🟡
- **Fallback stack:** `system-ui, -apple-system, "Segoe UI", Arial,
  sans-serif` when fonts fail — the demo must still read as a poster, not a
  document. ✅ (template requirement)

Scale: display 3–5rem with tight tracking (-0.02em); subheads uppercase,
letter-spaced +0.18em; body 1rem/1.6. Headlines end in `!` when they are
selling something; body never shouts.

## Layout & spacing
- **Poster-first composition:** one hero idea per viewport, headline sized to
  fill a horizontal band, ornament *behind* text (starbursts, rays), never
  competing with it. 🟡
- **Googie angles:** section dividers and cards use diagonal cuts
  (upswept-roof echo) — a `clip-path` polygon or rotated boomerang divider
  beats a straight rule. ⚠️
- **Spacing:** generous; 1950s ads breathe. Base unit 8px, section padding
  64–96px desktop. ⚠️
- **Radius:** pill shapes for buttons and tickets (the rounded-future look);
  near-zero radius for shelter-sign plates and data cards (civic register).
  ⚠️
- **Borders:** 2–3px solid ink outlines on cards and badges (pulp-comic
  energy); chrome borders get a 1px highlight + dark base line for the
  metallic read. ⚠️
- **Texture:** subtle halftone dot pattern or paper grain behind hero areas
  — CSS `radial-gradient` dots, not an image asset. ⚠️

## Components

### 1. Starburst badge (the signature ornament)
```html
<span class="starburst"><span>NEW!</span></span>
<style>
.starburst{
  --c:#E63B2A;
  width:110px;height:110px;display:inline-grid;place-items:center;
  background:var(--c);
  clip-path:polygon(50% 0%,61% 12%,76% 6%,80% 20%,95% 20%,93% 35%,107% 42%,99% 55%,107% 68%,93% 71%,95% 86%,80% 82%,76% 96%,61% 88%,50% 100%,39% 88%,24% 96%,20% 82%,5% 86%,7% 71%,-7% 68%,1% 55%,-7% 42%,7% 35%,5% 20%,20% 18%,24% 6%,39% 12%);
  color:#FFF6DE;font-family:Bungee,system-ui,sans-serif;font-size:1.1rem;
  transform:rotate(-8deg);
}
</style>
```

### 2. Fallout-shelter sign plate (civic register)
```html
<div class="shelter">
  <span class="shelter-mark">CD</span>
  <div><strong>FALLOUT SHELTER</strong><br>CAPACITY 250 · OPEN 9–6 DAILY</div>
</div>
<style>
.shelter{display:flex;gap:14px;align-items:center;background:#152B3C;
  color:#7DFF9E;border:3px solid #7DFF9E;border-radius:6px;
  padding:14px 18px;font-family:"Space Mono",monospace;}
.shelter-mark{border:2px solid #7DFF9E;border-radius:50%;width:44px;height:44px;
  display:grid;place-items:center;font-weight:700;}
</style>
```

### 3. Rocket ticket (pill button, atomic-ad register)
```html
<a class="ticket" href="#book">Get Your Tickets! <span aria-hidden="true">→</span></a>
<style>
.ticket{display:inline-block;background:#1E9A96;color:#FFF6DE;
  font-family:Bungee,system-ui,sans-serif;font-size:1.05rem;
  padding:16px 34px;border-radius:999px;text-decoration:none;
  border:3px solid #22303A;box-shadow:0 6px 0 #22303A;
  transition:transform .12s ease,box-shadow .12s ease;}
.ticket:hover{transform:translateY(-2px) rotate(-1deg);}
.ticket:active{transform:translateY(4px);box-shadow:0 1px 0 #22303A;}
</style>
```

### 4. Boomerang divider (Googie motif, pure CSS/SVG)
```html
<svg class="boomerang" viewBox="0 0 600 60" aria-hidden="true">
  <path d="M10 45 Q300 -10 590 45" stroke="#E63B2A" stroke-width="10" fill="none" stroke-linecap="round"/>
  <circle cx="300" cy="22" r="12" fill="#F2B234" stroke="#22303A" stroke-width="4"/>
</svg>
```

### 5. Radar sweep (interactive motif, CSS keyframes)
```html
<div class="radar"><div class="sweep"></div></div>
<style>
.radar{width:180px;height:180px;border-radius:50%;position:relative;
  background:radial-gradient(circle,#0F6E6B 0%,#152B3C 75%);
  border:6px solid #C7CDD4;overflow:hidden;}
.radar::before{content:"";position:absolute;inset:0;border-radius:50%;
  background:repeating-radial-gradient(circle at center,transparent 0 28px,rgba(125,255,158,.25) 28px 30px);}
.sweep{position:absolute;inset:0;border-radius:50%;
  background:conic-gradient(from 0deg,rgba(125,255,158,.9),transparent 25%);
  animation:sweep 3.2s linear infinite;}
@keyframes sweep{to{transform:rotate(360deg);}}
@media (prefers-reduced-motion:reduce){.sweep{animation:none;}}
</style>
```

### 6. Pulp poster card (halftone + angled caption)
```html
<article class="pulp">
  <div class="pulp-art" aria-hidden="true"></div>
  <h3>Thrill to the Space Highway!</h3>
  <p>Real rocket-bus rides every 20 minutes from the North Terminal.</p>
</article>
<style>
.pulp{background:#FBEECB;border:3px solid #22303A;border-radius:14px;
  padding:18px;max-width:320px;}
.pulp-art{height:150px;border-radius:8px;border:2px solid #22303A;
  background:
    radial-gradient(circle at 70% 30%,#F2B234 0 26px,transparent 27px),
    radial-gradient(circle at 25% 65%,#1E9A96 0 40px,transparent 41px),
    radial-gradient(#22303A 1.2px,transparent 1.3px) 0 0/12px 12px,
    linear-gradient(160deg,#E63B2A,#F2B234);}
.pulp h3{font-family:Bungee,system-ui,sans-serif;font-size:1.15rem;margin:14px 0 6px;}
</style>
```

### 7. Marquee ticker (neon roadside strip)
```html
<div class="ticker"><div class="ticker-track">
  <span>ATOMIC HARBOR EXPO ★ OPENS JULY 4TH ★ FREE PARKING FOR FLYING CARS ★</span>
  <span aria-hidden="true">ATOMIC HARBOR EXPO ★ OPENS JULY 4TH ★ FREE PARKING FOR FLYING CARS ★</span>
</div></div>
<style>
.ticker{background:#152B3C;border-top:4px solid #FF5C39;border-bottom:4px solid #FF5C39;
  overflow:hidden;white-space:nowrap;}
.ticker-track{display:inline-block;animation:tick 18s linear infinite;color:#7DFF9E;
  font-family:"Space Mono",monospace;padding:10px 0;}
.ticker-track span{padding-right:60px;}
@keyframes tick{to{transform:translateX(-50%);}}
@media (prefers-reduced-motion:reduce){.ticker-track{animation:none;}}
</style>
```

## Motion
Googie motion is mechanical-optimistic, not liquid: steady radar sweeps,
ticker crawls, rocket-shake hovers, and bouncy neon flickers. No spring
physics language is documented for the era — use linear or snappy
`cubic-bezier(.2,.9,.25,1)` loops, durations 0.12–3.5s, and always honor
`prefers-reduced-motion` by freezing loops. ⚠️

## Do / Don't
- ✅ DO put one starburst or boomerang *behind* the headline as the page's
  signature ornament; 🟡 DON'T scatter six small ones — atompunk ornament is
  bold and singular, mid-century pattern tiling is a different skill.
- ✅ DO use butter-cream grounds with teal + red accents and chrome edges;
  DON'T reach for purple-blue gradients or glassmorphism — they read as
  vaporwave, not the atomic age. (template anti-slop rule)
- ✅ DO write headlines like 1955 ad copy ("See the Home of Tomorrow!");
  DON'T write deadpan minimal microcopy ("Explore exhibits") — the register
  is half the style.
- ✅ DO mix the pulpy consumer register (ads, tickets, diners) with ONE civic
  note (fallout-shelter plate, capacity readout); DON'T mix in the dark
  Fallout bunker-CRT register as the page's base — it cancels the optimism.
- ✅ DO use neon as a sign color on dark bands; DON'T use neon as body text
  on cream — legibility first.
- ✅ DO tilt badges and price tags -6° to -10° for the hand-pasted poster
  feel; DON'T rotate paragraphs or navigation.

## Copy voice
The voice of a 1958 World's Fair barker crossed with a civil-defense
pamphlet: exclamatory, second-person, future-as-ticket. Short sentences,
present tense, exclamation marks on promises, deadpan civics on data.

Examples:
- "Blast off to the World of Tomorrow — gates open July 4th, rain or shine!"
- "Thrill to the Atomic Kitchen! Dinner in 30 seconds, cooked by science."
- "SHELTER CAPACITY 250. Doors close at 1800 hours. Please remain cheerful."

## Sources
- Wikipedia — Googie architecture (motifs: boomerangs, starbursts, flying
  saucers, diagrammatic atoms, parabolas; 1945–early 1970s; named after John
  Lautner's Googies coffee shop, term coined by critic Douglas Haskell, 1952):
  https://en.wikipedia.org/wiki/Googie_architecture
- Aesthetics Wiki — Atompunk (retro-future of 1945–1969, optimism and dread
  of the atomic age, Raygun Gothic kinship) / Raygun Gothic (starbursts,
  rockets, atom models on everyday objects):
  https://aesthetics.fandom.com/wiki/Atompunk
- astronomy.com — Googie / Space Age themes (bold playful colors, chrome,
  neon, "the future is friendly", waned after Apollo 11 / ecology movement):
  https://www.astronomy.com/observing/googie-architecture-space-age-themes-shaped-modern-style/
- heysami/woven — aesthetic-atompunk.md (three sub-dialects: bunker-CRT,
  Tomorrowland/Googie, NASA-Worm; "pick one and commit"):
  https://github.com/heysami/woven/blob/HEAD/design-library/aesthetic-atompunk.md
