# Accessibility, haptics, and sound ✅/🟡

Accessibility **is not an add-on**: it's designed from the start. It's one
of the 8 principles (Responsibility).

Legend: ✅ = direct HIG/official-doc quote in ≥2 sources; 🟡 = consistent in
≥3 independent sources; ⚠️ = doubtful or single source.

---

## 1. VoiceOver ✅

- ✅ **Every interactive element has a name**: icon-only buttons need an
  `accessibilityLabel` (`.help` or identifiers are not substitutes). Labels
  as nouns, hints as actions.
- ✅ `accessibilityHint` for non-obvious actions; group with
  `accessibilityElement(children: .combine)` where applicable.
- ✅ Logical reading order; focus that **returns** after closing a modal;
  announcements for async completions/failures.
- ✅ Hide the decorative from VoiceOver (`.accessibilityHidden(true)` on
  icons that duplicate adjacent text).
- ✅ Complex app gestures need an equivalent `accessibilityAction`.
- ✅ No color-only information; decorative images hidden from accessibility.
- ✅ Test with Accessibility Inspector on real hardware.

### E1 — VoiceOver labels and grouping ✅

**When to use it:** on EVERY interactive control, especially icon-only
ones. Without a label, VoiceOver reads the symbol name or "button", which
says nothing.

```swift
import SwiftUI

struct PlayerBar: View {
    var body: some View {
        HStack(spacing: 24) {
            // ✅ Icon-only button: needs accessibilityLabel.
            Button {
                play()
            } label: {
                Image(systemName: "play.fill")
                    .accessibilityHidden(true) // The label says it all
            }
            .accessibilityLabel("Play")            // Noun: what it is
            .accessibilityHint("Starts playback")  // Action: what it does

            // ✅ Group what reads as a unit: "Episode 12,
            // 3 of 10, 2 minutes" in one announcement instead of three.
            VStack(alignment: .leading) {
                Text("Episode 12")
                Text("3 of 10 · 2 min")
                    .font(.caption)
                    .foregroundStyle(.secondary)
            }
            .accessibilityElement(children: .combine)

            // ✅ Complex gestures (e.g. swipe) with an equivalent action.
            Button("Dismiss", action: dismiss)
                .accessibilityAction(named: "Archive") { archive() }
        }
    }
}
```

---

## 2. Dynamic Type ✅/🟡

- ✅ **All text uses system text styles, never hardcoded sizes**; the system
  scales size, leading, and tracking.
- ✅ 12 content size categories: 7 standard (xSmall → xxxLarge) + 5
  accessibility sizes (AX1–AX5).
- 🟡 Body scales ~**310% at AX5** vs. default (non-linear curve); Body goes
  from ~14pt (xSmall) to ~23pt (xxxLarge), up to ~53pt at AX5. **Forbidden to
  disable Dynamic Type** or pin sizes that prevent scaling.
- ✅ Test layouts at xSmall **and** AX5; allow elegant wrap/truncation;
  provide **Large Content Viewer** for fixed-size chrome (tab/tool/nav bar).

### E2 — Surviving AX5 ✅

**When to use it:** in any layout with text. If the text may truncate at
AX5, the layout must flow, not break.

```swift
import SwiftUI

struct NewsRow: View {
    var body: some View {
        HStack(alignment: .top, spacing: 12) {
            Image(systemName: "newspaper")
                .font(.title2)
            VStack(alignment: .leading, spacing: 4) {
                // ✅ System style: scales with Dynamic Type. The stack
                // grows and text wraps; nothing truncates at AX5.
                Text("News headline")
                    .font(.headline)
                Text("Two-line summary that can get very long")
                    .font(.subheadline)
                    .foregroundStyle(.secondary)
            }
        }
        .padding(16)
    }
}

// 🟡 Custom spacing that also scales: @ScaledMetric.
struct MetricCard: View {
    @ScaledMetric(relativeTo: .body) private var separation = 16

    var body: some View {
        VStack(spacing: separation) {
            Text("Title").font(.title3)
            Text("Body").font(.body)
        }
    }
}

// ✅ Fixed chrome (tab/tool bar) with expandable content: Large Content Viewer.
struct CompactButton: View {
    var body: some View {
        Button("Share", systemImage: "square.and.arrow.up") { share() }
            .labelStyle(.iconOnly)
            .accessibilityShowsLargeContentViewer()
            .accessibilityLargeContentViewer {
                Label("Share", systemImage: "square.and.arrow.up")
            }
    }
}
```

On the web: don't pin `px` in body; use `rem`/`em` and let the system's text
size setting scale (or media queries by content size when critical). 🟡

---

## 3. Reduce Motion / Transparency / Increase Contrast ✅/🟡

### Reduce Motion ✅
- ✅ No parallax, zoom, blur transitions, or elastic overshoot; substitute
  with a brief crossfade (~100ms). Direct manipulation (1:1 drag)
  **keeps** working — only decorative autonomous motion is removed.
- On the web: `prefers-reduced-motion`. Substitution table and opt-in
  pattern in `motion.md` §6 (slide → crossfade, error shake → static
  style + move focus, skeleton shimmer → static blocks).

### Reduce Transparency ✅
- ✅ Offer an **opaque fallback** for any visual depending on
  translucency/blur (**Liquid Glass materials included**): explicit
  `accessibilityReduceTransparency` branch.
- On the web: `prefers-reduced-transparency`.

### Increase Contrast ✅
- ✅ Strengthen borders and separation when `colorSchemeContrast == .increased`;
  system components adapt, customs need their own branch.
