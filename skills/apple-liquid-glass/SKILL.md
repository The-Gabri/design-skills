---
name: apple-liquid-glass
description: Apple Human Interface Guidelines in the Liquid Glass era (iOS 26+): the two-layer model (functional vs. content), material rules, the SwiftUI glassEffect API, semantic colors, SF typography, components, apple.com web style, and spring motion. Use when designing app screens, websites, or mockups with the real current Apple look.
---

# Apple Design — Liquid Glass Era (iOS 26+)

## Verification legend
- ✅ = direct quote or rule from the HIG / official Apple docs, confirmed in ≥2 independent sources.
- 🟡 = consistently documented in ≥3 independent sources; no verbatim Apple quote at hand.
- ⚠️ = community approximation (useful, but not dogma).

## Purpose
Produce designs (app screens, websites, mockups) in the real current Apple visual language: iOS/iPadOS 26+, macOS Tahoe 26+, unified under **Liquid Glass**. The core mental model is the **two-layer model**: a content layer (standard materials) and a functional layer (Liquid Glass floating above it).

## Workflow
1. **Platform and layer.** Every element is *content* (what the user consumes) or *functional* (navigation/controls floating above). This decision governs everything else. ✅
2. **Materials.** Content → standard materials or flat fills. Functional → Liquid Glass. ✅
3. **System first.** With the iOS 26 SDK, `TabView`, `NavigationStack`, toolbars, sheets, and `.glass` buttons adopt the material on their own; don't rewrite backgrounds/blurs that fight the system. 🟡
4. **Tokens, not bare values.** Text styles, semantic colors, 8pt grid, concentric radii → `references/system/tokens.md`. ✅
5. **Spring motion.** Default damping 1.0; bounce only after gesture momentum; every animation interruptible → `references/system/motion.md`. 🟡
6. **Web:** `backdrop-filter` imitates the look, **is not** the real material → `references/materials/glass-css-web.md` and `references/web/apple-web-style.md`. ⚠️
7. **Validate** against the Operating Rules and both appearances + Reduce Transparency.

## The two-layer model (the 80% of this skill)
Apple defines exactly two layers in every iOS 26+ interface:

| Layer | What lives there | Material |
|---|---|---|
| **Content** | The document, feed, photo, list, map, or media the person consumes | Standard materials only (`.ultraThinMaterial` / `.thin` / `.regular` / `.thick`) or flat fills. **Never Liquid Glass.** ✅ |
| **Functional** | Navigation and controls floating over the content: tab bars, sidebars, toolbars, floating buttons, sheets, alerts, popovers, Dock | **Liquid Glass** ✅ |

Key HIG quotes (verbatim):
- ✅ "Liquid Glass forms a distinct functional layer for controls and navigation elements — like tab bars and sidebars — that floats above the content layer."
- ✅ **"Don't use Liquid Glass in the content layer."** Exception: a control in the content with a transient interactive element (a slider, a toggle) takes a glass appearance *while the person manipulates it*, to signal live interactivity.
- ✅ "Use Liquid Glass effects sparingly… Limit these effects to the most important functional elements in your app."
- Content extends edge-to-edge and *underneath* the floating controls; use the system's **scroll edge effect** instead of opaque rectangles behind bars. ✅
- 🟡 Never stack glass on glass: glass cannot sample other glass (this is why `GlassEffectContainer` exists); one floating level only.
- 🟡 What goes *on top of* the glass (icons, labels) takes no glass: solid fills/vibrancy, so it reads as one thin fused layer, not a second sheet of glass.

### Liquid Glass variants ✅
- **regular** (default): blurs and adjusts background luminance to protect legibility. "Most system components use this variant." For components with lots of text (alerts, sidebars, popovers) or backgrounds that threaten legibility.
- **clear**: highly translucent, keeps the background prominent. **Only over visually rich backgrounds** (photos, video). If the underlying content is bright, add **a 35%-opacity dark dimming layer**; not needed if the content is dark or AVKit playback controls already provide their own.

