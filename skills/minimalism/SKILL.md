---
name: minimalism
description: Radical minimalism for interfaces — extreme reduction, monochrome palettes, one typeface, vast whitespace, hairline rules; the Rams / Pawson lineage. Use when a product should feel inevitable, quiet, and precise.
---

# Radical Minimalism

## Verification legend
- ✅ = documented in the source's own writing (Rams's ten principles; Pawson's *Minimum* / interviews) or confirmed in ≥2 independent sources.
- 🟡 = consistently described across ≥3 independent design sources without a citable primary text.
- ⚠️ = community approximation — a defensible synthesis for this skill, not dogma.

## Purpose
Design interfaces reduced to the point where every remaining element feels
inevitable. Radical minimalism is not empty minimalism: whitespace is composed,
typography does all the talking, and removal is a discipline, not a shortcut.
The lineage is Dieter Rams ("Less, but better"; "Good design is as little
design as possible" ✅) and John Pawson ("The great discipline is continuing
to reduce until you can't improve a design by further subtraction" ✅; author
of *Minimum* ✅). Pawson's framing is the operating definition: minimalism is
"less a style than a method, an ethics of making grounded in care and
precision" ✅ (Designarcus / ArchDaily interviews).

## Principles

1. **Subtract until further subtraction would weaken it.** Reduction is the
   design process, not a filter applied at the end. Pawson's discipline ✅:
   keep removing elements until removing one more would make the design worse.
   If you can delete something and nothing is lost, it was never load-bearing.
2. **Less, but better.** Rams's formulation ✅. Fewer elements, each executed
   to a higher standard. One button with perfect type, spacing, and behavior
   beats three "nice" buttons.
3. **Unobtrusive and honest.** Two of Rams's ten principles ✅: the interface
   should not call attention to itself; it should express what it is, never
   promise more than it delivers. No decorative chrome, no "delight" that
   exists to be noticed.
4. **Whitespace is a material.** In Pawson's plain space, emptiness is "a vital
   component of design" 🟡. Treat the void as the primary element: composition
   happens in the space around things, not in the things.
5. **One voice.** One typeface, one or two weights, one color role per surface.
   Restriction is what makes the remaining choices feel considered rather than
   default 🟡.
6. **Thorough down to the last detail.** Rams ✅. In a reduced interface every
   surviving detail is under a magnifying glass: alignment, hairline weights,
   and copy must be exact, because there is nothing else to look at.

## Color
Monochrome or near-monochrome. Color appears only as structure (rules,
borders) or as a single functional signal — never as decoration.

| Token | Value | Role |
|---|---|---|
| `--paper` | `#FAFAF8` ⚠️ | Primary background. Warm-white; never pure `#FFFFFF` on large areas (it glares). |
| `--ink` | `#161513` ⚠️ | Primary text. Warm near-black; softer than `#000` 🟡 (pure black on white is a known eye-strain anti-pattern). |
| `--faint` | `#8A877F` ⚠️ | Secondary text, captions, metadata. Must still pass 4.5:1 on `--paper` for body text — use only for large or non-essential text if contrast is borderline. |
| `--hairline` | `#E2E0D9` ⚠️ | 1px rules, dividers, borders. Barely there. |
| `--wash` | `#F1EFEA` ⚠️ | Subtle surface for inset areas; the only "card" allowed, and only when the content is genuinely separate. |
| `--signal` | `#1A1A1A` ⚠️ | The single functional accent, if any: same hue family as ink, used at most once per view (e.g. the one primary action, or one status mark). If a true color is required (error/success), use muted, desaturated tones — never saturated brand color. |

Rules: never gradients, never shadows to fake elevation (use a hairline),
never color-coding more than one thing per screen, never pure black on pure
white. Dark mode = invert the pair (`--paper`/`--ink` swap), nothing else changes.

## Typography
One typeface for everything. The movement's canon is the neutral grotesque:
Helvetica / Neue Haas Grotesk historically ✅ (Rams-era Braun, Swiss-adjacent
minimalism), with system sans (`-apple-system`, Inter alternatives) as the
pragmatic modern default 🟡. No display face, no serif for "warmth" — warmth
comes from spacing.

