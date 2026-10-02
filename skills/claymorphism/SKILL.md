---
name: claymorphism
description: "Claymorphism — soft puffy 3D UI molded from pastel clay: chunky radii, layered inner/outer shadows, squishy press states. Use for playful consumer apps, onboarding flows, kids' products, anything where warmth beats density."
---

# Claymorphism

## Confidence legend
- ✅ = rule consistent across 3+ independent sources (cross-referenced)
- 🟡 = seen in 2 sources, exact values vary
- ⚠️ = community recipe, unstandardized — useful, not canon

## Purpose
Design interfaces that look molded from soft pastel clay: every surface bulges gently off the background, lit by a single top-left light source that never moves. The style trades information density for tactility — it is a good default for consumer apps, onboarding flows, kids' and education products, creative tools, and playful SaaS. It is a poor choice for finance, legal, medical, government, or data-dense enterprise UIs, where it reads as unserious. 🟡

## Principles
1. **Raised, never flat.** Every surface appears pushed up from behind the page, like clay extruded through the screen. ✅
2. **The dual-shadow grammar.** The clay illusion is built from exactly three stacked shadow layers: one soft colored outer drop (lift), one white inset highlight from the top-left (the light), one dark inset shade on the bottom-right (the thickness). ✅
3. **One fixed light source.** The highlight always comes from the top-left, the dark shade settles bottom-right — on every element, everywhere. Mixing directions breaks the molded illusion. 🟡
4. **Pastel, but saturated.** Fills are high-luminosity, mid-to-high saturation pastels (sweet candy tones), not washed-out tints — roughly HSL 65–100% saturation, 85–92% lightness. ✅
5. **Chunky and touch-first.** Generous padding (20–32px inside cards/buttons) and large hit targets; thin padding reads as "flat UI wearing a shadow," not clay. 🟡
6. **Squish on press.** Interactive elements react like real material: a slight scale-down (0.96–0.98) with shadows collapsing inward on `:active`, bouncing back with a springy ease. 🟡

## Color
Palette (a tinted lilac wash background with candy fills — the most cross-referenced scheme):

| Token | Hex | Role |
|---|---|---|
| `--clay-bg` | `#F0EEFB` 🟡 | Tinted airy page background |
| `--clay-surface` | `#FBFAFF` 🟡 | Near-white raised surface |
| `--clay-ink` | `#2E2A45` ⚠️ | Primary text (deep plum reads softer than black) |
| `--clay-muted` | `#8A82A8` ⚠️ | Secondary text |
| `--clay-violet` | `#7C5CFC` 🟡 | Hero accent (primary buttons, active toggles) |
| `--clay-pink` | `#FFD6E8` ✅ | Candy pink fill (s ≈ 100%, l ≈ 92%) |
| `--clay-mint` | `#C8F4DE` ✅ | Candy mint fill (s ≈ 67%, l ≈ 87%) |
| `--clay-amber` | `#FFE8B3` ✅ | Candy amber fill (s ≈ 100%, l ≈ 85%) |
| `--clay-lav` | `#D6CCFF` ✅ | Candy lavender fill (s ≈ 100%, l ≈ 90%) |
| `--clay-peach` | `#FDBCB4` 🟡 | Candy peach fill |

Rules: shadows are **colored**, not neutral black — tint the outer drop with a darker shade of the element's own hue (10–40% opacity); the inner highlight is white at 40–70% opacity. Barely-there borders are optional (a lighter tint of the fill); **never** thin dark strokes. 🟡

## Typography
Rounded geometric sans only: **Quicksand, Nunito, Poppins, Comfortaa** (all free on Google Fonts; Quicksand/Nunito are the most-cited pair). 🟡 Weights: headings 700, buttons/labels 600–700, body 500. Slightly looser line-height (1.5–1.6). Thin-line or sharp grotesques (Inter/Roboto at light weights) clash with the soft-plastic language — if a font isn't available, a system rounded stack (`ui-rounded, "SF Pro Rounded", "Segoe UI Rounded"`) is the fallback. ⚠️

## Layout & spacing
- **Radii scale:** one fixed card radius, 24–32px, applied everywhere — mixing radii breaks the soft-molded illusion; buttons and pills fully rounded (999px); small chips/inputs 16–24px. ✅
- **Spacing scale:** 20–32px internal padding on cards and buttons; 12–16px for chips; 8px optical gaps between stacked clay elements. 🟡
- **Separation:** shadows do the separating, not strokes — elements sit on the tinted background with room to cast their drop shadow. 🟡
- **Depth hierarchy:** interactive elements (buttons) get a larger outer shadow (12–16px blur) than static containers (cards, 8–12px blur) so touch targets read as more "liftable." 🟡