## Principles
Apple's eight design principles (HIG, re-introduced at WWDC26): **Purpose, Agency, Responsibility, Familiarity, Flexibility, Simplicity, Craft, Delight**. In practice:
- **Purpose:** the "razor test" — if removing an element loses nothing, remove it. One primary task per screen.
- **Agency:** the user stays in control; direct manipulation, easy undo, confirm only what's truly destructive and irreversible.
- **Responsibility:** privacy, permissions, security and transparency as a design principle, not a legal note.
- **Familiarity:** system components first (tabs, sheets, alerts, menus); what looks the same must behave the same. Never re-invent a tab bar or sheet with different behavior.
- **Flexibility:** accessibility from the first sketch (VoiceOver, Dynamic Type, Reduce Motion); design by size classes, not device models.
- **Simplicity:** "Simplicity isn't minimalism" — remove the unnecessary so the central purpose shines. One primary action per screen; progressive disclosure.
- **Craft:** nothing is random — every spacing, timing, alignment and word is deliberate. In the Liquid Glass era, opaque bars or pre-2025-style icons are a craft failure, not a preference.
- **Delight:** the natural result of getting the other seven right — never decoration at the expense of the task.
→ Full detail: `references/foundations/principles.md`.

## Color
- **Semantic colors, always.** `label`, `secondaryLabel`, `systemBackground`, `separator`, `systemBlue`… In native code use the **names**, never hex: Apple may change values per release. ✅
- **Real Dark Mode.** Every custom color is a set with light and dark variants. No "light-only" design. ✅
- **Contrast:** 4.5:1 for normal text, 3:1 for large text (WCAG AA) — and it must survive **over translucent materials**. ✅
- **One tint per screen.** Blue = primary action / default tint; red = destructive / error; green = success. Never one color with two meanings; never color as the only information channel. ✅
- **Glass has no color of its own:** it picks up what's behind it. Tint only what needs emphasis. Put color in the **content layer**, so floating glass controls pick up your brand dynamically. ✅
- Since 26.1 the user can choose the system look (**Clear** = more transparent, **Tinted** = more opaque) — it affects third-party apps: your design must survive both. 🟡
→ `references/foundations/color.md`, `references/system/tokens.md`.

## Typography
- **The system family:** **SF Pro** for UI (optical variants **Text** ≤19pt and **Display** ≥20pt; the variable font handles it natively), **SF Compact** (watch), **SF Mono** (code/data), **New York** (editorial serif). ✅
- **Semantic text styles, never fixed sizes.** `.largeTitle` (34) → `.caption2` (11). Body 17pt. Minimum 11pt for system text. ✅
- **Dynamic Type is non-negotiable:** layouts must survive xSmall → AX5; custom fonts must scale too (`relativeTo:`). ✅
- Hierarchy through **weight and color** before extreme size jumps; max 3–4 styles per screen. Left-aligned paragraphs, never justified. Line length 35–50 characters on mobile; ~672pt max measure on iPad. ✅
- Web: system font stack (`-apple-system, BlinkMacSystemFont, "SF Pro Text", …`); fluid display type with `clamp()`; hero semibold (not black) with tight negative tracking. Do **not** self-host SF Pro (Apple license: only on Apple platforms). 🟡
→ `references/foundations/typography.md`, `references/system/tokens.md`.

## Layout & spacing
- **8pt grid** (4pt fine step). Closed vocabulary: **4, 8, 12, 16, 20, 24, 32** (48 for hero breathing room). Horizontal margins: 16pt iPhone, 20pt iPad. ✅/🟡
- **Minimum touch target 44×44pt**; ≥8pt separation between adjacent tappable elements. ✅
- **Always respect safe areas** (notch, Dynamic Island, home indicator). Interactive content never sits under hardware; backgrounds may extend. In web: `viewport-fit=cover` + `env(safe-area-inset-*)`. ✅
- **Radii:** 8 / 12 / 16; capsule for prominent controls; concentric radii (inner = outer − padding); `.rect(cornerRadius: .containerConcentric)` in iOS 26+. Squircle `.continuous` on large surfaces. 🟡
- **Adaptability by size classes, never device checks** (`horizontalSizeClass`); iOS 26 scroll edge effects replace opaque bar backgrounds. ✅/🟡
→ `references/system/layout.md`, `references/system/tokens.md`.

