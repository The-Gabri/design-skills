---
name: notion
description: Notion's minimal document aesthetic — calm block-based pages, warm paper tones, and quiet UI. Use for docs, wikis, dashboards, and productivity UIs.
---

# Notion

## Principles

1. **Everything is a block.** Text, images, checklists, databases — all content is a discrete, movable block stacked in a single document column. Hierarchy comes from block types, not chrome.
2. **The canvas is quiet.** Near-white backgrounds, hairline borders, no heavy shadows. UI exists as whispers; the content is the interface.
3. **Warm, analog undertones.** Notion's grays run warm (yellow-brown undertone), never cold blue-gray. Pure `#000000` is avoided — it reads as clinical against the warm canvas.
4. **Color is surgical.** Blue is reserved for links, selections, and CTAs. Block colors come in restrained pastel pairs (text color + matching pale background) used sparingly to annotate, not decorate.
5. **Calm productivity.** Generous whitespace, one body size, three heading levels. The page breathes; nothing competes for attention.

## Color

Confidence: ✅ official/documented · 🟡 cross-referenced · ⚠️ community approximation.

| Token | Hex | Role |
|---|---|---|
| `--notion-page` | `#FFFFFF` ✅ | Page canvas |
| `--notion-sidebar` | `#F7F6F3` 🟡 | Sidebar / panel background (warm off-white) |
| `--notion-text` | `#37352F` 🟡 | Body text — warm near-black, never pure black |
| `--notion-text-gray` | `#787774` 🟡 | Secondary / muted text |
| `--notion-text-faint` | `#9B9A97` 🟡 | Placeholders, hints |
| `--notion-border` | `#E9E9E7` 🟡 | Hairline dividers, table rules |
| `--notion-border-strong` | `rgba(0,0,0,0.09)` 🟡 | Block handles, input borders |
| `--notion-blue` | `#2383E2` 🟡 | Links, selections, the singular accent (marketing CTA blue `#0075DE` 🟡) |
| `--notion-blue-bg` | `#E7F3F8` 🟡 | Blue callout / selected block fill |
| `--notion-red` | `#E16259` 🟡 | Red accent — text highlight, warnings, notifications |
| `--notion-red-bg` | `#FDEBEC` 🟡 | Red callout background |
| `--notion-yellow-bg` | `#FBF3DB` 🟡 | Yellow callout background |
| `--notion-green-bg` | `#EDF3EC` 🟡 | Green callout background |
| `--notion-gray-bg` | `#F1F1EF` 🟡 | Gray callout background / kanban column header |
| `--notion-purple-bg` | `#F6F3F9` 🟡 | Purple callout background |
| `--notion-pink-bg` | `#FAF1F5` 🟡 | Pink callout background |
| `--notion-orange-bg` | `#FBECDD` 🟡 | Orange callout background |
| `--notion-brown-bg` | `#F4EEEE` 🟡 | Brown callout background |
| `--notion-select-blue` | `#0B6E99` 🟡 | Blue select-tag text |
| `--notion-select-blue-bg` | `#D3E5EF` 🟡 | Blue select-tag pill |
| `--notion-select-green` | `#0F7B6C` 🟡 | Green select-tag text |
| `--notion-select-green-bg` | `#DBEDEA` 🟡 | Green select-tag pill |
| `--notion-select-yellow` | `#CB912F` 🟡 | Yellow select-tag text |
| `--notion-select-yellow-bg` | `#FDECC8` 🟡 | Yellow select-tag pill |
| `--notion-select-red` | `#D44C47` 🟡 | Red select-tag text |
| `--notion-select-red-bg` | `#FFE2DD` 🟡 | Red select-tag pill |
| `--notion-select-purple` | `#9065B0` 🟡 | Purple select-tag text |
| `--notion-select-purple-bg` | `#E8DEEE` 🟡 | Purple select-tag pill |
| `--notion-select-gray` | `#787774` 🟡 | Gray select-tag text |
| `--notion-select-gray-bg` | `#E3E2E0` 🟡 | Gray select-tag pill |
| `--notion-hover` | `rgba(0,0,0,0.04)` 🟡 | Row / block hover fill |

