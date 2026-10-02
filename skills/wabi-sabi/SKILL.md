---
name: wabi-sabi
description: The Japanese aesthetic of imperfection and transience — asymmetry, roughness, simplicity, modesty, and intimacy rendered in quiet earth tones, weathered textures, and generous negative space. Use for artisan brands, ceramics, tea houses, slow-living products, and editorial pages that should feel handmade and human rather than polished.
---

# Wabi-Sabi

## Confidence legend
- ✅ = documented in the philosophy's canonical sources (Leonard Koren's *Wabi-Sabi for Artists, Designers, Poets & Philosophers*, Wikipedia/Stanford Encyclopedia of Philosophy summaries, Zen aesthetic theory) and confirmed across ≥2 independent sources.
- 🟡 = cross-referenced across design writing on the aesthetic (muted earth palettes, material honesty, web applications); no single canonical web spec exists.
- ⚠️ = community approximation — my translation of the philosophy into web tokens; useful but not dogma.

## Principles
1. **Imperfect** ✅ — Asymmetry, irregularity, and roughness are character, not defects. "Wabi-sabi is the beauty of things imperfect, impermanent, and incomplete" (Koren, via Wikipedia). Stop experiencing asymmetry as failure.
2. **Impermanent** ✅ — Everything passes; beauty intensifies because it fades. From the Buddhist three marks of existence (*sanbōin*): impermanence (*mujō*), suffering, emptiness. Design for the object as it ages, not as it ships.
3. **Incomplete** ✅ — Nothing perfectly finished; the viewer participates. The aesthetic concept of *ma* (間) — meaningful negative space, the pregnant pause — belongs here. Leave gaps for the eye to rest and the mind to complete.
4. **Simple and modest** ✅ — *Kanso* (simplicity), *shibumi* (understated beauty), *seijaku* (tranquility). Remove excess until the essential shows. Quiet presence over strong expression.
5. **Intimate and natural** ✅ — *Shizen* (naturalness), *fukinsei* (irregularity/asymmetry). Human scale, handmade marks, materials left to be themselves: clay, wood, stone, linen. Appreciation of natural objects and the forces of nature.
6. **Not japandi** 🟡 — Japandi is a styled interior-design fusion: polished, balanced, quietly refined. Wabi-sabi is the deeper philosophy underneath: warmer, looser, more weathered. A japandi room looks carefully arranged; a wabi-sabi room looks gently lived in. If your layout wants crisp balance, you want the japandi skill, not this one.

## Color
There is no official wabi-sabi swatch book — the documented guidance is "muted, earthy colors that resemble the natural world; bright, poppy colors are scarce" (design thesis research, corroborated by interior/editorial writing). Families 🟡, hex values ⚠️.

| Token | Hex | Role |
|---|---|---|
| `--washi` | `#F1EAE0` ⚠️ | Background — unbleached paper, the default surface |
| `--washi-deep` | `#E6DACA` ⚠️ | Recessed/alternate background, aged paper |
| `--ink` | `#2E2A24` ⚠️ | Primary text — sumi ink, warm near-black |
| `--ink-soft` | `#5C554A` ⚠️ | Secondary text — faded ink |
| `--clay` | `#A9714B` ⚠️ | Warm accent — fired terracotta |
| `--ash` | `#8C887C` ⚠️ | Neutral mid — wood ash gray |
| `--moss` | `#767A58` ⚠️ | Cool accent — muted green, moss/patina |
| `--kintsugi` | `#C6A15B` 🟡 | Gold seam — kintsugi repair gold ✅ (lacquer mixed with powdered gold is the documented technique; this hex is my approximation of aged gold lacquer) |

Rules: one accent per screen (clay **or** moss **or** kintsugi gold, never all three at full strength). Gold is a seam, not a button color — reserve it for repair lines, hairline dividers, and marks of honor. Text sits on washi in ink; dark sections are rare and brief, like the inside of a kiln.

## Typography
- **Display:** a text serif with visible hand and warmth. Closest free options: **Shippori Mincho** (Japanese mincho, calligraphic stroke contrast — the most on-theme Google Font) or **Cormorant Garamond**. Weights 400–600; headlines set large with loose line-height (1.15–1.3) and *ragged, never justified* edges. ✅ asymmetry of the line over the symmetry of the block.
- **Body:** a quiet humanist sans — **Karla**, **Klee One** (handwritten-adjacent Japanese Gothic), or system sans as fallback. 16–18px, line-height 1.7–1.9. Generous measure (55–65ch) so paragraphs breathe.
- **Annotations:** one handwritten voice for maker's notes, prices, margin comments — **Caveat** or **Nanum Pen Script**, slightly rotated (−1 to −2deg), in ink-soft. ⚠️ web convention, but it reads instantly as "the maker's hand".
- Rules: no all-caps display type (shouting breaks *seijaku*); letter-spacing stays natural; italic is for whispers, not emphasis. Sentence case everywhere.

