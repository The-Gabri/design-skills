---
name: teenage-engineering
description: Teenage Engineering industrial minimalism — off-white hardware-catalog pages, thin technical typography, spec-table density, restrained safety-orange accents, and dry lowercase copy. Use for pocket-gadget product pages, spec sheets, and manual-style layouts.
---

# teenage-engineering

Design in the visual language of Teenage Engineering (Stockholm): consumer
electronics presented like precision instruments. The page is a catalog, the
product is the artifact, and every label earns its place.

## Principles

1. **Less, but better — with a sense of humor.** Dieter Rams' discipline
   (honest materials, geometric constraint, function first) crossed with
   narrative and wit. Formal without being cold; Kouthoofd treats product
   design as storytelling, closer to Olivetti than to Braun austerity. 🟡
2. **The product is the hero; the page is the stage.** Chrome stays
   monochrome so the device itself carries all the color. Product photography
   (or line art) is always shown straight-on, uncropped, on white or off-white —
   never in a decorative frame. ⚠️
3. **Spec-sheet honesty.** Dimensions in millimeters *and* inches, weight in
   grams *and* ounces, audio specs as measured values (impedance, SNR, dBu).
   Numbers are the marketing. ✅ (official site spec sections)
4. **Color = function.** Orange means *engineered / important / do not ignore*
   (industrial safety equipment), borrowed from the OP-1's color-coded encoders
   where each color maps to an on-screen parameter. Accent is signal, never
   decoration. 🟡
5. **Everything sits on a calculated grid.** Layouts derive from a strict
   grid (International Typographic Style lineage); thin 1px rules separate
   sections, generous whitespace does the rest. 🟡

## Color

| token | hex | role | confidence |
|---|---|---|---|
| `--te-paper` | `#F5F4F0` | page background, off-white | 🟡 widely documented |
| `--te-ink` | `#0F0E12` | text, near-black (true black, never dark gray) | 🟡 two independent analyses |
| `--te-line` | `#E4E2DA` | hairline dividers, spec-table rules | ⚠️ approximation |
| `--te-orange` | `#FF4D00` | signal accent: record dots, buy now, one callout | ⚠️ community approximation |
| `--te-red` | `#E1251B` | secondary signal (record indicators, OB-4 red) | ⚠️ approximation |
| `--te-aluminum` | `#C8C8C6` | machined-metal tone for device illustration | ⚠️ approximation |
| `--te-oled` | `#A6E22E` | device-display green (UI of the hardware, not the page) | ⚠️ approximation |

Usage rules: the interface itself is monochrome (ink on paper, thin lines).
Orange appears at most 2–3 times per view, always as signal — a buy link, a
record LED, a dimension marker. Never as decoration, never on hover states.
Dark sections are rare; when used, `#0F0E12` background with `#F5F5F5` text and
`#333` hairlines. ⚠️

## Typography

- **Official:** custom Univers variants (UniversTE20T/40L) — proprietary, not
  publicly available. 🟡
- **Closest free substitutes:** a light neo-grotesque for headlines
  (`Archivo`, `Inter Tight` — thin weights, tight tracking) and a true
  monospace for labels and specs (`Space Mono`, `IBM Plex Mono`).
- **Scale (documented for TE hardware UI, transfers well):** micro labels
  9–11px, body 13px, subheads 16px, display 22px+. 🟡
- **Case rules (official site):** wordmark, product names, section headings,
  and body copy are **lowercase** ("teenage engineering", "ep-136 k.o.–sidekick",
  "specifications", "buy now"). Model numbers always use an **en-dash**:
  `EP–133`, `TP–7`, `CM–15`, `OB–4` — never a hyphen. Mono micro-labels
  (version tags, units) may run uppercase with ~0.12em tracking. ✅

## Layout & spacing

- **Grid:** strict 12-column / calculated modular grid; generous margins and
  large vertical rhythm. Nothing is approximate.
- **Spacing scale:** 8pt base (`8 / 16 / 24 / 32 / 48 / 64px`); whitespace is a
  feature, not emptiness.
- **Rules:** 1px hairlines (`--te-line`) between major sections; spec tables
  use 1px cell gaps.
- **Radius & shadow:** effectively zero — no border-radius, no drop shadows,
  no glass. A product sits flat on the page. ⚠️
- **Imagery:** product shown large, centered or left-aligned, on plain paper;
  technical line-art figures with numbered callouts and dimension arrows for
  manuals.

