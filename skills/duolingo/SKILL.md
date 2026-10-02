---
name: duolingo
description: Duolingo's playful chunky gamified style — use for gamified learning UIs, kid-friendly products, and anything that should feel like a rewarding game.
---

# Duolingo

The look of duolingo.com and the Duolingo app: a mass-market education
product that wears its game-like personality on its sleeve. Learning is
reframed as play — streaks, XP, hearts, leagues — and the visual system
backs that up with chunky tactile buttons, one hero green, and type that
reads like a toy with confidence.

## Principles

1. **Gamification as the design language.** Every color, button, and
   micro-interaction serves motivation and retention: variable rewards
   (streaks, XP, gems), instant feedback, loss aversion (hearts),
   character-driven emotion. The UI should feel like a level, not a form.
2. **Tactile and chunky, never flat-washed.** Depth is physical, not
   atmospheric: solid colored bottom shadows (`0 4px 0`) read as a
   physical lip of thickness, and buttons literally depress on press.
   No blurred drop shadows, no glows, no gradients (outside skill nodes).
3. **One hero color + a semantic palette.** Feather Green `#58CC02`
   carries brand, primary actions, and success. Around it sits a fixed
   gamification accent system where each color has one meaning — they
   are never free decoration.
4. **Confidence through weight and roundness.** Buttons use bold,
   often uppercase, letter-spaced labels; borders are unusually thick
   (4px is the most common border width); radii are generous. Boldness
   plus warmth lowers the intimidation of learning.
5. **Encouragement is the copy default.** Failure states teach, never
   punish: "Oops —" not "Error", "Nice!" not "Correct". Celebrate
   everything; scold nothing.

## Color

