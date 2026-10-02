# watchOS ✅/🟡

The watch is a **glanceable companion**, not a phone in miniature ✅. Interactions of seconds: the "ten-second test" — if you had ten seconds of attention, what would you show? ✅

## Glanceable first ✅/🟡

- ✅ Every screen answers in a glance (≤2 s); **one clear focus per screen**; 2–3 level hierarchy max.
- ✅ The surfaces that matter are often **outside the app**: **complications**, **Smart Stack**, **notifications**, **Live Activities** — design them first, not last.
- ✅ Launch straight to the detail view chosen by location/recency/frequency, so unambiguous it needs no title.
- ✅ **No indeterminate spinners**: promise a notification instead.
- ✅ **Always dark** (there is no light mode); background color is used to communicate, not to decorate.
- ✅ **SF Compact** is the system font (**SF Compact Rounded in complications**).
- 🟡 Converging metrics: default body text **16 pt**, **minimum 12 pt**; default controls 44×44 pt, minimum 28×28 pt; ≤3 glyph buttons or ≤2 text buttons per row; action sheets ≤4 buttons including Cancel (Cancel top-left). No hierarchy built on size alone (the whole range runs 12–32 pt).
- 🟡 Dynamic Type on watch: **xS–xxxL + AX1–AX3** (independent of the iPhone setting; the "Text Size" setting is local to the Watch). No iOS styles like Subheadline or Callout; Footnote splits into Footnote 1 / Footnote 2. Practical bias: the number that matters in large (`.title2`/`.largeTitle`), everything else in `.caption`/`.footnote`.
- 🟡 watchOS 26: Liquid Glass, wrist-flick dismiss, Controls on the watch.
- ✅ Watch app icons: the system masks to a **circle** from a square **1088×1088** layout (no appearance variants); keep the brand away from the edge, no baked highlights or shadows (the system applies them).

## Complications ✅/🟡