## Components

### 1. minimal nav

```html
<header class="te-nav">
  <a class="te-wordmark" href="#">teenage engineering</a>
  <nav>
    <a href="#">products</a><a href="#">field system™</a>
    <a href="#">guides</a><a href="#">support</a>
  </nav>
  <a class="te-cart" href="#">cart (0)</a>
</header>
<style>
.te-nav{display:flex;align-items:center;justify-content:space-between;
  padding:20px 32px;border-bottom:1px solid #E4E2DA;
  font-family:'Space Mono',monospace;font-size:12px;background:#F5F4F0}
.te-nav a{color:#0F0E12;text-decoration:none}
.te-nav nav{display:flex;gap:28px}
.te-nav a:hover{opacity:.6;transition:opacity 200ms ease}
</style>
```

### 2. product hero (lowercase, model first)

```html
<section class="te-hero">
  <p class="te-kicker">tp–9 · pocket looper</p>
  <h1>tape buddy</h1>
  <p class="te-dek">a tape recorder, without the tape.</p>
  <p class="te-price">$199 <a href="#">buy now</a></p>
</section>
<style>
.te-kicker{font-family:'Space Mono',monospace;font-size:11px;
  letter-spacing:.12em;text-transform:uppercase;color:#0F0E12}
.te-hero h1{font-family:'Archivo',sans-serif;font-weight:300;
  font-size:clamp(56px,9vw,120px);letter-spacing:-.03em;margin:.2em 0}
.te-dek{font-size:18px;font-weight:300;max-width:34ch}
.te-price{font-family:'Space Mono',monospace;font-size:13px}
.te-price a{color:#FF4D00;text-decoration:none}
</style>
```

### 3. spec table (dual units, grouped)

```html
<section class="te-specs">
  <h2>specifications</h2>
  <h3>dimensions and weight</h3>
  <dl>
    <div><dt>size</dt><dd>96 mm x 68 mm x 16 mm</dd><dd class="alt">3.78" x 2.68" x 0.63" inches</dd></div>
    <div><dt>weight</dt><dd>170 g</dd><dd class="alt">6.0 oz</dd></div>
  </dl>
  <h3>audio</h3>
  <dl>
    <div><dt>input</dt><dd>impedance: 10k</dd><dd>max level: 8 dBu / 2 Vrms</dd></div>
    <div><dt>output</dt><dd>max level: 1.4 Vrms</dd><dd>SNR: 108 dBA (typical)</dd></div>
    <div><dt>format</dt><dd>48 kHz / 24-bit</dd><dd>128 GB internal storage</dd></div>
  </dl>
</section>
<style>
.te-specs h2{font-size:22px;font-weight:300}
.te-specs h3{font-family:'Space Mono',monospace;font-size:11px;
  letter-spacing:.12em;text-transform:uppercase;font-weight:400;
  border-top:1px solid #E4E2DA;padding-top:16px}
.te-specs dl>div{display:grid;grid-template-columns:1fr 1fr 1fr;gap:8px;
  padding:10px 0;border-top:1px solid #E4E2DA;font-size:13px}
.te-specs dt{font-family:'Space Mono',monospace;font-size:11px;color:#0F0E12;opacity:.6}
.te-specs .alt{opacity:.6}
</style>
```

### 4. line-art figure with numbered callouts

```html
<figure class="te-figure">
  <svg viewBox="0 0 400 260" role="img" aria-label="tp–9 front view">
    <!-- thin-stroked device, callout lines to numbered labels -->
    <rect x="120" y="40" width="160" height="180" fill="none" stroke="#0F0E12" stroke-width="1.5"/>
    <circle cx="160" cy="90" r="14" fill="none" stroke="#0F0E12" stroke-width="1.5"/>
    <circle cx="160" cy="90" r="14" fill="none" stroke="#FF4D00" stroke-width="3" stroke-dasharray="22 66"/>
    <line x1="174" y1="90" x2="230" y2="60" stroke="#0F0E12" stroke-width="1"/>
    <text x="236" y="63" font-family="Space Mono" font-size="10">1 — record encoder</text>
  </svg>
  <figcaption>fig. 01 — front panel, all controls labeled.</figcaption>
</figure>
<style>
.te-figure{border-top:1px solid #E4E2DA;padding-top:24px}
.te-figure figcaption{font-family:'Space Mono',monospace;font-size:11px;opacity:.6;margin-top:12px}
</style>
```