Text-color options (for inline highlights): default `#37352F`, gray `#787774`, brown `#9F6B53`, orange `#D9730D`, yellow `#CB912F`, green `#448361`, blue `#337EA9`, purple `#9065B0`, pink `#C14C8A`, red `#D44C47` — all 🟡.

## Typography

- **UI + body:** Inter is the workhorse 🟡. Fallback stack:
  `font-family: "Inter", -apple-system, BlinkMacSystemFont, "Segoe UI", Helvetica, Arial, sans-serif;`
  Body is a single size: 14–16px at 400 weight, ~1.5 line-height.
- **Headings:** same sans family, bold (700), three levels — H1 30px, H2 24px, H3 20px 🟡. Page titles are large and bold, often paired with a leading page icon.
- **Display / marketing:** Notion's marketing site pairs a custom serif face with the sans UI 🟡. Closest free substitute: **Source Serif 4** or **Lyon Text**-style serif for display lines.
- **Code:** mono — `ui-monospace, SFMono-Regular, Menlo, Consolas, monospace` ✅ (in-product behavior).
- **Type rules:** one body size everywhere; hierarchy via weight and the three heading levels only; never modify letter-spacing casually; `tabular-nums` for database numbers.

## Layout & spacing

- **Document column:** single content column ~**720px** wide, centered 🟡 (up to ~900px on wide screens). Sidebar 240px, collapsible 🟡.
- **Block rhythm:** 8–12px between blocks, 24–32px around headings 🟡. Blocks can have an optional full-width cover image and a large page icon above the title.
- **Radius:** 3px for chrome/buttons 🟡, 6px for blocks, callouts, menus, and code blocks.
- **Borders:** 1px hairlines (`#E9E9E7`) as the dominant separation pattern — they exist as whispers. Inline blocks never lift.
- **Elevation:** essentially flat. Reserved for menus, modals, and toasts only, using the signature double shadow: `box-shadow: 0 0 0 1px rgba(0,0,0,0.06), 0 4px 12px rgba(0,0,0,0.08)` 🟡.
- **Selection:** a faint blue fill (`#E7F3F8` / `rgba(35,131,226,0.08)`), not an outline.

## Components

### 1. Breadcrumb + page title

```html
<div class="n-breadcrumb">Workspace / Projects / <span>Q4 Product Sprint</span></div>
<h1 class="n-page-title"><span class="n-page-icon">🗂️</span> Q4 Product Sprint</h1>
<p class="n-meta">Last edited by Mara Chen · Oct 2, 2026</p>
```
```css
.n-breadcrumb{font-size:13px;color:#787774;margin-bottom:8px}
.n-breadcrumb span{color:#37352F;font-weight:500}
.n-page-title{font-size:30px;font-weight:700;letter-spacing:-0.01em;color:#37352F;margin:0 0 6px}
.n-page-icon{font-size:36px;margin-right:10px;vertical-align:-4px}
.n-meta{font-size:13px;color:#9B9A97;margin:0 0 28px}
```

### 2. Toggle block

```html
<details class="n-toggle" open>
  <summary class="n-toggle-head"><span class="n-caret">▾</span> Sprint goals</summary>
  <div class="n-toggle-body">
    <p>Ship the new onboarding flow and cut trial-to-paid time by 15%.</p>
  </div>
</details>
```
```css
.n-toggle{margin:8px 0;border-radius:3px}
.n-toggle-head{cursor:pointer;list-style:none;font-weight:600;font-size:16px;color:#37352F;padding:4px 6px;border-radius:3px}
.n-toggle-head::-webkit-details-marker{display:none}
.n-toggle-head:hover{background:rgba(0,0,0,0.04)}
.n-caret{display:inline-block;width:22px;color:#787774;font-size:12px;transition:transform .15s ease}
details:not([open]) .n-caret{transform:rotate(-90deg)}
.n-toggle-body{padding:4px 6px 8px 32px;color:#37352F;line-height:1.6}
```

### 3. Callout

