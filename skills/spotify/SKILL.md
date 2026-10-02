---
name: spotify
description: Recreate Spotify's music-product aesthetic — near-black charcoal surfaces, one neon-green accent, pill-and-circle geometry, Circular-style grotesque type, card-row grids, and a persistent now-playing bar.
---

# Spotify

Spotify's product language is **content-first darkness**: a near-black shell that
disappears so album art can glow. The entire UI is achromatic charcoal; the only
true color is the functional green, used sparingly and never decoratively. It
feels like a premium audio device — tactile, rounded, touch-first.

## Principles

1. **Content-first darkness.** The UI recedes into charcoal (`#121212`–`#1f1f1f`)
   so that cover art and photography carry all the color. The shell never
   competes with the media.
2. **One accent, used functionally.** Green marks only what you can *do*: the
   play button, the active nav item, the primary CTA, the progress fill. It is
   never a background and never paired with a second accent.
3. **Pill-and-circle geometry.** Buttons are full pills, controls are circles.
   Everything you touch is round and oversized — the geometry of a physical
   audio device.
4. **Bold, heavyweight display type.** Headlines jump straight to 700–900
   weight; marketing type pulses and stretches like an audio wave.
5. **The page is always playing.** A persistent now-playing bar anchors the
   bottom of every view; playback state (play, like, progress) is ambient UI,
   always visible and one tap away.

## Color

| Token | Hex | Role | Confidence |
|---|---|---|---|
| `green` | `#1DB954` | Official brand green — wordmark, brand moments | ✅ |
| `green-bright` | `#1ED760` | Product green — play button, active nav, CTAs, progress | ✅ |
| `brand-black` | `#191414` | Brand black — the dark side of the identity | ✅ |
| `true-black` | `#000000` | Pure black — OLED depth, deep shadows | ✅ |
| `white` | `#FFFFFF` | Primary text on dark, light fills | ✅ |
| `bg` | `#121212` | App canvas / deep background | 🟡 |
| `surface` | `#181818` | Cards, sidebar, section backgrounds | 🟡 |
| `surface-raised` | `#282828` | Card hover, modals, elevated controls | 🟡 |
| `interactive` | `#1f1f1f` | Hover/interactive surfaces on canvas | 🟡 |
| `text-sub` | `#B3B3B3` | Secondary text, metadata | 🟡 |
| `text-mute` | `#6A6A6A` | Captions, tertiary text, disabled icons | 🟡 |
| `hairline` | `#404040` | Dividers, borders | 🟡 |
| `pill-light` | `#EEEEEE` | Rare light pill fill (cookie banners, marketing CTAs) | 🟡 |

Green is **never** used as a background or decor, and never combined with other
brand colors — per Spotify's guidelines it sits on black, white, or
non-duotoned photography only.

**Duotone imagery.** Brand imagery applies a duotone over photos (two spot
colors, often green-adjacent + black). On product surfaces, covers supply raw
color instead — the duotone is a marketing/brand-campaign treatment.

## Typography

- **CircularSp / Circular** (Lineto, customized for Spotify) — proprietary,
  licensed only to Spotify; currently being replaced by **Spotify Mix**
  (Dineto/Dinamo Typefaces), a bespoke sans that "remixes" narrow and wide
  forms and subtly embeds sound-wave shapes. ✅ (documented via brand press
  and marketing-interactive.com)
- **Closest free substitute: `Figtree`** (Google Fonts) — geometric humanist
  grotesque with Circular's roundness. Fallback stack: `Figtree, Inter,
  Helvetica Neue, helvetica, arial, sans-serif`. ⚠️ (community approximation;
  several guides suggest Inter or Plus Jakarta Sans — Figtree reads closest
  in display weights)
- **Weights:** 400 body · 600 semibold (secondary emphasis) · 700 bold (nav,
  headings, emphasis) · 800/900 display.
- **Scale:** hero 96–128 px / 900 · playlist/section titles 24–32 px / 700 ·
  card titles 14–16 px / 700 · body 14–16 px / 400 · caption 11–12 px / 400 in
  `text-sub`.
- **Labels:** CTA and nav labels are UPPERCASE with `letter-spacing: 1.4–2px`.
- **Track tables:** numerals use `font-variant-numeric: tabular-nums`.

## Layout & spacing

- **App shell:** 3-pane — 240 px left sidebar, fluid main column, optional
  right "now playing" rail; persistent bottom now-playing bar (~80 px).
- **Main view:** vertically scrolling stack of sections, each a heading +
  horizontally scrollable card row (cards ~180–200 px wide, 24 px gap).
- **Card grid:** responsive grid, `minmax(180px, 1fr)`, gap 24 px.
- **Spacing scale:** 8-pt base (`8 / 16 / 24 / 32` px). Section padding 24–32 px.
- **Radius:** cards 8 px · buttons/search 999 px (full pill) · play controls 50%
  (circles) · cover art 4–8 px.
- **Elevation:** flat with heavy dark shadows — `0 8px 24px rgba(0,0,0,0.5)`
  on elevated cards/modals; the now-playing bar floats with a soft top shadow.
- **Playlist hero:** full-bleed gradient extracted from the cover art
  (dominant hues fading into `bg`) above the track table. 🟡

## Components

### 1. Sidebar nav

```html
<nav class="sidebar">
  <a class="nav-item" href="#">Home</a>
  <a class="nav-item active" href="#">Search</a>
  <a class="nav-item" href="#">Your Library</a>
