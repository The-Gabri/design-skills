---
name: claude-anthropic
description: Anthropic's Claude warm-paper editorial aesthetic — cream canvas, ink text, coral accent, serif display — for calm, literary AI product and marketing pages.
---

# Claude / Anthropic

The look of Anthropic's Claude (anthropic.com, claude.ai): the warmest,
most editorial interface in the AI category. It reads like a literary
publication, not a SaaS marketing page — warm cream paper, ink-black type,
a single terracotta-coral accent, and a refined serif that speaks at
reading pace.

## Principles

1. **Warmth is the brand.** A tinted cream canvas (`#faf9f5`) instead of
   cool gray-white is the single most defining choice — it positions the
   product against OpenAI's cool slate, Google's saturated blue, and
   Microsoft's corporate cyan.
2. **One accent, used deliberately.** Coral appears sparingly on buttons
   and generously on occasional full-bleed callout cards. Never cyan or
   blue — the warm accent is the counter-positioning.
3. **Literary, not technical.** Slab-serif display headlines at weight 400
   with negative letter-spacing pair with a humanist sans body. Copy reads
   like an essay; sentence case everywhere, never shouted uppercase.
4. **Calm by default, expressive on action.** Color means something
   (status, working state) rather than decorating. Lots of neutral
   surface; small bursts of coral.
5. **Generous whitespace, soft geometry.** Wide measure, large section
   gaps, gentle radii (8–16px), hairline warm borders instead of shadows
   or glow.
6. **The cream–dark rhythm.** Marketing pages alternate the warm canvas
   with dark product surfaces (code editors, model tables, pre-footer
   CTAs). The contrast is the page's pacing.

## Color

| Token | Hex | Role | Legend |
|---|---|---|---|
| Canvas | `#faf9f5` | Warm cream page background — the brand's defining surface | 🟡 |
| Surface | `#ffffff` | Cards, message bubbles, chat input | 🟡 |
| Surface warm | `#f5f2ec` | Slightly darker cream, secondary panels | 🟡 |
| Border | `#e8e4dd` | Warm hairline borders and dividers | 🟡 |
| Border subtle | `#f0ede7` | Very subtle separators | 🟡 |
| Ink | `#141413` | Primary text — warm near-black, never pure black | 🟡 |
| Ink secondary | `#5c5952` | Warm gray body copy | 🟡 |
| Ink muted | `#9e9b95` | Timestamps, metadata, placeholders | 🟡 |
| Coral | `#d97757` | **Claude coral** — the signature accent: primary CTAs, brand mark | ✅ |
| Coral hover | `#c15f3c` | Darker coral for hover/active states | 🟡 |
| Coral wash | `#faf0eb` | Coral-tinted highlight backgrounds | 🟡 |
| Dark surface | `#1f1e1c` | Dark product surfaces: code blocks, model tables, footer | ⚠️ |
| Dark ink | `#faf9f5` | Text on dark surfaces | 🟡 |

Legend: ✅ literal fill in the Claude SVG brand assets ·
🟡 cross-referenced across documented teardowns ·
⚠️ community approximation.

Notes: Claude coral `#d97757` is the literal fill of the Claude starburst
mark in the official brand assets; teardowns also cite `#cc785c` and
`#d97559` for web usage — all the same warm terracotta family. Ink is
always warm, never cold blue-black.

## Typography

