# iOS ✅/🟡

> **Platform rule:** don't replicate one platform's UI on another — adapt the intent to each platform's strengths. ✅

## iOS ✅/🟡

- ✅ **Portrait-first**, one-handed use: primary actions within thumb reach (lower zone); the nav bar up top is for navigation and secondary actions.
- ✅ Safe areas for notch, **Dynamic Island** (~59 pt of status bar on those devices), and home indicator (34 pt bottom inset). Backgrounds may extend under bars; interactive content never sits under them.
- ✅ **Tab bar** (2–5 tabs, navigation only) and **navigation stack** (drill-down, large titles on root screens) as base patterns. See `../components/navigation.md`.
- ✅ **System share sheet** for sharing; **system pickers** for dates and options.
- ✅ Permissions **in context** (at the point of use, not at app launch), with clear purpose strings; degrade gracefully when denied and offer a link to Settings.
- 🟡 iOS 26: functional chrome goes in Liquid Glass; system bars adopt glass on their own when recompiling with Xcode 26. Don't stack custom glass over system glass.

## iPadOS ✅/🟡

- ✅ **Sidebar** (`NavigationSplitView`) as the primary navigation in regular width; the tab bar lives near the top and can become a sidebar (`sidebarAdaptable`).
- ✅ **Multitasking**: Split View and Slide Over — the app must work at all widths with no hardcoded geometries.
- ✅ **Pointer and keyboard**: hover support, keyboard shortcuts, and drag & drop between apps.
- ✅ **Popovers** instead of sheets for light options anchored to a control.
- 🟡 The iPad allows tab bar customization (add/remove/reorder); keep ≤5 tabs by default.

## Widgets ✅/🟡

Widgets **are not mini-apps** ✅: glanceable information, not complex controls. Buttons/toggles only backed by App Intents (iOS 17+) ✅.

### The limits that drive the design 🟡

