---
name: twitch
description: Twitch's streamer aesthetic — near-black canvas, Twitch Purple CTAs, red LIVE badges, stream-card grids, and the docked community chat — for live-streaming-style UIs.
---

# Twitch

The visual language of Twitch (twitch.tv): a dark, community-first product
system where the chrome stays near-black and quiet so live content screams.
Purple is the brand's heartbeat, red means LIVE and nothing else, and chat
is a first-class citizen — always docked, always moving.

> Style reference only. Do not reproduce the Twitch wordmark, the Glitch
> mascot, or Roobert — always build with fictional streamers/content and
> the substitute typefaces below.

## Principles

1. **Quiet chrome, kinetic content.** The interface is achromatic
   (`#0E0E10` / `#18181B`) by design; saturation lives inside thumbnails,
   category art, and avatars. Twitch's own dark-mode docs call it "quiet
   chrome, kinetic content". (🟡)
2. **Purple is the only brand voice.** Twitch Purple (`#9146FF`) carries
   the logo, Follow/Subscribe CTAs, links, focus rings, and live-avatar
   rings. It is never diluted into decoration. (✅ official brand rule)
3. **Red means LIVE, nothing else.** The LIVE pill is vivid red (`#EB0400`)
   — and red never appears on buttons, icons, or badges that aren't about
   liveness. (🟡 cross-referenced in multiple teardowns)
4. **Chat is the community.** Chat is always docked beside the stream:
   badges, colored usernames, emote tokens, and a one-line composer. It
   scrolls continuously and is the signature social surface. (✅ product)
5. **Rounded almost nothing.** Twitch's radius scale is tiny: cards at
   4px, badges at 2px, pills at 9000px. Sharp, compact, dense — never
   pill-everything. (🟡 documented at 2–4px on product cards)
6. **Density over breathing room.** Thumbnails nearly touch (gaps ~4–8px),
   type runs 12–16px, sections are rails not hero statements. It reads
   like a control room, not a landing page. (🟡)

## Color

| Token | Hex | Role | Legend |
|---|---|---|---|
| Twitch Purple | `#9146FF` | Brand, primary CTA, links, focus rings, live-avatar ring | ✅ |
| Purple Hover | `#772CE8` | Hover/pressed state on purple CTAs | 🟡 |
| Purple Active | `#5C16C5` | Link text, active toggle states, deep brand work | 🟡 |
| Purple (dark mode bright) | `#BF94FF` | Active/purple text on dark backgrounds | 🟡 |
| Purple Link (dark) | `#A970FF` | Hover link color on dark canvas | 🟡 |
| LIVE Red | `#EB0400` | LIVE badge fill ONLY — never purple, never elsewhere | 🟡 |
| Canvas | `#0E0E10` | Page background, near-black with a faint cool tint | 🟡 |
| Surface | `#18181B` | Cards, sheets, the chat column, elevated rows | 🟡 |
| Surface 2 | `#1F1F23` | Modals, chat input, active rows, chips | ⚠️ |
| Divider | `#2A2A2D` | 1px separators between rows and blocks | ⚠️ |
| Text Primary (dark) | `#EFEFF1` | Headings and body text on dark | 🟡 |
| Text Muted | `#ADADB8` | Metadata, timestamps, viewer counts, secondary labels | 🟡 |
| Text Primary (light) | `#0E0E10` | Text on light backgrounds | 🟡 |
| White | `#FFFFFF` | LIVE badge text, CTA text, logo | ✅ |
| Status Green | `#00C853` | "Online" / success states (rarely; chat uses badges) | ⚠️ |
| Viewer Chip | `rgba(0,0,0,0.6)` | Translucent dark overlay behind viewer counts on thumbnails | 🟡 |

Sources: Twitch identity guidelines (brand.twitch.tv) for Purple/White/
Black; product teardowns (shadcn.io/design/twitch, fivetaku/insane-design,
axhub-make) for the dark surface stack, text tones, LIVE red, and the
purple ladder `#9146FF → #772CE8 → #5C16C5`.

## Typography

- **Face (official):** Roobert — Twitch's custom face (2019, Collins),
  named for synth pioneer Robert Moog. Mono-linear, geometric, slightly
  quirky. (✅)
- **Closest free substitutes (⚠️ community guidance):**
  - Display / headings → **Inter Medium (500)** at -0.2px tracking, or the
    system stack. This is what Twitch's own CSS stack effectively falls
    back to and it's the closest open stand-in.
  - UI / body → **Inter** (or system stack) — 14px chrome labels at
    400/600, 19.6px line-height, zero letter-spacing.
