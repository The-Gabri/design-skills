---
name: broadsheet
description: Classic newspaper broadsheet design — blackletter nameplate, six-column grid, serif display headlines, kickers, decks, rules and folios. Use when a page should read like a printed front page.
---

# Broadsheet

Classic newspaper broadsheet: the look of a printed front page — ink on newsprint,
everything hung on a multi-column grid, hierarchy carried by type size and position
rather than color. Modeled on the NYT/Guardian print traditions.

## Confidence legend
- ✅ = documented in the cited source (style guides, rate cards, published histories).
- 🟡 = cross-referenced across ≥2 independent sources, no single canonical citation.
- ⚠️ = community approximation — useful, not dogma. Do not present as official.

## Principles

1. **Hierarchy is typographic, not chromatic.** Size, weight, and position carry
   meaning; color is scarce and earned. The lead story is the biggest, not the
   brightest. 🟡
2. **The grid is the page.** Every story is a rectangle measured in columns;
   nothing floats, nothing bleeds casually. 🟡
3. **The nameplate never changes.** It is set once — blackletter, full measure —
   and becomes the brand. The New York Times masthead kept its blackletter form
   for over a century; the only major change was *removing* the final period in
   1967. ✅
4. **Above the fold earns the glance; below the fold earns the reader.** The top
   half of the page is a poster: nameplate, one dominant story, teasers. Depth
   lives below. 🟡
5. **Restraint signals authority.** Hairline rules, justified columns, quiet
   gutters — the visual calm is what makes the paper feel trustworthy. 🟡
6. **Print has furniture.** Ears, skyboxes, kickers, cutlines, jump lines, folios:
   small fixed elements with fixed jobs, repeated issue after issue. ✅

## Color

Newsprint is printed CMYK (or greyscale); spot color is rationed. ✅

| Token | Hex | Role | Confidence |
|---|---|---|---|
| `--paper` | `#F5F1E6` | Newsprint background | ⚠️ |
| `--paper-dim` | `#ECE7D8` | Aged/recycled tint, sidebars | ⚠️ |
| `--ink` | `#1A1A1A` | Body text, headlines (100K in print) | ✅ |
| `--ink-soft` | `#3D3D3D` | Decks, cutlines | ⚠️ |
| `--rule` | `#9A958A` | Hairlines, column rules | ⚠️ |
| `--accent` | `#A31F1F` | Spot red: skyboxes, section labels, folios | ⚠️ |
| `--sky` | `#EFEAD9` | Skybox/teaser tint | ⚠️ |

Rules: never color body text; never more than one spot color on a page;
photos and art print greyscale unless the edition is full color. ✅

## Typography

- **Display serif — the headline voice.** The New York Times unified its print
  headlines on *Cheltenham* in 2003: Matthew Carter drew multiple weights plus a
  heavily condensed width to replace the Victorian mix of faces. ✅ Cheltenham was
  designed for newspapers (large x-height, short descenders — more words per
  column). ✅ Free substitutes: **Bitter** (slab, print-like) 🟡,
  system stack: `Georgia, 'Times New Roman', serif` ⚠️.
- **Body serif.** NYT sets body in *Imperial* (custom). ✅ Substitutes: Georgia,
  Source Serif. Body is justified, paragraphs indented (no blank lines between),
  hyphenation on, measure ~39–45 characters per column. 🟡
- **Sans for labels.** Kickers, bylines, cutlines, folios: a grotesque
  (Franklin Gothic at the NYT; Guardian uses its own Egyptian/Humanist sans). ✅
  Substitute: `Helvetica, Arial, sans-serif` ⚠️.
- **Nameplate.** Blackletter, centered, spanning the full measure. The NYT
  blackletter has unique spurs and a diamond-shaped terminal — a protected
  trademark; never imitate a real paper's nameplate, style your own. ✅

### Type scale (print points; web values scale up ~1.6×)

