# The two-layer model (iOS 26+)

The HIG describes every app as **two distinct layers**. All Liquid Glass design revolves around this distinction.

**Verification legend:** ✅ = direct quote or rule from the HIG / official docs confirmed in ≥2 sources; 🟡 = consistently documented in ≥3 sources; ⚠️ = approximation or unverified.

## Verbatim Apple quotes ✅

From WWDC26, session 251 "Communicate your brand identity on iOS":

> "Think of your app as two distinct layers: the UI layer, which serves as the global navigation, and the content layer, which sits beneath these controls and contains all the features that make your app unique."

> "Conceptually, the content layer is the best opportunity to express your brand identity. This allows the UI layer of your app to act as a foundation that helps people get around and find what they're looking for."

> "With the new design language we introduced, our recommendation is to move color into the content area of your app, into the scroll view. That way, Liquid Glass controls sit above the content layer and pick up your brand color dynamically."

From the HIG "Materials" page (reproduced identically in ≥3 mirrors):

> "Liquid Glass forms a distinct functional layer for controls and navigation elements — like tab bars and sidebars — that floats above the content layer, establishing a clear visual hierarchy between functional elements and content."

> "**Don't use Liquid Glass in the content layer.** Liquid Glass works best when it provides a clear distinction between interactive elements and content, and including it in the content layer can result in unnecessary complexity and a confusing visual hierarchy."

> "Use Liquid Glass effects sparingly… Limit these effects to the most important functional elements in your app."

From WWDC25, session 219 "Meet Liquid Glass":

> "Liquid Glass is best reserved for the navigation layer that floats above the content of your app."

> "making [a tableview] Liquid Glass would make it compete with other elements and muddy the hierarchy. So keep it in the content layer instead."

## The two layers ✅

| | **Functional (UI) layer** | **Content layer** |
|---|---|---|
| What it is | Floats on top: tab bars, toolbars, sidebars, floating controls, alerts, popovers, sheets | The app's substance: data, lists, tables, cards, images, scroll views, backgrounds |
| Material | **Liquid Glass lives here.** System components adopt the material automatically | Standard materials at rest, NEVER Liquid Glass. Brand identity lives here: color, typography |
| Example | The tab bar floating over the feed | The photo feed, the document, the map |

**Decision rule:** if the glass is over functional UI → fine; if it's over content → almost always wrong.

## Actionable rules ✅

1. **Content scrolls underneath the functional layer.** Extend content full-screen under sidebars, toolbars, and tab bars; use scroll-edge effects instead of solid backgrounds under controls.
2. **No glass-on-glass stacking**: a single floating layer at a time.
3. **Move color into the content layer**, into the scroll view: floating Liquid Glass controls pick up your brand color dynamically.
4. 🟡 Material variants: **Regular** (default) and **Clear** (only over rich media, with an attenuation layer behind to preserve contrast). Consistently documented in SwiftUI; no source contradicts this.

## The exception: transient controls ✅

Documented as the **single exception**: a control living in the content layer but with a **transient** interactive element (a slider, a toggle) adopts a Liquid Glass appearance **only while the person is manipulating it**. At rest it returns to standard content.

## SwiftUI: content under the functional layer ✅

```swift
import SwiftUI

// WHEN: a list screen with a floating Liquid Glass tab bar.
// Rule: the scroll reaches the screen edges and the content passes
// UNDERNEATH the bar; no solid background clipping the view.
struct FeedView: View {
    var body: some View {
        NavigationStack {
            // Content fills the whole screen: the tab bar floats above.
            ScrollView {
                LazyVStack(spacing: 12) {
                    ForEach(0..<30) { i in
                        RowCard(index: i)
                    }
                }
                .padding()
                // Bottom padding so the last row isn't hidden
                // behind the floating functional layer.
                .padding(.bottom, 90)
            }
            .ignoresSafeArea(edges: .bottom) // ✅ content goes edge to edge
            .navigationTitle("Home")
            // ✅ The system tab bar adopts Liquid Glass on its own:
            // no need to apply any material by hand.
            .toolbar {
                ToolbarItemGroup(placement: .bottomBar) {
                    Button("New", systemImage: "plus") { /* ... */ }
                    Spacer()
                    Button("Search", systemImage: "magnifyingglass") { /* ... */ }
                }
            }
        }
    }
}
```

```swift
import SwiftUI

// WHEN: ❌ DON'T — glass inside the content.
// A table or list in the content layer NEVER takes Liquid Glass:
// it competes with functional controls and muddies the hierarchy (WWDC25/219).
struct BadExampleDoNotCopy: View {
    var body: some View {
        List {
            Text("Row 1")
            Text("Row 2")
        }
        // .glassEffect()          // ❌ NEVER on content at rest
        // .background(.ultraThinMaterial)  // ❌ same: content is standard
    }
}
```

## CSS: the same model on the web ✅

```css
/* WHEN: a web layout with a functional navigation bar floating
   over the content, iOS 26 style. */
:root { color-scheme: light dark; }

.functional-bar {
  position: sticky;
  bottom: 1rem;
  margin-inline: auto;
  width: fit-content;
  padding: 0.5rem 1rem;
  border-radius: 999px;

  /* Functional layer: the "glass" floats over the content.
     NEVER apply this treatment to content cards. */
  background: color-mix(in srgb, Canvas 55%, transparent);
  backdrop-filter: blur(24px) saturate(1.6);
  -webkit-backdrop-filter: blur(24px) saturate(1.6);
  box-shadow: 0 8px 32px rgb(0 0 0 / 0.18);
}

.content {
  /* Content layer: this is where brand color and substance live. */
  background: var(--brand-soft-color);
}

/* ❌ DON'T: .card { backdrop-filter: blur(...); }
   Glass-on-glass muddies the hierarchy: glass-on-glass is forbidden. */
```

## Do / don't pairs

1. **Glass in the functional layer only** ✅
   - ✅ DO: system tab bars, toolbars, and floating controls with Liquid Glass.
   - ❌ DON'T: cards, tables, lists, or backgrounds of the content layer with a glass effect.

2. **Color in the content, not in the glass** ✅
   - ✅ DO: brand color goes in the scroll view / content-layer background; the floating glass picks it up dynamically.
   - ❌ DON'T: tint glass controls with brand color; glass "has no inherent color: it picks up what's behind it."

3. **Edge-to-edge content under the UI** ✅
   - ✅ DO: extend the scroll under tab bars and toolbars (scroll-edge effects).
   - ❌ DON'T: clip content with solid backgrounds exactly where the bar starts.

4. **One floating layer** ✅
   - ✅ DO: a single floating glass element per zone.
   - ❌ DON'T: sheets over popovers over bars, all with glass (glass-on-glass).

See also: `principles.md` (Familiarity, Simplicity), `../materials/liquid-glass.md`, `color.md` (meaningful tint).
