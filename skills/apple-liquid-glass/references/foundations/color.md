# Color

HIG semantic-color rules + copy-pasteable SwiftUI and CSS examples.

**Verification legend:** ✅ = direct quote or rule from the HIG / official docs confirmed in ≥2 sources; 🟡 = consistently documented in ≥3 sources; ⚠️ = approximation or unverified.

## Rules ✅ (verified in ≥4 sources)

1. **Semantic colors, always.** `label`, `secondaryLabel`, `systemBackground`, `separator`, `systemBlue`… In native code use the **names**, never hex: Apple may change the values per release.
2. **Real Dark Mode.** Every custom color is defined as a set with light and dark variants (asset catalog). There is no "light-only" design.
3. **Contrast:** 4.5:1 for normal text, 3:1 for large text (WCAG AA). Apple adds that contrast must survive **over translucent materials** (glass, vibrancy). ✅
4. **One tint per screen.** The accent/tint organizes the hierarchy. Don't tint multiple controls on the same bar.
5. **Color is never the only channel.** State or meaning comes with text, an icon, or a symbol: if color fails (color blindness, grayscale), the app stays usable.

## Tint semantics ✅

- `systemBlue` = primary action / default tint.
- `systemRed` = destructive / error.
- `systemGreen` = success / available.
- Orange/yellow = warning; gray = inactive or neutral.
- Never reuse one color with two meanings on the same screen (e.g. red = "delete" and red = "new").

## Clear / Tinted (iOS 26+) 🟡

Since 26.1 the user can choose the system "look" (**Clear** = more transparent, **Tinted** = more opaque, with more contrast) and **it affects third-party apps**: your design must survive both. Also, icons and widgets can carry the **user's global tint** — don't hardcode that your app "looks" a single way. 🟡

## Color in Liquid Glass ✅

HIG quote:

> "Glass has no inherent color; it picks up what's behind it. Tint only elements that need emphasis — a primary action, a status indicator."

Tint with meaning, not decoration. And: "Provide light and dark color variants even in a single-appearance app." ✅

## Vibrancy 🟡

On content over materials (alerts, sidebars), labels turn vibrant: use dynamic colors (`label`, `secondaryLabel`), which vibrate on their own over the background. Don't hardcode hex over glass. 🟡

---

## SwiftUI

### Semantic text and background colors ✅

```swift
struct ProfileCard: View {
    var body: some View {
        VStack(alignment: .leading, spacing: 8) {
            // WHEN → 95% of your app's text.
            // Adapts on its own to light/dark mode and Increase Contrast.
            Text("Hi, Alex")
                .foregroundStyle(.primary)

            // WHEN → subtitles, metadata, timestamps.
            Text("Active 5 minutes ago")
                .foregroundStyle(.secondary)

            Divider()
            // Semantic separator: it lightens on its own in dark mode;
            // a hardcoded gray would look wrong.
        }
        .padding()
        // WHEN → root background of any view.
        // .systemBackground is white in light and black in dark: never hardcode it.
        .background(Color(uiColor: .systemBackground))
    }
}
```

### Settings-style grouped background ✅

```swift
struct SettingsList: View {
    var body: some View {
        VStack(spacing: 0) {
            Text("Notifications")
            Divider().background(Color(uiColor: .separator)) // ✅ semantic separator
            Text("Privacy")
        }
        // WHEN → Settings-style forms and settings.
        .background(Color(uiColor: .systemGroupedBackground))
    }
}
```

### One accent per screen ✅

```swift
struct MainScreen: View {
    var body: some View {
        NavigationStack {
            List {
                Button("View details") { /* ... */ }
            }
            // WHEN → define the accent ONCE, high in the hierarchy.
            // All interactive elements (links, toggles, buttons) inherit this tint.
            .tint(.blue) // ✅ blue = primary/safe action
            .navigationTitle("Home")
        }
    }
}
// Global alternative (once, at the root view):
// ContentView().tint(.blue)
```

### Destructive button vs. primary action ✅

```swift
struct DeleteDialog: View {
    var body: some View {
        VStack(spacing: 16) {
            // PRIMARY ACTION: the main, safe action. Filled, prominent,
            // with the accent (blue by default).
            Button("Save changes") { /* ... */ }
                .buttonStyle(.borderedProminent)
                .tint(.blue)

            // DESTRUCTIVE ACTION: delete, remove, sign out.
            // System red, NEVER the accent. Don't make it prominent
            // if there's a primary action on the same screen.
            Button("Delete account", role: .destructive) { /* ... */ }
                .buttonStyle(.bordered)
            // ✅ `role: .destructive` tints the button red automatically.
        }
    }
}
```

### State with a triple channel: color + icon + text ✅

```swift
struct SyncStatus: View {
    enum Status { case ok, error, syncing }
    let status: Status

    var body: some View {
        // WHEN → any status indicator (success, error, warning).
        // Color REINFORCES; icon and text COMMUNICATE.
        // A color-blind user must understand it without the color.
        HStack(spacing: 8) {
            Image(systemName: icon).foregroundStyle(color)
            Text(text).foregroundStyle(.primary)
        }
    }

    private var icon: String {
        switch status {
        case .ok: "checkmark.circle.fill"
        case .error: "xmark.circle.fill"
        case .syncing: "arrow.triangle.2.circlepath"
        }
    }
    private var color: Color {
        switch status {
        case .ok: .green
        case .error: .red
        case .syncing: .secondary // gray: the motion already signals activity
        }
    }
    private var text: String {
        switch status {
        case .ok: "Synced"
        case .error: "Sync failed"
        case .syncing: "Syncing…"
        }
    }
}
```

