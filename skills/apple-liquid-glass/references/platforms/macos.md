# macOS Tahoe 26 ✅/🟡

The biggest macOS redesign in years: Liquid Glass in the Dock, sidebars, toolbars, **menu bar**, and Control Center.

## Transparent menu bar ✅/🟡

- ✅ "The **menu bar is fully transparent** by default" (Apple at WWDC; 9to5Mac, AppleInsider, MacRumors). The stated goal: make the screen feel larger. Height: **24 pt**. 🟡
- ✅ The user can get the background back: **System Settings → Menu Bar → "Show menu bar background"** (on/off toggle). Design consequence: assume neither background nor transparency — legibility must work both ways.
- ✅ **Menu bar**: every app action exists as a menu command; discoverable keyboard shortcuts; expose the full functionality there, not just in toolbars.
- 🟡 Menu bar extras float directly over the wallpaper: define them as **template icons** (SF Symbol or black-and-clear shape) so the system recolors them in light/dark mode and selected state. No full-color icons in the menu bar.
- ✅ **Reduce Transparency**: with the accessibility setting on, the menu bar becomes an opaque gray bar and glass falls back to opaque — layouts must survive ("Test with Reduce Transparency and Increase Contrast"). macOS 26.1 adds a "Tinted" mode that increases material opacity.
- 🟡 Control Center and the menu bar are now one customizable canvas (System Settings → Menu Bar): you can choose which controls live in each, resize them (Small/Medium/Large), and reorder them; third-party items can be locked out. Third-party/iPhone controls arrive via a controls gallery.

### Example: app commands in the menu bar 🟡

```swift
import SwiftUI

// ═══════════════════════════════════════════════════════════════════
// WHEN: every Mac app exposes its functionality as menu commands.
// It's the canonical home of each action: discoverable shortcuts,
// Services, legacy Touch Bar. The user can search commands from Help.
// LIMITS: commands must always exist (not just in toolbars);
// the system organizes the menu hierarchy by convention.
// ═══════════════════════════════════════════════════════════════════

struct MyApp: App {
    var body: some Scene {
        WindowGroup {
            Content()
        }
        // Add your commands to the system's canonical menus. 🟡
        .commands {
            CommandMenu("Habits") {
                Button("Mark today's habit") {
                    markHabit()
                }
                // Discoverable shortcut: appears next to the command in the menu. ✅
                .keyboardShortcut("h", modifiers: [.command, .shift])

                Divider()

                Button("Sync now") {
                    sync()
                }
                .keyboardShortcut("r", modifiers: .command)
                .disabled(!isConnected) // Degrades gracefully: disabled, not hidden. ✅
            }
        }
    }
}
```

## App icons: tinted / clear ✅/🟡

- ✅ Four icon styles (System Settings → Appearance → "Icon & widget style", a setting **independent** of Light/Dark): **Default** (colorful, white symbol), **Dark** (near-black neutral background, glyph with its own tint), **Clear** (light gray, dark-gray symbol — on macOS it looks "more gray than transparent"), **Tinted** (mid gray, white symbol; in grayscale, tinted with the system/folder color).
- ✅ Authoring format: **Icon Composer `.icon`** file (≤4 layer groups, 1024×1024 canvas, no baked shadows/gloss); the system renders the Default, Dark, Clear, Tinted variants + the glass depth. Keep the legacy `.icns` only as a fallback for older macOS.
- ✅ The system mask crops **all** layers to the rounded-rectangle (squircle) shape: deliver square layers without a mask, content centered. Free-form icons overflowing the shape get a generic system background and "look broken".
- 🟡 Actionable rule: the icon must stay recognizable desaturated to grays — don't depend on color alone. In iOS 18+ the Tinted style was already adjustable; on macOS the user picks the tint color (tied to folder color/theme).
- 🟡 Folders accept custom color, emoji, or symbol (Finder → right-click → Customize; global color in Appearance → Folder color).

## Windows, sidebars, and toolbars ✅/🟡

- ✅ Toolbars, sidebars, and menus are **Liquid Glass**: they refract content and the desktop; content **scrolls underneath** with a scroll-edge effect (progressive blur). Rule: "Don't paint opaque bar backgrounds and don't stack custom glass on system glass."
- ✅ More rounded windows with **concentric corner radii** aligned to the window corners: derive nested radii from the container, never hardcode them. Controls trending toward capsule and slightly taller; menus/popovers "morph" from the control that opened them.
- ✅ **Windows**: one window = one task; don't reinvent window chrome (traffic lights); respect main/key/inactive states. Windows **resizable and often multiple**.
- ✅ **Sidebar** as the primary navigation (outline views with disclosure triangles); trailing **inspector** for details.
- ✅ **Tables**: sortable, resizable columns; alternating backgrounds in wide tables.
- ✅ **Settings**: Settings window with a toolbar of tabs; sensible defaults.
- 🟡 Finder brings a **floating sidebar** (controversial: the "double bezel" effect criticized on Reddit). Apple's own apps don't always match each other (Terminal with a compact title bar vs. apps with a full header) — avoid mixing your own chrome styles.

