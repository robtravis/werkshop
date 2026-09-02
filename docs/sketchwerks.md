# Sketchwerks

**Realtime hand-drawn line art, stable under camera motion.** Feature edges become wobbly,
textured strokes (pencil, charcoal, ink) through a single Geometry Nodes system.

Sidebar tab: **Sketchwerks**

---

## Why it exists

It replaces the Cinema 4D Sketch & Toon workflow, and fixes what makes Grease Pencil Line Art
and Freestyle painful for animation:

- **No jitter, no crawl.** The wobble and texture are keyed to *world-space* geometry, never
  to the camera or the screen, so lines can't swim as the camera moves. This is the whole
  point; everything else is detail.
- **No baking, no overlay pass.** Strokes are real mesh ribbons that render and anti-alias
  natively, identical in the viewport and the final frame.
- **Realtime.** Everything updates live as you move objects, drag sliders or scrub.

> **Render in EEVEE.** Strokes are flat emission, so Cycles spends path-tracing effort that
> produces nothing and stresses the GPU far harder for no gain.

---

## Quick start

1. Put the objects you want outlined in a **collection**.
2. In the Sketchwerks tab, pick that collection and press **+** to create a line set.
3. Choose a **Style Preset**: *HB Pencil*, *Charcoal*, and others.
4. Adjust **Width** and **Color**, then open any section below to refine.

A line set is a self-contained object with its own modifier and material. Add several to give
different collections different styles in the same scene; the list at the top switches between
them and the panel follows.

---

## Marking edges

Drawn edges are auto-detected by angle, but you can override:

- **Mark Line / Clear** forces selected edges to always draw
- **Mark Hide / Clear** removes selected edges from the line art

Select the edges in Edit Mode and use the buttons. They're stored as mesh attributes, so they
survive edits and live in the .blend.

---

## The sections

| | |
|---|---|
| **Line** | width, colour, the base look |
| **Edges** | which edges qualify: angle, creases, boundaries, view silhouettes |
| **Wobble** | the hand-drawn deviation, world-locked |
| **Overshoot** | strokes running past their corners, as a person draws |
| **Breakup** | strokes thinning and dropping out along their length |
| **Dashes** | broken and dashed line styles |
| **Shading** | ambient-occlusion smudge: tone, not just outline |
| **Hidden Lines** | camera-raycast occlusion, with hidden edges styled separately |
| **Fill / Matte** | the occlusion matte for build-on animation |
| **Draw-On Animation** | keyframeable draw-on, for lines that appear as if being drawn |

---

## Occlusion between objects

A line set only occludes against its own collection by default, so two sets ignore each other
and lines show through objects they should sit behind.

Press **Build Occluder Set**. It gathers every static line set's source into one shared
collection and points all sets at it. Collections are linked rather than moved, so the
outliner is unchanged, and it is safe to press again after adding a set.

Geometry that should block lines but is never drawn, such as a ceiling, can be dragged into
that collection by hand. The button leaves manual additions alone.

---

## Build-on animation

Objects draw themselves on in sequence, and each starts occluding once it has been drawn.

1. Put each stage's objects in their own collection. **Link** them (`Shift+M`) rather than
   moving them.
2. Create a line set for it.
3. Press **Make Build-On**.
4. Keyframe **Draw Amount** 0 to 1, with **Linear** keys.

Make Build-On enables the draw-on and its occlusion matte, and sizes the stroke ordering to
the object. The matte dissolves in on its own as the drawing completes, so a build-on only
begins hiding the background once it exists. **Fade** sets how long that dissolve takes and
**Finish Early** lands it before the final strokes.

Do not also make the parent a line set. An object in two line-set sources is drawn twice.

---

## Performance

Line art on a real building is heavy. In order of effect:

- **Detail Limit** stops the system drawing finer than the render can resolve. It is
  camera-derived and self-tuning, and applies to renders as well as the viewport.
- **Fast Viewport** switches every line set to a coarser detail limit for camera work. It
  writes a viewport-only value, so leaving it on can never coarsen a render.
- **Cull Off-Camera** removes source objects the camera never sees across the whole frame
  range. Press again to restore.
- **Build Proxy Occluder** builds a low-poly stand-in for the occlusion raycast, which is the
  biggest win when that raycast dominates.

> Synthetic test scenes are not a guide here. Simple cubes evaluate hundreds of times faster
> than an Archipack house. Judge performance on your real scene.

---

## Check Setup

**Check Setup** scans every line set and warns about configurations that are known to look
broken: a build-on that will strobe on a moving camera, a build-on that cannot occlude, a fill
on a static set that can z-fight, a holdout with an opaque film, alpha dropped on save,
geometry drawn twice, and eased draw-on keys.

It only reports. It never changes anything. Run it after setting a scene up, and again before
rendering.

---

## Lines-only renders

1. Exclude the geometry collections from the view layer. The lines still occlude correctly.
2. Leave **Depth Occlusion off**. With the geometry excluded there is no depth buffer.
3. Render in **EEVEE**, with **Film > Transparent** on and **Color Mode RGBA**.

> RGB silently drops the alpha, writing the background black. With black lines on top that is
> a completely black frame.

---

## Beta notes

- Blender **4.2** or newer, the only Werkshop add-on that runs below 5.2, because it carries
  a compatibility shim for the modifier-input change. It is developed and tested on 5.2, so
  treat older versions as unverified rather than supported.
- After updating, press **Update Node Group** in the panel header. It regenerates the node
  group from the new code while keeping every line set's settings, materials and keyframes.
  Sockets added in a new version only appear after this runs.
- **Freeze Lines was removed in Beta 2.** Detail Limit made it unnecessary, and a frozen set
  showed a stale drawing while you worked. Files saved with a frozen set are restored
  automatically on load.
