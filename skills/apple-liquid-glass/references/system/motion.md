# Motion in depth 🟡

Copy-pasteable rules and examples (SwiftUI + CSS) for Apple-feeling
animation.

Legend: ✅ = direct HIG/official-doc quote in ≥2 sources; 🟡 = consistent
in ≥3 independent sources; ⚠️ = heuristic, doubtful, or single source.

> **Note on springs ⚠️**: the HIG **does not publish canonical spring
> constants** for third-party implementations. The `response`/`damping`
> numeric values below are **perceptual heuristics**, not Apple's official
> specification.

---

## 1. Apple's spring model 🟡

Apple replaced the physical triplet (mass/stiffness/damping) with two
designer-oriented parameters. Attributed to the **"Designing Fluid
Interfaces" (WWDC18)** talk in 6+ sources; no direct quote verified.

- **damping ratio**: controls overshoot. `1.0` = critically damped (smooth
  settle, no bounce); `< 1.0` = bounce, lower = springier.
- **response**: seconds to reach the target. Lower = faster. **Not
  "duration"**: a spring has no fixed duration; the settle time *emerges*
  from the parameters.

Values Apple uses in the system (identical table in 6 sources) 🟡:

| Interaction | damping | response |
|---|---|---|
| Move / reposition (e.g. PiP) | 1.0 | 0.4 |
| Rotation | 0.8 | 0.4 |
| Drawer / sheet | 0.8 | 0.3 |

**House rule ✅**: **damping 1.0 by default for almost everything**
(elegant, non-distracting); bounce (~0.8) **only** when the gesture
contributed momentum (flick, drag with velocity). Bounce on a menu that
appeared by fade = bad; bounce on a card you flung with your finger = good.

### E1 — Default spring: critically damped ✅

**When to use it:** starting point for ANY state change caused by a tap
without momentum (opening/closing views, toggles, selections, tabs).
`dampingFraction 1.0` = critically damped: reaches the target in the
shortest time WITHOUT overshoot (WWDC18: "start with 100% damping").

```swift
import SwiftUI

extension Animation {
    static let uiDefault = Animation.spring(response: 0.35, dampingFraction: 1.0)
}

struct SwitchDemo: View {
    @State private var active = false

    var body: some View {
        Capsule()
            .fill(active ? .green : .gray.opacity(0.3))
            .frame(width: 64, height: 36)
            .overlay(alignment: active ? .trailing : .leading) {
                Circle().fill(.white).padding(4)
            }
            .onTapGesture {
                withAnimation(.uiDefault) { active.toggle() }
            }
    }
}

// Verified signature: Animation.spring(response:dampingFraction:blendDuration:)
// (defaults response: 0.55, dampingFraction: 0.825, blendDuration: 0).
// dampingFraction = 1.0 → no overshoot; > 1 overdamped;
// < 1 underdamped (bounces); 0 oscillates forever (never use 0). ✅
```

### E2 — Spring with bounce (~0.8) after gesture momentum ✅

**When to use it:** on RELEASING a gesture with momentum (flick to dismiss,
sheet snap). The gesture's momentum is rewarded with a little bounce
(WWDC18: in the Music app, dismissing "Now Playing" with a swipe uses 80%
damping; opening it with a tap, 100%).

```swift
import SwiftUI

struct DraggableCard: View {
    @Environment(\.accessibilityReduceMotion) private var reduceMotion
    @State private var offset = CGSize.zero

    var body: some View {
        RoundedRectangle(cornerRadius: 16)
            .fill(.blue)
            .frame(width: 200, height: 120)
            // No animation here: while dragging the view follows the finger 1:1.
            .offset(offset)
            .gesture(
                DragGesture()
                    .onChanged { value in
                        offset = value.translation
                    }
                    .onEnded { _ in
                        // With Reduce Motion, return without animation.
                        withAnimation(reduceMotion ? nil : .spring(response: 0.35, dampingFraction: 0.8)) {
                            offset = .zero
                        }
                    }
            )
    }
}

// Modern alternative (iOS 17+): .spring(duration: 0.4, bounce: 0.2) —
// bounce goes from 0 (critically damped) to 1 (max bounce). ✅
```

### E3 — `withAnimation` for state changes ✅

