---
name: perplexity
description: Perplexity's answer-engine aesthetic — off-white minimalism, ink text, one signature teal, inline numbered citations and source chips — for answer-first search and Q&A interfaces.
---

# Perplexity

The look of Perplexity (perplexity.ai): the answer engine, not a search
page. The interface erases itself — off-white canvas, quiet ink text, a
single teal accent — so that the answer, its inline citations, and its
sources are the entire design. Strict minimalism: white space dominates,
the content is the design, no decoration anywhere.

## Principles

1. **The answer is the interface.** The whole page is a pipeline: ask bar
   → steps → sources → answer → related questions. Chrome never competes
   with content.
2. **Radical restraint.** No gradients, no glass effects, no decorative
   elements. Depth comes from hairline borders and whitespace, never
   shadows or glow.
3. **Trust is typographic.** Claims are anchored by inline numbered
   citations `[1][2]`, superscripted mid-sentence in teal. The citation
   system — numbers that expand into source cards — is the single most
   distinctive interaction in the category.
4. **Sources are first-class citizens.** A numbered source-chip row
   (favicon + site name) sits above every answer, each chip clickable,
   each number matching the citations below.
5. **One accent, nothing else.** The signature teal appears on citations,
   active states, and the send button — and nowhere else. Body text is
   always ink; UI chrome is always neutral.
6. **Threads, not pages.** Conversation stacks vertically like a thread;
   the ask bar persists at the bottom so the next question is always one
   keystroke away.

## Color

| Token | Hex | Role | Legend |
|---|---|---|---|
| Parchment | `#F8F8F6` | Page background — the warm off-white canvas | 🟡 |
| Paper | `#FAF8F5` | Alternate documented parchment tone | 🟡 |
| Surface | `#FFFFFF` | Cards, ask bar, source chips | 🟡 |
| Ink | `#271A00` | Primary text — warm near-black "aged sepia", never pure black | 🟡 |
| Ink secondary | `#7C7464` | "Moss shadow" — muted body copy, metadata | 🟡 |
| Ink muted | `#9A958A` | Placeholders, timestamps, counts | ⚠️ |
| Fog | `#D1CFC7` | Hairline borders, dividers | 🟡 |
| Border subtle | `rgba(39,26,0,.10)` | Input borders, card outlines | ⚠️ |
| Teal | `#20B8CD` | **Signature accent** — citations, active states, send button | 🟡 |
| Teal deep | `#1591A3` | Darker teal for small text on light surfaces (WCAG-safe) | 🟡 |
| Teal ink | `#0F3639` | Deep teal for active/focus states | 🟡 |
| Teal wash | `rgba(32,184,205,.10)` | Focus rings, selected-chip tint | ⚠️ |

Legend: ✅ official/documented · 🟡 cross-referenced across documented
teardowns · ⚠️ community approximation.

Notes: `#20B8CD` is the teal cited by multiple independent teardowns for
citations and interactive elements; brand-mark teardowns also cite
`#20B2AA`. Both are the same signature cyan-teal family — use `#20B8CD`
for UI, drop to `#1591A3` where small text needs contrast on parchment.
There is no secondary brand color; any second hue is a mistake.

## Typography

- **Interface sans:** pplxSans (⚠️ proprietary). Closest free
  substitutes: **Inter** or the system stack
  (`-apple-system, "Segoe UI", Roboto, sans-serif`).
- **Answer serif:** pplxSerif (⚠️ proprietary) — answers are set in
  serif, giving replies a "declared, editorial" voice distinct from the
  UI chrome. Closest free substitutes: **Source Serif 4** or **Georgia**.
- **Answer rules:** 17–18px, line-height 1.65–1.75, weight 400, measure
  ~70ch. Headings inside answers are rare; short bold lead-ins instead.
- **Ask bar text:** 16–18px sans, regular weight — the bar is the hero,
  never shouted.
- **Citations:** superscript numerals, ~0.75em, teal, weight 600 —
  visually attached to the claim they support.
- **Eyebrow labels:** "Sources", "Related" in 13px sans, ink-secondary,
  sentence case, no tracking games.

## Layout & spacing

- **Content column:** ~720–760px centered; the thread is a single
  centered column on desktop, full-bleed ask bar inside it.
- **Home:** centered wordmark + one large ask bar — the ask-first layout
  is the brand's most recognizable screen. Nothing else competes.
