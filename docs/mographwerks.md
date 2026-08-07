# Mographwerks

**A C4D-style cloner for Blender.** Select an object, add a cloner, and you have an array you
can shape with effectors and fields instead of by hand.

Sidebar tab: **Mographwerks**

---

## Quick start

1. Select the object you want to clone.
2. **Add ▸ Cloner** (or the **Add** menu in the Mographwerks tab) and pick a mode.
3. The object goes into a new collection with the cloner; the panel fills in.
4. Add an **Effector** to make the clones do something, and a **Field** to control which ones.

---

## The one idea worth knowing

**A generator is a cloner *or* a fracture.** Both emit instances, so everything downstream —
every effector, every field — works identically on a grid of chairs and on the shards of a
broken wall. There is no separate fracture toolset to learn.

## Cloners

| | |
|---|---|
| **Grid** | counts and spacing on three axes |
| **Linear** | a line along an offset |
| **Radial** | a ring |
| **Honeycomb** | a hex pack — offset rows, closed to √3⁄2 so it's a real hex lattice, not a stretched grid |
| **Object** | clones onto another object's Vertices, Face Centers, or a Scatter |
| **Curve** | clones along a curve, with Trim and Follow |

Grid, Linear and Radial have **viewport handles** — drag the coloured boxes to set spacing,
offset or radius.

## Fracture

Four methods, reached from the **Fracture** tab:

| | |
|---|---|
| **Voronoi** | real Voronoi cells cut out of the real mesh — exact piece count, watertight |
| **Grid** | a lattice with adjustable **Jitter** — brick, tile, regular stonework |
| **Live** | a fast non-destructive approximation, good for previewing motion |
| **Pieces** | takes geometry you've already broken and puts it on the effector stack |

Voronoi and Grid are a **bake**: they produce real shards, joined and handed to the Pieces
generator. **Margin** insets every shared face by the same distance, so the gap between two
shards is the same wherever they meet. **Cell Scale** stretches the cells along an axis —
that's how you get planks and slabs rather than blobs.

## Source

How a multi-object selection is used:

- **Each Object** — one member per clone point, cycling through them *(default)*
- **Whole Group** — the whole collection clones as a unit, so the arrangement repeats
- **Pick Random** — a random member at each point

Your originals aren't copied or moved out of your hands; the source collection is deactivated
so only the clones show.

## Effectors

What the clones actually *do*. They stack — each adds its offset, rotation and scale on top of
the ones before. Reorder by dragging, mute with the toggle.

| | |
|---|---|
| **Plain** | every clone equally |
| **Random** | a different amount per clone, from Seed |
| **Step** | a ramp from the first clone to the last |
| **Push Apart** | shoves overlapping clones off each other until they clear |

Every effector has a **Strength** and an optional **Field**.

**Push Apart** computes its own direction, so it replaces Offset rather than adding to it. It's
iterative: one iteration makes things *worse* (both clones shove away and can land on a third),
which is why the default is 8. It converges on each clone's own size plus Radius.

> Order matters once rotation is involved — rotations don't commute the way offsets do.

## Fields

A field is a **mask**: it decides how much each clone feels its effector. Ten types — Linear,
Sphere, Box, Random, Ring, Radial, Voronoi, Waves, Noise and **Sequence**.

The field is an object in the viewport. Move, rotate and scale it and the mask follows; its
**+Z is the direction** and its **scale is the falloff length**. **Fit to Clones** sizes it to
the generator in one click.

**Sequence** is the one that builds things. Instead of a shape in space it sweeps by
**Progress** (0 → 1) along an axis, with **Spread** controlling how wide the wave is — 0 moves
every clone together, high gives a long travelling wave. Progress is a normal keyframable
slider, so a build is two keys.

Falloff shape uses the **Robert Penner easing set** — Sine, Power, Expo, Circular, Back,
Elastic, Bounce — each with In / Out / In-Out, plus Exponent, Base, Size, Bounces and Mirror.

---

## Beta notes

- **[What's new in beta.23](mographwerks-releases.md)** — the Color effector, shared fields,
  and the field-space fix.
- Blender **5.2** or newer.
- 20,000 clones with a field, an ease and two effectors re-evaluate in about **1.7 ms**
  (modifier evaluation; viewport drawing is on top of that).
- Fracture is a bake and takes real time on dense meshes — start with a low piece count.
