---
status: draft
verified: none
---
# Blender rendering

**Covers**: the `.blend` meta-sources, headless rendering, aligned `.png` views, and the
transparency workflow.

## Initial facts

- The `.blend` meta-sources live in `Git Blends/Pak128.Britain-blends/` (a separate git
  repository from `New/`). `[CODE GitBlends master @ 1c1acf58]`
- The render script is `render_SimutransRender_pak128Britain-65.py`, with `bl_info` name "Render
  Simutrans Views Pak128.Britain-refresh", version `(1, 5)`, and `blender` `(2, 6, 5)`.
  `[CODE GitBlends master @ 1c1acf58]`
- The script renders 4 or 8 direction views and saves them with direction suffixes (for example
  `_W`, `_NE`). `[CODE GitBlends master @ 1c1acf58]`
- The script has a mask mode for materials whose names start with `sp_`, rendered to magenta
  `(1,0,0.5)`. Per the current workflow this mode is obsolete and belongs to a different pakset;
  it should be ignored. `[FORUM:https://forum.simutrans.com/index.php/topic,2401.msg162208.html#msg162208]`
- Blender 2.79 is required because the render scripts depend on its software renderer. The
  executable is `C:\Program Files\Blender Foundation\Blender\blender.exe`; the scripts directory
  is `C:\Program Files\Blender Foundation\Blender\2.79\scripts`. Blender must be driven headless;
  `.blend` files are never hand-edited (AGENTS.md hard rule 5).
  `[CODE local Blender installation, 2026-09-19]`
- Rendered `.png` views are placed into the `New/` `.dat` objects that use them.
  `[CODE GitBlends master @ 1c1acf58]`
- Vehicle models are assemblies of simple mesh primitives. `gnr-sturrock-single.blend` contains
  114 objects (mostly cubes, cylinders, circles, and planes), 27 materials, and renders at
  128x128 with the `BLENDER_RENDER` engine. `[CODE GitBlends master @ 1c1acf58]`

## Workflow and conventions

From the revised graphics workflow in forum post
`msg162208` (https://forum.simutrans.com/index.php/topic,2401.msg162208.html#msg162208):

- View count and alignment, set with the "Rendering views for Simutrans" script's `op_list`:
  - Road vehicles: render 8 views, normal alignment.
  - All other vehicles (trams, rail, water, aircraft): render 8 views, vehicle alignment.
  - Buildings, signs, signals, stations, and stops: render 4 views, normal alignment.
  A vehicle or way therefore produces 8 `.png` files, one per alignment; the other objects produce
  4. `[FORUM:https://forum.simutrans.com/index.php/topic,2401.msg162208.html#msg162208]`
- The current workflow uses alpha transparency. Set the render "output" to RGBA so that Blender
  writes a transparent background, and export anti-aliased images so that edges blend with the
  background. Most older `.blend` files have output set to RGB, which produces black backgrounds.
  With alpha transparency, no post-processing of the exported graphics is needed, except for
  multi-tile buildings and objects that need special colours.
  `[FORUM:https://forum.simutrans.com/index.php/topic,2401.msg162208.html#msg162208]`
- Many existing graphics still use the old system, a flat special-colour background with no
  anti-aliasing to the background. The aim is to convert all of them to the alpha-transparency
  type. This is limited by missing source files: not all `.blend` files exist, and most London
  Underground vehicles will need to be recreated. `[RECOLLECTION:2026-09-19]`
- The older method set the rendered background to `#e7ffff`, which is the engine's special
  transparency colour `0x00E7FFFF`. It applies only where the alpha-transparency workflow is not
  used. `[CODE simutrans-extended master @ f378cf551]`
- The "Make Masks" function in the render script is obsolete and belongs to a different pakset's
  workflow. `[FORUM:https://forum.simutrans.com/index.php/topic,2401.msg162208.html#msg162208]`
- Liveries are built from separate coloured polygons (planes), or from textures, rather than from
  player colours; see [liveries-and-special-colours](liveries-and-special-colours.md).
- The guide states that standard pak128 artwork is less bright and smoother, and that
  pak128.Britain artwork must be darker and consistent with the existing assets.
  `[FORUM:https://forum.simutrans.com/index.php/topic,2401.0/all.html]`
- Model templates and the blend repositories are linked from the guide. The blend repository used
  by this workspace is `Git Blends/Pak128.Britain-blends/`.
  `[FORUM:https://forum.simutrans.com/index.php/topic,2401.0/all.html]`
- For multi-tile buildings, the tool that splits the graphics into tiles does not work with alpha
  transparency; the post describes the alternatives.
  `[FORUM:https://forum.simutrans.com/index.php/topic,2401.msg162208.html#msg162208]`

## Related docs

- [liveries-and-special-colours](liveries-and-special-colours.md) — read when handling special colours and liveries.
- [image-layout](image-layout.md) — read when placing rendered views into image sheets.
- [scaling-conventions](../scaling-conventions.md) — read when deciding model and image scale.

## Open questions

- What is the exact command line used to render a blend file headless, and is it automated?
- Are there other render scripts in use besides `...-65.py`, and which is canonical?
- Which blend produces which `.png` and `.dat` object?
- Which objects still need the old `#e7ffff` background rather than alpha transparency?