| Element | Print size | Web equiv. | Notes | Confidence |
|---|---|---|---|---|
| Nameplate | ~120pt+ | 84–120px | Blackletter, full measure | 🟡 |
| Banner head | 72–120pt | 56–84px | Rare; huge news only | 🟡 |
| Main head | 30–60pt | 34–56px | Serif, sentence case (NYT uses all-caps — one of few still doing so ✅) | ✅/🟡 |
| Kicker | 10–12pt | 11–13px | Sans, small caps, letterspaced | 🟡 |
| Deck | 14–18pt | 18–24px | Serif italic or regular, one–two sentences | 🟡 |
| Body | 9.5–10.5pt | 15–17px | Justified, indented, ~10% extra leading | 🟡 |
| Byline | 8–9pt | 12–13px | Sans caps: "By FIRST LAST" | 🟡 |
| Cutline | 7.5–8.5pt | 12px | Sans; explains, doesn't repeat | 🟡 |
| Folio | 6–8pt | 10–11px | Sans caps: name, date, page, price | 🟡 |

## Layout & spacing

- **The six-column grid.** Standard US broadsheet page: 12 in wide × 22 in tall
  folded ✅; modern print area after the 2007 downsizing: **6 columns over
  11.55 in** (NYT rate card, 2007). ✅ One column = **12 picas 2 points**
  (~2.03 in) on a six-column grid. ✅
- **Gutters are sunken, not ruled.** Columns are divided by ~1 pica of white
  space; visible column rules are rare. ✅/🟡
- **Rules have weights and jobs:** hairline 0.5pt separates stories; a double
  rule (thick over thin, ~2pt/0.5pt) sits under the nameplate; a heavy bar
  (~3–4pt) can crown a section. 🟡
- **Margins:** ~10 mm top/bottom/outside on a digital broadsheet page. ⚠️
- **The fold:** the top half of the page is seen first on newsstands; the lead
  story's headline and art must land above it. ✅

## Components

### 1. Nameplate + folio bar

```html
<header class="paper-head">
  <div class="skyline">
    <span class="ear">LATE EDITION</span>
    <span class="folio-top">Vol. CXLII · No. 47 · Friday, October 2, 2026</span>
    <span class="ear price">50¢</span>
  </div>
  <h1 class="nameplate">The Morning Chronicle</h1>
  <div class="rule-double"></div>
  <div class="folio-bar">
    <span>Established 1884</span><span>chronicle.example</span><span>Weather: Fair, 68°</span>
  </div>
  <div class="rule-single"></div>
</header>
```

```css
.nameplate{
  font-family:"Old English Text MT","Cloister Black",Georgia,serif;
  font-size:clamp(56px,10vw,110px); text-align:center; margin:0; line-height:1;
  letter-spacing:.01em; color:#1A1A1A;
}
.skyline{display:flex; justify-content:space-between; align-items:baseline;
  font:600 11px/1.4 Helvetica,Arial,sans-serif; text-transform:uppercase;
  letter-spacing:.08em; border-bottom:3px solid #1A1A1A; padding-bottom:4px;}
.rule-double{border-top:3px solid #1A1A1A; border-bottom:1px solid #1A1A1A;
  height:3px; margin:6px 0;}
.rule-single{border-top:1px solid #9A958A; margin:4px 0;}
.folio-bar{display:flex; justify-content:space-between;
  font:600 10px/1.6 Helvetica,Arial,sans-serif; text-transform:uppercase;
  letter-spacing:.12em; color:#3D3D3D;}
```

### 2. Article header stack (kicker / headline / deck / byline / dateline)

```html
<article>
  <p class="kicker">City Hall</p>
  <h2 class="headline">Council Votes 7–2 to Restore the Crosstown Trolley</h2>
  <p class="deck">The $240 million plan would bring rails back to Grand Avenue
  by 2029, seventy-five years after the last streetcar ran.</p>
  <p class="byline">By Elena Marsh</p>
  <p class="dateline">CITY HALL — <span>The City Council voted 7 to 2…</span></p>
</article>
```