- ✅ Verify semantic colors and materials in both modes.

### Bold Text and Differentiate Without Color ✅
- ✅ **Bold Text**: don't assume light weights on critical text.
- ✅ **Differentiate Without Color**: state is **never** communicated with
  color alone — add an icon, shape, or label (see
  `../foundations/color.md`).

### E3 — Accessibility branches in SwiftUI ✅

**When to use it:** in any visual depending on transparency, blur, or fine
contrast. Three explicit branches, not one happy path.

```swift
import SwiftUI

struct CriticalCard: View {
    @Environment(\.accessibilityReduceTransparency) private var reduceTransparency
    @Environment(\.colorSchemeContrast) private var contrast

    var body: some View {
        VStack(alignment: .leading, spacing: 8) {
            HStack(spacing: 8) {
                // ✅ State with icon + text, never color alone.
                Image(systemName: statusSymbol)
                Text(statusText)
                    .font(.headline)
            }
            .foregroundStyle(statusColor)
            Text("Status detail")
                .font(.subheadline)
                .foregroundStyle(.secondary)
        }
        .padding(16)
        // ✅ With Reduce Transparency: opaque background instead of material.
        .background(
            reduceTransparency
                ? AnyShapeStyle(.background)
                : AnyShapeStyle(.regularMaterial),
            in: RoundedRectangle(cornerRadius: 12)
        )
        // ✅ With Increase Contrast: a border that separates even if the background fails.
        .overlay(
            RoundedRectangle(cornerRadius: 12)
                .stroke(contrast == .increased ? .primary : .clear, lineWidth: 1)
        )
    }
}

/* In CSS: */
@media (prefers-reduced-transparency: reduce) {
  .glass { background: var(--bg-2); backdrop-filter: none; }
}
```

---

## 4. Haptics ✅/🟡

- ✅ Use the **documented system patterns**: `.success`, `.warning`,
  `.error`, `.selection`, `.impact`.
- ✅ Haptics **accompany** meaningful state changes (success on completion),
  not every tap. **Never haptics as the only channel**: always with visual
  feedback. Some people can't perceive them → equivalent visual/audible cue.
- ✅ Respect the user's haptics setting; the app must stay usable without
  haptics or sound.
- 🟡 In iOS 26, `.interactive()` on glass adds press scaling, bounce, and
  shimmer from the touch point — integrated tactile-visual feedback.
- ⚠️ Intensity rules: match intensity to the action's significance
  (consensus pattern, no direct HIG quote).

### E4 — Haptics with meaning ✅

**When to use it:** state changes the user should *feel*
(completing, error, crossing a threshold). Never on every tap.

```swift
import SwiftUI

struct SaveAction: View {
    @State private var saved = false

    var body: some View {
        Button(saved ? "Saved" : "Save") {
            save()
            saved = true
            // ✅ Success notification: accompanies the visual change
            // (the button changes state). Doesn't replace the UI.
            let generator = UINotificationFeedbackGenerator()
            generator.notificationOccurred(.success)
        }
        .sensoryFeedback(.success, trigger: saved) // ✅ iOS 17+: declarative,
                                                   // respects the system setting
    }
}

// ✅ Selection in pickers/segments: .selection (light, frequent).
// ✅ Physical impact: .impact(.medium) when dropping a drag in place.
```

---

## 5. Sound ✅/🟡

- ✅ Use sound sparingly and only on significant state changes.
- ✅ Never sound as the only information channel.
- ✅ Respect silent mode / system settings; no audio autoplay the user can't stop.
- On the web: no audio autoplay without prior interaction.

---

## Quick checklist ✅

1. Every interactive element has a VoiceOver name.
2. Survives AX5 without truncating.
3. Contrast ≥4.5:1 (3:1 large text).
4. Reduce Motion and Reduce Transparency respected.
5. Haptics/sound never alone.
6. Destructive actions confirmable without color (clear verb + confirm dialog).

## Do / don't pairs

**D1 — VoiceOver ✅**
- ✅ **Do:** `accessibilityLabel` on every icon-only button; group with
  `.combine` what reads as a unit; focus that returns after closing the
  modal.
- ❌ **Don't:** rely on `.help` or the symbol name ("button",
  "image") as a label; leave decorative icons visible to VoiceOver.

**D2 — Dynamic Type ✅**
- ✅ **Do:** system text styles + `@ScaledMetric` for custom spacing; test
  at xSmall and AX5.
- ❌ **Don't:** hardcoded sizes, `minimumScaleFactor` as the general
  strategy to "make it fit" (shrinks to illegibility), or disabling
  Dynamic Type.

**D3 — Reduce Motion ✅**
- ✅ **Do:** brief crossfade (~100ms) preserving feedback; direct
  manipulation still 1:1.
- ❌ **Don't:** abrupt cuts that disorient, or keeping parallax "because it
  looks good".

**D4 — Differentiate Without Color ✅**
- ✅ **Do:** state = icon + label + color (color is redundant, not the
  message).
- ❌ **Don't:** a red/green dot as the sole error/success indicator.

**D5 — Haptics ✅**
- ✅ **Do:** system patterns at meaningful moments, always with a visual
  cue; usable without haptics.
- ❌ **Don't:** haptics on every tap, or as the sole confirmation of an
  action.

**D6 — Sound ✅**
- ✅ **Do:** only on significant state changes, respecting silent mode;
  never autoplay without user control.
- ❌ **Don't:** UI sounds on every interaction or audio the user can't stop.

See also: `motion.md` (substitution table and opt-in pattern),
`../components/controls.md`, `../foundations/color.md`.
