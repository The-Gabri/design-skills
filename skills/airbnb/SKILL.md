---
name: airbnb
description: Airbnb brand and product style — Rausch red, warm neutrals, Cereal type, photo-led listing cards. Use for travel, stays, and hospitality UIs.
---

# Airbnb — brand and product style

Airbnb's design language is a generous, photography-led consumer marketplace: a
white canvas where property photos carry the visual weight, one voltage of
warm red (Rausch) reserved for moments of action, and soft rounded geometry
everywhere. The brand promise is *belonging* — the UI should feel like a
welcoming home, never a cold dashboard.

## Principles

1. **Photography leads, chrome follows.** The most important visual on any
   screen is a photo of a place. UI chrome (cards, pills, nav) is quiet
   white/gray so photography can breathe. Never let decorative UI compete with
   imagery.
2. **One accent, used scarcely.** Rausch red carries every primary CTA, the
   search orb, and the saved-heart fill — and almost nothing else. Most pages
   are ~90% white + ink with one or two red moments. If red covers more than
   ~10% of the viewport, it's wrong.
3. **Warm, never cold.** Grays are warm (never blue-gray), blacks are soft
   (`#222222`, never pure `#000000`), corners are rounded. The system should
   feel human and hospitable — closer to a well-kept guesthouse than to a
   fintech app.
4. **Travel-magazine pacing.** Generous vertical rhythm between sections,
   unhurried scrolling, editorial-style groupings ("Guest favorites",
   "Trending in…"). Density is fine inside the listing grid, but sections
   breathe.
5. **Modest typography, confident hierarchy.** Display type stays small
   (22–28px) and light-to-medium weight — the photography provides the heft.
   Emphasis comes from weight contrast and spacing, not size or color.
6. **Belonging in every word.** Copy is warm, first-person-plural, and
   reassuring. It reduces anxiety about staying in a stranger's home.

## Color

Legend: ✅ official/documented · 🟡 cross-referenced across teardowns · ⚠️
community approximation.

| Token | Hex | Role | Legend |
|---|---|---|---|
| Rausch | `#FF5A5F` | Brand red — logo, search orb, heart fill, primary CTAs | ✅ |
| Primary Coral | `#FF385C` | Post-2020 product CTA red (replaces Rausch in the app UI) | 🟡 |
| Rausch hover | `#FF7E82` | Button/heart hover tint | ⚠️ |
| Rausch pressed | `#E04C51` | Pressed state | ⚠️ |
| Ink | `#222222` | Primary text (never pure black) | 🟡 |
| Foggy | `#767676` | Secondary text (DLS name) | ✅ |
| Hof | `#484848` | Tertiary text (DLS name) | ✅ |
| Canvas | `#FFFFFF` | Page background | ✅ |
| Warm surface | `#F7F7F7` | Secondary background, section fills | 🟡 |
| Hairline | `#EBEBEB` | Dividers, card borders | 🟡 |
| Border strong | `#DDDDDD` | Inputs, segmented controls | 🟡 |
| Babu | `#00A699` | Teal — trust/success accents (DLS name) | ✅ |
| Arches | `#FC642D` | Orange — highlights, badges (DLS name) | ✅ |
| Star gold | `#FFB400` | Rating stars | 🟡 |
| Success | `#008A05` | Confirmations | 🟡 |
| Error | `#C13515` | Form errors, destructive | 🟡 |

Rules: never use pure `#000000` or cool blue-grays (`#F5F5F5` loses the
warmth). Red is for action only — never body text, never large surfaces,
never decoration.

## Typography

- **Airbnb Cereal** ✅ — custom geometric sans by Dalton Maag (2018), built
  for warmth and approachability. Variable font; product weights 400 / 500 /
  700. Proprietary, not on Google Fonts.
- **Closest free substitute:** **Nunito Sans** ⚠️ — rounded, warm humanist
  sans with a similar friendly geometry. Load 400/600/700/800 from Google
  Fonts, system stack fallback: `-apple-system, "Segoe UI", Roboto, sans-serif`.
- Historic in-house fallback was **Circular** 🟡.

Type scale (modest by design 🟡):

| Use | Size / weight | Example |
|---|---|---|
| Hero display | 28–32px / 700 | "Inspiration for your next getaway" |
| Section title | 22px / 600 | "Guest favorites in Lisbon" |
| Card title | 15px / 600 | Listing location line |
| Body | 14–16px / 400 | Descriptions, meta lines |
| Small / caption | 12px / 400–500 | "Total before taxes", dates |