- **Family:** one grotesque, e.g. `"Helvetica Neue", Helvetica, -apple-system, "Segoe UI", Arial, sans-serif` ⚠️
- **Weights:** 400 for everything; 500 reserved for the wordmark or the single
  most important word on a page. Never 700. 🟡
- **Scale (ratio ~1.333):** `13 / 16 / 21 / 28 / 37 / 50 / 67 / 89` ⚠️.
  Body at 16–17px, line-height 1.6. Display type is set tight (line-height
  1.05–1.15) and tracked slightly negative (`-0.02em`).
- **Measure:** body copy 55–65 characters ⚠️; display lines broken by hand,
  never orphaned by accident.
- **Case:** sentence case, always. All-caps only for micro-labels at 11–13px
  with `0.08em` letter-spacing ⚠️.
- Type does the work that decoration would: size contrast and whitespace carry
  the hierarchy — there are no colored labels, badges, or bold rainbow headers.

## Layout & spacing
- **Grid:** 12 columns exist to be ignored gracefully — most views are a single
  centered column, `max-width: 1120px` ⚠️, with content measure capped far
  narrower for text.
- **Spacing scale:** `8 / 16 / 24 / 40 / 64 / 96 / 160 / 240` ⚠️. Sections are
  separated by 160–240px of air, not by rules or background changes. Vertical
  rhythm is the layout system.
