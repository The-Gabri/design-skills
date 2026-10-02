---
name: discord
description: Discord's blurple-and-charcoal gamer aesthetic — three-tone dark shell, server rail, chat-message anatomy — for community, gaming, and chat products.
---

# Discord

The Discord look: a dark, dense three-pane chat application built around
community servers. Surfaces are charcoal grays, the only saturated color is
**Blurple** (`#5865F2`), and the signature silhouette is the server icon
rail with squircle-to-circle icon morphing. Everything feels compact,
functional, and a little playful — built for people who live in group chat.

Sources: Discord brand guidelines (discord.com/branding) for brand colors and
the Clyde logo; the Discord desktop/web client for surface tokens, the server
rail, channel list, message anatomy, presence system, and gg sans typeface.

## Principles

1. **Dark-first, never inverted.** The app is charcoal at rest; dark themes are
   the default state, not an option. Light theme exists but is rarely seen.
2. **One accent rules.** Blurple is the only saturated color in the chrome —
   CTAs, mentions, active states, links. Everything else is gray or status.
3. **Three depths of gray.** Server rail (darkest) → channel/member panels →
   chat surface (lightest). Depth is communicated by background steps, not
   shadows.
4. **Density over whitespace.** Tight message rows, compact channel lists,
   12px metadata everywhere. It is a tool people stare at for hours; pixels
   are expensive.
5. **Playful voice, serious function.** The product copy jokes around
   ("Hanging out with...") while the UI itself is precise and information-dense.
6. **Presence is ambient.** Green/yellow/red dots on every avatar broadcast
   who's here without ever being asked.

## Color

Legend: ✅ official/documented · 🟡 cross-referenced · ⚠️ community approximation.

| Token | Hex | Role | Confidence |
|---|---|---|---|
| Blurple | `#5865F2` | Brand primary; CTAs, mentions, active states, links in marketing | ✅ |
| Blurple hover | `#4752C4` | Hover/pressed state of blurple buttons | 🟡 |
| Blurple light | `#7289DA` | Legacy blurple; secondary accent, selected items | ✅ |
| Green | `#57F287` | Brand green; success, confirmations | ✅ |
| Yellow | `#FEE75C` | Brand yellow; warnings, stars | ✅ |
| Fuchsia | `#EB459E` | Brand fuchsia; nitro/stream accents | ✅ |
| Red | `#ED4245` | Brand red; destructive actions, errors | ✅ |
| Online green | `#23A55A` | Presence dot, online status | ✅ |
| Idle yellow | `#F0B232` | Idle/away presence | 🟡 |
| DND red | `#F23F43` | Do-not-disturb presence | 🟡 |
| Offline gray | `#80848E` | Offline/invisible presence | 🟡 |
| Streaming purple | `#593695` | "Streaming" presence | 🟡 |
| BG tertiary | `#1E1F22` | Deepest surface: server rail, inputs | 🟡 |
| BG secondary | `#2B2D31` | Channel list, member list panels | 🟡 |
| BG primary | `#313338` | Main chat surface | 🟡 |
| BG floating | `#111214` | Modals, popovers, tooltips | 🟡 |
| Header primary | `#F2F3F5` | Usernames, channel headers | 🟡 |
| Text normal | `#DBDEE1` | Message body (cooler than pure white) | 🟡 |
| Text muted | `#949BA4` | Timestamps, secondary metadata | 🟡 |
| Channel muted | `#80848E` | Inactive channel names in sidebar | 🟡 |
| Link blue | `#00A8FC` | Hyperlinks inside messages (distinct from blurple) | 🟡 |
| Mention wash | `rgba(88,101,242,0.1)` | Background wash on rows that mention you | 🟡 |
| Divider | `rgba(78,80,88,0.4)` | 1px hairline rules between messages/groups | ⚠️ |

## Typography

- **UI font: "gg sans"** (proprietary, replaced Whitney in 2021). Closest free
  substitutes: `Inter`, or the system stack
  `"gg sans", "Helvetica Neue", Helvetica, Arial, sans-serif`. (🟡)
- **Display/brand font: Ginto** — used for marketing headlines and the
  wordmark. Closest free substitute: `Poppins` or a bold geometric sans. (🟡)
