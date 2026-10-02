---
name: scandinavian
description: Scandinavian design language — airy functionalism, light woods, white space, muted naturals with one democratic pop accent. Use for bright, honest, hygge-warm product and brand pages (not dark/moody — that's japandi).
---

# Scandinavian Design

## Verification legend
- ✅ = documented in design history / designer monographs / official brand guidelines, confirmed in ≥2 independent sources.
- 🟡 = consistently described across ≥3 independent design sources, no single canonical spec.
- ⚠️ = community approximation or my working token — useful, not doctrine.

## Purpose
Produce interfaces and pages with the real Scandinavian design language: the post-war Nordic movement (Sweden, Denmark, Norway, Finland, Iceland) built on functionalism, democratic access, honest materials, and designing for long dark winters — so light, warmth, and clarity are functional requirements, not decoration. ✅

## Principles
1. **Form follows function, warmth follows form.** Every object earns its place by working well; beauty comes from honest construction, never ornament. The Danish *hygge* layer — wool, linen, candlelight-soft tones — keeps the minimalism from feeling cold. 🟡
2. **Lagom — "not too much, not too little."** The Swedish ideal of the measured middle: restraint in color, type, and layout. Nothing shouts; if the typeface is noticed, it has failed (cf. Sweden Sans design brief). 🟡
3. **Design for the light you don't have.** Nordic winters mean ~6 hours of daylight: interiors and pages are built bright — white and pale grounds, reflective surfaces, uncluttered compositions that let light (literal and visual) move. 🟡
4. **Democratic design.** Good design is for everyone, not collectors — the IKEA lineage. Clear pricing, plain language, repairable honest products. On the web: legible type, obvious affordances, no gatekeeping. ✅
5. **Honest materials, visible craft.** Light woods (pine, birch, ash, beech) shown as wood, not lacquered into anonymity; wool, linen, leather, stone, matte ceramics. Grain and weave are the decoration. 🟡
6. **Craft lineage matters.** Aalto, Wegner, Jacobsen, Mogensen, Kaare Klint, Henningsen, Panton, Maija Isola — reference the lineage through proportion and material honesty, never pastiche. Name real designers only for real pieces. ✅

## Color
Base is always light and neutral; accents are muted naturals with **one** restrained pop per composition. Hexes are working approximations (⚠️); the roles and families are cross-referenced (🟡).

| Token | Hex | Role | Confidence |
|---|---|---|---|
| `--snow` | `#FAFAF7` | Page background, near-white with a breath of warmth | ⚠️ |
| `--porcelain` | `#FFFFFF` | Cards, elevated surfaces | ⚠️ |
| `--linen` | `#F2EDE2` | Warm secondary surface, section bands | ⚠️ |
| `--oat` | `#E4DCCB` | Tertiary surface, image placeholders, dividers | ⚠️ |
| `--fog` | `#B9B3A6` | Hairline borders, inactive states | ⚠️ |
| `--stone` | `#6F6A5E` | Secondary text, captions | ⚠️ |
| `--ink` | `#23211D` | Primary text, near-black kept warm and soft | ⚠️ |
| `--birch` | `#D9C29B` | Light wood tone (pine/birch/ash) | ⚠️ |
| `--oak` | `#B28C5A` | Mid wood tone, furniture accents | ⚠️ |
| `--fjord` | `#5F7E9C` | Dusty blue accent — textiles, links, details | ⚠️ |
| `--sage` | `#8C9A7B` | Muted green accent — the second choice, never with fjord | ⚠️ |
| `--lingonberry` | `#A63D40` | The democratic pop: one red accent per page (CTA *or* badge, not both) | ⚠️ |
| `--ochre` | `#C99A4B` | Burnt-amber alternative pop for autumnal ranges | ⚠️ |

Rules:
- Backgrounds stay in the white→linen range. Dark sections are an accent device, used sparingly (one band max) — a dark page is japandi, not Scandinavian. 🟡
- Black appears as graphic punctuation: thin rules, small labels, hardware — never large fills. 🟡
- Pick **one** accent family per page: fjord *or* sage *or* lingonberry. Muted pastels (dusty pink, pale blue) may layer quietly underneath. 🟡
- Wood tones are materials, not brand colors: use them in imagery and product swatches, sparingly as UI fills. ⚠️

## Typography
- **Voice of the letterforms:** modern, clean sans-serifs; humble, easygoing, quiet. Sweden's commissioned national typeface *Sweden Sans* (Söderhavet) was explicitly designed to embody *lagom* — "simple, doesn't shout." 🟡
- **Free substitutes:** `Josefin Sans` or `Jost` for display (geometric, Nordic-flavored); `Karla`, `Source Sans 3`, or system humanist for body. Pair one geometric display face with one warm humanist text face — never two geometrics. ⚠️
- **Scale:** generous but calm — display 40–64 px light/regular, never black weight for headlines; body 16–18 px with 1.6 line-height. Whitespace does the shouting. ⚠️
- **Labels:** uppercase, 11–13 px, letter-spacing 0.12–0.2 em, stone grey — the signature Scandi micro-label ("NEW ARRIVAL", "OAK / WOOL"). 🟡
- **Warmth exception:** a single handwritten or script accent (designer signature, "hej!") is documented in Nordic graphic design as the warmth counterpoint — use once per page at most. 🟡

## Layout & spacing
- **Air first:** 8 pt base scale, but sections breathe at 96–160 px vertical rhythm. Generous margins are the luxury signal — restraint reads as quality. 🟡
- **Grid:** 12-column, max content width ~1200 px, left-aligned editorial compositions. Centered layouts are the exception (never the default hero). ⚠️
- **Radius:** small and honest — 4–8 px on cards, 999 px only for small filter pills and avatars. Scandinavian is not blobby. ⚠️
- **Borders & shadow:** 1 px `--fog` hairlines; shadows are soft daylight — `0 8px 30px rgba(35,33,29,.08)`, never hard offset shadows (that's neo-brutalism). ⚠️
- **Light rule:** compose as if lit by a north-facing window — soft, diffuse, even. No dramatic chiaroscuro, no vignettes. 🟡
- **Texture:** linen/weave/wood-grain suggested through imagery and material swatches; texture carries as much weight as color (Neptune design director, via Livingetc). 🟡

## Components
Six signature components, copy-pasteable. Assumes the tokens above as CSS custom properties.

### 1. Airy editorial hero (left-aligned, never centered)
```html
<section class="hero">
  <p class="kicker">New collection — Autumn</p>
  <h1>Furniture for<br>the long light.</h1>
  <p class="lede">Solid oak, honest wool, and joinery we're happy to show you. Designed in Copenhagen, built to be kept.</p>
  <div class="cta-row">
    <a class="btn-primary" href="#">Shop the collection</a>
    <a class="btn-ghost" href="#">Our craft</a>
  </div>
</section>
```
```css
.hero{max-width:1200px;margin:0 auto;padding:120px 32px 96px}
.kicker{font-size:12px;letter-spacing:.18em;text-transform:uppercase;color:var(--stone)}
.hero h1{font-family:"Josefin Sans",sans-serif;font-weight:400;font-size:clamp(40px,6vw,68px);line-height:1.05;color:var(--ink);margin:20px 0}
.lede{font-size:18px;line-height:1.6;color:var(--stone);max-width:46ch}
.cta-row{display:flex;gap:16px;margin-top:32px}
```

### 2. Honest product card (the democratic-design card)
Price visible, materials named, no fake urgency.
```html
<article class="product">
  <div class="product-media"><span class="badge">New</span><!-- product image --></div>
  <div class="product-body">
    <h3>Kvist dining chair</h3>
    <p class="product-meta">Solid oak · Wool bouclé · Maja Lindqvist</p>
    <div class="product-row">
      <span class="price">€249</span>
      <button class="btn-small">Add to basket</button>
    </div>
  </div>
</article>
```
```css
.product{background:var(--porcelain);border:1px solid var(--oat);border-radius:8px;overflow:hidden}
.product-media{aspect-ratio:4/3;background:var(--linen);position:relative}
.badge{position:absolute;top:12px;left:12px;background:var(--ink);color:var(--snow);
  font-size:11px;letter-spacing:.14em;text-transform:uppercase;padding:6px 10px;border-radius:999px}
.product-body{padding:20px 20px 22px}
.product h3{font-family:"Josefin Sans",sans-serif;font-weight:600;font-size:20px;margin:0 0 6px}
.product-meta{font-size:14px;color:var(--stone);margin:0 0 16px}
.product-row{display:flex;justify-content:space-between;align-items:center}
.price{font-size:18px;font-weight:600}
```

### 3. Buttons — quiet hierarchy
```css
.btn-primary{background:var(--ink);color:var(--snow);border-radius:6px;
  padding:14px 28px;font-size:15px;letter-spacing:.02em;text-decoration:none;display:inline-block}
.btn-primary:hover{background:#000}
.btn-ghost{border:1px solid var(--fog);color:var(--ink);border-radius:6px;
  padding:13px 27px;font-size:15px;text-decoration:none;display:inline-block;background:transparent}
.btn-ghost:hover{border-color:var(--ink)}
.btn-small{background:transparent;border:1px solid var(--fog);border-radius:6px;
  padding:9px 16px;font-size:14px;cursor:pointer;color:var(--ink)}
.btn-small:hover{background:var(--ink);color:var(--snow);border-color:var(--ink)}
/* The single pop: one .btn-pop per page, lingonberry, used for THE primary action only */
.btn-pop{background:var(--lingonberry);color:#fff;border-radius:6px;padding:14px 28px;
  font-size:15px;text-decoration:none;display:inline-block}
```

### 4. Filter pills
```html
<div class="filters" role="tablist" aria-label="Filter products">
  <button class="pill is-active" data-filter="all">All</button>
  <button class="pill" data-filter="seating">Seating</button>
  <button class="pill" data-filter="lighting">Lighting</button>
  <button class="pill" data-filter="tables">Tables & storage</button>
</div>
```
```css
.filters{display:flex;gap:10px;flex-wrap:wrap}
.pill{border:1px solid var(--fog);background:var(--porcelain);border-radius:999px;
  padding:9px 20px;font-size:14px;cursor:pointer;color:var(--stone)}
.pill.is-active,.pill:hover{background:var(--ink);border-color:var(--ink);color:var(--snow)}
```

### 5. Craft tabs (materials / makers / guarantee)
```html
<div class="tabs">
  <div class="tab-list" role="tablist">
    <button class="tab is-active" data-tab="materials" role="tab">Materials</button>
    <button class="tab" data-tab="makers" role="tab">Makers</button>
    <button class="tab" data-tab="guarantee" role="tab">Guarantee</button>
  </div>
  <div class="tab-panel is-active" id="panel-materials" role="tabpanel">…</div>
  <div class="tab-panel" id="panel-makers" role="tabpanel">…</div>
  <div class="tab-panel" id="panel-guarantee" role="tabpanel">…</div>
</div>
```
```css
.tab-list{display:flex;gap:32px;border-bottom:1px solid var(--oat)}
.tab{background:none;border:0;padding:14px 2px;font-size:15px;color:var(--stone);
  cursor:pointer;border-bottom:2px solid transparent;margin-bottom:-1px;letter-spacing:.02em}
.tab.is-active{color:var(--ink);border-bottom-color:var(--ink);font-weight:600}
.tab-panel{display:none;padding:32px 0}
.tab-panel.is-active{display:block;animation:fadeUp .25s ease-out}
@keyframes fadeUp{from{opacity:0;transform:translateY(8px)}to{opacity:1;transform:none}}
```

### 6. FAQ accordion (thin rules, generous air)
```html
<div class="accordion">
  <div class="acc-item">
    <button class="acc-head" aria-expanded="false">
      <span>How do I care for oiled oak?</span>
      <span class="acc-icon" aria-hidden="true">+</span>
    </button>
    <div class="acc-body"><p>Wipe with a dry cloth…</p></div>
  </div>
</div>
```
```css
.acc-item{border-bottom:1px solid var(--oat)}
.acc-head{width:100%;display:flex;justify-content:space-between;align-items:center;
  background:none;border:0;padding:24px 0;font-size:17px;cursor:pointer;color:var(--ink);text-align:left}
.acc-icon{font-size:22px;color:var(--stone);transition:transform .2s ease-out;font-weight:300}
.acc-head[aria-expanded="true"] .acc-icon{transform:rotate(45deg)}
.acc-body{max-height:0;overflow:hidden;transition:max-height .25s ease-out}
.acc-body p{margin:0 0 24px;color:var(--stone);line-height:1.6;max-width:62ch}
```

## Motion
Scandinavian design defines no signature motion language — movement is quiet and functional: 150–250 ms `ease-out` fades and 8 px rises, accordion `max-height` ease, nothing bouncy or springy. Honor `prefers-reduced-motion` by disabling transitions. One line, because there is genuinely nothing more. 🟡

## Do / Don't
- **Do** keep the page white-dominant with one restrained pop accent (lingonberry red *or* dusty blue) per composition. **Don't** stack multiple saturated accents — that reads as Memphis, not Nordic.
- **Do** left-align heroes and editorial blocks; let whitespace frame the content. **Don't** default to a centered hero with a pill button — the template bans it for a reason.
- **Do** name materials and makers on product cards ("Solid oak · Wool bouclé · Maja Lindqvist"). **Don't** hide craft behind "premium quality" adjectives.
- **Do** use black as graphic punctuation (thin rules, micro-labels, small badges). **Don't** fill large areas with black or deep charcoal — a dark moody page is japandi.
- **Do** let one handwritten or script touch add warmth (a signature, a "hej!"). **Don't** set body copy or UI labels in script.
- **Do** photograph/draw products in soft, even daylight on pale grounds with visible wood grain. **Don't** use dramatic side-lighting, vignettes, or glossy reflections.
- **Do** write prices plainly next to honest specs. **Don't** use fake urgency ("only 2 left!", countdown timers) — it violates democratic design.
- **Do** keep corners small (4–8 px) and shadows diffuse like daylight. **Don't** use hard offset shadows or fully-rounded blobby cards.

## Copy voice
Plain, warm, confident — the knowledgeable friend, never the salesperson. Short sentences. Concrete nouns (oak, wool, linen, light). Quiet pride in craft, zero hype. Mentions of seasons, light, and home are native; exclamation marks are rare.

- "Solid oak, honest wool, and joinery we're happy to show you."
- "Made to be kept — and repaired, not replaced."
- "Furniture for the long light."
- Newsletter: "The Sunday Light — a short letter on craft and home, once a month. No noise."

## Not this skill
- **japandi** (sibling skill): darker, earthier, wabi-sabi-inflected, low-contrast shadow play. Scandinavian is brighter, airier, white-dominant, with democratic pop-color accents.
- **minimalism** (sibling skill): colder and more reductive; Scandinavian keeps the hygge layer — texture, warmth, and human presence.

## Sources consulted
- The Spruce, "What Is Scandinavian Style?" — neutral palettes, light woods (ash, beech, pine), light, texture, clean-lined furniture: https://www.thespruce.com/what-is-scandinavian-design-4149404
- Livingetc, "4 Scandinavian Color Palettes" — pale woods, muted whites, soft greys, inky blue/sage accents, texture carrying weight: https://www.livingetc.com/ideas/scandinavian-color-palettes
- Resene ColourWise, "Scandinavian style design & colour" — black/white/soft grey base; watery blues, frosted turquoise, produce greens; stronger red, burnt orange, olive accents: https://www.resene.com/pdf/ColourWise/scandinaviandesign.pdf
- KNKX/NPR, "Not Too Much, Not Too Little: Sweden, In A Font" — Sweden Sans, Söderhavet, *lagom* ("not too much, not too little"), humble/easygoing/clean tradition: https://www.knkx.org/2015-02-08/not-too-much-not-too-little-sweden-in-a-font
- Design-history knowledge: Aalto, Wegner, Jacobsen, Mogensen, Kaare Klint, Henningsen lineage; democratic design / IKEA; hygge — standard references, tagged ✅ where uncontroversial.
