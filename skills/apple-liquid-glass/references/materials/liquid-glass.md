# Liquid Glass — conceptual rules (iOS 26+ / macOS Tahoe 26+)

> Design rules for Apple's dynamic material. The full native API and
> verification marks: legend **✅** = direct HIG/official-doc rule confirmed
> in ≥2 sources · **🟡** = consistently documented in ≥3 independent sources
> (no direct quote) · **⚠️** = doubtful or unverified: handle with care.
> Copy-pasteable examples are in `liquid-glass-examples.md`.

## 1. What Liquid Glass is

✅ It's the dynamic material introduced in iOS/iPadOS 26, macOS Tahoe 26,
watchOS 26, and tvOS 26 (announced at WWDC 2025): the biggest visual redesign
since iOS 7. Apple defines it as a *meta-material* that bends and focuses
light in real time: refraction/lensing, specular highlights that respond to
motion, adaptive shadows, and translucency that adapts to the content
underneath.

✅ It unifies the design language across all Apple platforms for the first
time (the visual depth is inherited from visionOS).

✅ In the 26.x cycle — and refined in the 27th generation — the 26+ SDK
applies Liquid Glass **automatically** to bars, tab bars, sheets, menus,
toolbars, and standard system controls; only *custom* chrome needs explicit
adoption. 🟡

### 1.1 The two-layer model

Every iOS 26+ interface is split into two layers, and the material has its
assigned one. ✅

- **Content layer**: the document, feed, photo, list, or map — the real
  content the person consumes, edge-to-edge.
- **Functional layer**: the navigation and controls floating above: tab
  bars, sidebars, toolbars, floating buttons, sheets, alerts, popovers,
  Dock. **Liquid Glass lives here.** ✅

In the content layer, standard materials (`.ultraThinMaterial` →
`.thickMaterial`) or opaque backgrounds are used — never Liquid Glass (§3).

## 2. The variants: regular / clear

✅ There are exactly two `Glass` variants: **regular** and **clear**. Their
optics differ: **they must not be mixed in the same context** (never combine
them in the same element or group).

| Variant | Behavior | When to use |
|---|---|---|
| `.regular` ✅ | Adaptive by default: blurs and adjusts background luminance to keep the foreground legible. | Components with lots of text or where legibility is at risk: alerts, sidebars, popovers. **"Most system components use this variant."** ✅ |
| `.clear` ✅ | Highly translucent: only the base refraction, no adaptive luminance mask. | **Only** over visually rich backgrounds (photos, videos) for an immersive experience. Never for functional text or over flat backgrounds. ✅ |

✅ Contrast rule for `.clear`: if the underlying content is **bright**, add
behind it a dark dimming layer of **35% opacity**. If the background is
already dark enough, no need; nor if you use AVKit's media playback controls
(they bring their own layer).

✅ The scroll edge effects (§7) further improve the legibility of the
`.regular` variant.

🟡 `.identity` is not an "effect" but the opt-out: it keeps the modifier in
the chain but applies no material. Useful for toggling states without
changing the hierarchy or re-running sampling:
`glassEffect(isActive ? .regular : .identity)`.

## 3. "Don't use Liquid Glass in the content layer" — and its exception

✅ **"Don't use Liquid Glass in the content layer."** (verbatim HIG quote,
Materials page). Putting it there creates unnecessary complexity and a
confusing visual hierarchy. In the content layer: standard materials or
opaque.

✅ **Single exception**: content-layer controls with a *transient*
interactive element — **sliders and toggles** — take a Liquid Glass
appearance **only while the person manipulates them**, to emphasize their
interactivity; on release they return to their non-glass state.

## 4. Sparing use and meaningful tint

✅ **"Use Liquid Glass effects sparingly."** The system's standard
components already adopt the material automatically; glass on custom controls
is limited to the **most important** functional elements. Overusing it
distracts from the content it's supposed to frame. Typically 1–2 glass
surfaces per screen. 🟡

✅ "Differentiate controls from content": under controls use the scroll edge
effect, not a solid or semi-opaque background; extend content full-screen
under sidebars, toolbars, and tab bars.

✅ "Reduce the use of toolbar backgrounds and tinted controls": don't paint
custom backgrounds on bars (remove opaque `toolbarBackground(.visible)`)
unless the brand demands it.

