---
name: netflix
description: Netflix's dark cinematic brand language — full-bleed billboard heroes, horizontal content rails, Top 10 rows, and red-accent CTAs — for streaming-style entertainment UIs.
---

# Netflix

The visual language of Netflix's streaming product (netflix.com/apps):
a dark, cinematic, content-first system. The content IS the interface —
artwork fills the screen edge to edge, the brand speaks only in one red,
and every layout decision serves one metric: get the viewer to press Play.

> Style reference only. Do not reproduce the Netflix wordmark, the N
> symbol, Netflix Sans, or real Netflix titles/artwork — always build with
> fictional content and the substitute typefaces below.

## Principles

1. **Dark by doctrine.** The canvas is always near-black (`#141414`) —
   Netflix's interfaces have no light mode. Dark recedes so the artwork
   glows like a theater screen. (✅ documented)
2. **Content is the interface.** There is almost no "chrome": artwork tiles
   are the navigation, the hero is the product shot. Text describes only
   what the artwork can't. (✅ documented via product)
3. **One red, used as a weapon.** Netflix Red (`#E50914`) appears only on
   the brand mark, the Play button, the Continue Watching progress bar,
   and the Top 10 badge — never as decoration. Scarcity is what makes it
   feel premium. (✅ official brand rule)
4. **Cinema-scale typography.** Display type is huge, condensed, and
   uppercase — title treatments dominate the billboard like a movie
   poster; body copy stays small and quiet underneath. (🟡)
5. **Horizontal everything.** Discovery happens in horizontal rails you
   scroll sideways, not in grids you scan downward. Rows stack: each rail
   is one clear idea ("Trending Now", "Top 10", "Because you watched").
   (✅ documented via product)
