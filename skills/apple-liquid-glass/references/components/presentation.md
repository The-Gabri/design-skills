# Presentation and modality

**Verification legend** (applies to each rule and snippet):
- ✅ = direct HIG rule or official Apple documentation, confirmed in ≥2 independent sources.
- 🟡 = consistently documented in ≥3 sources, no verbatim Apple quote at hand.
- ⚠️ = doubtful / single source / disagreeing communities — not dogma.

Modality doctrine: **one modal at a time**, simple bounded tasks, obvious dismiss, confirm before losing changes. **Always choose the lightest form that serves.**

🟡 Choose the lightest form that fits: inline → sheet/menu/popover → full-screen/alert. Low-friction modals (sheets, popovers, menus) block the rest of the app but don't demand a yes/no decision; high-friction modals (alerts, confirmation dialogs) demand a decision — reserve them for genuinely consequential or destructive moments. **Never leave the person trapped:** every modal needs an obvious exit (Done/Cancel/Close/swipe).

---

## Decision map ✅

| I need | Use | Why |
|---|---|---|
| Create/edit, form, related list | **sheet** | Dismissible, keeps the context underneath |
| Required first-run flow, immersive task (camera, video, onboarding) | **fullScreenCover** | Blocks return until explicit dismiss |
| Light options anchored to a control (iPad-friendly) | **popover** | Non-modal in regular width; becomes a sheet in compact |
| Confirm a destructive or significant action | **confirmationDialog** | Action-oriented, supports several buttons |
| Critical info requiring acknowledgment | **alert** | Blocking, minimal, impossible to ignore |
| Pick from a short list, non-destructive | **confirmationDialog** or **Menu** | Dialog for lists tied to a trigger; Menu for a persistent control |

🟡 The most common mistake: `fullScreenCover` for an ordinary form — it takes away the easy exit a sheet gives for free.

## Sheets ✅/🟡

