# The 8 Apple design principles

The current Human Interface Guidelines (HIG) principles: **Purpose, Agency, Responsibility, Familiarity, Flexibility, Simplicity, Craft, Delight**.

**Verification legend:** ✅ = direct quote or rule from the HIG / official docs confirmed in ≥2 sources; 🟡 = consistently documented in ≥3 sources; ⚠️ = approximation or unverified.

## Correct dating ✅

Re-introduced officially on **2026-06-08** at WWDC26 (session 250, "Principles of great design") and published on the HIG page `developer.apple.com/design/human-interface-guidelines/design-principles`. ✅

⚠️ **They are not from 2023.** Several outdated skills date them to 2023; no source found confirms it. Don't use that date.

## What's now obsolete ✅

- **Clarity / Deference / Depth**: those were the iOS 7 (2013) themes. Apple no longer lists them as principles. Skills still quoting them as "the three principles" are outdated. ✅
- **The 6 classics** (Aesthetic Integrity, Consistency, Direct Manipulation, Feedback, Metaphors, User Control) from the 2013 HIG: superseded by the 8-principle framework. Don't cite them as the official list. Their spirit lives on, redistributed among the new ones (🟡 approximation: User Control + Feedback → Agency + Familiarity; Metaphors + Consistency → Familiarity; Aesthetic Integrity → Craft + Delight; Direct Manipulation was subsumed into Agency).
- ⚠️ One minority source describes them as **7 principles** (Delight as a sub-theme of Craft). The official HIG and most sources list 8: keep 8.

## The 8 principles

### 1. Purpose — design with intent ✅

Every feature asks the person for time, attention, and trust. The principle is phrased as deciding **what NOT to build**: before designing the interface, clarify why the feature must exist.

- ✅ **Do:** the "razor test" — if removing an element loses nothing, cut it. The primary task obvious on open: a clear title, one primary action, a focused hierarchy.
- ❌ **Don't:** screens where secondary content, decoration, or extra controls compete with the app's main reason. No "just in case" features.

### 2. Agency — the person is in control ✅

The app responds to the user, not the other way around. Offer options instead of forcing a single path; make exploration, escape, correction, and recovery easy. Undo for mistakes; confirmation only for truly destructive, irreversible actions.

- ✅ **Do:** direct manipulation of content (drag, pinch), undo instead of confirm by default, clear exits from every mode, the ability to skip unnecessary guided flows, always-available cancel.
- ❌ **Don't:** forced paths with no shortcuts; destructive dead-ends with no way back ("Are you sure?" as the only safety net instead of undo); unclear system states.

### 3. Responsibility — act in people's best interest ✅

Privacy, permissions, security, and transparency as a *design principle*, not a legal footnote. A genuine novelty of the set (no direct equivalent in the classics) 🟡.

- ✅ **Do:** ask for the minimum data needed; explain why a permission is requested at the moment you request it; anticipate misuse (abuse cases); confirm consequential actions with system dialogs.
- ❌ **Don't:** collect data "just in case"; unexplained permissions; product claims you can't back up; automations the user didn't ask for and can't review.

### 4. Familiarity — build on what people already know ✅

Consistent metaphors and platform patterns. What looks the same must behave the same and live in the same place. Only break a pattern if you can demonstrate the new one is better.

- ✅ **Do:** use system components (tabs, sheets, alerts, menus, NavigationStack, Form, List) before inventing a custom one. A native control inherits accessibility, haptic feedback, and platform behavior for free. Clear feedback on state changes.
- ❌ **Don't:** reinvent a tab bar or sheet with different behavior "because it looks better"; break a familiar pattern without demonstrating the improvement; visual metaphors that don't hold up.

### 5. Flexibility — adapt to contexts and people ✅

Accessibility from the start, not as an add-on: different devices, input methods (touch vs. mouse vs. voice vs. keyboard), and the full spectrum of abilities. Personalization when no single layout serves.

- ✅ **Do:** accessibility from the first sketch (VoiceOver, Dynamic Type, Reduce Motion — see `../system/accessibility.md`); multiple input methods; preserve context across configuration changes; design by size classes, not device models.
- ❌ **Don't:** layouts hardcoded to one screen size; touch-only interactions with no alternative; accessibility as a "polish phase" before launch.

### 6. Simplicity — be clear and direct, not minimalist ✅

"Simplicity isn't minimalism": remove the unnecessary so the central purpose shines. Be concise (plain language, fewer steps) and clear (hierarchy: order, spacing, contrast). The common path first; the advanced stuff one level down.

- ✅ **Do:** the important things near and prominent; progressive disclosure (advanced features a tap away); concise labels; one primary action per screen.
- ❌ **Don't:** minimalism that amputates needed capability; junk-drawer screens with everything visible; flat hierarchies where everything competes with everything.

### 7. Craft — every detail is a decision ✅

Nothing is random: every spacing, timing, alignment, and word is deliberate and defensible. Shipping isn't the goal. Detail quality builds trust.

- ✅ **Do:** prototype, test in real contexts (hardware, light, one hand), iterate, and stay current with the active conventions 🟡 — in the Liquid Glass era, opaque bars or pre-2025-style icons are a craft failure, not a preference.
- ❌ **Don't:** "eyeballed" values without a system; default typography left unadjusted; motion copied from another platform that feels foreign.

### 8. Delight — make it human ✅

The natural result of getting the other seven right, not decorative confetti on top. Decide which emotion you want to evoke and reinforce it in every decision — never at the task's expense.

- ✅ **Do:** one characterful micro-interaction per surface; appropriate symbols; responsive feedback; a touch of glass with restraint.
- ❌ **Don't:** animation on every tap; charm that slows progress, weakens clarity, or harms accessibility. Decoration alone is not delight.

## Cross-cutting tactical rules 🟡

Derived from guides consistent across ≥3 sources; they serve the 8 principles:

- **Feedback in four kinds**: status, completion, warning, error. Confirm meaningful actions, expose in-progress state, warn before problems, validate inline (not on submit).
- **Wayfinding**: every screen must answer where am I? where can I go? what's here? how do I get out? Never trap the user.
- **Direct manipulation with immediate, local feedback**; controls near what they affect; nothing destructive without clear advance warning — but nothing reversible interrupted by routine confirmations.
- **A custom control must justify itself** with real material benefit and keep semantics, focus, accessibility, and state communication.

## Using them in practice

The principles are instruments of **arbitration**, not a mechanical checklist 🟡 (the HIG's own framing). Use them to break ties: if Familiarity and Delight clash, Familiarity wins; if Craft and Simplicity clash, Craft probably asks for less but better made. 🟡

See also: `two-layers.md`, `color.md`, `typography.md`, `../system/accessibility.md`, `../system/motion.md`.
