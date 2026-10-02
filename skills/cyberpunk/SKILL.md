---
name: cyberpunk
description: Cyberpunk neon-dystopia aesthetic — near-black ground, one hot neon accent per screen, glitch RGB-split type, scanlines, corner-bracket panels, terminal motifs. Use for dark futuristic interfaces with attitude.
---

# Cyberpunk

## Verification legend
- ✅ = documented in a primary/official source (designer quote, shipped UI).
- 🟡 = cross-referenced across ≥2 independent design analyses or design systems.
- ⚠️ = community approximation (useful, not dogma).

## Principles
1. **One hot accent per screen.** Cyberpunk 2077's rule: yellow is the single hero accent; cyan reads as data/interactive, magenta as glitch/danger. The moment every neon fires at full saturation, the screen becomes synthwave wallpaper instead of an interface. 🟡
2. **The city is hostile; the interface is a weapon.** UI frames the user as an operator working against systems: authentication gates, trace timers, breach percentages, monospaced telemetry. Decoration should read as *instrumentation*, not illustration. 🟡
3. **Glitch is punctuation, not a loop.** RGB-split and clip-path glitch belong as one-shot events — on hover, on error, on a headline's entrance — never as a permanent animation on body text. Continuous glitch = unreadable noise. 🟡
4. **High tech rendered low-fi.** Scanlines, noise grain, hairline grids, corner brackets: the future arrives through degraded surfaces. Keep these textures at whisper opacity (scanlines ~0.07) so they add atmosphere without fogging content. 🟡
5. **Typography is military-terminal, not sci-fi-rounded.** Condensed heavy uppercase display type + strict monospace for data. No chrome letters, no orbit rings as typography. ⚠️
6. **Geometry cuts inward.** Angular chamfered corners (clip-path), L-bracket corner frames instead of closed rectangles, skewed call-to-action edges. Rectangles with rounded corners belong to another genre entirely. 🟡

## Color
The near-black void ground is mandatory; everything else earns its place by contrast.

| Token | Hex | Role | Confidence |
|---|---|---|---|
| `--void` | `#050507` | page ground | 🟡 |
| `--void-2` | `#0A0A0F` | panel ground / raised surface | 🟡 |
| `--panel` | `#0D0D14` | card surface | 🟡 |
| `--line` | `#1E1E2A` | hairline borders, grid lines | 🟡 |
| `--seam` | `#2B1E45` | violet bridge between magenta and cyan zones | 🟡 |
| `--yellow` | `#FCEE0A` | THE hot accent — headlines, primary CTA, active state (one per screen) | ✅ brand element (CDPR: "yellow is our most important brand element"), hex 🟡 |
| `--cyan` | `#00F0FF` | data / interactive / links | 🟡 |
| `--magenta` | `#FF2A6D` | danger / glitch only — never a hover color | 🟡 |
| `--red` | `#FF3C3C` | hostile / critical alert | 🟡 |
| `--green` | `#05FFA1` | success / link established | 🟡 |
| `--ink` | `#EDEDF2` | primary text | 🟡 |
| `--dim` | `#8A8A99` | secondary text, metadata | 🟡 |

Neon glow recipes (layered shadows, never a background gradient wash) 🟡:
```css
--glow-yellow: 0 0 6px rgba(252,238,10,.9), 0 0 22px rgba(252,238,10,.45), 0 0 60px rgba(252,238,10,.18);
--glow-cyan:   0 0 6px rgba(0,240,255,.9),  0 0 22px rgba(0,240,255,.4),  0 0 60px rgba(0,240,255,.15);
--glow-magenta:0 0 6px rgba(255,42,109,.9), 0 0 22px rgba(255,42,109,.4);
```
Rule of thumb: glow = tight core + soft halo + wide faint bloom. If the halo alone is readable at arm's length, you've gone too far.

## Typography
- **Display:** condensed heavy sans, all caps, tight tracking, often sheared slightly. The shipped-game UI typeface is custom; closest free substitutes widely used in 2077 fan design systems: **Rajdhani** (700/600) or **Orbitron** (800/900) for hero display. ⚠️ community approximations
  - The `cyberpunk` demo ships **Orbitron 800/900** for display and **Share Tech Mono** for mono, loaded via Google Fonts with system fallbacks (`Impact`/monospace) so the file still works offline.
