# Typography

HIG typography rules + copy-pasteable SwiftUI and CSS examples.

**Verification legend:** ✅ = direct quote or rule from the HIG / official docs confirmed in ≥2 sources; 🟡 = consistently documented in ≥3 sources; ⚠️ = approximation or unverified.

## The system family ✅

- **SF Pro**: the interface (UI). Optical variants **Text** (≤19pt) and **Display** (≥20pt); in native code the variable font handles it on its own. ✅
- **SF Compact**: watch. **SF Mono**: code and data. **New York**: editorial serif. ✅

## Rules ✅

1. **Semantic styles, never fixed sizes.** `.body`, `.headline`, `.caption`… (SwiftUI) or `UIFont.preferredFont(forTextStyle:)`. Styles scale with **Dynamic Type** for free.
2. **Dynamic Type is never disabled.** Layouts must survive AX5 size without truncating: truncatable content (nav titles) truncates with dignity; readable content (body) grows and the layout flows.
3. **Minimum 11pt** for iOS system text; body 17pt.
4. **Line height ≥1.3×** the font size for body text.
5. **Line length 35–50 characters** on mobile; on iPad the text width is constrained (~672pt 🟡) instead of stretching full-screen.
6. **Left-aligned, never justified** — never center long paragraphs.
7. **Hierarchy through weight and color** before extreme size jumps.
8. 🟡 If you use a custom font: it must scale with Dynamic Type (`relativeTo:` / `UIFontMetrics`) — a font that doesn't scale is an accessibility violation. And use the system font for functional chrome (tabs, nav bars) even when the content uses a custom font.

## Key styles (iOS, default "Large" size) ✅

| Style | Size / line height |
|---|---|
| largeTitle | 34/41 |
| title1 (≡ title) | 28/34 |
| title2 | 22/28 |
| title3 | 20/25 |
| headline | 17/22, semibold |
| body | 17/22 |
| callout | 16/21 |
| subheadline | 15/20 |
| footnote | 13/18 |
| caption1 (≡ caption) | 12/16 |
| caption2 | 11/13 |

---

## SwiftUI

### Hierarchy of a reading screen ✅

```swift
import SwiftUI

// WHEN: a reading screen (article detail, card, onboarding).
// Rule: max 3–4 styles per screen; hierarchy is built with
// weight and color before extreme size jumps.
struct ArticleScreenView: View {
    var body: some View {
        ScrollView {
            VStack(alignment: .leading, spacing: 12) {

                // Kicker ("Technology", "New"): caption, semibold, secondary.
                Text("TECHNOLOGY")
                    .font(.caption)
                    .fontWeight(.semibold)
                    .foregroundStyle(.secondary)

                // The screen's headline: largeTitle (34pt). One per screen.
                Text("The chip that fits in your pocket")
                    .font(.largeTitle)
                    .fontWeight(.bold)

                // Metadata: subheadline (15pt), secondary color.
                Text("By Ada Lovelace · 5 min read")
                    .font(.subheadline)
                    .foregroundStyle(.secondary)

                Divider().padding(.vertical, 4)

                // Reading body: body (17pt), always left-aligned.
                Text("The latest generation of mobile processors doubles energy efficiency without growing in size.")
                    .font(.body)

                // Emphasis inside the body: headline (17pt semibold),
                // same size as body but with weight. Stands out without shouting.
                Text("More power, less battery spent")
                    .font(.headline)
                    .padding(.top, 8)

                // Photo caption or legal note: caption (12pt), tertiary color.
                Text("Photo: archive / Conceptual illustration.")
                    .font(.caption)
                    .foregroundStyle(.tertiary)
            }
            .padding()
        }
    }
}
```

### System designs: default, rounded, serif, monospaced ✅

