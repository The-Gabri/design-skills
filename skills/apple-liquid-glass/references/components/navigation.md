# Navigation

**Verification legend** (applies to each rule and snippet):
- ✅ = direct HIG rule or official Apple documentation, confirmed in ≥2 independent sources.
- 🟡 = consistently documented in ≥3 sources, no verbatim Apple quote at hand.
- ⚠️ = doubtful / single source / disagreeing communities — not dogma.

The HIG distinguishes four patterns: **tabs** (navigation between sections), **hierarchy** (navigation stack), **sidebar/split view**, and **modality** (the latter in `presentation.md`).

---

## Bottom tab bar (iPhone)

- ✅ **The tab bar is for navigation only, never for actions.** HIG quote: *"Use a tab bar to support navigation, **not to provide actions**. If you need to provide controls that act on elements in the current view, use a toolbar instead."*
- ✅ **Maximum 5 tabs on iPhone.** HIG quote: *"Avoid overflow tabs… the trailing tab becomes a More tab… The More tab makes it harder for people to reach and notice content on tabs that are hidden."* More than 5 creates a "More" tab that hides destinations.
- 🟡 **Practical range: 2–5 destinations** at the same level. Include only the essential tabs: each extra tab costs more than it contributes.
- ✅ **Each tab keeps its own navigation state** (scroll position, depth). HIG quote: *"…let people quickly switch between sections of the view while preserving the current navigation state within each section."* Tapping the active tab returns to its root / scrolls to top (re-tap pops to root).
- ✅ **The tab bar always visible when navigating between sections.** HIG quote: *"Make sure the tab bar is visible when people navigate to different sections of your app. If you hide the tab bar, people can forget which area of the app they're in. The exception is when a modal view covers the tab bar, because a modal is temporary and self-contained."*
- ✅ **Never disable or hide individual tabs, even if their content is unavailable.** HIG quote: *"Don't disable or hide tab bar buttons, even when their content is unavailable… If a section is empty, explain why its content is unavailable."* If the section is empty, show an empty state inside (`ContentUnavailableView`).
- ✅ **Icon + text label always; a single word whenever possible.** HIG quote: *"Include tab labels to help with navigation… Use single words whenever possible."* No icon-only tabs.
- 🟡 **Selected state: filled symbol + accent tint; the active symbol is filled, the rest outline and dimmed.** One tint color for the active one; never a different tint per tab.
- 🟡 **Badges only for new or critical information**, sparingly.
- 🟡 **The tab bar hides when the keyboard is on screen** (system behavior; no need to manage it by hand).

## Floating tab bar (iOS 26 / Liquid Glass)

- ✅ **In iOS 26 the tab bar floats over the content** as a separate glass surface; content extends edge-to-edge underneath and "peeks out" from under it. WWDC25: *"The tab bar on iPhone floats above the content, and can be configured to minimize on scroll, keeping the focus on your content."* No need to rebuild it or paint backgrounds: the system already does it.
- 🟡 **Minimize-on-scroll: it shrinks, it doesn't disappear.** The `tabBarMinimizeBehavior` modifier takes `.onScrollDown`, `.onScrollUp`, `.automatic`, `.never`. The bar collapses to a pill and re-expands on reverse scroll; **never hide it fully on scroll** — the user must not be left without navigation.
- 🟡 **Floating accessory** (`.tabViewBottomAccessory`, iOS 26+): an accessory view for persistent cross-cutting content — mini-player, ongoing activity status, recording bar. When the bar minimizes, the accessory compacts and goes inline next to the pill. It's the only legitimate "glass on glass" spot: the accessory integrates with the tab bar, it doesn't float loose. ⚠️ The dynamic variant `.tabViewBottomAccessory(isEnabled:content:)` is iOS 26.1+: only use it if the deployment target is ≥26.1.
- 🟡 **iPadOS**: the tab bar goes **near the top**; it can be promoted to a sidebar (`tabViewStyle(.sidebarAdaptable)`). Allow customization (add/remove/reorder) with ≤5 tabs by default.
- ✅ **macOS has no tab bar pattern** (the equivalent is the sidebar); **tvOS**: the tab bar goes at the top.

## The search tab