Real Duolingo palette (the animal-named tokens from Duolingo's own
system, corroborated by public teardowns and Duolingo's design site).

| Token | Hex | Role | Legend |
|---|---|---|---|
| Feather green | `#58CC02` | Primary brand, primary CTAs, correct answers, completed nodes | ✅ |
| Feather green shade | `#46A302` | Darker shade — the 3D button "ledge" under green buttons | ✅ |
| Mask green | `#89E219` | Light green accent, growth/secondary emphasis | 🟡 |
| Macaw blue | `#1CB0F6` | Info, "Check" button, gems, Super | ✅ |
| Macaw blue shade | `#1899D6` | Darker shade — ledge under blue buttons | 🟡 |
| Cardinal red | `#FF4B4B` | Hearts, errors, wrong answers | ✅ |
| Fox orange | `#FF9600` | Streak flame | ✅ |
| Bee yellow | `#FFC800` | XP, crowns, mastery | ✅ |
| Beetle purple | `#CE82FF` | Accent, leagues | 🟡 |
| Eel | `#4B4B4B` | Primary text — dark charcoal, not black | ✅ |
| Wolf | `#AFAFAF` | Muted/secondary body text | 🟡 |
| Hare | `#CFCFCF` | Faint chrome, disabled states | 🟡 |
| Swan | `#E5E5E5` | Borders, hairlines | ✅ |
| Snow | `#F7F7F7` | Secondary background | 🟡 |
| Polar | `#FFFFFF` | Primary canvas — the signature snow-white background | ✅ |
| Night owl | `#131F24` | Dark-mode canvas (blue-tinted navy, not true black) | 🟡 |

Rules: green is reserved for primary action and positive feedback;
the warm spectrum (bee, fox, cardinal) is for gamification elements
only — streaks, hearts, XP — never general UI. White dominates;
color is punctuation.

## Typography

- **Display:** Feather Bold (✅ proprietary, by Johnson Banks, 2019) —
  ultra-rounded, heavy, slightly condensed. Closest free substitutes:
  **Baloo 2** or **Fredoka** (🟡 widely cited in teardowns).
- **UI/body:** Duolingo Sans / DIN Next Rounded Pro (✅ proprietary) —
  a rounded workhorse. Substitutes: **Nunito** / **Nunito Sans** /
  **Varela Round** (🟡). Only two weights exist: 500 and 700 —
  no light, no black.
- **Duolingo "loves bold":** body text routinely runs at 700.
  Button labels are ~17px, 700/800, **uppercase with letter-spacing**
  (~0.8px): `CHECK`, `CONTINUE`, `GOT IT`.
- **Scale:** 48–64px display headlines → 15px labels; tight
  line-height (1.17–1.2) on headings.

## Layout & spacing

- **Base unit 8px**; comfortable rhythm: 16px component gaps,
  48px section gaps on marketing, ~96px between big chapters.
- **Radii chunky and consistent:** 12px/16px on buttons and cards,
  full pill `9999px` on buttons and badges.
- **Borders thick:** 2–4px `swan` borders on cards and answer tiles;
  4px is the most common border width in the system.
- **Buttons are slabs:** `box-shadow: 0 4px 0 <darker-shade>` under a
  16px-radius button. On `:active`, `translateY(4px)` + shadow collapses
  to `0 0 0` — the button physically presses down.
- **App rhythm:** HUD strip on top (streak flame · gems · hearts),
  lesson card centered, one big action button anchored at the bottom
  of the viewport. Marketing rhythm: big hero in Feather, alternating
  two-column feature blocks, full-bleed green footer panel.
- **Min touch target 44×44px.**

## Components

Copy-pasteable HTML/CSS. Base context:
`body { background:#FFFFFF; color:#4B4B4B; font-family:Nunito,system-ui,sans-serif; }`

**1. Primary 3D button (the signature move)**

```html
<a class="duo-btn" href="#">Start learning</a>
<style>
.duo-btn{display:inline-flex;align-items:center;justify-content:center;
background:#58CC02;color:#fff;font:800 17px/1 Nunito,system-ui,sans-serif;
letter-spacing:.8px;text-transform:uppercase;text-decoration:none;
padding:14px 32px;border-radius:16px;border:0;
box-shadow:0 4px 0 #46A302;transition:transform .06s ease,box-shadow .06s ease}
.duo-btn:hover{filter:brightness(1.05)}
.duo-btn:active{transform:translateY(4px);box-shadow:0 0 0 #46A302}
</style>
```

**2. Blue 3D button (Check / action)**

```html
<button class="duo-check">Check</button>
<style>
.duo-check{background:#1CB0F6;color:#fff;font:800 17px/1 Nunito,system-ui,sans-serif;
letter-spacing:.8px;text-transform:uppercase;padding:14px 32px;border:0;
border-radius:16px;box-shadow:0 4px 0 #1899D6;cursor:pointer;
transition:transform .06s ease,box-shadow .06s ease}
.duo-check:active{transform:translateY(4px);box-shadow:0 0 0 #1899D6}
.duo-check:disabled{background:#CFCFCF;box-shadow:0 4px 0 #AFAFAF;cursor:not-allowed}
</style>
```

**3. Ghost 3D button (secondary, white)**

```html
<button class="duo-ghost">Maybe later</button>
<style>
.duo-ghost{background:#fff;color:#4B4B4B;font:800 17px/1 Nunito,system-ui,sans-serif;
letter-spacing:.8px;text-transform:uppercase;padding:12px 30px;border-radius:16px;
border:2px solid #E5E5E5;border-bottom-width:6px;cursor:pointer;
transition:transform .06s ease}
.duo-ghost:active{transform:translateY(4px);border-bottom-width:2px}
</style>
```

**4. Progress bar**

```html
<div class="duo-progress"><i style="width:35%"></i></div>
<style>
.duo-progress{height:16px;border-radius:999px;background:#E5E5E5;overflow:hidden}
.duo-progress i{display:block;height:100%;border-radius:999px;background:#58CC02;
box-shadow:inset 0 -4px 0 rgba(0,0,0,.08);transition:width .4s cubic-bezier(.34,1.56,.64,1)}
</style>
```

**5. Streak counter**

```html
<div class="duo-streak">
  <svg width="18" height="22" viewBox="0 0 18 22" fill="none">
    <path d="M9 0C9 6 3 8 3 14a6 6 0 0 0 12 0c0-3-2-4-2-7-3 1-4 3-4 3C8 6 9 3 9 0Z" fill="#FF9600"/>
  </svg>
  <b>12</b>
</div>
<style>
.duo-streak{display:inline-flex;align-items:center;gap:6px;font:800 17px Nunito,sans-serif;
color:#FF9600}
</style>
```

**6. Hearts**

```html
<div class="duo-hearts">
  <svg width="22" height="20" viewBox="0 0 22 20" fill="#FF4B4B"><path d="M11 20C6 14.5 1 10.7 1 5.9 1 2.9 3.4.5 6.5.5c2 0 3.6 1.1 4.5 2.8C11.9 1.6 13.5.5 15.5.5c3.1 0 5.5 2.4 5.5 5.4 0 4.8-5 8.6-10 14.1Z"/></svg>
  <b>3</b>
</div>
<style>
.duo-hearts{display:inline-flex;align-items:center;gap:6px;font:800 17px Nunito,sans-serif;
color:#FF4B4B}
.duo-hearts.lost svg{fill:#E5E5E5}
</style>
```

**7. XP bar with lightning badge**

```html
<div class="duo-xp"><span class="duo-xp-badge"><svg width="14" height="18" viewBox="0 0 14 18"><path d="M8 0 0 10h4l-1 8 7-10H6l2-8Z" fill="#fff"/></svg></span><div class="duo-xp-track"><i style="width:60%"></i></div></div>
<style>
.duo-xp{display:flex;align-items:center;gap:10px}
.duo-xp-badge{width:32px;height:32px;border-radius:50%;background:#FFC800;
display:flex;align-items:center;justify-content:center;box-shadow:0 3px 0 #D9A500}
.duo-xp-track{flex:1;height:12px;border-radius:999px;background:#E5E5E5;overflow:hidden}
.duo-xp-track i{display:block;height:100%;background:#FFC800;border-radius:999px;
box-shadow:inset 0 -3px 0 rgba(0,0,0,.08);transition:width .5s cubic-bezier(.34,1.56,.64,1)}
</style>
```

**8. Lesson card with word-bank answer**

```html
<div class="duo-lesson">
  <p class="duo-hint">Translate this sentence</p>
  <h2 class="duo-prompt">The boy drinks water.</h2>
  <div class="duo-answer"></div>
  <div class="duo-bank">
    <button class="duo-chip">el</button>
    <button class="duo-chip">niño</button>
    <button class="duo-chip">bebe</button>
    <button class="duo-chip">agua</button>
  </div>
</div>
<style>
.duo-lesson{max-width:560px;margin:0 auto;padding:24px}
.duo-hint{font:700 15px Nunito,sans-serif;color:#AFAFAF;text-transform:uppercase;letter-spacing:.8px}
.duo-prompt{font:800 28px "Baloo 2",Nunito,sans-serif;color:#4B4B4B;margin:8px 0 24px}
.duo-answer{min-height:56px;border-bottom:2px solid #E5E5E5;display:flex;flex-wrap:wrap;gap:10px;margin-bottom:24px}
.duo-bank{display:flex;flex-wrap:wrap;gap:10px;justify-content:center}
.duo-chip{background:#fff;border:2px solid #E5E5E5;border-bottom-width:4px;
border-radius:12px;padding:10px 16px;font:700 17px Nunito,sans-serif;color:#4B4B4B;cursor:pointer}
.duo-chip:active{transform:translateY(2px);border-bottom-width:2px}
.duo-chip.used{visibility:hidden}
</style>
```

**9. League leaderboard row**

```html
<div class="duo-league-row first"><span class="rank">1</span><span class="avatar">M</span><span class="name">Marta</span><span class="pts">1,240 XP</span></div>
<style>
.duo-league-row{display:flex;align-items:center;gap:12px;padding:12px 16px;
border:2px solid #E5E5E5;border-radius:16px;font:700 16px Nunito,sans-serif}
.duo-league-row.first{border-color:#FFC800;background:#FFFBEA}
.duo-league-row .rank{font:800 16px Nunito,sans-serif;color:#AFAFAF;width:24px;text-align:center}
.duo-league-row .avatar{width:36px;height:36px;border-radius:50%;background:#1CB0F6;
color:#fff;display:flex;align-items:center;justify-content:center;font:800 16px Nunito,sans-serif}
.duo-league-row .name{flex:1;color:#4B4B4B}
.duo-league-row .pts{color:#FFC800;font-weight:800}
</style>
```

**10. Celebration modal (lesson complete)**

```html
<div class="duo-celebrate">
  <h2>Lesson complete!</h2>
  <p>+20 XP &nbsp;·&nbsp; 12-day streak</p>
  <button class="duo-btn">Continue</button>
</div>
<style>
.duo-celebrate{background:#58CC02;color:#fff;text-align:center;padding:48px 24px;border-radius:24px}
.duo-celebrate h2{font:800 36px "Baloo 2",Nunito,sans-serif;margin:0 0 8px}
.duo-celebrate p{font:700 18px Nunito,sans-serif;margin:0 0 24px;color:#D7FFB8}
.duo-celebrate .duo-btn{background:#fff;color:#58CC02;box-shadow:0 4px 0 #46A302}
</style>
```

## Motion

Duolingo doesn't publish easing specs; what teardowns document is a
signature feel: bouncy, springy, tactile. Presses are instant
(~60ms); fills and score popups use a springy overshoot like
`cubic-bezier(.34,1.56,.64,1)` over 300–500ms. Characters wiggle and
celebration screens bounce in. When in doubt: springy in, instant out,
nothing linear or floaty.

## Do / Don't

- **Do** give every button a solid 4px darker-shade ledge and a press
  that collapses it — **don't** use soft blurred shadows or glows.
- **Do** write button labels uppercase, 800 weight, letter-spaced
  (`CHECK`, `CONTINUE`) — **don't** write sentence-case labels.
- **Do** reserve feather green for the primary action and success —
  **don't** make every panel green; color is punctuation on white.
- **Do** use the warm spectrum semantically: orange = streak,
  yellow = XP, red = hearts/errors — **don't** reassign them
  (red is never "delete", blue is never "error").
- **Do** run body text at 700 weight with friendly tracking —
  **don't** drop to thin/light weights; the brand never whispers.
- **Do** make failure kind: show the correct answer, keep the tone
  warm, cost one heart — **don't** flash "ERROR" or lock the user out.
- **Do** celebrate completion with a full-bleed green takeover —
  **don't** dismiss progress with a quiet toast.

## Copy voice

Encouraging, quirky, coach-like. Celebrates small wins out loud;
never scolds. Short exclamations, playful nudges, mascot energy
(without quoting the mascot).

- "Amazing! You've hit a 12-day streak — keep the fire burning."
- "Oops — the correct answer is *el gato*. You'll get the next one!"
- Nudge: "Your streak is in danger. Duo believes in you. Tap to keep it alive."