6. **Decide fast, reduce friction.** Two buttons on the billboard (Play /
   More Info), match percentages and maturity badges on hover cards —
   everything exists to end "eye gymnastics" and get a decision in
   seconds. (🟡, per Netflix's own 2024 redesign rationale)

## Color

| Token | Hex | Role | Legend |
|---|---|---|---|
| Netflix Red | `#E50914` | Brand mark, Play button, progress bars, Top 10 badge — only | ✅ |
| Symbol Dark Red | `#B20710` | The N symbol's darker ribbon tone | ✅ |
| Canvas | `#141414` | Page background, the "warm charcoal" — dark-only | ✅ |
| Pure Black | `#000000` | Billboard scrims, video-letterbox edges, nav when scrolled | 🟡 |
| White | `#FFFFFF` | Primary text, Play button fill, Top 10 numeral fill (when not outlined) | ✅ |
| Grey 400 | `#B3B3B3` | Secondary text, rail "Explore all" links | 🟡 |
| Grey 700 | `#808080` | Footer text, muted metadata | 🟡 |
| Hairline | `rgba(255,255,255,0.1)` | Subtle dividers in dropdowns/panels | 🟡 |
| Scrim bottom | `linear-gradient(transparent, rgba(20,20,20,.9) 75%, #141414)` | Billboard fade into canvas | ✅ |
| Scrim left | `linear-gradient(90deg, rgba(20,20,20,.85), transparent 55%)` | Billboards: keeps left-side text legible over artwork | 🟡 |

Sources: Netflix brand site (brand.netflix.com) for Red/Canvas/White;
Dalton Maag case study for the typeface; product teardowns for scrims,
greys, and rail behavior.

## Typography

- **Face (official):** Netflix Sans — proprietary, designed by Dalton Maag
  (2018), replaced Gotham across the product. Weights documented:
  400 / 500 / 700. (✅)
- **Closest free substitutes (⚠️ community guidance):**
  - Display / title treatments → **Bebas Neue** — condensed, tall,
    cinematic; the right stand-in for billboard titles and Top 10 numerals.
  - UI / body → **Inter** (or system stack) — clean grotesque close to
    Netflix Sans's neutral voice at small sizes.
- **Scale:** billboard title treatment 56–96px (condensed caps, tight
  leading ~0.95); rail section headers 18–22px, weight 500–700;
  body/synopsis 14–16px at 400; metadata 12–13px muted.
- **Rules:** titles shout, metadata whispers. Rail headers are sentence
  case, medium weight, white. Never set body copy in the display face.

## Layout & spacing

- **Billboard:** full-bleed, ~70–85vh. Artwork edge-to-edge, left-aligned
  content block anchored ~4% from the left edge and vertically centered-low.
  Left and bottom scrims fade into `#141414`.
- **Rails:** section headers at 4% side padding (✅ Netflix's web gutter),
  white 18–22px medium. Tiles nearly touch — gaps of 4–8px, not 24px.
  Rows stack with 24–40px vertical rhythm; no section boxes or cards
  wrapping a rail.
- **Tile aspect ratios:** 16:9 landscape for trending/hero rows,
  2:3 portrait for Top 10 and catalog rows. Corner radius small: ~4px
  (🟡 documented at 4pt on product tiles).
- **Z-pattern of a row:** header row (title left, "Explore all ›" right on
  hover), then a horizontal scroll strip with arrow chevrons on hover,
  pagination dots/segments at the top-right while scrolling (🟡).
- **Nav:** transparent over the billboard; on scroll it fills to solid
  `#141414` (web) — brand mark left, text links center-left, search /
  notifications / profile right. Height ~68px.

## Components

Base context: `body { background:#141414; color:#fff;
font-family:'Netflix Sans', Inter, system-ui, sans-serif; }`. Use the
`nfx-` prefix on all classes.

**1. Billboard hero** (signature)

```html
<header class="nfx-billboard">
  <div class="nfx-billboard-art" aria-hidden="true"></div>
  <div class="nfx-billboard-copy">
    <p class="nfx-series-tag"><span class="nfx-n">N</span> SERIES</p>
    <h1 class="nfx-title">MIDNIGHT<br>HARVEST</h1>
    <p class="nfx-top10">#1 in TV Shows Today</p>
    <p class="nfx-synopsis">A coastal town hides a decades-old secret — and the
    only one digging it up is the sheriff's runaway daughter.</p>
    <div class="nfx-cta-row">
      <a class="nfx-play" href="#"><svg viewBox="0 0 24 24"><path d="M8 5v14l11-7z"/></svg>Play</a>
      <a class="nfx-more" href="#"><svg viewBox="0 0 24 24"><circle cx="12" cy="12" r="10" fill="none" stroke="currentColor" stroke-width="2"/><path d="M12 8v.1M12 11v5" stroke="currentColor" stroke-width="2" stroke-linecap="round"/></svg>More Info</a>
    </div>
  </div>
  <span class="nfx-maturity">TV-MA</span>
</header>
<style>
.nfx-billboard{position:relative;height:78vh;min-height:520px;overflow:hidden}
.nfx-billboard-art{position:absolute;inset:0;
  background:linear-gradient(90deg,rgba(20,20,20,.88) 0%,rgba(20,20,20,.25) 45%,transparent 70%),
             linear-gradient(0deg,#141414 4%,transparent 38%),
             radial-gradient(120% 90% at 70% 20%,#3a1418 0%,#141414 60%)}
.nfx-billboard-copy{position:absolute;left:4%;bottom:26%;max-width:560px}
.nfx-series-tag{display:flex;align-items:center;gap:8px;font-weight:700;letter-spacing:.35em;font-size:14px;margin-bottom:12px}
.nfx-n{color:#E50914;font-family:'Bebas Neue',sans-serif;font-size:22px;letter-spacing:0}
.nfx-title{font-family:'Bebas Neue',Impact,sans-serif;font-size:clamp(64px,9vw,120px);line-height:.92;letter-spacing:.01em;text-shadow:0 4px 24px rgba(0,0,0,.6)}
.nfx-top10{display:flex;align-items:center;gap:8px;font-weight:700;font-size:18px;margin:14px 0 10px}
.nfx-top10::before{content:"TOP 10";background:#E50914;font-size:11px;letter-spacing:.08em;padding:3px 7px;border-radius:3px}
.nfx-synopsis{font-size:16px;line-height:1.5;color:#e8e8e8;text-shadow:0 2px 8px rgba(0,0,0,.7);max-width:44ch}
.nfx-cta-row{display:flex;gap:12px;margin-top:22px}
.nfx-play{display:inline-flex;align-items:center;gap:10px;background:#fff;color:#000;
  font-weight:700;font-size:18px;padding:10px 30px 10px 22px;border-radius:4px;text-decoration:none}
.nfx-play svg{width:26px;height:26px;fill:#000}
.nfx-play:hover{background:rgba(255,255,255,.75)}
.nfx-more{display:inline-flex;align-items:center;gap:10px;background:rgba(109,109,110,.7);color:#fff;
  font-weight:700;font-size:18px;padding:10px 28px;border-radius:4px;text-decoration:none}
.nfx-more svg{width:26px;height:26px}
.nfx-more:hover{background:rgba(109,109,110,.4)}
.nfx-maturity{position:absolute;right:0;bottom:32%;border-left:3px solid #fff;background:rgba(20,20,20,.5);
  padding:8px 34px 8px 12px;font-size:14px;letter-spacing:.05em}
</style>
```

**2. Content rail** (signature) — header + horizontal strip + chevrons

```html
<section class="nfx-rail">
  <h2 class="nfx-rail-head">Trending Now <a href="#">Explore all ›</a></h2>
  <div class="nfx-strip">
    <button class="nfx-chev left" aria-label="Scroll left">‹</button>
    <div class="nfx-tiles">
      <a class="nfx-tile" href="#"><span>NEON HARBOR</span></a>
      <a class="nfx-tile" href="#"><span>IRONWOOD</span></a>
      <a class="nfx-tile" href="#"><span>SALTWATER STATIC</span></a>
    </div>
    <button class="nfx-chev right" aria-label="Scroll right">›</button>
  </div>
</section>
<style>
.nfx-rail{margin:28px 0}
.nfx-rail-head{font-size:20px;font-weight:500;padding:0 4%;margin-bottom:10px;display:flex;align-items:baseline;gap:14px}
.nfx-rail-head a{font-size:12px;color:#54b9c5;text-decoration:none;opacity:0;transition:opacity .2s}
.nfx-rail:hover .nfx-rail-head a{opacity:1}
.nfx-strip{position:relative}
.nfx-tiles{display:flex;gap:6px;overflow-x:auto;padding:0 4%;scrollbar-width:none}
.nfx-tiles::-webkit-scrollbar{display:none}
.nfx-tile{position:relative;flex:0 0 17.5vw;min-width:200px;aspect-ratio:16/9;border-radius:4px;
  background:linear-gradient(135deg,#2b2b2e,#101012);display:flex;align-items:flex-end;
  padding:12px;font-family:'Bebas Neue',sans-serif;font-size:22px;letter-spacing:.04em;
  color:#fff;text-decoration:none;transition:transform .25s ease}
.nfx-chev{position:absolute;top:0;bottom:0;width:4%;border:0;background:rgba(20,20,20,.55);color:#fff;
  font-size:44px;cursor:pointer;opacity:0;transition:opacity .2s;z-index:2}
.nfx-strip:hover .nfx-chev{opacity:1}
.nfx-chev.left{left:0;border-radius:0 4px 4px 0}
.nfx-chev.right{right:0;border-radius:4px 0 0 4px}
</style>
```

**3. Title card with hover preview** (signature) — the card expands in
place on hover, revealing actions and metadata

```html
<div class="nfx-card">
  <div class="nfx-card-art">VIOLET HOUR</div>
  <div class="nfx-card-pop">
    <div class="nfx-card-actions">
      <button class="nfx-round" aria-label="Play">▶</button>
      <button class="nfx-round ghost" aria-label="Add to My List">＋</button>
      <button class="nfx-round ghost" aria-label="Not for me" style="margin-left:auto">👎</button>
    </div>
    <p class="nfx-meta"><b class="match">98% Match</b><span class="age">16+</span><span>2 Seasons</span><span class="hd">HD</span></p>
    <p class="nfx-genres">Neo-Noir · Heist · Slow Burn</p>
  </div>
</div>
<style>
.nfx-card{position:relative;width:240px;border-radius:4px;transition:transform .3s ease,box-shadow .3s ease}
.nfx-card-art{aspect-ratio:16/9;border-radius:4px;background:linear-gradient(135deg,#3d1420,#141414);
  display:flex;align-items:center;justify-content:center;font-family:'Bebas Neue',sans-serif;font-size:28px;letter-spacing:.05em}
.nfx-card-pop{display:none;background:#181818;border-radius:0 0 4px 4px;padding:14px}
.nfx-card:hover{transform:scale(1.18);z-index:5;box-shadow:0 16px 40px rgba(0,0,0,.7);border-radius:4px}
.nfx-card:hover .nfx-card-pop{display:block}
.nfx-card-actions{display:flex;gap:8px;margin-bottom:12px}
.nfx-round{width:36px;height:36px;border-radius:50%;border:2px solid #fff;background:#fff;color:#000;
  font-size:14px;cursor:pointer;display:flex;align-items:center;justify-content:center}
.nfx-round.ghost{background:transparent;color:#fff;border-color:rgba(255,255,255,.5)}
.nfx-meta{display:flex;align-items:center;gap:8px;font-size:13px;color:#bcbcbc;margin:0 0 8px}
.nfx-meta .match{color:#46d369}
.nfx-meta .age{border:1px solid rgba(255,255,255,.4);padding:1px 7px;font-size:12px}
.nfx-meta .hd{border:1px solid rgba(255,255,255,.4);border-radius:3px;padding:0 5px;font-size:11px}
.nfx-genres{font-size:13px;color:#fff;margin:0}
.nfx-genres::before{content:""}
</style>
```
Replace the `👎`/`▶`/`＋` glyphs with inline SVG in production builds.

**4. Top 10 row** (signature) — giant outlined numerals behind portrait posters

```html
<div class="nfx-top10-row">
  <div class="nfx-top10-item"><span class="nfx-num">1</span><div class="nfx-poster">GLASSHOUSE</div></div>
  <div class="nfx-top10-item"><span class="nfx-num">2</span><div class="nfx-poster">LOW ORBIT</div></div>
</div>
<style>
.nfx-top10-row{display:flex;gap:8px;padding:0 4%;overflow-x:auto}
.nfx-top10-item{display:flex;align-items:flex-end;flex:0 0 auto}
.nfx-num{font-family:'Bebas Neue',Impact,sans-serif;font-size:clamp(120px,14vw,220px);line-height:.78;
  color:#141414;-webkit-text-stroke:4px #595959;letter-spacing:-.05em;margin-right:-14px;position:relative;z-index:0}
.nfx-poster{width:clamp(110px,11vw,170px);aspect-ratio:2/3;border-radius:4px;z-index:1;
  background:linear-gradient(160deg,#40242c,#101014);display:flex;align-items:flex-end;
  padding:10px;font-family:'Bebas Neue',sans-serif;font-size:20px;letter-spacing:.04em}
</style>
```

**5. Continue Watching tile** — red progress bar on the poster's bottom edge

```html
<a class="nfx-cw" href="#">
  <span class="nfx-cw-art">ECHO PROTOCOL</span>
  <span class="nfx-cw-bar"><i style="width:64%"></i></span>
  <span class="nfx-cw-meta">S1:E4 "Static" · 22m left</span>
</a>
<style>
.nfx-cw{position:relative;display:block;width:280px;text-decoration:none;color:#fff}
.nfx-cw-art{display:flex;align-items:flex-end;aspect-ratio:16/9;border-radius:4px;
  background:linear-gradient(135deg,#1d2b33,#0d0d0f);padding:12px;
  font-family:'Bebas Neue',sans-serif;font-size:24px;letter-spacing:.04em}
.nfx-cw-bar{position:absolute;left:0;right:0;bottom:44px;height:3px;background:rgba(255,255,255,.25)}
.nfx-cw-bar i{display:block;height:100%;background:#E50914}
.nfx-cw-meta{display:block;font-size:13px;color:#B3B3B3;margin-top:8px;text-align:center}
</style>
```

**6. Maturity rating badge**

```html
<span class="nfx-age">18+</span>
<style>
.nfx-age{border-left:3px solid #fff;background:rgba(20,20,20,.6);
  padding:6px 22px 6px 10px;font-size:13px;letter-spacing:.05em}
</style>
```
(Standalone pill variant: `.nfx-age{border:1px solid rgba(255,255,255,.4);padding:1px 7px;}`
as seen on hover cards — see component 3.)

**7. Top 10 corner badge** — red ribbon on thumbnail top-left

```html
<span class="nfx-badge">TOP 10</span>
<style>
.nfx-badge{background:#E50914;color:#fff;font-size:10px;font-weight:700;letter-spacing:.08em;
  padding:3px 7px;border-radius:3px;box-shadow:0 2px 6px rgba(0,0,0,.5)}
</style>
```

**8. Nav (transparent → solid on scroll)**

```html
<nav class="nfx-nav">
  <a class="nfx-logo" href="#">NOCTURNE</a>
  <div class="nfx-links"><a class="on" href="#">Home</a><a href="#">TV Shows</a><a href="#">Movies</a><a href="#">New & Popular</a><a href="#">My List</a></div>
  <div class="nfx-tools"><button aria-label="Search">⌕</button><button aria-label="Notifications">🔔</button><span class="nfx-avatar"></span></div>
</nav>
<style>
.nfx-nav{position:fixed;top:0;left:0;right:0;height:68px;display:flex;align-items:center;gap:32px;
  padding:0 4%;z-index:50;background:linear-gradient(#000,transparent);transition:background .4s}
.nfx-nav.solid{background:#141414}
.nfx-logo{color:#E50914;font-family:'Bebas Neue',Impact,sans-serif;font-size:30px;letter-spacing:.14em;text-decoration:none}
.nfx-links{display:flex;gap:20px}
.nfx-links a{color:#e5e5e5;text-decoration:none;font-size:14px;transition:color .2s}
.nfx-links a:hover{color:#b3b3b3}
.nfx-links a.on{color:#fff;font-weight:600}
.nfx-tools{margin-left:auto;display:flex;align-items:center;gap:20px}
.nfx-tools button{background:none;border:0;color:#fff;font-size:18px;cursor:pointer}
.nfx-avatar{width:32px;height:32px;border-radius:4px;background:linear-gradient(135deg,#E50914,#7a0a10)}
</style>
```
Use inline SVG icons for search/bell in production (glyphs shown for brevity).

**9. "New episodes" ribbon** — thin promotional strip under nav rails

```html
<p class="nfx-ribbon">New episodes of <b>GLASSHOUSE</b> drop Friday — only on Nocturne.</p>
<style>
.nfx-ribbon{background:#E50914;color:#fff;text-align:center;font-size:14px;padding:8px 16px;margin:0}
</style>
```

**10. Footer**

```html
<footer class="nfx-foot">
  <div class="nfx-social"><a href="#">f</a><a href="#">⌕</a><a href="#">▶</a></div>
  <nav class="nfx-foot-links">
    <a href="#">Audio Description</a><a href="#">Help Center</a><a href="#">Gift Cards</a><a href="#">Media Center</a>
    <a href="#">Investor Relations</a><a href="#">Jobs</a><a href="#">Terms of Use</a><a href="#">Privacy</a>
    <a href="#">Legal Notices</a><a href="#">Cookie Preferences</a><a href="#">Corporate Information</a><a href="#">Contact Us</a>
  </nav>
  <button class="nfx-service">Service Code</button>
  <p class="nfx-copy">© 1997–2026 Nocturne Entertainment</p>
</footer>
<style>
.nfx-foot{padding:48px 4% 32px;color:#808080;font-size:13px}
.nfx-social{display:flex;gap:24px;font-size:20px;margin-bottom:20px}
.nfx-social a{color:#808080;text-decoration:none}
.nfx-foot-links{display:grid;grid-template-columns:repeat(4,minmax(140px,1fr));gap:12px;max-width:900px;margin-bottom:24px}
.nfx-foot-links a{color:#808080;text-decoration:none}
.nfx-foot-links a:hover{text-decoration:underline}
.nfx-service{background:transparent;border:1px solid #808080;color:#808080;
  padding:7px 10px;font-size:13px;cursor:pointer;margin-bottom:20px}
.nfx-service:hover{color:#fff;border-color:#fff}
.nfx-copy{font-size:12px}
</style>
```
(Real product detail: the "Service Code" button and 4-column muted link
grid are signature Netflix footer elements — 🟡.)

## Motion

- **Billboard rotation:** cross-dissolve ~800ms `ease` between featured
  titles; autoplay muted loops behind it. (🟡)
- **Hover expansion:** title cards scale ~1.15–1.2 over ~300ms `ease-out`,
  revealing the preview panel — the single most recognizable Netflix
  interaction. Delay expansion ~400ms so casual mouse passes don't trigger
  it. (🟡)
- **Rail scrolling:** smooth, page-by-page (one viewport of tiles per
  click), ~450ms `ease-in-out`; chevrons fade in on rail hover only.
  (🟡)
- **Nav:** transparent → solid `#141414` fade over ~400ms on scroll.
  (🟡)
- No page-load choreography, no parallax storytelling — motion serves
  browsing, never decoration.

## Do / Don't

- **Do** reserve `#E50914` for brand + Play + progress + Top 10 badge only —
  **don't** use it for links, icons, or decorative flourishes; diluted red
  stops reading as Netflix.
- **Do** make the billboard full-bleed with left/bottom scrims fading into
  `#141414` — **don't** box the hero in a rounded container or add a
  drop shadow.
- **Do** give tiles 4–8px gaps so rails read as one continuous filmstrip —
  **don't** spread cards into a spaced grid; whitespace between tiles kills
  the browsing rhythm.
- **Do** show the red progress bar on the bottom edge of every "continue"
  tile — **don't** invent your own progress style; the 3px red bar is the
  affordance users scan for.
- **Do** render Top 10 numerals as giant outlined figures *behind* the
  portrait posters — **don't** shrink them into a corner badge (that's a
  different component).
- **Do** left-align billboard copy at the 4% gutter with a condensed
  uppercase title treatment — **don't** center the hero or lead with a
  pill CTA; that's every other SaaS page.
- **Do** use sentence-case, medium-weight rail headers ("Trending Now") —
  **don't** uppercase or letterspace them like section eyebrows.
- **Do** put the maturity badge on the billboard's right edge with a white
  left border — **don't** float age ratings in a corner chip.

## Copy voice

Punchy, entertainment-first, conspiratorial. Short sentences. It talks like
a friend who watches too much TV — confident recommendations, playful
urgency, zero corporate filler. Real Netflix cadence: "Watch anywhere.
Cancel anytime."

- Billboard synopsis: "A coastal town hides a decades-old secret — and the
  only one digging it up is the sheriff's runaway daughter."
- Rail nudges: "Because you watched *Glasshouse*" · "#1 in TV Shows Today"
  · "New episodes Friday. Your couch is already waiting."
- Empty/error states: "Lost your way? Let's get you back to something
  worth watching."
