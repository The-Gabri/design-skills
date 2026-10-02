---
name: solana
description: Solana's gradient green/purple web3 aesthetic — dark canvas, purple→green gradient, stats-heavy developer-marketing pages.
---

# Solana

The look of solana.com and the Solana ecosystem: a near-black canvas lit by
Solana's signature purple-to-green gradient. Marketing reads like a spec
sheet — live-network numbers (TPS, transactions, addresses) are the hero
imagery. It feels less like a crypto brand and more like a performance
report you can build on.

## Principles

1. **Performance is the design.** Headlines are numbers: TPS, total
   transactions, active addresses, trading volume. Stats bands are the
   signature section, not an afterthought.
2. **One gradient, used with intent.** The purple `#9945FF` → green
   `#14F195` gradient is the brand's most recognizable asset — it lives
   in the logo, headlines, buttons, and ambient glows. Everywhere else
   stays neutral so the gradient keeps its punch.
3. **Dark is the only mode.** The canvas is near-black; depth comes from
   soft radial glows (lavender and green), not from stacked cards or
   shadows.
4. **Developer-first marketing.** Code blocks, validators, CLIs, and docs
   links sit on the homepage, not behind a docs subdomain. Copy speaks to
   builders ("Start building", "Read the docs").
5. **Big, plain type.** Massive tight-tracked headlines in plain case
   ("The fastest growing financial platform"), minimal adjectives,
   credibility claimed through scale rather than superlatives.

## Color

Official brand colors from Solana's branding site (via dailycoin.com /
cryptonews.net brand-guide coverage): Solana Purple and Solana Green,
always paired as a gradient. Background tokens cross-referenced from
solana-foundation/solana-com and ecosystem frontends.

| Token | Hex | Role | Legend |
|---|---|---|---|
| Solana Purple | `#9945FF` | Gradient start; logo, CTAs, active accents | ✅ |
| Solana Green | `#14F195` | Gradient end; success, stat highlights | ✅ |
| Brand gradient | `linear-gradient(135deg, #9945FF 0%, #14F195 100%)` | Buttons, headline text, logo, glows | ✅ |
| Gradient mid blue | `#5C7CF5` | Optional 3-stop midpoint (`#9945FF → #5C7CF5 → #14F195`) for wide hero washes, matching token-logo usage | 🟡 |
| Void | `#06070B` | Page background — near-black | 🟡 |
| Panel | `#0D0C11` | Cards and elevated panels | 🟡 |
| Hairline | `rgba(255,255,255,0.08)` | Thin borders, table rules, dividers | ⚠️ |
| Ink | `#F4F4F5` | Primary text, near-white | 🟡 |
| Ink muted | `#A1A1AA` | Secondary text, captions | ⚠️ |
| Lavender glow | `rgba(153,69,255,0.25)` | Ambient radial glow, purple side | ⚠️ |
| Mint glow | `rgba(20,241,149,0.18)` | Ambient radial glow, green side | ⚠️ |

Rules: never use the gradient as a body-text color (use it on headline
fragments and CTAs); on text, use a near-horizontal angle (100°) so the
stops read cleanly left-to-right — buttons, borders, and the logo mark
keep the 135° diagonal; never introduce a second accent color — purple and
green are the only brand colors. Text on solid gradient buttons must be
near-black, not white (the green end is too bright for white text).

## Typography

Solana's site uses a custom display face and a mono-coded docs voice; no
official webfont is published. Closest free substitutes below.

- **Display / headlines:** "Space Grotesk" (Google Fonts) — geometric,
  techy, echoes Solana's custom wordmark. Weight 600–700, size
  `clamp(2.5rem, 6vw, 5rem)`, letter-spacing `-0.03em`, line-height `1.02`.
  Headlines often mix one gradient-filled word/phrase into a white line.
- **Body / UI:** "Inter" (Google Fonts) — neutral grotesk for paragraphs,
  nav, buttons. 400 body, 500 labels, 600 small-caps eyebrows.
- **Stats:** Space Grotesk 700 with tabular figures (`font-variant-numeric:
  tabular-nums`), `clamp(2rem, 4vw, 3.5rem)`.