- **Radii:** 24–28px for the ask bar (soft pill), 12–16px for source
  chips and cards. Generous, friendly roundness — never sharp, never
  fully circular except avatars.
- **Borders:** 1px hairlines in Fog/subtle ink. The ask bar gets a
  slightly stronger border + a soft shadow only on focus.
- **Rhythm:** sections separated by whitespace and hairlines, not by
  card boxes — sources row, answer, related questions read as one
  continuous column.
- **Sidebar:** narrow left rail (~260px) with thread history and
  Discover nav; collapsible, invisible on mobile.

## Components

Copy-pasteable HTML/CSS. Base context:
`body{background:#F8F8F6;color:#271A00;font-family:-apple-system,BlinkMacSystemFont,"Segoe UI",Roboto,Inter,sans-serif}`.
Answers use `.pplx-answer{font-family:Georgia,"Source Serif 4",serif}`.

**1. Hero ask bar** (the ask-first home screen)

```html
<div class="px-hero">
  <div class="px-mark" aria-hidden="true"></div>
  <h1>perplexity</h1>
  <form class="px-ask">
    <input type="text" placeholder="Ask anything…" aria-label="Ask anything" />
    <button type="submit" aria-label="Send">↑</button>
  </form>
  <p class="px-hint">Answers with cited sources — every claim traceable.</p>
</div>
<style>
.px-hero{max-width:760px;margin:0 auto;padding:18vh 24px 0;text-align:center}
.px-mark{width:44px;height:44px;margin:0 auto 20px;border-radius:12px;
background:#20B8CD;
clip-path:polygon(0 0,100% 0,100% 62%,62% 100%,0 100%)}
.px-hero h1{font-size:34px;font-weight:600;letter-spacing:-.02em;margin:0 0 28px}
.px-ask{display:flex;align-items:center;background:#fff;border:1px solid rgba(39,26,0,.12);
border-radius:28px;padding:8px 8px 8px 24px;transition:border-color .18s ease,box-shadow .18s ease}
.px-ask:focus-within{border-color:#20B8CD;box-shadow:0 8px 32px rgba(32,184,205,.14)}
.px-ask input{flex:1;border:0;outline:0;background:transparent;font-size:17px;color:#271A00}
.px-ask input::placeholder{color:#9A958A}
.px-ask button{width:44px;height:44px;border:0;border-radius:50%;background:#20B8CD;
color:#fff;font-size:20px;cursor:pointer;flex:none}
.px-ask button:hover{background:#1591A3}
.px-hint{font-size:13.5px;color:#7C7464;margin:18px 0 0}
</style>
```

**2. Thread follow-up ask bar** (sticky bottom of a thread)

```html
<div class="px-threadbar">
  <form class="px-ask px-ask-sm">
    <input type="text" placeholder="Ask a follow-up…" aria-label="Ask a follow-up" />
    <button type="submit" aria-label="Send">↑</button>
  </form>
</div>
<style>
.px-threadbar{position:sticky;bottom:0;max-width:760px;margin:0 auto;padding:12px 24px 24px;
background:linear-gradient(transparent,#F8F8F6 32%)}
.px-ask-sm{border-radius:24px;padding:6px 6px 6px 20px;box-shadow:0 4px 20px rgba(39,26,0,.08)}
.px-ask-sm input{font-size:15.5px}
.px-ask-sm button{width:38px;height:38px;font-size:18px}
</style>
```

**3. Focus selector** (scope pill on the ask bar)

```html
<button class="px-focus" type="button">
  <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><circle cx="12" cy="12" r="9"/><circle cx="12" cy="12" r="4"/></svg>
  Focus: Web
</button>
<style>
.px-focus{display:inline-flex;align-items:center;gap:7px;border:1px solid #D1CFC7;
background:#fff;color:#7C7464;font-size:13px;font-weight:500;border-radius:999px;
padding:7px 14px;cursor:pointer}
.px-focus:hover{border-color:#20B8CD;color:#1591A3}
</style>
```

**4. Steps indicator** (Searching → Reading → Writing)