- **Radius:** `0`. Corners are square; a hairline border is the only allowed
  container treatment ⚠️. (Pragmatic exception: native-feeling controls such as
  a toggle may use the platform's capsule — but only if the whole product does.)
- **Borders:** exactly `1px solid var(--hairline)`. Hairlines divide; they never
  decorate.
- **Shadows:** none, ever. Elevation is expressed with a rule or with space.
- **Density:** if a screen looks "full," it is wrong. The target is one idea
  per viewport-height, with the next idea a full scroll away 🟡.

## Components
All components copy-pasteable. Tokens assumed from the Color table above.

### 1. Hairline rule
The fundamental structural element. Divides sections, frames the footer,
underlines the nav.
```html
<hr class="rule">
```
```css
.rule {
  border: 0;
  border-top: 1px solid var(--hairline);
  margin: 0;
}
```

### 2. Minimal nav
Wordmark left, few text links, one quiet action right. No background, no blur,
no shadow — it sits on the paper until scroll, then gains only a hairline.
```html
<header class="nav">
  <a class="wordmark" href="#">MONO</a>
  <nav class="nav-links">
    <a href="#">Object</a>
    <a href="#">Ethos</a>
    <a href="#">Stockists</a>
  </nav>
  <button class="nav-action" id="bag-button">Bag (0)</button>
</header>
```
```css
.nav {
  display: flex; align-items: baseline; justify-content: space-between;
  padding: 24px 40px;
  border-bottom: 1px solid transparent;
  font-size: 14px;
}
.nav.scrolled { border-bottom-color: var(--hairline); }
.wordmark { font-weight: 500; letter-spacing: 0.12em; text-decoration: none; color: var(--ink); }
.nav-links { display: flex; gap: 32px; }
.nav-links a, .nav-action {
  color: var(--ink); text-decoration: none; background: none; border: 0;
  cursor: pointer; font: inherit; padding: 0;
}
.nav-links a:hover, .nav-action:hover { color: var(--faint); }
```

### 3. Quiet primary button
One rectangle, hairline border, no fill, no radius, no shadow. The fill —
solid ink — is the hover state, and it is the loudest thing on the page.
```html
<button class="btn">Add to bag</button>
```
```css
.btn {
  font: inherit; font-size: 15px;
  color: var(--ink); background: transparent;
  border: 1px solid var(--ink);
  padding: 14px 40px; border-radius: 0; cursor: pointer;
  transition: background-color 200ms ease-out, color 200ms ease-out;
}
.btn:hover { background: var(--ink); color: var(--paper); }
.btn:active { opacity: 0.85; }
```

### 4. Text button
For secondary actions: an underlined word. No box at all.
```html
<button class="text-btn">Read the ethos</button>
```
```css
.text-btn {
  font: inherit; color: var(--ink); background: none; border: 0;
  padding: 0; cursor: pointer; text-decoration: underline;
  text-underline-offset: 4px; text-decoration-color: var(--hairline);
  transition: text-decoration-color 200ms ease-out;
}
.text-btn:hover { text-decoration-color: var(--ink); }
```

### 5. Details accordion
The only disclosure pattern. A hairline top border, a row of text, a `+`/`−`
mark. One open at a time; content fades in, nothing slides.
```html
<div class="detail">
  <button class="detail-head" id="detail-btn-1" aria-expanded="false" aria-controls="detail-panel-1">
    <span>Materials</span><span class="detail-mark" aria-hidden="true">+</span>
  </button>
  <div class="detail-panel" id="detail-panel-1" hidden>
    <p>Glazed stoneware. Fired once, glazed inside and out.</p>
  </div>
</div>
```
```css
.detail { border-top: 1px solid var(--hairline); }
.detail-head {
  width: 100%; display: flex; justify-content: space-between; align-items: baseline;
  background: none; border: 0; padding: 20px 0; cursor: pointer;
  font: inherit; font-size: 15px; color: var(--ink);
}
.detail-panel p { margin: 0 0 24px; color: var(--faint); font-size: 15px; line-height: 1.6; max-width: 60ch; }
```
```js
const btn = document.getElementById('detail-btn-1');
const panel = document.getElementById('detail-panel-1');
btn.addEventListener('click', () => {
  const open = btn.getAttribute('aria-expanded') === 'true';
  btn.setAttribute('aria-expanded', String(!open));
  panel.hidden = open;
  btn.querySelector('.detail-mark').textContent = open ? '+' : '−';
});
```

### 6. Hairline input
No box, no label chip — a line with a placeholder. The border darkens on focus.
```html
<label class="field">
  <span class="field-label">Email for restock notices</span>
  <input class="field-input" type="email" id="notify-email" placeholder="you@example.com">
</label>
<p class="field-msg" id="notify-msg" role="status"></p>
```
```css
.field { display: block; max-width: 360px; }
.field-label { display: block; font-size: 13px; color: var(--faint); margin-bottom: 8px; }
.field-input {
  width: 100%; font: inherit; font-size: 16px; color: var(--ink);
  background: transparent; border: 0; border-bottom: 1px solid var(--hairline);
  border-radius: 0; padding: 8px 0; outline: none;
}
.field-input:focus { border-bottom-color: var(--ink); }
.field-msg { font-size: 13px; color: var(--faint); min-height: 20px; }
```

### 7. Quiet toggle
A single binary control: hairline track, ink knob. No color change on state —
position alone signals it.
```html
<button class="toggle" id="theme-toggle" role="switch" aria-checked="false" aria-label="Dark mode">
  <span class="toggle-knob"></span>
</button>
```
```css
.toggle {
  width: 44px; height: 24px; border: 1px solid var(--ink); border-radius: 999px;
  background: transparent; cursor: pointer; padding: 0; position: relative;
}
.toggle-knob {
  position: absolute; top: 2px; left: 2px; width: 18px; height: 18px;
  border-radius: 50%; background: var(--ink);
  transition: transform 200ms ease-out;
}
.toggle[aria-checked="true"] .toggle-knob { transform: translateX(20px); }
```

### 8. Single product block
The whole product page, reduced: object, name, one sentence, price, one action.
Whitespace does the selling.
```html
<section class="product">
  <p class="product-index">01</p>
  <h1 class="product-name">Object 01 — Carafe</h1>
  <p class="product-line">One litre of glazed stoneware. One colour. Made to be used daily and kept for decades.</p>
  <p class="product-price">€120</p>
  <button class="btn" id="add-to-bag">Add to bag</button>
</section>
```
```css
.product { padding: 160px 40px; max-width: 1120px; margin: 0 auto; }
.product-index { font-size: 13px; color: var(--faint); letter-spacing: 0.08em; margin: 0 0 24px; }
.product-name { font-size: clamp(37px, 6vw, 67px); font-weight: 400; letter-spacing: -0.02em; line-height: 1.05; margin: 0 0 32px; }
.product-line { font-size: 17px; line-height: 1.6; color: var(--faint); max-width: 52ch; margin: 0 0 40px; }
.product-price { font-size: 17px; margin: 0 0 48px; }
```

### 9. Footer bar
One hairline, one line of small text, links separated by space — never by
pipes or bullets.
```html
<footer class="footer">
  <hr class="rule">
  <div class="footer-row">
    <span>© 2026 MONO</span>
    <nav><a href="#">Contact</a><a href="#">Shipping</a><a href="#">Returns</a></nav>
  </div>
</footer>
```
```css
.footer-row {
  display: flex; justify-content: space-between; align-items: baseline;
  padding: 32px 40px 48px; font-size: 13px; color: var(--faint);
}
.footer-row nav { display: flex; gap: 24px; }
.footer-row a { color: var(--faint); text-decoration: none; }
.footer-row a:hover { color: var(--ink); }
```

## Motion
Minimalism has barely a motion language, and that is the point: **almost
nothing moves** 🟡. What does move is slow and mechanical:
- Opacity fades and 1px color transitions only; duration `150–250ms`,
  `ease-out`. No springs, no bounce, no parallax, no scroll-jacking.
- Nothing animates on scroll into view — content is simply there. (Entrance
  animations are decoration announcing themselves; see Don'ts.)
- `prefers-reduced-motion`: with so little motion, compliance is trivial —
  keep the instant state changes, drop the 200ms fades.
- One line: if you are reaching for a keyframe, you have left the style.

## Do / Don't

- **Do** let a page be 80% empty space. **Don't** fill the void with a
  "subtle" background pattern or texture to make it feel designed — the void
  is the design.
- **Do** use one typeface at 400 with size contrast for hierarchy. **Don't**
  introduce a second font "for the headings" or bold key words for emphasis —
  emphasis comes from position and space.
- **Do** divide with a single 1px hairline. **Don't** use cards, shadows, or
  background tints to group content — if it needs a box to be understood, the
  copy is unclear.
- **Do** write one honest sentence where others write a paragraph. **Don't**
  write marketing superlatives ("revolutionary," "world's best") — the style's
  honesty principle forbids them.
- **Do** give the single primary action the only filled/hover state on the
  page. **Don't** add secondary buttons, badges, star ratings, or trust seals
  beside it — one action, one decision.
- **Do** keep the palette to ink, paper, faint, and hairline. **Don't** add an
  accent color "to make the CTA pop" — in this style, restraint *is* the pop.
- **Do** left-align almost everything; ragged right edges are part of the calm.
  **Don't** center large blocks of text — centered paragraphs read as posters,
  not interfaces.

## Copy voice
Plain, declarative, short. Present tense. No adjectives that sell; adjectives
that specify. Numbers instead of praise ("1 litre", "fired once"). The voice
assumes the reader is intelligent and in no hurry.

Example strings:
- "One object. Nothing else."
- "Made to be used daily and kept for decades."
- "If it does not need to be here, it is not here."

## Sources
- Dieter Rams, "Ten principles of good design" (documented principle list; "Less but better", "as little design as possible"): https://www.vitsoe.com/gb/about/good-design
- John Pawson on calm, simple spaces — "continuing to reduce until you can't improve a design by further subtraction" (ArchDaily, 2019): https://www.archdaily.com/918121/john-pawson-on-making-calm-simple-spaces/
- John Pawson, *Minimum* (Phaidon) — the movement's visual canon.
- "Japanese Minimalism: Negative space as content… hairline borders, slow opacity transitions" (frontend-design aesthetic survey, cross-referenced): https://github.com/danielnoamtuby/claude-skills/blob/HEAD/frontend-design/SKILL.md
