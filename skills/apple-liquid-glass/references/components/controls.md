# Controls

**Verification legend** (applies to each rule and snippet):
- ✅ = direct HIG rule or official Apple documentation, confirmed in ≥2 independent sources.
- 🟡 = consistently documented in ≥3 sources, no verbatim Apple quote at hand.
- ⚠️ = doubtful / single source / disagreeing communities — not dogma.

System controls adopt Liquid Glass on their own when built with the iOS 26 SDK: don't rewrite backgrounds or blurs that fight the system.

Choose the control by **behavior**: switch = instant independent toggle; checkbox (macOS) = selection within a set; segmented = pick one of a few; menu/picker = pick one of many.

---

## Button hierarchy (iOS 26)

- 🟡 **One prominent (filled) button per screen = the primary action.** The rest: bordered (secondary) or plain/borderless (tertiary). Two filled buttons competing side by side flatten the hierarchy and create decision friction: demote one. HIG: *"Reserve the most prominent style for the single most likely or important action."*
- ⚠️ **One source's nuance:** allows "one or two prominent buttons per view, max". Keep the rule of **one** as the norm; two only with clearly distinct roles.
- 🟡 **System styles before customs:** `.plain`, `.gray`, `.tinted`, `.bordered`, `.borderedProminent`. In iOS 26, prominent actions use the glass prominent style: `.glassProminent` for the primary, `.glass` for the secondary, `.borderless` for the tertiary.
- ✅ **Buttons are capsule-shaped by default in iOS 26**, hugging the content. Sizes: `.mini` / `.small` / `.regular` / `.large` / `.extraLarge` (`.extraLarge`, iOS 17+, is the WWDC25 session 323 recommendation for full-screen CTAs).
- 🟡 **Don't stretch a glass button to the screen's full width**: glass is the functional layer floating over content; a full-width glass bar competes visually with the content and breaks the "floating control" reading.
- 🟡 **Glass in buttons ONLY in the navigation layer** (tab bars, floating toolbars): `.glass` for that layer's controls, `.glassProminent` for the primary action. **Don't apply glass to buttons inside content lists or cards**; remove custom backgrounds so the system's material reads well. HIG: *"Don't use Liquid Glass in the content layer."*
- 🟡 **Distinguish the preferred option by STYLE, never by size.**
- 🟡 **In toolbars:** monochrome icons by default, no custom backgrounds/borders — the hierarchy comes from grouping, not decoration. Group by function/frequency; the most-used action within thumb reach.

## Labels, roles, and tints

- 🟡 **The button must look tappable.** Label with a **short Title Case verb naming the result** ("Save", "Send", "Add to cart"), never the mechanism: no generic "OK", "Submit", or "Confirm" when a specific verb exists. Few words so it fits with Dynamic Type and in other languages.
- 🟡 **Destructive actions: `.destructive` role (red) + clear label, never the default button.** HIG: *"Never give the primary role to a destructive action — people press prominent buttons without reading them."* In alerts/dialogs, the destructive action is never the default and is always paired with Cancel.
- 🟡 **Assign roles (`.destructive`, `.cancel`), don't fake them with style**: the system presents them consistently.
- 🟡 **Tint with meaning, not decoration**: `.tint()` only with semantic meaning (accent = primary action; red = destructive; green = success/confirmation). Never color as the only information channel (pair with icon or text). Tinting each button a different color "to tell them apart" confuses: color is a system language with fixed meaning.
- ✅ **Press feedback always**: scale ~0.97 + slight opacity drop, 80–160 ms. Never wait for the animation to finish before executing the action.

## Toggles, sliders, steppers, pickers

- 🟡 **Toggle/switch: an instant binary setting that takes effect immediately.** Never for something requiring confirmation, never requiring "Apply" afterwards. The label describes the enabled state or the controlled setting.
- 🟡 **Slider: continuous ranges where the exact value is secondary.** For values the user must type precisely, text field. With a label and value readout; ticks for discrete steps.
- 🟡 **Stepper: small, precise increments (range ~1–10).** Large ranges → slider or text field.
- 🟡 **Pickers: wheel for dates/times and multi-component values; menu picker (`.menu`) to pick 1 of 5–15 options inline in a form.** Wheel NOT for short simple lists; long scrolling lists → pushed list. Use the platform's picker, not a custom wheel.
- 🟡 **Segmented control: 2–5 mutually exclusive views/filters**, all visible at once. Never for actions or on/off; never for navigation between sections.

