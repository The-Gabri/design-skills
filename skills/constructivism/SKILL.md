---
name: constructivism
description: Russian Constructivism (1919–1931) — Rodchenko, El Lissitzky, Klutsis. Red/black/cream palette, diagonal compositions, bold grotesque type as structure, photomontage, agitational poster language. Use for posters, exhibitions, festivals, and anything that should shout rather than whisper.
---

# Russian Constructivism

## Principles

1. **The artist is an engineer, not a decorator.** Constructivists called themselves "constructors": design serves a social purpose — agitate, inform, mobilize. Every element must work like a machine part. Decoration is counter-revolutionary. ✅
2. **The diagonal is the movement.** Compositions are built on sharp diagonal axes (roughly 30–45°) that create urgency and forward motion — the red wedge piercing the circle in Lissitzky's *Beat the Whites with the Red Wedge* (1919), Rodchenko's tilted planes in the *Books (Please)!* poster (1924). Text itself follows the diagonal. ✅
3. **Type is a structural material.** Headlines are set huge, bold, condensed, often rotated along the diagonal; words are scaled to fill the composition; baselines are broken on purpose. "The text IS the design — remove the words and you lose the composition entirely." ✅
4. **Photomontage over illustration.** Klutsis and Rodchenko fused photographs with geometric shapes and bold text — factual imagery plus emotional direction in one plane. Photos are cropped hard, enlarged, silhouetted, and tipped diagonally. Never a soft, framed photograph. ✅
5. **Three colors are enough.** Red (energy, the new order), black (structure, the worker), and paper white/cream. Red framed by black is the canonical pairing. A limited palette used flat is more violent and more legible than any spectrum. ✅
6. **The poster shouts.** Copy is imperative, exclamatory, slogan-short: orders and declarations, not descriptions. Large exclamation marks are structural elements. The layout should read like a loudspeaker. 🟡

## Color

The palette comes from lithographic posters of the 1920s: cheap inks on cheap paper.