```html
<div class="n-callout n-callout--blue">
  <span class="n-callout-icon">💡</span>
  <div><strong>Reminder:</strong> freeze the scope by Friday — no new tickets after standup.</div>
</div>
```
```css
.n-callout{display:flex;gap:10px;padding:12px 14px;border-radius:6px;margin:10px 0;line-height:1.55;font-size:15px}
.n-callout--blue{background:#E7F3F8;color:#37352F}
.n-callout--gray{background:#F1F1EF;color:#37352F}
.n-callout--yellow{background:#FBF3DB;color:#37352F}
.n-callout--green{background:#EDF3EC;color:#37352F}
.n-callout--red{background:#FDEBEC;color:#37352F}
.n-callout-icon{font-size:18px;line-height:1.4;flex-shrink:0}
```
Callout icons are emoji-as-content — the one place emoji is legitimate in this style.

### 4. Quote

```html
<blockquote class="n-quote">“Make every detail perfect and limit the number of details to perfect.”</blockquote>
```
```css
.n-quote{border-left:3px solid #37352F;margin:10px 0;padding:2px 0 2px 14px;color:#37352F;font-size:15px;line-height:1.6}
```

### 5. Divider

```html
<hr class="n-divider">
```
```css
.n-divider{border:0;border-top:1px solid #E9E9E7;margin:16px 0}
```

### 6. Code block

```html
<pre class="n-code"><code class="language-js">const blocks = page.children;
blocks.forEach(b => render(b));</code></pre>
```
```css
.n-code{background:#F7F6F3;border-radius:6px;padding:14px 16px;font-family:ui-monospace,SFMono-Regular,Menlo,Consolas,monospace;font-size:13.5px;line-height:1.6;color:#37352F;overflow:auto;margin:10px 0}
```

### 7. To-do list

```html
<label class="n-todo"><input type="checkbox" checked><span class="n-todo-done">Finalize sprint scope</span></label>
<label class="n-todo"><input type="checkbox"><span>Book usability sessions</span></label>
```
```css
.n-todo{display:flex;gap:8px;align-items:flex-start;padding:3px 0;font-size:15px;color:#37352F;cursor:pointer}
.n-todo input{appearance:none;width:16px;height:16px;border:1.5px solid rgba(0,0,0,0.25);border-radius:3px;margin-top:3px;flex-shrink:0;cursor:pointer}
.n-todo input:checked{background:#2383E2;border-color:#2383E2}
.n-todo input:checked::after{content:"✓";color:#fff;font-size:11px;display:block;text-align:center;line-height:14px}
.n-todo-done{color:#9B9A97;text-decoration:line-through}
```

### 8. Database table view

```html
<table class="n-db">
  <thead><tr><th>Task</th><th>Status</th><th>Owner</th><th>Due</th></tr></thead>
  <tbody>
    <tr><td class="n-db-title">📄 Onboarding flow v2</td>
        <td><span class="n-tag n-tag--blue">In progress</span></td>
        <td><span class="n-avatar">MC</span> Mara Chen</td>
        <td>Oct 9</td></tr>
    <tr><td class="n-db-title">📄 Billing emails</td>
        <td><span class="n-tag n-tag--green">Done</span></td>
        <td><span class="n-avatar">JT</span> Jon Tao</td>
        <td>Oct 2</td></tr>
  </tbody>
</table>
```
```css
.n-db{width:100%;border-collapse:collapse;font-size:14px}
.n-db th{text-align:left;font-size:12px;font-weight:500;color:#787774;border-bottom:1px solid #E9E9E7;padding:8px 10px}
.n-db td{border-bottom:1px solid #E9E9E7;padding:8px 10px;color:#37352F}
.n-db tbody tr:hover{background:rgba(0,0,0,0.04);cursor:pointer}
.n-db-title{font-weight:500}
.n-tag{display:inline-block;font-size:12px;font-weight:500;padding:2px 8px;border-radius:3px}
.n-tag--blue{color:#0B6E99;background:#D3E5EF}
.n-tag--green{color:#0F7B6C;background:#DBEDEA}
.n-tag--yellow{color:#CB912F;background:#FDECC8}
.n-tag--red{color:#D44C47;background:#FFE2DD}
.n-tag--purple{color:#9065B0;background:#E8DEEE}
.n-tag--gray{color:#787774;background:#E3E2E0}
.n-avatar{display:inline-flex;width:22px;height:22px;border-radius:50%;background:#E3E2E0;color:#787774;font-size:10px;font-weight:600;align-items:center;justify-content:center;margin-right:6px;vertical-align:-6px}
```

