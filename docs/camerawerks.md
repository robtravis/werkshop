# Camerawerks

**Shot-based camera moves.** Build a walkthrough as a list of shots rather than as a soup of
camera keyframes.

Sidebar tab: **Camerawerks**. It ships with **[Motionwerks](motionwerks.md)** — one install
gives you both, because they share the same keyframe engine.

---

## The idea

A **shot** is a camera position plus a move. You frame the view you want, capture it as a
shot, choose how the camera gets there, and Camerawerks writes the keyframes. The shot list
is the edit — reorder it, retake a shot, and the timeline follows.

---

## Shots

1. Frame the view in the viewport.
2. **Add Shot** — the current camera position is captured.
3. Pick a **move** for how the camera travels into it.
4. **Jump** to review, **Retake** to recapture a shot's framing from the current view.

**Look Through** puts you in the camera; **Frame Start** sets where the sequence begins.

**Markers from Shots** writes a timeline marker per shot, so Motionwerks cues can be bound to
the same beats the camera is cutting on.

## Path

The camera's route between shots. **Smooth** relaxes the path so a sequence of shots reads as
one move rather than a series of lurches; **Reset** returns it to the straight interpretation;
**Select** picks the path object so you can shape it by hand.

## Aim

What the camera looks at. **Add Track Empty** creates a target the camera aims at, so you can
orbit a building while staying locked on the entrance. **Move Match** matches one shot's
motion to another's.

## Focus

Depth of field, driven from the shot list. **Add Focus Empty** gives you a focus target to
place in the scene; focus distance is keyframed along with everything else.

## Shake

Handheld feel. Adds a low-amplitude noise on top of the shot's motion, so a locked-off move
reads as a held camera rather than a crane.

---

## Beta notes

- Blender **5.2** or newer.
- **Remove** (the last panel) deletes generated animation. `Delete All` is exactly that —
  every shot and its keyframes. There's no undo prompt beyond Blender's own.
- Camera and camera *data* share one Action with two slots in Blender 5.2. That's normal and
  handled, but it means the camera's `lens` and `dof` curves live beside its transform curves
  in the same Action — worth knowing if you go digging in the Dope Sheet.