## Layout & spacing
- **Ma (negative space)** ✅ — the primary material. Sections get 2–3× the whitespace a corporate page would use. Empty space is content.
- **Deliberate asymmetry** ✅ — *fukinsei*: focal elements sit off-center (rule of thirds, not the grid's middle). Overlap blocks by small, irregular amounts. Never center everything; a centered hero with a pill button is the anti-pattern of this skill.
- **Organic edges** 🟡 — torn/deckled edges between sections, irregular border radii (`border-radius: 48% 52% 55% 45% / 50% 46% 54% 50%` — never a perfect circle or a uniform 8px), dashed "stitched" hairlines instead of hard rules.
- **Texture over flatness** 🟡 — paper grain via inline SVG `feTurbulence` at low opacity; never a sterile flat `#fff`. Texture should be felt at 10% opacity, not seen.
- **Rhythm:** sections alternate paper tones; content column ~65ch; side notes drift into margins at wide widths. Vertical rhythm follows content, not a rigid 8pt grid — snap to multiples of 4px only where it aids alignment.

## Components
All snippets are plain HTML/CSS, copy-pasteable. Assumes the tokens above.

**1. Grain-textured paper panel** — the signature surface.
```html
<svg width="0" height="0" style="position:absolute" aria-hidden="true">
  <filter id="paper-grain">
    <feTurbulence type="fractalNoise" baseFrequency="0.9" numOctaves="2" result="n"/>
    <feColorMatrix in="n" type="matrix" values="0 0 0 0 0  0 0 0 0 0  0 0 0 0 0  0 0 0 0.06 0"/>
  </filter>
</svg>

<section class="wabi-panel">
  <!-- content -->
</section>

<style>
.wabi-panel{
  position:relative; background:var(--washi); padding:clamp(2.5rem,6vw,5rem);
}
.wabi-panel::after{
  content:""; position:absolute; inset:0; pointer-events:none;
  filter:url(#paper-grain); /* 6% opacity grain baked into the filter */
}
</style>
```

**2. Kintsugi seam divider** — a gold "repaired crack" between sections.
```html
<div class="kintsugi-seam" aria-hidden="true">
  <svg viewBox="0 0 600 24" preserveAspectRatio="none">
    <path d="M0,14 L70,10 L130,16 L210,8 L290,15 L360,9 L440,17 L520,11 L600,14"
          fill="none" stroke="var(--kintsugi)" stroke-width="2.5" stroke-linecap="round"/>
    <path d="M210,8 L235,18 L262,12" fill="none" stroke="var(--kintsugi)"
          stroke-width="1.5" stroke-linecap="round" opacity="0.7"/>
  </svg>
</div>

<style>
.kintsugi-seam{ max-width:420px; margin:0 auto; opacity:.9; }
.kintsugi-seam svg{ width:100%; height:22px; display:block; }
</style>
```
Rule: the crack path must be jagged and hand-drawn, never a straight line or a perfect zigzag.

**3. Torn-edge card** — deckled, uneven border via layered radius.
```html
<article class="torn-card">
  <h3>Winter teabowl</h3>
  <p>Thrown in January, glazed with wood ash. The lip warped in the kiln — we kept it.</p>
</article>

<style>
.torn-card{
  background:#FAF6EE; padding:2rem;
  border-radius: 4% 6% 5% 7% / 6% 5% 7% 4%;   /* irregular, never uniform */
  box-shadow: 3px 5px 0 rgba(46,42,36,.06);    /* soft offset, not a crisp shadow */
  border:1px dashed rgba(46,42,36,.25);        /* stitched, not ruled */
}
</style>
```

**4. Asymmetric offset hero** — grid with an off-center focal point.
```html
<header class="wabi-hero">
  <div class="wabi-hero-copy">
    <p class="wabi-kicker">Handmade ceramics · Est. 2011</p>
    <h1>Beautiful<br>because<br>it's broken.</h1>
  </div>
  <figure class="wabi-hero-vessel"><!-- vessel SVG / photo --></figure>
  <p class="wabi-handnote">fired at 1,300°C — warped on purpose</p>
</header>

<style>
.wabi-hero{
  display:grid; grid-template-columns: repeat(12,1fr);
  gap:1.5rem; align-items:end; padding:clamp(3rem,8vw,7rem) 5vw;
}
.wabi-hero-copy{ grid-column:2 / span 6; }
.wabi-hero-vessel{ grid-column:9 / span 3; margin-bottom:-2rem; } /* overlapping, sinking */
.wabi-handnote{
  grid-column:3 / span 4; font-family:"Caveat",cursive;
  transform:rotate(-1.5deg); color:var(--ink-soft);
}
@media (max-width:720px){
  .wabi-hero-copy,.wabi-hero-vessel,.wabi-handnote{ grid-column:1 / -1; }
}
</style>
```

**5. Quiet button** — ink outline, irregular radius, no fill until hover.
```html
<a class="wabi-btn" href="#">Visit the kiln</a>

<style>
.wabi-btn{
  display:inline-block; padding:.8rem 1.9rem;
  border:1.5px solid var(--ink); color:var(--ink);
  border-radius:12px 16px 13px 18px; /* irregular pill, never a uniform radius */
  text-decoration:none; transition:background .35s ease,color .35s ease;
}
.wabi-btn:hover{ background:var(--ink); color:var(--washi); }
</style>
```

**6. Vessel frame** — irregular "handmade" image frame for objects.
```html
<figure class="vessel">
  <img src="teabowl.jpg" alt="Ash-glazed teabowl with a gold kintsugi seam">
  <figcaption>Chawan, winter firing — <span class="sold">sold</span></figcaption>
</figure>

<style>
.vessel img{
  width:100%; display:block;
  border-radius: 52% 48% 55% 45% / 8% 10% 9% 11%; /* clay-like, not circular */
  filter:sepia(.12) contrast(.96);
}
.vessel figcaption{ font-size:.9rem; color:var(--ink-soft); margin-top:.8rem; }
.vessel .sold{ font-family:"Caveat",cursive; color:var(--clay); font-size:1.1rem; }
</style>
```

**7. Stitched tag** — dashed chip for categories/filters.
```html
<span class="stitch-tag">wood-fired</span>

<style>
.stitch-tag{
  display:inline-block; padding:.35rem .9rem; font-size:.8rem;
  border:1px dashed var(--ink-soft); border-radius:14px 18px 15px 20px;
  color:var(--ink-soft); background:transparent;
}
.stitch-tag[aria-pressed="true"]{ border-style:solid; color:var(--ink); background:#FAF6EE; }
</style>
```

**8. Process accordion** — plainspoken, one open at a time.
```html
<div class="wabi-acc">
  <button class="wabi-acc-head" aria-expanded="false">01 · Clay</button>
  <div class="wabi-acc-body"><p>We dig it an hour from here...</p></div>
</div>

<style>
.wabi-acc{ border-top:1px dashed rgba(46,42,36,.3); }
.wabi-acc-head{
  width:100%; text-align:left; background:none; border:0; cursor:pointer;
  font-family:inherit; font-size:1.15rem; padding:1.1rem .25rem; color:var(--ink);
}
.wabi-acc-head::before{ content:"+"; color:var(--clay); margin-right:.75rem; }
.wabi-acc-head[aria-expanded="true"]::before{ content:"–"; }
.wabi-acc-body{ max-height:0; overflow:hidden; transition:max-height .5s ease; }
.wabi-acc-body p{ padding:0 .25rem 1.4rem 2rem; color:var(--ink-soft); max-width:60ch; }
</style>
<script>
document.querySelectorAll('.wabi-acc-head').forEach(h=>{
  h.addEventListener('click',()=>{
    const open = h.getAttribute('aria-expanded')==='true';
    document.querySelectorAll('.wabi-acc-head').forEach(x=>{
      x.setAttribute('aria-expanded','false');
      x.nextElementSibling.style.maxHeight=null;
    });
    if(!open){ h.setAttribute('aria-expanded','true');
      h.nextElementSibling.style.maxHeight=h.nextElementSibling.scrollHeight+'px'; }
  });
});
</script>
```

## Motion
Wabi-sabi defines no motion language — so: move slowly or not at all. One line of doctrine: transitions 300–600ms `ease` (never springy/bouncy), fades and gentle reveals over slides, and `prefers-reduced-motion` disables all of it. Nothing should feel "animated"; the page should feel *settled*.

## Do / Don't
- **Do** leave one section visibly emptier than comfort allows — that emptiness is *ma*. / **Don't** fill every gap with a card, badge, or CTA.
- **Do** let one element sit off-grid or overlap its neighbor by an uneven amount. / **Don't** center-align the whole page; centered hero + pill button + three feature cards is the opposite of this skill.
- **Do** use one muted accent (clay, moss, or kintsugi gold) per screen. / **Don't** combine terracotta, sage, and gold at full saturation — that's a palette, not restraint.
- **Do** draw every divider, crack, and radius slightly irregular by hand (SVG paths, uneven radii). / **Don't** use mathematically perfect zigzags, uniform 8px radii, or crisp drop shadows.
- **Do** write prices and margin notes in a handwritten voice, slightly rotated. / **Don't** use all-caps display type or tight letter-spacing for "impact".
- **Do** show the repair: a kintsugi seam, a visible mend, an honest "sold" or "warped in the kiln". / **Don't** hide flaws behind polish — hiding them is the one true violation here.
- **Do** photograph/describe materials honestly (ash glaze, raw linen, weathered wood). / **Don't** use glossy stock-photo perfection or neon anything.

## Copy voice
Plain-spoken, unhurried, a little poetic. Short sentences. The maker talks about the material, the weather, and what went wrong — never about "disruption", "premium", or "curated". Second person is rare; first-person plural is warm ("we kept it", "we fire twice a year").

- "Thrown in January, glazed with wood ash. The lip warped in the kiln — we kept it."
- "Nothing here is new. Everything here is still becoming."
- "If a bowl survives a hundred winters, it has earned its cracks. We fill them with gold."
