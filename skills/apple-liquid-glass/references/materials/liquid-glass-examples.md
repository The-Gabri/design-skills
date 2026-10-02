# Liquid Glass — copy-pasteable SwiftUI examples (iOS 26+)

> Real snippets, ready to paste. Each block has a `WHEN` comment with the
> situation to use it in. Conceptual rules in `liquid-glass.md`.
> Legend: **✅** verified (HIG/official docs, ≥2 sources) · **🟡**
> consistently documented in ≥3 sources · **⚠️** unverified — don't use.
>
> **Non-existent APIs** (⚠️ circulating in community sources, not in the
> official docs): `.glassClear`, `.glassBorderless` as button styles,
> `GlassEffectUnion` / `glassEffectUnion`. They don't appear in these examples.

## 1. `.glassEffect(.regular)` — custom floating toolbar ✅

```swift
import SwiftUI

// WHEN: a custom toolbar floating over content (functional layer).
// With the 26 SDK the system toolbars already come with glass on their own;
// this snippet is for when you need a custom floating bar.
// ✅ .regular is the default variant: it protects legibility over
// any background. The default shape is a capsule.
struct ViewWithFloatingToolbar: View {
    @State private var liked = false

    var body: some View {
        ZStack {
            // Edge-to-edge content, extended underneath the bar.
            PhotoList()

            VStack {
                Spacer()

                HStack(spacing: 20) {
                    Button("Like", systemImage: liked ? "heart.fill" : "heart") {
                        liked.toggle()
                    }
                    Button("Share", systemImage: "square.and.arrow.up") {
                        // share action
                    }
                    Button("Delete", systemImage: "trash") {
                        // delete action
                    }
                }
                .padding(.horizontal, 24)
                .padding(.vertical, 14)
                // ✅ .glassEffect AFTER padding/font/color: sampling
                // uses the view's final shape.
                .glassEffect(.regular, in: .capsule)
                .labelStyle(.iconOnly)
                .padding(.bottom, 16)
            }
        }
    }
}
```

Notes: ✅

- The content must peek *underneath* the bar: don't put opaque fills behind it.
- If you anchor it to the screen's bottom edge, prefer
  `.safeAreaBar(.bottom)` over manual `VStack` + `Spacer`: the system only
  adds the scroll edge effect that way.

## 2. `.glassEffect(.clear)` — controls over photo/video ✅

```swift
import SwiftUI

// WHEN: player or viewer over rich media (photo, video) at full screen.
// ✅ .clear is "aggressively transparent": only over visually rich
// backgrounds, never over dense text or flat backgrounds.
struct ControlsOverPhoto: View {
    var body: some View {
        ZStack {
            Image("sunset")
                .resizable()
                .aspectRatio(contentMode: .fill)
                .ignoresSafeArea()

            // ✅ If the content underneath is BRIGHT, the HIG asks for
            // a 35% dark dimming layer: without it the text is unreadable.
            // (On dark backgrounds it's not needed.)
            Color.black.opacity(0.35)
                .ignoresSafeArea()

            VStack {
                Spacer()

                HStack(spacing: 28) {
                    Button("Back", systemImage: "backward.fill") {}
                    Button("Play", systemImage: "play.fill") {}
                    Button("Forward", systemImage: "forward.fill") {}
                }
                .font(.title)
                .padding(.horizontal, 28)
                .padding(.vertical, 16)
                .glassEffect(.clear, in: .capsule)
                .labelStyle(.iconOnly)
                .padding(.bottom, 24)
            }
        }
        // ✅ The content OVER the glass is solid (never glass):
        // it reads as one thin fused layer.
        .foregroundStyle(.white)
    }
}
```

## 3. `GlassEffectContainer` — group of controls ✅

```swift
import SwiftUI

// WHEN: two or more sibling glass surfaces close together.
// WHY: glass CANNOT sample other glass. Without a container, each
// .glassEffect samples its background separately (including the neighbor's
// glass) and the result is inconsistent plus more GPU cost. The container
// groups the elements into a single sampling region: better merging and
// better performance. ✅
// The `spacing` must match the layout's real spacing for the visual
// merge to look right in transitions. 🟡
struct FloatingPalette: View {
    var body: some View {
        GlassEffectContainer(spacing: 16) {
            HStack(spacing: 16) {
                Button("Pencil", systemImage: "pencil") {}
                Button("Eraser", systemImage: "eraser") {}
                Button("Trash", systemImage: "trash") {}
            }
            .labelStyle(.iconOnly)
            .font(.title2)
            // Each button carries its own glassEffect; the container unifies them.
            .buttonStyle(.glass)
        }
        .padding()
    }
}
```

