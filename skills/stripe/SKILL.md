---
name: stripe
description: Recreate Stripe.com's marketing and dashboard aesthetic — blurple brand, animated gradient-mesh hero, light-weight tight type, diagonal sections, code-first storytelling, blue-tinted shadows.
---

# Stripe

Stripe's visual language is the gold standard of fintech design: technical and
luxurious at once, precise and warm. It feels like a financial institution
redesigned by a world-class type foundry — confident enough to whisper.

## Principles

1. **Craft as credibility.** Pixel-perfect type, layered shadows, and physics-smooth animation tell developers "this infrastructure is engineered."
2. **Clarity over cleverness.** One idea per section, short declarative sentences, generous whitespace. Never ornament the message.
3. **Developers are the audience.** Code samples appear before marketing claims; API references sit beside pricing. The product *is* the story.
4. **Optimistic ambition.** Stripe's mission is literally "increase the GDP of the internet." Copy assumes the reader is building something that matters.
5. **Color as brand, not decoration.** Blurple (#635bff) is reserved for actions and interactive highlights; the gradient mesh is a signature moment, not a background everywhere.

## Color

| Token | Hex | Role | Confidence |
|---|---|---|---|
| `blurple` | `#635bff` | Primary CTA, links, interactive accents | ✅ |
| `navy` | `#0a2540` | Headings, dark sections, footer | ✅ |
| `canvas` | `#ffffff` | Page background | ✅ |
| `canvas-soft` | `#f6f9fc` | Alt bands beneath the hero, cool-tinted sections | ✅ |
| `ink-body` | `#425466` | Body text — slate, never pure black | ✅ |
| `ink-mute` | `#50617a` | Captions, table labels, secondary text | 🟡 |
| `hairline` | `#e3e8ee` | 1px card/table borders, cool hairlines | 🟡 |
| `blurple-hover` | `#665efd` | Button hover state | 🟡 |
| `success` | `#15be53` | "Succeeded" badges, positive deltas | 🟡 |
| `error` | `#df1b41` | Form errors, failed payments | ⚠️ |
| `mesh-light-blue` | `#6ec3f4` | Gradient mesh stop | ⚠️ |
| `mesh-blue` | `#3a3aff` | Gradient mesh stop | ⚠️ |
| `mesh-pink` | `#ff61ab` | Gradient mesh stop | ⚠️ |
| `mesh-red` | `#e63946` | Gradient mesh stop | ⚠️ |
| `mesh-orange` | `#ff6118` | Illustration accent stop | 🟡 |

**Gradient mesh.** The hero uses an animated WebGL canvas (Stripe's "minigl")
rendering organic color blobs — not a flat CSS gradient. Recreated stops run
light blue → blue → pink → red (`#6ec3f4 → #3a3aff → #ff61ab → #e63946`),
often skewed **-12°** at the section's diagonal cut. Use this mesh only for the
hero signature moment; Stripe's gradients are the one sanctioned exception to
the purple-blue-gradient ban. CSS static fallback:

```css
background: linear-gradient(100deg, #6ec3f4, #3a3aff 30%, #ff61ab 65%, #e63946);
```

**Shadows.** Multi-layer, blue-tinted elevation — the brand's quiet signature:

```css
box-shadow:
  0 18px 36px -18px rgba(0,0,0,.1),
  0 30px 60px -12px rgba(50,50,93,.25);
```

## Typography

Stripe ships **Söhne** (Klim Type Foundry, proprietary, variable `sohne-var`)
with OpenType `"ss01"` enabled globally. Free substitutes:

- **Headlines/body:** `Inter` at weight **300** with tight tracking
  (`letter-spacing: -0.02em` at display sizes, relaxing downward). Weight 300
  headlines are the signature anti-convention — Stripe whispers instead of
  shouting.
- **Code/data:** `ui-monospace, SFMono-Regular, Menlo, Consolas, monospace`
  (or `SourceCodePro` for closer flavor).
- **Money and counts:** always `font-feature-settings: "tnum"` — tabular
  figures are the quiet signal it's financial infrastructure.

Stack:

```css
font-family: "Inter", -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto,
  Helvetica, Arial, sans-serif;
```

- Display: 56px / weight 300 / `-1.4px` tracking; 48px / 300 / `-0.96px`.
- Headings are deep navy `#0a2540`, never black.
- Body: 17px / 400 / `#425466`, line-height 1.6.

## Layout & spacing

- **Diagonal section rhythm.** Sections cut at slight diagonals (the mesh canvas
  is skewed -12°). Alternate: gradient hero → white content → `#f6f9fc` alt band
  → navy developer band → white → navy footer.
- **Max content width:** ~1080px, generous vertical padding (96–144px between
  major sections).
- **Radius:** conservative — 4–8px cards, pill buttons for CTAs.
- **Composited product mockups.** Faux dashboard UIs rendered at small scale
  inside rounded containers with the blue-tinted multi-layer shadow — a code
  panel, a payments table, and a chart card layered into one composition. This
  composite is the brand's most-photographed visual.
- **8pt spacing grid** on UI surfaces; hairline `1px #e3e8ee` dividers in tables.

## Components

### 1. Gradient mesh hero

```html
<section class="hero">
  <div class="mesh" aria-hidden="true">
    <canvas id="mesh-canvas"></canvas>
  </div>
  <div class="hero-inner">
    <p class="eyebrow">Now in public beta</p>
    <h1>Payments infrastructure<br>for ambitious businesses</h1>
    <p class="lede">Millions of companies use Meridian to accept payments, send payouts, and manage their businesses online.</p>
    <div class="cta-row">
      <a class="btn-primary" href="#">Start now</a>
      <a class="btn-secondary" href="#">Contact sales</a>
    </div>
  </div>
</section>
```

```css
.hero { position: relative; overflow: hidden; padding: 140px 24px 220px; }
.mesh {
  position: absolute; inset: -20% -5% auto; height: 120%;
  transform: skewY(-12deg); transform-origin: top left;
  background: linear-gradient(100deg, #6ec3f4, #3a3aff 30%, #ff61ab 65%, #e63946);
}
.hero-inner { position: relative; max-width: 1080px; margin: 0 auto; color: #0a2540; }
```

Animate the canvas with slow-drifting radial blobs (20–30s loop) behind the
static CSS fallback; the fallback alone must still look Stripe-accurate.

### 2. Blurple pill CTA

```html
<a class="btn-primary" href="#">Start now</a>
```

```css
.btn-primary {
  display: inline-block; padding: 12px 28px; border-radius: 999px;
  background: #635bff; color: #fff; font-weight: 600; font-size: 15px;
  text-decoration: none; transition: background .2s, transform .2s;
}
.btn-primary:hover { background: #665efd; transform: translateY(-1px); }
.btn-secondary {
  display: inline-block; padding: 12px 28px; border-radius: 999px;
  background: #fff; color: #0a2540; font-weight: 600; font-size: 15px;
  text-decoration: none; box-shadow: 0 2px 8px rgba(50,50,93,.15);
}
```

### 3. Code snippet block (dark)

Stripe's code blocks are navy `#0a2540` with syntax-colored text and a copy
button. Put a code sample next to every product claim.

```html
<pre class="code-block"><code><span class="c-kw">const</span> payment = <span class="c-kw">await</span> meridian.payments.<span class="c-fn">create</span>({
  amount: <span class="c-num">2000</span>,
  currency: <span class="c-str">'usd'</span>,
  <span class="c-cmt">// Automatic tax, fraud checks, and retries included</span>
});</code></pre>
```

```css
.code-block {
  background: #0a2540; color: #c4d2e0; border-radius: 8px;
  padding: 24px; font: 13.5px/1.7 ui-monospace, SFMono-Regular, Menlo, Consolas, monospace;
  overflow-x: auto; box-shadow: 0 18px 36px -18px rgba(0,0,0,.25), 0 30px 60px -12px rgba(50,50,93,.35);
}
.c-kw { color: #7aa2ff; } .c-fn { color: #ff61ab; }
.c-str { color: #8ce99a; } .c-num { color: #ffcf5c; } .c-cmt { color: #6b7f93; }
```

### 4. Dashboard table

```html
<table class="payments-table">
  <thead><tr><th>Customer</th><th>Status</th><th class="num">Amount</th><th>Date</th></tr></thead>
  <tbody>
    <tr><td>Acme Corp</td>
        <td><span class="badge success">Succeeded</span></td>
        <td class="num">$2,400.00</td><td>Oct 2</td></tr>
    <tr><td>Bloom Studio</td>
        <td><span class="badge success">Succeeded</span></td>
        <td class="num">$182.50</td><td>Oct 1</td></tr>
    <tr><td>North Labs</td>
        <td><span class="badge failed">Failed</span></td>
        <td class="num">$99.00</td><td>Sep 30</td></tr>
  </tbody>
</table>
```

```css
.payments-table { width: 100%; border-collapse: collapse; font-size: 14px; }
.payments-table th { text-align: left; color: #50617a; font-weight: 500;
  font-size: 12px; text-transform: uppercase; letter-spacing: .06em;
  padding: 10px 12px; border-bottom: 1px solid #e3e8ee; }
.payments-table td { padding: 12px; border-bottom: 1px solid #e3e8ee; color: #0a2540; }
.payments-table .num { text-align: right; font-feature-settings: "tnum"; }
.badge { display: inline-block; padding: 3px 10px; border-radius: 999px;
  font-size: 12px; font-weight: 600; }
.badge.success { background: rgba(21,190,83,.12); color: #0f9d4a; }
.badge.failed { background: rgba(223,27,65,.10); color: #df1b41; }
```

### 5. API language tabs

A tab row (cURL · Node · Python · Ruby) above the code block; active tab is
blurple text with a 2px blurple underline, inactive tabs muted. Swapping tabs
rewrites the code sample — never leave a tab decorative.

### 6. Pricing cards

Three cards on white, hairline borders, 8px radius; the middle (recommended)
card carries a soft blurple tint band or elevated shadow. Each card: plan name
(small caps), big tabular price, short description, feature list with check
marks, pill CTA. Prices always in `tnum`.

### 7. Diagonal divider

```css
.diagonal-band { background: #f6f9fc;
  clip-path: polygon(0 0, 100% 4vw, 100% 100%, 0 calc(100% - 4vw)); }
```

### 8. Logo wall

A single row of customer wordmarks in muted navy at 60% opacity, generous
gutters — social proof as quiet texture, never a carousel.

### 9. Testimonial

Large light-weight pull quote (32px / weight 300 / navy), customer name and
title in 14px muted below, company logo above. One quote per section.

### 10. Footer

White background, 4–6 columns of link groups in 13px `#425466`, small legal row
at the bottom (`© year · Privacy · Terms`). No giant dark footer — Stripe's is
light and quiet.

## Motion

Stripe's signature motion is the **animated gradient mesh**: color blobs drift
on a slow 20–30s loop with ease-in-out pacing, plus a subtle parallax follow of
the cursor (±10px). Cards lift `translateY(-2px)` with the blue-tinted shadow
deepening on hover; buttons darken on hover. Easing is smooth and physical —
nothing bouncy, nothing instant. (Demo-only extras — scroll reveals, animated
stat counters, magnetic CTAs — are presentation polish, not brand canon.)

## Do / Don't

- **Do** put a real code sample next to every product claim. / **Don't** describe an API in prose alone.
- **Do** use weight-300 tight headlines in navy `#0a2540`. / **Don't** use bold black hero text — it reads as a different company.
- **Do** reserve blurple `#635bff` for actions and links. / **Don't** use blurple for body text or decorative shapes.
- **Do** use tabular numerals (`tnum`) for every amount, count, and metric. / **Don't** let money render in proportional figures.
- **Do** cut sections on diagonals with the mesh skewed -12°. / **Don't** stack plain horizontal bands with hard edges.
- **Do** keep radius conservative (4–8px) and shadows blue-tinted. / **Don't** use pill-shaped cards or neutral gray shadows.
- **Do** show one composited dashboard mockup per major feature. / **Don't** use generic stock illustrations or icon grids.
- **Do** write the mesh as animated blobs with a CSS-gradient fallback. / **Don't** ship a flat static gradient and call it the hero.

## Copy voice

Precise, ambitious, developer-literate. Short declarative sentences; the reader
is assumed to be building something important. Never hype words ("revolutionary",
"game-changing"), never exclamation marks in headlines.

- "Payments infrastructure for the internet."
- "Accept payments, send payouts, and manage your business online — with one integration."
- "We handle the complexity of money movement so you can focus on your product."