- **Scale:** section headers 18px, weight 500, -0.18px tracking; card
  titles 14px 600; metadata 12–13px muted; chat 13px 400; LIVE pill 10–11px
  700 uppercase.
- **Rules:** headings get the display face, everything else Inter.
  Sentence case everywhere except the LIVE badge (always uppercase).
  Never put body copy in the display face.

## Layout & spacing

- **Shell:** top nav 5rem (80px) tall; left "followed channels" rail
  24rem (384px) wide (collapsible to 5rem); chat column ~340px on the
  right in the stream view. (🟡 documented)
- **Stream view:** video on top-left filling the space between rails,
  chat docked in a full-height right column — this video-left/chat-right
  split is the single most recognizable Twitch layout. (✅)
- **Discovery grid:** thumbnails nearly touch — 4–8px gaps, not 24px.
  Cards have NO box-shadow and NO border by default; on hover/focus a
  2px solid `#9146FF` ring appears around the thumbnail. (🟡)
- **Radii:** cards 4px, badges 2px, CTAs full pill (9000px), search input
  6px. No rounded-xl card corners. (🟡)
- **Search:** max-width ~40rem, height 3rem, radius 6px, dark surface
  fill. (🟡)
- **Spacing rhythm:** 4 / 8 / 12 / 16px steps; section headers get
  16px bottom margin; cards sit in sections like "Live channels we think
  you'll like" — plain 18px/500 sentence-case headers, no eyebrow labels.

## Components

Base context: `body { background:#0E0E10; color:#EFEFF1;
font-family:Inter, system-ui, -apple-system, "Segoe UI", Roboto, sans-serif; }`.
Use the `tw-` prefix on all classes.

**1. Stream card with LIVE badge** (signature) — thumbnail + red LIVE pill
+ viewer chip, then title/streamer/category lines

```html
<a class="tw-card" href="#">
  <span class="tw-thumb">
    <span class="tw-live">LIVE</span>
    <span class="tw-viewers">12.4K viewers</span>
    <span class="tw-art">PIXELNOVA</span>
  </span>
  <span class="tw-card-meta">
    <span class="tw-avatar"></span>
    <span class="tw-card-text">
      <b class="tw-card-title">GRANDMASTER CLIMB — no breaks until Diamond</b>
      <span class="tw-card-name">PixelNova</span>
      <span class="tw-card-cat">Starfall Odyssey</span>
      <span class="tw-tags"><i>English</i><i>Ranked</i></span>
    </span>
  </span>
</a>
<style>
.tw-card{display:block;width:300px;text-decoration:none;color:#EFEFF1}
.tw-thumb{position:relative;display:block;aspect-ratio:16/9;border-radius:4px;
  background:linear-gradient(135deg,#5C16C5 0%,#9146FF 60%,#BF94FF 100%);
  border:2px solid transparent;transition:border-color .15s}
.tw-card:hover .tw-thumb,.tw-card:focus-visible .tw-thumb{border-color:#9146FF}
.tw-live{position:absolute;top:8px;left:8px;background:#EB0400;color:#fff;
  font-size:10px;font-weight:700;letter-spacing:.06em;padding:3px 8px;border-radius:2px}
.tw-viewers{position:absolute;bottom:8px;left:8px;background:rgba(0,0,0,.6);color:#fff;
  font-size:12px;padding:3px 8px;border-radius:4px}
.tw-art{position:absolute;inset:0;display:flex;align-items:center;justify-content:center;
  font-weight:700;font-size:26px;letter-spacing:.08em;color:rgba(255,255,255,.85)}
.tw-card-meta{display:flex;gap:10px;margin-top:10px}
.tw-avatar{flex:0 0 40px;width:40px;height:40px;border-radius:50%;
  background:linear-gradient(135deg,#1F1F23,#2A2A2D)}
.tw-card-text{display:flex;flex-direction:column;gap:2px;min-width:0}
.tw-card-title{font-size:14px;font-weight:600;line-height:1.3;white-space:nowrap;
  overflow:hidden;text-overflow:ellipsis}
.tw-card-name,.tw-card-cat{font-size:13px;color:#ADADB8}
.tw-card-name:hover{color:#A970FF}
.tw-tags{display:flex;gap:6px;margin-top:4px}
.tw-tags i{font-style:normal;font-size:11px;color:#ADADB8;background:#1F1F23;
  border-radius:9000px;padding:2px 10px}
</style>
```
Note: title is bold and truncates to one line; streamer name and category
are 13px muted. The thumbnail shows NO shadow and NO border until hover.

**2. LIVE badge** (standalone)