```html
<ol class="px-steps">
  <li class="done"><span>1</span>Searching the web</li>
  <li class="done"><span>2</span>Reading 6 sources</li>
  <li class="active"><span class="spin"></span>Writing answer</li>
</ol>
<style>
.px-steps{display:flex;gap:20px;list-style:none;margin:0 0 18px;padding:0;
font-size:13.5px;color:#9A958A}
.px-steps li{display:flex;align-items:center;gap:8px}
.px-steps li.done{color:#7C7464}
.px-steps li.done span{color:#1591A3;font-weight:700}
.px-steps li.active{color:#271A00}
.px-steps .spin{width:12px;height:12px;border-radius:50%;border:2px solid #D1CFC7;
border-top-color:#20B8CD;animation:pxspin .8s linear infinite;display:inline-block}
@keyframes pxspin{to{transform:rotate(360deg)}}
</style>
```

**5. Sources row** (numbered favicon chips, horizontal scroll)

```html
<div class="px-sources">
  <p class="px-label">Sources</p>
  <div class="px-chips">
    <a class="px-chip" href="#"><span class="n">1</span><span class="f" style="background:#1a73e8">N</span>NASA Science</a>
    <a class="px-chip" href="#"><span class="n">2</span><span class="f" style="background:#0f9d58">T</span>timeanddate.com</a>
    <a class="px-chip" href="#"><span class="n">3</span><span class="f" style="background:#666">W</span>Wikipedia</a>
  </div>
</div>
<style>
.px-label{font-size:13px;color:#7C7464;margin:0 0 10px}
.px-chips{display:flex;gap:10px;overflow-x:auto;padding-bottom:6px}
.px-chip{flex:none;display:flex;align-items:center;gap:9px;background:#fff;
border:1px solid rgba(39,26,0,.10);border-radius:14px;padding:9px 14px 9px 9px;
font-size:13.5px;color:#271A00;text-decoration:none}
.px-chip:hover{border-color:#20B8CD}
.px-chip .n{font-size:11px;font-weight:700;color:#1591A3;background:rgba(32,184,205,.10);
border-radius:6px;padding:2px 7px}
.px-chip .f{width:22px;height:22px;border-radius:6px;color:#fff;font-size:11px;
font-weight:700;display:flex;align-items:center;justify-content:center}
</style>
```

**6. Answer block with inline citations**

```html
<article class="pplx-answer">
  <h2>When is the next total solar eclipse over Spain?</h2>
  <p>The next total solar eclipse visible from Spain happens on
  <strong>12 August 2026</strong>, with totality crossing the north of the
  country from Galicia to the Balearic Islands.<sup><a href="#s1">1</a></sup>
  It will be the first total solar eclipse seen from mainland Spain in
  over a century.<sup><a href="#s2">2</a></sup></p>
</article>
<style>
.pplx-answer{font-family:Georgia,"Source Serif 4",serif;font-size:17.5px;
line-height:1.7;color:#271A00;max-width:70ch}
.pplx-answer h2{font-family:-apple-system,BlinkMacSystemFont,"Segoe UI",Roboto,Inter,sans-serif;
font-size:22px;font-weight:600;letter-spacing:-.01em;margin:0 0 14px}
.pplx-answer p{margin:0 0 1em}
.pplx-answer sup a{color:#1591A3;font-family:-apple-system,BlinkMacSystemFont,"Segoe UI",Roboto,Inter,sans-serif;
font-size:.72em;font-weight:700;text-decoration:none;margin-left:2px}
.pplx-answer sup a:hover{text-decoration:underline}
</style>
```

**7. Citation tooltip** (hover a citation number → source card)

```html
<span class="px-cite">1<span class="px-tip"><strong>NASA Science</strong><em>nasa.gov — Eclipse predictions</em></span></span>
<style>
.px-cite{position:relative;display:inline-block;color:#1591A3;font-weight:700;
font-size:.72em;vertical-align:super;cursor:pointer;margin-left:2px}
.px-cite:hover{text-decoration:underline}
.px-tip{display:none;position:absolute;bottom:130%;left:50%;transform:translateX(-50%);
width:230px;background:#fff;border:1px solid rgba(39,26,0,.12);border-radius:12px;
padding:12px 14px;box-shadow:0 10px 30px rgba(39,26,0,.12);z-index:5}
.px-cite:hover .px-tip{display:block}
.px-tip strong{display:block;font-size:13.5px;color:#271A00}
.px-tip em{display:block;font-style:normal;font-size:12px;color:#7C7464;margin-top:3px}
</style>
```

**8. Related questions**

