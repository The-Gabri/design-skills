# Design tokens, Apple-style 🟡/⚠️

Quick-reference tokens for web mockups and code: spacing, radii, hex colors
(web/export only), and SF Symbols. Semantic names in native code, never
hardcoded hex.

Legend: ✅ = direct HIG/official-doc quote in ≥2 sources; 🟡 = consistent in
≥3 independent sources; ⚠️ = doubtful, single source, or version-dependent.

---

## 1. Spacing — 8pt grid ✅/🟡

- ✅ **Base 8pt grid**, 4pt fine step. Closed vocabulary: **4, 8, 12, 16,
  20, 24, 32** (48 for hero breathing room).
- ✅ **Horizontal margins**: 16pt iPhone, 20pt iPad (regular width). 🟡
- ✅ **Minimum touch target 44×44pt**; **8pt** minimum separation between
  adjacent tappable elements.
- ✅ Layout must fit the screen: no horizontal scroll or pinch-zoom for
  primary content.

SwiftUI — spacing vocabulary:

```swift
import SwiftUI

// WHEN: in any VStack/HStack/padding. No 5, 11, 13, or 17
// unless the system API asks for it. 🟡
enum Spacing {
    static let xs: CGFloat  = 4   // Minimum separation (icon + label)
    static let sm: CGFloat  = 8   // Related elements
    static let md: CGFloat  = 16  // Groups inside a section
    static let lg: CGFloat  = 24  // Between sections
    static let xl: CGFloat  = 32  // Between large blocks
    static let xxl: CGFloat = 48  // Hero breathing room / page separators
}

struct ProfileCard: View {
    var body: some View {
        VStack(alignment: .leading, spacing: Spacing.sm) {
            HStack(spacing: Spacing.md) {
                Image(systemName: "person.crop.circle.fill")
                    .font(.system(size: 56))
                VStack(alignment: .leading, spacing: Spacing.xs) {
                    Text("Alex").font(.headline)
                    Text("Member since 2026")
                        .font(.subheadline)
                        .foregroundStyle(.secondary)
                }
            }
            Divider().padding(.vertical, Spacing.sm)
        }
        .padding(Spacing.lg) // Multiples of 8 in outer padding too
    }
}
```

CSS — same scale for the web:

```css
/* WHEN: gap, padding, and margin for the whole web system. 🟡 */
:root {
  --space-1: 4px;  --space-2: 8px;  --space-3: 16px;
  --space-4: 24px; --space-5: 32px; --space-6: 48px;
}
.card {
  display: flex; flex-direction: column;
  gap: var(--space-3); padding: var(--space-4);
}
```

---

## 2. Radii 🟡/⚠️

- 🟡 **Scale**: 8 (sm) / 12 (md) / 16 (lg); prominent controls as capsule
  (`.capsule`).
- 🟡 **Concentric radii**: inner radius = outer radius − padding.
- 🟡 **Continuous squircle** (`.continuous`) on large surfaces; in iOS 26,
  `.rect(cornerRadius: .containerConcentric)` aligns radii with the
  container automatically.
- ⚠️ Single-source measurements (search field 10pt radius, sheet 10pt,
  grouped table 14pt): use with caution.

```swift
// WHEN: surfaces containing other elements with radius.
// .containerConcentric keeps the inner radius concentric with the
// outer container (iOS 26+). 🟡
struct ConcentricCard: View {
    var body: some View {
        VStack(spacing: 8) {
            Text("Content").padding(12)
        }
        .padding(16)
        .background(.quaternary, in: .rect(cornerRadius: 16))
        .clipShape(.rect(cornerRadius: .containerConcentric))
    }
}
```

---

## 3. Semantic colors ✅ / hex ⚠️ web-only

**Rule #1 ✅**: in native code always use **semantic names**
(`label`, `systemBackground`, `separator`, `systemBlue`…): the system
resolves them per light/dark appearance and Apple may change their values
per release. Color is never the only information channel (see
`../foundations/color.md` and *Differentiate Without Color* in
`accessibility.md`).

**Families ✅**: 4 label levels, 3 background levels × 2 sets
(ungrouped/grouped), `separator`/`opaqueSeparator`, fills.

**Reference hex (light → dark; ⚠️ web export only)**:

| Name | Light | Dark |
|---|---|---|
| systemBlue (action/tint) | #007AFF | #0A84FF |
| systemGreen (success) | #34C759 | #30D158 |
| systemRed (destructive) | #FF3B30 | #FF453A |
| systemOrange | #FF9500 | #FF9F0A |
| systemYellow | #FFCC00 | #FFD60A |
| systemPurple | #AF52DE | #BF5AF2 |
| systemPink | #FF2D55 | #FF375F |
| systemTeal | #5AC8FA | #64D2FF |
| systemIndigo | #5856D6 | #5E5CE6 |
| systemMint | #00C7BE | #00C7BE |
| systemCyan | #32ADE6 | #64D2FF |
| systemBrown | #A2845E | #AC8E68 |
| systemGray…Gray6 | #8E8E93…#F2F2F7 | #8E8E93…#1C1C1E |
| label | #000000 | #FFFFFF |
| secondaryLabel | rgba(60,60,67,.6) | rgba(235,235,245,.6) |
| tertiaryLabel | rgba(60,60,67,.3) | rgba(235,235,245,.3) |
| quaternaryLabel | rgba(60,60,67,.18) | rgba(235,235,245,.18) |
| systemBackground | #FFFFFF | #000000 |
| secondarySystemBackground | #F2F2F7 | #1C1C1E |
| tertiarySystemBackground | #FFFFFF | #2C2C2E |
| systemGroupedBackground | #F2F2F7 | #000000 |
| separator | rgba(60,60,67,.29) | rgba(84,84,88,.6) |
| opaqueSeparator | #C6C6C8 | #38383A |
| link | #007AFF | #0A84FF |

⚠️ `systemMint`/`systemCyan`/`systemBrown`, `quaternaryLabel`,
`tertiarySystemBackground`, and `opaqueSeparator`: verified in only 1–2
sources; the rest of the table in ≥4. System colors vary by OS version:
treat them as reference, not spec.

Semantics ✅: **one tint per screen**; blue = primary action/default tint,
red = destructive, green = success.

Quick dark-mode CSS:

```css
/* WHEN: Apple-style web without access to native semantics. 🟡 */
:root {
  --label: #000; --label-2: rgba(60,60,67,.6); --label-3: rgba(60,60,67,.3);
  --bg: #fff; --bg-2: #f2f2f7; --separator: rgba(60,60,67,.29);
  --accent: #007aff; --danger: #ff3b30;
}
@media (prefers-color-scheme: dark) {
  :root {
    --label: #fff; --label-2: rgba(235,235,245,.6); --label-3: rgba(235,235,245,.3);
    --bg: #000; --bg-2: #1c1c1e; --separator: rgba(84,84,88,.6);
    --accent: #0a84ff; --danger: #ff453a;
  }
}
```

Contrast ✅: 4.5:1 normal text, 3:1 large text (≥18pt or bold);
verify in both modes and with Increase Contrast.

---

## 4. Typography — pointer and link

The full scale, emphasized weights, tracking, and Dynamic Type are in
`../foundations/typography.md` (don't duplicate here).

Quick notes:
- ✅ System styles at the "Large" size: largeTitle 34/41,
  title1 28/34, title2 22/28, title3 20/25, headline 17/22 semibold,
  body 17/22, callout 16/21, subheadline 15/20, footnote 13/18,
  caption1 12/16, caption2 11/13. **Below 11pt there is no iOS system
  text.** 🟡
- 🟡 macOS equivalents for mockups: largeTitle 26, title1 22, title2 17,
  title3 15, headline 13 bold, body 13, callout 12, subheadline 11,
  footnote/caption1 10, caption2 10 medium (2 sources: use with caution).
- 🟡 Families: SF Pro (Display/Text), SF Compact, SF Mono, New York (serif).
  Web stack:
  ```css
  --font: -apple-system, BlinkMacSystemFont, "SF Pro Text", "SF Pro Display",
          "Helvetica Neue", system-ui, sans-serif;
  --font-mono: "SF Mono", SFMono-Regular, Menlo, Monaco, monospace;
  ```
- 🟡 On the web: **don't self-host SF Pro** (Apple license: only on Apple
  platform software); the system stack resolves SF automatically on Apple
  devices.

---

## 5. SF Symbols ✅/🟡

- ✅ **Prefer SF Symbols** (6,900+ in v7) over custom glyphs: they match the
  adjacent text's weight, scale with Dynamic Type, and adapt to color modes
  for free. They ship in the system, not in the app.
- ✅ **The symbol's weight follows the adjacent text** (inherited from the
  nearby font weight); **9 weights × 3 scales** (small/medium/large).
  One consistent scale inside the same container (don't mix `.imageScale`
  values in the same row).