- **Code font: Consolas / "gg mono"** — code blocks and inline code use a
  monospace stack with a dark inset background. (🟡)
- Scale: compact. Message text ~16px/1.375, usernames 16px semibold,
  timestamps 12px muted, sidebar labels 12px uppercase with wide tracking
  (category headers like "TEXT CHANNELS"). Buttons 14px medium.

## Layout & spacing

- **3-column app shell** (desktop): 72px server rail (`#1E1F22`) →
  240px channel sidebar (`#2B2D31`) → flexible chat column (`#313338`);
  optional 240px member list on the right. (🟡)
- **Radius:** small and functional — 8px buttons, 4px inputs/embeds, 50%
  avatars and server icons (server icons are rounded squares that morph
  toward circles on hover/active — the "squircle-er" effect). (⚠️)
- **Shadows:** almost none inside the app. Floating layers (modals, tooltips)
  use a soft dark shadow; everything else is flat steps of gray.
- **Dividers:** 1px hairlines at low alpha, never hard borders. Channel rows
  are separated by spacing and hover states, not lines.
- **Active server indicator:** a white pill bar on the rail's leading edge —
  short rounded bar for unread, taller full bar for the selected server. (🟡)

## Components

### 1. Server rail
```html
<nav class="rail">
  <button class="rail-btn active"><span class="bar"></span><span class="icon">PF</span></button>
  <div class="rail-sep"></div>
  <button class="rail-btn unread"><span class="bar"></span><span class="icon">GG</span></button>
</nav>
<style>
.rail{background:#1e1f22;width:72px;display:flex;flex-direction:column;align-items:center;padding:12px 0;gap:8px}
.rail-btn{position:relative;width:48px;height:48px;border:0;background:transparent;cursor:pointer}
.rail-btn .icon{display:flex;width:48px;height:48px;border-radius:50%;background:#313338;color:#fff;
  align-items:center;justify-content:center;font-weight:700;transition:border-radius .15s,background .15s}
.rail-btn:hover .icon{border-radius:16px;background:#5865f2}
.rail-btn.active .icon{border-radius:16px;background:#5865f2}
.rail-btn .bar{position:absolute;left:-16px;top:50%;transform:translateY(-50%);width:4px;height:8px;
  border-radius:0 4px 4px 0;background:#fff;opacity:0;transition:height .15s,opacity .15s}
.rail-btn.active .bar{height:40px;opacity:1}
.rail-btn.unread .bar{height:8px;opacity:1}
.rail-sep{width:32px;height:2px;background:rgba(78,80,88,.6);border-radius:1px;margin:4px 0}
</style>
```

### 2. Channel list
```html
<aside class="channels">
  <button class="server-head">Pixel Forge <span>▾</span></button>
  <div class="cat">TEXT CHANNELS</div>
  <a class="chan active"># general</a>
  <a class="chan"># clips</a>
  <a class="chan lock"># mod-chat</a>
  <div class="cat">VOICE CHANNELS</div>
  <a class="chan voice"><svg width="16" height="16" viewBox="0 0 24 24" fill="currentColor"><path d="M3 9v6h4l5 5V4L7 9H3z"/><path d="M16 8a5 5 0 010 8" stroke="currentColor" stroke-width="2" fill="none"/></svg> Lobby <span class="vc-count">3</span></a>
  <div class="user-panel">…</div>
</aside>
<style>
.channels{background:#2b2d31;width:240px;display:flex;flex-direction:column;padding:0 8px 8px}
.server-head{background:none;border:0;color:#f2f3f5;font-weight:700;font-size:15px;text-align:left;
  padding:16px 8px;display:flex;justify-content:space-between;width:100%;cursor:pointer}
.cat{color:#949ba4;font-size:12px;font-weight:700;letter-spacing:.05em;padding:16px 8px 4px}
.chan{display:block;color:#80848e;font-size:15px;padding:6px 8px;border-radius:4px;text-decoration:none;cursor:pointer}
.chan:hover{background:rgba(78,80,88,.3);color:#dbdee1}
.chan.active{background:rgba(78,80,88,.6);color:#fff}
.chan.lock{opacity:.6}
.vc-count{float:right;font-size:12px}
</style>
```
Voice channels show who is connected as nested avatar rows; the channel name
is followed by a speaker count.