```html
<span class="tw-live">LIVE</span>
```
Same style as above: `#EB0400`, white, 10px/700, uppercase, 2px radius.
Rule: LIVE badges are always red — never purple. Purple on a live state
reads as a different platform. (🟡)

**3. Chat message** (signature) — badge, colored username, emote tokens

```html
<p class="tw-msg"><span class="tw-badge sub">SUB</span><b class="tw-user" style="color:#FF6961">RiftRunner</b>: that last play was insane POGGERS</p>
<p class="tw-msg"><span class="tw-badge mod">MOD</span><b class="tw-user" style="color:#1E90FF">NovaMod</b>: welcome in, raiders! rules in the panels below</p>
<p class="tw-msg tw-join"><i>EmberFox subscribed for 14 months!</i></p>
<style>
.tw-msg{font-size:13px;line-height:1.6;margin:0 0 6px;color:#EFEFF1}
.tw-badge{display:inline-block;font-size:10px;font-weight:700;letter-spacing:.04em;
  color:#fff;border-radius:2px;padding:1px 6px;margin-right:6px}
.tw-badge.sub{background:#9146FF}
.tw-badge.mod{background:#00C853}
.tw-badge.vip{background:#EAB308;color:#0E0E10}
.tw-user{font-weight:700;margin-right:2px}
.tw-join{font-size:12px;color:#ADADB8;font-style:italic}
</style>
```
Real detail: usernames carry user-chosen colors (chatter's own color
choice); badges precede the name; emotes are inline tokens like
`POGGERS` / `KEKW` / `GG` rendered as plain caps in our static demo. (🟡)

**4. Chat panel** (signature) — header, scrollback, composer

```html
<aside class="tw-chat">
  <header class="tw-chat-head">STREAM CHAT <button class="tw-ghost" aria-label="Chat settings"><svg viewBox="0 0 24 24" width="16" height="16" fill="none" stroke="#ADADB8" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><circle cx="12" cy="12" r="3"/><path d="M12 2v3M12 19v3M2 12h3M19 12h3M4.9 4.9l2.1 2.1M17 17l2.1 2.1M19.1 4.9 17 7M7 17l-2.1 2.1"/></svg></button></header>
  <div class="tw-chat-scroll">
    <p class="tw-msg"><b class="tw-user" style="color:#BF94FF">GlitchFan</b>: the emote wall is going off KEKW</p>
  </div>
  <form class="tw-chat-form">
    <input class="tw-chat-input" placeholder="Send a message" aria-label="Send a message">
    <button class="tw-chat-send" type="submit">Chat</button>
  </form>
</aside>
<style>
.tw-chat{display:flex;flex-direction:column;width:340px;height:600px;background:#18181B;
  border-left:1px solid #2A2A2D}
.tw-chat-head{display:flex;align-items:center;justify-content:space-between;
  font-size:12px;font-weight:600;letter-spacing:.06em;color:#EFEFF1;
  padding:12px 16px;border-bottom:1px solid #2A2A2D}
.tw-ghost{background:none;border:0;color:#ADADB8;cursor:pointer;font-size:16px}
.tw-chat-scroll{flex:1;overflow-y:auto;padding:12px 16px}
.tw-chat-form{padding:12px 16px;border-top:1px solid #2A2A2D;display:flex;gap:8px}
.tw-chat-input{flex:1;background:#1F1F23;border:1px solid transparent;border-radius:6px;
  color:#EFEFF1;font-size:13px;padding:9px 12px}
.tw-chat-input:focus{outline:none;border-color:#9146FF}
.tw-chat-send{background:#9146FF;color:#fff;border:0;border-radius:4px;font-size:13px;
  font-weight:600;padding:0 16px;cursor:pointer}
.tw-chat-send:hover{background:#772CE8}
.tw-chat-send:active{background:#5C16C5}
</style>
```

**5. Follow button** (primary CTA — pill, purple)

```html
<button class="tw-follow">Follow</button>
<button class="tw-follow on">Following</button>
<style>
.tw-follow{background:#9146FF;color:#fff;border:0;border-radius:9000px;
  font-size:13px;font-weight:600;padding:8px 20px;cursor:pointer}
.tw-follow:hover{background:#772CE8}
.tw-follow:active{background:#5C16C5}
.tw-follow.on{background:#1F1F23;color:#EFEFF1}
.tw-follow.on:hover{background:#2A2A2D}
</style>
```
Real detail: after following, the button flips to a dark "Following"
pill — the CTA stays in the same place, only the state changes. (🟡)

**6. Category pills** (filter chips)