- 🟡 **A sheet is a card that rises for a self-contained subtask** (create, edit, configure) keeping the context visible behind.
- ✅ **Only one sheet at a time from the main interface.** HIG quote: *"Display only one sheet at a time from the main interface. If something people do within a sheet results in another sheet appearing, close the first sheet before displaying the new one."*
- 🟡 **Resizable detents: `.medium` and `.large`** (the API also offers `.fraction` and `.height`). Choose detents per the content; `.medium` for progressive disclosure (e.g. Share).
- ✅ **Include the grabber in a resizable sheet.** HIG quote: *"Include a grabber in a resizable sheet. A grabber shows people that they can drag the sheet to resize it; they can also tap it to cycle through the detents."* It works with VoiceOver to resize without seeing the screen. (The 36×5pt geometry is community convention; Apple describes it only as "a small horizontal indicator".)
- ✅ **Buttons: Cancel at the leading edge, Done at the trailing edge** (in the sheet's top toolbar). HIG quote: *"for sheets with a single view, the Cancel button belongs on the leading edge of the top toolbar. When present, the Done button belongs on the trailing edge."* **If there's Done, there's always Cancel** (rule added March 2026): *"Provide an alternative to the Done button. If you provide a Done button, always pair it with a Cancel button… Relying solely on the Done button implies that completing the task is the only way to exit the sheet, which can feel restrictive or misleading."* **Never all three together** (Cancel + Done + Back): Back "isn't intended to dismiss a sheet" — in multi-step flows, from step 2 on the Cancel is replaced by Back.
- 🟡 **Swipe-to-dismiss yes, but intercept it if there are unsaved changes** (`interactiveDismissDisabled`) and confirm the discard instead of losing input silently.
- ✅ **Confirm before discarding unsaved changes.**
- 🟡 **iOS 26:** sheets are glass at partial height and turn opaque when expanded; concentric radii with the screen; half sheets get inset from the edge so the content peeks out. Don't fight the system's material (remove opaque `.background()`s).
- 🟡 **On iPad, prefer page sheet / form sheet styles**: default size centered over a dimmed background. macOS: rounded cards over the darkened parent window.

## Alerts ✅/🟡

- ✅ **Critical + actionable, nothing else**: errors requiring attention, destructive confirmations, info demanding acknowledgment. Sparing use.
- 🟡 **When NOT to use an alert:** never at app launch, never purely informational, never for routine undoable deletes. Abuse trains the person to dismiss without reading.
- ✅ **Title = what happened and why**, ≤1–2 lines, **without the word "Error"**. Concrete message, never "An error has occurred".
- ✅ **1–3 buttons with verbs** ("Delete", "Retry", "View all"); "OK" only for pure info. **Cancel always cancels**, goes leading/bottom, **never the default**; the destructive one is red and **never the default**. **No custom content or controls inside** — if you need them, use a sheet.
- ⚠️ **~270pt wide** appears in a single source (the historical HIG measure for alerts): take it as a mockup reference, not verified dogma here.

## Confirmation dialogs (action sheets) ✅/🟡

- 🟡 **A confirmation dialog is a set of options IN RESPONSE to an action the person just took intentionally** ("Delete draft?"): the follow-up to an intentional but risky tap — **not an alert**.
- ✅ **The destructive one at the top of the group in destructive style, Cancel separate at the bottom.**
- 🟡 On iPhone it rises from the bottom; on iPad/Mac it appears as a popover near the trigger.
- 🟡 **Decision rule:** app interrupts with critical info? → alert. User tapped something risky and must choose? → confirmation dialog. Quick pick from a short non-destructive list? → confirmation dialog or Menu.
- ✅ Difference in one sentence: **alert = "something needs you right now (error/notice)"** → 1–2 buttons; **confirmationDialog = "what do you want to do?"** → list of actions.

## Popovers (iPad) ✅/🟡

- 🟡 **Transient panel anchored to its trigger with an arrow, only in regular width (iPad/Mac).** For a focused set of options/controls tied to a specific element. Dismisses on outside tap. **On iPhone (compact width) they adapt to sheets: design the content to survive both.**
- 🟡 **Never in cascade** (one at a time); **never for warnings**; save work on auto-dismiss.
- ⚠️ **~320pt minimum** popover width appears in a single source — useful practical convention, not a verified quote.
- 🟡 **Never nested.** macOS: they can be detachable.

## Full-screen 🟡

- 🟡 **Full-screen ONLY for immersive content or tasks demanding the whole screen**: camera, video, photo, full editor, blocking first-run onboarding, complex multi-step flow. Everything else is a sheet. Provide an obvious Done/Cancel/Close. Use it less than sheets.
- 🟡 **The most common misuse:** using `fullScreenCover` for an ordinary create/edit form — it takes away the easy exit a sheet gives for free.

## Share sheet 🟡

- 🟡 **For sharing/exporting use the system share sheet** (it brings AirDrop, Messages, Markup, and third-party actions). Don't build a custom share grid.

---

## SwiftUI examples

### 1. Sheet with `.medium` and `.large` detents, visible grabber ✅

**When:** create/edit form, filters, or auxiliary content where the person must keep the context underneath visible. The grabber communicates draggability.

```swift
import SwiftUI

struct CreateNoteView: View {
    @State private var showSheet = false

    var body: some View {
        Button("New note") { showSheet = true }
            .sheet(isPresented: $showSheet) {
                NoteForm()
                    // The allowed heights: half screen and full screen
                    .presentationDetents([.medium, .large])
                    // The drag "handle": mandatory when there's more than one detent
                    .presentationDragIndicator(.visible)
            }
    }
}

struct NoteForm: View {
    @Environment(\.dismiss) private var dismiss
    @State private var text = ""

    var body: some View {
        NavigationStack {
            Form {
                TextField("Write your note", text: $text)
            }
            .navigationTitle("New note")
            .toolbar {
                // "Cancel" top-left: discards without saving
                ToolbarItem(placement: .cancellationAction) {
                    Button("Cancel") { dismiss() }
                }
                // "Save" top-right, bold: confirms the action
                ToolbarItem(placement: .confirmationAction) {
                    Button("Save") {
                        save()
                        dismiss()
                    }
                }
            }
        }
    }

    private func save() {
        // Persist the note
    }
}
```

**Design notes:**
- The `.cancellationAction` / `.confirmationAction` placements are semantic: iOS positions them (top-left/right), bolds them, and makes them keyboard-accessible. Don't use `.topBarLeading` for this.
- In iOS 26 the sheet already has a Liquid Glass background by default: don't add a custom `presentationBackground` unless the content truly demands it.
- Availability: `presentationDetents` and `presentationDragIndicator` require iOS 16+.

### 2. System alert (critical info requiring a response) ✅

**When:** something failed badly (network error on save, needed permission) or there's critical info the person must explicitly acknowledge. The alert is **blocking and minimal**: 1–2 buttons, no lists.

```swift
import SwiftUI

struct SaveDocumentView: View {
    @State private var showError = false
    @State private var errorMessage = ""

    var body: some View {
        Button("Save") {
            save()
        }
        // System alert: short title + explanatory message
        .alert("Couldn't save", isPresented: $showError) {
            Button("Retry") { save() }
            // The .cancel role gives it the right style and preferred position
            Button("Discard", role: .cancel) { }
        } message: {
            Text(errorMessage)
        }
    }

    private func save() {
        do {
            try persist()
        } catch {
            // Concrete message, nothing like "An error has occurred"
            errorMessage = "Check your connection and try again."
            showError = true
        }
    }

    private func persist() throws {
        // Save logic
    }
}
```

### 3. confirmationDialog (choosing between several actions) ✅

**When:** the person picks between several actions (confirming a delete, deciding what to do with an attachment, changing an option). Replaces the old action sheet. For destructive actions, the destructive button goes first.

```swift
import SwiftUI

struct PhotoListView: View {
    @State private var photoToDelete: Photo?
    @State private var showConfirmation = false

    var body: some View {
        List(photos) { photo in
            PhotoRow(photo)
                .swipeActions(edge: .trailing) {
                    Button(role: .destructive) {
                        // Prepare the photo and present the dialog
                        photoToDelete = photo
                        showConfirmation = true
                    } label: {
                        Label("Delete", systemImage: "trash")
                    }
                }
        }
        // ⚠️ Attach the confirmationDialog to the element that triggers it
        // (one source mentions that in Liquid Glass the animation "morphs"
        // from the origin; the docs only state it presents near the trigger
        // on iPad/Mac — anchoring it to the trigger is good practice)
        .confirmationDialog(
            "Delete this photo?",
            isPresented: $showConfirmation,
            titleVisibility: .visible
        ) {
            Button("Delete photo", role: .destructive) {
                if let photo = photoToDelete { delete(photo) }
            }
            Button("Cancel", role: .cancel) { }
        } message: {
            // The message explains the irreversible consequence
            Text("It will be deleted from all your devices and you won't be able to recover it.")
        }
    }

    private func delete(_ photo: Photo) {
        // Delete logic
    }
}
```

**Alert vs. confirmationDialog, in one sentence:** alert = "something needs you right now (error/notice)" → 1–2 buttons; confirmationDialog = "what do you want to do?" → list of actions.

### 4. Popover anchored to a button (iPad / regular width) ✅

**When:** supplementary info or a secondary action attached to the control that opened it, on iPad (regular width). Not modal: dismisses on outside tap. On iPhone (compact) the same code shows as a partial-screen sheet.

```swift
import SwiftUI

struct ToolbarBar: View {
    @Environment(\.horizontalSizeClass) private var horizontalSize
    @State private var showInfo = false

    var body: some View {
        Button("Details") { showInfo = true }
            // The popover is born ANCHORED to the button: don't present it from a distant ancestor
            .popover(isPresented: $showInfo) {
                InfoCard()
                    // Fixed size and self-contained content: no infinite scrolling
                    .frame(width: 320, height: 240)
            }
    }
}
```

**Design notes:**
- In compact width (portrait iPhone) the popover presents as a sheet: if your content doesn't work as a sheet, choose `.sheet` directly in that case (`horizontalSize == .compact`).
- The popover must not contain long flows or deep navigation: for that you want a sheet.

### 5. ❌ What NOT to do

**5a. Sheet inside a sheet.** A sheet opening another sheet on top breaks the mental model ("where am I?"), the dismiss gesture becomes ambiguous (do I close the top one or both?), and in iOS 26 the second sheet covers the first one's glass.

```swift
import SwiftUI

// ❌ DON'T DO THIS: a sheet opening another sheet on top
struct OuterView: View {
    @State private var showFirst = false

    var body: some View {
        Button("Open") { showFirst = true }
            .sheet(isPresented: $showFirst) {
                VStack {
                    Text("First sheet")
                    ButtonOpeningSecondSheet() // ← modal over modal: disorients
                }
            }
    }
}
```

**✅ Instead:** one presentation with internal navigation (`NavigationStack` with `navigationDestination`), or chain the second step after dismissing the first.

```swift
// ✅ Instead: a single sheet with an internal flow
.sheet(isPresented: $showSheet) {
    NavigationStack {
        StepOne()
            .navigationDestination(for: Route.self) { route in
                switch route {
                case .stepTwo: StepTwo()
                }
            }
    }
    .presentationDetents([.medium, .large])
    .presentationDragIndicator(.visible)
}
```

**5b. Alert for a non-critical decision.**

```swift
// ❌ DON'T DO THIS: blocking alert for something trivial
.alert("Turn on dark mode?", isPresented: $showAlert) {
    Button("Yes") { enableDarkMode() }
    Button("No", role: .cancel) { }
}
```

The alert is the system's most aggressive interruption; using it for a routine preference trains the person to dismiss it unread, and when a real error arrives they'll ignore it too. **Do this instead:**
- Reversible preference → direct `Toggle` in the UI (no confirmation).
- Pick among several → `confirmationDialog` or `Menu`.
- Only use `.alert` for a real error, a data-loss risk, or an irreversible decision demanding full attention.

---

## Do / don't pairs

1. **Detents**
   - ✅ **DO:** `.presentationDetents([.medium, .large])` + `.presentationDragIndicator(.visible)` for draggable sheets; the grabber announces the gesture.
   - ❌ **DON'T:** draggable sheet with no grabber — the person won't discover they can drag and the sheet looks broken/trapped.

2. **Sheet buttons**
   - ✅ **DO:** `.cancellationAction` for Cancel and `.confirmationAction` for Save/Done in the toolbar: position, bold, and keyboard shortcuts for free. If there's Done, there's always Cancel.
   - ❌ **DON'T:** loose text buttons in the sheet's body for Cancel/Save; they break the platform convention.

3. **Alert vs confirmationDialog**
   - ✅ **DO:** `.alert` for critical errors or notices demanding acknowledgment (1–2 buttons, concrete message, never "An error has occurred").
   - ❌ **DON'T:** `.alert` with a list of 3+ options or for routine decisions — that's `.confirmationDialog`'s or a direct `Toggle`'s job.

4. **confirmationDialog**
   - ✅ **DO:** destructive button with `role: .destructive` first, `role: .cancel` to exit, and a `message` explaining the irreversible consequence.
   - ❌ **DON'T:** confirmation dialogs for reversible actions ("Are you sure you want to turn on notifications?") — friction without reason.

5. **Popover**
   - ✅ **DO:** `.popover` anchored to the button that triggers it, small self-contained content (a reasonable fixed `frame`), on iPad/regular width.
   - ❌ **DON'T:** a popover with a long flow or deep navigation inside; nor on iPhone if the sheet fallback breaks the design — use `.sheet` directly.

6. **Nesting**
   - ✅ **DO:** a single level of modal presentation; extra steps with `navigationDestination` inside the same sheet.
   - ❌ **DON'T:** sheet inside sheet, or alert over confirmationDialog over sheet — each additional modal layer multiplies disorientation.

**API notes (for whoever maintains this reference):**
- Verified signatures: `.sheet(isPresented:onDismiss:content:)`, `.presentationDetents(_:selection:)`, `.presentationDragIndicator(_:)`, `.alert(_:isPresented:actions:message:)`, `.confirmationDialog(_:isPresented:titleVisibility:actions:message:)` with `titleVisibility: .visible`, `.popover(isPresented:content:)`, `ToolbarItemPlacement.cancellationAction` / `.confirmationAction`, `Button(_:role:action:)` with `.destructive` / `.cancel` roles ✅
- `confirmationDialog(_:item:...)` (iOS 27) exists per recent sources but **isn't used here**: the skill targets iOS 26.

See also: `navigation.md` (tab bar and toolbars), `controls.md` (menus and context menus).
