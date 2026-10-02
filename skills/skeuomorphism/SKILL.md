---
name: skeuomorphism
description: iOS 6-era skeuomorphism — leather, linen, wood, green felt, brushed metal, stitched seams, glossy gel buttons and embossed type, as shipped in iOS 1–6 (2007–2012).
---

# Skeuomorphism (iOS 6 era)

## Legend
- ✅ = documented in Apple's iOS 6-era HIG / SDK behavior, confirmed in ≥2 independent sources.
- 🟡 = widely cross-referenced in contemporary teardowns and recreations; behavior is agreed, exact values vary.
- ⚠️ = community approximation (useful, not dogma).

## Purpose
Produce interfaces that look and feel like Apple's software from the Scott Forstall era — iOS 1 through iOS 6 (2007–2012), peaking with iOS 6 and OS X Mountain Lion. Every control references a physical object; light, texture and stitching carry the information architecture. Use it for retro product pages, nostalgia-driven marketing, or interfaces that want warmth and tactile affordance over minimalism.

Historical anchor: iOS 6 (Sept 2012) was the last release under Scott Forstall, Apple's chief skeuomorphism proponent; Jony Ive's flat iOS 7 (2013) replaced linen, leather and gloss with flat surfaces ("people had already become comfortable with touching glass"). 🟡