- 🟡 **The search tab is a distinct role** (`Tab(role: .search)`, iOS 18+): it goes at the **trailing** edge, visually separated from the rest, and in iOS 26 it expands into a search field when selected. **Reserved for real search**; don't mix primary actions disguised as search.
- ⚠️ **`.tabViewSearchActivation(.searchTabSelection)` (iOS 26+): a single source.** It would link the `TabView`'s `.searchable` with the `.search`-role tab, but the signature isn't doubly verified: **confirm it in Apple's official SwiftUI documentation before treating it as definitive**. If unconfirmed, drop the modifier and keep only `Tab(role: .search)` + `.searchable` — the basic functionality is verified.

## The "swipe to go back" gesture is sacred

- 🟡 **Never break or reassign the swipe-from-left-edge gesture** (swipe-to-go-back). It's system muscle memory.
- 🟡 **The back button is a chevron + the previous screen's title, not a generic "Back".** Don't relabel it, don't replace it with a custom glyph, don't move it from the leading edge: it breaks muscle memory and the interactive gesture.
- 🟡 **Large title on a section's root destination; inline on pushed screens.** The large title collapses to inline on scroll.
- ✅ **Titles ≤15 characters; omit the title if redundant.**

## Toolbars and nav bars

- 🟡 **Anatomy**: leading (Back/Close, sidebar toggle, title), center/title, trailing (actions, 1–2 max). The rest goes in an overflow menu (•••).
- 🟡 **The toolbar holds the current screen's actions, not navigation between sections.** On iPhone it usually goes at the bottom; on iPad/Mac at the top and/or bottom; on iPadOS the nav bar doubles as a toolbar surface.
- 🟡 **In iOS 26 toolbars are floating Liquid Glass capsules**: group related controls in one glass container; one primary action (e.g. Done) separate and tinted as the focal point. **Don't mix text and icon in the same group** (they read as one merged button).
- 🟡 **Bars are transparent and float over scrolling content**; the system shows a soft scroll-edge effect only when content passes underneath. No custom backgrounds, hairlines, or "tint hacks": fighting the system produces double blur.
- ✅ **A single `.prominent` action** (tinted background) per bar, at the trailing edge. Bar buttons use **standard SF symbols** (no literal "Back" text); symbol before text except actions without a symbol ("Edit"). No borders on bar buttons — the bar is the container.
- ✅ **macOS: every toolbar item must also exist as a menu bar command.**
- 🟡 **Floating chrome with scroll**: for bars that travel with content (photo editor controls, text editor formatting bar) use `.safeAreaBar(edge:)` — it participates in the safe area and scroll edge effects. Don't use `.overlay(alignment: .bottom)` or `VStack { Spacer() }` by hand. The glass goes in a single `GlassEffectContainer` (one sampling surface; glass can't sample other glass).
- 🟡 **Layer rule**: `.glassEffect` only on fixed chrome (bars, toolbars), never inside list cells or scrolling views (produces unstable shimmer and per-frame GPU cost).

## Sidebar and split views (iPad/Mac)

- 🟡 **On iPad/Mac the pattern is the sidebar, not the bottom tab bar.** `NavigationSplitView` (sidebar → content → detail) collapses automatically to a `NavigationStack` on iPhone. One `TabView` can present as a sidebar with `.tabViewStyle(.sidebarAdaptable)` in regular width.
- 🟡 **The sidebar allows deeper hierarchies: max two levels.** If the hierarchy is deeper, a split view with a content column between sidebar and detail.
- 🟡 **In iOS 26 the sidebar also floats over content** in glass (`backgroundExtensionEffect`): extend content underneath.
- 🟡 On Mac, sidebars use outline views with disclosure triangles; each toolbar item must also exist as a menu bar command.

## Search fields

- ✅ **A single search field per screen**; with **clear** and **cancel**; result count; kind "no results" recovery (suggestions, not an empty wall).
- 🟡 In iOS 26, the search tab expands into a search field; `.searchToolbarBehavior(.minimize)` shows the `.searchable` as a compact button that expands on tap.

---

## SwiftUI examples

### 1. TabView with 4 destinations (iOS 26 floating tab bar) ✅

**When to use it:** an iPhone app's primary navigation with 2–5 same-level sections (music, notes, exercise). The iOS 26 tab bar already floats as a Liquid Glass capsule with no opt-in.