- **Body/UI:** a neutral grotesque at small sizes so the neon does the talking — system stack is fine. ⚠️
- **Data/mono:** **Share Tech Mono** (closest free match for terminal chrome) or **JetBrains Mono** / system `Consolas, "Courier New", monospace`. Used for: metadata rows, hex IDs, timecodes, status readouts, terminal, version strings, button micro-labels. 🟡
- Scale: hero `clamp(3rem, 9vw, 7rem)` display / section heads 1.5–2.25rem / body 0.95–1.05rem / metadata 0.7–0.8rem mono, uppercase, letter-spacing 0.08–0.2em.
- Usage rule: caps for *system* voice only (nav, labels, readouts). Prose body stays sentence case so the caps keep their punch. 🟡

## Layout & spacing
- **Ground texture stack (bottom to top):** hairline grid (`background-size: 48px`, 3–5% alpha) → radial vignette darkening edges → scanline overlay (alpha ~0.07, `pointer-events:none`, topmost below content chrome) → noise grain at 4–8%. 🟡
- **Panels float on brackets, not boxes:** L-shaped corner brackets at the four corners of a panel instead of a full border; or a chamfered `clip-path` with a single neon edge. Corners cut 10–18px.
- **Metadata rows** run along a panel edge: `SYS://NETRUNNER v4.2.077 · NODE 0xA4F2 · 02:31:07` in 0.72rem mono, dim color, separated by `//` or `·`.
- **Hairline dividers:** `linear-gradient(90deg, transparent, var(--accent), transparent)` at 1px — a neon filament, not a rule. 🟡
- Spacing: 8px base scale; section rhythm `padding: 96px 24px` desktop, 56px mobile; max content width 1120px, terminal blocks max 720px for readability.
- Radius: `0` for structural UI (chamfers instead); `2px` max for small interactive bits. Rounded pills are genre-breaking.

## Components

### 1. Glitch headline (one-shot RGB split)
```html
<h1 class="glitch" data-text="OWN THE GRID">OWN THE GRID</h1>
```
```css
.glitch { position: relative; color: var(--ink); }
.glitch::before, .glitch::after {
  content: attr(data-text);
  position: absolute; inset: 0; opacity: 0;
}
.glitch::before { color: var(--magenta); }
.glitch::after  { color: var(--cyan); }
.glitch:hover::before, .glitch.glitching::before {
  opacity: 1; animation: gl-a .32s steps(2) both;
  text-shadow: -2px 0 var(--magenta);
  clip-path: inset(10% 0 55% 0);
}
.glitch:hover::after, .glitch.glitching::after {
  opacity: 1; animation: gl-b .32s steps(2) both;
  text-shadow: 2px 0 var(--cyan);
  clip-path: inset(60% 0 5% 0);
}
@keyframes gl-a { 50% { transform: translate(-6px, 2px); clip-path: inset(55% 0 12% 0); } }
@keyframes gl-b { 50% { transform: translate(6px, -2px); clip-path: inset(8% 0 70% 0); } }
@media (prefers-reduced-motion: reduce) {
  .glitch:hover::before, .glitch:hover::after { animation: none; opacity: .85; }
}
```
One-shot on hover or on entrance via a `.glitching` class — never an infinite loop on body copy. 🟡

### 2. Corner-bracket panel
```html
<section class="bracket">
  <p class="meta">SYS://MODULE · v2.077.4</p>
  <h3>Black ICE drill</h3>
</section>
```
```css
.bracket { position: relative; background: var(--panel); padding: 28px; }
.bracket::before, .bracket::after {
  content: ""; position: absolute; width: 18px; height: 18px;
  border: 2px solid var(--yellow);
}
.bracket::before { top: -2px; left: -2px; border-right: 0; border-bottom: 0; }
.bracket::after  { bottom: -2px; right: -2px; border-left: 0; border-top: 0; }
/* two more corners via an inner span if a full frame is needed */
```
L-brackets, not closed rectangles. 🟡

