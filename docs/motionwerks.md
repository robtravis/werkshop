# Motionwerks

**Staged build animation.** Numbered "cue" collections that trigger on timeline markers — a
product assembling itself, a building revealing in stages, a sequence timed to voiceover.

Sidebar tab: **Motionwerks**, with a **Cues / Camera** switch at the top. The Camera half is
**[Camerawerks](camerawerks.md)** — same install, same tab.

[Release notes](motionwerks-releases.md)

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
2. **Add Cue**, then add objects with them selected.
3. Pick a **preset** — the motion the cue performs.
4. **Apply Cue** to generate the keyframes.

**From Markers** creates a cue per marker in one go, if your markers already lay out the story.

Cues **start on their marker**. Items within a cue are staggered by **Spacing**, and the whole
build takes **Timing** — so a cue of thirty windows can sweep in over two seconds without you
touching a keyframe.

The list is in **marker order**, always, however you added to them, and cues number themselves
`01`, `02`, `03`. Rename one and it keeps your name and the number: `03 Kitchen`.

### Beside the list

| | |
|---|---|
| **−** | remove the selected cue (the objects stay in the scene) |
| **▶** | **Follow Selection** — picking a cue moves the playhead to its marker |
| **▲** | **Live Sync** — cues follow their markers as you drag them |
| **⟳** | **Sync** — catch cues up to markers that moved with Live Sync off |

### Actions

Each cue owns a list of objects, and each object takes part in whichever **actions** you
switch on for it. The toggles are on the object's own row.

| | |
|---|---|
| **Motion** | move or scale into place, from a preset, with In/Out and axis |
| **Material** | fade or switch material over the cue |
| **Drives** | drive *any* Geometry Nodes **Progress** input on any object |

The count beside each action — `2/3` — is how many of the cue's objects take part. The
checkbox fills or clears all of them at once.

**Drives** is the bridge to the rest of the suite: bind a Mographwerks cloner's Progress to a
cue and the clones build on the marker, with the same timing as everything else.

---

## Presets

The preset picker holds the motions you use, and **+** saves the current settings as a new one.
A preset stores the curve, easing, direction, axis and distance — so *"windows drop in from
above with a soft landing"* becomes one pick rather than six settings.

**Apply to All** gives every object in the cue the selected object's preset.

---

## Markers

⚠ **Cues bind to markers by name, and Blender allows two markers to share a name.** If that
happens, every cue bound to that name follows whichever marker comes first — so a whole
sequence can collapse onto one frame.

Motionwerks will not create a colliding name itself (a second "Cue" becomes `Cue.001`), and
the panel warns you when any two markers share a name, naming them and their frames. Rename
one in the timeline to separate them.

**Renaming a marker breaks its binding** — move it instead. Moving is free and instant; the
cue follows.

---

## Beta notes

- Blender **5.2** or newer.
- Motionwerks generates **plain object keyframes**. If you hand-edit them and then re-Apply
  the cue, your edits are replaced — Apply regenerates.
- ⚠ Don't re-Apply a cue whose animation has drifted from its stored settings — Apply
  re-derives everything from the marker and the stored timing, which can move the whole cue.
