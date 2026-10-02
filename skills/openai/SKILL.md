---
name: openai
description: Recreate OpenAI's brand style — restrained research-lab calm: white canvas, near-black ink, hairline borders, Söhne-style quiet typography, index-style research cards, generous whitespace.
---

# OpenAI

OpenAI's visual language is research-paper calm: a near-monochrome system where
restraint *is* the brand. White space does the compositional work, type never
shouts, and the only confident color is the ChatGPT green accent — used rarely,
like a signature. It reads as "we take the work seriously" without a single
decorative element.

## Principles

1. **Restraint as identity.** Hierarchy comes from size and spacing, never from
   weight or color. Weights cap at 600; 700+ feels off-brand. Bold is reserved
   for hero/page headings, and even those often sit at 500–600.
2. **Research calm, not product hype.** Pages read like an index, not a sales
   deck. Copy is measured and precise; superlatives are rationed. Whitespace
   separates sections more often than dividers or color bands do.
3. **Monochrome until it matters.** Text is ink on white; the single accent
   (ChatGPT green) marks actions, active states, and links. One color, used
   sparingly, beats a rainbow.
4. **The grid is invisible.** Content sits on a quiet 12-col grid with very
   wide gutters. Cards often have no visible container — just a hairline or
   nothing at all, letting the index rows breathe.
5. **Type does the branding.** There is almost no decoration — no gradients, no
   shadows, no ornamental icons. The blossom-like mark and the Söhne-flavored
   sans are the entire visual signature.

## Color

| Token | Hex | Role | Confidence |
|---|---|---|---|
| `ink` | `#0d0d0d` | Primary text, headings, brand mark, primary CTA fill | ✅ |
| `ink-soft` | `#1a1a1a` | Secondary headings, CTA hover fill | 🟡 |
| `canvas` | `#ffffff` | Page canvas | ✅ |
| `canvas-soft` | `#fafafa` | Section breaks, footer surface | 🟡 |
| `surface` | `#f7f7f8` | Cards, sidebar, secondary panels, user-message bubbles | 🟡 |
| `surface-deep` | `#ececec` | Disabled bg, divider tint, table stripes | 🟡 |
| `hairline` | `#e5e5e5` | 1px dividers, input borders, card outlines on white | 🟡 |
| `hairline-soft` | `#ededed` | Card outline on white surfaces | ⚠️ |
| `graphite` | `#3c3c3c` | Body text (some contexts) | 🟡 |
| `slate` | `#6e6e80` | Secondary text, captions, metadata | 🟡 |
| `ash` | `#9b9b9b` | Tertiary text, placeholders, disabled labels | ⚠️ |
| `brand-green` | `#10a37f` | The lone accent: ChatGPT accent, links, active states | ✅ |
| `green-deep` | `#0a7a5e` | Hover/pressed state for the accent | 🟡 |
| `green-soft` | `#e8f5f0` | Tonal fills: success badges, highlight callouts | 🟡 |
| `code-dark` | `#1e1e1e` | Dark code block background | 🟡 |
| `ink-invert` | `#0d0d0d` | Dark-mode canvas; `#171717` surface, `#2f2f2f` borders, `#ececec` text, `#19c08e` green | 🟡 |
| `error` | `#ef4146` | Validation, destructive actions | 🟡 |
| `warning` | `#f5a623` | Advisory states | ⚠️ |

Confidence: ✅ documented in OpenAI's brand/type usage or universally agreed
teardown values · 🟡 cross-referenced across multiple independent teardowns of
openai.com/chatgpt · ⚠️ community approximation.

## Typography

- **UI / body / headings:** `Söhne` (Klim Type Foundry, proprietary — the
  longtime OpenAI interface face), increasingly documented alongside **OpenAI
  Sans** (their in-house brand face, ~2025). Fallback stack is the system
  stack: `-apple-system, BlinkMacSystemFont, "Segoe UI", system-ui, sans-serif`.
  Free substitute closest in spirit: **Inter** (documented as the standard
  approximation); DM Sans and Plus Jakarta Sans are rounder alternatives. ✅
- **Editorial display:** `Signifier` (Klim serif) — used *only* for editorial
  display headlines and announcements. The product UI itself is sans-only.
  Free fallback: `Source Serif Pro`, Georgia. 🟡