### 3. Chat message (the anatomy)
```html
<div class="msg">
  <img class="avatar" src="avatar.png" alt="">
  <div class="msg-body">
    <div class="msg-head"><span class="user role-mod">Nova</span><span class="time">Today at 21:14</span></div>
    <div class="msg-text">Clutch or kick, <span class="mention">@Milo</span> — your call.</div>
    <div class="reactions"><button class="react mine">🔥 2</button><button class="react">💀 5</button></div>
  </div>
</div>
<style>
.msg{display:flex;gap:16px;padding:4px 16px 4px 20px}
.msg:hover{background:rgba(4,4,5,.07)}
.avatar{width:40px;height:40px;border-radius:50%;flex-shrink:0}
.msg-head{display:flex;align-items:baseline;gap:8px}
.user{font-weight:600;color:#f2f3f5;font-size:16px}
.time{color:#949ba4;font-size:12px}
.msg-text{color:#dbdee1;font-size:16px;line-height:1.375}
.role-mod{color:#eb459e}
.mention{background:rgba(88,101,242,.3);color:#c7d2fe;border-radius:3px;padding:0 4px;cursor:pointer}
.mention:hover{background:#5865f2;color:#fff}
.reactions{display:flex;gap:4px;margin-top:4px}
.react{background:rgba(78,80,88,.3);border:1px solid rgba(78,80,88,.6);color:#dbdee1;border-radius:8px;
  font-size:14px;padding:2px 6px;cursor:pointer}
.react.mine{background:rgba(88,101,242,.3);border-color:#5865f2;color:#c7d2fe}
</style>
```
Usernames are colored by server role. Mentions highlight the whole row with
the blurple wash; a row that mentions *you* gets the wash plus a left edge bar.

### 4. User panel (bottom of channel list)
```html
<div class="me">
  <div class="avatar-wrap"><img src="you.png" alt=""><span class="dot online"></span></div>
  <div class="me-name">you<small>online</small></div>
  <div class="me-icons"><svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><circle cx="12" cy="12" r="3"/><path d="M19.4 15a1.65 1.65 0 0 0 .33 1.82l.06.06a2 2 0 1 1-2.83 2.83l-.06-.06a1.65 1.65 0 0 0-1.82-.33 1.65 1.65 0 0 0-1 1.51V21a2 2 0 1 1 4 0v-.09A1.65 1.65 0 0 0 9 19.4a1.65 1.65 0 0 0-1.82.33l-.06.06a2 2 0 1 1-2.83-2.83l.06-.06a1.65 1.65 0 0 0 .33-1.82 1.65 1.65 0 0 0-1.51-1H3a2 2 0 1 1 0-4h.09A1.65 1.65 0 0 0 4.6 9a1.65 1.65 0 0 0-.33-1.82l-.06-.06a2 2 0 1 1 2.83-2.83l.06.06a1.65 1.65 0 0 0 1.82.33H9a1.65 1.65 0 0 0 1-1.51V3a2 2 0 1 1 4 0v.09a1.65 1.65 0 0 0 1 1.51 1.65 1.65 0 0 0 1.82-.33l.06-.06a2 2 0 1 1 2.83 2.83l-.06.06a1.65 1.65 0 0 0-.33 1.82V9a1.65 1.65 0 0 0 1.51 1H21a2 2 0 1 1 0 4h-.09a1.65 1.65 0 0 0-1.51 1z"/></svg></div>
</div>
<style>
.me{background:#232428;margin:0 -8px -8px;padding:8px;display:flex;align-items:center;gap:8px}
.avatar-wrap{position:relative}
.dot{position:absolute;right:-2px;bottom:-2px;width:14px;height:14px;border-radius:50%;
  border:3px solid #232428;background:#23a55a}
.dot.online{background:#23a55a}.dot.idle{background:#f0b232}.dot.dnd{background:#f23f43}
.me-name{color:#f2f3f5;font-size:14px;font-weight:600;display:flex;flex-direction:column}
.me-name small{color:#949ba4;font-weight:400;font-size:12px}
</style>
```