Body line-height ~1.43. Letter-spacing stays neutral (0) — no tight display
tracking, no wide caps except tiny labels.

## Layout & spacing

- **8px base unit** ✅ (documented DLS). Spacing scale runs
  2 / 4 / 8 / 12 / 16 / 24 / 32 / 64. Major section rhythm: 64px 🟡.
- **Grid:** listing grid is responsive, 2–6 columns on desktop, generous
  gutters (24px). Cards stack full-width on mobile — never cramped two-up on
  small screens.
- **Radius — soft everywhere** 🟡: buttons 8px · listing photos 12–14px ·
  badges 14px · category chips 32px · search bar and orbs fully pill/circle.
  Essentially no hard corners except the page grid itself.
- **Borders:** 1px hairlines (`#EBEBEB`) for dividers; segmented controls get
  `#DDDDDD` outlines.
- **Elevation:** capped at one shadow tier 🟡 —
  `box-shadow: rgba(0,0,0,0.02) 0 0 0 1px, rgba(0,0,0,0.04) 0 2px 6px, rgba(0,0,0,0.1) 0 4px 8px`
  — used only on hover-floated cards, dropdowns, and the search pill.
- **Search bar prominence:** the search pill gets the most vertical space in
  the header — finding a destination is the primary action of the product.

## Components

### 1. Header + product tabs
White sticky header. Rausch lowercase wordmark left; center tabs
(Stays / Experiences / Services) with a 2px Rausch underline on the active
tab; right side: "Become a host" text link, globe icon, and a pill
(hamburger + avatar circle) that opens the account menu.

```html
<header class="abnb-header">
  <a class="abnb-logo" href="#">airbnb</a>
  <nav class="abnb-tabs">
    <a class="is-active" href="#">Stays</a>
    <a href="#">Experiences</a>
    <a href="#">Services</a>
  </nav>
  <div class="abnb-actions">
    <a href="#">Become a host</a>
    <button class="abnb-menu" aria-label="Menu">
      <svg><!-- hamburger --></svg><span class="abnb-avatar">G</span>
    </button>
  </div>
</header>
```
```css
.abnb-header{position:sticky;top:0;background:#fff;display:flex;align-items:center;
  justify-content:space-between;padding:0 24px;height:80px;border-bottom:1px solid #EBEBEB;z-index:50}
.abnb-logo{color:#FF5A5F;font-weight:800;font-size:26px;letter-spacing:-1px;text-decoration:none}
.abnb-tabs{display:flex;gap:32px}
.abnb-tabs a{color:#717171;text-decoration:none;font-weight:500;padding:28px 0}
.abnb-tabs a.is-active{color:#222;font-weight:600;border-bottom:2px solid #FF5A5F}
.abnb-menu{display:flex;align-items:center;gap:10px;border:1px solid #DDDDDD;
  border-radius:999px;padding:6px 6px 6px 12px;background:#fff;cursor:pointer}
.abnb-avatar{width:32px;height:32px;border-radius:50%;background:#717171;color:#fff;
  display:grid;place-items:center;font-weight:600}
```

### 2. Search pill (Where / When / Who + orb)
The signature control: a full-pill white bar with a soft shadow, divided by
1px hairlines into labeled segments, terminated by a circular Rausch search
orb with a magnifier.

```html
<form class="abnb-search" role="search">
  <label class="abnb-seg"><span>Where</span><input placeholder="Search destinations"></label>
  <label class="abnb-seg"><span>Check in</span><input placeholder="Add dates"></label>
  <label class="abnb-seg"><span>Check out</span><input placeholder="Add dates"></label>
  <label class="abnb-seg"><span>Who</span><input placeholder="Add guests"></label>
  <button class="abnb-orb" aria-label="Search">
    <svg viewBox="0 0 24 24" width="18" height="18" fill="none" stroke="#fff" stroke-width="3">
      <circle cx="11" cy="11" r="7"/><path d="M16 16l5 5"/>
    </svg>
  </button>
</form>
```
```css
.abnb-search{display:flex;align-items:stretch;background:#fff;border:1px solid #DDDDDD;
  border-radius:999px;box-shadow:0 1px 2px rgba(0,0,0,.08),0 4px 12px rgba(0,0,0,.05);
  max-width:850px;margin:0 auto;overflow:hidden}
.abnb-seg{flex:1;padding:12px 24px;display:flex;flex-direction:column;cursor:pointer;border-radius:999px}
.abnb-seg + .abnb-seg{border-left:1px solid #EBEBEB}
.abnb-seg:hover{background:#F7F7F7}
.abnb-seg span{font-size:12px;font-weight:700}
.abnb-seg input{border:0;outline:0;font-size:14px;color:#222;background:transparent}
.abnb-seg input::placeholder{color:#717171}
.abnb-orb{width:48px;height:48px;margin:8px;border:0;border-radius:50%;
  background:#FF5A5F;display:grid;place-items:center;cursor:pointer;flex:none}
.abnb-orb:hover{background:#FF7E82}
```