**When to use it:** wrap the EXACT mutation the user's interaction caused.
Explicit > implicit: you know what animates and when. If the user taps
mid-animation, the spring resumes from the current on-screen velocity —
never restarts from zero or blocks input.

```swift
import SwiftUI

struct PanelDemo: View {
    @State private var open = false

    var body: some View {
        VStack(spacing: 16) {
            Button(open ? "Close" : "Open") {
                withAnimation(.spring(response: 0.4, dampingFraction: 1.0)) {
                    open.toggle()
                }
            }
            if open {
                Text("Panel content")
                    .padding()
                    .background(.quaternary, in: RoundedRectangle(cornerRadius: 12))
            }
        }
    }
}

// Signature: withAnimation(_ animation: Animation? = .default,
// _ body: () throws -> Result). Accepts nil (useful for neutralizing
// with Reduce Motion). ✅
```

### E4 — `.transition` for appearing/disappearing ✅

**When to use it:** views entering/leaving the hierarchy (banners, cards,
overlays). ASYMMETRIC enter and exit: slides in from the bottom with fade;
exits with fade only (exits are usually quicker).

```swift
import SwiftUI

struct NoticeDemo: View {
    @State private var visible = false

    var body: some View {
        VStack {
            Button("Show notice") {
                // The transition only runs if the change happens inside
                // withAnimation (or under .animation on an ancestor).
                withAnimation(.spring(response: 0.4, dampingFraction: 1.0)) {
                    visible.toggle()
                }
            }
            if visible {
                Text("Important notice")
                    .padding()
                    .background(.yellow.opacity(0.2), in: RoundedRectangle(cornerRadius: 12))
                    .transition(.asymmetric(
                        insertion: .move(edge: .bottom).combined(with: .opacity),
                        removal: .opacity
                    ))
            }
        }
    }
}

// Verified pieces: .transition(_:), .asymmetric(insertion:removal:),
// .combined(with:), .move(edge:), .opacity, .scale(scale:), .slide, .push. ✅
```

---

## 2. Interruptibility — the golden rule 🟡

**Every animation interruptible and re-directable at any moment**: animate
from the *current on-screen value* (and its velocity), never block or
ignore user input. System animations are additive: a gesture mid-animation
resumes from where it is.

- ✅ **Velocity handoff**: the gesture's release velocity transfers to the
  spring to avoid velocity discontinuities.
- ✅ Respond to **pointerdown**, not release; direct manipulation is 1:1
  (the element follows the pointer with the grab offset); limits with
  **rubber-banding** (progressive resistance), never hard stops.
- 🟡 Don't block input behind an animation; never make motion the only
  information channel.
- 🟡 Nothing on autoplay the user can't stop; auto-advancing carousels
  start paused under `prefers-reduced-motion`.
- ⚠️ In pure CSS there are no truly re-targetable springs: if
  interruptibility matters (drag, sheets), use a spring library
  (Motion/Framer) or WAAPI with your own model.
- 🟡 For gestures the user can reverse midway, use library springs
  (they re-target with velocity) instead of keyframes (they restart from
  zero). Decompose 2D motion into independent X and Y springs.

---

## 3. Hero transitions: `matchedGeometryEffect` 🟡/✅

- ✅ `matchedGeometryEffect(id:in:properties:anchor:isSource:)` exists in
  SwiftUI (documented API).
- 🟡 Pattern: the element "travels" between screens keeping its identity
  (same `id` in the same `Namespace`); the transition communicates spatial
  relationship instead of a cut. Requires animation applied to the state
  change that toggles visibility.
- ⚠️ On the web: equivalent with FLIP (First-Last-Invert-Play) or the View
  Transitions API (`document.startViewTransition()` + shared
  `view-transition-name`). Same idea, different mechanics.

### E5 — Shared element between positions ✅

**When to use it:** the SAME element traveling between two positions/states
(segment indicator, mini-player → detail screen). Same id + same Namespace =
matched pair; SwiftUI interpolates the frame from one to the other.