### 3. Chamfered neon button (primary CTA)
```html
<a class="cta" href="#"><span>JACK IN</span></a>
```
```css
.cta {
  --cut: 12px;
  display: inline-block; background: var(--yellow); color: #0A0A0F;
  font: 700 .85rem/1 "Rajdhani", "Arial Narrow", sans-serif;
  letter-spacing: .18em; text-transform: uppercase; text-decoration: none;
  padding: 16px 34px;
  clip-path: polygon(var(--cut) 0, 100% 0, 100% calc(100% - var(--cut)), calc(100% - var(--cut)) 100%, 0 100%, 0 var(--cut));
  transition: filter .15s ease, transform .15s ease;
}
.cta:hover { filter: drop-shadow(0 0 12px rgba(252,238,10,.7)); transform: translateY(-1px); }
.cta.ghost { background: transparent; color: var(--cyan);
  box-shadow: inset 0 0 0 1px var(--cyan); }
```
2077's buttons are angular/yellow-first; chamfer + no radius is the signature. 🟡

### 4. Scanline + grid ground (global utility)
```css
body::before { /* scanlines — the whisper, not the hum */
  content: ""; position: fixed; inset: 0; z-index: 60; pointer-events: none;
  background: repeating-linear-gradient(0deg,
    transparent 0 2px, rgba(0,0,0,.28) 2px 4px);
  opacity: .22; /* ≈ .07 effective over dark ground */
}
body::after { /* hairline grid */
  content: ""; position: fixed; inset: 0; z-index: -1; pointer-events: none;
  background-image:
    linear-gradient(rgba(0,240,255,.045) 1px, transparent 1px),
    linear-gradient(90deg, rgba(0,240,255,.045) 1px, transparent 1px);
  background-size: 48px 48px;
  mask-image: radial-gradient(ellipse at 50% 30%, black 30%, transparent 75%);
}
```
🟡 (recipes cross-referenced across cyberpunk CSS systems)

### 5. Terminal window
```html
<div class="term">
  <div class="term-bar"><span>ghostlink — zsh</span><span class="dots"><i></i><i></i><i></i></span></div>
  <pre class="term-body">$ trace --target arasaka.local
<span class="ok">[OK]</span> handshake 0xA4F2 … 12ms
<span class="warn">[!]</span> ICE detected on hop 4 — re-routing</pre>
</div>
```
```css
.term { background: #020204; border: 1px solid var(--line); max-width: 720px; }
.term-bar { display: flex; justify-content: space-between; padding: 8px 12px;
  border-bottom: 1px solid var(--line); font: .72rem/1 Consolas, monospace;
  letter-spacing: .14em; text-transform: uppercase; color: var(--dim); }
.term-body { padding: 16px; font: .85rem/1.7 Consolas, "Courier New", monospace; color: var(--ink); }
.term-body .ok { color: var(--green); } .term-body .warn { color: var(--yellow); }
```
Terminal chrome is dark-on-darker with hairline borders; color carries the signal. 🟡

### 6. Neon filament divider + telemetry row
```html
<div class="telemetry">
  <span>UPTIME 99.98%</span><span>LAT 4ms</span><span>NODES 1,204</span><span class="live">● LIVE</span>
</div>
```
```css
.telemetry { display: flex; gap: 28px; flex-wrap: wrap;
  font: .72rem/1 Consolas, monospace; letter-spacing: .16em; color: var(--dim);
  text-transform: uppercase; }
.telemetry .live { color: var(--green); animation: blink 1.6s steps(2) infinite; }
@keyframes blink { 50% { opacity: .25; } }
hr.filament { border: 0; height: 1px;
  background: linear-gradient(90deg, transparent, var(--cyan), transparent); }
```
Telemetry as ornament: live numerics, signal glyphs, timecodes that don't need to mean anything. 🟡

### 7. Breach progress / trace bar
```html
<div class="trace"><div class="trace-fill" style="--p:72%"></div><span>TRACE 72%</span></div>
```
```css
.trace { position: relative; height: 26px; background: var(--void-2);
  border: 1px solid var(--line); overflow: hidden;
  clip-path: polygon(10px 0, 100% 0, calc(100% - 10px) 100%, 0 100%); }
.trace-fill { width: var(--p); height: 100%;
  background: repeating-linear-gradient(-55deg, var(--yellow) 0 8px, #b8ac06 8px 16px);
  box-shadow: var(--glow-yellow); }
.trace span { position: absolute; inset: 0; display: grid; place-items: center;
  font: 700 .7rem Consolas, monospace; letter-spacing: .2em; color: #fff;
  text-shadow: 0 1px 2px #000; }
```
Diagonal hazard-stripes are the 2077 loading-bar vernacular. ⚠️

