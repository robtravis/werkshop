# Werkshop

Blender add-ons for archviz, by [Vivinel](https://www.vivinel.com/).

> ⚠ **Beta.** Expect changes. Blender **5.2** or newer.

| | |
|---|---|
| **[Werkbench](docs/werkbench.md)** | Origin, align, transform and parametric primitives |
| **[Mographwerks](docs/mographwerks.md)** | C4D-style cloners, effectors and fields |
| **[Motionwerks](docs/motionwerks.md)** | Cue-based archviz phasing, triggered on markers |
| **[Camerawerks](docs/camerawerks.md)** | Shot-based camera moves *(the Camera half of the Motionwerks tab)* |
| **[Sketchwerks](docs/sketchwerks.md)** | Realtime hand-drawn line art |

---

## Install

Add the repository once; from then on updates arrive through Blender.

1. **Edit ▸ Preferences ▸ System** — tick **Allow Online Access**.
   *Blender will not contact a remote repository without this, and it fails quietly.*
2. **Edit ▸ Preferences ▸ Get Extensions ▸ Repositories ▸ + ▸ Add Remote Repository**
3. URL:

   ```
   https://robtravis.github.io/werkshop/index.json
   ```

4. Name it **Werkshop**, tick **Check for Updates on Startup**, press **Create**.
5. The add-ons appear under Werkshop — install and enable the ones you want.

### Sidebar tab order

Blender orders sidebar tabs by the order add-ons are *enabled*, and gives an add-on no way to
ask for a position. To get **Werkbench · Mographwerks · Motionwerks · Sketchwerks**, enable
them in that order, then **Preferences ▸ ☰ ▸ Save Preferences**.

*Camerawerks has no tab of its own — it is the Camera half of the Motionwerks tab.*

### If you already have a manually-installed copy

Remove it first. The extension and the old copy register the same panels and operators, and
enabling both gives you duplicate tabs and errors. Your preferences and any custom keymaps for
these add-ons reset when you switch — the extension is a different add-on as far as Blender is
concerned.

---

## Reporting a bug

Include:

- which add-on, and its version (**Preferences ▸ Add-ons**)
- your Blender version and OS
- what you did, and what happened instead

A `.blend` that shows it is worth a hundred words. If Blender printed an error, the console
text is the most useful thing you can send — **Window ▸ Toggle System Console** on Windows, or
launch Blender from a terminal on macOS.

---

This repository holds **built releases only** — it is what Blender downloads from. The add-on
sources live elsewhere.