- ✅ **No realtime updates**: "Widgets periodically refresh their information but don't support continuous, real-time updates." For realtime, the HIG literally says: "Offer Live Activities to show real-time updates."
- ✅ The system decides the refresh cadence (the timeline proposes; iOS schedules by battery and usage). For date/time, use the system's automatic feature instead of spending refresh budget.
- ✅ The view can't touch the network or use timers: everything painted must already be computed inside the entry.
- 🟡 Text with text elements (never rasterize text), **≥11 pt**; Dynamic Type from **Large up to AX5**.
- 🟡 Data changes: animations of up to **~2 seconds** to signal new information.
- ✅ In iOS 17+, the system manages margins — don't add your own; corner radius with `ContainerRelativeShape` (never hardcode radii).
- ✅ Background with `.containerBackground(for: .widget)` so the system can substitute it (glass in tinted/clear, monochrome where needed).
- ✅ System families: `.systemSmall` (2×2, one tap target), `.systemMedium` (4×2), `.systemLarge` (4×4; iPad: `.systemExtraLarge` 8×4 — extra large **doesn't** exist on iPhone). Lock Screen accessories: circular, rectangular, inline (only ONE tap target).

### Deep links 🟡

- ✅ **Tapping outside a button opens the app at the exact location**: "Ensure that a widget interaction opens your app at the right location. Deep link to details and actions that directly relate to the widget's content, and don't make people navigate to the relevant area in the app." Design the deep link's destination, not just "open the app".
- ✅ Gallery description: succinct, starts with an action verb, no "This widget shows…"; group the sizes with a single description.

### Example: widget with deep link 🟡

```swift
import WidgetKit
import SwiftUI

// ═══════════════════════════════════════════════════════════════════
// WHEN: "at a glance" content that changes slowly — the day's summary,
// next appointment, habit streak, today's weather.
// LIMITS: no realtime (the system rations refreshes); the view
// can't touch the network or use timers: everything you paint must
// already be computed inside the entry. On tap, the widget can only
// open the app (not run logic). 🟡
// ═══════════════════════════════════════════════════════════════════

// 1. The entry: just enough data to paint a "photo" of the widget. 🟡
struct HabitEntry: TimelineEntry {
    let date: Date          // Moment when WidgetKit starts showing this entry.
    let habitsDone: Int     // Already computed: the view can't fetch anything.
    let habitsTotal: Int
}

// 2. The provider: decides WHAT shows and WHEN. 🟡
struct HabitProvider: TimelineProvider {
    // Used before real data exists: cheap and generic.
    func placeholder(in context: Context) -> HabitEntry {
        HabitEntry(date: Date(), habitsDone: 2, habitsTotal: 5)
    }

    // Gallery preview: answers fast, with sample data if needed.
    func getSnapshot(in context: Context, completion: @escaping (HabitEntry) -> Void) {
        completion(HabitEntry(date: Date(), habitsDone: 3, habitsTotal: 5))
    }

    // Pre-computes future entries and asks for the next batch with a reload policy.
    func getTimeline(in context: Context, completion: @escaping (Timeline<HabitEntry>) -> Void) {
        let now = Date()
        // One entry per hour for 6 h: the widget "changes" without spending
        // the system's reload budget. 🟡
        let entries = (0..<6).compactMap { offset in
            Calendar.current.date(byAdding: .hour, value: offset, to: now)
                .map { HabitEntry(date: $0, habitsDone: 3, habitsTotal: 5) }
        }
        let reloadAt = Calendar.current.date(byAdding: .hour, value: 6, to: now)!
        // .after(date): asks for another batch no earlier than that date.
        // Alternatives: .atEnd (after the last entry passes) and .never
        // (only when YOU call WidgetCenter). 🟡
        completion(Timeline(entries: entries, policy: .after(reloadAt)))
    }
}

// 3. The view: one layout branch per family. 🟡
struct HabitView: View {
    @Environment(\.widgetFamily) private var family
    let entry: HabitEntry

    var body: some View {
        switch family {
        case .systemSmall:
            VStack(alignment: .leading, spacing: 4) {
                Text("\(entry.habitsDone)/\(entry.habitsTotal)")
                    .font(.largeTitle.bold())
                Text("habits today")
                    .font(.caption)
                    .foregroundStyle(.secondary)
            }
        default: // .systemMedium: room for the progress bar
            VStack(alignment: .leading, spacing: 8) {
                Text("Today's habits")
                    .font(.headline)
                ProgressView(value: Double(entry.habitsDone),
                             total: Double(entry.habitsTotal))
                Text("\(entry.habitsDone) of \(entry.habitsTotal) completed")
                    .font(.caption)
                    .foregroundStyle(.secondary)
            }
        }
    }
}

// 4. Widget declaration and bundle. 🟡
struct HabitWidget: Widget {
    let kind = "HabitWidget" // Stable ID: never change it after shipping. ✅

    var body: some WidgetConfiguration {
        StaticConfiguration(kind: kind, provider: HabitProvider()) { entry in
            HabitView(entry: entry)
                // Mandatory background in iOS 17+; without it the widget comes out blank. ✅
                .containerBackground(for: .widget) { Color(.systemBackground) }
                // Touching the widget opens the app at this URL (one widgetURL per family). 🟡
                .widgetURL(URL(string: "habits://today"))
        }
        .configurationDisplayName("Today's habits")
        .description("Your daily progress at a glance.")
        .supportedFamilies([.systemSmall, .systemMedium])
        // Disables the system's margins: you draw them. ✅
        // Drop the modifier if you prefer system-managed margins.
        .contentMarginsDisabled()
    }
}

@main
struct HabitsBundle: WidgetBundle {
    var body: some Widget {
        HabitWidget()
    }
}
```

**Manual reload from the app** (when data changes, e.g. the user checks a habit) ✅:
```swift
import WidgetKit
WidgetCenter.shared.reloadTimelines(ofKind: "HabitWidget")
```

**Receiving the deep link in the app** 🟡: register the `habits://` scheme in the Info.plist and handle it with `.onOpenURL { url in … }` in your `App`.

### Do / don't pairs — widgets

1. **Layout per family**
   - ✅ **DO:** one layout branch per family (`switch` on `widgetFamily`): big number in `.systemSmall`, progress detail in `.systemMedium`. Each family has its density.
   - ❌ **DON'T:** one "works for everything" layout squeezed with `scaleEffect` or tiny fonts: illegible when small, empty when large.

2. **Deep links**
   - ✅ **DO:** one `.widgetURL` per family — the whole card opens a clear destination (`habits://today`).
   - ❌ **DON'T:** nest several `.widgetURL`s in the hierarchy or use `Link` in `.systemSmall` or accessory families: tap areas get ambiguous and `Link` is ignored on the Lock Screen.

3. **Widget background**
   - ✅ **DO:** `.containerBackground(for: .widget)` on the root view (mandatory in iOS 17+; without it, white in the Smart Stack).
   - ❌ **DON'T:** fake the background with your own `RoundedRectangle`: it breaks the system's clipping and the tinted mode.

4. **Data freshness**
   - ✅ **DO:** pre-compute many future entries (one per hour) and reload with `.after(date)` or `.atEnd`: the widget "changes" without spending the reload budget. If it's looked at more than it can update, show "last updated". 🟡
   - ❌ **DON'T:** ask for a reload every few minutes expecting realtime: the system rations reloads and the widget will go stale anyway. For realtime, Live Activity.

## Live Activities ✅/🟡

For **events with active progress that are time-sensitive**: deliveries, sports, timers, trips ✅. Not for: music playing (that's the Now Playing framework's), normal notifications, marketing, or background processes that don't matter minute-by-minute 🟡.

- ✅ Maximum **8 hours** active; then it moves to the Lock Screen as static. In total: up to **4 additional hours** on the lock screen — **12 hours** max visible.
- ✅ Three Dynamic Island presentations: **compact** (leading + trailing, when only ONE is active), **minimal** (circular/oval view, when SEVERAL are active), **expanded** (leading, trailing, center, bottom; appears on long-press of compact or minimal; supports interactive buttons since iOS 17+).
- ✅ Gestures: tap compact/minimal → opens the app (deep link); long-press → expanded view.
- ✅ Also appear in **StandBy** and the watchOS **Smart Stack** — legibility at a distance is mandatory.
- ✅ Own sandbox: **no network or location access**. Updates arrive via ActivityKit in the app or ActivityKit push. **Data limit: static + dynamic combined ≤ 4 KB**.
- ✅ System-limited updates: push notifications for realtime.
- 🟡 Golden rule: only start when the app is in the foreground and after a discrete user action (starting an order, a workout, a timer). The user can silence or disable it — it's a convenience, not a guarantee.
- 🟡 Images no larger than the presentation (e.g. the minimal one ≤ 45×36.67 pt); if exceeded, the system may fail to start it. Only essential data, no clutter. Alert updates: only for essential news, never duplicating push.
- Every tap target deep-links to the app's relevant screen. ✅

### Example: order Live Activity 🟡

```swift
import ActivityKit
import WidgetKit
import SwiftUI

// ═══════════════════════════════════════════════════════════════════
// WHEN: in-progress events the user started — an order, a trip, a
// workout, a game's score.
// LIMITS: max 8 h active (the system closes it on its own) and up to
// 12 h visible on the lock screen; attributes + state ≤ 4 KB; remote/
// local updates are budget-rationed; the activity lives in its own
// sandbox: no network or location of its own.
// It can only start with the app in the foreground. 🟡
// ═══════════════════════════════════════════════════════════════════

// 1. The attributes: what's FIXED about the event goes outside; what CHANGES, inside ContentState. 🟡
struct OrderAttributes: ActivityAttributes {
    struct ContentState: Codable, Hashable {
        var stage: String         // "In the kitchen", "On its way", "Delivered"
        var minutesLeft: Int
    }
    var orderNumber: String      // Fixed for the whole order
    var store: String
}

// 2. The presentation: lock screen + Dynamic Island (compact, minimal, expanded). 🟡
struct OrderLiveActivity: Widget {
    var body: some WidgetConfiguration {
        ActivityConfiguration(for: OrderAttributes.self) { context in
            // Lock screen / banner
            HStack {
                VStack(alignment: .leading) {
                    Text("Order \(context.attributes.orderNumber)")
                        .font(.headline)
                    Text("\(context.state.stage) · \(context.state.minutesLeft) min")
                        .font(.subheadline)
                        .foregroundStyle(.secondary)
                }
                Spacer()
                Image(systemName: "takeoutbag.and.cup.and.straw.fill")
                    .font(.title2)
            }
            .activityBackgroundTint(.black.opacity(0.6)) // ✅
        } dynamicIsland: { context in
            DynamicIsland {
                // Expanded (on long-press): optional leading/trailing/center/bottom regions
                DynamicIslandExpandedRegion(.leading) {
                    Text(context.state.stage).font(.headline)
                }
                DynamicIslandExpandedRegion(.trailing) {
                    Text("\(context.state.minutesLeft) min").font(.title2.bold())
                }
                DynamicIslandExpandedRegion(.bottom) {
                    ProgressView(value: Double(context.state.minutesLeft), total: 30)
                }
            } compactLeading: {   // Compact pill, left side
                Image(systemName: "takeoutbag.and.cup.and.straw.fill")
            } compactTrailing: {  // Compact pill, right side: the key datum
                Text("\(context.state.minutesLeft)m")
                    .font(.caption.bold())
            } minimal: {          // When the island is busy with another activity
                Image(systemName: "takeoutbag.and.cup.and.straw.fill")
            }
        }
    }
}
```

**Lifecycle from the app** (start → update → end) ✅:
```swift
import ActivityKit

// Only after a user action and with the app in the foreground. ✅
func startOrder(number: String, store: String) async {
    guard ActivityAuthorizationInfo().areActivitiesEnabled else { return } // The user can disable them. ✅
    let attributes = OrderAttributes(orderNumber: number, store: store)
    let state = OrderAttributes.ContentState(stage: "In the kitchen", minutesLeft: 25)
    let content = ActivityContent(
        state: state,
        staleDate: Date().addingTimeInterval(300), // "this data expires in 5 min" ✅
        relevanceScore: 50                          // Breaks ties if there are several activities. ✅
    )
    do {
        _ = try Activity.request(attributes: attributes, content: content) // ✅
    } catch {
        print("Couldn't start the Live Activity: \(error)")
    }
}

func updateOrder(_ activity: Activity<OrderAttributes>, stage: String, minutes: Int) async {
    let state = OrderAttributes.ContentState(stage: stage, minutesLeft: minutes)
    await activity.update( // ✅
        ActivityContent(state: state, staleDate: Date().addingTimeInterval(300))
    )
}

func endOrder(_ activity: Activity<OrderAttributes>) async {
    let final = OrderAttributes.ContentState(stage: "Delivered", minutesLeft: 0)
    // .immediate removes it now; .default leaves it a while; .after(date) leaves it until then. ✅
    await activity.end( // ✅
        ActivityContent(state: final, staleDate: nil),
        dismissalPolicy: .immediate
    )
}
```

**Assembly notes:**
- The UI lives in the widgets extension, not in the app. 🟡
- Declare that the app supports Live Activities in the Info.plist (`NSSupportsLiveActivities`). ⚠️ (configuration key; confirm currency in the official docs)
- For countdowns that "tick" on their own without spending updates, the native way is `Text(timerInterval:)`. ⚠️
- Buttons inside the activity (iOS 17+): `Button(intent:)` with a `LiveActivityIntent`. ✅ (name and `Button(intent:)` usage; exact members unverified)

### Do / don't pairs — Live Activities

1. **Start**
   - ✅ **DO:** start only after a discrete user action and with the app in the foreground (`Activity.request` inside `do/catch`, checking `areActivitiesEnabled` first).
   - ❌ **DON'T:** start it in the background, at app open "just in case", or assume it can always start: the user can disable them per app and there's a max of simultaneous activities (documented as 5 per app. ⚠️).

2. **State modeling**
   - ✅ **DO:** fixed things (order no., teams) in `ActivityAttributes`; what changes (stage, score) in `ContentState`, small and `Codable`.
   - ❌ **DON'T:** put everything in `ContentState` or leave the activity hanging when the event ends: always end with `end(_:dismissalPolicy:)` choosing `.immediate`, `.default`, or `.after(date)`.

3. **Updates**
   - ✅ **DO:** realistic `staleDate` on each `ActivityContent` (the system marks content as stale) and `relevanceScore` to break ties in the Dynamic Island.
   - ❌ **DON'T:** push an update per second "so the timer moves": the budget is rationed; for countdowns use the native tick (`Text(timerInterval:)`. ⚠️).

## StandBy ✅/🟡

The widget **scales to fill the Lock Screen**; design test: legible at a distance (~6 feet / 1.8 m). ✅

- ✅ "Limit usage of rich images or color to convey meaning in StandBy. Instead, make use of the additional space by scaling up and rearranging text so people can glance at the widget content from a greater distance." And: "don't use background colors for your widget when it appears in StandBy" — use `containerBackground(for: .widget)` so the system removes the background.
- ✅ In dim ambient light, the system applies a **monochromatic red tint** (automatic night Red Tint mode); SF Symbols and text re-tint well, but gradients/photos as backgrounds get clipped. Design and test the red mode.
- ✅ In StandBy widgets render with **background removed** (vibrant rendering mode: desaturates text/images, vibrant effect over the background).
- 🟡 Practical rules: hero number ≥ 56 pt, high contrast (white on black or accent on dark), **no interactive buttons** in StandBy (tap opens the app); design the small size so it works in the stacked carousel. Supporting StandBy guarantees the widget works well in CarPlay.

### Do / don't pairs — StandBy

1. **Distance design**
   - ✅ **DO:** scale text up and rearrange it for distance reading; high white-on-black contrast; hero number ≥ 56 pt.
   - ❌ **DON'T:** rely on rich images or colors to convey meaning: they're lost in the night red tint.

2. **Interactivity**
   - ✅ **DO:** assume any tap opens the app (deep link) and the widget shows without its background.
   - ❌ **DON'T:** put interactive buttons or custom background colors in StandBy.

See also: `../components/navigation.md`, `../components/presentation.md`, `macos.md`, `watchos.md`.