## Menus and context menus

- 🟡 **Pull-down menu:** a list of actions/options from a button (often •••). Group related ones, use separators, destructives at the end in destructive style, submenus sparingly (one level).
- 🟡 **Pop-up menu:** picks ONE value from a compact set; shows the current selection. Good on iPadOS/macOS.
- 🟡 **Context menus:** long-press (touch) / right-click (pointer) on a content item → that item's contextual actions, optionally with a preview. **In iOS 26 the menu "morphs" out of its source control (glass).** Keep ≤ ~8 items; destructives at the end with `role: .destructive`. **Don't hide essential actions ONLY here** — a visible path must exist. In list rows: `.swipeActions` for common actions.
- 🟡 **Swipe actions in rows:** leading edge = positive actions (read/pin), trailing edge = negative, the destructive outermost with full-swipe to execute. Always mirrored in the context menu or edit mode.
- ⚠️ **"Max 3 swipe actions per side"** appears in a single source — useful as a practical cap, not an official rule.
- ✅ **Don't hide primary actions in a menu** (menus expose secondary actions).
- ✅ **macOS: every action must also exist in the menu bar** (see `navigation.md`).

## Touch targets and separation

- ✅ **Minimum touch target: 44×44pt on all touch platforms.** HIG quote: *"As a general rule, a button needs a hit region of at least 44x44 pt."* Even if the visible glyph is smaller, enlarge the hit area (`.contentShape`, `minWidth/minHeight`). On visionOS 60×60.
- 🟡 **Minimum 8pt separation between adjacent tappable elements**, to avoid mis-taps — especially near destructive actions. (Nuance from Apple's published guide: ~12pt padding around bezeled elements, ~24pt "around visible edges" for unbezeled ones; design with 8pt as the absolute minimum and more air near dangerous actions.)
- 🟡 **44×44pt is also the minimum list row height** (60pt with subtitle); bar controls: 44pt.

## Text fields and forms

- ✅ **The placeholder is not the label**: visible label + hint as placeholder.
- ✅ **Keyboard type** matching the input (`.emailAddress`, `.phonePad`, `.URL`); `.textContentType` for autofill (email, password, address).
- ✅ **Errors next to the affected field**; preserve text after failed validation; inline validation with clear messages.
- ✅ Secure field for passwords; system date/time pickers.

## Progress and states

- ✅ **Determinate** (bar) when the proportion is known; **indeterminate** (spinner) when it's not.
- ✅ **Show progress for operations > ~1s**; never leave the user guessing. For long waits, context ("Importing 12 of 340…").
- ✅ **Empty states**: never a blank screen — explain what's missing and give a clear next action (`ContentUnavailableView`).
- 🟡 **Skeletons**: show the *shape* of the content while loading; no shimmer under Reduce Motion.
- ✅ **Badges**: only genuinely critical information; low numbers with meaning.
- ✅ **Success feedback**: after silent actions (copy to clipboard), acknowledge: status text, sound, or haptics. **Never haptics as the only channel.**
- ✅ **Links**: for navigation/external resources, not for destructive actions.

---

## SwiftUI examples

### 1. Primary button — `.glassProminent` ✅

**When to use it:** for THE main action of a view (one primary per screen). `.glassProminent` is the most-emphasized style; `.tint()` paints the accent tint. In iOS 26 the system draws it as a Liquid Glass capsule automatically.

```swift
import SwiftUI

struct PrimaryButton: View {
    var body: some View {
        Button("Save changes") {
            // The screen's main action
        }
        .buttonStyle(.glassProminent)
        .tint(.accentColor)          // ✅ .tint(_:) on glass buttons: verified in 3+ sources
        .controlSize(.large)         // ✅ sizes .mini/.small/.regular/.large/.extraLarge
    }
}
```

### 2. Button hierarchy: primary / secondary / tertiary 🟡

**When to use it:** when a screen has several actions with different weight.

```swift
import SwiftUI

// Community convention (consistent in 3+ sources):
//   primary   → .glassProminent + tint (only one per screen)
//   secondary → .glass without tint
//   tertiary  → .borderless (no chrome)
struct ButtonHierarchy: View {
    var body: some View {
        VStack(spacing: 12) {
            Button("Publish") {
                // Main action
            }
            .buttonStyle(.glassProminent)
            .tint(.accentColor)

            Button("Save draft") {
                // Secondary action
            }
            .buttonStyle(.glass)

            Button("Discard") {
                // Tertiary action: plain text, no glass chrome
            }
            .buttonStyle(.borderless)
            .foregroundStyle(.secondary)
        }
    }
}
```

### 3. Configured glass button — `.glass(_:)` with tint ✅

**When to use it:** when the primary needs a different semantic meaning than the default accent (e.g. green = success) or you want the `.clear` variant. The `.glass(_:)` factory takes a `Glass` value; the explicit `GlassButtonStyle(_:)` init only exists in 26.1+ — use the factory.

```swift
import SwiftUI

struct ConfiguredGlassButton: View {
    var body: some View {
        Button("Confirm payment") {
            // Affirmative action
        }
        .buttonStyle(.glass(.regular.tint(.green)))   // ✅ .glass(_:) factory in 26.0
        .controlSize(.large)
    }
}
```

### 4. Extra-large button for a full-screen CTA ✅

**When to use it:** full-screen CTA (onboarding, welcome screen). WWDC25 session 323 recommendation: `.controlSize(.extraLarge)` for prominent action buttons. `.extraLarge` exists since iOS 17.

```swift
import SwiftUI

struct ExtraLargeButton: View {
    var body: some View {
        Button("Get started") {
            // Onboarding action
        }
        .buttonStyle(.glassProminent)
        .tint(.accentColor)
        .controlSize(.extraLarge)   // ✅ WWDC25 session 323
    }
}
```

### 5. Toggle ✅

**When to use it:** binary settings inside forms or settings views. With the iOS 26 SDK the thumb becomes wider (oval) and, WHILE DRAGGING, the knob turns into Liquid Glass (session 323, WWDC25). Don't add `.glassEffect()` on top: the system does it on its own during the interaction.

```swift
import SwiftUI

struct ToggleSetting: View {
    @State private var notifications = true

    var body: some View {
        Toggle("Notifications", isOn: $notifications)
            .toggleStyle(.switch)   // ✅ system style; the thumb is oval in iOS 26
    }
}
```

### 6. Slider with ticks and neutral value ✅

**When to use it:** continuous values in a range (volume, speed, intensity). Since iOS 26 you can draw ticks (`SliderTick`) and define a neutral value (e.g. speed 1x). The scrubber takes a glass appearance while manipulated (session 323, WWDC25).

```swift
import SwiftUI

struct SliderSetting: View {
    @State private var speed = 1.0

    var body: some View {
        Slider(value: $speed, in: 0.5...2.0, step: 0.25) {
            Text("Speed")
        } ticks: {
            SliderTick(value: 0.5)
            SliderTick(value: 1.0)
            SliderTick(value: 1.5)
            SliderTick(value: 2.0)
        }
        .sliderNeutralValue(1.0)    // ✅ WWDC25 session 323 (3+ sources)
    }
}
```

### 7. Stepper ✅

**When to use it:** small discrete values (quantity, retries) where stepping one at a time is the natural interaction. In iOS 26 it adopts the system's renewed look automatically.

```swift
import SwiftUI

struct StepperSetting: View {
    @State private var quantity = 1

    var body: some View {
        Stepper("Quantity: \(quantity)", value: $quantity, in: 1...10)
        // Explicit-closure form (Apple-documented signature):
        // Stepper("Quantity") { quantity += 1 } onDecrement: { quantity -= 1 }
    }
}
```

### 8. Segmented picker ✅

**When to use it:** choosing between 2–4 mutually exclusive options all visible at once (day/week/month). In iOS 26 the selected segment is more rounded, without thin separators, and turns to glass when interacting (session 323, WWDC25).

```swift
import SwiftUI

struct PeriodSelector: View {
    @State private var period = "Day"

    var body: some View {
        Picker("Period", selection: $period) {
            Text("Day").tag("Day")
            Text("Week").tag("Week")
            Text("Month").tag("Month")
        }
        .pickerStyle(.segmented)   // ✅ system style
    }
}
```

### 9. Menu-style picker (popover) ✅

**When to use it:** choosing one option among many (more than 4–5) without taking space. The `.menu` picker presents the system's glass popover automatically.

```swift
import SwiftUI

struct LanguageSelector: View {
    @State private var language = "English"

    var body: some View {
        Picker("Language", selection: $language) {
            Text("English").tag("English")
            Text("Spanish").tag("Spanish")
            Text("French").tag("French")
            Text("German").tag("German")
        }
        .pickerStyle(.menu)   // ✅ system style: automatic glass popover
    }
}
```

### 10. Pull-down menu from a button ✅

**When to use it:** a button offering several related actions (sort, filters, share options). Tap shows the menu; the system morphs the button into the menu automatically (🟡: "buttons fluidly morph into menus", 1 source with Apple text).

```swift
import SwiftUI

struct ButtonWithMenu: View {
    var body: some View {
        Menu {
            Button("Sort by name", systemImage: "textformat.abc") { }
            Button("Sort by date", systemImage: "calendar") { }
            Divider()
            Button("Delete", systemImage: "trash", role: .destructive) { }
        } label: {
            Label("Options", systemImage: "ellipsis.circle")
        }
        .buttonStyle(.glass)   // ✅ the menu's label can carry the glass style
        // HIG note: the destructive action goes last, separated by Divider.
    }
}
```

### 11. Menu with primary action (tap vs. long-press) 🟡

**When to use it:** when the button already has an obvious action (tap) and the rest are secondary: tap runs the primary action, long-press opens the menu. Available since iOS 16.

```swift
import SwiftUI

struct PrimaryActionMenu: View {
    var body: some View {
        Menu(primaryAction: {
            // Primary action: runs on a simple tap
        }) {
            Button("Rename", systemImage: "pencil") { }
            Button("Duplicate", systemImage: "doc.on.doc") { }
            Divider()
            Button("Delete", systemImage: "trash", role: .destructive) { }
        } label: {
            Label("Share", systemImage: "square.and.arrow.up")
        }
        .buttonStyle(.glass)
    }
}
```

### 12. Context menu (long-press) ✅

**When to use it:** secondary actions on a content element (a row, a photo) without adding visible buttons. Appears on long-press / right-click. The context menu is the system's: don't reimplement it.

```swift
import SwiftUI

struct RowWithContextMenu: View {
    var body: some View {
        Text("Document.pdf")
            .padding()
            .contextMenu {   // ✅ system modifier
                Button {
                    // Edit
                } label: {
                    Label("Edit", systemImage: "pencil")
                }
                Button {
                    // Share
                } label: {
                    Label("Share", systemImage: "square.and.arrow.up")
                }
                Divider()
                Button(role: .destructive) {
                    // Delete
                } label: {
                    Label("Delete", systemImage: "trash")
                }
            }
        // Rule: destructive last, after Divider, with role: .destructive.
    }
}
```

### 13. Correct touch target: 44×44pt minimum ✅

**When to use it:** icon-only buttons. Even if the symbol measures ~20pt, the touch area must be at least 44×44pt (HIG rule). Using a real `Button` also gives the accessibility trait for free (VoiceOver announces "button") and the system's pressed state.

```swift
import SwiftUI

struct CorrectIconButton: View {
    var body: some View {
        Button {
            // Action
        } label: {
            Image(systemName: "star.fill")
                .frame(width: 44, height: 44)   // ✅ real 44×44pt touch area
                .contentShape(Rectangle())      // ✅ the whole box responds to touch
        }
        .accessibilityLabel("Save to favorites")
    }
}
```

### 14. ❌ Common mistake: gesture glued to the icon (insufficient touch area)

**DON'T DO THIS:** `.onTapGesture` over an `Image` without an explicit size leaves a touch area the size of the symbol (~20×20pt), far below the HIG's 44×44pt minimum. You also lose the VoiceOver "button" trait and the system's pressed state. Use snippet 13 instead.

```swift
import SwiftUI

struct WrongIconButton: View {
    var body: some View {
        Image(systemName: "star.fill")
            .foregroundStyle(.yellow)
            .onTapGesture {
                // ❌ ~20×20pt: impossible to tap precisely
            }
    }
}
```

---

## Do / don't pairs

**A. Hierarchy: a single primary**
- ✅ **DO:** one `.glassProminent` (with accent `.tint()`) per screen or group; secondaries with `.glass` without tint; tertiaries with `.borderless`. (Snippets 1–2.)
- ❌ **DON'T:** two or more prominent buttons together, or tinting the secondary `.glass` "to make it stand out". Prominence marks *the* preferred action; if everything is prominent, nothing is, and each extra tint competes with the accent (the "one accent per screen" rule).

**B. System first: don't rewrite the controls**
- ✅ **DO:** use `Toggle`, `Slider`, `Stepper`, `Picker`, `Menu`, `.contextMenu` as-is. With the iOS 26 SDK they adopt the look and interaction glass on their own (WWDC25 session 323). (Snippets 5–9, 12.)
- ❌ **DON'T:** wrap controls in manual `.glassEffect()` or draw custom backgrounds with blur. Glass can't sample other glass (milky double-blur) and the control already morphs to glass during interaction; your extra layer breaks the system's animation.

**C. Glass buttons: capsule and content-hugging, not full-width**
- ✅ **DO:** `.glass`/`.glassProminent` buttons capsule-shaped (the system provides it) and hugging the content. 🟡
- ❌ **DON'T:** stretch a glass button to the screen's full width. Glass is the functional layer floating over content; a full-width glass bar competes with the content and breaks the "floating control" reading.

**D. Tint with meaning, not decoration**
- ✅ **DO:** `.tint()` only with semantic meaning (accent = primary action; red = destructive via `role: .destructive`; green = success/confirmation). Never color as the only information channel (pair with icon or text).
- ❌ **DON'T:** tint each button a different color "to tell them apart". Color is a system language with fixed meaning; using it as decoration confuses (a green button shouldn't lead to a destructive action).