```swift
import SwiftUI

struct SegmentsDemo: View {
    @Namespace private var indicator
    @State private var selection = "Week"
    private let options = ["Day", "Week", "Month"]

    var body: some View {
        HStack(spacing: 4) {
            ForEach(options, id: \.self) { option in
                Button {
                    withAnimation(.spring(response: 0.35, dampingFraction: 1.0)) {
                        selection = option
                    }
                } label: {
                    Text(option)
                        .font(.subheadline.weight(.semibold))
                        .padding(.horizontal, 16)
                        .padding(.vertical, 8)
                        .background {
                            if selection == option {
                                Capsule()
                                    .fill(.background)
                                    .matchedGeometryEffect(id: "indicator", in: indicator)
                            }
                        }
                }
                .buttonStyle(.plain)
            }
        }
        .padding(4)
        .background(.quaternary, in: Capsule())
    }
}

// Rules: only ONE view with the same id visible at once; stable ids
// (never array indexes); the state change goes in withAnimation.
// ⚠️ Modifier order (one source, Chris Eidhof): apply
// .matchedGeometryEffect BEFORE .frame on the flexible view, or the
// outer frame will pin the size and the animation won't interpolate well.
```

---

## 4. Durations ⚠️

Community guidance (Emil Kowalski / animation review standards, consistent
in ≥3 sources, **no Apple origin**):

| Element | Duration |
|---|---|
| Press feedback | 100–160ms |
| Tooltips, small popovers | 125–200ms |
| Dropdowns, selects | 150–250ms |
| Modals, drawers | 200–500ms |
| Marketing / explainer | may be longer |

Rule: **functional UI, under 300ms**. The more frequent the element, the
shorter and subtler the animation.

### E6 — `transition` with spring-like cubic-bezier (CSS) ✅/⚠️