### 3.1 Morphing between states 🟡

```swift
import SwiftUI

// WHEN: a glass element that transforms (compact ↔ expanded)
// and you want the glass to "morph" from one state to another instead of fading.
// NEEDS: GlassEffectContainer + same id in the same @Namespace +
// animation on the state change. 🟡
struct MorphCard: View {
    @Namespace private var ns
    @State private var isExpanded = false

    var body: some View {
        GlassEffectContainer {
            if isExpanded {
                ExpandedCard()
                    .glassEffect()
                    .glassEffectID("card", in: ns)
            } else {
                CompactCard()
                    .glassEffect()
                    .glassEffectID("card", in: ns)
            }
        }
        .animation(.smooth, value: isExpanded)
    }
}
```

### 3.2 Separators in system toolbars 🟡

```swift
// WHEN: you need a visual cut between items in a system toolbar with glass
// (iOS 26). 🟡
.toolbar {
    ToolbarItem(placement: .primaryAction) { Button("Edit") { } }
    ToolbarSpacer(.fixed)              // the official separator for glass toolbars
    ToolbarItem(placement: .primaryAction) { Button("Share") { } }
}
```

## 4. Buttons: `.buttonStyle(.glass)` / `.glassProminent` ✅

```swift
import SwiftUI

// WHEN: action buttons in the functional layer. Don't rebuild glass
// with hand-drawn blurs/shadows: the system style already brings the
// material, the touch response (.interactive), and Reduce Transparency
// adaptation.
// ✅ .glass = neutral/secondary action; .glassProminent = primary action
// (the .borderedProminent replacement in 26).
struct GlassButtons: View {
    var body: some View {
        VStack(spacing: 16) {
            // Secondary action: neutral glass.
            Button("Cancel") { /* dismiss */ }
                .buttonStyle(.glass)

            // Primary action: tinted glass.
            // ✅ .tint(_:) takes ONE color (no gradients); the color goes
            // on the prominent's background, never on the symbol/text.
            Button("Save") { /* save */ }
                .buttonStyle(.glassProminent)
                .tint(.blue)

            // Shape and size adjust with system modifiers,
            // without redrawing the label by hand. ✅
            Button("Share", systemImage: "square.and.arrow.up") { /* share */ }
                .buttonStyle(.glass)
                .buttonBorderShape(.capsule)
                .controlSize(.large)
        }
    }
}
```

Precedence rule: ✅ `.buttonStyle(.glass)` first; only if the system style
isn't enough, build the button with manual `.glassEffect()` (see §5).

## 5. Custom button with `.glassEffect` + meaningful tint ✅/🟡

```swift
import SwiftUI

// WHEN: a primary action button that doesn't fit .buttonStyle(.glass)
// (custom shape or content). Tint only with semantic meaning: here the
// view's main action. Never more than 1–2 tinted actions per view.
// 🟡 .tint(_:) and .interactive() are Glass METHODS, not view
// modifiers: they go inside glassEffect(...).
Button(action: share) {
    Label("Share", systemImage: "square.and.arrow.up")
        .padding(.horizontal, 20)
        .padding(.vertical, 12)
}
.glassEffect(.regular.tint(.blue).interactive(), in: .capsule)
```

And the macOS form (small rounded rects instead of capsules): 🟡

```swift
.glassEffect(.regular.interactive(), in: .rect(cornerRadius: 16))
// On iOS: .rect(cornerRadius: .containerConcentric) aligns the radii with
// the container at all sizes. 🟡
```

## 6. Floating card over content ✅

```swift
import SwiftUI

// WHEN: an info card floating over a photo or map
// (functional layer). The content fills the screen underneath. ✅
struct FloatingCard: View {
    var body: some View {
        ZStack(alignment: .bottom) {
            Image("landscape")
                .resizable()
                .scaledToFill()
                .ignoresSafeArea()      // content under the glass

            GlassEffectContainer(spacing: 16) {
                VStack(alignment: .leading, spacing: 8) {
                    Text("Sunset in the Pyrenees")
                        .font(.headline)
                        .foregroundStyle(.primary)
                    Text("2 hours ago · 24 photos")
                        .font(.subheadline)
                        .foregroundStyle(.secondary)
                }
                .padding(16)
                .glassEffect(.regular, in: .rect(cornerRadius: .containerConcentric))
            }
            .padding()
        }
    }
}
```

*If the background is bright and you prefer `.clear`, the 35% dimming veil goes BEHIND the glass: `Color.black.opacity(0.35)`.* ✅ (see §2)