### The shadow recipe (this IS claymorphism)
```css
/* Card — saturated pastel fill, 28px radius, the canonical three layers */
.clay-card {
  background: var(--clay-lav);
  border-radius: 28px;
  padding: 28px;
  box-shadow:
    8px 8px 24px rgba(108, 76, 240, 0.30),        /* outer drop: soft, colored */
    inset -6px -6px 14px rgba(80, 50, 200, 0.18), /* inner bottom-right shade */
    inset  6px  6px 14px rgba(255, 255, 255, 0.60);/* inner top-left highlight */
}
```
- Outer shadow: diagonal offset (x = y, 8–12px), blur 2–3× the offset, colored tint of the fill at 15–35% opacity. 🟡
- Inner highlight: **negative offset** toward the light (`inset 6px 6px`), white at 40–70%. Inner shade: **positive offset** away from the light, dark tint at 5–15%. ✅
- Never a single shadow, never a hard-edged one (blur always > 0). ✅
- Light mode is the native habitat; dark mode is a partial citizen — invert fill lightness to 25–35% at the same hue, soften the outer shadow, drop the white inset to ~15% opacity. ⚠️

## Components
1. **Clay card** — the atom. Saturated pastel fill, 28px radius, three-layer shadow, 28px padding.
```css
.clay-card { /* see recipe above */ }
.clay-card:hover  { transform: translateY(-2px); }
.clay-card:active { transform: scale(0.98); }
```

2. **Clay button** — fully rounded, chunkier than the card it sits on (bigger shadow = more liftable), squishes on press:
```css
.clay-btn {
  background: var(--clay-violet);
  color: #fff;
  border: 0; border-radius: 999px;
  padding: 16px 36px;
  font-weight: 700; font-size: 1.05rem;
  box-shadow:
    0 12px 20px rgba(124, 92, 252, 0.35),
    inset -4px -4px 10px rgba(60, 30, 160, 0.25),
    inset  4px  4px 10px rgba(255, 255, 255, 0.45);
  transition: transform 180ms cubic-bezier(0.34, 1.56, 0.64, 1), box-shadow 180ms ease;
  cursor: pointer;
}
.clay-btn:hover  { transform: translateY(-2px) scale(1.02); }
.clay-btn:active { transform: scale(0.96); box-shadow:
    0 4px 10px rgba(124, 92, 252, 0.30),
    inset 4px 4px 10px rgba(60, 30, 160, 0.35),
    inset -4px -4px 10px rgba(255, 255, 255, 0.30); }
```
Note the `:active` state flips the insets — the whole shadow set collapses inward so the button reads as pressed *into* the page. 🟡

3. **Squishy toggle** — a clay pill track; the knob is a smaller clay ball that squishes and slides:
```css
.clay-toggle { width: 76px; height: 42px; border-radius: 999px; background: #E3DEF6;
  box-shadow: inset 4px 4px 10px rgba(46, 42, 69, 0.18), inset -3px -3px 8px rgba(255,255,255,0.8);
  position: relative; cursor: pointer; transition: background 200ms ease; }
.clay-toggle .knob { position: absolute; top: 5px; left: 5px; width: 32px; height: 32px;
  border-radius: 50%; background: var(--clay-surface);
  box-shadow: 3px 3px 8px rgba(46,42,69,0.25), inset 3px 3px 6px rgba(255,255,255,0.9);
  transition: left 220ms cubic-bezier(0.34, 1.56, 0.64, 1), transform 220ms cubic-bezier(0.34, 1.56, 0.64, 1); }
.clay-toggle[aria-checked="true"] { background: var(--clay-violet); }
.clay-toggle[aria-checked="true"] .knob { left: 39px; transform: scale(1.05); }
```
```html
<div class="clay-toggle" role="switch" aria-checked="false" tabindex="0"><span class="knob"></span></div>
```

4. **Blob avatar / icon badge** — organic blob radii give the cartoonish clay feel no plain circle can:
```css
.clay-blob {
  width: 64px; height: 64px;
  border-radius: 42% 58% 61% 39% / 45% 42% 58% 55%;
  background: var(--clay-pink);
  box-shadow:
    6px 6px 16px rgba(255, 143, 177, 0.35),
    inset -5px -5px 12px rgba(200, 60, 110, 0.20),
    inset  5px  5px 12px rgba(255, 255, 255, 0.55);
  display: grid; place-items: center;
}
```
Fill the blob with a rounded, filled SVG icon (single-color or duotone) — never thin-line glyphs. 🟡

5. **Clay segmented tabs** — an inset "mold" track with a raised active segment that hops between options:
```css
.clay-tabs { display: inline-flex; gap: 6px; padding: 8px; border-radius: 999px; background: #E9E4FA;
  box-shadow: inset 4px 4px 10px rgba(46,42,69,0.15), inset -3px -3px 8px rgba(255,255,255,0.8); }
.clay-tab { border: 0; border-radius: 999px; padding: 12px 28px; font-weight: 700;
  background: transparent; color: var(--clay-muted); cursor: pointer;
  transition: all 220ms cubic-bezier(0.34, 1.56, 0.64, 1); }
.clay-tab[aria-selected="true"] { background: var(--clay-surface); color: var(--clay-ink);
  box-shadow: 4px 4px 10px rgba(46,42,69,0.18), inset 3px 3px 6px rgba(255,255,255,0.9), inset -3px -3px 6px rgba(46,42,69,0.08); }
```

