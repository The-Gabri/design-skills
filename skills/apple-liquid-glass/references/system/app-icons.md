# App icons ✅/🟡

Construction rules and practical guide for the app icon in the iOS 26 /
macOS Tahoe era. The icon is the app's first impression: one idea, legible
at 29pt.

Legend: ✅ = direct HIG/official-doc quote in ≥2 sources; 🟡 = consistent in
≥3 independent sources; ⚠️ = doubtful or single source.

---

## 1. Rules ✅/🟡

- ✅ **The system applies the mask**: export a **1024×1024px square
  without rounding or cropping**. The system applies the shape
  (squircle/superellipse), never the asset.
- ✅ **One centered glyph on a simple background**: one brand, one idea.
  A silhouette recognizable at a glance.
- ✅ **No text in the icon** unless it's the brand; the accessible name
  comes from the app name. No photos as icons either.
- ✅ **No Apple hardware or replicated standard UI components** in the
  design.
- 🟡 **Full-bleed opaque background** (no edge transparency): **luminance**
  contrast (not just hue) must separate the brand from the background.
- ✅ **Design in Icon Composer** (Apple's official tool): the system
  generates the variants and sizes from there.
- ✅ Provide **Light, Dark, Tinted, and Clear** variants: in iOS 26+ the
  user can choose the global system look and it affects third-party apps.
- 🟡 **macOS Tahoe**: icons with glass layers (squircle with depth);
  the system composes the layers — design background and foreground
  separately. Tints as on iOS.
- ✅ Test at **real sizes** (home screen, Spotlight, Settings): fine detail
  dies small. If it doesn't read at 48px, it's no good.

---

## 2. Practical construction guide 🟡

Recommended flow in Icon Composer (or your vector tool exporting at
1024×1024):

**Step 1 — Canvas and grid.**
Square 1024×1024 canvas. Draw the glyph in vector, centered. 🟡 Safe zone:
keep the glyph inside the ~72% central area of the canvas — the system
visually crops with the squircle mask and the edges "breathe".

**Step 2 — Simple, opaque background.**
One flat color, a subtle gradient, or minimal texture filling the canvas
edge to edge. No transparencies: the system decides what falls outside the
mask, and an alpha background produces dirty edges. 🟡

**Step 3 — One glyph, high luminance contrast.**
The glyph must separate from the background by **luminance**, not just hue:
blue on purple can share the same brightness and become invisible to some
users. Test the icon in grayscale: if it reads, the contrast is enough. 🟡

**Step 4 — Light/Dark/Tinted/Clear variants.**
Define the 4 appearances in Icon Composer: Light (full-color design),
Dark (adapted dark-background version, not a simple inversion),
Tinted (monochrome glyph over the system tint), and Clear (glass).
iOS 26+ offers them to the user as a global look. ✅/🟡

**Step 5 — Layers for Tahoe (macOS).**
Separate background and foreground into layers: Tahoe's system composes the
glass with depth between them. Avoid "flattening" the icon into one image
if targeting macOS. 🟡

**Step 6 — Test at real sizes.**
Check the icon at 180px (home), 120px (Spotlight), 87px (Settings), and
48px (notifications). Rule: if a detail can't be told apart at 48px, remove
it. ✅

```
Control sizes (iOS, reference 🟡):
 1024px  master asset (App Store / Icon Composer)
  180px  home screen (@3x)
  120px  Spotlight (@3x)
   87px  Settings (@3x)
   48px  notifications
```

**Step 7 — No text, no photos.**
If the temptation is to put the app's name inside the icon: don't. The name
already appears under the icon in the system. The exception is a brand whose
letter *is* the logo (then it's a glyph, not informational text). ✅

---

## 3. Icons in context: SF Symbols vs. app icon

Don't confuse with SF Symbols (`tokens.md` §5): symbols are for the
**interface** (toolbars, tab bars, buttons) and follow the outline/filled
rule; the **app icon** is a unique brand piece with an opaque background.
Never use an unmodified SF Symbol as an app icon: it's generic and doesn't
differentiate your product. 🟡

---

## Do / don't pairs

**D1 — Mask ✅**
- ✅ **Do:** 1024×1024 square without rounding; the system applies the
  squircle.
- ❌ **Don't:** pre-render rounded corners in the asset: the system applies
  its own mask on top and you get a double crop with weird edges.

**D2 — Simplicity ✅**
- ✅ **Do:** one centered glyph, simple background, silhouette recognizable
  at 48px.
- ❌ **Don't:** scenes, photos, informational text, or several competing
  elements: at home-screen size everything becomes noise.

**D3 — Variants ✅/🟡**
- ✅ **Do:** Light, Dark, Tinted, and Clear in Icon Composer; separate
  layers for Tahoe's glass.
- ❌ **Don't:** ship only the light version: in iOS 26+ the user can force
  the global look and your icon will clash or look broken.

**D4 — Contrast 🟡**
- ✅ **Do:** separate glyph and background by luminance; grayscale test.
- ❌ **Don't:** rely only on hue difference (same-brightness blue on
  purple): some users won't be able to tell the brand apart.

**D5 — Real testing ✅**
- ✅ **Do:** test on the device's home screen, Spotlight, and Settings.
- ❌ **Don't:** validate only on the editor's 1024px canvas: fine detail
  that looks good there dies small.

See also: `tokens.md` §5 (SF Symbols), HIG *App Icons*:
https://developer.apple.com/design/human-interface-guidelines/app-icons
