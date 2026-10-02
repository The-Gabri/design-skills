# design-skills

70 design languages as **agent skills** — each one a `SKILL.md` in the open
[Agent Skills](https://agentskills.io) format (YAML frontmatter with `name` +
`description`), so they plug straight into **Claude Code, Codex, Cursor,
Windsurf, Copilot** and any agent that reads the format.

Every skill ships with:
- `SKILL.md` — principles, real color/typography/layout tokens, components,
  motion, do/don't pairs and copy-pasteable code. Confidence legend:
  ✅ official/documented · 🟡 cross-referenced · ⚠️ community approximation.
- `demo.html` — a single-file page that *looks like the style*, so you can see
  what you're getting.

**[Browse all 70 live demos](https://the-gabri.github.io/design-skills/)** —
scroll, filter, and pick the style you like.

## Categories

- **A. Platform & corporate systems** (20) — Apple Liquid Glass, Material 3,
  Fluent 2, Carbon, Polaris, Ant Design, Geist, shadcn/ui, One UI...
- **B. Product & brand styles** (20) — Stripe, Linear, Duolingo, Notion,
  Teenage Engineering, Nothing, Claude, Spotify...
- **C. Movements & aesthetics** (20) — Swiss, Bauhaus, Brutalism,
  Neo-brutalism, Y2K, Frutiger Aero, Vaporwave, Skeuomorphism, Claymorphism...
- **D. Editorial, print & niche** (10) — Broadsheet, DIY zine, Art Nouveau,
  Pop Art, Constructivism, De Stijl, Wabi-sabi...

## Use

Copy any `skills/<slug>/` folder into your agent's skills directory.
No build step, no dependencies.

## License

MIT — do whatever you want with it.