- **Code:** `Söhne Mono` (Klim); fallback `ui-monospace, "JetBrains Mono",
  Menlo, Consolas, monospace`. 🟡

| Role | Size | Weight | Tracking | Leading |
|---|---|---|---|---|
| Display / hero | 56–80px | 500 | −0.02em | 1.1 |
| H1 | 40–48px | 500–600 | −0.01em | 1.15 |
| H2 | 28–32px | 600 | −0.01em | 1.2 |
| H3 | 20–24px | 600 | 0 | 1.3 |
| Body large (lede) | 18px | 400 | 0 | 1.6 |
| Body | 16px | 400 | 0 | 1.6–1.65 |
| Caption / metadata | 12–14px | 400–500 | 0–0.04em | 1.4 |
| Label / eyebrow (uppercase) | 12px | 500 | 0.04em | 1.3 |
| Code | 14px | 400 | 0 | 1.55 |

Rules: weights cap at 600 for headings and 500 for UI labels — size carries the
hierarchy. Tracking goes negative only on display sizes and returns to zero by
16px. Generative line-height 1.55–1.65 for all reading text.

## Layout & spacing

- **Canvas rhythm:** single-column content max-width ~768px for reading; marketing
  grid max-width ~1200–1400px with very wide gutters (64–96px). Sections are
  separated by 96–160px of whitespace, not by dividers.
- **Spacing scale:** 4 / 8 / 12 / 16 / 24 / 32 / 48 / 64 / 96 / 160px. Radii:
  8px small, 12px cards/CTA, 16px large panels, 9999px pills/chips.
- **Borders:** hairline 1px `#e5e5e5`, used sparingly — whitespace is the
  primary divider. Cards frequently have no border at all (the research index).
- **Shadows:** essentially none. Elevation is conveyed by a hairline border or
  a `#f7f7f8` surface, never by drop shadows.
- **Nav:** full-width, hairline bottom border, logo left, links center-left,
  "Try ChatGPT"-style primary CTA right. Sticky.
- **Footer:** hairline top border, 4–5 columns of quiet text links, then a
  bottom row with the mark and legal links.

## Components

### 1. Nav bar

```html
<nav class="oai-nav">
  <a class="oai-brand" href="#">
    <svg width="24" height="24" viewBox="0 0 48 48" aria-hidden="true">
      <!-- original geometric blossom: six petals around a center -->
      <g fill="none" stroke="#0d0d0d" stroke-width="4.5">
        <path d="M24 4 C30 12 30 22 24 30 C18 22 18 12 24 4 Z"/>
        <path d="M24 4 C30 12 30 22 24 30 C18 22 18 12 24 4 Z" transform="rotate(60 24 24)"/>
        <path d="M24 4 C30 12 30 22 24 30 C18 22 18 12 24 4 Z" transform="rotate(120 24 24)"/>
        <path d="M24 4 C30 12 30 22 24 30 C18 22 18 12 24 4 Z" transform="rotate(180 24 24)"/>
        <path d="M24 4 C30 12 30 22 24 30 C18 22 18 12 24 4 Z" transform="rotate(240 24 24)"/>
        <path d="M24 4 C30 12 30 22 24 30 C18 22 18 12 24 4 Z" transform="rotate(300 24 24)"/>
      </g>
    </svg>
    <span>OpenAI</span>
  </a>
  <div class="oai-links">
    <a href="#">Research</a><a href="#">API</a><a href="#">Company</a>
  </div>
  <a class="oai-btn oai-btn-primary" href="#">Try ChatGPT</a>
</nav>
```

```css
.oai-nav{display:flex;align-items:center;gap:32px;padding:14px 24px;
  border-bottom:1px solid #e5e5e5;background:#fff;position:sticky;top:0;z-index:50}
.oai-brand{display:flex;align-items:center;gap:10px;font-weight:600;font-size:17px;
  color:#0d0d0d;text-decoration:none;margin-right:auto}
.oai-links{display:flex;gap:28px}
.oai-links a{color:#0d0d0d;text-decoration:none;font-size:15px}
.oai-links a:hover{text-decoration:underline}
```

### 2. Buttons