```html
<div class="tw-pills"><button class="on">Games</button><button>IRL</button><button>Music</button><button>Esports</button></div>
<style>
.tw-pills{display:flex;gap:8px}
.tw-pills button{background:#1F1F23;color:#EFEFF1;border:0;border-radius:9000px;
  font-size:13px;padding:7px 16px;cursor:pointer}
.tw-pills button:hover{background:#2A2A2D}
.tw-pills button.on{background:#9146FF;color:#fff;font-weight:600}
</style>
```

**7. Top nav** (80px, dark, search centered)

```html
<nav class="tw-nav">
  <a class="tw-brand" href="#" aria-label="Home">
    <svg viewBox="0 0 24 24" width="28" height="28" fill="#9146FF"><path d="M4 2 2.5 6v14h5v3h3l3-3h4l5-5V2H4zm16 11-3 3h-4l-3 3v-3H6V4h14v9zM17 7h-2v5h2V7zm-5 0h-2v5h2V7z"/></svg>
  </a>
  <a class="tw-nav-link on" href="#">Following</a>
  <a class="tw-nav-link" href="#">Browse</a>
  <div class="tw-search"><input placeholder="Search" aria-label="Search"></div>
  <div class="tw-nav-right">
    <button class="tw-nav-icon" aria-label="Notifications"><svg viewBox="0 0 24 24" width="20" height="20" fill="none" stroke="#EFEFF1" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"><path d="M18 8a6 6 0 0 0-12 0c0 7-3 9-3 9h18s-3-2-3-9"/><path d="M13.7 21a2 2 0 0 1-3.4 0"/></svg><i class="tw-dot"></i></button>
    <button class="tw-login">Log In</button>
    <button class="tw-signup">Sign Up</button>
  </div>
</nav>
<style>
.tw-nav{height:80px;display:flex;align-items:center;gap:20px;padding:0 16px;
  background:#18181B;border-bottom:1px solid #0E0E10}
.tw-nav-link{color:#EFEFF1;font-size:14px;text-decoration:none;font-weight:600;
  border-bottom:2px solid transparent;padding-bottom:4px}
.tw-nav-link:hover{color:#A970FF}
.tw-nav-link.on{color:#BF94FF;border-color:#9146FF}
.tw-search{flex:1;max-width:640px;margin:0 auto}
.tw-search input{width:100%;height:48px;background:#1F1F23;border:1px solid transparent;
  border-radius:6px;color:#EFEFF1;font-size:14px;padding:0 16px}
.tw-search input:focus{outline:none;border-color:#9146FF}
.tw-nav-right{margin-left:auto;display:flex;align-items:center;gap:10px}
.tw-nav-icon{position:relative;background:none;border:0;font-size:20px;cursor:pointer}
.tw-dot{position:absolute;top:2px;right:2px;width:10px;height:10px;border-radius:50%;
  background:#EB0400;border:2px solid #18181B}
.tw-login{background:transparent;border:0;color:#EFEFF1;font-size:13px;font-weight:600;
  padding:8px 16px;border-radius:4px;cursor:pointer}
.tw-login:hover{background:#2A2A2D}
.tw-signup{background:#9146FF;border:0;color:#fff;font-size:13px;font-weight:600;
  border-radius:4px;padding:8px 16px;cursor:pointer}
.tw-signup:hover{background:#772CE8}
</style>
```
Real detail: the notification badge is the SAME red as LIVE (`#EB0400`) —
red is reserved for "happening now" signals. Sign Up is a small purple
block (4px radius, not a pill) on the real product. (🟡)

**8. Toast / subscription notification**

```html
<div class="tw-toast">
  <span class="tw-toast-icon">★</span>
  <p><b>EmberFox</b> just subscribed — 14 months in a row!</p>
  <button aria-label="Dismiss">✕</button>
</div>
<style>
.tw-toast{display:flex;align-items:center;gap:12px;background:#1F1F23;
  border-left:3px solid #9146FF;border-radius:4px;padding:12px 16px;
  max-width:380px;box-shadow:0 8px 24px rgba(0,0,0,.5)}
.tw-toast-icon{width:32px;height:32px;border-radius:50%;background:#9146FF;color:#fff;
  display:flex;align-items:center;justify-content:center;font-size:16px;flex:0 0 32px}
.tw-toast p{font-size:13px;margin:0;flex:1}
.tw-toast button{background:none;border:0;color:#ADADB8;cursor:pointer}
</style>
```
Twitch toasts slide in bottom-right over the video; hype-train and
sub/gift notifications carry the purple left-border + glow. (⚠️)