### Reacting to the color scheme only when needed ✅

```swift
struct HeroView: View {
    // WHEN → ONLY when a semantic color doesn't serve you and you need
    // an explicit decision (an illustration, a brand gradient).
    // If semantic colors can solve it, use them.
    @Environment(\.colorScheme) private var colorScheme

    var body: some View {
        RoundedRectangle(cornerRadius: 24)
            .fill(colorScheme == .dark
                  ? Color(red: 0.15, green: 0.18, blue: 0.35) // night blue
                  : Color(red: 0.85, green: 0.90, blue: 1.0)) // sky blue
    }
}
```

---

## CSS (web with an Apple look)

### Semantic variables + `light-dark()` ✅

```css
/* WHEN → base of any web page with automatic light/dark mode.
   Define the semantic tokens ONCE; the browser picks the value per the OS.
   Requires `color-scheme: light dark` at the root: without it, light-dark() won't switch. */
:root {
  color-scheme: light dark;

  --bg: light-dark(#ffffff, #000000);            /* like .systemBackground */
  --bg-grouped: light-dark(#f2f2f7, #1c1c1e);   /* like .systemGroupedBackground */
  --text: light-dark(#1c1c1e, #f5f5f7);          /* Apple near-black / near-white */
  --text-secondary: light-dark(#6e6e73, #98989d); /* Apple-style secondary gray */
  --separator: light-dark(#c6c6c8, #38383a);
  --accent: #0071e3; /* Apple blue: THE single accent for the whole UI */
}

body {
  background: var(--bg);
  color: var(--text);
}
```

### Classic equivalent with `prefers-color-scheme` ✅

```css
/* WHEN → compatibility with older browsers or adjustments
   light-dark() can't express (shadows, borders, images).
   For simple colors, prefer light-dark(): less duplication. */
:root {
  --bg: #ffffff;
  --text: #1c1c1e;
  --card: #f5f5f7;
}

@media (prefers-color-scheme: dark) {
  :root {
    --bg: #000000;
    --text: #f5f5f7;
    --card: #1c1c1e;
  }
}
```

### Increased contrast ✅

```css
/* WHEN → users with "Increase contrast" on in the OS.
   Don't invent your own palette: strengthen borders and darken secondary text. */
@media (prefers-contrast: more) {
  :root {
    --text-secondary: var(--text); /* goodbye to washed-out grays */
    --border-subtle: currentColor; /* visible borders without guessing */
  }
}
```

### Primary vs. destructive button ✅

```css
/* WHEN → web replica of the iOS convention: blue = primary and safe,
   red = destructive. */
.button-primary {
  background: var(--accent); /* #0071e3: the ONLY accent */
  color: #ffffff;
  border-radius: 12px;
  padding: 12px 24px;
  font-weight: 600;
}

.button-destructive {
  background: transparent;
  color: #ff3b30; /* iOS system red: only for destroying */
  border: 1px solid currentColor;
  border-radius: 12px;
  padding: 12px 24px;
}
```

### Triple-channel status on the web ✅

```html
<!-- WHEN → status messages: color decorates, icon and text communicate. -->
<p class="status status--error" role="alert">
  <span aria-hidden="true">✕</span>
  Failed to save: check your connection
</p>
```

```css
.status { display: flex; gap: 8px; align-items: center; font-weight: 500; }
.status--ok { color: light-dark(#1d8127, #30d158); }      /* system green */
.status--error { color: light-dark(#d70015, #ff453a); }   /* system red */
.status--warning { color: light-dark(#9a6a00, #ffd60a); } /* system yellow */
```

---

## Do / don't pairs

1. **Semantic colors vs. hardcoded hex** ✅
   - ✅ DO: `Color(uiColor: .systemBackground)`, `.foregroundStyle(.primary)`, `light-dark(...)` — they adapt on their own to dark mode, contrast, and future OS changes.
   - ❌ DON'T: a fixed `#ffffff` as background, `#000` as text — in dark mode you get black-on-black or a white flash.

2. **One accent per screen** ✅
   - ✅ DO: one `.tint(.blue)` high in the hierarchy (or `--accent` in CSS).
   - ❌ DON'T: blue buttons, green links, purple toggles, and orange badges in the same view.

3. **Color reinforces, it doesn't communicate alone** ✅
   - ✅ DO: error = ✕ icon + "Error" text + red.
   - ❌ DON'T: a red dot with no label for "failed" — roughly 1 in 12 men can't tell red from green.

4. **Red only for destroying** ✅
   - ✅ DO: `Button("Delete", role: .destructive)` in red; the primary in the accent.
   - ❌ DON'T: the "Continue" button in red "because it grabs attention" — in iOS red means danger/irreversible.

5. **Real contrast on secondary text** ✅
   - ✅ DO: `#6e6e73` on white / `#98989d` on black (≥ 4.5:1); with `prefers-contrast: more`, secondary becomes primary text.
   - ❌ DON'T: `#cccccc` on white "because it looks elegant" — if people have to squint, it's an accessibility bug.

6. **Desaturate what's inactive** ✅
   - ✅ DO: disabled controls in gray or reduced opacity — reads as "unavailable" in any language.
   - ❌ DON'T: a disabled button in washed-out blue or soft red — it looks like an error or a valid variant.

See also: `two-layers.md` (color in the content), `../system/tokens.md` (hex values), `../materials/liquid-glass.md`.