### 5. price / buy row

```html
<p class="te-buy"><span>$199</span> <a href="#">buy now</a> <span class="te-note">ships in 3–5 days. 2-year warranty.</span></p>
<style>
.te-buy{font-family:'Space Mono',monospace;font-size:13px;
  border-top:1px solid #E4E2DA;border-bottom:1px solid #E4E2DA;padding:16px 0}
.te-buy a{color:#FF4D00;text-decoration:none}
.te-buy .te-note{opacity:.55;margin-left:16px}
</style>
```

### 6. manual-style numbered steps

```html
<ol class="te-manual">
  <li><span>01</span>press record. the orange dot means it's listening.</li>
  <li><span>02</span>spin the reel to scrub back through time.</li>
  <li><span>03</span>press play. that's the whole manual.</li>
</ol>
<style>
.te-manual{list-style:none;padding:0;font-size:15px;font-weight:300}
.te-manual li{padding:14px 0;border-top:1px solid #E4E2DA;display:flex;gap:24px}
.te-manual span{font-family:'Space Mono',monospace;font-size:11px;opacity:.55}
</style>
```

### 7. feature list (period-terminated, lowercase)

```html
<ul class="te-features">
  <li>records everything, all the time.</li>
  <li>7 hours of battery. yes, really.</li>
  <li>fits in the same pocket as your keys.</li>
</ul>
<style>
.te-features{list-style:none;padding:0;font-size:16px;font-weight:300}
.te-features li{padding:8px 0}
.te-features li::before{content:"— "}
</style>
```

### 8. section divider + lowercase heading

```html
<div class="te-rule"></div>
<h2 class="te-h2">complete your setup</h2>
<style>
.te-rule{border-top:1px solid #E4E2DA;margin:64px 0 0}
.te-h2{font-size:26px;font-weight:300;margin:16px 0 32px}
</style>
```

### 9. minimal footer

```html
<footer class="te-footer">
  <p>teenage engineering · stockholm, sweden</p>
  <p><a href="#">terms</a> <a href="#">privacy</a> <a href="#">contact</a></p>
</footer>
<style>
.te-footer{display:flex;justify-content:space-between;padding:32px;
  border-top:1px solid #E4E2DA;font-family:'Space Mono',monospace;
  font-size:11px;color:#0F0E12;opacity:.7}
.te-footer a{color:#0F0E12;text-decoration:none;margin-left:16px}
</style>
```

### 10. mono version tag

```html
<span class="te-tag">os 1.2.4 · rev c</span>
<style>
.te-tag{font-family:'Space Mono',monospace;font-size:10px;letter-spacing:.1em;
  text-transform:uppercase;border:1px solid #E4E2DA;padding:4px 8px}
</style>
```

## Motion

There is no motion language. Allowed: link hover `opacity 200ms ease`
(1.0 → 0.6), and mechanical indicator blinks on hardware UI (linear,
step-like — no springs, no easing theatrics). No scroll animations, no
parallax, no hover transforms. If you need animation to make the design work,
the design doesn't work. ⚠️

## Do / Don't

- **Do** write everything lowercase, including "buy now" — **don't** uppercase
  CTAs for emphasis.
- **Do** give dimensions and weight in both metric and imperial —
  **don't** round to marketing-friendly numbers.
- **Do** use an en-dash in model numbers (`EP–133`) — **don't** use a hyphen
  (`EP-133`).
- **Do** let one orange element carry the whole page's color —
  **don't** add a second accent color "for balance".
- **Do** end feature bullets with periods — **don't** use exclamation marks,
  ever.
- **Do** draw products as thin-stroked line art with numbered callouts in
  manuals — **don't** render them in 3D or with drop shadows.
- **Do** keep hover feedback to an opacity shift — **don't** lift, scale, or
  tilt cards.

## Copy voice

Dry, technical, understatedly funny. Short sentences. Lowercase. No
superlatives ("best", "amazing", "revolutionary" never appear). Prices are
stated as facts. Specs replace adjectives.

Real examples from teenage.engineering (official site): ✅

- "the plan was to build a mixer for the K.O.ii. but it became more of an
  effect-box with a built-in sequencer. quite cool actually."
- "studio - home - office - on stage" / "complete your setup"

Write new copy in the same voice, e.g.:

- "a tape recorder, without the tape."
- "battery life: yes."
- "we made the buttons big enough to find in the dark. you're welcome."