```swift
import SwiftUI

// Tab model: an enum with name and icon so literals aren't repeated
enum AppSection: Hashable {
    case home, library, activity, profile

    var title: String {
        switch self {
        case .home: "Home"
        case .library: "Library"
        case .activity: "Activity"
        case .profile: "Profile"
        }
    }

    var icon: String {
        switch self {
        case .home: "house"
        case .library: "books.vertical"
        case .activity: "chart.bar"
        case .profile: "person"
        }
    }
}

struct MainRoot: View {
    @State private var selection: AppSection = .home

    var body: some View {
        TabView(selection: $selection) {
            // Each tab has ITS OWN NavigationStack: the TabView never goes inside a stack
            Tab(AppSection.home.title, systemImage: AppSection.home.icon, value: .home) {
                NavigationStack { HomeView() }
            }
            Tab(AppSection.library.title, systemImage: AppSection.library.icon, value: .library) {
                NavigationStack { LibraryView() }
            }
            Tab(AppSection.activity.title, systemImage: AppSection.activity.icon, value: .activity) {
                NavigationStack { ActivityView() }
            }
            Tab(AppSection.profile.title, systemImage: AppSection.profile.icon, value: .profile) {
                NavigationStack { ProfileView() }
            }
        }
        // The bar minimizes to a pill on scroll down and returns on scroll up.
        // iPhone only; on iPad the bar doesn't minimize. No-op on iOS < 26.
        .tabBarMinimizeBehavior(.onScrollDown)
        // iPad: promotes the tab bar to a sidebar automatically (regular width)
        .tabViewStyle(.sidebarAdaptable)
    }
}
```

### 2. Floating accessory over the tab bar (mini-player) ✅

**When to use it:** persistent content visible across all tabs without a full screen: mini music/podcast player, ongoing activity status, recording bar.

```swift
import SwiftUI

struct RootWithPlayer: View {
    @State private var selection: AppSection = .home
    @State private var playing = true

    var body: some View {
        TabView(selection: $selection) {
            Tab("Home", systemImage: "house", value: AppSection.home) {
                NavigationStack { HomeView() }
            }
            Tab("Library", systemImage: "books.vertical", value: AppSection.library) {
                NavigationStack { LibraryView() }
            }
            Tab("Profile", systemImage: "person", value: AppSection.profile) {
                NavigationStack { ProfileView() }
            }
        }
        .tabBarMinimizeBehavior(.onScrollDown)
        // Floating panel over the tab bar; when the bar minimizes,
        // the accessory shrinks and goes inline next to the pill
        .tabViewBottomAccessory {
            MiniPlayer(playing: $playing)
        }
    }
}

struct MiniPlayer: View {
    @Binding var playing: Bool
    // The accessory's placement changes: .expanded (over the bar)
    // or .inline (next to the minimized bar). Adapt the content.
    @Environment(\.tabViewBottomAccessoryPlacement) private var placement

    var body: some View {
        HStack(spacing: 12) {
            // In inline mode only the essentials: icon + play/pause
            if placement == .expanded {
                Image(systemName: "music.note")
                    .imageScale(.large)
                VStack(alignment: .leading, spacing: 2) {
                    Text("Song name").font(.subheadline)
                    Text("Artist").font(.caption).foregroundStyle(.secondary)
                }
                Spacer()
            }
            Button {
                playing.toggle()
            } label: {
                Image(systemName: playing ? "pause.fill" : "play.fill")
                    .font(.title3)
            }
            // Minimum 44pt touch target
            .frame(minWidth: 44, minHeight: 44)
        }
        .padding(.horizontal, 16)
        .padding(.vertical, 8)
    }
}
```