```swift
import SwiftUI

// WHEN: typographic contrast without leaving the system family
// (zero custom fonts, zero bundle weight, Dynamic Type intact).
struct FontDesignsView: View {
    var body: some View {
        VStack(alignment: .leading, spacing: 20) {

            // Weight: hierarchy by thickness. .headline already brings semibold.
            Text("Bold headline")
                .font(.title2)
                .fontWeight(.bold) // avoid hairlines in UI text 🟡

            // Rounded: friendly tone. Wellness, kids, onboarding.
            Text("Welcome back")
                .font(.system(.title, design: .rounded, weight: .semibold))

            // Serif (New York): editorial tone. News, long reads.
            Text("Weekend chronicle")
                .font(.title2)
                .fontDesign(.serif)
                .fontWeight(.bold)

            // Monospaced (SF Mono): data and code. Timers, figures.
            Text("01:24:36")
                .font(.system(.title3, design: .monospaced, weight: .medium))

            // Monospaced digits in proportional font:
            // stops numbers from "jumping" as they change (prices, counters).
            Text("7 of 128 left")
                .font(.body)
                .monospacedDigit()

            // Back to SF Pro explicitly.
            Text("Back to SF Pro")
                .font(.system(.body, design: .default))
        }
        .padding()
    }
}
// Two ways to apply a design: `.fontDesign(.serif)` over an existing
// style, or `.font(.system(.title2, design: .rounded, weight: .bold))` ✅
```

### Text in fixed-size containers ✅

```swift
import SwiftUI

// WHEN: FIXED-size containers where the text can't grow
// (widgets, complications, compact 1–2 line labels).
// NEVER as an accessibility strategy: shrinking text takes away
// the large size the user chose on purpose.
struct CompactCardView: View {
    let headline: String

    var body: some View {
        VStack(alignment: .leading, spacing: 6) {
            // Up to 2 lines; if it still doesn't fit, shrinks to 80%
            // before truncating with "…".
            Text(headline)
                .font(.headline)
                .lineLimit(2)
                .minimumScaleFactor(0.8)

            Text("Updated 12 minutes ago")
                .font(.caption)
                .foregroundStyle(.secondary)
                .lineLimit(1)

            // Paths or URLs: middle truncation keeps start AND end.
            Text("/Documents/Reports/Q3-Results.pdf")
                .font(.caption)
                .foregroundStyle(.secondary)
                .lineLimit(1)
                .truncationMode(.middle) // "/Documents/…/Q3-Results.pdf"
        }
        .padding()
    }
}
// The system's order of action: first tightens tracking,
// then shrinks by the factor, finally truncates. ✅
// `lineLimit(nil)` = no limit (multi-line text by default). ✅
```

### Dynamic Type: free, keep it ✅

There is no "magic" snippet: any `Text` with a semantic style **scales on its own** when the user changes the size in Settings, including AX1–AX5 (body goes from 17pt to ~53pt in AX5).

```swift
import SwiftUI

// WHEN: always. This is the default behavior to preserve,
// not something to enable.
struct FreeDynamicTypeView: View {
    var body: some View {
        VStack(alignment: .leading, spacing: 8) {
            // Scales on its own with the user's setting. Zero extra code.
            Text("This text respects the size the user chose")
                .font(.body)

            // WHEN: your own font that ALSO scales (branding without
            // breaking accessibility). Declared "relative to" a style.
            Text("Headline in our brand font")
                .font(.custom("Georgia", size: 20, relativeTo: .title2))
        }
        .padding()
    }
}

// WHEN: spacing and icons that grow with the text
// (a fixed 16 padding looks cramped when the text is AX5).
struct ScaledMetricsView: View {
    @ScaledMetric(relativeTo: .body) private var separation: CGFloat = 16
    @ScaledMetric(relativeTo: .body) private var iconSize: CGFloat = 24

    var body: some View {
        HStack(spacing: separation) {
            Image(systemName: "checkmark.circle.fill")
                .font(.system(size: iconSize))
            Text("Task completed")
                .font(.body)
        }
    }
}
// ⚠️ If one specific layout breaks at huge sizes, you can clamp it
// with `.dynamicTypeSize(.large ... .accessibility3)` — last resort, not default.
```

---

## CSS (Apple-style web)

### The system font stack ✅