</nav>
```

```css
.sidebar { width: 240px; background: #121212; padding: 24px 12px; }
.nav-item {
  display: flex; align-items: center; gap: 16px; padding: 12px;
  color: #B3B3B3; font-weight: 700; font-size: 14px;
  text-decoration: none; border-radius: 4px;
  transition: color .2s;
}
.nav-item:hover { color: #FFFFFF; }
.nav-item.active { color: #FFFFFF; }
.nav-item.active .nav-icon { color: #1ED760; } /* green marks the active item */
```

### 2. Playlist / album card

```html
<article class="card">
  <div class="card-cover"><img src="cover.jpg" alt="Midnight Frequency cover"></div>
  <h3 class="card-title">Midnight Frequency</h3>
  <p class="card-sub">Late-night synths for empty streets</p>
  <button class="card-play" aria-label="Play Midnight Frequency">▶</button>
</article>
```

```css
.card {
  background: #181818; border-radius: 8px; padding: 16px;
  transition: background .3s; position: relative;
}
.card:hover { background: #282828; }
.card-cover img { border-radius: 4px; aspect-ratio: 1; width: 100%; display: block; }
.card-title { font-size: 16px; font-weight: 700; color: #fff; margin: 16px 0 8px; }
.card-sub { font-size: 14px; color: #B3B3B3; margin: 0;
  display: -webkit-box; -webkit-line-clamp: 2; -webkit-box-orient: vertical; overflow: hidden; }
.card-play {
  position: absolute; right: 24px; bottom: 88px;
  width: 48px; height: 48px; border: none; border-radius: 50%;
  background: #1ED760; color: #000; font-size: 18px; cursor: pointer;
  opacity: 0; transform: translateY(8px);
  transition: opacity .3s, transform .3s, scale .2s;
  box-shadow: 0 8px 24px rgba(0,0,0,.5);
}
.card:hover .card-play { opacity: 1; transform: none; }
.card-play:hover { scale: 1.04; }
```

### 3. Circular play button

```css
.play-btn {
  width: 56px; height: 56px; border-radius: 50%; border: none;
  background: #1ED760; color: #000; cursor: pointer;
  display: grid; place-items: center;
  transition: transform .15s ease, background .15s;
  box-shadow: 0 8px 24px rgba(0,0,0,.5);
}
.play-btn:hover { transform: scale(1.04); background: #1DB954; }
```

### 4. Track row (playlist table)

```html
<div class="track-row">
  <span class="track-num">1</span>
  <img class="track-cover" src="cover.jpg" alt="">
  <div class="track-meta">
    <p class="track-name">Neon Coastline</p>
    <p class="track-artist">Glass Harbor</p>
  </div>
  <span class="track-album">Saltwater Static</span>
  <button class="like-btn" aria-label="Save to your library">♡</button>
  <span class="track-time">3:42</span>
</div>
```

```css
.track-row {
  display: grid; grid-template-columns: 32px 40px 4fr 3fr 40px 48px;
  align-items: center; gap: 16px; padding: 8px 16px; border-radius: 4px;
  font-variant-numeric: tabular-nums;
}
.track-row:hover { background: rgba(255,255,255,.08); }
.track-num { color: #B3B3B3; font-size: 14px; text-align: right; }
.track-row:hover .track-num { color: transparent; position: relative; }
/* swap the number for a play glyph on hover */
.track-row:hover .track-num::after { content: "▶"; color: #fff; font-size: 11px;
  position: absolute; inset: 0; display: grid; place-items: center; }
.track-name { color: #fff; font-size: 16px; font-weight: 400; margin: 0; }
.track-artist, .track-album { color: #B3B3B3; font-size: 14px; margin: 0; }
.track-name:hover, .track-artist:hover { text-decoration: underline; }
.track-time { color: #B3B3B3; font-size: 14px; }
.track-row.playing .track-name { color: #1ED760; }
```

### 5. Now-playing bar

```html
<footer class="player">
  <div class="player-track">
    <img src="cover.jpg" alt="">
    <div><p>Neon Coastline</p><p class="dim">Glass Harbor</p></div>
  </div>
  <div class="player-center">
    <div class="controls">
      <button>⏮</button>
      <button class="play-btn">▶</button>
      <button>⏭</button>
    </div>
    <div class="progress"><span class="time">1:12</span>
      <div class="bar"><div class="fill" style="width:34%"></div></div>
      <span class="time">3:42</span>
    </div>
  </div>
  <div class="player-right"><div class="vol"><div class="bar"><div class="fill" style="width:70%"></div></div></div></div>
</footer>
```

```css
.player {
  display: grid; grid-template-columns: 1fr 2fr 1fr; align-items: center;
  height: 88px; padding: 0 16px; background: #000;
  border-top: 1px solid #282828; box-shadow: 0 -8px 24px rgba(0,0,0,.5);
}
.bar { height: 4px; background: #404040; border-radius: 2px; position: relative; }
.fill { height: 100%; background: #B3B3B3; border-radius: 2px; }
.bar:hover .fill { background: #1ED760; }
```

### 6. Pill CTA button

```html
<button class="cta">Get Premium</button>
```

```css
.cta {
  background: #fff; color: #191414; border: none; border-radius: 999px;
  padding: 14px 32px; font-size: 13px; font-weight: 700;
  letter-spacing: 1.4px; text-transform: uppercase; cursor: pointer;
  transition: transform .15s, background .15s;
}
.cta:hover { transform: scale(1.04); background: #f0f0f0; }
.cta.green { background: #1ED760; color: #000; }
.cta.green:hover { background: #1DB954; }
```

### 7. Explicit badge

```css
.badge-e {
  display: inline-grid; place-items: center;
  width: 16px; height: 16px; border-radius: 2px;
  background: #B3B3B3; color: #121212;
  font-size: 10px; font-weight: 700; line-height: 1;
}
```

### 8. Search input (pill)

```css
.search {
  background: #242424; border: 1px solid transparent; border-radius: 999px;
  padding: 12px 16px 12px 44px; color: #fff; font-size: 14px; width: 360px;
  transition: border-color .2s, background .2s;
}
.search::placeholder { color: #B3B3B3; }
.search:hover { background: #2a2a2a; border-color: #404040; }
.search:focus { outline: 2px solid #fff; background: #2a2a2a; }
```

### 9. Equalizer (playing state)

```html
<span class="eq"><i></i><i></i><i></i></span>
```

```css
.eq { display: inline-flex; align-items: flex-end; gap: 2px; height: 14px; }
.eq i { width: 3px; background: #1ED760; animation: eq 1s ease-in-out infinite; }
.eq i:nth-child(2) { animation-delay: .25s; }
.eq i:nth-child(3) { animation-delay: .5s; }
@keyframes eq { 0%,100% { height: 4px; } 50% { height: 14px; } }
.eq.paused i { animation-play-state: paused; height: 4px; }
```

## Motion

- Fast and functional: hover states `150–300 ms ease`; cards fade/slide up on
  reveal; the play button scales `1 → 1.04` on hover. ⚠️ (community-observed;
  no public motion spec)
- Signature transitions: the track number swaps to a play glyph on row hover;
  the card's circular play button slides up and fades in on card hover.
- Marketing motion pulses type like an audio wave (Spotify Mix launch film),
  but product UI keeps animation minimal so playback stays the star.

## Do / Don't

- ✅ Use `#1ED760` only for play/pause controls, the active nav item, CTAs,
  and progress fill. ❌ Never use green as a background or decorative wash.
- ✅ Keep every surface charcoal and let cover art be the only other color.
  ❌ Never introduce a second accent color next to the green.
- ✅ Make CTA and nav labels UPPERCASE with 1.4–2 px letter-spacing.
  ❌ Never sentence-case button labels or use default letter-spacing.
- ✅ Use full pills for buttons/search and true circles for play controls.
  ❌ Never use small-radius rectangles for primary actions.
- ✅ Apply the duotone treatment to brand/marketing photography.
  ❌ Never place the green logo on duotoned photography (brand guide: black,
  white, or non-duotoned photography only).
- ✅ Start playlist pages with a cover-art gradient hero, then the track table.
  ❌ Never ship a light theme for the listening experience — dark is the identity.
- ✅ Mark secondary text in `#B3B3B3` and tabular numerals in track tables.
  ❌ Never set body text in pure black on white for product UI.

## Copy voice (for brand styles)

Bold, music-first, never corporate. Short declarative bursts; the music is
always the hero, never the app.

- "Music for every moment."
- "Your library, on shuffle."
- "New drops. Zero skips."
- "Made for Maya. Updated every morning."

---

**Sources:** Spotify partner brand guidelines v1.4 (are.na PDF: logo misuse +
green-on-black/white/photography rules); shadcn.io/design/spotify
(dark-first rationale, green usage rules, fallback stack); opencoworkai
open-codesign DESIGN.md (color tokens, type scale, 3-pane layout);
vocal.media (Circular/Lineto typography history); marketing-interactive.com
(Spotify Mix bespoke typeface, Dinamo Typefaces).
