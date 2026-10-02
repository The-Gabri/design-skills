---
name: brutalism
description: Raw web brutalism — system fonts, default blue links, honest unstyled HTML, no decoration. Use for pages that reject corporate polish: zines, hacker blogs, manifestos, raw indexes.
---

# Brutalism

Web brutalism is the deliberate rejection of corporate web polish. Documented by
the gallery at brutalistwebsites.com (founded by Pascal Deville, 2014) as "sites
that broke corporate web design conventions" — default browser styling,
unstyled links, system fonts. Its architectural namesake (béton brut: raw
concrete, Reyner Banham 1955) translates to the web as **honesty of materials**:
let the HTML, the links, and the document hierarchy show through instead of
covering them up with decoration. A major strand descends from punk zine
photocopy culture and from the motherfuckingwebsite.com manifesto: the site is
the content, not the chrome.

## Principles

1. **Honesty of markup.** Use real HTML elements for what they are —
   `<h1>–<h6>`, `<table>`, `<hr>`, `<marquee>`. No div-soup pretending to be
   something else. If the page looks like raw HTML, that is the style.
2. **Content over chrome.** Decoration is suspicion. Strip everything that does
   not carry information: no hero gradients, no animations for their own sake,
   no frameworks. A stylesheet under ~100 lines is the ideal.
3. **System defaults are the palette.** System fonts, browser-default blue
   links, black text on white. The browser's own styling is a design system;
   use it.
4. **Visible structure.** Rules (`<hr>`), borders, tables, and boxes with
   default 1px lines. Grid should be visible, not implied.
5. **Speed as aesthetics.** No webfonts, no JS frameworks, no images you do
   not need. A brutalist page loads instantly — that is part of the statement.
6. **Deliberate, not accidental.** Ugly-by-default is not the goal; hostility
   to polish is. Hierarchy must still be readable: headings, lists, and links
   must be obvious at a glance.

## Color

The palette IS the browser's default palette. Tokens are CSS basic-color
defaults, documented in the CSS spec:

| Token | Hex | Role | Legend |
|---|---|---|---|
| `white` | `#FFFFFF` | page background | ✅ documented |
| `black` | `#000000` | body text, rules, borders | ✅ documented |
| `link` | `#0000EE` | unvisited links — the signature color | ✅ documented |
| `visited` | `#551A8B` | visited links | ✅ documented |
| `active` | `#FF0000` | active link state | ✅ documented |
| `gray` | `#808080` | secondary borders, disabled states | ✅ documented |
| `silver` | `#C0C0C0` | default table/field borders | ✅ documented |
| `highlight` | `#FFFF00` | the one allowed accent (marking, stickers) | ⚠️ community convention |

Use exactly two or three of these per page. One solid-color background (often
yellow, gray, or plain white) may replace `white` — "big fonts, solid-colour
backgrounds" is documented brutalist vocabulary (Landowski, ✅).

## Typography

- **Stack (in order):** `Times New Roman, Times, serif` (document voice);
  `Helvetica, Arial, sans-serif` (signage voice); `Courier New, Courier, monospace`
  (data/code voice). 🟡 cross-referenced — no webfonts, ever; the system stack
  is the point.
- **Scale:** browser defaults. `h1` big and blunt, body 16px, no finesse.
- **Weights:** `400` and `700` only. Underlines only on links.
- **Rules:** no letter-spacing tweaks, no custom line-height beyond `1.4–1.6`
  for readability. Left-align everything.

## Layout & spacing

- **Flow layout:** single column, `max-width: 60ch–80ch`, stacked blocks. No
  centered heroes.
- **Visible rules:** `hr { border: 0; border-top: 1px solid #000; }` between
  every section. Tables with `border-collapse` and 1px solid borders.
- **Spacing:** browser default margins, or crude uniform padding (`8px` /
  `16px`). No rhythm systems.
- **Radius/shadows:** `border-radius: 0`. No shadows. Ever.