### 9. Kanban board view

```html
<div class="n-board">
  <div class="n-col"><div class="n-col-head"><span class="n-col-dot" style="background:#D3E5EF"></span>To do <span class="n-col-count">2</span></div>
    <div class="n-card">Draft release notes</div></div>
  <div class="n-col"><div class="n-col-head"><span class="n-col-dot" style="background:#DBEDEA"></span>Done <span class="n-col-count">1</span></div>
    <div class="n-card n-card--done">Fix login redirect</div></div>
</div>
```
```css
.n-board{display:flex;gap:12px;overflow-x:auto;padding:4px 0}
.n-col{flex:0 0 240px;background:#F7F6F3;border-radius:6px;padding:8px}
.n-col-head{display:flex;align-items:center;gap:8px;font-size:13px;font-weight:600;color:#37352F;padding:4px 6px 10px}
.n-col-dot{width:8px;height:8px;border-radius:50%}
.n-col-count{color:#9B9A97;font-weight:400}
.n-card{background:#fff;border:1px solid #E9E9E7;border-radius:6px;padding:10px 12px;font-size:14px;margin-bottom:8px;box-shadow:0 1px 2px rgba(0,0,0,0.04)}
.n-card--done{color:#9B9A97;text-decoration:line-through}
```

### 10. Link / bookmark card

```html
<a class="n-bookmark" href="#">
  <span class="n-bookmark-body"><span class="n-bookmark-title">Notion — One workspace. Every team.</span>
  <span class="n-bookmark-desc">Write, plan, and get organized in one place.</span></span>
  <span class="n-bookmark-url">notion.so</span>
</a>
```
```css
.n-bookmark{display:block;border:1px solid #E9E9E7;border-radius:6px;padding:12px 14px;margin:10px 0;text-decoration:none;color:#37352F}
.n-bookmark:hover{background:rgba(0,0,0,0.04)}
.n-bookmark-title{display:block;font-weight:500;font-size:14px}
.n-bookmark-desc{display:block;font-size:13px;color:#787774;margin-top:2px}
.n-bookmark-url{display:block;font-size:12px;color:#9B9A97;margin-top:6px}
```

## Motion

Notion has almost no signature motion language. Blocks fade/expand in ~150ms `ease` on toggle; database views switch instantly; page transitions are simple fades. Keep everything subtle and instant-feeling — no springs, no parallax, no flourish.

## Do / Don't

- **Do** keep text warm near-black (`#37352F`) on white — **don't** use pure black or cold blue-grays (`#6B7280`, `#9CA3AF`).
- **Do** separate with 1px hairlines (`#E9E9E7`) — **don't** use heavy borders or visible drop shadows on inline blocks.
- **Do** use blue (`#2383E2`) only for links, selections, and CTAs — **don't** scatter it across borders or decorative elements.
- **Do** keep one body size and three heading levels — **don't** build a 6-size type scale.
- **Do** use pastel block backgrounds (blue/yellow/green/red) to annotate meaning — **don't** use them as section decoration or gradients.
- **Do** use emoji as document content (page icons, callout icons) — **don't** use emoji as UI icons (nav, buttons, toolbar).
- **Do** let the 720px document column carry the page — **don't** add centered hero sections with pill buttons.
- **Do** show database data in tight table rows with tag pills — **don't** build card-heavy dashboards.

## Copy voice

Calm, helpful, quietly confident. Plain sentences, no hype. The tool disappears; your work is the subject.

- "Write, plan, and get organized — all in one place."
- "A new tool that blends your everyday work apps into one."
- "Drag anywhere to rearrange. Everything is a block."