## 7. Tab bar — don't add glass manually ✅/🟡

```swift
import SwiftUI

// WHEN: the app's tab bar. With the 26 SDK it adopts Liquid Glass on its own:
// do NOT put .glassEffect over it. ✅
struct AppTabs: View {
    var body: some View {
        TabView {
            Tab("Home", systemImage: "house") { HomeView() }
            Tab("Search", systemImage: "magnifyingglass", role: .search) { SearchView() }
            Tab("Settings", systemImage: "gear") { SettingsView() }
        }
        // 🟡 iOS 26: the tab bar minimizes on scroll.
        .tabBarMinimizeBehavior(.onScrollDown)
    }
}
```

## 8. Sheet — don't fight the system's material 🟡

```swift
import SwiftUI

// WHEN: presenting a sheet. The system already brings its material: no
// opaque .background() or manual blurs. The grabber (.visible) is also
// a VoiceOver hint. 🟡
struct MainView: View {
    @State private var showSheet = false

    var body: some View {
        Button("Details") { showSheet = true }
            .buttonStyle(.glassProminent)
            .sheet(isPresented: $showSheet) {
                NavigationStack {
                    Form { /* … */ }
                        .navigationTitle("Details")
                        .toolbar {
                            ToolbarItem(placement: .cancellationAction) { Button("Cancel") { } }
                            ToolbarItem(placement: .confirmationAction) {
                                Button("OK") { }.buttonStyle(.glassProminent)
                            }
                        }
                }
                .presentationDetents([.medium, .large])
                .presentationDragIndicator(.visible)
                // No opaque .background(): let the system's material show.
            }
    }
}
```

## 9. Pre-26 fallback with `#available` 🟡

```swift
import SwiftUI

// WHEN: your deployment target includes iOS < 26. The 26+ SDK applies glass
// automatically to system components; for custom chrome you must gate and
// provide a fallback with standard materials. 🟡
struct CompatibleButton: View {
    var body: some View {
        Group {
            if #available(iOS 26, *) {
                Text("Hello")
                    .padding()
                    .glassEffect(.regular.interactive(), in: .rect(cornerRadius: 16))
            } else {
                Text("Hello")
                    .padding()
                    // Pre-26 fallback: standard material + hairline. 🟡
                    .background(.ultraThinMaterial, in: RoundedRectangle(cornerRadius: 16))
                    .overlay(
                        RoundedRectangle(cornerRadius: 16)
                            .strokeBorder(.quaternary, lineWidth: 0.5)
                    )
            }
        }
    }
}
```

## 10. Reduce Transparency — your own solid fallback ✅/🟡

```swift
import SwiftUI

// WHEN: you build custom translucency (not system glass,
// which already falls back to opaque on its own). System glass respects
// Reduce Transparency automatically; yours does NOT: provide a solid variant. ✅
struct AdaptiveBar: View {
    @Environment(\.accessibilityReduceTransparency) private var reduceTransparency

    var body: some View {
        HStack(spacing: 20) {
            Button("Like", systemImage: "heart") { }
            Button("Share", systemImage: "square.and.arrow.up") { }
        }
        .padding(.horizontal, 24)
        .padding(.vertical, 14)
        .labelStyle(.iconOnly)
        .background {
            if reduceTransparency {
                // ✅ Solid fallback: legible without translucency.
                Capsule().fill(Color(.systemBackground))
            } else {
                Capsule().fill(.ultraThinMaterial)
            }
        }
    }
}
```

## 11. Widget — don't fight the background 🟡

```swift
import WidgetKit
import SwiftUI

// WHEN: a widget. The system applies glass in tinted/clear modes;
// your job is not to fight the background and to mark what can be tinted. 🟡
struct SimpleWidget: Widget {
    var body: some WidgetConfiguration {
        StaticConfiguration(kind: "steps", provider: Provider()) { entry in
            VStack(alignment: .leading) {
                Text("\(entry.steps)")
                    .font(.system(size: 48, weight: .bold, design: .rounded))
                    .widgetAccentable()              // the system decides the tint
                Text("steps today")
                    .font(.caption)
                    .foregroundStyle(.secondary)
            }
            .containerBackground(for: .widget) {
                // The system replaces it with glass in tinted/clear modes.
                Color.blue.opacity(0.15)
            }
        }
    }
}
```

// ✅ The content must still read in monochrome when the system
// replaces the background with glass.

// ⚠️ `.containerBackground(.liquidMaterial, for: .widget)` appears in 1 source
// only: unverified, don't use.