**When to use it:** UI states that should feel iOS-like (hover, popovers,
sheets, dialogs). Web approximation of the critically damped spring:
strong ease-out, smooth arrival, NO bounce (CSS doesn't do real physics).

```css
:root {
  --ease-out:    cubic-bezier(0.23, 1, 0.32, 1);  /* UI: entrances, exits, state changes */
  --ease-in-out: cubic-bezier(0.77, 0, 0.175, 1); /* motion/morphing on screen */
  --ease-drawer: cubic-bezier(0.32, 0.72, 0, 1);  /* ⚠️ iOS feel for drawers/sheets */
}

/* ⚠️ A real spring can't be cloned with cubic-bezier (no bounce or
   re-targeting), but these curves give the *iOS feel*. */
/* ⚠️ ease-drawer (0.32, 0.72, 0, 1) comes from Ionic Framework (popularized
   by Vaul/Emil Kowalski), not from Apple; at 300–500ms it "feels" like
   an iOS sheet. It's imitation, not spec. */

.dialog {
  opacity: 0;
  transform: translateY(12px) scale(0.98);
  transition:
    opacity 200ms var(--ease-out),
    transform 280ms var(--ease-drawer);
}
.dialog.open { opacity: 1; transform: translateY(0) scale(1); }

/* Guideline map: micro-feedback 100–160ms, popovers/menus 150–250ms,
   sheets/modals 250–500ms. Exits slightly faster than entrances. 🟡 */
/* Decision tree (community consensus): enters/leaves → ease-out
   (starts fast, feels immediate); moves/transforms on screen → ease-in-out;
   hover/color → ease; constant motion (marquees, progress) → linear.
   ⚠️ ease-in FORBIDDEN in UI (starts slow exactly when the user is watching).
   For reversible transitions, mirror the curve so the return path matches. */
```

### E7 — Mapping to Framer Motion / Motion ⚠️

**When to use it:** on the web, when interruptibility matters (drag,
re-grabbable sheets). Practical analogy, not mathematical equivalence.

```js
// WHEN: default — critically damped (damping 1.0) ⚠️
animate(el, { y: 0 }, { type: "spring", bounce: 0, duration: 0.4 });

// WHEN: with gesture momentum — a little bounce (damping ~0.8) ⚠️
animate(el, { y: target }, { type: "spring", bounce: 0.2, duration: 0.4 });

// ⚠️ bounce: 0 ≈ damping 1.0; bounce: 0.1–0.3 ≈ damping ~0.8;
// duration ≈ response. Motion derives internal stiffness/damping
// from those two values.
```

---

## 5. Micro-interactions 🟡/⚠️

- 🟡 **Pressed state**: scale ~0.97 (range 0.95–0.98) on press + slight
  opacity drop, 80–160ms, minimal bounce on release. Applies to any
  pressable element.
- ⚠️ Never `scale(0)` in appearances: start at `scale(0.9–0.97)` +
  `opacity: 0` ("nothing in the real world appears from nothing").
- ⚠️ Popovers: `transform-origin` at the trigger, not the center.
  Modals: centered, origin center.
- ⚠️ Scroll parallax/reveal: small offsets (±8–24px); reveals with fade +
  short translate (12–24px); entrances with `translateY` of 10–22px, never
  100px.
- 🟡 Web techniques: `animation-timeline: view()/scroll()` with `@supports` +
  IntersectionObserver fallback; for continuous scrub, a damped scroll value
  (lerp) in rAF — never tie transforms directly to raw scroll. On mobile,
  natural scroll with parallax, not aggressive scroll-snap.

```css
/* WHEN: any pressable element on the web. Minimum scale 0.95–0.97,
   never 0 (E7). 🟡/⚠️ */
.button {
  transition: transform 120ms ease-out, opacity 120ms ease-out;
}
.button:active { transform: scale(0.96); opacity: 0.85; }
```

---

## 6. `prefers-reduced-motion` 🟡/✅

Base: WCAG 2.2 SC 2.3.3 + the HIG Motion guide (Apple asks to respect
"Reduce Motion"); the substitution table is community consensus.

| With motion | Reduced variant |
|---|---|
| Slide from the edge | Crossfade ~100ms |
| Modal with scale + fade | Fade only ~100ms |
| Staggered list reveal | All at once or instant |
| Parallax | Nothing — fixed layer |
| Background video on autoplay | Static frame, play on demand |
| Auto-advancing carousel | Manual control only |
| Error shake | Static error style + move focus |
| Route transition | Instant |
| Skeleton shimmer | Static neutral blocks |

**What to keep** (not vestibular triggers): opacity fades, color changes,
blur, few-pixel moves, spinners/progress (no shimmer), brief press feedback.

### E8 — Reduce Motion in SwiftUI ✅

**When to use it:** in EVERY custom animation. Rule: crossfades/opacity are
still allowed; neutralize large translations, scale-from-zero, parallax, and
loops. The `reduceMotion ? nil : <animation>` pattern is the standard idiom.

```swift
import SwiftUI

struct HeroDemo: View {
    @Environment(\.accessibilityReduceMotion) private var reduceMotion
    @State private var appeared = false

    var body: some View {
        Text("Welcome")
            .font(.largeTitle.bold())
            .opacity(appeared ? 1 : 0)
            // With Reduce Motion: no displacement, crossfade only.
            .offset(y: appeared ? 0 : (reduceMotion ? 0 : 24))
            .animation(reduceMotion ? nil : .spring(response: 0.4, dampingFraction: 1.0), value: appeared)
            .onAppear { appeared = true }
    }
}
```

### E9 — `prefers-reduced-motion` with crossfade fallback (CSS) ✅

**When to use it:** MANDATORY after every rule with motion. With Reduce
Motion the slide becomes a crossfade: feedback is kept, vestibular motion
(translations, scales, parallax) is removed.

```css
/* WHEN: after every rule with motion. General pattern (scoped override):
   under reduced, transform: none and the transition becomes a brief opacity. */
.dialog {
  opacity: 0;
  transform: translateY(12px);
  transition: opacity 200ms ease-out, transform 280ms var(--ease-drawer, cubic-bezier(0.32, 0.72, 0, 1));
}
.dialog.open { opacity: 1; transform: translateY(0); }

@media (prefers-reduced-motion: reduce) {
  .dialog {
    transform: none;                      /* kills the displacement */
    transition: opacity 150ms ease-out;    /* fade only */
  }
  .dialog.open { transform: none; }
}
```

**Recommended pattern — motion opt-in** (the final visible state is the
base style; motion only exists under `no-preference`):

```css
.card { /* static styles */ }
@media (prefers-reduced-motion: no-preference) {
  .card { transition: transform 300ms cubic-bezier(0.23, 1, 0.32, 1); }
}
```

- 🟡 Don't use `* { animation-duration: 0.01ms !important }` as the only
  strategy: it kills safe fades and can speed up JS animations. In JS:
  `matchMedia('(prefers-reduced-motion: reduce)')` to not start
  IntersectionObserver reveals or autoplay when active.
- Rule: *reduce/substitute motion, never delete the message* —
  the modal that slid in now appears with a fade, not with nothing.

---

## Do / don't pairs

**D1 — Interruptible vs. blocking animations ✅**
- ✅ **Do:** springs for everything the user can touch or reverse. If they
  change their mind mid-animation, the spring blends the in-flight velocity
  into the new target: the gesture always rules. (WWDC18: "animations must
  be re-directable mid-flight and never block input".)
- ❌ **Don't:** fire-and-forget animations that ignore touches until done,
  or fixed-duration curves for reversible interactions (a closing sheet must
  be re-grabbable midway).

**D2 — Bounce only after gesture momentum ✅**
- ✅ **Do:** `dampingFraction: 1.0` (or `bounce: 0`) by default on
  touch-driven state changes. `~0.8` (or `bounce: 0.2–0.3`) only when
  releasing a gesture with momentum, to "reward" that momentum.
- ❌ **Don't:** decorative bounce on touch opens, navigation, or state
  changes without momentum — it distracts from the task (WWDC18: opening
  "Now Playing" with a tap = 100% damping; dismissing with a swipe = 80%).

**D3 — Nothing appears from nothing ✅**
- ✅ **Do:** minimum scale `0.9–0.95` + opacity, e.g.
  `.transition(.scale(scale: 0.95).combined(with: .opacity))`.
- ❌ **Don't:** `.scale` down to 0 (or `transform: scale(0)` in CSS): the
  element collapses to a point and "disappears into a black hole"; it feels
  broken.

**D4 — Explicit at the mutation; don't mix modes ✅**
- ✅ **Do:** `withAnimation` around the exact mutation the interaction
  caused; `.animation(_:value:)` only when a view must always animate
  changes of one specific value (e.g. a progress bar).
- ❌ **Don't:** implicit + explicit on the same property at once: the outer
  one wins but the implicit one also fires = unpredictable.

**D5 — During 1:1 drag, don't animate the tracked property ✅**
- ✅ **Do:** during the gesture, the view follows the finger without
  animation (raw `.offset`). The spring goes on the "chasing" property or
  on release.
- ❌ **Don't:** put `transition`/`animation` on the property tracking the
  finger: it adds lag and breaks the direct-manipulation illusion. Same on
  the web: no `transition` on the dragged property; easing only on release.

**D6 — Reduce Motion: substitute, don't delete ✅**
- ✅ **Do:** brief crossfade (~100ms) instead of slide/spring/parallax; the
  user still receives feedback of the change.
- ❌ **Don't:** remove all animation leaving abrupt cuts that disorient, or
  keep the motion "because it looks good".

**D7 — `matchedGeometryEffect`: one pair, stable ids ✅**
- ✅ **Do:** exactly one visible view per `id` inside the same
  `@Namespace`; stable, semantic ids (`"indicator"`, `"card"`).
- ❌ **Don't:** ids accidentally duplicated across namespaces, or array
  indexes as ids (identity becomes unstable and the interpolation jumps).

**D8 — Don't fire `withAnimation` inside `body` ⚠️**
- ✅ **Do:** fire animations from gestures, button actions, or
  `.onChange`.
- ❌ **Don't:** call `withAnimation` inside `body`: body runs on every
  render and the animation would re-fire arbitrarily.
- ⚠️ *One source (community SwiftUI guide); pattern broadly consistent
  with SwiftUI's render model, but not verified in official documentation.*

**D9 — Under Reduce Motion, the finger still rules ⚠️**
- ✅ **Do:** 1:1 finger tracking during a drag is NOT neutralized
  (neutralizing it would break the gesture itself); what substitutes to
  crossfade/instant is the *settle* on release and momentum flings.
- ⚠️ *One source (accessible motion guide); reasonable criterion consistent
  with "substitute, don't delete", but no direct Apple quote at hand.*

See also: `accessibility.md` (Reduce Motion/Transparency),
`../foundations/principles.md` (interaction principle), WWDC18
"Designing Fluid Interfaces".