6. **Clay input** — pressed-in "mold" state (the inverse of a card), which puffs slightly on focus:
```css
.clay-input { border: 0; border-radius: 20px; padding: 16px 22px; font-size: 1rem;
  background: #E9E4FA; color: var(--clay-ink);
  box-shadow: inset 5px 5px 12px rgba(46,42,69,0.15), inset -4px -4px 10px rgba(255,255,255,0.8);
  outline: none; transition: box-shadow 200ms ease; }
.clay-input:focus { box-shadow: inset 3px 3px 8px rgba(46,42,69,0.12), inset -3px -3px 8px rgba(255,255,255,0.8),
    0 0 0 4px rgba(124, 92, 252, 0.25); }
.clay-input::placeholder { color: var(--clay-muted); }
```

7. **Clay stat chip / counter** — small raised lozenge for numbers, badges, counts:
```css
.clay-chip { display: inline-flex; align-items: center; gap: 8px; border-radius: 999px;
  background: var(--clay-mint); padding: 10px 20px; font-weight: 700;
  box-shadow: 5px 5px 12px rgba(60, 160, 110, 0.30),
    inset -3px -3px 8px rgba(40, 120, 80, 0.18), inset 3px 3px 8px rgba(255,255,255,0.55); }
```

8. **Clay progress ring** — a thick pastel track with a chunky rounded thumb, used in fitness/streak UIs:
```css
.clay-progress { height: 22px; border-radius: 999px; background: #E9E4FA; overflow: hidden;
  box-shadow: inset 4px 4px 10px rgba(46,42,69,0.15), inset -3px -3px 8px rgba(255,255,255,0.8); }
.clay-progress > i { display: block; height: 100%; width: 65%; border-radius: 999px;
  background: var(--clay-amber);
  box-shadow: inset 3px 3px 6px rgba(255,255,255,0.55), inset -3px -3px 6px rgba(160,110,30,0.25); }
```

## Motion
Soft bounce is the signature: `cubic-bezier(0.34, 1.56, 0.64, 1)` (overshooting spring) on presses, toggles, tab hops and hovers. 🟡 Press = 140–200ms ease-out with `scale(0.96–0.98)` + shadow collapse; release = springy return. Hover = gentle `translateY(-2px)` lift, never a hard snap. Autoplay and sharp linear transitions kill the softness — motion must always feel like poking dough. Respect `prefers-reduced-motion` (replace the bounce with a plain crossfade/scale, no overshoot).

## Do / Don't
- ✅ Do keep one light source: highlight top-left, shade bottom-right, on every element. / ⚠️ Don't flip shadow directions between components — the molded illusion collapses.
- ✅ Do tint outer shadows with a darker shade of the element's own hue. / ⚠️ Don't use neutral gray/black drops — they read as flat UI, not clay.
- ✅ Do give every element exactly the shadow trio (outer + inner light + inner dark). / ⚠️ Don't use a single `box-shadow` — it looks flat, not clay.
- ✅ Do use one consistent card radius (24–32px) and pill buttons (999px) across the whole screen. / ⚠️ Don't mix 8px sharp-ish radii with 32px blobs.
- ✅ Do make the pressed state invert: insets collapse inward so the button reads as pushed *into* the page. / ⚠️ Don't fake a press with only `scale()` and the same shadows — it looks like a sticker shrinking.
- ✅ Do pair with rounded, filled SVG icons in a single color or duotone. / ⚠️ Don't use thin-line icon sets — they clash with the soft-plastic language.
- ✅ Do keep surfaces flat-colored; at most a light-to-slightly-darker fill shading. / ⚠️ Don't add textures, heavy gradients, or noise — they fight the clay concept.

## Copy voice
Warm, simple, slightly playful — the copy of a friendly toy, not a bank. Short words, exclamation points are fine, gentle nudges over imperatives. 🟡
- "Squish away! Your streak is looking extra puffy today."
- "Yay — habit saved. Give yourself a little poke."
- "Oops, that tap slipped! Try that one more time."

## Sources consulted
- https://www.setproduct.com/blog/claymorphism-design-guide — CSS recipe + press-state shadow collapse (canonical three-layer formula).
- https://github.com/yelixir-dev/vibe-style-skills/blob/HEAD/skills/claymorphism/SKILL.md — dual-shadow grammar, radii 20–30px, colored outer shadows.
- https://github.com/x77jh8gvrn-alt/staqd-skills/blob/HEAD/skills/claymorphism/SKILL.md — dual-shadow depth, pressed vs. raised states, dark-mode notes.
- https://github.com/atul-labs/lex/blob/HEAD/skills/design-intelligence/references/styles/claymorphism.md — tokens, HSL fill ranges (65–100% s / 85–92% l), no-borders rule, depth hierarchy.
- https://github.com/andriusgodeliauskas/claude-skills-agents/blob/HEAD/skills/13-claymorphism/SKILL.md — three-shadow formula with inner-light negative offset, radius 32px, typography hints.
- https://github.com/shekhsahebali/ux-ux-skills/blob/HEAD/claymorphism/SKILL.md — blob radii, flat fills, rounded filled icons, contrast prioritization.
