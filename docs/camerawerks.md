# Camerawerks

**Shot-based camera moves.** Build a walkthrough as a list of shots rather than as a soup of
camera keyframes.

Camerawerks is the **Camera** half of the **[Motionwerks](motionwerks.md)** tab — one install,
one tab, a switch at the top. They share the same keyframe engine, which is why they ship
together; everything here works with or without cues.

[Release notes](motionwerks-releases.md)

---

## The idea

A **shot** is a camera position plus a move. You frame the view you want, capture it as a
shot, choose how the camera gets there, and Camerawerks writes the keyframes. The shot list
is the edit — reorder it, retake a shot, and the timeline follows.

The whole camera track is **regenerated** from the shot list every time something changes.
There is no stored state to drift, which is why moving a marker or editing a shot updates
immediately with nothing to press.

---

## Shots

| | |
|---|---|
| **Add Shot** | capture the current viewport view as a shot |
| **Frame a Shot** | fly a temporary camera to frame it, then capture |

**Frame a Shot** is the one to reach for while you are looking through the camera. You cannot
frame a new shot from inside the sequence camera — the view *is* the previous shot — so the
panel says so and offers this instead.

Every shot **gets a timeline marker when you capture it**, so it can be dragged and can never
drift — the same contract cues have. If a marker already sits on that frame, the shot adopts
it rather than adding a second, which is how a shot and a cue come to share a trigger.

Shots stay in **frame order** however you add them, and number themselves `01`, `02`, `03`.
Rename one and it keeps your name and the number.

### Beside the list

| | |
|---|---|
| **⤓** | **Retake** — replace the selected shot's framing with the current view |
| **−** | remove the selected shot |
| **▣** | **Look Through** — toggle the sequence camera |
| **▶** | **Follow Selection** — picking a shot moves the playhead to it |
| **▲** | **Live Markers** — rebuild when a followed marker moves |
| **⟳** | **Rebuild** — regenerate the track by hand |

**Add Move** adds a shot derived from the selected one — a push, dolly, boom, pan, tilt, orbit
or crane — instead of framing it by hand. The dropdown is the move library.

**Markers from Shots** only appears when a shot has lost its marker — one you deleted, or a
shot made before markers were automatic. It is a repair, not a step.

---

## The selected shot

**Follows** is the marker this shot rides. Move that marker and the shot goes with it —
including from the timeline, which is the fastest way to retime an edit. Clear it and the
shot falls back to a fixed **Frame**.

**Move** is what the camera does *during* the shot: it holds the captured framing, then
performs the move across the rest of its span. **Cut** holds and cuts. **Fly to Next** lands
exactly on the next shot's framing, so there is no visible edit — a morph is a cut you cannot
see.

**Zoom** changes focal length across the hold.

---

## Rig

Everything true of the whole sequence, in one box.

**Camera** — the camera Camerawerks drives. It makes its own on the first shot; point this at
one of your own if you would rather. A camera you assigned is never deleted, only its
Camerawerks animation.

**Aim** — *Shot Framing* uses each shot's captured angle. *Track To* aims the camera at a
target instead, and the shots then set position only. ⚠ A Track To constraint overrides keyed
rotation, so these are modes, not options you stack.

**Focus** — *Off*, *Object* (Blender holds focus exactly), or *Pull Focus* (the distance is
keyed per shot, so it can miss and recover like a real lens).

**Path** — fly the camera along an editable Bezier through the shots. Once the path exists,
**it** decides the route and the shots become waypoints; rotation and lens stay keyed from the
shots. Needs at least two shots to appear.

**Shake** — handheld wobble on top of everything else, from a preset. The preset writes the
three values and leaves them editable.

---

## Beta notes

- Blender **5.2** or newer.
- **Delete Camerawerks Camera** removes the camera, path, helpers, every shot and the
  animation. It asks first. A camera you assigned yourself is kept — only its animation goes.
- Camera and camera *data* share one Action with two slots in Blender 5.2. That's normal and
  handled, but it means `lens` and `dof` curves live beside the transform curves in the same
  Action — worth knowing if you go digging in the Dope Sheet.
- ⚠ Shots bind to markers **by name**, like cues. Two markers sharing a name will pull two
  shots onto one frame; the panel warns when that happens.
