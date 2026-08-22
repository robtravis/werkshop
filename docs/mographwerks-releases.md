# Mographwerks — release notes

[← back to Mographwerks](mographwerks.md)

---

## 1.0.0-beta.28

**Updating:** **Edit ▸ Preferences ▸ Get Extensions ▸ Check for Updates**.

### In Place — effect objects without cloning them

A new cloner mode: **In Place**. Point it at a collection and it makes no copies and moves
nothing. Every object stays exactly where you put it, and effectors and fields then act on
them **individually**.

This is the one you want for text. Put your characters in a collection, add a cloner in In
Place mode, add an effector and a field, and the field sweeps across the letters where they
already sit — no re-spacing, no rebuilding your layout as a grid.

It is not only for text: hand-placed debris, an imported assembly, anything you have arranged
deliberately and want to animate with fields without giving up the arrangement.

Notes:

- It follows the collection. Add an object and it joins in; remove one and it leaves.
- Your objects are never moved, renamed or reparented.
- **Moving the cloner does not move the group** — In Place means in place. To move things,
  move the objects, or use one of the other modes.

---

## 1.0.0-beta.27

**Updating:** **Edit ▸ Preferences ▸ Get Extensions ▸ Check for Updates**.

Everything in beta.26 below, plus:

- **From Object hides the original**, the way cloning a selection or a collection already did.
  Remove Cloner brings it back. An object you had already hidden yourself is left alone.
- **The new collection is created where the source lived**, rather than one level up.
- **Nested cloners now update all the way to the top.** A change deep in a chain used to
  refresh only the cloner directly above it, leaving everything higher showing a stale result
  until some unrelated edit forced a rebuild. That is what made deep nesting look like it had
  a level limit. It does not — nesting works to at least six levels; what runs away is the
  **count**, since every level multiplies. Four levels of 4×4 is 65,536 clones.
- The Source panel warns if a cloner has ended up **inside its own source collection**, which
  produces no clones at all and has no other symptom.

---

## 1.0.0-beta.26

**Updating:** **Edit ▸ Preferences ▸ Get Extensions ▸ Check for Updates**. Nothing to download
by hand.

### Freeze, and Convert to Mesh

Two new buttons at the bottom of the panel, and they do different things.

**Freeze** bakes the clones exactly as they are — effectors and fields applied — so they stop
responding to changes. Instancing is kept, so a heavy scene does not blow up, the cloner stays
editable underneath, and **Unfreeze** brings it back. The bake is saved in your .blend, so it
survives closing and reopening the file.

Use it to hold a result you like while you carry on working around it.

**Convert to Mesh** flattens the whole stack into plain mesh data — effectors baked in, no
modifiers left. Your source objects and the cloner's collection are kept, not deleted. This one
cannot be undone except with Undo.

Both work through nested cloners, and Convert captures **the frame you are parked on**. You do
not need to Freeze before converting; they are independent.

> If you have been trying `Object ▸ Convert ▸ Mesh` on a cloner and getting an empty mesh —
> that is why. A cloner's geometry is instances, not mesh, so Blender's own Convert copies
> nothing. The new button adds the missing Realize step for you. Apologies: an earlier note
> here said Convert alone was enough. It is not.

### Cloning a cloner — From Object

**Add a Cloner** now has a **From Object** picker beside From Collection. Point it at any object
— including another cloner — and the buttons build a cloner of that, where it stands.

**This is now the right way to nest cloners.** Previously the only route was pointing an outer
cloner at the inner one's *collection*, and that collection also holds the inner cloner's field
gizmos — so your fields got cloned as geometry and appeared to wander when you changed spacing.
From Object clones the cloner and leaves its fields alone. If you have a setup doing this, the
Source panel now warns you and points at the fix.

Nesting through Object works to at least three levels; an old note in the panel claimed
otherwise and was wrong.

### Smaller

- "From Collection" is no longer truncated to "From Collecti…".
- The Color effector's buttons no longer clip in a narrow sidebar, and their explanation moved
  into tooltips.
- **Add Field ▸ Use Existing** lets a second effector read a field that already exists, instead
  of making one you then have to swap away.

---

## 1.0.0-beta.23

