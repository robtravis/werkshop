# Archwerks for Cinema 4D

**Parametric architecture for Cinema 4D: walls, windows, doors, cutouts, fireplaces, floors,
ceilings, roofs, stairs, railings, cabinets, countertops and sinks, with live dimensions you
can type into.**

> ⚠ **Beta.** Expect changes. Cinema 4D **2027** (macOS or Windows). Units follow your
> preferences.

**[Download Archwerks 0.55.0 for Cinema 4D](../c4d/Archwerks-0.55.0-c4d.zip)**

---

## Install

1. Quit Cinema 4D.
2. Put the **Archwerks** folder from the zip in your Cinema 4D plugins folder.
   In Cinema 4D: **Edit ▸ Preferences**, **Open Preferences Folder** (bottom left), then the
   **plugins** folder inside it (make it if it isn't there).
   Or keep the folder anywhere and add its location under **Edit ▸ Preferences ▸ Plugins**.
3. Start Cinema 4D. You should see an **Archwerks** menu in the main menu bar.

### Updating

Quit Cinema 4D, replace the old **Archwerks** folder with the new one, and start Cinema 4D
again.

---

## Start

**Archwerks ▸ Archwerks Panel** opens the panel. **Archwerks ▸ Archwerks Layout** switches to a
Top plan view beside Perspective, with the panel open.

The panel has three tabs: **Build**, **Openings** and **Kitchen**. Pick a button and its
card shows the choices for it (a style, a size). There is no Place button: choosing a type
starts placing.

## Build

| | |
|---|---|
| **Wall** | Draw a wall, or pick a wall preset to draw with |
| **Walls from Spline** | Turn the selected splines into walls |
| **Floor** | A floor in the selected walls' rooms, or one you draw |
| **Ceiling** | A ceiling over the selected walls' rooms, or one you draw |
| **Slab** | A slab under or over the selected walls |
| **Stair** | A stair along the selected spline, or a straight one |
| **Railing** | A railing on the selected stair, or along a path |
| **Beam** | A row of beams |
| **Baseboard** | Baseboards along the selected walls' rooms |
| **Crown** | Crown molding along the selected walls' rooms |
| **Wall Panels** | Picture-frame panels on the selected walls |
| **Roof** | A roof over the selected walls, or one you draw |
| **Roof Cutter** | A cutter in the selected roof |

### Drawing walls (AW Draw)

Pick a wall type, then click the corners in the view.

- Type a length and press **Return** to place a point exactly.
- **Shift** holds 45 degrees.
- Click the first point to close a room.
- **Escape** ends a run.

## Openings

| | |
|---|---|
| **Window** | Pick a window, then click a wall to place it |
| **Door** | Pick a door, then click a wall to place it |
| **Cutout** | A shaped hole through a wall: an arch to walk through, or a pass-through over a counter |
| **Fireplace** | Pick a fireplace, then click a wall |

Hover a wall and click to place. **Shift** centres it on the wall. Type a size while placing
(**36x60**). Everything placed in one go is linked: change a setting on one and they all
change, each keeping its own place along its wall.

## Kitchen

| | |
|---|---|
| **Cabinet** | Pick a cabinet, then click a wall to place it |
| **Countertop** | A countertop over the selected cabinets |
| **Sink** | Pick a sink for the selected countertop |
| **Add to Pulls Library** | Keep the selected object as a pull or knob |

Cabinets snap to a wall and to the cabinets beside them on it. Off the walls, a cabinet stands
free on the floor for an island: it faces you, **R** turns it a quarter, and it snaps beside
another cabinet or back to back with it.

Set a cabinet's top zone to **Sink** and the countertop over it adds a sink to suit. A
countertop's **Sinks** tab holds its sinks' settings.

---

## Editing

Select an Archwerks object: its settings are in the Attribute Manager. Drag its handles with
the **Move** tool or **AW Edit Dimensions**, where you can also click a dimension and type a
value.

| | |
|---|---|
| **Edit Dimensions** | Click a dimension label and type its value |
| **Floor Plan** | Lay a floor plan image on the floor to trace over |
| **Scale Plan** | Drag across a known dimension and type its length |
| **Tidy into Groups** | Sort every Archwerks object into the Archwerks groups |

## Sending a scene

A scene that uses Archwerks objects needs the plugin to open them. Before sending a file to
someone without it, make the Archwerks objects editable (**Make Editable**), so they are plain
geometry.

---

## Reporting a problem

Please send:

- what you did, and what you expected
- a screenshot
- the Python console's text (**Extensions ▸ Console**) if it shows errors
- your Archwerks version (it is in the zip's name) and your Cinema 4D version

A small scene that shows it helps most.
