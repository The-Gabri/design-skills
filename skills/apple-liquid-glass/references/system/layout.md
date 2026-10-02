# Layout and adaptability ✅/🟡

Composition rules and copy-pasteable examples (SwiftUI + CSS). Base numeric
values are in `tokens.md`.

Legend: ✅ = direct HIG/official-doc quote in ≥2 sources; 🟡 = consistent in
≥3 independent sources; ⚠️ = doubtful or single source.

---

## 1. Base rules ✅/🟡

- ✅ **8pt grid** (4pt fine step); all spacing falls on the grid.
- ✅ **Horizontal margins**: 16pt iPhone, 20pt iPad (regular width). 🟡
- ✅ **44×44pt touch target**; **8pt** minimum separation between tappable
  elements. Nothing interactive under the notch, Dynamic Island, or the home
  indicator (~34pt). `ignoresSafeArea` only for backgrounds and decoration.
- ✅ Layout must **fit the screen**: no horizontal scroll or pinch-zoom for
  primary content. **One primary action per screen.**
- 🟡 **Readable text width on iPad ~672pt max** (≈ 65–75 characters): only
  for **running text** (constrained with `readableContentGuide`); tables
  and lists fill their column. Tables: see E5.
- ✅ Test on the smallest width (iPhone SE) and the largest text (AX5):
  nothing truncates or breaks.

Screen zones (iOS, reference 🟡):
status bar 20pt classic (44–54pt with Dynamic Island), nav bar 44pt row +
~52pt large title (~96pt total), tab bar ~49pt, flexible content.

---

## 2. Safe areas ✅

- ✅ Always respect **safe areas**: notch, Dynamic Island (~59pt of status
  bar on those devices), home indicator (34pt bottom inset),
  cameras/housings. Backgrounds may extend under bars; interactive content
  **never** sits under them.
- ✅ On the web: `viewport-fit=cover` + `env(safe-area-inset-*)`.

### E1 — Floating bar over scroll: `safeAreaInset` / `safeAreaBar` ✅

**When to use it:** an action bar (save, buy, CTA) pinned over a
`ScrollView`/`List` without covering content. The content reserves its space
automatically and slides under the bar.

```swift
import SwiftUI

struct ArticleDetail: View {
    var body: some View {
        ScrollView {
            LazyVStack(alignment: .leading, spacing: 16) {
                ForEach(articles) { article in
                    ArticleCard(article: article)
                }
            }
            .padding(16)
        }
        // iOS 15+. The bar adjusts the safe area: the last scroll
        // element is never hidden behind the button.
        .safeAreaInset(edge: .bottom, spacing: 0) {
            Button("Add to list") {
                addToList()
            }
            .buttonStyle(.borderedProminent)
            .frame(maxWidth: .infinity)
            .padding(.horizontal, 16)
            .padding(.vertical, 8)
            .background(.ultraThinMaterial)
        }
    }
}
```

In iOS 26+, if the goal is Liquid Glass, prefer `safeAreaBar` —
it participates in the scroll edge system and extends glass correctly ✅:

```swift
import SwiftUI

struct GlassArticleDetail: View {
    var body: some View {
        List {
            ForEach(articles) { ArticleCard($0) }
        }
        // ✅ iOS 26+: verified signature —
        // safeAreaBar(edge:alignment:spacing:content:)
        .safeAreaBar(edge: .bottom) {
            HStack(spacing: 8) {
                Button("Edit") { edit() }.buttonStyle(.glass)
                Spacer()
                Button("Save") { save() }.buttonStyle(.glassProminent)
            }
            .padding(.horizontal, 16)
            .padding(.vertical, 8)
        }
        .scrollEdgeEffectStyle(.soft, for: .bottom) // Soft fade passing under the bar
    }
}

// Pre-iOS 26 fallback: `.safeAreaInset(edge: .bottom)` with a material
// background gives the same layout without the glass.
```

### E2 — Scroll edge effects in iOS 26 ✅