## Components

Copy-pasteable HTML/CSS. Total stylesheet for all of these is under 60 lines.

### 1. Raw nav
```html
<nav>
  <a href="/">INDEX</a> ·
  <a href="/blog">BLOG</a> ·
  <a href="/projects">PROJECTS</a> ·
  <a href="/about">ABOUT</a>
</nav>
<hr>
```
```css
nav { font-family: Courier New, Courier, monospace; }
nav a { margin-right: .5em; }
```

### 2. Page header
```html
<header>
  <h1>NULL POINTER</h1>
  <p>notes on software, by someone who reads the source.</p>
</header>
<hr>
```

### 3. Marquee
```html
<marquee>NEW POST EVERY SUNDAY &middot; NO COOKIES &middot; NO TRACKING &middot; NO FEEDBACK FORM &middot;</marquee>
<hr>
```

### 4. Article list
```html
<h2>Posts</h2>
<ul>
  <li><a href="#">Why your framework is a liability</a> — 2026-09-28</li>
  <li><a href="#">I deleted 4,000 lines of CSS</a> — 2026-09-14</li>
</ul>
```

### 5. Data table
```html
<table>
  <tr><th>project</th><th>language</th><th>status</th></tr>
  <tr><td><a href="#">tinydns</a></td><td>C</td><td>done</td></tr>
  <tr><td><a href="#">rawsock</a></td><td>Rust</td><td>broken</td></tr>
</table>
```
```css
table { border-collapse: collapse; }
th, td { border: 1px solid #000; padding: 4px 8px; text-align: left; }
th { background: #C0C0C0; }
```

### 6. Bare form
```html
<form>
  <label>email:<br><input type="email" size="30"></label><br>
  <label>message:<br><textarea rows="4" cols="30"></textarea></label><br>
  <button type="submit">SEND</button>
</form>
```

### 7. Code block
```html
<pre><code>curl -s https://example.com | sh   # don't do this</code></pre>
```
```css
pre { background: #C0C0C0; padding: 8px; overflow-x: auto; }
```

### 8. Aside / sticker
```html
<aside>last updated: 2026-10-02. everything here is hand-written HTML.</aside>
```
```css
aside { background: #FFFF00; padding: 8px; display: inline-block; font-weight: bold; }
```

### 9. Footer
```html
<hr>
<footer>
  <p>no cookies. no tracking. <a href="#">view source</a> (it's short).</p>
</footer>
```

### 10. Fieldset grouping
```html
<fieldset>
  <legend>archive</legend>
  <a href="#">2026</a> <a href="#">2025</a> <a href="#">2024</a>
</fieldset>
```

## Motion

None. No transitions, no animations, no scroll effects. A `<marquee>` is the
only permitted moving element, and it is mandatory to be ironic about it.

## Do / Don't

- DO use default blue `#0000EE` links, underlined. DON'T restyle links to
  "look better" — unstyled links are the signature.
- DO use `Times New Roman` for a blog, `Courier New` for a hacker index.
  DON'T load any webfont — one `@font-face` kills the style.
- DO separate sections with visible `<hr>` rules. DON'T use whitespace-only
  section separation; whitespace minimalism belongs to another skill.
- DO ship one tiny inline script if you need interactivity (a filter, a
  toggle). DON'T ship a framework — 5 KB of vanilla JS is the ceiling.
- DO let tables look like tables: 1px solid borders, silver headers.
  DON'T card-ify rows or round anything.
- DO write blunt, opinionated copy. DON'T write marketing copy; brutalism
  with a "Get started" CTA is just a broken landing page.

## Copy voice

Blunt, opinionated, allergic to marketing. Short sentences. Swear lightly or
not at all. State facts; skip persuasion.

- "This site has no cookies, no tracking, and no interest in your data."
- "I deleted 4,000 lines of CSS. Nothing changed except the load time."
- "If you want animations, there are three thousand other websites."