### 3. Category bar
Horizontal scrollable strip of icon + label chips (Amazing views, Cabins,
Beachfront, Tiny homes, Castles, Treehouses…). Selected chip gets a 2px
ink/black sliding underline — labels stay gray, never filled pills.

```html
<div class="abnb-cats" role="tablist">
  <button class="abnb-cat is-active" role="tab" aria-selected="true">
    <svg><!-- simple line icon --></svg><span>Cabins</span>
  </button>
  <!-- … -->
</div>
```
```css
.abnb-cats{display:flex;gap:32px;overflow-x:auto;padding:12px 24px;border-bottom:1px solid #EBEBEB}
.abnb-cat{display:flex;flex-direction:column;align-items:center;gap:8px;background:none;border:0;
  color:#717171;font-size:12px;font-weight:600;cursor:pointer;padding-bottom:10px;white-space:nowrap}
.abnb-cat svg{width:26px;height:26px;stroke:currentColor;fill:none;stroke-width:1.6}
.abnb-cat.is-active{color:#222;border-bottom:2px solid #222}
```

### 4. Listing card (the anatomy)
Photo-first: image block (4:3, 12px radius) with heart top-right, "Guest
favorite" badge top-left, carousel dots; then 4–5 lines of meta: location
(bold) + ★ rating right-aligned, host/distance (gray), dates (gray), price
(bold nightly) + total line.

```html
<article class="abnb-card">
  <div class="abnb-photo">
    <img src="cabin.jpg" alt="A-frame cabin among pines">
    <span class="abnb-badge">Guest favorite</span>
    <button class="abnb-heart" aria-label="Save to wishlist" aria-pressed="false">
      <svg viewBox="0 0 24 24"><path d="M12 21.35l-1.45-1.32C5.4 15.36 2 12.28 2 8.5 2 5.42 4.42 3 7.5 3c1.74 0 3.41.81 4.5 2.09C13.09 3.81 14.76 3 16.5 3 19.58 3 22 5.42 22 8.5c0 3.78-3.4 6.86-8.55 11.54L12 21.35z"/></svg>
    </button>
    <div class="abnb-dots"><i class="on"></i><i></i><i></i></div>
  </div>
  <div class="abnb-meta">
    <div class="abnb-row"><strong>Joshua Tree, California</strong><span class="abnb-rating">★ 4.96</span></div>
    <p>Desert views · 2 bedrooms</p>
    <p>Jan 12 – 17</p>
    <p><strong>$214</strong> night · <span class="abnb-total">$1,284 total</span></p>
  </div>
</article>
```
```css
.abnb-card{font-size:15px}
.abnb-photo{position:relative;aspect-ratio:4/3;border-radius:12px;overflow:hidden;background:#F7F7F7}
.abnb-photo img{width:100%;height:100%;object-fit:cover;display:block}
.abnb-badge{position:absolute;top:12px;left:12px;background:rgba(255,255,255,.95);
  border-radius:14px;padding:5px 12px;font-size:13px;font-weight:600}
.abnb-heart{position:absolute;top:8px;right:8px;background:none;border:0;cursor:pointer;padding:4px}
.abnb-heart svg{width:26px;height:26px;fill:rgba(0,0,0,.45);stroke:#fff;stroke-width:2;transition:transform .15s ease-out}
.abnb-heart[aria-pressed="true"] svg{fill:#FF5A5F;stroke:#FF5A5F;transform:scale(1.12)}
.abnb-dots{position:absolute;bottom:10px;left:50%;transform:translateX(-50%);display:flex;gap:5px}
.abnb-dots i{width:6px;height:6px;border-radius:50%;background:rgba(255,255,255,.6)}
.abnb-dots i.on{background:#fff}
.abnb-meta{padding-top:12px;display:grid;gap:2px}
.abnb-meta p{margin:0;color:#717171}
.abnb-row{display:flex;justify-content:space-between}
.abnb-rating{font-weight:400;white-space:nowrap}
.abnb-total{color:#717171;text-decoration:underline}
```