**✅ DO:** an accessory for cross-cutting content (playback, ongoing activity); read the placement and compact the content in `.inline`.
**❌ DON'T:** tab-specific actions in the accessory (those go in floating glass buttons inside the tab's view); two stacked glass surfaces without grouping (glass can't sample other glass).

### 3. NavigationStack: title, automatic back, and toolbar ✅

**When to use it:** hierarchical navigation inside a tab (list → detail → subdetail). Back comes free from the system: a button with the previous screen's title + the "swipe to go back" gesture, which must never be broken.

```swift
import SwiftUI

// Typed destinations: navigation is driven by data, not by embedding views
enum LibraryRoute: Hashable {
    case shelf(id: UUID)
    case book(id: UUID)
}

struct LibraryView: View {
    @State private var path = NavigationPath()
    @State private var searchText = ""

    // Sample data (in a real app it'd come from the model)
    let shelves = ["Favorites", "To read", "Read"]

    var body: some View {
        NavigationStack(path: $path) {
            List {
                ForEach(shelves, id: \.self) { name in
                    NavigationLink(value: LibraryRoute.shelf(id: UUID())) {
                        Label(name, systemImage: "books.vertical")
                    }
                }
            }
            .navigationTitle("Library")   // Large title: collapses to inline on scroll
            .searchable(text: $searchText, prompt: "Search the library")
            // iOS 26: the search field shows as a compact button that expands on tap
            .searchToolbarBehavior(.minimize)
            // Each destination type resolves once here, not in each NavigationLink
            .navigationDestination(for: LibraryRoute.self) { route in
                switch route {
                case .shelf(let id):
                    ShelfView(id: id)
                case .book(let id):
                    BookView(id: id)
                }
            }
            .toolbar {
                // Leading group: navigation/actions controls
                ToolbarItem(placement: .topBarLeading) {
                    Button("Sort", systemImage: "arrow.up.arrow.down") { }
                }
                // The primary action goes trailing; at most ONE .prominent action per bar
                ToolbarItem(placement: .topBarTrailing) {
                    Button("Add", systemImage: "plus") { }
                        .buttonStyle(.glassProminent)
                }
            }
        }
    }
}

struct ShelfView: View {
    let id: UUID

    var body: some View {
        List {
            NavigationLink(value: LibraryRoute.book(id: UUID())) {
                Text("The Name of the Wind")
            }
        }
        .navigationTitle("Favorites")   // ≤15 characters; omit if redundant
        .toolbar {
            // Neighboring items share one glass background; the spacer splits them into groups
            ToolbarItem(placement: .bottomBar) {
                Button("Share", systemImage: "square.and.arrow.up") { }
            }
            ToolbarSpacer(.fixed, placement: .bottomBar)
            ToolbarItem(placement: .bottomBar) {
                Button("Delete", systemImage: "trash") { }
            }
            .tint(.red)   // Red is only for destructive/error; blue only for the primary action
        }
    }
}
```

**✅ DO:** short titles (≤15 characters) collapsing from large to inline; a single `.prominent` action per bar at the trailing edge; the Back button as the system provides it.
**❌ DON'T:** a homemade `TextField` in the toolbar for search (use `.searchable`); a `NavigationStack` wrapping the `TabView` (each tab has its own); opaque backgrounds or hand-drawn hairlines in the toolbar (in iOS 26 the bar is already glass; separation comes from the scroll edge effect).

### 4. Floating toolbar with glass over scrolling content ✅/🟡

**When to use it:** contextual controls that travel with content while scrolling without occupying the system toolbar: photo editor controls, a text editor's formatting bar, a detail sheet's actions.

```swift
import SwiftUI

struct PhotoEditor: View {
    @State private var selectedFilter = 0
    let filters = ["Original", "Vivid", "Drama", "B&W"]

    var body: some View {
        NavigationStack {
            ScrollView {
                // Content: the photo and its adjustments; extends edge to edge
                // and passes UNDERNEATH the floating bar
                VStack(spacing: 16) {
                    Image(systemName: "photo")
                        .resizable().scaledToFit()
                        .frame(maxWidth: .infinity)
                    ForEach(0..<20) { i in
                        Text("Adjustment \(i + 1)").frame(maxWidth: .infinity, alignment: .leading)
                    }
                }
                .padding()
            }
            .navigationTitle("Edit")
            // safeAreaBar: the bar participates in the safe area and the scroll
            // edge effects; content flows underneath naturally.
            // ALWAYS prefer over .overlay(alignment: .bottom) or VStack with Spacer().
            .safeAreaBar(edge: .bottom) {
                GlassEffectContainer {
                    HStack(spacing: 8) {
                        ForEach(filters.indices, id: \.self) { i in
                            Button(filters[i]) { selectedFilter = i }
                                .buttonStyle(.glass)
                                // The active button takes the prominent treatment
                                .tint(selectedFilter == i ? .blue : nil)
                        }
                    }
                    .padding(8)
                    .glassEffect(.regular, in: .capsule)  // one glass surface
                }
                .padding(.horizontal)
                .padding(.bottom, 8)
            }
        }
    }
}
```

**✅ DO:** one glass surface per bar; let content flow underneath (the system's scroll edge effect); `.clear` only over visually rich media (photo/video).
**❌ DON'T:** `.glassEffect` inside list cells or scrolling views (unstable shimmer and per-frame GPU cost); `overlay(alignment: .bottom)` with a handmade `.ultraThinMaterial` background; stacking glass on glass.

### 5. Sidebar with NavigationSplitView (iPad/Mac) ✅/🟡

**When to use it:** many sections or nested groups in regular width: productivity, mail, settings, catalogs. Three columns: sidebar → content → detail. On iPhone it collapses on its own to a `NavigationStack`.

```swift
import SwiftUI

struct ProductivityApp: View {
    // Column visibility (the user can collapse the sidebar)
    @State private var visibility: NavigationSplitViewVisibility = .all
    @State private var selectedCategory: String? = "Inbox"
    @State private var selectedTask: String?

    let categories = ["Inbox", "Today", "Projects", "Archive"]

    var body: some View {
        NavigationSplitView(columnVisibility: $visibility) {
            // Column 1: primary sidebar with clear sections
            List(categories, id: \.self, selection: $selectedCategory) { category in
                Label(category, systemImage: "tray")
            }
            .navigationTitle("Tasks")
        } content: {
            // Column 2: content for the sidebar selection
            if let category = selectedCategory {
                List(["Buy bread", "Call the bank", "Finish report"], id: \.self,
                     selection: $selectedTask) { task in
                    Text(task)
                }
                .navigationTitle(category)
            } else {
                ContentUnavailableView("Choose a category", systemImage: "tray")
            }
        } detail: {
            // Column 3: detail; empty state when nothing is selected
            if let task = selectedTask {
                VStack(alignment: .leading, spacing: 12) {
                    Text(task).font(.largeTitle)
                    Text("Task detail…").foregroundStyle(.secondary)
                    Spacer()
                }
                .padding()
            } else {
                ContentUnavailableView("Select a task", systemImage: "checklist")
            }
        }
        // 🟡 .navigationSplitViewStyle(.balanced): balances the column widths.
        // Standard API since iOS 16, but the exact signature was only seen in
        // one community source: check the official docs if using anything but .automatic.
        .navigationSplitViewStyle(.balanced)
    }
}
```

**✅ DO:** persistent selection per column; empty states (`ContentUnavailableView`) in content and detail; on Mac, every toolbar item also as a menu bar command.
**❌ DON'T:** hand-replicate the sidebar on iPhone (tabs or hierarchy); columns without selection state (blank screens with no explanation).

### 6. Search tab in the tab bar ✅ with a ⚠️ piece

**When to use it:** the app's global search with its own persistent destination (Music, Photos, App Store). The `.search`-role tab goes at the trailing edge, visually separated, and becomes a search field when selected.

```swift
import SwiftUI

struct RootWithSearch: View {
    @State private var selection: AppSection = .home
    @State private var searchText = ""

    var body: some View {
        TabView(selection: $selection) {
            Tab("Home", systemImage: "house", value: AppSection.home) {
                NavigationStack { HomeView() }
            }
            Tab("Library", systemImage: "books.vertical", value: AppSection.library) {
                NavigationStack { LibraryView() }
            }
            // .search role (iOS 18+): the system separates it from the rest and in iOS 26
            // turns it into a search field when selected
            Tab(role: .search) {
                NavigationStack {
                    SearchResultsView(text: searchText)
                        .navigationTitle("Search")
                }
            }
        }
        // ⚠️ .tabViewSearchActivation(.searchTabSelection): ONE source only.
        // Confirm the signature in Apple's official documentation before
        // treating it as definitive; unconfirmed, plain Tab(role: .search)
        // + .searchable is enough for search to work.
        .searchable(text: $searchText)
        .tabViewSearchActivation(.searchTabSelection)
        .tabBarMinimizeBehavior(.onScrollDown)
    }
}

struct SearchResultsView: View {
    let text: String

    var body: some View {
        if text.isEmpty {
            // Useful empty state: suggestions, not an empty wall
            ContentUnavailableView("Search your library", systemImage: "magnifyingglass",
                                   description: Text("Artists, songs, and playlists"))
        } else {
            List {
                Text("Results for “\(text)”")
            }
        }
    }
}
```

**✅ DO:** a single search field per screen; result counts; kind "no results" recovery (suggestions).
**❌ DON'T:** a search tab that searches nothing real; two competing search fields on the same screen; presenting `.tabViewSearchActivation` as verified API.

### 7. Web: glass-style floating toolbar (CSS) ⚠️

**When to use it:** approximating the iOS 26 floating toolbar on the web (a web version of the app or a mockup). **Mandatory reminder: `backdrop-filter` imitates the look, it is not Liquid Glass** (no refraction or dynamic sampling).

```css
/* ⚠️ Visual approximation, not the real material.
   Functional chrome floating over scrolling content. */
.floating-toolbar {
  position: fixed;
  left: 50%;
  bottom: calc(16px + env(safe-area-inset-bottom)); /* respects the home indicator */
  transform: translateX(-50%);
  display: flex;
  gap: 8px;
  padding: 8px 12px;
  border-radius: 999px; /* pill like the iOS 26 tab bar */
  background: rgba(255, 255, 255, 0.55);
  -webkit-backdrop-filter: blur(20px) saturate(180%); /* -webkit- mandatory on Safari/iOS */
  backdrop-filter: blur(20px) saturate(180%);
  border: 1px solid rgba(255, 255, 255, 0.5);
  box-shadow:
    0 8px 32px rgba(0, 0, 0, 0.12),
    inset 0 1px 0 rgba(255, 255, 255, 0.6);
}
/* Dark variant */
@media (prefers-color-scheme: dark) {
  .floating-toolbar {
    background: rgba(20, 20, 22, 0.45);
    border-color: rgba(255, 255, 255, 0.12);
  }
}
/* Mandatory fallbacks: no backdrop-filter or reduced transparency → legible solid */
@supports not ((backdrop-filter: blur(1px)) or (-webkit-backdrop-filter: blur(1px))) {
  .floating-toolbar { background: var(--bg); border-color: var(--separator); }
}
@media (prefers-reduced-transparency: reduce) {
  .floating-toolbar { background: var(--bg); -webkit-backdrop-filter: none; backdrop-filter: none; }
}
```

**✅ DO:** use it only for floating functional chrome (nav, bars, sheets); solid fallbacks; `env(safe-area-inset-bottom)` for the home indicator.
**❌ DON'T:** glass in content cards or grids (never more than 1–3 blurred surfaces); animate `backdrop-filter` (animate only `transform` and `opacity`); claim this *is* Liquid Glass.

---

## Do / don't pairs

| ✅ Do | ❌ Don't | Why |
|---|---|---|
| Tab bar with 2–5 stable same-level destinations | Actions ("New", "Post") as tabs | HIG: the tab bar navigates, it doesn't act ✅ |
| Each tab with its own `NavigationStack` | A `NavigationStack` wrapping the `TabView` | Navigation state is per tab; wrapping it breaks back and restoration 🟡 |
| Let iOS 26 put glass on tab bars/toolbars on its own | Repaint backgrounds, blurs, or hairlines by hand over system bars | Fighting the system produces double blur and breaks the scroll edge effect ✅ |
| Minimize the tab bar on scroll (`.onScrollDown`) | Hide it fully on scroll | The minimized bar returns on reverse scroll; hidden, the user loses their place ✅ |
| The system's Back button as-is (previous screen's title + swipe gesture) | Customize the back button or break the gesture | "Swipe to go back" is sacred; customizing it disorients ✅ |
| `.searchable` for search (in toolbar, in tab, or minimized) | A homemade `TextField` inside a `ToolbarItem` | The system positions, animates, and wires search for free; the homemade one breaks the glass layout ✅/🟡 |
| `safeAreaBar` for floating chrome over scroll | `overlay(alignment: .bottom)` or `VStack { Spacer() }` | `safeAreaBar` participates in the safe area and scroll edge effects 🟡 |
| One floating glass level (`GlassEffectContainer` if there are neighbors) | Glass on glass without grouping | Glass can't sample other glass: it produces artifacts ✅ |
| Sidebar (`NavigationSplitView` or `.sidebarAdaptable`) on iPad/Mac | Hand-replicating sidebars on iPhone | On iPhone: tabs or hierarchy; the sidebar is a regular-width pattern ✅ |
| Titles ≤15 characters, large title that collapses | Long fixed titles that don't collapse | The large title is orientation; on scroll it must yield space to content ✅ |
| Empty states (`ContentUnavailableView`) in empty tabs and unselected columns | Disabled/hidden tabs or blank columns | Never hide destinations: if empty, explain inside ✅ |

See also: `presentation.md` (modality), `controls.md` (toolbar actions).