## Principles
1. **Metaphor is the interface.** A calendar is a leather datebook (Calendar), a notes app is a yellow legal pad (Notes), a newsstand is a wooden shelf (Newsstand/iBooks), settings panels are machined metal. The user never has to learn what a control does — the object tells them. ✅
2. **Materials signal zones.** Linen = system furniture (folders, Notification Center, multitasking tray). Leather = bound collections (Calendar, Contacts, Reminders, Find My Friends). Wood = shelves of things (iBooks, Newsstand). Green felt = the game table (Game Center). Brushed metal = machinery (iTunes). Keep one material per semantic zone. 🟡
3. **Light always comes from above.** Every raised surface gets a 1px top inner highlight; every shadow falls below. Text is embossed on dark surfaces and engraved on light ones — never flat against its background. 🟡
4. **Pressable things glisten.** Buttons, switches, segmented controls and app icons carry a top-half gloss (the "gel" highlight); static content areas never do. The gloss is the affordance. 🟡
5. **Craft details are structural, not decoration.** Stitched seams mark where two materials meet (leather nav headers), torn page edges and ruled lines make paper feel cut and bound (Passbook's paper-shredder delete animation reinforced that data was gone). ✅
6. **Warmth over efficiency.** Drop shadows, felt grain, gold trim and realistic knobs cost pixels on purpose — the era's argument was that software should feel valuable and hand-made, the way flat design later argued it should get out of the way. ⚠️

## Color
Palette of the era — base material tones, cross-referenced against iOS 6 screenshots and CSS recreations:

| Token | Hex | Role |
|---|---|---|
| `--linen` | `#c9cbcd` ⚠️ | System furniture: folders, Notification Center, trays (dark variant `#2e2e2e` for the notification shade) |
| `--leather-dark` | `#4a3421` ⚠️ | Bound covers: Calendar/Contacts/Reminders chrome |
| `--leather-tan` | `#8a5a33` ⚠️ | Calendar's "tan patent-leather" datebook look |
| `--stitch` | `#d9c69a` ⚠️ | Thread color for stitched seams on leather |
| `--felt` | `#3f6b34` ⚠️ | Game Center green baize table |
| `--wood` | `#6f4a2c` ⚠️ | iBooks/Newsstand shelves (darker iTunes U variant `#4e3823` ⚠️) |
| `--paper` | `#fdf6c8` ⚠️ | Notes yellow legal pad |
| `--rule-blue` | `#a9c6df` ⚠️ | Ruled lines on the legal pad |
| `--margin-red` | `#e5a3a3` ⚠️ | Red margin line on the legal pad |
| `--metal` | `#c7ccd1` ⚠️ | Brushed aluminum panels (machinery zones) |
| `--chrome-blue-hi` | `#8fb0dd` ⚠️ | Top of default nav-bar / button blue gradient |
| `--chrome-blue-lo` | `#4d7ab8` ⚠️ | Bottom of default nav-bar / button blue gradient |
| `--ink-dark` | `#1c1c1c` 🟡 | Primary text on light materials |
| `--ink-light` | `#f2ede2` 🟡 | Embossed text on dark materials |

Text treatment (the rule, not the hex): on dark, type is embossed — light fill with `text-shadow: 0 -1px 0 rgba(0,0,0,.6)`; on light, type is engraved — dark fill with `text-shadow: 0 1px 0 rgba(255,255,255,.6)`. 🟡

## Typography
- **Helvetica Neue** (system font of iOS 6; weights: regular, medium, bold) — all chrome, buttons, table rows. ✅
- **Marker Felt** — Notes app body text only; never for chrome or headings. ✅
- Type scale of the era: nav-bar titles ~17–20pt bold, table rows 17pt, section headers 17pt bold uppercase-ish gray, button labels 15–17pt bold. 🟡
- Headings in marketing of the era leaned on big Helvetica Neue Light/Thin with generous letterspacing, set against dark leather or linen. ⚠️

## Layout & spacing
- **8px base rhythm** for padding inside controls; 10–15px gutters in grouped table views. ⚠️
- **Radii:** small controls 6–8px; grouped tables and panels 8–10px; app icons and hero buttons 10–12px with a heavier gloss. 🟡
- **Borders:** raised surfaces get `border: 1px solid rgba(0,0,0,.35)` + `inset 0 1px 0 rgba(255,255,255,.5)` (top highlight). Recessed surfaces (text fields, slider tracks) invert it: `inset 0 2px 4px rgba(0,0,0,.35)` with a faint bottom highlight. 🟡
- **Shadows:** soft and dark — `0 1px 3px rgba(0,0,0,.5)` on floating panels; long soft drop under shelves. ⚠️
- **Stitching:** `2px dashed var(--stitch)` set ~6px inside the leather edge; the two thread rows on either side of a seam are the iOS 6 Calendar signature. 🟡

## Components
Copy-pasteable HTML/CSS. All textures are pure CSS gradients (no image assets — the era shipped PNGs; these are faithful approximations).

### 1. Gray linen background (folders / Notification Center)
```html
<div class="linen">…content…</div>
```
```css
.linen {
  background-color: #c9cbcd;
  background-image:
    repeating-linear-gradient(0deg, rgba(255,255,255,.06) 0 1px, transparent 1px 3px),
    repeating-linear-gradient(90deg, rgba(0,0,0,.05) 0 1px, transparent 1px 3px),
    linear-gradient(#d4d6d8, #c2c4c6);
}
```

### 2. Stitched leather panel (Calendar / Reminders chrome)
```html
<section class="leather">
  <div class="leather-inner">…content…</div>
</section>
```
```css
.leather {
  background:
    radial-gradient(120% 90% at 50% 0%, rgba(255,255,255,.08), transparent 60%),
    repeating-linear-gradient(45deg, rgba(0,0,0,.04) 0 2px, transparent 2px 4px),
    linear-gradient(#54402a, #3a2b1c);
  border: 1px solid rgba(0,0,0,.5);
  box-shadow: inset 0 1px 0 rgba(255,255,255,.15), 0 2px 6px rgba(0,0,0,.45);
  padding: 14px;
}
.leather-inner {
  border: 2px dashed #d9c69a;   /* the stitch */
  border-radius: 4px;
  padding: 18px;
}
```

### 3. Glossy blue button (App Store / alert default)
```html
<button class="gel-btn">Buy Now</button>
```
```css
.gel-btn {
  font: bold 16px "Helvetica Neue", Helvetica, Arial, sans-serif;
  color: #fff;
  text-shadow: 0 -1px 0 rgba(0,0,0,.5);            /* embossed */
  padding: 10px 28px;
  border: 1px solid #1e3f73;
  border-radius: 8px;
  background: linear-gradient(#8fb0dd 0%, #5b8ac4 48%, #3c6dae 52%, #4d7ab8 100%);
  box-shadow: inset 0 1px 0 rgba(255,255,255,.55), 0 1px 3px rgba(0,0,0,.4);
  cursor: pointer;
}
.gel-btn::before {                                /* the gel gloss */
  content: ""; display: block; height: 46%;
  background: linear-gradient(rgba(255,255,255,.45), rgba(255,255,255,.05));
  border-radius: 8px 8px 40px 40px / 8px 8px 12px 12px;
  margin: -9px -27px 0;                          /* sits on the button's top half */
}
.gel-btn:active {
  background: linear-gradient(#3c6dae, #2c5288);
  box-shadow: inset 0 2px 5px rgba(0,0,0,.4);
}
```

### 4. iOS 6 toggle switch
Pure-CSS switch in the style of Lea Verou's 2013 iOS 6 recreation — silver knob, sliding ON/OFF track:
```html
<label class="ios6-switch">
  <input type="checkbox" checked>
  <span class="track"><span class="labels"><span>ON</span><span>OFF</span></span><span class="knob"></span></span>
</label>
```
```css
.ios6-switch input { display: none; }
.ios6-switch .track {
  display: inline-block; position: relative; width: 94px; height: 27px;
  border-radius: 14px; border: 1px solid #6d6d6d; overflow: hidden;
  background: linear-gradient(#8a8a8a, #b5b5b5);
  box-shadow: inset 0 2px 5px rgba(0,0,0,.45), 0 1px 0 rgba(255,255,255,.6);
  cursor: pointer;
}
.ios6-switch .labels { position: absolute; inset: 0; display: flex;
  transition: transform .25s ease; }
.ios6-switch .labels span { flex: 0 0 94px; line-height: 27px; text-align: center;
  font: bold 13px "Helvetica Neue", Helvetica, Arial, sans-serif; }
.ios6-switch .labels span:first-child { color: #fff; text-shadow: 0 -1px 0 rgba(0,0,0,.5);
  background: linear-gradient(#5b8ac4, #2f5fa0); }  /* ON = blue */
.ios6-switch .labels span:last-child { color: #7a7a7a; text-shadow: 0 1px 0 rgba(255,255,255,.7); }
.ios6-switch input:not(:checked) + .track .labels { transform: translateX(-94px); }
.ios6-switch .knob {
  position: absolute; top: -1px; left: 0; width: 44px; height: 27px; border-radius: 13px;
  border: 1px solid #7a7a7a;
  background: linear-gradient(#ffffff 0%, #e8e8e8 45%, #cfcfcf 55%, #f4f4f4 100%);
  box-shadow: 0 1px 3px rgba(0,0,0,.5), inset 0 1px 0 #fff;
  transition: left .25s ease;
}
.ios6-switch input:not(:checked) + .track .knob { left: 48px; }
```

### 5. Glossy segmented control
```html
<div class="seg" role="tablist">
  <button class="on" role="tab">Day</button><button role="tab">Week</button><button role="tab">Month</button>
</div>
```
```css
.seg { display: inline-flex; border: 1px solid #1e3f73; border-radius: 7px; overflow: hidden;
  box-shadow: inset 0 1px 0 rgba(255,255,255,.4), 0 1px 2px rgba(0,0,0,.3); }
.seg button {
  font: bold 13px "Helvetica Neue", Helvetica, Arial, sans-serif; color: #fff;
  text-shadow: 0 -1px 0 rgba(0,0,0,.5); padding: 7px 20px; border: 0;
  border-right: 1px solid rgba(0,0,0,.35);
  background: linear-gradient(#7d9fd2 0%, #527cb8 50%, #3f68a8 50%, #4d7ab8 100%);
  cursor: pointer;
}
.seg button:last-child { border-right: 0; }
.seg button.on { background: linear-gradient(#9db9e2 0%, #6f96cc 50%, #5780bd 50%, #6b90c8 100%);
  box-shadow: inset 0 2px 6px rgba(0,20,60,.55); }
```

### 6. Embossed nav bar with back button
```html
<header class="navbar"><button class="back">Apps</button><h1>Inkwell</h1></header>
```
```css
.navbar {
  display: flex; align-items: center; gap: 12px; padding: 10px 12px;
  background: linear-gradient(#8fb0dd, #4d7ab8);
  border-bottom: 1px solid #1e3f73;
  box-shadow: inset 0 1px 0 rgba(255,255,255,.5);
}
.navbar h1 { margin: 0; font: bold 19px "Helvetica Neue", Helvetica, Arial, sans-serif;
  color: #fff; text-shadow: 0 -1px 1px rgba(0,0,0,.55); }
.back {
  font: bold 13px "Helvetica Neue", Helvetica, Arial, sans-serif; color: #fff;
  text-shadow: 0 -1px 0 rgba(0,0,0,.5); padding: 6px 12px 6px 20px;
  border: 1px solid #1e3f73; border-radius: 5px; cursor: pointer;
  background: linear-gradient(#7d9fd2, #3f68a8);
  clip-path: polygon(12px 0, 100% 0, 100% 100%, 12px 100%, 0 50%); /* chevron point */
  box-shadow: inset 0 1px 0 rgba(255,255,255,.45);
}
```

### 7. Yellow ruled notepad card (Notes)
```html
<article class="notepad"><h3>Shopping list</h3><p>Oat milk<br>AA batteries<br>Stamps</p></article>
```
```css
.notepad {
  font-family: "Marker Felt", "Comic Sans MS", cursive; color: #3a3226;
  background:
    linear-gradient(90deg, transparent 0 34px, #e5a3a3 34px 36px, transparent 36px),
    repeating-linear-gradient(#fdf6c8 0 26px, #a9c6df 26px 27px);
  border: 1px solid #d8cf9e; border-radius: 2px;
  box-shadow: 0 2px 5px rgba(0,0,0,.25), inset 0 1px 0 #fff;
  padding: 8px 14px 14px 48px; line-height: 27px;
}
```

### 8. Brushed-metal slider
```html
<div class="metal-slider"><div class="fill"></div><div class="knob"></div></div>
```
```css
.metal-slider { position: relative; height: 9px; border-radius: 5px;
  background: repeating-linear-gradient(90deg, #b9bec3 0 2px, #a9aeb4 2px 3px);
  border: 1px solid #6f747a; box-shadow: inset 0 2px 4px rgba(0,0,0,.5), 0 1px 0 rgba(255,255,255,.5); }
.metal-slider .fill { position: absolute; inset: 0 auto 0 0; width: 40%; border-radius: 5px;
  background: linear-gradient(#7d9fd2, #3f68a8); }
.metal-slider .knob { position: absolute; top: -9px; left: 40%; width: 26px; height: 26px;
  margin-left: -13px; border-radius: 50%; border: 1px solid #6f747a;
  background: radial-gradient(circle at 35% 30%, #ffffff, #d9dde1 45%, #a9aeb4 100%);
  box-shadow: 0 2px 4px rgba(0,0,0,.45), inset 0 1px 0 #fff; }
```

### 9. Wooden bookshelf row (iBooks / Newsstand)
```html
<div class="shelf"><div class="book">…</div><div class="book">…</div><div class="ledge"></div></div>
```
```css
.shelf { position: relative; padding: 18px 18px 0;
  background:
    repeating-linear-gradient(93deg, rgba(0,0,0,.12) 0 3px, transparent 3px 9px),
    repeating-linear-gradient(88deg, rgba(255,255,255,.05) 0 2px, transparent 2px 14px),
    linear-gradient(#7d5732, #5d3f22);
  border: 1px solid #3a2812; border-radius: 4px;
  box-shadow: inset 0 1px 0 rgba(255,255,255,.2), 0 2px 5px rgba(0,0,0,.4);
  display: flex; gap: 14px; align-items: flex-end; }
.shelf .book { width: 84px; height: 118px; border-radius: 2px 6px 6px 2px;
  border-left: 4px solid rgba(0,0,0,.3);
  box-shadow: 2px 3px 6px rgba(0,0,0,.5), inset 0 1px 0 rgba(255,255,255,.3); }
.shelf .ledge { position: absolute; left: 0; right: 0; bottom: 0; height: 12px;
  background: linear-gradient(#8a6236, #4e3319);
  border-top: 1px solid rgba(255,255,255,.25);
  box-shadow: 0 3px 5px rgba(0,0,0,.5); }
```

## Motion
The era has almost no motion language of its own — motion served the metaphor: page-curl transitions (iBooks, Maps), flip transitions for "utility" backs (Weather, Stocks), 0.3–0.5s ease-out push/pop slides between screens. Keep animation short, ease-out, and literal; no springs, no parallax, no bounce. One line is enough: **if it doesn't curl, flip, or slide, it doesn't move.**

## Do / Don't
- ✅ Do put a 1px top inner highlight on every raised surface (`inset 0 1px 0 rgba(255,255,255,.5)`). ❌ Don't use a two-stop gradient with no highlight — it reads as flat, not machined.
- ✅ Do emboss type on dark (light fill, dark shadow below-text) and engrave it on light (dark fill, white shadow below). ❌ Don't set pure white text on linen with no shadow — it floats instead of sitting in the material.
- ✅ Do draw stitches as `2px dashed` thread rows, ~6px inside the leather edge, always in pairs flanking a seam. ❌ Don't use dotted borders or a single centered dashed line and call it stitching.
- ✅ Do reserve gloss for pressable things: buttons, switches, segmented controls, icons. ❌ Don't gloss body text, paper, or leather backgrounds — gloss means "touch me".
- ✅ Do match texture lighting: highlights top, shadows bottom, consistent across every material on the page. ❌ Don't mix a top-lit button with a bottom-lit panel.
- ✅ Do use Marker Felt only inside the yellow notepad context. ❌ Don't set UI chrome or headlines in Marker Felt — in iOS 6 it lived in exactly one app.
- ✅ Do give the status-bar-era page a device frame cue (status bar, home indicator era cues) if you're recreating an app screen. ❌ Don't put a 2012 UI inside a modern notched-phone frame — the metaphors clash.

## Copy voice
2012-era Apple voice: warm, a little magical, plain-spoken, fond of superlatives and "just works" confidence. Short sentences. Features as small miracles, not specs.
- "The most beautiful way to keep a journal on iPad. Ever."
- "Your notes, torn straight from a yellow legal pad — minus the paper cuts."
- "Stitched, bound, and buffed to a shine. It just feels right in your hands."

## Sources
- AppleInsider, "What Apple learned from skeuomorphism and why it still matters" (2022): iOS 6 as the skeuomorphism peak; Forstall as chief proponent; Ive's 2013 USA Today quote on the liberty of not referencing the physical world.
- AppleInsider / NYT via AppleInsider (2012): Ive expected to replace textures with "clean edges, flat surfaces"; Forstall's "Corinthian leather" in Find My Friends and Calendar.
- Cult of Mac (2012), "8 Tacky Design Crimes That Jonathan Ive Should Set Right In iOS 7": the canonical inventory of iOS 6's leather stitching, tan patent-leather Calendar, green felt Game Center.
- iMore, "iOS 6: A fresh coat of paint": material-by-material survey — wood (iBooks/Newsstand/iTunes U), leather (Find My Friends, Calendar, Reminders), silver (default apps), linen.
- Lea Verou (2013), "iOS 6 switch style checkboxes with pure CSS": the reference pure-CSS recreation of the iOS 6 toggle (sliding ON/OFF track, silver knob).
- Product Hunt, "Legacy iOS UI Kit" (2024): 153 recreated iOS 6 screens and 12 material textures, confirming the material set (linen, leather, felt, wood, metal) as the era's vocabulary.