- ✅ Families (WidgetKit since watchOS 9; ClockKit only for pre-9 deployment targets): `circularSmall` (single value/icon/gauge), `graphicCorner` (corners, gauge with label or text with icon), `graphicCircular` (large circle: gauge, icon with value), `graphicRectangular` (wide rectangle: multi-line text, graph), `graphicExtraLarge` (full-width circle: large gauge or prominent value). In the current HIG mirror, the iOS accessory families (circular, corner, inline, rectangular) serve as complications and Smart Stack on the Watch.
- ✅ **Tinted mode is a first-class appearance** for complications, not a fallback: tinting desaturates full-color images, so signals depending on color alone disappear. Line width in complications ≥ 2 pt.
- ✅ Documented anti-pattern: **supporting a single complication family** = fewer watch faces to live on = less real surface area of use. Design for several families.
- ✅ A complication's tap must land on the app's **relevant content**, not the generic home.
- ✅ **Limited update budget**: timelines declare display times and the system enforces the budget (design against the mechanism, don't assume live refresh). Budget quoted in a single source: ~40–70 `reloadTimelines` per day — burn through it and the complication stays stale by the afternoon. Treat as indicative, not an official figure (Apple publishes no number). ⚠️
- ✅ Timely and fresh information, sensible placeholder, no using the slot for branding; legible on all faces (system tint, glass in watchOS 26).
- 🟡 "Be a tool, not a billboard": no marketing on system surfaces.

### Example: steps complication with WidgetKit 🟡

```swift
import WidgetKit
import SwiftUI

// ═══════════════════════════════════════════════════════════════════
// WHEN: a critical datum on the watch face — steps, next appointment,
// a device's battery level.
// LIMITS: accessory families render TINTED (monochrome): color can't be
// the only information channel; no scroll and no interaction except
// opening the app on tap. Since watchOS 9 ClockKit is deprecated: the
// complication IS a WidgetKit widget. 🟡
// It lives in a WidgetKit extension inside the watch app. ✅
// ═══════════════════════════════════════════════════════════════════

struct StepsEntry: TimelineEntry {
    let date: Date
    let steps: Int
    let goal: Int
}

struct StepsProvider: TimelineProvider {
    func placeholder(in context: Context) -> StepsEntry {
        StepsEntry(date: Date(), steps: 4000, goal: 10_000)
    }

    func getSnapshot(in context: Context, completion: @escaping (StepsEntry) -> Void) {
        completion(StepsEntry(date: Date(), steps: 6500, goal: 10_000))
    }

    func getTimeline(in context: Context, completion: @escaping (Timeline<StepsEntry>) -> Void) {
        let now = Date()
        let entry = StepsEntry(date: now, steps: 6500, goal: 10_000)
        completion(Timeline(entries: [entry], policy: .after(now.addingTimeInterval(1800))))
    }
}

struct StepsComplication: View {
    @Environment(\.widgetFamily) private var family
    let entry: StepsEntry

    var body: some View {
        switch family {
        case .accessoryCircular:
            // On the circular face the Gauge is the natural primitive. ✅
            Gauge(value: Double(entry.steps), in: 0...Double(entry.goal)) {
                Text("\(entry.steps / 1000)k")
            } currentValueLabel: {
                Text("\(entry.steps)")
            }
            .gaugeStyle(.accessoryCircularCapacity) // ⚠️ face style; confirm the signature in the official docs
            .widgetURL(URL(string: "habits://steps")) // Tap opens the watch app. 🟡
        default: // .accessoryRectangular: about 3 lines, mini-dashboard
            VStack(alignment: .leading, spacing: 2) {
                Text("Steps")
                    .font(.caption2)
                    .foregroundStyle(.secondary)
                Text("\(entry.steps)")
                    .font(.title2.bold())
                ProgressView(value: Double(entry.steps), total: Double(entry.goal))
            }
            .widgetURL(URL(string: "habits://steps"))
        }
    }
}

struct StepsWidget: Widget {
    let kind = "StepsWidget"

    var body: some WidgetConfiguration {
        StaticConfiguration(kind: kind, provider: StepsProvider()) { entry in
            StepsComplication(entry: entry)
                // Native face background; better than a handmade translucent shape. ✅
                .containerBackground(for: .widget) { AccessoryWidgetBackground() }
        }
        .configurationDisplayName("Steps")
        .description("Your step progress on the watch face.")
        .supportedFamilies([.accessoryCircular, .accessoryRectangular])
    }
}

@main
struct WatchBundle: WidgetBundle {
    var body: some Widget {
        StepsWidget()
    }
}
```

## Always-On ✅/🟡

When the wrist drops, the watch dims the screen but doesn't turn it off. Rules (convergent in 3+ sources) ✅:

1. Reduce visual complexity: drop animations, secondary UI, and non-essential detail; only the critical information.
2. **Hide sensitive or private data** (message contents, health, finance) — use redacted/placeholder content (`.privacySensitive()`).
3. Reduce update frequency: **no more than once per minute** (`TimelineView` with `.everyMinute` schedule).
4. Use the system's dimming, **don't implement your own dimming**; content must stay legible at reduced brightness.
5. Test both states: the transition must not produce **layout jumps** on wrist raise.
6. 🟡 Read `isLuminanceReduced` to detect the state (not device lists — Apple's doc predates the SE's Always-On).

### Example: Always-On branch 🟡

```swift
import SwiftUI

// ═══════════════════════════════════════════════════════════════════
// WHEN: any watch screen that must stay useful with the wrist down
// (workout, audio, training navigation).
// LIMITS: the dimmed state is detected via the system environment;
// the sensitive is redacted, the secondary dims, the layout doesn't
// move between states.
// ═══════════════════════════════════════════════════════════════════

struct WorkoutView: View {
    @Environment(\.isLuminanceReduced) private var dimmed // ✅
    let pace: String
    let privateMessage: String

    var body: some View {
        VStack(spacing: 4) {
            // Critical datum: visible in both states, no continuous animation. ✅
            Text(pace)
                .font(.largeTitle.bold())
                .opacity(dimmed ? 0.75 : 1) // Soft dimming, no jumps. 🟡

            // Sensitive datum: redacted when the screen is dimmed. ✅
            Text(privateMessage)
                .font(.caption)
                .privacySensitive(true)
        }
    }
}
```

## Digital Crown ✅/🟡

- ✅ "Use the Digital Crown to provide vertical navigation for scrolling or switching between screens" — it's the primary vertical navigation, but **always with a touch equivalent**: never the only path. Always visual feedback; haptic feedback only on meaningful state changes.
- 🟡 Navigation model: prefer **vertical paging** via Digital Crown between one-screen-high pages (horizontal paging is considered "harder to navigate"); two-level pattern with `NavigationSplitView` (untitled source list; launch straight to detail with the selection initialized); `NavigationStack` only if neither fits, and hierarchical navigation must remember the last destination between launches.

### Example: crown-adjustable value with touch 🟡

```swift
import SwiftUI

// ═══════════════════════════════════════════════════════════════════
// WHEN: adjusting a continuous value (volume, timer, zoom) on the
// watch. The crown is primary but tap always exists.
// LIMITS: in a ScrollView crown scrolling is automatic; for custom
// values digitalCrownRotation is used with a touch equivalent.
// ═══════════════════════════════════════════════════════════════════

struct TimerAdjustment: View {
    @State private var minutes: Double = 10

    var body: some View {
        VStack(spacing: 8) {
            Text("\(Int(minutes)) min")
                .font(.title2.bold())
            // Touch equivalent: the crown is never the only path. ✅
            Stepper("", value: $minutes, in: 1...60, step: 5)
                .labelsHidden()
        }
        // The crown adjusts the value; the Stepper does the same with the finger. 🟡
        .digitalCrownRotation($minutes, from: 1, through: 60, by: 5,
                             sensitivity: .medium, isHapticFeedbackEnabled: true)
    }
}
```

## What NOT to do on such a small screen ✅/🟡

- ✅ **Don't port the iPhone screen**: multiple sections, 16 pt margins, bottom accessory bar — none of that is the Watch. One idea per screen, edge-to-edge.
- ✅ **No full-screen background color in long-duration views** (the HIG calls it out explicitly for workout and audio apps): OLED battery drain and it flattens the hierarchy.
- ✅ No deep hierarchies: short focused tasks, actionable notifications instead of deep navigation.
- ✅ No fixed widths: the supported range is **162–211 pt wide**; `maxWidth: .infinity` and reflow. No `List` inside `ScrollView` (double scroll, breaks the crown).
- ✅ Icon-only buttons almost always → **always with `.accessibilityLabel`**.
- ✅ Performance: don't decode phone-size images (downsample on load; the largest display is 422×514), no animations running in Always-On, no timer polling (use timelines/push/background refresh); complications and Smart Stack have **far less memory** than the app.
- ✅ No complex multi-step interactions; no horizontal scroll; no flows asking for more than a few seconds.

### Do / don't pairs — watchOS

1. **Tinted complications**
   - ✅ **DO:** design in monochrome thinking about tinting: use `.widgetAccentable()` only on the glyph that should tint ✅ and convey state with shape/text besides color.
   - ❌ **DON'T:** rely on color as the only channel (e.g. "red = bad"): on the face it renders tinted and the information is lost.

2. **Background on watchOS**
   - ✅ **DO:** `.containerBackground(for: .widget) { AccessoryWidgetBackground() }`: the native face background.
   - ❌ **DON'T:** a handmade translucent `Capsule`/`RoundedRectangle` or applying `.widgetAccentable()` to the container that also carries the background (it drags the background into the tint group and goes flat on device).

3. **Always-On**
   - ✅ **DO:** read `isLuminanceReduced`, redact the sensitive with `.privacySensitive()`, update at most every minute, dim with the system's dimming.
   - ❌ **DON'T:** your own dimming, animations running in the dimmed mode, or timer polling to refresh data.

4. **Navigation**
   - ✅ **DO:** Digital Crown for scroll/selection/adjustment with a touch equivalent; vertical paging between one-page screens; remember the last destination between launches.
   - ❌ **DON'T:** horizontal paging, deep hierarchies, or `List` inside `ScrollView` (double scroll breaking the crown).

5. **What fits in a complication**
   - ✅ **DO:** one datum and one mental action ("today's steps", "next appointment"): `Gauge` in `.accessoryCircular`, 2–3 lines in `.accessoryRectangular`.
   - ❌ **DON'T:** try to fit navigation, lists, or scroll on the face: the complication opens the app; it's not a mini-app.

See also: `ios.md`, `macos.md`, `../components/controls.md`, `../materials/liquid-glass.md`.