✅ **Paper** `#ECE2C8` — aged uncoated poster stock; the default ground. Warmer than white, never clinical.  
✅ **Ink** `#141414` — near-black for type, rules, structure. Red framed by black is the canonical Rodchenko pairing.  
✅ **Signal red** `#C8102E` — the revolutionary red: energy, action, the wedge, the call to act.  
🟡 **Constructivist red alt** `#D21E1E` — sampled from museum reproductions of Rodchenko's 1924–25 posters; acceptable when you need a slightly brighter red for screen. The exact tint varies across prints; consistency matters more than the number.  
🟡 **Off-black field** `#1E1A16` — for full-bleed dark sections (Lissitzky's black grounds). Slightly warm, so it sits with the paper.  
⚠️ **Ochre yellow** `#E3A82B` — rare fourth color (seen in Rodchenko's rubber-trust poster alongside red/blue). Use sparingly or not at all; red/black/cream must dominate.

Rules:
- Flat fills only. No gradients, no tints, no pastels, no translucency-as-decoration.
- Red is for **energy and action** (headlines, CTAs, the wedge). Black is for **structure** (rules, body text, frames). Never swap their jobs.
- Dark sections use cream type; red sections use cream or black type. Never red type on black — it dies.

## Typography

The real thing: hand-lettered **grotesque block lettering** — Rodchenko drew his own heavy, condensed, angular capitals for posters and *LEF* magazine covers; Lissitzky set type along diagonal trajectories. There is no single "official" typeface; the *treatment* is the system. ✅

Closest free substitutes (🟡):
1. **Anton** (Google Fonts) — ultra-bold condensed single weight; the closest free stand-in for Rodchenko's poster capitals.
2. **Oswald** (Google Fonts) — condensed grotesque with real weights (500/600/700); subheads and kickers.
3. **Archivo** (Google Fonts) — neutral grotesque for body; use 400/500 only.

Rules:
- Headlines: **UPPERCASE always**, Anton, tight tracking (−1%), line-height 0.9–1.0, sizes 48–140px. Scale words to fill the line; it is fine — good — for one word to be three times the size of the next.
- **Rotate headlines** −3° to −8°, or set them on a full diagonal bar. Type must have *direction*, not sit level.
- Kickers/labels: Oswald 600, 12–14px, letter-spacing 12–18% em, uppercase. This is the only "quiet" voice allowed.
- Body: Archivo 15–17px, line-height 1.55, flush left, never justified. Keep it short — constructivist pages are not essays.
- **Exclamation marks are punctuation and ornament.** Use them freely in headlines. Never italicize for emphasis — use scale, weight, or red instead.
- Mixed sizes inside one headline are a feature: `THE POSTER` small over `SHOUTS!` enormous.

## Layout & spacing

- **The diagonal axis rules everything.** Anchor the composition to one dominant diagonal (30–45°). Red bars, wedges, and headline baselines all ride it. Everything else braces against it.
- **Overlapping planes.** Bars slide over circles; the wedge pierces the disc; type sits on top of imagery. Cut elements off the page edge — the composition continues past the frame.
- **Broken grid, deliberate tension.** Asymmetric, off-center, collaged. Nothing is centered "for balance"; mass is balanced by force, like Lissitzky's small red rectangles dominating dispersing white ones.
- **Full-bleed color fields.** Entire sections in flat red or flat black, with cream type knocked out. This is the poster's logic applied to the page.
- **Radius:** `0` everywhere. Circles are perfect circles; everything else is a hard edge.
- **Rules:** 3–6px solid black bars; 8–24px red bars at the diagonal angle. Rules are beams, not hairlines.
- **Depth:** flat. If a layer must lift, use a hard offset "print" shadow (`box-shadow: 8px 8px 0 #141414`) — a misregistered print pass, never a blur.
- **Spacing scale (base 8px):** `8 / 16 / 32 / 64 / 96`. Whitespace is the pause between shouts.

## Components

All copy-pasteable. Base vars:

```css
:root {
  --paper: #ECE2C8;
  --ink: #141414;
  --red: #C8102E;
  --black-field: #1E1A16;
  --rule: 4px solid var(--ink);
  --display: "Anton", "Arial Narrow", sans-serif;
  --head: "Oswald", "Arial Narrow", sans-serif;
  --body: "Archivo", Arial, sans-serif;
}
```

### 1. Wedge hero (after Lissitzky, 1919)

```html
<section class="wedge-hero">
  <svg class="wedge-art" viewBox="0 0 400 400" aria-hidden="true">
    <circle cx="250" cy="200" r="120" fill="#ECE2C8"/>
    <polygon points="60,320 260,80 300,120 100,360" fill="#C8102E"/>
    <rect x="40" y="60" width="46" height="14" fill="#C8102E" transform="rotate(24 63 67)"/>
  </svg>
  <div class="wedge-copy">
    <p class="kicker">festival of the new art · nº 07</p>
    <h1>BEAT THE<br>OLD WORLD<br><span>WITH THE NEW!</span></h1>
    <p class="lede">Three days of posters, film and noise. Art leaves the museum and takes the street.</p>
  </div>
</section>
<style>
.wedge-hero { background: var(--black-field); color: var(--paper); display: grid;
  grid-template-columns: 1fr 1.2fr; align-items: center; padding: 96px 48px; overflow: hidden; }
.wedge-art { width: 100%; max-width: 420px; }
.kicker { font: 600 13px/1 var(--head); letter-spacing: .18em; text-transform: uppercase; color: var(--red); }
.wedge-copy h1 { font: 400 clamp(56px, 8vw, 128px)/0.92 var(--display); margin: 16px 0;
  transform: rotate(-4deg); }
.wedge-copy h1 span { color: var(--red); }
.lede { font: 400 18px/1.55 var(--body); max-width: 38ch; }
</style>
```

### 2. Agit marquee bar

```html
<div class="agit"><div class="agit-track">
  <span>DOWN WITH DECORATION!</span><span>ART INTO LIFE!</span><span>THE POSTER SHOUTS!</span><span>WORKERS OF ALL COUNTRIES!</span>
</div></div>
<style>
.agit { background: var(--ink); color: var(--paper); overflow: hidden; border-top: var(--rule); border-bottom: var(--rule); }
.agit-track { display: flex; gap: 64px; padding: 12px 0; white-space: nowrap; width: max-content;
  animation: agit 18s linear infinite; }
.agit-track span { font: 400 28px/1 var(--display); text-transform: uppercase; }
.agit-track span:nth-child(even) { color: var(--red); }
@keyframes agit { to { transform: translateX(-50%); } }
</style>
```

### 3. Poster card (event / exhibition)

```html
<article class="poster">
  <div class="poster-ribbon">FRI 09</div>
  <p class="poster-kicker">cinema-eye series</p>
  <h3>MAN WITH<br>A MOVIE<br>CAMERA</h3>
  <p class="poster-meta">Vertov · 1929 · live score<br>hall B · 21:00</p>
  <a class="btn-agit" href="#">TAKE A SEAT</a>
</article>
<style>
.poster { background: var(--paper); border: var(--rule); padding: 28px; max-width: 340px; position: relative; }
.poster-ribbon { position: absolute; top: 18px; right: -14px; background: var(--red); color: var(--paper);
  font: 600 13px/1 var(--head); letter-spacing: .14em; padding: 10px 16px; transform: rotate(4deg); }
.poster-kicker { font: 600 12px/1 var(--head); letter-spacing: .18em; text-transform: uppercase; color: var(--red); margin: 0; }
.poster h3 { font: 400 52px/0.95 var(--display); margin: 14px 0; transform: rotate(-2deg); }
.poster-meta { font: 500 15px/1.5 var(--body); border-top: var(--rule); padding-top: 12px; }
</style>
```

### 4. Diagonal section header

```html
<div class="sec-head"><span class="sec-no">02</span><h2>PROGRAMME</h2><span class="sec-bar"></span></div>
<style>
.sec-head { display: flex; align-items: center; gap: 20px; padding: 32px 0; overflow: hidden; }
.sec-no { font: 400 56px/1 var(--display); color: var(--red); transform: rotate(-6deg); }
.sec-head h2 { font: 400 44px/1 var(--display); margin: 0; letter-spacing: .01em; }
.sec-bar { flex: 1; height: 14px; background: var(--red); transform: rotate(-2deg); min-width: 80px; }
</style>
```

### 5. Agit button

```html
<a class="btn-agit" href="#">GET TICKETS</a>
<a class="btn-agit btn-black" href="#">READ THE MANIFESTO</a>
<style>
.btn-agit { display: inline-block; font: 400 22px/1 var(--display); text-transform: uppercase;
  letter-spacing: .04em; color: var(--paper); background: var(--red); padding: 18px 34px;
  text-decoration: none; box-shadow: 8px 8px 0 var(--ink); transform: rotate(-1.5deg); }
.btn-agit:hover { background: var(--ink); box-shadow: 8px 8px 0 var(--red); }
.btn-agit:active { transform: rotate(-1.5deg) translate(4px, 4px); box-shadow: 4px 4px 0 var(--ink); }
.btn-black { background: var(--ink); box-shadow: 8px 8px 0 var(--red); }
.btn-black:hover { background: var(--red); box-shadow: 8px 8px 0 var(--ink); }
</style>
```

### 6. Manifesto block (red field)

```html
<section class="manifesto">
  <p class="manif-kicker">from the manifesto</p>
  <blockquote>THE POSTER IS NOT DECORATION.<br>THE POSTER IS AN ORDER!</blockquote>
  <p class="manif-sign">— workers' art committee, 1925</p>
</section>
<style>
.manifesto { background: var(--red); color: var(--paper); padding: 96px 48px; }
.manif-kicker { font: 600 13px/1 var(--head); letter-spacing: .18em; text-transform: uppercase; margin: 0 0 24px; }
.manifesto blockquote { font: 400 clamp(40px, 6vw, 88px)/0.95 var(--display); margin: 0;
  transform: rotate(-2deg); max-width: 16ch; }
.manif-sign { font: 600 14px/1 var(--head); letter-spacing: .14em; text-transform: uppercase; margin: 32px 0 0; }
</style>
```

### 7. Programme rows (rule-separated list)

```html
<ul class="rows">
  <li><span class="when">FRI 09 · 19:00</span><strong>opening rally: the wedge returns</strong><em>hall A</em></li>
  <li><span class="when">SAT 10 · 11:00</span><strong>photomontage atelier with klutsis' method</strong><em>workshop 2</em></li>
  <li><span class="when">SUN 11 · 16:00</span><strong>books (please)! — the lengiz posters</strong><em>gallery</em></li>
</ul>
<style>
.rows { list-style: none; margin: 0; padding: 0; }
.rows li { display: flex; align-items: baseline; gap: 20px; padding: 20px 0; border-bottom: 3px solid var(--ink); }
.when { font: 600 13px/1.4 var(--head); letter-spacing: .1em; background: var(--ink); color: var(--paper);
  padding: 8px 12px; transform: rotate(-2deg); flex: none; }
.rows strong { font: 400 26px/1.1 var(--display); text-transform: uppercase; }
.rows em { margin-left: auto; font: 500 14px/1.4 var(--body); font-style: normal; flex: none; }
</style>
```

### 8. Photomontage collage (CSS/SVG, no photos needed)

```html
<div class="montage" aria-label="photomontage collage">
  <svg viewBox="0 0 600 400">
    <defs><pattern id="dots" width="14" height="14" patternUnits="userSpaceOnUse">
      <circle cx="7" cy="7" r="3" fill="#141414"/></pattern></defs>
    <rect x="40" y="60" width="280" height="280" fill="url(#dots)"/>
    <circle cx="430" cy="200" r="110" fill="#C8102E"/>
    <polygon points="300,360 520,60 560,100 340,400" fill="#141414"/>
    <rect x="120" y="120" width="200" height="34" fill="#ECE2C8" transform="rotate(-12 220 137)"/>
    <text x="140" y="146" font-family="Anton, sans-serif" font-size="26" fill="#141414" transform="rotate(-12 220 137)">SHOUT!</text>
  </svg>
</div>
<style>
.montage { background: var(--paper); border: var(--rule); }
.montage svg { display: block; width: 100%; height: auto; }
</style>
```
Photomontage guidance: layer hard-edged cutouts (circles, wedges, halftone fields, type bars) at conflicting angles. When you have real photos, crop them brutally, silhouette or duotone them to red/black, and tip them on the diagonal — never a soft framed rectangle.

## Motion

Constructivism defines no screen-motion language — posters are static. When you must animate: hard cuts and linear mechanical motion only (marquee bars, instant state flips, 150–250ms linear slides). No easing curves, no bounce, no fade-and-float "delight".

## Do / Don't

- ✅ DO set headlines uppercase, huge, condensed, and slightly rotated — type must have direction. — ❌ DON'T set headlines level, title-case, or in a light humanist sans.
- ✅ DO build the page on one dominant diagonal: red bars, wedges, and type all ride it. — ❌ DON'T center the layout symmetrically or stack polite centered cards.
- ✅ DO use flat red/black/cream only, with hard edges and radius 0. — ❌ DON'T use gradients, translucency, soft shadows, or a fourth "pretty" color.
- ✅ DO let the red wedge pierce the circle, the bar slide over the photo — overlap and cut off the page edge. — ❌ DON'T box everything in neat padded containers with breathing room on all sides.
- ✅ DO write imperatives and exclamations: "Take a seat!", "Down with decoration!" — ❌ DON'T write soft marketing copy ("Discover our curated experience…").
- ✅ DO use the exclamation mark as a structural element, oversized if needed. — ❌ DON'T italicize or use light weights for emphasis; use scale, weight, or red.
- ✅ DO make the CTA a red block with a hard black offset shadow that inverts on hover. — ❌ DON'T use pill buttons, ghost buttons, or gradient CTAs.

## Copy voice

Constructivist copy is agitation: short imperative declarations, slogans, orders. It addresses a collective ("comrades", "workers", "all"), names an enemy (the old, the decorative, the passive), and ends with a command. Exclamation marks everywhere; no hedging, no "maybe", no brand warmth.

- "The poster does not decorate. It orders. Come and see — leave and build!"
- "Down with art for art's sake! Art belongs on the street, in the factory, in your hands!"
- "Tickets on sale now. The wedge waits for no one!"

## Sources consulted

- Smarthistory, "Suprematism, Part II: El Lissitzky" — *Beat the Whites with the Red Wedge* (1919), red triangle/white circle symbolism, text aligned to the diagonal: https://smarthistory.org/suprematism-part-ii-el-lissitzky/
- Smarthistory, "Constructivism, Part II" — Rodchenko's advertising posters, Klutsis photomontage, Stenberg brothers' diagonal compositions, red/yellow/blue/black/white palette: https://smarthistory.org/constructivism-part-ii/
- ELEPHANT, "The Memeification of Rodchenko's Iconic Soviet Portrait" — the 1924 Lengiz *Books (Please)!* poster: tilted perspective, photomontage, slogan "BOOKS in all fields of knowledge": https://elephant.art/the-memeification-of-rodchenkos-iconic-soviet-portrait-lilya-brik-14102020/
- UQAM thesis, "Revolution by design" (archipel.uqam.ca) — Rodchenko's *Novy LEF* covers: red framed by black (red = the Soviet state, black = the proletariat), bold typography as "arresting noises shouted through a loudspeaker", slogan-like statements.
- Wikipedia, "Beat the Whites with the Red Wedge" — 1919, Lissitzky, red wedge vs. white circle on black-and-white ground: https://en.wikipedia.org/wiki/Beat_the_Whites_with_the_Red_Wedge
- designyourway.net, "What Is Constructivism in Graphic Design?" — type as structural element, rotated headlines, broken baselines, photomontage method: https://www.designyourway.net/blog/what-is-constructivism-in-graphic-design/
