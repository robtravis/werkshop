# Motionwerks

**Archviz phasing.** Numbered "cue" collections that trigger on timeline markers — a building
assembling itself, a renovation revealing in stages, a walkthrough narrated by voiceover.

Sidebar tab: **Motionwerks**. Installing this also gives you the
**[Camerawerks](camerawerks.md)** tab.

---

## The idea

A **cue** is a named group of objects bound to a **marker**. You say *these walls, this
motion, on that marker*, and Motionwerks generates the keyframes. Move the marker and the
animation follows it.

That binding is the whole value. Blender can already retime a group with NLA strips or a
box-select in the Dope Sheet, but it has no named persistent grouping, no marker binding, no
parametric stagger, and nothing that regenerates. Motionwerks writes plain object keyframes —
the most stable representation Blender has — so nothing here strands you.

---

## Cues

1. Put your objects in the scene and add markers where things should happen.
2. **Add Cue**, then **Add Objects** with the objects selected.
3. Pick a **preset** — the motion the cue performs.
4. **Apply** to generate the keyframes.

**Populate from Markers** creates a cue per marker in one go, if your markers already lay out
the story.

Cues **start on their marker**. Items within a cue are staggered by **Spacing**, and the whole
build takes **Timing** — so a cue of thirty windows can sweep in over two seconds without you
touching a keyframe.

The list reorders by dragging. **Jump** moves the playhead to a cue's marker.

### Cue actions

| | |
|---|---|
| **Motion** | move or scale into place, from a preset, with In/Out and axis |
| **Material Transition** | fade or switch material over the cue |
| **Drives** | drive *any* Geometry Nodes **Progress** input on any object |

**Drives** is the bridge to the rest of the suite: bind a Mographwerks cloner's Sequence
Progress to a cue and the clones build on the marker, with the same timing as everything else.

## Sync

**Live Sync** keeps cues attached to their markers as you drag them, so re-timing a
storyboard is dragging markers rather than regenerating anything.

**Markers from Shots** goes the other way — it writes markers from Camerawerks shots, so the
camera cuts and the build phases share one timeline.

---

## Presets

The preset picker holds the motions you use, and **Save Preset** adds your own. A preset
stores the curve, easing, direction, axis and distance — so *"windows drop in from above with
a soft landing"* becomes one pick rather than six settings.

---

## Beta notes

- Blender **5.2** or newer.
- Motionwerks generates **plain object keyframes**. If you hand-edit them and then re-Apply
  the cue, your edits are replaced — Apply regenerates.
- Cues are bound to markers by name. Renaming a marker breaks the binding; move it instead.