```html
<div class="px-related">
  <p class="px-label">Related</p>
  <button class="px-rel">How long will totality last in Zaragoza?<span>+</span></button>
  <button class="px-rel">Where is the best place in Spain to watch it?<span>+</span></button>
  <button class="px-rel">When is the next eclipse after 2026?<span>+</span></button>
</div>
<style>
.px-related{margin-top:28px}
.px-rel{display:flex;align-items:center;justify-content:space-between;width:100%;
background:transparent;border:0;border-top:1px solid rgba(39,26,0,.10);
padding:15px 4px;font-size:15.5px;color:#271A00;cursor:pointer;text-align:left}
.px-rel:last-child{border-bottom:1px solid rgba(39,26,0,.10)}
.px-rel span{color:#9A958A;font-size:20px;font-weight:300;line-height:1}
.px-rel:hover{color:#1591A3}
.px-rel:hover span{color:#1591A3}
</style>
```

**9. Sidebar thread list**

```html
<aside class="px-side">
  <button class="px-new">+ New thread</button>
  <p class="px-label">Today</p>
  <a class="px-thread active" href="#">Next total solar eclipse over Spain</a>
  <a class="px-thread" href="#">Tallest peak in the Pyrenees</a>
  <a class="px-thread" href="#">Why is the sky blue?</a>
</aside>
<style>
.px-side{width:260px;flex:none;padding:20px 14px;border-right:1px solid rgba(39,26,0,.08)}
.px-new{display:block;width:100%;border:1px solid #D1CFC7;background:#fff;border-radius:999px;
padding:10px;font-size:14px;font-weight:500;color:#271A00;cursor:pointer;margin-bottom:22px}
.px-new:hover{border-color:#20B8CD;color:#1591A3}
.px-thread{display:block;padding:9px 12px;border-radius:10px;font-size:14px;
color:#7C7464;text-decoration:none;white-space:nowrap;overflow:hidden;text-overflow:ellipsis}
.px-thread:hover{background:rgba(39,26,0,.05);color:#271A00}
.px-thread.active{background:rgba(32,184,205,.10);color:#271A00}
</style>
```

**10. Answer toolbar** (Copy / Share / Rewrite — ghost buttons)

```html
<div class="px-tools">
  <button>Copy</button><button>Share</button><button>Rewrite</button>
</div>
<style>
.px-tools{display:flex;gap:6px;margin-top:18px}
.px-tools button{border:1px solid transparent;background:transparent;color:#7C7464;
font-size:13.5px;font-weight:500;border-radius:999px;padding:7px 14px;cursor:pointer}
.px-tools button:hover{border-color:#D1CFC7;color:#271A00;background:#fff}
</style>
```

## Motion

Perplexity defines almost no decorative motion: there are no page
transitions, no loading screens — the response begins immediately and the
answer streams in word by word. Source chips fade in with a light
stagger; hovers are 150–200ms `ease-out`. The one signature moment is
citation numbers that subtly glow-pulse on hover before expanding into
source cards.

## Do / Don't

- **Do** put the ask bar first and make it the largest element on the
  screen — **don't** lead with a nav, a hero headline, or feature cards.
- **Do** superscript every citation number in teal, attached to the claim
  — **don't** dump a link list at the bottom and call it citing.
- **Do** number the source chips 1..n to match the citations exactly —
  **don't** let chip order and citation order drift apart.
- **Do** set answers in serif at reading size on the bare canvas —
  **don't** box the answer in a card with a shadow; it isn't a widget.
- **Do** use teal only for citations, active states, and the send button
  — **don't** tint headings, icons, or body copy teal.
- **Do** keep the background warm off-white (`#F8F8F6`) — **don't** use
  cool gray, pure white, or dark mode as the default light theme.
- **Do** separate Sources / Answer / Related with whitespace and
  hairlines — **don't** wrap each in identical bordered cards.
- **Do** stream the answer starting with steps ("Searching… Reading…") —
  **don't** show a spinner or a blank loading page first.

## Copy voice

Direct, neutral, cited — the voice of a research assistant, not a
salesperson. Short declarative sentences, no hype adjectives, no
exclamation marks. Claims end with citations; uncertainty is stated
plainly ("sources disagree on…").

- Ask bar placeholder: "Ask anything…"
- Steps: "Searching the web" → "Reading 4 sources" → "Writing answer"
- Answer lead: "The next total solar eclipse visible from Spain happens
  on 12 August 2026, with totality crossing the north of the country.[1]
  It is the first total eclipse seen from mainland Spain in over a
  century.[2]"
- Related header: "Related" (one word, no flourish)
