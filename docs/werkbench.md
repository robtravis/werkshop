# Werkbench

**The bench where you assemble things before anything moves.** Origin, alignment, transform
and object creation. No timeline — anything that animates lives in Motionwerks.

Sidebar tab: **Werkbench**

---

## Origin

Move an object's origin without moving the mesh.

The X/Y/Z sliders run **−1 to +1 across the object's bounding box**, in World or Local space,
so −1 is one face and +1 is the opposite one regardless of how big the object is. Alongside
them: **Drop to Floor**, **Reset Transform**, **Center Origin**, and **Re-apply** (run the
same origin again after you've edited the mesh).

> Drop to Floor moves the object in **Z only**. It puts things on the ground; it doesn't
> re-centre them.

## Align

Illustrator-style align and distribute — a 3×3 grid of X/Y/Z × Min/Center/Max.

- **Distribute Gaps** — equal *empty space* between objects regardless of their size.
  Blender cannot do this natively; its own distribute spaces origins or bounds, which leaves
  visibly uneven gaps whenever the objects differ in size.
- **Align To**: Selection · Active · Cursor · World. **Active** holds the active object still
  and moves everything else to it — Illustrator's Key Object. Blender's own `object.align`
  moves the active one too.
- **Use Origins** matches origins instead of bounding boxes. Use it when the origin carries
  meaning: a door on its hinge, a wall on its pivot.

## Create

Eight **parametric primitives** — Plane, Cube, Circle, UV Sphere, Ico Sphere, Cylinder, Cone,
Torus. Blender's own Add Mesh is only adjustable in the redo panel and only until your next
click; these stay editable and keyframable for ever, because each one is a Geometry Nodes
group on the object.

**Group / Ungroup** (⌘G) is the C4D null-grouping gesture:

```
Chair.Group              collection, nested where Chair already lived
  ├── Chair.Group        wireframe handle, fitted to the group's bounds
  ├── Chair
  └── Legs
```

Nothing moves. The handle is a wireframe mesh rather than an Empty — an Empty's cube display
can only ever be a cube, and scaling one non-uniformly shears rotated children. It's
edges-only and never renders, so clicking through the middle picks whatever is actually there.

### Viewport handles

Every primitive's **size is draggable in the viewport** — the coloured box handles. They're
native Geometry Nodes gizmos, so they appear whenever the modifier is active, and dragging one
writes the modifier value, which means it undoes and keyframes like any other edit.

| | handles |
|---|---|
| Plane | Width, Height |
| Cube | Size X, Y, Z |
| Circle · UV Sphere · Ico Sphere | Radius |
| Cylinder | Radius, Height |
| Cone | Bottom Radius, Height |
| Torus | Ring Radius, Pipe Radius |

### Parameter names

The primitives use **Cinema 4D's vocabulary**, not Blender's: a cylinder has a **Height**, not
a Depth; a torus has a **Ring Radius** and a **Pipe Radius**, not Major and Minor. Segment
counts are abbreviated to **Seg** so they fit the panel — *Rotation Seg*, *Height Seg*,
*Cap Seg*.

Select a primitive and its parameters appear under Create, in a panel titled with the object's
own name.

## Transform

Location, rotation and scale, each with a **keyframe diamond** — Blender's own, so they key,
clear and show driven state exactly like the Properties editor.

**Dimensions** is greyed out on a Werkbench primitive. Editing it would write a scale that
fights Radius and Height, giving you a shape whose numbers no longer describe it — so the real
parameters stay the single source of truth, and Dimensions stays visible as a readout.

**Visibility** (nested under Transform) holds Viewports and Renders, each keyframable — which
is how you make something appear or vanish on a frame.

---

## Beta notes

- Blender **5.2** or newer. Earlier versions are not supported: the panel reads modifier
  inputs through an API that only exists in 5.2.
- Primitives created by an older build keep their original parameters and won't gain the
  viewport handles. Delete and re-add to pick them up.