### Example: primary navigation with sidebar 🟡

```swift
import SwiftUI

// ═══════════════════════════════════════════════════════════════════
// WHEN: a Mac app with several sections — the sidebar is the canonical
// primary navigation (the iPhone tab bar's intent travels here).
// LIMITS: in Tahoe the sidebar is system Liquid Glass: don't paint
// opaque backgrounds or stack custom glass over its own.
// ═══════════════════════════════════════════════════════════════════

struct Sidebar: View {
    @State private var selection: Section? = .today

    var body: some View {
        // On Mac, three columns is the canonical pattern: sidebar + content + inspector. 🟡
        NavigationSplitView {
            List(Section.all, selection: $selection) { section in
                Label(section.title, systemImage: section.icon)
            }
            .navigationSplitViewColumnWidth(min: 180, ideal: 220)
            // .navigationTitle goes in the content column, not the sidebar. ✅
        } detail: {
            if let selection {
                SectionView(section: selection)
            } else {
                Text("Select a section")
                    .foregroundStyle(.secondary)
            }
        }
        .inspector(isPresented: .constant(false)) {
            // Trailing panel for the selected item's details. ✅
            Text("Inspector")
        }
    }
}
```

## Mac controls and conventions ✅

- ✅ Controls: default size **28 pt** on Mac (not 44); checkboxes for selection in sets, steppers for numbers.
- ✅ **Pointer and keyboard first**: precise targets, hover states, full keyboard navigation, rich shortcuts; Mac conventions (drag-and-drop, Services, context menus).
- ✅ Drag & drop between apps; services; Touch ID where applicable.
- 🟡 Spotlight in Tahoe **replaces Launchpad**: opens apps, searches files, clipboard history (24 h), and runs **Actions** (App Intents: send email, timer, note, reminder…) without opening the app. Consequence: model central commands as App Intents on Mac too.
- 🟡 Mac widgets follow the iOS widget rules (glanceable, deep links, safe in tint/clear; see `ios.md`) and also live on the **desktop behind windows** — verify legibility with reduced desktop opacity. On Mac there are no accessory families.

## macOS vs. iOS differences ✅

- ✅ Same app, **different expression**: the Mac sidebar becomes a tab bar on iPhone; the intent travels, the UI doesn't.
- ✅ Features that change shape: Live Activities (iOS) → complications (watchOS); menu bar commands (Mac) → toolbar items (iPad).
- ✅ **No Dynamic Type on macOS** — type sizing follows Mac conventions, not iOS's.
- ✅ Dense, informative layouts are expected and welcome on Mac (the opposite of iOS, where per-screen simplicity rules).
- ✅ **Handoff** and **Continuity**: start on one device, continue on another; shared state.

### Do / don't pairs — macOS

1. **Menu bar as the canonical home**
   - ✅ **DO:** every app action exists as a menu command with a discoverable shortcut (`CommandMenu` + `keyboardShortcut`); think "menu first".
   - ❌ **DON'T:** leave functionality only in toolbars or view buttons: on Mac, what isn't in a menu barely exists.

2. **Transparency not assumed**
   - ✅ **DO:** legibility in the menu bar with both transparent (Tahoe default) and opaque (Reduce Transparency or the Settings toggle) backgrounds: template icons and contrast measured in both.
   - ❌ **DON'T:** assume a background exists (text that only reads over the wallpaper) or paint your own opaque background that kills the system's glass.

3. **System window chrome**
   - ✅ **DO:** native traffic lights and chrome; container-derived concentric radii; one window = one task.
   - ❌ **DON'T:** reinvent the title bar, hardcode corner radii, or stack custom glass over system toolbars/sidebars.

4. **Tinted/clear icons**
   - ✅ **DO:** author in Icon Composer (square 1024 layers, no pre-rendered mask); brand recognizable in grayscale.
   - ❌ **DON'T:** depend on color alone for the icon's identity: in Tinted/Clear the color is gone.

5. **Mac density vs. iOS simplicity**
   - ✅ **DO:** use the big screen: trailing inspector, tables with sortable columns, multiple windows.
   - ❌ **DON'T:** port the iPhone screen 1:1 (16 pt margins, one centered column, tab bar): on Mac it feels empty and on iOS a Mac sidebar is unusable.

See also: `ios.md`, `watchos.md`, `../components/navigation.md`, `../materials/liquid-glass.md`.