### 5. Buttons
```html
<button class="btn">Join Server</button>
<button class="btn secondary">Cancel</button>
<button class="btn success">Accept</button>
<button class="btn danger">Delete</button>
<button class="btn link">Learn more</button>
<style>
.btn{background:#5865f2;color:#fff;border:0;border-radius:8px;padding:10px 16px;font-size:14px;font-weight:500;cursor:pointer}
.btn:hover{background:#4752c4}
.btn:active{background:#3c45a5}
.btn.secondary{background:#4e5058}.btn.secondary:hover{background:#6d6f78}
.btn.success{background:#23a55a}.btn.success:hover{background:#1a7f44}
.btn.danger{background:#ed4245}.btn.danger:hover{background:#c03537}
.btn.link{background:none;color:#00a8fc;padding:0}
</style>
```

### 6. Role badges & mention chips
Role badges are small uppercase pills next to usernames (`MOD`, `NITRO`).
Boost/level badges use the tier color (fuchsia for Nitro). Unread-mention
badges are red `#ed4245` pills with white numerals on the rail and channel
rows.

### 7. Embed (rich link / bot message)
```html
<div class="embed">
  <div class="embed-grid">
    <div>
      <div class="embed-author">PatchBot</div>
      <div class="embed-title">Patch 4.2 is live</div>
      <div class="embed-desc">Nova's ult now has a 90s cooldown.</div>
    </div>
    <img class="embed-thumb" src="patch.png" alt="">
  </div>
</div>
<style>
.embed{background:#2b2d31;border-left:4px solid #5865f2;border-radius:4px;padding:12px 16px 12px 12px;max-width:516px}
.embed-author{color:#fff;font-size:14px;font-weight:600}
.embed-title{color:#00a8fc;font-size:16px;font-weight:600}
.embed-desc{color:#dbdee1;font-size:14px}
.embed-grid{display:grid;grid-template-columns:1fr auto;gap:16px}
.embed-thumb{width:80px;height:80px;border-radius:8px;object-fit:cover}
</style>
```

### 8. Reaction chips
Pill chips under a message with emoji + count; the chip tints blurple with a
blurple border once you have reacted (see message component above). Clicking
toggles your reaction.

### 9. Toast / notification
```html
<div class="toast">Milo started streaming <b>Ranked Grind</b><button>Join</button></div>
<style>
.toast{background:#111214;color:#dbdee1;border-radius:8px;padding:12px 16px;font-size:14px;
  box-shadow:0 8px 24px rgba(0,0,0,.5);display:flex;gap:12px;align-items:center}
.toast button{background:#5865f2;color:#fff;border:0;border-radius:6px;padding:6px 12px;cursor:pointer}
</style>
```

## Motion

No documented signature motion language — Discord's UI is snappy and
functional. Hover/active states transition in ~100–150ms ease; server icons
morph radius on hover; channel switching cross-fades message lists. One line:
keep it fast and subtle, never decorative.

## Do / Don't

- ✅ Do stack three gray depths rail → panels → chat so depth reads without shadows.
- ✅ Do use Blurple for exactly one thing per screen (primary CTA or active state).
- ✅ Do color usernames by role and give every avatar a presence dot with a
  canvas-colored ring.
- ✅ Do write empty states like a friend: "No one's around to play with hmm."
- ❌ Don't use gradients in the app chrome — Discord surfaces are flat grays.
- ❌ Don't put two saturated brand colors (green + fuchsia) in the same CTA row.
- ❌ Don't round message rows into bubbles — Discord messages are flat rows,
  not chat bubbles.
- ❌ Don't use the link blue (`#00A8FC`) for buttons; it is for in-message
  hyperlinks only.

## Copy voice

Discord copy sounds like a funny friend who runs the group chat: lowercase
energy, gamer references, gentle roasts, zero corporate speak. CTAs are
conversational, empty states are jokes.

- "Hanging out with 3 friends in Lobby — hop in, we saved you a spot."
- "This channel is quiet... too quiet. Say something, coward."
- "Oops, looks like that invite expired. Classic."
