# Glass in CSS — visual approximation ⚠️

> ⚠️ **EXPLICIT WARNING — read me first:** `backdrop-filter` **is NOT**
> Liquid Glass: it imitates the look (translucent veil + blur) without
> dynamic refraction, without environment sampling, without touch response,
> and without adapting to system settings (Clear/Tinted, Reduce
> Transparency). It's a **visual approximation** for the web, not the real
> material. ⚠️
>
> On the web it only makes sense for **floating functional chrome** (sticky
> nav, bars, modals/sheets, toasts) — the same two-layer rule: no glass in
> the content. ✅/⚠️
>
> Legend: ✅ transferable HIG rule · 🟡 community consensus (≥3 sources)
> · ⚠️ visual approximation not verified as the real material.

## 1. Base recipe: `backdrop-filter: blur() saturate()` ⚠️

Four ingredients consistent across all recipes: 🟡

1. **Frost** — `backdrop-filter: blur()` + `saturate()` (blur alone
   desaturates and the effect "dies"; consensus: `saturate(140–180%)`).
2. **Translucency** — `background` with low alpha (0.08–0.18 in dark,
   0.55–0.7 in light over photo).
3. **Light edge** — 1px hairline brighter than the fill + inset top highlight.
4. **Depth** — diffuse ambient shadow, never hard.

```css
/* WHEN: a sticky nav bar or floating toolbar on an Apple-style website.
   ⚠️ Only the look, not the real material (see warning). */
/* Dark variant (the most used in iOS demos) */
.glass {
  background: rgba(255, 255, 255, 0.12);
  -webkit-backdrop-filter: blur(16px) saturate(160%); /* Safari/iOS first */
  backdrop-filter: blur(16px) saturate(160%);
  border: 1px solid rgba(255, 255, 255, 0.25);
  border-radius: 20px;
  box-shadow:
    0 8px 32px rgba(0, 0, 0, 0.25),          /* ambient shadow */
    inset 0 1px 0 rgba(255, 255, 255, 0.35),  /* top highlight */
    inset 0 -1px 0 rgba(0, 0, 0, 0.12);       /* bottom shading */
}

/* WHEN: light variant over photography. ⚠️ */
.glass-light {
  background: rgba(255, 255, 255, 0.55);
  -webkit-backdrop-filter: blur(20px) saturate(180%);
  backdrop-filter: blur(20px) saturate(180%);
  border: 1px solid rgba(255, 255, 255, 0.5);
  box-shadow:
    0 8px 32px rgba(0, 0, 0, 0.12),
    inset 0 1px 0 rgba(255, 255, 255, 0.6);
}
```

Details: 🟡

- The `-webkit-` prefix is **mandatory** for Safari/iOS, and goes before the
  standard line.
- Glass needs something behind it (photo, gradient, video): over a flat
  color it does nothing.
- Guideline blur ranges: nav bars `blur(8–12px)`; panels
  `blur(16–24px)`; heavy modals `blur(24–40px)`. ⚠️
- Text over glass: measure against the worst background; if contrast
  collapses, raise the fill opacity or add a scrim behind the text; **never
  long paragraphs over glass**. ✅/🟡

### 1.1 regular / clear variants ⚠️

```css
/* WHEN: you want the visual equivalent of .regular — protected legibility:
   more veil, more blur. ⚠️ */
.glass-regular {
  background: color-mix(in srgb, var(--bg) 55%, transparent);
  -webkit-backdrop-filter: blur(20px) saturate(1.8);
  backdrop-filter: blur(20px) saturate(1.8);
}

/* WHEN: the visual equivalent of .clear — only over rich media (photo,
   video). If the background is bright, add the 35% dimming veil.
   (Real HIG quote: "If the content beneath is bright, add a subtle 35%
   darkening layer" ✅; the rest of this snippet is approximation ⚠️.) */
.glass-clear {
  position: relative;
  background: rgba(255, 255, 255, 0.08);
  -webkit-backdrop-filter: blur(12px) saturate(160%);
  backdrop-filter: blur(12px) saturate(160%);
  border-radius: 20px;
  color: #fff;
}
.glass-clear::before {
  /* 35% dimming veil BETWEEN the background and the content */
  content: "";
  position: absolute;
  inset: 0;
  border-radius: inherit;
  background: rgba(0, 0, 0, 0.35);
  pointer-events: none;
}
.glass-clear > * {
  /* The content sits above the veil */
  position: relative;
}
```