- **Code:** "JetBrains Mono" or ui-monospace stack, 0.875rem, green-tinted
  comments.
- **Eyebrows:** 0.75rem uppercase, letter-spacing `0.2em`, muted ink —
  e.g. "NETWORK · LIVE".

Legend: typefaces are ⚠️ community substitutes for the site's custom face;
usage rules (huge headlines, plain case, stat typography) are ✅
documented from solana.com.

## Layout & spacing

- **Max container:** 1200px, 24px gutters (16px mobile).
- **Hero:** full-viewport, centered headline, gradient headline fragment,
  dual CTA row, then a stats band. Background: near-black with two large
  radial glows (purple top-left, green bottom-right) — this replaces any
  hero image.
- **Stats band:** 4–5 columns of big numbers with small muted labels
  ("Transactions per second", "Total transactions", "Monthly active
  addresses", "Avg. cost per transaction", "App revenue"); each number
  counts up on scroll into view.
- **Spacing scale:** 24px base; sections 96–160px vertical; cards 24px
  padding; radius 12px cards, 8px buttons, pill for badges.
- **Dividers:** 1px hairline rules rather than spacing alone, especially
  around tables and stat bands.
- **Grid:** 12-col desktop; ecosystem cards 4-up → 2-up → 1-up; table
  scrolls horizontally below 720px.

## Components

### 1. Gradient hero

```html
<section class="hero">
  <div class="glow glow-purple"></div>
  <div class="glow glow-green"></div>
  <p class="eyebrow">Network · Live</p>
  <h1>Blockchains should be <span class="grad">measured in speed,</span> not in promises.</h1>
  <p class="lede">Prism is a high-throughput layer-1 for payments, trading, and consumer apps — built for builders who ship.</p>
  <div class="cta-row">
    <a class="btn btn-gradient" href="#">Start Building</a>
    <a class="btn btn-ghost" href="#">Read the Docs</a>
  </div>
</section>
```

```css
.hero { position: relative; overflow: hidden; text-align: center; padding: 160px 24px 120px; background: #06070B; }
.hero h1 { font: 700 clamp(2.5rem,6vw,5rem)/1.02 "Space Grotesk", sans-serif; letter-spacing: -0.03em; color: #F4F4F5; max-width: 16ch; margin: 0 auto 24px; }
.grad { background: linear-gradient(100deg, #9945FF 0%, #14F195 100%); -webkit-background-clip: text; background-clip: text; color: transparent; }
.glow { position: absolute; width: 60vw; height: 60vw; border-radius: 50%; filter: blur(120px); pointer-events: none; }
.glow-purple { background: rgba(153,69,255,.25); top: -20vw; left: -15vw; }
.glow-green  { background: rgba(20,241,149,.18); bottom: -25vw; right: -15vw; }
```

### 2. Stat counter band

```html
<section class="stats">
  <div class="stat"><span class="stat-num" data-target="71000">0</span><span class="stat-label">Transactions per second</span></div>
  <div class="stat"><span class="stat-num" data-target="410" data-suffix="B">0</span><span class="stat-label">Total transactions</span></div>
  <div class="stat"><span class="stat-num" data-target="96" data-prefix="$">0</span><span class="stat-label">Million monthly active addresses</span></div>
  <div class="stat"><span class="stat-num" data-target="0.00025" data-decimals="5" data-prefix="$">0</span><span class="stat-label">Avg. cost per transaction</span></div>
</section>
```

```css
.stats { display: grid; grid-template-columns: repeat(4, 1fr); gap: 24px; padding: 64px 24px; border-top: 1px solid rgba(255,255,255,.08); border-bottom: 1px solid rgba(255,255,255,.08); max-width: 1200px; margin: 0 auto; }
.stat-num { display: block; font: 700 clamp(2rem,4vw,3.25rem) "Space Grotesk", sans-serif; font-variant-numeric: tabular-nums; color: #F4F4F5; }
.stat-label { font-size: .85rem; color: #A1A1AA; }
```

### 3. Wallet connect button

```html
<button class="btn btn-gradient wallet-btn">
  <svg width="16" height="16" viewBox="0 0 16 16" aria-hidden="true"><path d="M3 1.5 6 1.5 5 4 2 4Z M7 1.5h3L9 4H6Z M11 1.5h3l-1 2.5h-3Z" fill="currentColor" opacity=".95"/></svg>
  Connect Wallet
</button>
```

```css
.btn-gradient { background: linear-gradient(135deg, #9945FF, #14F195); color: #06070B; font-weight: 700; border: 0; border-radius: 8px; padding: 14px 28px; cursor: pointer; display: inline-flex; align-items: center; gap: 10px; }
.btn-gradient:hover { filter: brightness(1.1); transform: translateY(-1px); }
.btn-ghost { border: 1px solid rgba(255,255,255,.2); color: #F4F4F5; border-radius: 8px; padding: 14px 28px; font-weight: 600; background: transparent; }
.btn-ghost:hover { border-color: #14F195; color: #14F195; }
```

### 4. Validator table

```html
<table class="validators">
  <thead><tr><th>Validator</th><th>Commission</th><th>APY</th><th>Skipped slots</th><th>Status</th></tr></thead>
  <tbody>
    <tr><td><span class="id">aurora-1</span></td><td>5%</td><td class="green">7.42%</td><td>0.02%</td><td><span class="dot ok"></span>Active</td></tr>
  </tbody>
</table>
```

```css
.validators { width: 100%; border-collapse: collapse; font-size: .95rem; }
.validators th { text-align: left; font-size: .75rem; text-transform: uppercase; letter-spacing: .12em; color: #A1A1AA; padding: 12px 16px; border-bottom: 1px solid rgba(255,255,255,.08); }
.validators td { padding: 16px; border-bottom: 1px solid rgba(255,255,255,.06); color: #F4F4F5; font-variant-numeric: tabular-nums; }
.validators tr:hover td { background: rgba(153,69,255,.05); }
.green { color: #14F195; }
.dot { display: inline-block; width: 8px; height: 8px; border-radius: 50%; margin-right: 8px; }
.dot.ok { background: #14F195; box-shadow: 0 0 8px #14F195; }
```

### 5. Code block (developer docs feel)

```html
<div class="codeblock">
  <div class="code-tabs"><button class="on">npm</button><button>yarn</button><button>cargo</button><button class="copy">Copy</button></div>
  <pre><code><span class="c"># scaffold a Prism app</span>
$ npm create prism-app@latest my-app
$ cd my-app && npm run dev</code></pre>
</div>
```

```css
.codeblock { background: #0D0C11; border: 1px solid rgba(255,255,255,.08); border-radius: 12px; overflow: hidden; }
.code-tabs { display: flex; border-bottom: 1px solid rgba(255,255,255,.08); }
.code-tabs button { background: none; border: 0; color: #A1A1AA; padding: 12px 20px; font: 600 .85rem "JetBrains Mono", monospace; cursor: pointer; }
.code-tabs button.on { color: #14F195; box-shadow: inset 0 -2px 0 #14F195; }
.codeblock pre { padding: 20px 24px; color: #F4F4F5; font: .9rem/1.7 "JetBrains Mono", monospace; overflow-x: auto; }
.codeblock .c { color: #5b5b66; }
```

### 6. Ecosystem cards

```html
<div class="cards">
  <article class="card"><span class="pill">DeFi</span><h3>Trade at the speed of light</h3><p>Onchain order books settling in 400 ms — market-making without the middlemen.</p><a href="#">Explore DeFi →</a></article>
</div>
```

```css
.cards { display: grid; grid-template-columns: repeat(4, 1fr); gap: 16px; }
.card { background: #0D0C11; border: 1px solid rgba(255,255,255,.08); border-radius: 12px; padding: 24px; }
.card:hover { border-color: rgba(153,69,255,.5); }
.card h3 { font: 600 1.15rem "Space Grotesk", sans-serif; color: #F4F4F5; margin: 12px 0 8px; }
.card p { color: #A1A1AA; font-size: .92rem; }
.card a { color: #14F195; font-weight: 600; font-size: .9rem; text-decoration: none; }
.pill { font-size: .72rem; font-weight: 700; letter-spacing: .14em; text-transform: uppercase; color: #14F195; }
```

### 7. Gradient-border feature card

A card with the gradient as its border (1px via background-clip trick),
used for the single flagship announcement or the main CTA block.

```css
.card-flag { border-radius: 14px; padding: 1px; background: linear-gradient(135deg, #9945FF, #14F195); }
.card-flag > div { border-radius: 13px; background: #06070B; padding: 40px; }
```

### 8. Live network status bar

A thin top banner announcing network health — Solana sites surface uptime
as social proof.

```html
<div class="netbar"><span class="dot ok"></span> Mainnet Beta · 400 ms block time · 0 outages this quarter</div>
```

```css
.netbar { display: flex; align-items: center; justify-content: center; gap: 10px; font-size: .8rem; color: #A1A1AA; background: #0D0C11; border-bottom: 1px solid rgba(255,255,255,.08); padding: 10px; }
```

### 9. Nav with gradient logo mark

```html
<nav class="nav">
  <a class="brand" href="#">
    <svg width="28" height="24" viewBox="0 0 28 24" aria-hidden="true"><defs><linearGradient id="lg" x1="0" y1="0" x2="1" y2="1"><stop offset="0" stop-color="#9945FF"/><stop offset="1" stop-color="#14F195"/></linearGradient></defs><path d="M6 1h9l-3 6H3zM12 9h9l-3 6h-9zM18 17h9l-3 6h-9z" fill="url(#lg)"/></svg>
    PRISM
  </a>
  <div class="links"><a href="#">Developers</a><a href="#">Validators</a><a href="#">Ecosystem</a><a href="#">Docs</a></div>
  <button class="btn btn-gradient">Connect Wallet</button>
</nav>
```

The logo mark is three slanted parallelograms in the brand gradient —
Solana's mark conveys speed and building; a Solana-style brand should use
an equivalent geometric mark, never a copied logo.

## Motion

Signature motion is minimal: stat counters count up over ~1.4s with
easeOutCubic when scrolled into view; section blocks may use a single
subtle fade-up reveal (≤600ms, ≤20px rise, ≤70ms stagger per sibling) —
nothing more; hover states are 150–250ms fades and 1px lifts; ambient
glows may drift very slowly. No scroll-jacking, no parallax heroes, no
multi-stage choreography — speed is the brand, so the page must feel
instant. Honor `prefers-reduced-motion`.

## Do / Don't

- **Do** put live network numbers above the fold — a Solana-style page
  without a stats band is not a Solana-style page.
- **Do** use the exact official hexes `#9945FF` and `#14F195` for the
  gradient; close-enough purples read as generic web3.
- **Do** keep the canvas near-black even in "light" sections — the
  aesthetic has no light mode.
- **Do** write headlines in plain case with one gradient fragment; never
  set a whole paragraph in gradient text.
- **Don't** pair the gradient with a third accent (no blue buttons, no
  orange alerts) — purple and green carry the entire brand.
- **Don't** use Inter/Roboto alone for headlines; the display face is
  geometric and heavy (Space Grotesk-class).
- **Don't** render the wallet button as an outline-only ghost — the
  primary wallet CTA is the solid gradient button with dark text.
- **Don't** fake stats with round numbers like "10,000 TPS" — Solana's
  credibility language is specific figures ("transactions per second"
  with real-ish data); rounded fantasy numbers break the illusion.

## Copy voice (for brand styles)

Solana's voice is terse, fast, and builder-addressed. Verbs over
adjectives. It talks about what the network *does* (settles, scales,
ships), not what it *is*. Numbers do the bragging, so adjectives don't
have to.

- "Built for scale. Ready for the world."
- "Stop waiting on blocks. Start building."
- "65,000 transactions per second. $0.00025 per transaction. One network."

---

*Sources: Solana brand guidelines (official purple `#9945FF` / green
`#14F195`, three-parallelogram mark = speed + building), solana.com
homepage structure and stat-band copy, solana-foundation/solana-com repo
(dark `#0D0C11` panels, radial glows).*