✅ Glass has no inherent color: it picks up what's behind it. Tint only what
needs emphasis — a primary action, a status indicator; the color goes on the
**background** of a prominent button, **not on its symbol/text**; don't tint
multiple controls on the same bar. Limit: **1, at most 2, tinted primary
actions per view.** ✅

✅ Provide light and dark color variants even in single-appearance apps:
Liquid Glass adaptivity needs both.

## 5. Glass on glass: `GlassEffectContainer`

✅ **Glass cannot sample other glass.** Two overlapping or interacting
`.glassEffect()` views look broken/doubled and also degrade performance.
**One glass layer per region.**

🟡 `GlassEffectContainer { ... }` groups adjacent glass shapes so they share
**a single sampling region / one render pass**: they unify the tint and allow
*morphing* (merging into each other in transitions). Don't wrap the whole
view tree in one giant container: **one container per cluster of glass that
belongs together** — better performance.

🟡 The `spacing:` parameter controls the distance at which shapes start
merging. Match or exceed the stack's interior spacing so they merge in
transitions but stay separate at rest.

🟡 **Morphing** (transforming between states): needs `GlassEffectContainer`
+ the same `id` in the same `@Namespace` (via `.glassEffectID("card", in: ns)`)
+ animation on the state change. (See the example in
`liquid-glass-examples.md`.)

⚠️ Never nest containers (documented in 1 source, consistent with the model).

### 5.1 Unverified APIs — do not use ⚠️

These signatures **circulate in community sources but aren't verified in the
official documentation**. Don't present them as real API; if you see them in
a third-party snippet, don't use them:

- ⚠️ `.glassClear` / `.glassBorderless` as button styles — absent from the docs.
- ⚠️ `GlassEffectUnion` (or `glassEffectUnion` as a union-effect modifier syntax) — unverified.
- ⚠️ `.containerBackground(.liquidMaterial, for: .widget)` — 1 source only, don't use.

## 6. Clear/Tinted preference (26.1+) and accessibility

✅ Since **iOS/iPadOS 26.1 and macOS 26.1**: Settings → Display & Brightness
→ Liquid Glass → **Clear** (default look, more transparent) or **Tinted**
(more opaque, more contrast). On Mac: System Settings → Appearance. Applies
to the whole system **including third-party apps** implementing Liquid
Glass, and to Lock Screen notifications.

✅ Apple themselves: *"Clear is more transparent, revealing the content
beneath. Tinted increases opacity and adds more contrast."*

Design implications:

- ✅ **Design for both** and verify text against the Tinted setting.
- ✅ **Reduce Transparency**: system glass automatically falls back to an
  opaque finish; custom translucency (what you build yourself) **doesn't** —
  you must provide your own solid fallback
  (`@Environment(\.accessibilityReduceTransparency)`). 🟡
- ✅ **Increase Contrast**: requires stronger fills/borders; if the default
  scheme doesn't meet minimum contrast, provide a higher-contrast one under
  this setting.
- ✅ Accessibility rule: verify text over glass against the **worst possible
  background** (the most problematic one), not the nominal background.

✅ (HIG quote): "the appearance of these variants may vary in response to
certain system settings, such as the preferred Liquid Glass appearance in
device settings, or accessibility settings that reduce transparency or
increase contrast."

## 7. The system's scroll edge effect