## Components
5–10 signature components with copy-pasteable code (full versions in references/):

### 1. Navigation — floating tab bar + search tab ✅/🟡
```swift
import SwiftUI

// WHEN: an iPhone app's primary navigation with 2–5 same-level sections.
// iOS 26 floats the tab bar as a Liquid Glass capsule on its own — no glass needed.
struct MainTabs: View {
    var body: some View {
        TabView {
            Tab("Home", systemImage: "house") { NavigationStack { HomeView() } }
            Tab("Library", systemImage: "books.vertical") { NavigationStack { LibraryView() } }
            Tab("Settings", systemImage: "gear") { NavigationStack { SettingsView() } }
            Tab(role: .search) { NavigationStack { SearchView().searchable(text: $q) } }
        }
        .tabBarMinimizeBehavior(.onScrollDown)  // shrinks to a pill, never hides
        .tabViewStyle(.sidebarAdaptable)        // iPad: becomes a sidebar
    }
}
```
Rules: tab bar is for **navigation, never actions**; max 5 tabs on iPhone; icon + label always; each tab keeps its own navigation state; search tab has role `.search` at the trailing edge; swipe-to-go-back is sacred. ✅

### 2. Custom floating toolbar — `.glassEffect(.regular)` ✅
```swift
import SwiftUI

// WHEN: custom floating toolbar (functional layer). .glassEffect goes LAST,
// after padding/font/color — sampling uses the view's final shape.
struct FloatingToolbar: View {
    var body: some View {
        HStack(spacing: 20) {
            Button("Like", systemImage: "heart") { }
            Button("Share", systemImage: "square.and.arrow.up") { }
        }
        .padding(.horizontal, 24).padding(.vertical, 14)
        .labelStyle(.iconOnly)
        .glassEffect(.regular, in: .capsule)
    }
}
```
Web approximation (⚠️ honest: not the real material):
```css
/* ⚠️ visual approximation only — backdrop-filter is not Liquid Glass. */
.floating-bar {
  border-radius: 999px;
  background: rgba(255, 255, 255, 0.55);
  -webkit-backdrop-filter: blur(20px) saturate(180%);
  backdrop-filter: blur(20px) saturate(180%);
  border: 1px solid rgba(255, 255, 255, 0.5);
  box-shadow: 0 8px 32px rgba(0, 0, 0, 0.12);
}
@supports not ((backdrop-filter: blur(1px)) or (-webkit-backdrop-filter: blur(1px))) {
  .floating-bar { background: var(--bg); } /* solid fallback: never illegible glass */
}
@media (prefers-reduced-transparency: reduce) {
  .floating-bar { background: var(--bg); backdrop-filter: none; }
}
```

### 3. Buttons — one prominent per screen ✅/🟡
```swift
Button("Publish") { }
    .buttonStyle(.glassProminent)  // primary: filled, capsule
    .tint(.accentColor)
    .controlSize(.large)

Button("Save draft") { }
    .buttonStyle(.glass)           // secondary: neutral glass

Button("Discard") { }
    .buttonStyle(.borderless)      // tertiary: plain text
    .foregroundStyle(.secondary)
```
Rules: one `.glassProminent` per screen; labels are short Title Case verbs naming the **result** ("Save", not "OK"); destructive uses `role: .destructive` (red), never the primary role; labels inherit the **meaning** of the tint. ✅

### 4. Transient glass — sliders and toggles ✅
```swift
import SwiftUI
// WHEN: iOS 26 controls adopt glass by themselves during interaction — don't add your own.
Toggle("Notifications", isOn: $notifications).toggleStyle(.switch)
Slider(value: $speed, in: 0.5...2.0, step: 0.25) {
    Text("Speed")
} ticks: {
    SliderTick(value: 0.5); SliderTick(value: 1.0)
    SliderTick(value: 1.5); SliderTick(value: 2.0)
}
.sliderNeutralValue(1.0)  // ✅ WWDC25 session 323
```
The knob/scrubber becomes Liquid Glass **only while being manipulated** — the single sanctioned exception to "no glass in the content layer." ✅