```css
.oai-btn{display:inline-block;padding:10px 20px;border-radius:12px;
  font-size:15px;font-weight:500;text-decoration:none;line-height:1.4}
.oai-btn-primary{background:#0d0d0d;color:#fff}
.oai-btn-primary:hover{background:#1a1a1a}
.oai-btn-secondary{background:#fff;color:#0d0d0d;border:1px solid #e5e5e5}
.oai-btn-secondary:hover{background:#fafafa;border-color:#d4d4d4}
.oai-btn-accent{background:#10a37f;color:#fff}
.oai-btn-accent:hover{background:#0a7a5e}
.oai-chip{display:inline-block;padding:6px 14px;border-radius:9999px;
  background:#fff;border:1px solid #e5e5e5;font-size:14px}
```

### 3. Announcement banner (event strip)

```html
<section class="oai-banner">
  <h2>OpenAI DevDay 2026</h2>
  <p>Join us September 29 at 10 a.m. PT for a first look at what's next in
     ChatGPT, Codex, and tools for building.</p>
  <a href="#">Get a reminder</a>
</section>
```

```css
.oai-banner{max-width:1200px;margin:0 auto;padding:48px 24px}
.oai-banner h2{font-size:40px;font-weight:600;letter-spacing:-0.01em;line-height:1.15;margin:0 0 12px}
.oai-banner p{font-size:18px;line-height:1.6;color:#3c3c3c;max-width:640px}
.oai-banner a{color:#10a37f;font-weight:500;text-decoration:none}
```

### 4. Research index cards (the signature pattern)

Text-first cards grouped under section headings, each with a category eyebrow
and a read-time label — no thumbnails required.

```html
<section class="oai-index">
  <div class="oai-index-head"><h3>Latest research</h3><a href="#">View all</a></div>
  <div class="oai-index-grid">
    <a class="oai-card" href="#">
      <span class="oai-eyebrow">Research</span>
      <span class="oai-read">8 min read</span>
      <h4>Reasoning models learn to use tools in reinforcement learning</h4>
    </a>
  </div>
</section>
```

```css
.oai-index-head{display:flex;justify-content:space-between;align-items:baseline;
  border-top:1px solid #e5e5e5;padding-top:24px;margin-bottom:32px}
.oai-index-head h3{font-size:28px;font-weight:600;letter-spacing:-0.01em;margin:0}
.oai-index-head a{font-size:15px;color:#0d0d0d}
.oai-index-grid{display:grid;grid-template-columns:repeat(3,1fr);gap:48px 32px}
.oai-card{display:block;text-decoration:none;color:#0d0d0d}
.oai-card .oai-eyebrow{display:block;font-size:12px;font-weight:500;
  letter-spacing:.04em;text-transform:uppercase;color:#6e6e80;margin-bottom:4px}
.oai-card .oai-read{display:block;font-size:13px;color:#9b9b9b;margin-bottom:12px}
.oai-card h4{font-size:20px;font-weight:500;line-height:1.3;margin:0}
.oai-card:hover h4{text-decoration:underline}
```

### 5. Hero (chat-style, chatgpt home pattern)

```html
<section class="oai-hero">
  <h1>We are building safe and beneficial artificial general intelligence.</h1>
  <form class="oai-chat">
    <input type="text" placeholder="What can I help with?" aria-label="Ask">
    <button type="submit" aria-label="Send">
      <svg width="20" height="20" viewBox="0 0 20 20"><path d="M10 2v16M2 10h16"
       stroke="currentColor" stroke-width="1.8" stroke-linecap="round"/></svg>
    </button>
  </form>
</section>
```

```css
.oai-hero{max-width:768px;margin:0 auto;padding:120px 24px 80px;text-align:center}
.oai-hero h1{font-size:clamp(32px,4.5vw,56px);font-weight:500;letter-spacing:-0.02em;
  line-height:1.1;margin:0 0 48px}
.oai-chat{display:flex;align-items:center;gap:12px;border:1px solid #e5e5e5;
  border-radius:9999px;padding:10px 10px 10px 28px;background:#fff}
.oai-chat input{flex:1;border:0;outline:0;font-size:16px;background:transparent}
.oai-chat button{width:44px;height:44px;border-radius:50%;border:0;
  background:#0d0d0d;color:#fff;cursor:pointer}
```