- **Display serif:** Copernicus / Tiempos Headline (⚠️ proprietary,
  Anthropic's documented headline face). Closest free substitutes:
  **Source Serif 4** or **Newsreader** (optical size, 400 weight).
- **Body sans:** Styrene / Anthropic Sans (⚠️ proprietary). Closest free
  substitutes: **Inter** or **Source Sans 3** at 400.
- **Display rules:** weight 400 (not bold), negative letter-spacing
  (~-0.02em to -0.04em), large sizes (clamp 2.5–4.5rem), short lines
  (1.05–1.15). The serif carries the voice; never set headlines in the
  sans.
- **Body rules:** 17–19px, line-height 1.6–1.7, ink secondary for
  paragraphs. Comfortable measure: 60–70ch.
- **Mono** reserved strictly for code, terminals, and IDs — not for
  labels or chrome.
- **Eyebrow labels:** sentence case or small serif italic, never tracked
  ALL-CAPS.

## Layout & spacing

- **Base spacing:** 8px grid; section gaps generous (96–160px on desktop,
  64px mobile).
- **Measure:** content column ~720px for prose, ~1120–1200px max for
  marketing sections. Asymmetric, editorial composition — not centered
  card grids.
- **Radii:** 8–12px cards, 16–20px chat bubbles and media, pill only for
  the chat input and small tags.
- **Borders:** 1px warm hairlines (`#e8e4dd`); depth comes from border
  contrast, not shadows. No drop shadows on light surfaces.
- **Chat UI:** AI responses sit directly on the canvas (no bubble);
  human messages appear as white bubbles with a hairline border.
- **Dark product panels:** code editors and comparison tables render on
  the dark surface with generous padding — the cream-to-dark switch is
  the page's chapter break.

## Components

Copy-pasteable HTML/CSS. Base context: `body { background:#faf9f5;
color:#141413; font-family:"Source Serif 4",Georgia,serif; }` — body copy
switches to sans via `.sans { font-family:Inter,system-ui,sans-serif; }`.

**1. Starburst brand mark** (inline SVG, coral fill — the literal logo
color)

```html
<svg width="28" height="28" viewBox="0 0 24 24" aria-hidden="true">
  <path fill="#d97757" d="M12 0l1.9 6.9L20.5 4l-2.9 6.6 6.6-2.9L21.3 14l6.7 1.9-6.7 1.9 2.9 6.6-6.6-2.9L20.5 28l-6.6-2.9L12 32l-1.9-6.9L3.5 28l2.9-6.6-6.6 2.9L2.7 17.6-4 15.7 2.7 13.8-.2 7.2l6.6 2.9L3.5 3.5l6.6 2.9z"/>
</svg>
```

**2. Nav (quiet, left mark + right links)**

```html
<header class="cl-nav">
  <a class="cl-brand" href="#"><svg width="24" height="24" viewBox="0 0 24 24"><path fill="#d97757" d="M12 2l2.1 7.2 6.9-3.2-3.2 6.9L25 15l-7.2 2.1 3.2 6.9-6.9-3.2L12 28l-2.1-7.2-6.9 3.2 3.2-6.9L-1 15l7.2-2.1-3.2-6.9 6.9 3.2z" transform="translate(-2 -2) scale(.9)"/></svg><span>Fieldnote</span></a>
  <nav><a href="#">Research</a><a href="#">Products</a><a href="#">Pricing</a></nav>
  <a class="cl-btn" href="#">Try for free</a>
</header>
<style>
.cl-nav{display:flex;align-items:center;gap:32px;padding:20px 32px;
border-bottom:1px solid #f0ede7}
.cl-brand{display:flex;align-items:center;gap:10px;font:500 18px "Source Serif 4",Georgia,serif;
color:#141413;text-decoration:none}
.cl-nav nav{display:flex;gap:24px;margin-left:auto}
.cl-nav nav a{font:400 14.5px Inter,system-ui,sans-serif;color:#5c5952;text-decoration:none}
.cl-nav nav a:hover{color:#141413}
</style>
```

**3. Primary button (coral)**

```html
<a class="cl-btn" href="#">Start writing with Fieldnote</a>
<style>
.cl-btn{display:inline-flex;align-items:center;background:#d97757;color:#fff;
font:500 15px Inter,system-ui,sans-serif;padding:12px 24px;border-radius:10px;
text-decoration:none;transition:background .2s ease;border:0}
.cl-btn:hover{background:#c15f3c}
</style>
```

**4. Secondary button (outline on cream)**

```html
<a class="cl-btn2" href="#">Read the research</a>
<style>
.cl-btn2{display:inline-flex;align-items:center;background:transparent;
color:#141413;font:500 15px Inter,system-ui,sans-serif;padding:11px 23px;
border-radius:10px;border:1px solid #d8d2c6;text-decoration:none;
transition:border-color .2s ease,background .2s ease}
.cl-btn2:hover{border-color:#9e9b95;background:#fff}
</style>
```

**5. Editorial hero**

```html
<section class="cl-hero">
  <p class="cl-kicker">Fieldnote — an AI writing companion</p>
  <h1>An assistant that thinks<br>before it speaks.</h1>
  <p class="cl-lede">Fieldnote reads your drafts the way a careful editor
  would — slowly, charitably, and with an eye for what you meant to say.</p>
  <div class="cl-cta"><a class="cl-btn" href="#">Start writing</a><a class="cl-btn2" href="#">See how it works</a></div>
</section>
<style>
.cl-hero{max-width:1120px;margin:0 auto;padding:120px 32px 96px}
.cl-kicker{font:italic 400 17px "Source Serif 4",Georgia,serif;color:#d97757;margin:0 0 20px}
.cl-hero h1{font:400 clamp(2.6rem,5.5vw,4.4rem)/1.08 "Source Serif 4",Georgia,serif;
letter-spacing:-.025em;margin:0 0 24px;max-width:14ch}
.cl-lede{font:400 19px/1.65 Inter,system-ui,sans-serif;color:#5c5952;
max-width:38ch;margin:0 0 36px}
.cl-cta{display:flex;gap:14px;flex-wrap:wrap}
</style>
```

**6. Chat UI mock** (AI response on bare canvas, human message as white
bubble)

```html
<div class="cl-chat">
  <div class="msg human">Can you make this paragraph gentler?</div>
  <div class="msg ai">
    <svg width="18" height="18" viewBox="0 0 24 24"><path fill="#d97757" d="M12 2l2.1 7.2 6.9-3.2-3.2 6.9L25 15l-7.2 2.1 3.2 6.9-6.9-3.2L12 28l-2.1-7.2-6.9 3.2 3.2-6.9L-1 15l7.2-2.1-3.2-6.9 6.9 3.2z" transform="translate(-2 -2) scale(.9)"/></svg>
    <p>Here's a softer version — I kept your meaning intact and lowered the
    temperature of the second sentence.</p>
  </div>
  <div class="cl-input"><input placeholder="Write to Fieldnote…" /></div>
</div>
<style>
.cl-chat{max-width:680px;margin:0 auto;background:#fff;border:1px solid #e8e4dd;
border-radius:20px;padding:28px;display:flex;flex-direction:column;gap:20px}
.msg{font:400 16px/1.6 Inter,system-ui,sans-serif}
.msg.human{align-self:flex-end;background:#fff;border:1px solid #e8e4dd;
border-radius:16px 16px 4px 16px;padding:12px 18px;max-width:75%}
.msg.ai{display:flex;gap:12px;align-items:flex-start;max-width:92%}
.msg.ai p{margin:0;color:#141413}
.cl-input{border:1px solid #e8e4dd;border-radius:999px;padding:6px 6px 6px 22px;
display:flex;background:#faf9f5}
.cl-input input{flex:1;border:0;background:transparent;outline:none;
font:400 15px Inter,system-ui,sans-serif;color:#141413}
.cl-input input::placeholder{color:#9e9b95}
</style>
```

**7. Feature block (editorial, not a card grid)**

```html
<div class="cl-feat">
  <h3>Reads like an editor, not a search box</h3>
  <p>Fieldnote holds your whole draft in mind — tone, structure, the
  argument you were building — and responds to what you meant, not just
  what you typed.</p>
</div>
<style>
.cl-feat{max-width:560px;padding:28px 0;border-top:1px solid #e8e4dd}
.cl-feat h3{font:400 26px/1.25 "Source Serif 4",Georgia,serif;
letter-spacing:-.015em;margin:0 0 12px}
.cl-feat p{font:400 16.5px/1.65 Inter,system-ui,sans-serif;color:#5c5952;margin:0}
</style>
```

**8. Pull quote**

```html
<blockquote class="cl-quote">
  <p>“The first writing tool that feels like it read the book, not the
  summary.”</p>
  <cite>Mara Ellison — novelist</cite>
</blockquote>
<style>
.cl-quote{max-width:760px;margin:0 auto;text-align:center;padding:48px 32px}
.cl-quote p{font:italic 400 clamp(1.5rem,3vw,2.1rem)/1.4 "Source Serif 4",Georgia,serif;
letter-spacing:-.01em;margin:0 0 18px}
.cl-quote cite{font:400 14px Inter,system-ui,sans-serif;color:#9e9b95;font-style:normal}
</style>
```

**9. Full-bleed coral callout**

```html
<section class="cl-callout">
  <h2>Thoughtful help, on your schedule.</h2>
  <p>Free to start. No credit card, no countdown timers, no dark patterns.</p>
  <a class="cl-btn cl-btn-light" href="#">Start writing</a>
</section>
<style>
.cl-callout{background:#d97757;color:#fff;text-align:center;
padding:96px 32px;margin:96px 0 0}
.cl-callout h2{font:400 clamp(2rem,4vw,3rem)/1.15 "Source Serif 4",Georgia,serif;
letter-spacing:-.02em;margin:0 0 16px}
.cl-callout p{font:400 17px/1.6 Inter,system-ui,sans-serif;opacity:.92;margin:0 0 32px}
.cl-btn-light{background:#fff;color:#141413}
.cl-btn-light:hover{background:#faf9f5}
</style>
```

**10. Footer (ink on canvas, hairline top border)**

```html
<footer class="cl-foot">
  <div class="cl-foot-in">
    <p class="cl-foot-brand">Fieldnote</p>
    <nav><a href="#">Research</a><a href="#">Safety</a><a href="#">Careers</a><a href="#">Privacy</a></nav>
    <p class="cl-foot-note">© 2026 Fieldnote Labs — a fictional demo. Built with care, not urgency.</p>
  </div>
</footer>
<style>
.cl-foot{border-top:1px solid #e8e4dd;padding:48px 32px 56px}
.cl-foot-in{max-width:1120px;margin:0 auto}
.cl-foot-brand{font:400 20px "Source Serif 4",Georgia,serif;margin:0 0 20px}
.cl-foot nav{display:flex;gap:22px;margin-bottom:28px}
.cl-foot nav a{font:400 14px Inter,system-ui,sans-serif;color:#5c5952;text-decoration:none}
.cl-foot-note{font:400 13px Inter,system-ui,sans-serif;color:#9e9b95;margin:0}
</style>
```

## Motion

Claude's marketing surfaces define almost no motion language: page-level
animation is essentially absent. Where motion exists (chat streaming,
subtle hovers), it is gentle and unhurried — 200–400ms `ease-out`,
never springy, never decorative. A single deliberate reveal beats
scattered fade-ups.

## Do / Don't

- **Do** set the whole page on the warm cream canvas `#faf9f5` — **don't**
  use cool gray-white or pure white as the body background.
- **Do** keep headlines in the serif at weight 400 with negative tracking
  — **don't** set them bold, in the sans, or in ALL-CAPS.
- **Do** use coral `#d97757` for exactly one primary action per section —
  **don't** tint body copy, icons, and dividers coral; the accent loses its
  meaning the moment it's everywhere.
- **Do** render AI chat replies on the bare canvas with no bubble —
  **don't** put every message in identical rounded bubbles.
- **Do** separate features with warm hairline rules — **don't** chop
  content into identical shadowed cards with one radius everywhere.
- **Do** reserve monospace for code and IDs only — **don't** use mono for
  labels, eyebrows, or marketing copy.
- **Do** pace long pages with a dark product surface for code or tables —
  **don't** stay cream for the entire page; the contrast is the rhythm.
- **Do** write in sentence case with calm, complete sentences — **don't**
  use urgency tactics ("Act now!", countdowns, hype adjectives).

## Copy voice

Thoughtful, humble, literate. Anthropic's voice explains rather than
sells, admits limits, and treats the reader as an adult. No exclamation
marks, no "revolutionary".

- Hero: "An assistant that thinks before it speaks."
- Feature: "Fieldnote reads your drafts the way a careful editor would —
  slowly, charitably, and with an eye for what you meant to say."
- Honest limit: "It won't always get the tone right. When it doesn't,
  say so — it learns faster from corrections than from praise."
