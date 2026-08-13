# Motionwerks — release notes

## Beta 20

**For Blender 5.2.** Supersedes Beta 17. Three builds went out in a day — 18, 19 and 20 — so
these notes cover all of them.

The short version: **two bugs that were damaging real work are fixed**, and the Duration /
Timing / Spacing panel now works the way you would expect, with the cue's span draggable
directly in the Timeline.

---

## Updating

Nothing to download and nothing to uninstall. **Edit ▸ Preferences ▸ Get Extensions ▸ Check for
Updates** and Motionwerks will offer beta.20.

**Your existing cues open unchanged.** Two settings changed how they are stored, and both
migrate automatically when the file loads — your Spacing and Timing values come across exactly
as they were.

---

## Two bugs worth knowing about

**Applying a cue could crash Blender.** Every Apply deleted and recreated the invisible anchor
each object animates from. If Blender still held a reference to one of those, the next
depsgraph update walked into freed memory. This was not rare and not new — it fired on every
Apply, and re-applying is something you do constantly. Anchors are now reused in place.

**Editing one object's motion rewrote every cue using the same preset.** If an object had its
own preset, the Motion sliders were editing the *library preset itself* — so nudging Scale
Frames for one object silently changed every other cue and object using that preset. Each
object now carries its own copy; the preset name records where the settings came from.

If a recent project behaved oddly — objects changing when you did not touch them, or cues
drifting out of step — those two are the likely cause.

---

## Duration bars in the Timeline

Each cue now draws as a coloured bar in the Timeline and Dope Sheet, using the colour you gave
its collection. Overlapping cues stack onto separate rows, which makes a cue that starts inside
another one obvious at a glance.

**Grab the right-hand end and drag to retime the cue.**

- **Drag** holds Timing steady and spreads or tightens the Spacing. Each object animates at the
  same speed; the build bunches up or spreads out.
- **Shift-drag** holds Spacing and changes Timing. The stagger rhythm stays; every object speeds
  up or slows down.

The header shows Duration, Timing and Spacing live while you drag, and says which one is giving.
One undo step per drag, so Ctrl+Z puts back the numbers and the keyframes together.

Turn the bars off with **Drag in Timeline** in the Motion panel.

---

## The panel inverted: Timing is typed, Duration is shown

**This is the biggest visible change.** Previously you typed Duration and Timing was a readout.
Now it is the other way round:

- **Timing** — how long each object's own motion lasts. Type it.
- **Spacing** — the gap between consecutive objects. Type it.
- **Duration** — the overall build. Shown greyed, because you drag it on the Timeline bar.

They are three views of one schedule: `Duration = (objects − 1) × Spacing + Timing`. Only two can
be set independently, and the two you now set are the two you cannot get at any other way.

**So editing Spacing now changes Duration**, where it used to hold Duration and change Timing.

**Spacing accepts fractions.** It had to: holding Timing steady while dragging needs a spacing
of 9.2 frames, and rounding to whole frames made Timing jump around by several frames instead of
holding still.

---

## Auto Apply

**Panel changes now take effect immediately** — Timing, Spacing, Curve, Easing and the whole
Scale / Move / Rotation block. No more pressing Apply Cue to see what you changed.

It is a toggle on the Apply Cue row, on by default. **Turn it off on a heavy cue**: a number
field updates on every increment while you drag it, not once when you let go, so a single slider
drag can be dozens of re-keys. Apply Cue is still there, greyed while Auto Apply is on.

---

## Smaller fixes

- Objects left permanently hidden, or stuck at zero scale, after a cue was edited — clearing an
  animation channel did not restore the value it had been driving.
- Objects losing their size when a cue was applied, from a measurement taken before Blender had
  finished updating.
- Deleting a saved preset no longer changes the cues that referenced it — they keep their own
  settings.
- Shift-drag on a duration bar now works from the first click.
- Corrected the add-on's tagline and maintainer, which still showed the old branding.

---

## Beta 17

**For Blender 5.2.** This build supersedes Beta 1, which is what everyone is on. Seventeen
builds went into it in one pass, so the notes below are cumulative rather than a changelog.

The short version: **Motionwerks and Camerawerks are now one tab**, and the two halves have
been rebuilt to look and behave the same way.

---

## Updating

You already have the Werkshop repository, so there is nothing to download and nothing to
uninstall. **Edit ▸ Preferences ▸ Get Extensions ▸ Check for Updates** and Motionwerks will
offer beta.17.

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
- **Add Move** could fail with *"MW_ShotPG is not in list"* — it held on to the source shot
  across adding the new one, and Blender is free to move the list in memory when it grows.
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
