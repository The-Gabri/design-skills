---
name: corporate-memphis
description: Corporate Memphis / Alegria flat-illustration style — elongated noodle-limbed figures, flat geometric shapes, bright limited palettes. Use for friendly SaaS/landing art, empty states, and cheerful marketing scenes.
---

# Corporate Memphis

## Verification legend
- ✅ = documented fact, confirmed in ≥2 independent sources (history, named systems, critiques).
- 🟡 = cross-referenced across ≥2 practitioner sources; consistent but no canonical spec.
- ⚠️ = community approximation (hex values, ratios) — useful, not official.

## Principles

1. **Disproportion is the signature, not an accident.** Figures have small heads (~1:6 head-to-body vs. a realistic 1:7.5), oversized blocky torsos, and long, elastic "noodle" limbs that bend without joints. Hands are mittens or 3–4 finger paddles; feet are rounded stumps. If you fix the proportions to look realistic, you killed the style. ✅
2. **Flat or nothing.** Zero gradients, zero shading, zero drop shadows, zero blur, zero texture. Every element is one solid color. Layering (what's in front) is the only depth cue. ✅
3. **Optimism is the product.** The style is a mood instrument: cheerful, approachable, inoffensive "friendly capitalism." Figures are perpetually in motion — waving, high-fiving, carrying oversized objects — never static, never frowning. ✅
4. **Designed for replication.** Illustrator Xoana Herrera (Buck team, Facebook's Alegria) stated the style was deliberately simplified during production so any artist could copy and implement it quickly across platforms. It is a *system*, not a masterpiece: repeatable parts, fixed vocabulary. 🟡
5. **Faces are symbolic, skin is non-representational.** Dot eyes, a smile curve, no nose, no eyebrows. Skin comes in blue, purple, orange, pink, teal, yellow — deliberately unnatural, so no figure reads as a real demographic. ✅ (see Do/Don't for the critique this invited)
6. **Know what it's named after, and what it isn't.** The name "Corporate Memphis" was coined by Mike Merrill for an Are.na collection (✅); the original Alegria system was built by Buck for Facebook in 2017 (✅). It borrows geometric cheer from the 1980s Memphis Group (Ettore Sottsass) but strips out that movement's rebellious anti-design edge — it's Memphis *domesticated*. ✅

## Color

Two working palettes. There is no official token sheet (Buck never published one), so all hexes are ⚠️ approximations sampled from observed Alegria-era examples — keep 3–5 colors per composition. 🟡

**"Bright Alegria" palette (the classic big-tech look)**
| Token | Hex | Role |
|---|---|---|
| `--ink` | `#22242B` | Body text, face dots, hair |
| `--paper` | `#FFFFFF` | Background (95% of compositions sit on white) ✅ |
| `--blue` | `#4A90E2` | Skin tone / primary shapes |
| `--coral` | `#FF6B6B` | Blobs, accent shapes, CTAs |
| `--sun` | `#FFC857` | Skin tone / highlight shapes |
| `--teal` | `#00B2A9` | Skin tone / secondary shapes |
| `--grape` | `#9B59B6` | Skin tone / tertiary shapes |
| `--leaf` | `#2ECC71` | Plants, success states |

**"Pastel friendly" palette (healthcare/education variant)**
| Token | Hex | Role |
|---|---|---|
| `--blush` | `#FFB3BA` | Skin / soft shapes |
| `--sky` | `#BAE1FF` | Skin / backgrounds |
| `--mint` | `#B4E7CE` | Shapes |
| `--butter` | `#FFF4A3` | Highlights |
| `--lilac` | `#D5AAFF` | Shapes |

**Skin-tone set** (rotate within one scene, don't default to one): blue `#4A90E2`, purple `#9B59B6`, coral `#FF6B6B`, orange `#FF8C42`, pink `#FF69B4`, yellow `#FFC857`, teal `#00B2A9`. ⚠️
**Rule:** limited palette per composition (3–5 colors max) 🟡; high contrast between figures and background ✅.

## Typography

No canonical typeface — Alegria-era brands used friendly rounded/geometric sans-serifs.
Closest free substitutes, in order of fit: **Poppins** (600–800 for headlines, 400–500 for body), **Nunito**, **Quicksand**. ⚠️
- Headlines: sentence case, tight letter-spacing (−0.02em), weight 700–800. 🟡
- Body: 16–18px, line-height 1.6, `#5B5F6A` muted ink on white. ⚠️
- No serif, no all-caps shouting, no thin weights — soft and round everywhere. 🟡

## Layout & spacing

- **Generous white space.** Illustrations need room; scenes breathe with 80–120px section padding. 🟡
- **Asymmetric balance.** Figures and shapes sit off-center; floating elements defy gravity (no ground shadows). ✅
- **Spot illustrations, not backgrounds.** The classic pattern: white/very light page, with a hero scene floating right of the copy, and small scenes anchoring feature blocks. ✅
- **Shape vocabulary** as decoration: circles/dots, triangles, irregular blobs, squiggles, plus-sign confetti, small cross-hatches. Memphis Group heritage, kept safe. ✅
- **Radius:** 20–28px on cards, full-pill on buttons and chips. ⚠️
- **Borders:** none, or a single 2px ink border on secondary buttons. No card shadows — flat. 🟡

## Components

All examples are copy-pasteable. Colors reference the tokens above. **No gradients, no shadows, anywhere.**

### 1. Blob figure (the atomic unit)

The canonical figure: head circle, dot eyes + smile, blocky rounded-rect torso, noodle-limb strokes with round linecaps, mitten hands, stump feet. Arms and legs are `<path>` strokes, not filled shapes — that's what makes limbs look elastic.

```html
<!-- Wave pose, 200x330 canvas. Skin/shirt/pants are swappable tokens. -->
<svg viewBox="0 0 200 330" width="200" height="330" role="img" aria-label="Waving flat-illustration figure">
  <!-- legs: thick round-cap strokes = noodle limbs -->
  <path d="M100 224 C 94 256 88 276 86 298" stroke="#2B3A67" stroke-width="24" stroke-linecap="round" fill="none"/>
  <path d="M108 224 C 114 252 120 274 122 298" stroke="#2B3A67" stroke-width="24" stroke-linecap="round" fill="none"/>
  <!-- torso: blocky rounded rect -->
  <rect x="68" y="112" width="64" height="116" rx="30" fill="#FFC857"/>
  <!-- arms: one raised wave, one relaxed -->
  <path d="M78 134 C 56 112 42 100 34 86" stroke="#FFC857" stroke-width="16" stroke-linecap="round" fill="none"/>
  <path d="M122 134 C 138 158 146 172 152 192" stroke="#FFC857" stroke-width="16" stroke-linecap="round" fill="none"/>
  <!-- mitten hands -->
  <circle cx="34" cy="86" r="11" fill="#4A90E2"/>
  <circle cx="152" cy="192" r="11" fill="#4A90E2"/>
  <!-- head -->
  <circle cx="100" cy="70" r="27" fill="#4A90E2"/>
  <!-- hair tuft -->
  <path d="M74 58 Q 80 30 100 30 Q 122 30 128 58 Q 114 44 100 46 Q 86 44 74 58 Z" fill="#22242B"/>
  <!-- face: dots + smile, no nose, no brows -->
  <circle cx="91" cy="66" r="3.2" fill="#22242B"/>
  <circle cx="109" cy="66" r="3.2" fill="#22242B"/>
  <path d="M90 79 Q 100 88 110 79" stroke="#22242B" stroke-width="3" stroke-linecap="round" fill="none"/>
</svg>
```

### 2. Figure pose variants (swap the arm paths)

Same body, different stories — limbs do the acting. 🟡

```html
<!-- CHEER: both arms up -->
<path d="M78 134 C 60 106 48 78 38 54" stroke="#FFC857" stroke-width="16" stroke-linecap="round" fill="none"/>
<path d="M122 134 C 140 106 152 78 162 54" stroke="#FFC857" stroke-width="16" stroke-linecap="round" fill="none"/>
<circle cx="38" cy="54" r="11" fill="#4A90E2"/>
<circle cx="162" cy="54" r="11" fill="#4A90E2"/>

<!-- HIGH-FIVE (pair): inner arms reach toward each other -->
<!-- left figure -->
<path d="M122 134 C 142 116 156 98 170 82" stroke="#00B2A9" stroke-width="16" stroke-linecap="round" fill="none"/>
<circle cx="170" cy="82" r="11" fill="#9B59B6"/>
<!-- right figure: same SVG group with transform="scale(-1,1) translate(-200,0)" -->

<!-- PHONE-HOLDER: one hand up, giant phone prop -->
<rect x="126" y="30" width="48" height="88" rx="12" fill="#FFC857"/>
<rect x="134" y="42" width="32" height="56" rx="6" fill="#FFFFFF"/>
<path d="M78 134 C 100 120 118 116 136 108" stroke="#00B2A9" stroke-width="16" stroke-linecap="round" fill="none"/>
<circle cx="136" cy="108" r="11" fill="#9B59B6"/>
```

### 3. Hero scene (blob + figures + floating geometry)

The signature composition: one big organic blob, 2–3 figures in action, confetti shapes orbiting, all flat. 🟡

```html
<svg viewBox="0 0 560 420" role="img" aria-label="Team celebrating on a coral blob">
  <!-- ground blob -->
  <path d="M60 340 C 60 250 140 200 260 200 C 390 200 470 240 500 320
           C 470 380 380 400 260 400 C 140 400 60 390 60 340 Z" fill="#FF6B6B"/>
  <!-- floating confetti -->
  <circle cx="90" cy="80" r="18" fill="#FFC857"/>
  <polygon points="470,60 500,110 440,110" fill="#00B2A9"/>
  <path d="M400 140 q 12 -18 24 0 q 12 18 24 0" stroke="#4A90E2" stroke-width="8" fill="none" stroke-linecap="round"/>
  <circle cx="150" cy="150" r="7" fill="#9B59B6"/>
  <circle cx="500" cy="200" r="7" fill="#9B59B6"/>
  <path d="M300 60 v28 M286 74 h28" stroke="#2ECC71" stroke-width="8" stroke-linecap="round"/>
  <!-- figures: place figure groups with translate/scale, e.g. -->
  <g transform="translate(150,60) scale(0.9)"> <!-- figure markup here --> </g>
  <g transform="translate(320,40) scale(1.0)"> <!-- figure markup here --> </g>
</svg>
```

### 4. Chunky CTA button

Flat, pill, high saturation. Primary on white; secondary is white with 2px ink border. 🟡

```css
.cm-btn {
  display: inline-flex; align-items: center; gap: 8px;
  background: #FF6B6B; color: #fff;
  font: 600 16px/1 Poppins, "Segoe UI", system-ui, sans-serif;
  padding: 16px 32px; border: 0; border-radius: 999px;
  cursor: pointer; transition: transform .15s ease;
}
.cm-btn:hover { transform: translateY(-2px); } /* flat — no shadow on hover */
.cm-btn:active { transform: translateY(1px) scale(.98); }
.cm-btn--ghost { background: #fff; color: #22242B; border: 2px solid #22242B; }
```

### 5. Feature card with mini scene

Flat tinted card, small scene on top, left-aligned copy. No shadows. ⚠️

```html
<div class="cm-card">
  <svg viewBox="0 0 200 140" class="cm-card__art"><!-- mini scene: figure + 2 shapes --></svg>
  <h3>Time off that runs itself</h3>
  <p>Requests, approvals, and balances — handled. Nobody chases a spreadsheet again.</p>
</div>
<style>
.cm-card { background: #FFF6EC; border-radius: 24px; padding: 28px; max-width: 320px; }
.cm-card h3 { font: 700 20px Poppins, "Segoe UI", system-ui, sans-serif; color: #22242B; margin: 16px 0 8px; }
.cm-card p { font: 400 16px/1.6 Poppins, "Segoe UI", system-ui, sans-serif; color: #5B5F6A; margin: 0; }
</style>
```

### 6. Testimonial card + face avatar

Avatar = head circle + dot eyes + smile at small scale. Vary skin tones across cards. 🟡

```html
<div class="cm-quote">
  <svg viewBox="0 0 64 64" width="56" height="56" aria-hidden="true">
    <circle cx="32" cy="32" r="28" fill="#9B59B6"/>
    <circle cx="24" cy="28" r="3" fill="#22242B"/>
    <circle cx="40" cy="28" r="3" fill="#22242B"/>
    <path d="M23 40 Q 32 47 41 40" stroke="#22242B" stroke-width="3" stroke-linecap="round" fill="none"/>
  </svg>
  <p>"Payroll used to eat my Fridays. Now it takes nine minutes."</p>
  <cite>Maya Chen — Ops lead, Brightline Studio</cite>
</div>
```

### 7. Pricing toggle card

Flat card, annual/monthly toggle updates the number. Big round numbers, coral highlight for the popular tier. ⚠️

```html
<label class="cm-toggle">
  <span>Monthly</span>
  <input type="checkbox" id="cm-billing">
  <span class="cm-toggle__track"><span class="cm-toggle__dot"></span></span>
  <span>Annual <em>−20%</em></span>
</label>
<div class="cm-price">
  <span class="cm-price__amount" data-monthly="16" data-annual="13">$16</span>
  <span>/ user / month</span>
</div>
```

### 8. Empty-state / onboarding scene pattern

The style's home turf: a single figure + 2–3 shapes in a big whitespace panel. ✅ (its original job was filling product whitespace)

```html
<div class="cm-empty">
  <svg viewBox="0 0 300 220"><!-- one cheer figure + circle + squiggle --></svg>
  <h3>No time-off requests yet</h3>
  <p>When someone asks for a break, it lands here. Go enjoy yours.</p>
  <button class="cm-btn">Request time off</button>
</div>
```

## Motion

No signature motion language is documented for the style; its native motion is simple flat shape-tweening (figures were built to be easy to animate — see Herrera's replicability note 🟡). If you animate: 2D transforms only (translate/rotate/scale), 200–400ms, `ease-out`; never add depth, blur, or parallax — flatness is the whole point. ⚠️ One line on reduced motion: honor `prefers-reduced-motion` and freeze looping figure animations.

## Do / Don't

- ✅ DO keep every figure in motion — waving, carrying, high-fiving. A stiff, symmetrical, standing-at-attention figure reads as a stock icon, not Alegria.
  ❌ DON'T draw static, front-facing, arms-at-sides figures.
- ✅ DO use the full skin-tone range within one scene (blue, purple, coral, teal, yellow). That's the mechanism the style uses for universality.
  ❌ DON'T render the whole cast in one skin tone — a page of identical blue people is exactly the "globohomo" critique (✅ documented backlash: starter-pack meme, subreddit, Fast Company).
- ✅ DO limit each composition to 3–5 flat colors, high contrast against the background.
  ❌ DON'T add gradients, drop shadows, or shading "to make it pop" — flatness *is* the pop here.
- ✅ DO use non-representational skin tones when the goal is abstract universality (onboarding, marketing whitespace).
  ❌ DON'T use facelessness as a diversity dodge: critics have explicitly called out using blank, featureless figures to avoid depicting real human variation (🟡/⚠️ community critique). If the scene is *about* real people (testimonials, "our customers"), pair the illustration with real names, roles, and — where credibility matters — real photos.
- ✅ DO give every figure a tiny face (dot eyes + smile) or a deliberately blank oval — pick one rule per set.
  ❌ DON'T mix faced and faceless figures in the same set; inconsistency reads as slop.
- ✅ DO keep line weight uniform if you use outlines at all (the style usually uses none).
  ❌ DON'T mix outlined and un-outlined figures, or flat figures with shaded/3D ones, in one product.
- ✅ DO use the style where it belongs: landing heroes, empty states, onboarding, error pages, marketing whitespace.
  ❌ DON'T illustrate a truth claim with it — "our happy customers" drawn as blob people instead of photographed is the anti-pattern critics cite (🟡).
- ✅ DO keep hands as mittens/paddles and feet as stumps.
  ❌ DON'T add detailed fingers, shoes, or wrinkles — detail collapses the geometric charm.

## Copy voice

Warm, plain-spoken, relentlessly optimistic team-coach energy. Short sentences. "We" and "you", never jargon. The visual equivalent of the illustrations: everything is going to be fine, and it's going to be fun.

- "Payday used to eat your Fridays. Not anymore."
- "Hire in days, not months — and actually enjoy the interviews."
- "Time off that runs itself. Go touch grass, we've got the paperwork."

## Sources consulted
- Corporate Memphis — Wikipedia (term coined by Mike Merrill; Alegria by Buck, 2017; visual characteristics; polarized reception). https://en.wikipedia.org/wiki/Corporate_Memphis
- Angelica Frey, "Facebook made a certain type of illustration ubiquitous—but it's time to stop knocking it" — Fast Company (2022): Alegria's origin, anodyne cheerfulness, "globohomo"/starter-pack backlash. https://www.fastcompany.com/90711508/facebook-made-a-certain-type-of-illustration-ubiquitous-but-its-time-to-stop-knocking-it
- "How Did Corporate Memphis Become Popular? And Why Do People Hate It?" — Jumpstart Magazine (Xoana Herrera on designing for replicability; unnatural skin tones; always in motion). https://www.jumpstartmag.com/how-did-corporate-memphis-become-popular/
- "Corporate Memphis Style Guide" — rfxlamia/claude-skillkit (recipe-level detail: proportions, no-gradient rule, palettes, poses).
- design-system-skills, illustration anti-patterns (peterbamuhigire) — the "faceless-everyone as a diversity dodge" critique.
