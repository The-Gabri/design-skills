# Skill + Demo Template (mandatory for all 70)

## SKILL.md structure (Agent Skills open format)

```markdown
---
name: <slug>
description: <one line, what style + when to use it>
---

# <Title>

## Principles
3–6 real principles of the style, grounded in the actual system/brand/movement.

## Color
Real palette: hex tokens with names and roles (bg, surface, text, accent...).
Mark confidence: ✅ official/documented · 🟡 cross-referenced · ⚠️ community approximation.

## Typography
Real typefaces (or closest free substitutes with names), scale, weights, usage rules.

## Layout & spacing
Grid, spacing scale, radius, borders/shadows — the tokens that make it recognizable.

## Components
5–10 signature components with copy-pasteable HTML/CSS (or SwiftUI/etc. where relevant).

## Motion
Easing curves, durations, signature transitions — only if the style defines them.

## Do / Don't
Concrete pairs. No generic advice ("don't use bad colors").

## Copy voice (for brand styles)
How text sounds in this style, with 2–3 example strings.
```

Rules:
- English only.
- Research the real thing first (official docs, brand guidelines, documented analyses).
  Never invent tokens and present them as official — use the ✅/🟡/⚠️ legend.
- No filler sections. If a style has no motion language, say so in one line.
- Code examples must be copy-pasteable and correct.

## demo.html rules (the anti-slop contract)

- Single HTML file, all CSS/JS inline. Must open by double-clicking, no build step.
- It must look like a REAL product page in that style — hero, nav, buttons,
  cards, type scale, a small interactive touch (toggle, tabs, hover states).
- Real-ish English copy about a plausible fictional product. NEVER lorem ipsum.
- BANNED unless the style itself demands it: purple-blue gradients, generic
  glass cards on dark bg, "Lorem ipsum", centered hero with pill button and
  three feature cards, Inter/Roboto as the only personality, emoji as icons.
- Every demo must have at least 3 details that are unmistakably THAT style
  (e.g. Duolingo: chunky 3D buttons with bottom border; Brutalism: raw borders,
  system fonts, marquee; Linear: dark, subtle gradients, keyboard shortcuts).
- Responsive. `<title>` = skill name. No external assets except Google Fonts
  (with system-font fallback) — everything else inline.
- Footer line: `Built from the <slug> skill · design-skills`.

## Docs showcase (docs/index.html)

- Dark neutral chrome (the showcase itself is NOT one of the styles).
- Hero: "design-skills — 70 design languages for AI agents".
- Search/filter by name + category (A/B/C/D).
- One card per skill: name, one-line description, category tag, and a
  lazy-loaded scaled `<iframe>` of its demo (`docs/demos/<slug>.html`).
- Clicking a card opens the full demo in a new tab.
- Badges: "Claude Code · Codex · Cursor · Copilot ready".