- ✅ **Outline in toolbars, filled in tab bar**: *"a mobile tab bar prefers
  the fill variant, whereas a toolbar takes the outline variant"* (HIG
  quote, 4+ sources). Extended rule: fill = selection/emphasis (active tab,
  swipe actions), outline = next to text (toolbars, lists).
- ✅ Rendering modes: **monochrome, hierarchical** (layered opacities),
  **palette** (per-layer colors), **multicolor** (Apple's intrinsic colors).
- ✅ Symbols align to the text baseline, scale with Dynamic Type, and mirror
  in RTL. Keep their conventional meaning: don't use a known symbol for
  something else (share = share, not "send").
- 🟡 House rule: interface symbol before custom icon; if there's no fitting
  symbol, build the custom one from the SF Symbols variable template
  (export Ultralight/Regular/Black for interpolation). **Every icon-only
  control carries an `accessibilityLabel`.**
- 🟡 New in v7: Draw On/Off, Variable Draw, gradients, improved Magic
  Replace; animations `.bounce`, `.pulse`, `.variableColor`, `.replace`.

```swift
import SwiftUI

// WHEN: any interface icon. The symbol inherits weight and scale
// from the text context: no need to "adjust it by hand". ✅
struct SymbolExamples: View {
    var body: some View {
        VStack(spacing: 16) {
            // 1. Weight follows the adjacent text ✅
            Label("Favorites", systemImage: "heart.fill")
                .font(.headline) // the symbol inherits semibold automatically

            // 2. One scale per container: don't mix imageScale ✅
            HStack {
                Image(systemName: "wifi").imageScale(.medium)
                Image(systemName: "battery.100").imageScale(.medium)
            }
            .font(.body)

            // 3. Hierarchical rendering: layers with differentiated opacities ✅
            Image(systemName: "cloud.sun.fill")
                .symbolRenderingMode(.hierarchical)
                .font(.largeTitle)

            // 4. Animated symbol reacting to a state change 🟡
            Image(systemName: "bell.badge")
                .symbolEffect(.bounce, value: hasAlert)
                .font(.title2)
        }
    }
    @State private var hasAlert = false
}

// WHEN: navigation chrome. Tab bar = filled (emphasis/selection),
// toolbar = outline (next to actions). ✅
struct Chrome: View {
    var body: some View {
        TabView {
            Text("Home").tabItem {
                Label("Home", systemImage: "house.fill") // filled ✅
            }
            Text("Settings").tabItem {
                Label("Settings", systemImage: "gearshape.fill") // filled ✅
            }
        }
        .toolbar {
            ToolbarItem(placement: .primaryAction) {
                Button("New", systemImage: "square.and.pencil") { // outline ✅
                }
            }
        }
    }
}
```

---

## Do / don't pairs

**D1 — Colors: semantic vs. hex ✅**
- ✅ **Do:** `foregroundStyle(.secondary)` / `.tint(.blue)` in native code; hex
  only in web export with light/dark custom props.
- ❌ **Don't:** hardcoded `Color(red: 0, green: 0.48, blue: 1)`: breaks in
  dark mode and Apple may change the value per release.

**D2 — Spacing: closed scale vs. eyeballed values ✅**
- ✅ **Do:** multiples of 8 (4 / 8 / 16 / 24 / 32 / 48).
- ❌ **Don't:** 5, 11, 13, 21 "because it looked fine on my screen".

**D3 — SF Symbols: context weight vs. custom icon ✅**
- ✅ **Do:** `Image(systemName:)` inside a `Label` or with the adjacent
  text's `.font`; outline in toolbars, filled in tab bar.
- ❌ **Don't:** draw your own "share"/"delete" icon or pin the symbol's
  weight by hand when the adjacent text already defines it.

**D4 — Radii: concentric vs. eyeballed radii 🟡**
- ✅ **Do:** `.rect(cornerRadius: .containerConcentric)` (iOS 26+) or
  inner = outer − padding.
- ❌ **Don't:** the same radius on container and inner element: the inner
  one looks tighter and the card "looks wrong" without knowing why.

**D5 — Contrast ✅**
- ✅ **Do:** verify 4.5:1 / 3:1 in light, dark, and with Increase Contrast.
- ❌ **Don't:** tertiary-gray text on secondary-gray background in dark mode
  (the pair that fails most audits).

See also: `../foundations/typography.md`, `../foundations/color.md`,
`layout.md` (grid and safe areas in context), `accessibility.md`.