**Updating:** you already have the repository, so **Edit ▸ Preferences ▸ Get Extensions ▸
Check for Updates** and Mographwerks will offer beta.23. Nothing to download by hand, and
nothing to uninstall first.

**Your existing files keep working.** From this build on, Mographwerks updates its own node
groups when you open a file made with an older version — you do not need to rebuild anything. A
console line saying it updated some node groups on open is that working, not a warning.

This is a big one — everything from beta.7 to beta.23, so it covers seventeen builds since the
last release.

### New

**A Color effector — a field can drive colour, not just motion.** Add an Effector, set its Type
to **Color**, and give it a field. Clones inside the field take Color B, clones outside take
Color A, everything between blends.

The effector writes the colour onto the clones; your material has to read it, and there is a
button for that — **Set Up Material** wires it up on the cloned object. Building the material
yourself: add an Attribute node, set its type to **Instancer**, and put `mg_color` in the name
field. Not Geometry — Geometry looks at the source mesh, finds nothing, and renders flat with no
error at all.

**…or a full gradient.** **Set Up with Ramp** wires the raw 0–1 field value through Blender's own
Color Ramp instead, seeded from your Color A and Color B. From there it is a normal ramp: as
many stops as you like, every interpolation mode, the eyedropper, and Blender's ramp presets.

**Shared effectors.** One effector's settings can drive several cloners at once. Set it up on
one, link the others to it, and changing the master moves them all. Each cloner keeps its own
**Progress**, deliberately — so you can still offset the timing of a shared build.

**Shared fields.** One gizmo can drive several effectors. In the **Add Field** menu, below the
falloff types, there is now a **Use Existing** section listing the fields already in your scene.
Pick one and both effectors read the same gizmo — move it and everything responds. This is how
you have a single field drive both a Plain and a Color effector.

**Radial Rings** is back, plus **Shift Index** and a **Material** override on cloners.

### Fixed

**Fields acted somewhere other than where they were drawn.** The biggest fix in the build. If
your cloner was moved, rotated or scaled away from the world origin, the field did its work in
one place while the gizmo was drawn in another — the gizmo was effectively lying to you. If you
built a workaround for this, it is no longer needed.

**"I can't add a material, or it doesn't show up."** The material system turned out to be
innocent. **Hide Source excludes the source collection**, so the source object cannot be clicked
or found in the outliner — so you select the cloner instead and assign the material there, where
it silently does nothing, because the cloner's own mesh is not what renders. It only bites
cloners made **From Collection**, which is why it looked intermittent. The **Material** override
on the cloner does what you were reaching for, and the Source panel now warns you when a
material has been put somewhere it cannot show.

**Nested cloners.** Pointing a cloner's Source at another cloner always produced the right
result — it just never re-evaluated, so you saw the inner object repeated rather than the
inner's whole run. Changing something unrelated in the scene would make it snap to correct. It
updates when you change it now.

**Gizmos disappeared when you added an effector.** They come back, and stay.

**Cloners no longer get slower as the scene grows.** Field stamping used to scale with the size
of the whole scene, whether or not the extra objects had anything to do with the cloner.

**Colour ignored the ramp above Strength 1.** Every clone read past the end of the ramp and came
out one flat colour. Colour now follows the field directly and ignores Strength — so Strength is
gone from the Color effector's controls, because it no longer does anything there. Motion is
unaffected, and still overshoots on springy eases, which is the point of them.

**Smaller:** deselecting everything returns the panel to **Add a Cloner** instead of holding the
last cloner you had selected; the Color effector's buttons no longer clip in a narrow sidebar.

### Known limits

- **Radial Count is per ring**, so inner rings are denser in arc terms.
- **Custom falloff curves** work on a field's Shape and Ease. Not yet on the Step effector's
  ramp, the Random distribution, density along a Curve cloner, or the Push Apart response.
- **Four fields per effector** is the maximum.
- **Live downstream modifiers.** There is no managed Realize modifier, so you cannot keep a
  cloner *live* while stacking a Boolean or Remesh after it. Use **Convert to Mesh** (below) and
  work on the result — if you need it live, say so.

---

## 1.0.0-beta.6 and earlier

Radial arcs, cloning from a collection, custom falloff curves, the Overlay blend mode and
Uniform Scale on Random. No notes were published for these.