**When to use it:** so content sliding under bars, the notch, or the home
indicator melts smoothly instead of cutting off abruptly.

```swift
import SwiftUI

struct BorderedList: View {
    var body: some View {
        List {
            ForEach(items) { ItemRow(item: $0) }
        }
        // ✅ iOS 26+: soft fade at the top edge on scroll
        .scrollEdgeEffectStyle(.soft, for: .top)
        // ✅ iOS 26+: mirrors and blurs the view into the adjacent
        // safe area (use sparingly: at most one per screen)
        .backgroundExtensionEffect()
    }
}
```

### E3 — Safe areas on the web with `env()` + `viewport-fit=cover` ✅

**When to use it:** any full-screen web on iOS (PWA, webview). Without this,
the notch, Dynamic Island, and home indicator eat your content.

```html
<!-- ✅ Step 1: the viewport declares cover so iOS extends the page
     under the notch. Without this, env() is 0. -->
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover" />
```

```css
/* ✅ Step 2: the system insets are EXACTLY the hardware size — always add
   your own margin on top. 0px fallback for browsers without support. */
.top-bar {
  position: sticky; top: 0;
  padding-top: calc(env(safe-area-inset-top, 0px) + 12px);
  padding-inline: calc(env(safe-area-inset-left, 0px) + 16px)
                  calc(env(safe-area-inset-right, 0px) + 16px);
}
.bottom-bar {
  position: fixed; left: 0; right: 0; bottom: 0;
  padding-bottom: calc(env(safe-area-inset-bottom, 0px) + 12px);
  padding-inline: calc(env(safe-area-inset-left, 0px) + 16px)
                  calc(env(safe-area-inset-right, 0px) + 16px);
}
/* ✅ In landscape the insets move to the sides: apply to all four.
   It's the most common bug. */
```

---

## 3. Adaptability: size classes, not devices ✅/🟡

- ✅ **Layout is governed by size classes (compact/regular), never by
  device type or orientation.** Identical functionality everywhere:
  tab bar ↔ sidebar swaps as width grows.
- ✅ Portrait iPhone = C×R; standard landscape iPhone = C×C; full-screen
  iPad = R×R; portrait iPad is **always** Regular; Slide Over forces
  compact (~320–375pt); Split View 1/2 compact on both (except 12.9/13"
  Pros which can yield R×R).
- ✅ Support **arbitrary window sizes** (Stage Manager, continuous
  resizing): no hardcoded widths, reflow with split views and Dynamic Type.

### E4 — Adapting iPhone/iPad with `horizontalSizeClass` ✅

**When to use it:** to change the layout STRUCTURE per available width (not
the device). Also works with iPad multitasking (Slide Over, Split View)
and Catalyst.

```swift
import SwiftUI

struct AdaptiveGallery: View {
    // ✅ Reads the horizontal size class from the environment:
    // .compact ≈ portrait iPhone, .regular ≈ full-screen iPad.
    @Environment(\.horizontalSizeClass) private var horizontalClass

    let compactColumns = [GridItem(.flexible()), GridItem(.flexible())]
    let regularColumns = [GridItem(.flexible()), GridItem(.flexible()), GridItem(.flexible())]

    var body: some View {
        ScrollView {
            LazyVGrid(
                columns: horizontalClass == .compact
                    ? compactColumns   // iPhone: 2 columns
                    : regularColumns,  // iPad: 3 columns
                spacing: 16
            ) {
                ForEach(photos) { photo in
                    PhotoThumbnail(photo: photo)
                }
            }
            // Larger margins on iPad, like the system apps
            .padding(.horizontal, horizontalClass == .compact ? 16 : 24)
        }
    }
}

// ❌ Don't check `UIDevice.current.userInterfaceIdiom == .pad` for this:
// it breaks with Slide Over, Split View, and Catalyst.
```

### E5 — Readable text width on iPad 🟡

**When to use it:** on regular-width screens (iPad, Mac Catalyst), where a
full-width paragraph is unreadable. Constrain the text measure to the
comfortable reading zone (~65–75 characters).