## 12. Standard materials in the content layer ✅

Standard materials live **only in the content layer** (card backgrounds,
list panels, sidebars…). Never Liquid Glass there. ✅

```swift
import SwiftUI

// WHEN EACH ONE APPLIES (least to most opaque): ✅
// .ultraThinMaterial — barely-there veil; over already-legible backgrounds.
// .thinMaterial      — light cards over moving content.
// .regularMaterial   — the general one: panels, section backgrounds.
// .thickMaterial     — max legibility: dense sidebars, menus.
struct ContentCard: View {
    var body: some View {
        VStack(alignment: .leading, spacing: 8) {
            Text("Card headline")
                .font(.headline)
            Text("Content text. It sits on a standard material, never on Liquid Glass: the material doesn't compete with the background for attention.")
                .font(.subheadline)
                .foregroundStyle(.secondary)
        }
        .padding(16)
        // ✅ Standard material in a rounded rect: content, not glass.
        .background(.regularMaterial, in: .rect(cornerRadius: 16))
    }
}
```

### 12.1 The choice table ✅/🟡

| Material | When |
|---|---|
| `.ultraThinMaterial` | The background is already legible and you just want a subtle veil (e.g. header over a dark photo). ✅ |
| `.thinMaterial` | Light cards over moving content where the background should keep breathing. ✅ |
| `.regularMaterial` | General use: panels, section backgrounds, list cards. ✅ |
| `.thickMaterial` | High density or legibility risk: sidebars, menus, text-heavy overlays. ✅ |

HIG rules on materials: ✅

- "Choose materials and effects based on semantic meaning and recommended usage. Avoid selecting a material based on the apparent color it imparts" (system settings may change their appearance).
- Thicker materials (more opaque) → better contrast for text and fine detail; thinner materials (more translucent) → retain context by recalling the background content.
- Over materials, vibrant system colors; avoid `quaternary` over thin and ultraThin materials (contrast too low). Vibrancy levels (default > secondary > tertiary > quaternary) indicate relative contrast.
- 🟡 Heuristic from tvOS transferable to iOS (⚠️ the iOS HIG publishes no equivalent table — don't present it as an official rule): ultraThin → full-screen views with light scheme; thin → partially-darkening overlays with light scheme; regular → partially-darkening overlays; thick → overlays with dark scheme.

## 13. Do / don't pairs

1. **Glass in the functional layer only.**
   - ✅ DO: tab bars, toolbars, sidebars, floating buttons, sheets, alerts, and popovers take Liquid Glass. ✅
   - ❌ DON'T: list cards, app backgrounds, scroll views, or paragraphs with glass. Content uses standard materials or flat fills. ✅

2. **Never glass on glass.**
   - ✅ DO: group nearby glass controls in a `GlassEffectContainer` so they share one sampling region (glass can't sample other glass). ✅
   - ❌ DON'T: stack `.glassEffect` over another `.glassEffect`, or put a glass card over a glass toolbar. ✅/🟡

3. **What goes on top of glass takes no glass.**
   - ✅ DO: icons and labels over glass with solid fills or vibrancy: they read as one thin fused layer. ✅
   - ❌ DON'T: apply `.glassEffect` to the icon already inside a `.glass` button. ✅/🟡

4. **`.regular` by default, `.clear` with conditions.**
   - ✅ DO: `.regular` for almost everything (it's adaptive and protects legibility); `.clear` only over rich media (photo, video). ✅
   - ❌ DON'T: `.clear` over flat backgrounds or dense text; if the background is bright, add the 35% dimming layer. ✅

5. **Sparing and meaningful.**
   - ✅ DO: limit glass to the most important functional elements; `.tint` only with semantic meaning (primary, destructive), never decorative. ✅
   - ❌ DON'T: a screen full of custom glass surfaces competing with the content for attention. ✅

6. **Don't rebuild the system.**
   - ✅ DO: let `TabView`, `NavigationStack`, toolbars, sheets, and `.buttonStyle(.glass)` bring their material on their own. 🟡
   - ❌ DON'T: custom stacks of blur + shadows + borders to imitate Liquid Glass in native code; nor opaque backgrounds that fight the system's scroll edge effect. 🟡

7. **Modifier order.**
   - ✅ DO: `.glassEffect(...)` **LAST** in the chain, after layout, padding, font, and color. 🟡
   - ❌ DON'T: put it mid-chain (it samples the wrong region); nor `.background(Color…)` / `.blur` / `.shadow()` / `.clipShape()` on the same layer as the glass. 🟡