**9. Left-rail channel row** (followed channels)

```html
<button class="tw-row">
  <span class="tw-row-avatar live"></span>
  <span class="tw-row-text"><b>RiftRunner</b><i>Neon Siege</i></span>
  <span class="tw-row-viewers">8.2K</span>
</button>
<style>
.tw-row{display:flex;align-items:center;gap:10px;width:100%;background:none;border:0;
  padding:8px 16px;cursor:pointer;text-align:left}
.tw-row:hover{background:#1F1F23}
.tw-row-avatar{position:relative;width:32px;height:32px;border-radius:50%;
  background:linear-gradient(135deg,#2A2A2D,#18181B);flex:0 0 32px}
.tw-row-avatar.live::after{content:"";position:absolute;inset:-3px;border-radius:50%;
  border:2px solid #EB0400}
.tw-row-text{display:flex;flex-direction:column;min-width:0;flex:1}
.tw-row-text b{font-size:14px;font-weight:600;color:#EFEFF1;white-space:nowrap;overflow:hidden;text-overflow:ellipsis}
.tw-row-text i{font-style:normal;font-size:12px;color:#ADADB8}
.tw-row-viewers{font-size:12px;color:#ADADB8}
</style>
```
Real detail: a live channel's avatar gets a RED ring (not purple) —
liveness again; purple rings mark channels going live in recommendations.
Viewer counts show live. (🟡)

**10. Raid/host banner** (channel-offline CTA)

```html
<div class="tw-offline">
  <p class="tw-offline-title">NovaForge is offline</p>
  <p class="tw-offline-sub">They usually stream Tue–Thu at 6 PM. Get notified when they're back.</p>
  <button class="tw-follow">Turn On Notifications</button>
</div>
<style>
.tw-offline{background:#18181B;border-radius:4px;padding:32px;text-align:center;max-width:520px}
.tw-offline-title{font-size:18px;font-weight:500;margin:0 0 8px}
.tw-offline-sub{font-size:14px;color:#ADADB8;margin:0 0 20px}
</style>
```

## Motion

- **LIVE pill:** the red dot/pill pulses (subtle 2s `ease-in-out`
  opacity/breath loop) — the single most recognizable Twitch motion. (🟡)
- **Card hover:** instant 2px purple ring on the thumbnail, no scale, no
  shadow — ~150ms. Twitch does not do the Netflix hover-zoom. (🟡)
- **Viewer counts tick:** numbers update every ~30s while live; in product
  copy they feel "happening now". (🟡)
- **Chat:** new messages slide in from the bottom, ~200ms `ease-out`;
  toasts slide up from bottom-right over the video. (⚠️)
- No page-load choreography, no parallax. Motion serves "it's live now",
  never decoration.

## Do / Don't

- **Do** make the LIVE badge `#EB0400` red on every thumbnail —
  **don't** ever render it in Twitch Purple; purple-on-live reads as a
  different platform and breaks the one job red has.
- **Do** give thumbnails no border and no shadow by default, then a 2px
  `#9146FF` ring on hover — **don't** put permanent borders or soft
  shadows on stream cards.
- **Do** keep the radius scale tiny (badges 2px, cards 4px, CTAs pill) —
  **don't** round stream cards to rounded-xl; it kills the dense
  control-room feel.
- **Do** dock chat in a full-height right column beside the stream —
  **don't** hide chat behind a tab or overlay it by default on desktop.
- **Do** write card titles in 14px semibold that truncate to one line with
  muted 13px streamer/category lines — **don't** center card text or grow
  it to 18px headlines.
- **Do** color usernames per-chatter (their chosen color) with badges
  before the name — **don't** render chat as uniform grey text; color is
  identity in Twitch chat.
- **Do** keep the notification badge and LIVE pill the same red —
  **don't** use red for errors, delete buttons, or decorative icons.
- **Do** make "Sign Up" a small purple rectangle (4px radius) and
  "Follow" a purple pill — **don't** swap them; each CTA has its shape.

## Copy voice

Hype, conspiratorial, community-owned. Short punchy lines, streamer
slang, and the emote lexicon (POGGERS, KEKW, GG, HYPE) — it talks like a
chat that's moving too fast to scroll. "You're already one of us" is the
brand's actual rebrand slogan (Collins, 2019). Calls to action are verbs,
not promises.

- Hero CTA: "Going live in 5. The raid train starts here."
- Community banner: "Join the Twitch community — you're already one of us."
- Chat system line: "EmberFox just gifted 10 subs to the chat. HYPE."
- Error/empty: "This channel is offline right now. The VODs are waiting."