**E. System menus, not handmade popovers**
- ✅ **DO:** `Menu` and `.contextMenu` for action lists; the system morphs the button into the menu/popover and manages the glass background. The destructive action always last, after a `Divider()`, with `role: .destructive`. (Snippets 10–12.)
- ❌ **DON'T:** build your own dropdown with `@State` + `ZStack` + manual blurred background. You lose the system's morphing, correct dismiss behavior, and the accessibility (VoiceOver, Dynamic Type) the native menu brings for free.

**F. 44×44pt touch targets with 8pt separation**
- ✅ **DO:** at least 44×44pt per tappable control (snippet 13: `.frame(width: 44, height: 44)` + `.contentShape(Rectangle())`) and at least 8pt between adjacent targets. ✅ (HIG rule)
- ❌ **DON'T:** snippet 14 (gesture glued to the icon, ~20pt) and icon-only buttons glued together. Below 44pt mis-taps skyrocket, especially in motion; and without a real `Button`, VoiceOver won't announce the control as interactive.

**G. No glass in the content layer**
- ✅ **DO:** reserve `.glass`, `.glassProminent`, and `.glassEffect()` for the functional layer: navigation, toolbars, floating buttons, menus, sheets. ✅ (HIG)
- ❌ **DON'T:** list cards, row backgrounds, or text with glass "because it looks pretty". "Don't use Liquid Glass in the content layer" — glass signals interactivity/navigation; in content it only distracts. The sole exception is the control *while manipulated* (slider/toggle already do it on their own).

See also: `navigation.md` (toolbar actions), `presentation.md` (menus vs dialogs).