```css
.kicker{font:700 12px/1.3 Helvetica,Arial,sans-serif; text-transform:uppercase;
  letter-spacing:.14em; color:#A31F1F; margin:0 0 6px;}
.headline{font-family:Georgia,'Times New Roman',serif; font-weight:700;
  font-size:clamp(34px,4.5vw,54px); line-height:1.02; letter-spacing:-.01em;
  margin:0 0 10px; color:#1A1A1A;}
.deck{font:italic 400 19px/1.4 Georgia,serif; color:#3D3D3D; margin:0 0 10px;}
.byline{font:700 12px/1.4 Helvetica,Arial,sans-serif; text-transform:uppercase;
  letter-spacing:.1em; margin:0 0 8px;}
.dateline{font:700 12px/1.4 Helvetica,Arial,sans-serif; text-transform:uppercase;
  letter-spacing:.06em; margin:0;}
.dateline span{font:400 15px/1.55 Georgia,serif; text-transform:none;
  letter-spacing:0; color:#1A1A1A;}
```

### 3. Multi-column story block with drop cap and jump line

```html
<div class="story-cols">
  <p class="lede">The City Council voted 7 to 2 on Thursday night…</p>
  <p>Supporters called it the most ambitious transit project…</p>
  <p>Opponents warned the cost estimates were "aspirational"…</p>
</div>
<p class="jump">Continued on Page A6.</p>
```

```css
.story-cols{columns:3; column-gap:22px; column-rule:1px solid #D8D3C2;
  font:400 15.5px/1.55 Georgia,serif; color:#1A1A1A; text-align:justify;
  hyphens:auto;}
.story-cols p{margin:0 0 .7em; text-indent:1.2em;}
.story-cols p.lede{text-indent:0;}
.story-cols p.lede::first-letter{font-size:3.2em; float:left; line-height:.85;
  padding-right:6px; font-weight:700;}
.jump{font:italic 700 12.5px/1.4 Helvetica,Arial,sans-serif; margin:8px 0 0;
  border-top:1px solid #9A958A; padding-top:6px;}
```

### 4. Photo with cutline

```html
<figure class="art">
  <div class="art-frame"><!-- halftone SVG or img here --></div>
  <figcaption><span class="cut">A rendering of the proposed streetcar on Grand
  Avenue near the Central Library.</span>
  <span class="credit">Illustration by The Morning Chronicle</span></figcaption>
</figure>
```

```css
.art{margin:12px 0;}
.art-frame{border:1px solid #1A1A1A; background:#DAD5C4;}
.art figcaption{font:400 12px/1.45 Helvetica,Arial,sans-serif; color:#3D3D3D;
  padding-top:6px; border-top:3px solid #1A1A1A; margin-top:0;}
.art .credit{font-size:10px; text-transform:uppercase; letter-spacing:.08em;
  color:#9A958A; display:block; margin-top:2px;}
```

### 5. Pull quote

```html
<blockquote class="pull">"Seventy-five years ago we tore the rails out.
This time we are putting them back on purpose."</blockquote>
```

```css
.pull{font:italic 700 22px/1.3 Georgia,serif; color:#1A1A1A; margin:14px 0;
  padding:10px 0; border-top:3px solid #1A1A1A; border-bottom:1px solid #9A958A;
  quotes:"“" "”";}
```

### 6. Story separator rules

```css
.rule-hair{border:0; border-top:1px solid #9A958A; margin:14px 0;}
.rule-heavy-double{border:0; border-top:4px solid #1A1A1A; position:relative;
  margin:16px 0;}
.rule-heavy-double::after{content:""; display:block; border-top:1px solid #1A1A1A;
  margin-top:2px;}
```

### 7. "Inside" index box

