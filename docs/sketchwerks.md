# Sketchwerks

**Realtime hand-drawn line art, stable under camera motion.** Feature edges become wobbly,
textured strokes — pencil, charcoal, ink — through a single Geometry Nodes system.

Sidebar tab: **Sketchwerks**

---

## Why it exists

It replaces the Cinema 4D Sketch & Toon workflow, and fixes what makes Grease Pencil Line Art
and Freestyle painful for animation:

- **No jitter, no crawl.** The wobble and texture are keyed to *world-space* geometry, never
  to the camera or the screen, so lines can't swim as the camera moves. This is the whole
  point; everything else is detail.
- **No baking, no overlay pass.** Strokes are real mesh ribbons that render and anti-alias
  natively in **EEVEE and Cycles**, identical in the viewport and the final frame.
- **Realtime.** Everything updates live as you move objects, drag sliders or scrub.

---

## Quick start

1. Put the objects you want outlined in a **collection**.
2. In the Sketchwerks tab, pick that collection and press **+** to create a line set.
3. Choose a **Style Preset** — *HB Pencil*, *Charcoal*, and others.
4. Adjust **Width** and **Color**, then open any section below to refine.

A line set is a self-contained object with its own modifier and material. Add several to give
different collections different styles in the same scene; the list at the top switches between
them and the panel follows.

---

## Marking edges

Drawn edges are auto-detected by angle, but you can override:

- **Mark Line / Clear** — force selected edges to always draw
- **Mark Hide / Clear** — remove selected edges from the line art

Select the edges in Edit Mode and use the buttons. They're stored as mesh attributes, so they
survive edits and live in the .blend.

---

## The sections

| | |
|---|---|
| **Line** | width, colour, the base look |
| **Edges** | which edges qualify — angle, creases, boundaries |
| **Wobble** | the hand-drawn deviation, world-locked |
| **Overshoot** | strokes running past their corners, as a person draws |
| **Breakup** | strokes thinning and dropping out along their length |
| **Dashes** | broken and dashed line styles |
| **Shading** | ambient-occlusion smudge — tone, not just outline |
| **Hidden Lines** | camera-raycast occlusion, with hidden edges styled separately |
| **Draw-On Animation** | keyframeable draw-on, for lines that appear as if being drawn |

---

## Performance

Line art on a real building is heavy. Two controls exist for it:

- **Freeze** — stop recalculating the strokes while you work on something else. The lines stay
  on screen; they just stop following the geometry until you unfreeze.
- **Fast Viewport** — a reduced-detail preview multiplier.

> Synthetic test scenes are not a guide here — simple cubes evaluate hundreds of times faster
> than an Archipack house. Judge performance on your real scene.

---

## Beta notes

- Blender **4.2** or newer — the only Werkshop add-on that runs below 5.2, because it carries
  a compatibility shim for the modifier-input change. It is developed and tested on 5.2, so
  treat older versions as unverified rather than supported.
- After updating, press **Rebuild** in the panel header. It regenerates the node group from
  the new code while keeping every line set's settings, materials and keyframes.