## Motion
Cyberpunk motion is snappy and mechanical — no springs, no bounces.
- **Glitch slices:** `steps(2)` or `cubic-bezier(.2,.9,.3,1)`, 200–400ms, one-shot. Chromatic offset ±2–6px; clip slices move between keyframes.
- **Neon flicker (signage only, never UI text):** irregular keyframes (on at 0/92/100%, dip at 93–94%), ~4s cycle, subtle (opacity .85–1). 🟡
- **Boot/typewriter sequences:** 8–22ms per char, mono cursor block `▊` blinking via `steps(1)`. Keep the whole boot under ~4s: 4–6 short lines, not a novel. Always provide a visible SKIP button, an Esc/Enter key shortcut, auto-finish on completion, and a hard failsafe timeout (~8s) that force-hides the overlay no matter what — a boot that can trap the user is a broken demo.
- **Hovers:** instant-ish — 120–180ms ease-out; glow ramps up, element translates −1px or skews −2deg. No scale-pop.
- **Entrances:** panels clip-wipe or rise 12px with 300ms `cubic-bezier(.16,1,.3,1)`; stagger 60ms.
- **Reduced motion:** glitch becomes a static RGB offset; flicker/blink off; boot sequence renders instantly; all entrances become opacity-only 1ms. Non-negotiable.

## Do / Don't
- ✅ Do pick ONE hot accent per screen (yellow hero, cyan data, magenta danger). → ❌ Don't light every element a different neon; that's a carnival, not Night City.
- ✅ Do fire the glitch once — on hover, on error, on headline entrance. → ❌ Don't loop glitch animations on readable text.
- ✅ Do use scanlines at whisper opacity (~0.07 effective) and hairline grids. → ❌ Don't plaster heavy visible CRT stripes or a perspective grid floor under a hero.
- ✅ Do frame panels with L-corner brackets or chamfered clip-paths. → ❌ Don't use fully-rounded cards or generic glassmorphism panels.
- ✅ Do write system copy in terse uppercase mono: `AUTH // 0xA4F2`. → ❌ Don't let the system apologize or joke — it never says "oops".
- ✅ Do decorate with telemetry: coordinates, hex IDs, timecodes, version strings. → ❌ Don't use lorem ipsum or meaningless latin anywhere, ever.
- ✅ Do skew/chamfer primary CTAs with the hero yellow. → ❌ Don't ship a centered hero with a pill button and three pastel feature cards.
- ✅ Do keep magenta strictly for glitch/danger states. → ❌ Don't use magenta as a hover or brand color.
- ✅ Do let body prose stay sentence case. → ❌ Don't uppercase whole paragraphs; caps are a scarce resource.

## Copy voice
The *system* speaks in clipped military-corporate caps; the *product* speaks plain and cocky in sentence case.

System strings:
- `HANDSHAKE OK // 0xA4F2 · 12ms`
- `TRACE COMPLETE — 2.4s · NO ALARMS`
- `SIGNAL LOST. RE-ROUTING…`

Product strings:
- "Your rig, their network. Ghostlink sits between them and makes you invisible."
- "Breach drills, live ICE maps, and exfil routes — one console, zero noise."
- "The corps built the walls. We built the door."

## Sources consulted
- CDPR senior graphic designer Irina Moraru on the 2077 yellow as "our most important brand element" (TweakTown Q&A): https://www.tweaktown.com/news/76570/cd-projekt-red-reveals-why-cyberpunk-2077s-cover-art-is-yellow/index.html
- heysami/woven — `design-library/aesthetic-cyberpunk.md`: palette anchors (#FCEE0A, #00F0FF, #FF2A6D, #2B1E45), one-accent rule, corner brackets, glitch-as-one-shot, forbidden imagery
- muris11/design-template — `skills/design-template-cyberpunk/SKILL.md`: neon glow token recipes, scanline/grid CSS, chromatic-aberration glitch recipe
- mmrahmanbappi/100-css-designs — neon cyberpunk CSS: layered text-shadow glow, glitch clip-path technique, scanline overlay, reduced-motion handling
- trueshadow01/cyberpunk2077website — 2077 fan design system: chamfered clip-paths, scanlines utility, HUD corner brackets, Rajdhani/JetBrains Mono stacks
- laetimes.com analysis of 2077 UI: diegetic UI as world-building (subtitles-as-translator-output framing)