✅ Content scrolling **under floating bars** receives a progressive edge
effect: blur + fade (progressive blur) where content peeks under the bar, to
keep the glass controls legible. (HIG quote: "Scroll edge effects further
enhance legibility by blurring and reducing the opacity of background
content.")

✅ `ScrollView`, `List`, and `Form` have it **automatically** with the 26 SDK
— no opt-in required.

🟡 Related API: `.scrollEdgeEffectStyle(_:for:)` with values `.automatic`
(platform default), `.soft` (progressive fade with variable blur),
`.hard` (sharp cut with a divider line); and `.scrollEdgeEffectHidden(_:for:)`
to suppress it.

🟡 Platform defaults (consistent in ≥3 sources): iOS/iPadOS → `.soft`;
macOS → `.hard`.

✅ "Scroll edge effects replace bar backgrounds. No opaque bar fills, no
hairline dividers — the separation cue is the scroll edge effect
blurring/fading content under the bar at screen edges." Where content doesn't
cover the window, a **background extension view** mirrors adjacent content
behind sidebars and inspectors. (`backgroundExtensionEffect()`.)

🟡 For custom floating bars: use `safeAreaBar(edge:)` (the bar pins and
content flows underneath with blur) instead of handmade fade gradients.

⚠️ One source adds that in iOS 27 `.automatic` has its own refined
appearance and no longer simply resolves to soft/hard — unconfirmed in HIG.

## 8. Adoption and compatibility

🟡 Automatic adoption is decided by the **build SDK (Xcode 26), not the
deployment target**: recompiling gives glass to bars/sheets/menus without
raising the target. First migration pass: **delete** what fights the system
(`barTintColor`, custom background images,
`configureWithOpaqueBackground()`, manual blurs behind bars).

⚠️ `UIDesignRequiresCompatibility = true` in Info.plist preserves the iOS 18
appearance (1 detailed source; Apple plans to remove it in Xcode 27).

🟡 With a deployment target < 26 you must gate with `if #available(iOS 26, *)`
and provide a fallback with standard materials (e.g. `.ultraThinMaterial` +
hairline) — documented practice in ≥3 sources. (Example in
`liquid-glass-examples.md`.)

⚠️ visionOS: one source (against `swiftinterface`) claims
`@available(visionOS, unavailable)` for `Glass`/`glassEffect` — unconfirmed
in HIG; don't present as verified.

## 9. The SwiftUI API — what really exists

Availability: `iOS 26.0+ / macOS 26+ / tvOS 26+ / watchOS 26+`.

### 9.1 `glassEffect(_:in:)` ✅

Approximate signature (consistent in ≥4 sources, one quoting Apple's docs
verbatim): 🟡

```swift
func glassEffect(_ glass: Glass = .regular, in shape: some Shape = DefaultGlassEffectShape()) -> some View
```

- 🟡 `DefaultGlassEffectShape` is the shape the system chooses (capsule on
  iOS). Accepts any `Shape`: `.circle`, `.capsule`,
  `RoundedRectangle(cornerRadius:style:)`,
  `.rect(cornerRadius: .containerConcentric)` (radii aligned with the
  container at all sizes) or a custom `Shape`. macOS prefers small rounded
  rects (e.g. `cornerRadius: 8`).
- ⚠️ There is **no** `isEnabled:` parameter in the official signature (one
  source warns explicitly; other community sources show signatures with
  `isEnabled` — ignore them).

```swift
Text("Hello").padding().glassEffect()                                   // .regular + capsule
Text("Hello").padding().glassEffect(.clear)                             // only over rich media
Text("Hello").padding().glassEffect(.regular.tint(.blue))               // meaningful tint
Text("Hello").padding().glassEffect(.regular, in: .capsule)
Text("Hello").padding().glassEffect(highlighted ? .regular : .identity) // toggle without re-sampling
```
🟡

### 9.2 `Glass` — the material descriptor ✅

`Glass` is a value struct with exactly three base presets:
`.regular` (default), `.clear`, `.identity`. Configurable with
**chainable** methods:

```swift
func tint(_ color: Color?) -> Glass               // tints the material; nil clears it
func interactive(_ isEnabled: Bool = true) -> Glass // touch reaction: press scaling, bounce, shimmer and lighting from the touch point
```

✅ **`.tint(_:)` and `.interactive()` are `Glass` methods, NOT standalone
view modifiers.** Correct:
`.glassEffect(.regular.tint(.blue).interactive())`; chaining order doesn't
matter. `.interactive()` only on elements that respond to touch/pointer.

⚠️ Don't confuse: `.tint` as a **view modifier** exists in SwiftUI for other
uses — e.g. `.buttonStyle(.glassProminent).tint(.blue)` is valid to tint the
prominent button; that's not the `Glass` method.

⚠️ Open conflict on `.interactive()`: documented in 5+ sources without
parameters; the `.interactive(_:)` form with Bool appears in only 2; and one
"verified" source claims it also exists on macOS 26+, while most say iOS-only.
Test on the SDK.

### 9.3 Button styles ✅

✅ `.buttonStyle(.glass)` (secondary) and `.buttonStyle(.glassProminent)`
(primary, the 26 replacement for `.borderedProminent`) exist.

⚠️ `.buttonStyle(.glass(.clear))` (GlassButtonStyle with a `Glass`
configuration) exists per Apple docs as quoted, but verified in only 2
sources: not recommended without testing on the SDK.

### 9.4 Related utilities 🟡

- `scrollEdgeEffectStyle(_:for:)` — blur/fade of content under the bar at scroll edges (e.g. `.scrollEdgeEffectStyle(.soft, for: .top)`).
- `backgroundExtensionEffect()` — blurred mirror of content at the safe area edges, behind floating toolbars.
- `ToolbarSpacer(.fixed)` — visual cut between items in glass toolbars.
- `tabBarMinimizeBehavior(_:)` — tab bar minimization (iOS 26).
- `.glassEffectTransition(_:)` — controls glass appearance: `.matchedGeometry` (smooth morph), `.materialize` (fade + materialize for distant elements), `.identity` (no transition). Use this modifier, **not** the generic `.transition(...)`. (⚠️ exact case names not verified directly against Apple.)

⚠️ `.glassEffect(..., transition:)` as an overload of the modifier itself
appears in only 1 source (3 document only the dedicated modifier): use the
dedicated modifier.

### 9.5 Audit checklist 🟡

1. **`.glassEffect` goes LAST**: sampling uses the view's final shape; layout/frame/padding/font/foregroundStyle first. Putting it mid-chain samples the wrong region.
2. **Remove explicit backgrounds before glass**: no `.background(Color…)`, no `.blur`, no `.opacity` over the glass view.
3. **No `.shadow()` over glass**: glass already brings its own shadow.
4. **No `.clipShape()` on the same layer as `glassEffect`**: breaks rendering and morph. Pass the shape via the `in:` parameter.
5. The Simulator renders glass **milkier** than real hardware: verify the final look on device.
6. No glass on every element: typically 1–2 surfaces per screen (§4).
7. ⚠️ Glyphs inside the container lose contrast (1 source): keep icons/labels as a **separate layer above** the glass, not inside the container.

### 9.6 Performance ✅/🟡

✅ (System doc quote): "Creating too many Liquid Glass effect containers and applying too many effects to views outside of containers can degrade performance." → one container per cluster, no loose glass everywhere.

🟡 Glass blur is expensive on GPU: don't animate the blur, don't put continuous motion behind glass (the blur re-samples every frame); off-screen / background → fall back to an opaque fallback.

## 10. UIKit and AppKit (compact reference) 🟡

### 10.1 UIKit (iOS 26)

In UIKit glass is an **effect** (`UIGlassEffect`) inside a
`UIVisualEffectView`. Real signature from the SDK header (`UIGlassEffect.h`):

```objc
typedef NS_ENUM(NSInteger, UIGlassEffectStyle) { UIGlassEffectStyleRegular, UIGlassEffectStyleClear };
@interface UIGlassEffect : UIVisualEffect
@property(nonatomic, getter=isInteractive) BOOL interactive;
@property(nonatomic, copy, nullable) UIColor *tintColor;
+ (UIGlassEffect *)effectWithStyle:(UIGlassEffectStyle)style;   // Swift: UIGlassEffect(style:)
@end
@interface UIGlassContainerEffect : UIVisualEffect
@property CGFloat spacing;
@end
```

```swift
let glassEffect = UIGlassEffect()              // .regular by default
glassEffect.isInteractive = true               // the Glass.interactive() counterpart
glassEffect.tintColor = .systemBlue            // tint inside the material, not an overlay

let effectView = UIVisualEffectView(effect: glassEffect)
let label = UILabel()
label.text = "Glass"
effectView.contentView.addSubview(label)       // content goes in contentView, NEVER directly

let container = UIVisualEffectView(effect: UIGlassContainerEffect())  // the GlassEffectContainer counterpart
container.contentView.addSubview(firstGlassView)   // children with UIGlassEffect
```

Mechanics rules: **materialize/dematerialize inside `UIView.animate`**
(`effectView.effect = glassEffect` to appear, `= nil` to disappear); **never
animate `alpha`**. Corner, size, and light/dark changes also go in animation
blocks. Labels become vibrant: use dynamic colors (`.label`,
`.secondaryLabel`).

⚠️ Circulating non-existent signatures: `UIGlassEffect(glass:isInteractive:)`
does NOT exist; neither do `UIGlassEffectView` / `UIGlassEffectContainerView`
as UIKit classes (1 source mentions them; the header uses
`UIVisualEffectView` + effects). `NSVisualEffectView` gained no Liquid Glass.

Others: `scrollView.topEdgeEffect.style = .automatic` (UIScrollEdgeEffect per
edge); `barButtonItem.hidesSharedBackground = true` (excludes the item from
the shared glass). iOS/iPadOS/Catalyst/tvOS 26.0; no UIKit equivalent on
macOS, watchOS, or visionOS. 🟡

⚠️ `UIGlassEffect` and SwiftUI's `glassEffect` **don't share containers** —
morphing groups must stay within a single framework.

### 10.2 AppKit (macOS Tahoe 26)

On macOS glass is a **view** (`NSGlassEffectView`), not an effect. SDK
header as quoted:

```objc
@interface NSGlassEffectView: NSView
@property (nullable, strong) __kindof NSView *contentView;   // glass renders AROUND the contentView; nil shows nothing
@property CGFloat cornerRadius;
@property (nullable, copy) NSColor *tintColor;
@property NSGlassEffectViewStyle style;   // 0 = Regular, 1 = Clear
@end
```

```swift
if #available(macOS 26, *) {
    let glassView = NSGlassEffectView()
    glassView.contentView = myContentView
    glassView.style = .regular            // Regular self-tints with the NSAppearance; Clear is more "raw glass"
    glassView.cornerRadius = 12.0
    glassView.tintColor = .controlAccentColor
}
```

- `NSGlassEffectContainerView`: merges nearby `NSGlassEffectView`s (one
  render pass); has `spacing`. `NSButton.BezelStyle.glass`: new bezel with
  Liquid Glass (`button.bezelStyle = .glass`, tintable via `bezelColor`).
  `NSVisualEffectView` remains the legacy API for ordinary materials and
  back-deployment: it is **NOT** the path for custom Liquid Glass in Tahoe.
- Guidance: default to SwiftUI's `.glassEffect()` and bridge only the
  specific view that needs AppKit control. All macOS-only and
  macOS-26-only: gate every symbol.

⚠️ `NSControl.BorderShape` and `NSScrollView`'s automatic scroll edge
effect: 1 source each, unconfirmed.

## 11. Verbatim HIG quotes ✅

- "Don't use Liquid Glass in the content layer."
- "Use Liquid Glass effects sparingly."
- "Only use clear Liquid Glass for components that appear over visually rich backgrounds."
- "If the underlying content is bright, consider adding a dark dimming layer of **35% opacity**." / "If the underlying content is sufficiently dark, or if you use standard media playback controls from AVKit that provide their own dimming layer, you don't need to apply a dimming layer."
- On `.regular`: "Most system components use this variant."
- "Glass has no inherent color; it picks up what's behind it. Tint only elements that need emphasis — a primary action, a status indicator. Put color on the *background* of a prominent button, not on its symbol/text. Don't tint multiple controls in one bar."
- "Provide light and dark color variants even in a single-appearance app — Liquid Glass adaptivity needs both."
- "Scroll edge effects replace bar backgrounds. No opaque bar fills, no hairline dividers."
- "Choose materials and effects based on semantic meaning and recommended usage. Avoid selecting a material based on the apparent color it imparts."

## Sources

- HIG Materials: https://developer.apple.com/design/human-interface-guidelines/materials — verified via faithful mirrors:
  - https://github.com/tsdsj/apple-style/blob/HEAD/skills/Apple-Style-HIG/reference/hig/materials.md
  - https://github.com/dickwu/apple-design-skill/blob/HEAD/references/hig/materials.md
  - https://github.com/elevatormusic/apple-hig/blob/HEAD/skills/apple-hig/guidelines/foundations/liquid-glass.md
- Official doc "Applying Liquid Glass to custom views": https://developer.apple.com/documentation/swiftui/applying-liquid-glass-to-custom-views
- API docs (via third parties): `glassEffectContainer`, `Glass.tint(_:)`, `Glass.interactive(_:)`, `view/glassEffectID(_:in:)`, `PrimitiveButtonStyle/glass(_:)`
- API surface against swiftmodule: https://github.com/is52hertz/videoplayer/blob/HEAD/.claude/skills/glass-know/references/api.md
- Clear/Tinted setting 26.1: https://www.macrumors.com/2025/10/20/ios-26-1-liquid-glass-toggle · https://9to5mac.com/2025/10/20/ios-26-1-beta-4-adds-new-setting-to-tone-down-liquid-glass-transparency
- Scroll edge effects: https://github.com/farkasseb/liquid-glass-skill/blob/HEAD/references/swiftui.md