### 5. Context menu — system menus, never handmade ✅
```swift
Text("Document.pdf").padding()
    .contextMenu {   // ✅ system modifier
        Button { } label: { Label("Edit", systemImage: "pencil") }
        Divider()
        Button(role: .destructive) { } label: { Label("Delete", systemImage: "trash") }
    }
```
Destructive always last, after a `Divider()`, with `role: .destructive`. In iOS 26 the menu morphs out of its source control. ✅

### 6. Sheets — detents, grabber, Done+Cancel ✅
```swift
.sheet(isPresented: $show) {
    NavigationStack {
        Form { /* … */ }
            .navigationTitle("New note")
            .toolbar {
                ToolbarItem(placement: .cancellationAction) { Button("Cancel") { } }
                ToolbarItem(placement: .confirmationAction) { Button("Save") { } }
            }
    }
    .presentationDetents([.medium, .large])
    .presentationDragIndicator(.visible)
}
```
One sheet at a time; grabber on resizable sheets (it's also the VoiceOver hint); if there is Done, there is always Cancel; full-screen only for immersive content (camera, video, photos) or complex flows. ✅

### 7. Alert vs. confirmationDialog — pick the lightest ✅
```swift
// WHEN: critical error needing acknowledgment → alert (1–2 buttons, concrete message)
.alert("Couldn't save", isPresented: $showError) {
    Button("Retry") { save() }
    Button("Discard", role: .cancel) { }
} message: {
    Text("Check your connection and try again.") // never "An error occurred"
}

// WHEN: the user tapped something risky and must choose → confirmationDialog
.confirmationDialog("Delete this photo?", isPresented: $confirm,
                    titleVisibility: .visible) {
    Button("Delete photo", role: .destructive) { }
    Button("Cancel", role: .cancel) { }
}
```
Alert = "something needs you **now** (error/notice)"; confirmationDialog = "what do you want to do?" — a list of actions. ✅

### 8. Segmented control / pickers ✅
```swift
Picker("Period", selection: $period) {
    Text("Day").tag("Day"); Text("Week").tag("Week"); Text("Month").tag("Month")
}
.pickerStyle(.segmented)   // 2–5 mutually exclusive views; never for actions
```

### 9. SF Symbols — 9 weights × 3 scales ✅
```swift
Label("Favorites", systemImage: "heart.fill").font(.headline) // symbol inherits weight
// Rule: outline in toolbars, filled in tab bars (active = filled + label). ✅
// One consistent imageScale per container; never repurpose a known symbol's meaning. ✅
```

### 10. Widgets & Live Activities ✅
```swift
// Widgets are glanceable, not mini-apps; no realtime (system rations refreshes);
// touching a widget deep-links to the relevant content. ✅
.containerBackground(for: .widget) { Color(.systemBackground) }

// Live Activities: user-initiated events with live progress (deliveries, sports,
// timers); max 8 h active; attributes + state ≤ 4 KB; start only in foreground. ✅
```

## Motion
- **Spring by default:** `dampingFraction 1.0` (critically damped, no overshoot) for any state change from a tap without momentum; bounce (~0.8) **only** when the gesture contributed momentum (fling to dismiss). ⚠️/🟡 (HIG publishes no canonical spring constants for third parties — treat numbers as perceptual heuristics.)
- **The golden rule:** every animation interruptible and re-directable at any moment, from the on-screen value and velocity; never block input. Respond to pointerdown, not release; direct manipulation is 1:1; limits with rubber-banding, never hard stops. 🟡
- **Hero transitions** via `matchedGeometryEffect(id:in:)` — same id + same `@Namespace`, animated state change. 🟡
- **Respect reduced motion:** slides → ~100ms crossfade; parallax → static; autoplay → still frame with on-demand play; never eliminate the message, just substitute the motion. ✅
- CSS mapping (⚠️ imitation, not spec): `--ease-out: cubic-bezier(0.23, 1, 0.32, 1)` for enter/exit; `--ease-drawer: cubic-bezier(0.32, 0.72, 0, 1)` for sheets; never `ease-in` for UI; mirror curves for reversible transitions.
→ `references/system/motion.md`.

## Do / Don't
1. **Glass in the functional layer only.** ✅ — DO: tab bars, floating toolbars, floating buttons, sheets, alerts, popovers. DON'T: list cards, app backgrounds, scroll views, paragraphs with glass (the content layer uses standard materials or flat fills). Exception: a slider/toggle knob becomes glass only while being manipulated.
2. **One floating level.** ✅/🟡 — DO: a single glass surface per zone; group neighbors in one `GlassEffectContainer`. DON'T: glass stacked on glass — glass can't sample glass.
3. **One accent per screen.** ✅ — DO: one `.tint(.blue)` high in the hierarchy; blue = primary, red = destructive, green = success. DON'T: blue buttons, green links, purple toggles and orange badges in the same view.
4. **System styles before customs.** 🟡 — DO: `Toggle`, `Slider`, `Picker`, `Menu`, `.contextMenu`, `.glassProminent` — they adopt the iOS 26 look themselves. DON'T: custom blur+shadow stacks to imitate Liquid Glass in native code.
5. **Buttons: one prominent, capsule, content-hugging.** 🟡 — DO: `.glassProminent` for the primary, `.glass` for secondary, `.borderless` for tertiary. DON'T: full-width glass bars or two filled primaries side by side.
6. **Sheets: one at a time, with an obvious exit.** ✅ — DO: `.medium`/`.large` detents, visible grabber, Cancel leading + Done trailing. DON'T: sheet-on-sheet, or blocking alerts for reversible preferences.
7. **Typography by system styles.** ✅ — DO: `.body`/`.headline`… scaling with Dynamic Type for free. DON'T: hardcoded point sizes or shrinking reading text to "make it fit".
8. **Touch targets 44×44pt.** ✅ — DO: real `Button` with 44×44pt hit area + `accessibilityLabel` on icon-only buttons. DON'T: tap gestures on bare icons (~20pt).
9. **Color reinforces, never communicates alone.** ✅ — DO: error = icon ✕ + "Error" text + red. DON'T: a bare red dot meaning "failed".
10. **Never say `backdrop-filter` *is* Liquid Glass.** ⚠️ — DO: present it as a visual approximation with `@supports` fallbacks and `prefers-reduced-transparency` respect. DON'T: ship illegible glass as the only option.
11. **Motion: springs, interruptible, reduced-motion safe.** ✅/🟡 — DO: damping 1.0 default, explicit `withAnimation` around the interaction's mutation, crossfade fallbacks. DON'T: decorative bounce on touch opens, fire-and-forget animations, or ignoring `prefers-reduced-motion`.

## Output contract
When producing a design with this skill, deliver:
1. The layer decision per element (what is functional, what is content).
2. Tokens used: text styles, semantic colors, 8/4pt-multiple spacings, radii.
3. Behavior in **light and dark** mode, and with Reduce Transparency on.
4. Motion spec: what animates, with which spring (damping/response), and what happens with `prefers-reduced-motion`.
5. If web: the "Apple-style" effect CSS with its no-`backdrop-filter` fallback (not the real material — see `references/materials/glass-css-web.md`).

## Sources consulted
- HIG — Materials (official page; verified via verbatim quotes consistent across 4+ independent sources): https://developer.apple.com/design/human-interface-guidelines/materials
- "Adopting Liquid Glass" / "Liquid Glass" (TechnologyOverviews): https://developer.apple.com/documentation/TechnologyOverviews/adopting-liquid-glass
- WWDC25 session 219 "Meet Liquid Glass": https://developer.apple.com/videos/play/wwdc2025/219/
- WWDC18 "Designing Fluid Interfaces" (spring damping/response values, attributed by 6+ sources; no direct quote verified): https://developer.apple.com/videos/play/wwdc2018/803/
- Cross-verified HIG compilations (olzn/skills, gauravrajkagwaniya/native_adaptive_ui, camillescholtz/swmpc, raintree-technology/agent-starter, davie521/claude-skills; Clear/Tinted 26.1 preference via 9to5Mac, MacRumors, AppleInsider).
- See `references/materials/liquid-glass.md` for the full native API with copy-pasteable examples, and the reference index below for everything else.

## Reference index (topic → file)
Each file combines verified rules (✅/🟡/⚠️ legend) with copy-pasteable code and do/don't pairs. 🧪 marks example-focused files.

**foundations/**
- **foundations/principles.md** — the 8 current HIG principles (WWDC26), actionable rules and do/don't per principle.
- **foundations/two-layers.md** — the two-layer model with verbatim Apple quotes, the transient-control exception, SwiftUI + CSS examples.
- **foundations/color.md** — semantic colors, single-meaning tints, light/dark mode, contrast + SwiftUI and CSS examples.
- **foundations/typography.md** — SF Pro/Text/Display/Compact/Mono, New York, text styles, Dynamic Type + SwiftUI and CSS examples.

**materials/**
- **materials/liquid-glass.md** — conceptual rules: regular/clear variants, "Don't use Liquid Glass in the content layer", glass-on-glass, Clear/Tinted 26.1+, Reduce Transparency, scroll edge effect, API anatomy.
- **materials/liquid-glass-examples.md** 🧪 — 13 SwiftUI snippets: `.glassEffect`, `GlassEffectContainer` + morphing, `.buttonStyle(.glass)`, standard materials, fallbacks.
- **materials/glass-css-web.md** — `backdrop-filter` with the explicit warning that it is a visual approximation (not the real material), `@supports` fallbacks, performance.

**components/**
- **components/navigation.md** — tab bar (2–5 destinations, floating in iOS 26, minimize-on-scroll, trailing search), sidebar, NavigationStack, sacred back gesture, toolbars + examples.
- **components/controls.md** — button hierarchy, Toggle/Slider/Stepper/pickers, context menus, 44×44pt targets, forms, empty states + examples.
- **components/presentation.md** — sheets (detents, grabber, Done+Cancel), alert vs confirmationDialog, popovers, full-screen only when immersive + examples.

**system/**
- **system/tokens.md** — 8pt spacing, radii, hex reference colors (web-only), SF Symbols (9 weights × 3 scales) + examples.
- **system/layout.md** — 8pt grid, safe areas, size classes, iPad multitasking, readable width, `safeAreaBar` + SwiftUI and CSS examples.
- **system/motion.md** — springs (damping 1.0 default; the HIG publishes no canonical constants — these are heuristics), interruptibility, `matchedGeometryEffect`, prefers-reduced-motion + examples.
- **system/accessibility.md** — VoiceOver, Dynamic Type, Reduce Motion/Transparency, Increase Contrast, Differentiate Without Color, haptics and sound + examples.
- **system/app-icons.md** — system-applied squircle, 1024×1024 unrounded, one centered glyph, no text, Light/Dark/Tinted/Clear variants + practical guide.

**platforms/**
- **platforms/ios.md** — widgets (limits, deep links), Live Activities (8h, Dynamic Island compact/minimal/expanded), StandBy + examples.
- **platforms/macos.md** — Tahoe: transparent menu bar, tinted/clear icons, sidebars, windows, differences vs. iOS + examples.
- **platforms/watchos.md** — complications, Always-On, SF Compact, Digital Crown, what NOT to do + examples.

**web/**
- **web/apple-web-style.md** — apple.com aesthetics: 80–104px heroes, one idea per scene, CTAs, bento, scroll storytelling without scroll-jacking + examples.
- **web/css-examples.md** 🧪 — copy-pasteable CSS: tokens, `clamp()` hero, scroll-snap, cards, translucent nav (with ⚠️ warning).