### 6. API code block (dark)

```css
.oai-code{position:relative;background:#1e1e1e;color:#ececec;border-radius:12px;
  padding:24px;font-family:ui-monospace,"JetBrains Mono",Menlo,Consolas,monospace;
  font-size:14px;line-height:1.55;overflow-x:auto}
.oai-code .tok-k{color:#c792ea} .oai-code .tok-s{color:#9ecbff} .oai-code .tok-f{color:#79c0ff}
.oai-copy{position:absolute;top:12px;right:12px;background:transparent;border:1px solid #2f2f2f;
  color:#b4b4b4;border-radius:8px;padding:6px 12px;font-size:13px;cursor:pointer}
.oai-copy:hover{background:#2f2f2f;color:#fff}
```

### 7. Footer

```html
<footer class="oai-footer">
  <div class="oai-footer-cols">
    <div><h5>Research</h5><a href="#">Overview</a><a href="#">Index</a><a href="#">Safety</a></div>
    <div><h5>API</h5><a href="#">Docs</a><a href="#">Pricing</a><a href="#">Playground</a></div>
    <div><h5>Company</h5><a href="#">About</a><a href="#">Careers</a><a href="#">News</a></div>
  </div>
  <div class="oai-footer-base">
    <span>OpenAI © 2015–2026</span>
    <div><a href="#">Privacy policy</a><a href="#">Terms of use</a><a href="#">Security</a></div>
  </div>
</footer>
```

```css
.oai-footer{border-top:1px solid #e5e5e5;background:#fafafa;margin-top:120px}
.oai-footer-cols{max-width:1200px;margin:0 auto;padding:64px 24px;display:grid;
  grid-template-columns:repeat(3,1fr);gap:32px}
.oai-footer-cols h5{font-size:13px;font-weight:600;margin:0 0 16px;color:#0d0d0d}
.oai-footer-cols a{display:block;font-size:14px;color:#6e6e80;text-decoration:none;
  margin-bottom:12px}
.oai-footer-base{max-width:1200px;margin:0 auto;padding:24px;display:flex;
  justify-content:space-between;border-top:1px solid #e5e5e5;font-size:13px;color:#6e6e80}
.oai-footer-base a{color:#6e6e80;text-decoration:none;margin-left:24px}
```

### 8. Callout / docs row (warning style)

```css
.oai-callout{border-left:3px solid #f5a623;background:#fffbeb;border-radius:0 8px 8px 0;
  padding:16px 20px;font-size:15px;line-height:1.6}
```

## Motion

OpenAI's marketing site has effectively no motion language: transitions are
instant or near-instant hover states (underline on links, `#fafafa` fills on
buttons). If you add any motion, keep it to `transition: all 150–200ms
ease-out` on hovers. No scroll animations, no parallax, no gradient shifts.

## Do / Don't

- **Do** let whitespace compose the page — 96–160px between sections, 48px
  gutters inside card grids.
- **Don't** add drop shadows or gradient backgrounds; elevation = a hairline
  border or a `#f7f7f8` surface.
- **Do** write category + read-time metadata on index cards ("Research ·
  8 min read") in 12–13px slate/ash text.
- **Don't** use weight 700+ for headings — cap at 600; let size do the work.
- **Do** reserve `#10a37f` green for actions, active states, and the rare
  accent; everything else stays monochrome.
- **Don't** put emojis, colorful icons, or decorative illustrations on the page;
  the blossom mark and type are the brand.
- **Do** use a chat-style pill input as a hero element when the product is
  conversational.
- **Don't** center a pill button under a centered headline *with three colorful
  feature cards* — that's every generic AI landing page, not this brand.

## Copy voice

Measured, precise, institutional. Short declarative sentences. Mission-forward
but never breathless; superlatives are rationed. Numbers and specifics beat
adjectives. Announcements start with "Introducing…" and index items read like
paper titles.

Example strings:

1. "We are conducting research toward safe, broadly beneficial artificial
   general intelligence."
2. "Introducing Meridian-1: our most capable model for agentic coding, now
   available in the API."
3. "Reasoning models show measurable gains on mathematics benchmarks. Read
   the 8-minute summary."