```css
/* WHEN: base of any web page or mockup with an Apple look.
   Uses the device's SF without downloading anything; on Windows/Android
   it degrades gracefully to the system sans. */
:root {
  --font-sans: -apple-system, BlinkMacSystemFont,
    "SF Pro Text", "SF Pro Display",
    "Helvetica Neue", Helvetica, Arial,
    system-ui, sans-serif;

  --font-mono: "SF Mono", SFMono-Regular,
    Menlo, Monaco, monospace;   /* WHEN: code, tabular figures */
}

body {
  font-family: var(--font-sans);
  -webkit-font-smoothing: antialiased; /* WHEN: macOS/iOS, refines rendering */
}
```

### Fluid scale with `clamp()` ✅

```css
/* WHEN: full-screen marketing/hero headlines, apple.com style.
   clamp(min, preferred, max): breathes with the viewport without media queries,
   with a floor and ceiling so it doesn't break at extremes. */
.hero {
  font-size: clamp(2.75rem, 1rem + 6vw, 5rem);
  font-weight: 600;                 /* Apple's hero is semibold, not black */
  letter-spacing: -0.025em;         /* negative tracking: display compresses */
  line-height: 1.05;                /* tight line height in display */
  text-wrap: balance;               /* ⚠️ progressive enhancement: balances lines */
}

/* WHEN: section titles. Scale less than the hero. */
.section-title {
  font-size: clamp(2rem, 1rem + 3vw, 3rem);
  font-weight: 600;
  letter-spacing: -0.02em;
  line-height: 1.1;
}

/* WHEN: reading body. Barely scales: legibility rules. */
.body {
  font-size: clamp(1rem, 0.95rem + 0.4vw, 1.125rem);
  line-height: 1.5;                 /* ≥1.3× for body; 1.5 is comfortable on web */
  max-width: 65ch;                  /* legible line length on desktop */
}

/* WHEN: kickers and labels ("New", sections, eyebrows). */
.kicker {
  font-size: 0.75rem;
  font-weight: 600;
  letter-spacing: 0.12em;
  text-transform: uppercase;
}
/* Tracking: -0.02em to -0.04em in display; 0.12em–0.2em in labels. ✅ */
/* On the web don't hand-replicate SF's optical tracking per style:
   in native code the variable font handles it. 🟡 */
/* ⚠️ In iOS Safari, inputs with font-size < 16px trigger auto-zoom on focus:
   keep forms at ≥16px. */
```

---

## Do / don't pairs

1. **System styles vs. fixed sizes** ✅
   - ✅ DO: `Text("Hi").font(.title)` — scales with Dynamic Type for free.
   - ❌ DON'T: `Text("Hi").font(.system(size: 28))` — pinned size, ignores the accessibility setting.

2. **Hierarchy by weight and color** ✅
   - ✅ DO: `.headline` (17 semibold) over `.body` (17 regular) for an elegant subhead.
   - ❌ DON'T: 5–6 styles per screen or jumping from `.caption` to `.largeTitle` with no steps in between.

3. **`minimumScaleFactor` is not accessibility** ✅
   - ✅ DO: only in fixed containers (widgets, 1–2 lines) with a high factor (≥0.8).
   - ❌ DON'T: shrink the reading body "so it fits" — readable content goes in a `ScrollView` and grows.

4. **Paragraphs left-aligned** ✅
   - ✅ DO: `.multilineTextAlignment(.leading)` (or the default).
   - ❌ DON'T: center multi-line blocks — the visual return point gets lost.

5. **Legibility floor: 11pt** ✅
   - ✅ DO: `.caption2` (11pt) as the minimum for system text.
   - ❌ DON'T: UI text below 11pt — if it doesn't fit, cut words, not points.

6. **On the web: `clamp()`, not fixed px** ✅
   - ✅ DO: `font-size: clamp(2rem, 1rem + 3vw, 3rem)` with a `rem` floor (respects the user's zoom).
   - ❌ DON'T: fixed `font-size: 48px` in headlines — breaks on unplanned viewports.

See also: `color.md`, `../system/tokens.md` (style table), `../system/accessibility.md`.