```swift
import SwiftUI

struct ReadingArticle: View {
    @Environment(\.horizontalSizeClass) private var horizontalClass

    var body: some View {
        ScrollView {
            VStack(alignment: .leading, spacing: 16) {
                Text(article.title)
                    .font(.largeTitle)
                    .fontWeight(.bold)
                    .textBalance() // Spreads the headline over balanced lines
                ForEach(article.paragraphs, id: \.self) { paragraph in
                    Text(paragraph).font(.body).lineSpacing(4)
                }
            }
            .padding(24)
            // 🟡 On iPad, text narrows to the readable column and centers;
            // on iPhone it takes the full width.
            .frame(maxWidth: horizontalClass == .compact ? .infinity : 672)
            .frame(maxWidth: .infinity) // Centers the column on iPad
        }
    }
}

// 672pt ≈ 70 characters of body text: the recommended measure for
// comfortable reading. The exact value is a cap, not magic.
```

### E6 — Carousels with `containerRelativeFrame` (no `GeometryReader`) ✅

**When to use it:** paginated cards where each card must measure an exact
fraction of the visible container (e.g. "2.2 cards peek to hint there's
more"). iOS 17+.

```swift
import SwiftUI

struct FeaturedCarousel: View {
    var body: some View {
        ScrollView(.horizontal, showsIndicators: false) {
            LazyHStack(spacing: 12) {
                ForEach(featured) { item in
                    FeaturedCard(item: item)
                        // ✅ Each card measures 2/5 of the container
                        // (count: 5, span: 2) → hints at the next one.
                        .containerRelativeFrame(.horizontal, count: 5, span: 2, spacing: 12)
                }
            }
            .scrollTargetLayout() // Enables card-by-card snapping
            .padding(.horizontal, 16)
        }
        .scrollTargetBehavior(.viewAligned) // Scroll stops card by card
    }
}
```

### E7 — `GeometryReader` for content peeking under controls ✅

**When to use it:** only when you need the container's REAL size in points
for a declarative calculation (a floating header's height for the content
peek). Read it in the background so it doesn't interfere with layout.

```swift
import SwiftUI

struct PeekingHeader: View {
    @State private var headerHeight: CGFloat = 0

    var body: some View {
        ZStack(alignment: .top) {
            ScrollView {
                LazyVStack(spacing: 16) {
                    ForEach(news) { article in
                        NewsCard(article: article)
                    }
                }
                .padding(.top, headerHeight + 8) // Calculated peek, not guessed
                .padding(.horizontal, 16)
            }
            FloatingHeader()
                .background {
                    GeometryReader { proxy in
                        Color.clear
                            .onAppear { headerHeight = proxy.size.height }
                            .onChange(of: proxy.size.height) { _, newValue in
                                headerHeight = newValue
                            }
                    }
                }
        }
    }
}

// Note: if you just need "the card = X fraction of the container", use
// .containerRelativeFrame (E6) instead of GeometryReader: it's declarative
// and doesn't break the layout system.
```

### E8 — Container queries vs. media queries (CSS) ✅/🟡

**When to use it:** `@container` when the SAME component lives in several
contexts (sidebar, content, modal) and must adapt to its container;
media queries for PAGE-LEVEL changes and for what containers can't see
(orientation, dark mode, reduced motion, pointer).

```css
/* ✅ Step 1: the container declares its children may query it */
.panel { container-type: inline-size; }

/* ✅ Step 2: the card changes per container, not per viewport */
.product-card {
  display: flex; flex-direction: column;
  gap: 16px; padding: 24px;
}
@container (min-width: 560px) {
  .product-card { flex-direction: row; align-items: center; }
  .product-card img { width: 160px; flex-shrink: 0; }
}
```

```css
/* 🟡 Mobile-first: mobile base, progressive enhancements. Compact < 768px /
   regular ≥ 768px (consistent in ≥3 sources). */
.container { padding-inline: 16px; }
.grid { display: grid; grid-template-columns: 1fr; gap: 16px; }

@media (min-width: 768px) {
  .container { padding-inline: 24px; }
  .grid { grid-template-columns: repeat(3, 1fr); gap: 24px; }
}
@media (min-width: 1024px) {
  .reading-container {
    max-width: 68ch; /* ≈ 65–75 characters: comfortable measure */
    margin-inline: auto;
  }
}
```

---

## 4. iPadOS multitasking 🟡

- 🟡 The app must survive **Split View and Slide Over** (sizes changing live): fluid layout with Auto Layout/SwiftUI, no hardcoded geometries. A stretched phone layout on iPad is a defect, not an adaptation.

## 5. iOS 26 — spacing with floating chrome 🟡

- 🟡 Tab bars and toolbars float as glass capsules **over** content: don't put critical content directly behind them; respect the extended safe area insets.
- 🟡 Scroll edge effects replace opaque bar backgrounds: remove `barTintColor`, custom backgrounds, and `configureWithOpaqueBackground()`.

---

## Do / don't pairs

**D1 — Safe areas ✅**
- ✅ **Do:** extend the background under the notch/Dynamic Island/home indicator, but keep interactive content and text inside the safe area (`safeAreaInset`/`safeAreaBar`; `env(safe-area-inset-*)` with `viewport-fit=cover` in CSS).
- ❌ **Don't:** buttons or text hidden by hardware. The classic web mistake is forgetting `viewport-fit=cover` (then `env()` returns 0 and everything looks fine in the emulator but breaks on the real device) or forgetting the sides in landscape.

**D2 — Spacing ✅**
- ✅ **Do:** closed scale of multiples of 8 (4 / 8 / 16 / 24 / 32 / 48).
- ❌ **Don't:** eyeballed values like 5, 11, 13, or 21: they break the vertical rhythm and every screen looks like a different app.

**D3 — Adaptation ✅**
- ✅ **Do:** `@Environment(\.horizontalSizeClass)` (compact/regular). Responds to rotation, Split View, Slide Over, and Catalyst with no extra code.
- ❌ **Don't:** `UIDevice.current.userInterfaceIdiom == .pad` or iPhone models. An iPad in Slide Over is compact and your "iPad layout" would break; a landscape iPhone 16 Pro Max can be regular.

**D4 — Long text on iPad 🟡**
- ✅ **Do:** ~65–75 characters per line (`.frame(maxWidth: 672)` in SwiftUI, `max-width: 68ch` in CSS) and center.
- ❌ **Don't:** edge-to-edge paragraphs on iPad or desktop: the eye loses the line on return. It's the most visible failure of "stretched mobile web".

**D5 — Floating bar ✅**
- ✅ **Do:** `.safeAreaInset(edge:)` (iOS 15+) or `.safeAreaBar(edge:)` (iOS 26+, with integrated glass). The system reserves the space and the scroll passes underneath with the correct edge effect.
- ❌ **Don't:** `.overlay(alignment: .bottom)` with a hand-made material, nor `VStack { content; Spacer(); bar }` fighting the safe area. The overlay covers the last scroll element and a manual material doesn't participate in the Liquid Glass system (it renders wrong on scroll and costs extra GPU).

**D6 — Measuring the container ✅**
- ✅ **Do:** for "X fraction of the container" use `.containerRelativeFrame` (iOS 17+); reserve `GeometryReader` for calculations that truly need the size in points (E7).
- ❌ **Don't:** wrap views in `GeometryReader` out of habit: it breaks lazy layout, invalidates the size-proposal system, and is cause #1 of layout loops and jumping scrolls.

**D7 — Reusable component: container query vs. media query ✅**
- ✅ **Do:** `@container` + `container-type: inline-size`: responds to the component's real container.
- ❌ **Don't:** media queries for components: a card in a 300px sidebar on a 1024px iPad would receive the "iPad layout" and break. Media queries for page structure and for `prefers-reduced-motion` / `prefers-color-scheme` / orientation.

See also: `tokens.md`, `../platforms/ios.md`,
`../materials/liquid-glass.md`.