### 5. Price toggle ("Display total before taxes")
A small right-aligned switch above results: nightly price vs. total price.
Understated 12–14px label, native-feeling toggle — never a big banner.

### 6. Reserve bar (sticky booking footer)
On a listing page, a sticky bottom bar: total price + date range left,
full-width Rausch pill button "Reserve" right. On cards, the price line
keeps "**$X** night" bold with the total as a quiet underlined link.

```css
.abnb-reserve{display:flex;align-items:center;justify-content:space-between;
  padding:16px 24px;border-top:1px solid #EBEBEB;background:rgba(255,255,255,.92);
  backdrop-filter:blur(8px);position:sticky;bottom:0}
.abnb-cta{background:#FF5A5F;color:#fff;border:0;border-radius:8px;
  padding:14px 28px;font-size:16px;font-weight:600;cursor:pointer}
.abnb-cta:hover{background:#FF7E82}
```

### 7. Date picker
Clean month grid, 15px day cells, generous 40px row height; selected range
gets a light Rausch-tinted wash (`#FFF1F2` ⚠️) with solid Rausch start/end
circles and white numerals. Past dates are `#B0B0B0` and inert.

### 8. Map pin
On the map, listings appear as white price pills (`$214`) with a 1px ink
shadow; the hovered/selected pin flips to solid ink (`#222`) with white text.
Rausch is not used on the map — price clarity wins over brand color.

```css
.abnb-pin{background:#fff;border-radius:999px;padding:6px 10px;font-weight:700;font-size:14px;
  box-shadow:0 2px 8px rgba(0,0,0,.25);cursor:pointer;border:0}
.abnb-pin.is-active{background:#222;color:#fff}
```

### 9. Reviews row
`★ 4.96 · 128 reviews` — star in `#FFB400` ⚠️ (or ink ★ in product), rating
bold, count gray and underlined. "Guest favorite" badge (white pill,
13px/600) marks the top 10% of homes — social proof is a first-class UI
element.

### 10. Footer
Full-width, top hairline, three link columns (Support / Hosting / Airbnb) in
14px ink with gray hover, then a bottom bar: "© 2026 · Privacy · Terms ·
Sitemap", language/currency pickers, and social icons. No card surface, no
shadow — clean text columns over white.

## Motion

No published motion spec — keep it quiet: 150–250ms `ease-out` fades and
small slides; the only signature moves are the wishlist heart's fill-and-pop
and the carousel dots' fade. Nothing bounces, nothing parallax-scrolls.

## Do / Don't

- ✅ Do let a large photo be the first thing on the screen; keep chrome quiet.
- ❌ Don't let Rausch cover more than ~10% of any viewport — no red
  backgrounds, no red body text, no red decoration.
- ✅ Do use warm grays (`#F7F7F7`, `#717171`); ❌ don't use cool blue-grays
  or pure black — they read as cold and corporate, the opposite of belonging.
- ✅ Do round everything: 8px buttons, 12px photos, full-pill search.
- ❌ Don't set display type heavy — headlines at 700 max, usually 500–600 at
  modest sizes; the photography provides the visual weight.
- ✅ Do show the total price ("$1,284 total before taxes") next to the
  nightly rate — price transparency is part of the trust contract.
- ❌ Don't use generic star-yellow review widgets; Airbnb's rating row is
  `★ 4.96` in plain text with an underlined review count.
- ✅ Do write CTAs as calm imperatives ("Reserve", "Show all photos",
  "Message host"); ❌ don't use hype ("Book NOW!!!", "Limited offer!!!").

## Copy voice

Warm, plain-spoken, belonging-first. Short sentences. It reassures the guest
and flatters the host, never shouts.

- "Belong anywhere." — the brand line; use the sentiment, not hype.
- "Guest favorite — one of the most loved homes on Airbnb, based on ratings,
  reviews, and reliability."
- "Rare find — this place is usually booked."
- Search placeholder: "Search destinations", date placeholder: "Add dates",
  guest placeholder: "Add guests". Empty states: "No exact matches — try
  adjusting your dates or exploring the map."