```html
<aside class="index-box">
  <h3>Inside</h3>
  <ul>
    <li><span>Metro</span><span>A3</span></li>
    <li><span>Business</span><span>B1</span></li>
    <li><span>Opinion</span><span>A14</span></li>
    <li><span>Arts</span><span>C1</span></li>
  </ul>
</aside>
```

```css
.index-box{border:1px solid #1A1A1A; padding:0; background:#F5F1E6;}
.index-box h3{font:700 12px/1 Helvetica,Arial,sans-serif; text-transform:uppercase;
  letter-spacing:.14em; background:#1A1A1A; color:#F5F1E6; margin:0; padding:8px 10px;}
.index-box ul{list-style:none; margin:0; padding:6px 10px 10px;}
.index-box li{display:flex; justify-content:space-between;
  font:400 13px/1.9 Georgia,serif; border-bottom:1px dotted #9A958A;}
.index-box li:last-child{border-bottom:0;}
```

## Motion

A broadsheet is ink on paper: it defines no motion language. On screen, keep
motion near zero — instant or ≤150 ms crossfades only, no parallax, no bounce.
⚠️

## Do / Don't

| Do | Don't |
|---|---|
| Span the nameplate across the full measure, ears flanking it | Shrink the nameplate into a top-left logo like a startup site |
| Justify body copy in narrow columns with hyphenation on | Center-align body text, or leave ragged-right at 60+ characters |
| Separate stories with hairline and double rules | Use thick colored dividers, cards, or drop shadows |
| Set kickers in letterspaced small-cap sans above the headline | Stack two competing serif headlines of similar size |
| Give one story the dominant position above the fold, with a jump line | Give five stories equal weight so the eye lands nowhere |
| Write cutlines that say something the photo doesn't ("who is third from left") | Repeat the headline under the photo |
| Reserve spot red for skyboxes, section labels, and folio accents | Set body text, decks, or bylines in color |

## Copy voice

Newspaper copy is terse, declarative, and present-tense. Headlines use active
verbs and drop articles: **"Council Votes 7–2 to Restore the Crosstown Trolley"**,
not "The Council Has Voted…". Kickers give section context in one or two words
("CITY HALL", "MARKETS"). The deck expands the headline in one sentence and never
repeats it verbatim. Bylines: "By Elena Marsh". Datelines: "CITY HALL —" (caps
city, em dash, then the lede). Cutlines identify, don't editorialize.

Example strings:
- Kicker + head: `MARKETS` / `Chronicle 500 Closes Above 6,400 for the First Time`
- Deck: `The index gained 1.2 percent as chipmakers rallied on stronger orders.`
- Cutline: `A rendering of the proposed streetcar on Grand Avenue near the Central Library.`

## Sources

- NYT 2007 broadsheet ad specs (6 columns, 11.55 in print width):
  https://assets.ctfassets.net/jxri9wzjewim/6hOtcdUEFRBSys2gs8iwcV/11e80a5c0894932115e116e360741307/nytimes_broadsheet_v072820.pdf
- Newspaper format dimensions (US broadsheet 12 in × 22 in folded):
  https://en.wikipedia.org/wiki/Broadsheet_(newspaper)
- Cheltenham / NYT 2003 typographic unification (Carter, Bodkin):
  https://en.wikipedia.org/wiki/Cheltenham_(typeface)
- NYT masthead history (blackletter trademark, 1967 period removal by Ed Benguiat):
  https://vectree.io/pdf/c/nyt-brand-history
- NYT stylebook history (all-caps headlines, "A head"):
  https://www.cjr.org/language_corner/new-york-times-stylebook.php
- Front-page anatomy (nameplate, kicker, deck, byline, dateline, cutline, jump line):
  https://www.scribd.com/document/522484653/Parts-of-the-Frontpage
- One-column measure on a six-column grid (12 picas 2 points):
  https://2.files.edl.io/rNnyp603mHepuPkRfmvrjaZ0s70VNYoEgMjZB2VKbzOePC.pdf