Fill props per mode (⚠️): light `--glass-fill: rgba(255,255,255,.55)`,
border `rgba(255,255,255,.5)`; dark `--glass-fill: rgba(20,20,22,.45)`,
border `rgba(255,255,255,.12)`.

## 2. Mandatory fallbacks 🟡

No glass without a fallback: the effect must degrade gracefully or not exist.

```css
/* WHEN: whenever you use .glass-* — guarantees legibility in browsers
   without backdrop-filter and respects users who asked for reduced transparency. 🟡 */

.glass {
  /* Legible base WITHOUT blur: more opaque fill */
  background: rgba(28, 28, 30, 0.82);
  border: 1px solid rgba(255, 255, 255, 0.25);
  border-radius: 20px;
}

/* 1) Only if the browser supports the filter: lower the fill opacity
   and enable the effect (progressive enhancement). */
@supports ((-webkit-backdrop-filter: blur(1px)) or (backdrop-filter: blur(1px))) {
  .glass {
    background: rgba(255, 255, 255, 0.12);
    -webkit-backdrop-filter: blur(16px) saturate(160%);
    backdrop-filter: blur(16px) saturate(160%);
  }
}

/* 2) The user asked for reduced transparency: solid variant, no blur.
   Exists in Safari/WebKit; where it's ignored, the @supports above still
   covers legibility. */
@media (prefers-reduced-transparency: reduce) {
  .glass {
    background: rgba(28, 28, 30, 0.97);
    -webkit-backdrop-filter: none;
    backdrop-filter: none;
  }
}
```

Contract rule: **never ship illegible glass as the only option.** 🟡

## 3. Performance 🟡

`backdrop-filter` is one of CSS's most expensive effects: it forces its own
composition layer and re-samples the background every frame while something
behind it changes. Cost grows with the **area** covered and the **number of
stacked surfaces**.

Practical rules:

- 1–3 blurred surfaces at once at most; **never** a grid of blurred cards.
- Don't animate the blur radius or `backdrop-filter` itself; animate only
  `transform` and `opacity` on elements with glass.
- Fixed glass (sticky nav) is cheap once composed; glass that moves over
  animated content is expensive.
- On low-end mobile, degrade to the solid variant.
- `will-change`: only on GPU-composition properties (`transform`,
  `opacity`, `filter`, `clip-path`); never `will-change: all` or on dozens
  of elements (compositor memory ceiling on iOS/WKWebView).
- ⚠️ Specific GPU figures circulating in articles (40–60% idle with abusive
  blur, etc.) are indicative of one specific case, not extrapolatable. Don't
  cite them as a rule.

## 4. Do / don't pairs

1. **Only floating functional chrome.**
   - ✅ DO: sticky nav, bars, modals/sheets, toasts — the web's functional layer. ✅/⚠️
   - ❌ DON'T: list cards, page backgrounds, body text with blur. Content uses solid backgrounds or simple CSS materials. ✅/⚠️

2. **Honesty about the material.**
   - ✅ DO: present `backdrop-filter` as a **visual approximation**, with its `@supports` fallback and respect for `prefers-reduced-transparency`. ⚠️
   - ❌ DON'T: claim the CSS "is" Liquid Glass; nor ship glass with no fallback as the only option. ⚠️

3. **Contrast before aesthetics.**
   - ✅ DO: measure text against the **worst possible background**; if it collapses, raise the fill opacity or add a scrim; over bright backgrounds, the 35% dimming veil. ✅/🟡
   - ❌ DON'T: long paragraphs over glass, or text that only reads over the nominal background. ✅

4. **Blur in moderation.**
   - ✅ DO: 1–3 blurred surfaces at once; animate only `transform`/`opacity`. 🟡
   - ❌ DON'T: grids of blurred cards, or animating the blur radius or `backdrop-filter` itself. 🟡

5. **Safari first.**
   - ✅ DO: the `-webkit-backdrop-filter` line before the standard one. 🟡
   - ❌ DON'T: assume `prefers-reduced-transparency` exists in every browser — `@supports` is the safety net. 🟡

## Sources

- Base recipe: community consensus across 6+ CSS recipes (frost + saturate + translucency + hairline + ambient shadow).
- Two-layer rules and the 35% dimming layer: HIG Materials (quoted in `liquid-glass.md`).
- `prefers-reduced-transparency`: Media Queries Level 5 spec (real support in Safari/WebKit).
