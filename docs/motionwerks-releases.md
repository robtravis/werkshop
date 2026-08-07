# Motionwerks — release notes

## Beta 16

**For Blender 5.2.** This build supersedes Beta 1, which is what everyone is on. Sixteen
builds went into it in one pass, so the notes below are cumulative rather than a changelog.

The short version: **Motionwerks and Camerawerks are now one tab**, and the two halves have
been rebuilt to look and behave the same way.

---

## Updating

You already have the Werkshop repository, so there is nothing to download and nothing to
uninstall. **Edit ▸ Preferences ▸ Get Extensions ▸ Check for Updates** and Motionwerks will
offer beta.16.

*(If you don't have the repository yet, add it once — Preferences ▸ Get Extensions ▸
Repositories ▸ + ▸ Add Remote Repository, URL `https://robtravis.github.io/werkshop/index.json`,
and tick Allow Online Access under Preferences ▸ System first.)*

**Your existing cues and shots are untouched.** Nothing about how they are stored has changed;
this build is the interface around them.

---

## One tab, two modes

**Camerawerks no longer has its own sidebar tab.** Open **Motionwerks** and there is a
**Cues / Camera** switch at the top.

It had a separate tab from the start, on the reasoning that you sometimes do camera work with
no cues involved — which is true, and it is still true, since the two halves remain completely
independent. But one install producing two tabs read as two add-ons, and at least one person
went looking for the one they thought they hadn't installed. A switch says outright that this
is one thing with two halves.

**If you use the sidebar tab order trick in the README, drop Camerawerks from your list** —
there are four tabs now, not five.

---

## Both halves now match

The cue side and the camera side were built months apart and had drifted into two different
dialects. They are now the same shape, top to bottom:

|  | Cues | Camera |
|---|---|---|
| top row | `Add Cue` · `From Markers` | `Add Shot` · `Frame a Shot` |
| list | cues, with side buttons | shots, with side buttons |
| box | the selected cue | the selected shot |
| box | **Actions** | **Rig** |

- **The cue list is a real Blender list now** — click a row to select it, double-click the name
  to rename, drag the corner to resize, and use the search and sort in the filter menu. It was
  a hand-built column of radio buttons before.
- **Both lists stay in chronological order** however you add to them. Add a shot at frame 30
  after one at frame 84 and it sorts into place. Drag a marker and anything bound to it moves
  in the list as you drag.
- **Cues and shots number themselves** — `01`, `02`, `03` in playing order. Rename one and it
  keeps your name and the number: `03 Kitchen`.
- **Follow Selection for cues**, matching the camera side — picking a cue moves the playhead to
  its marker. It's the ▶ toggle beside the list, on by default.
- **Sync and Live Sync moved onto the cue list** as side buttons. The Sync panel is gone; it
  was a whole panel for two buttons that act on the list above it.
- **Shots make their own markers.** Capture a shot and it gets a marker, exactly as adding a
  cue does — so a shot can be dragged in the timeline and can never drift. If a marker is
  already on that frame the shot adopts it, which is how a shot and a cue share a trigger.
  **Markers from Shots** is now only a repair, and only appears when something has lost its
  marker.
- **Shots are named `01 Shot`, `02 Shot`** rather than after the frame they landed on. An old
  shot called `01 f48` renames itself the next time the track rebuilds — it was keeping a
  frame number that stopped being true the moment it moved.
- **Retake and Look Through are labelled buttons under the shot list**, so both lists have
  the same four side buttons — remove, Follow Selection, live markers, rebuild.
- **Nothing is red any more.** The open action used to paint its whole row red, which read as
  an error rather than a selection. Warnings keep their ⚠ icon.

---

## Fixed

**Cues all landing on frame 1.** This is the big one, and it could hit anybody.

A cue binds to its marker **by name**, and Blender does not stop you having two markers with
the same name. Add Cue defaults the name to "Cue", so adding two cues without renaming them
created two markers both called `Cue` — and every cue bound to that name resolved to whichever
came first. All of them landed on the earliest one.

Two changes: **Add Cue can no longer create a colliding name** (a second one becomes
`Cue.001`), and **the panel now tells you when markers share a name**, in both modes, because
camera shots bind the same way.

If you already have a scene where this happened, the warning will name the markers. Rename one
in the timeline and re-point the cues that went astray.

**Other fixes**

- Inserting a cue between two others left it called something like `03 Cue.001` for good. Names
  are rebuilt in one pass now, and old `.001` names heal themselves the next time you add or
  remove a cue.
- A shot bumped off an occupied frame was labelled with the frame it *asked* for rather than
  the one it got.
- The marker badge is gone from shot rows. It meant "this shot follows a marker" — true of
  every shot now, so it said nothing. The **Follows** field still names which one.
- The mystery `—` beside each action is gone. It now reads `0/3`, `2/3` and so on, or nothing
  when the cue has no objects.

---

## Known

- **Path needs at least two shots.** A curve through one waypoint is meaningless, so the Path
  section is hidden until there is a second shot. If Path vanishes, that's why.
- **Cues are bound to markers by name.** Renaming a marker still breaks the binding — move it
  instead. The new warning covers the duplicate case, not the rename case.
- Motionwerks writes **plain object keyframes**. Hand-edit them and re-Apply, and your edits
  are replaced — Apply regenerates.

---

## Beta 1

First public build.
