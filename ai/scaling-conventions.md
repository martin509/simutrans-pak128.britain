---
status: draft
verified: none
---
# Scaling conventions

**Covers**: the pakset's scale system, its calibration rulers, logarithmic scaling of long
objects, and oversized images. The authoritative description is the revised graphics workflow in
the forum post
`msg162208`: https://forum.simutrans.com/index.php/topic,2401.msg162208.html#msg162208 .

## The scale system

- The 15 m ruler sets the **length** scale only. It is imported into Blender to calibrate the axis
  along an object's length, on which one tile represents 15 m. It does not set the width or height
  scale; see the next point.
  `[FORUM:https://forum.simutrans.com/index.php/topic,2401.msg162208.html#msg162208]`
- Width and height use 1.25 times the **length** scale; the pakset's scale is not the same on all
  axes. `[FORUM:https://forum.simutrans.com/index.php/topic,2401.msg162208.html#msg162208]`
- Aircraft use a separate linear length scale: 128 pixels (one tile) represents 46 m of length. A
  46 m ruler in Collada format is provided in the blend repository at `air/46m-rule.dae`.
  `[FORUM:https://forum.simutrans.com/index.php/topic,2401.msg162208.html#msg162208]`
- Objects longer than 15 m use a logarithmic scale, proportional to the square root of the length
  in so far as it exceeds 15 m. In practice this applies only to ships; rail and road vehicles are
  never that long. Worked example from the post: for a 50 m ship, sqrt(15) = 3.87 and sqrt(50) =
  7.07, giving a ratio of 1.83; scale the length ruler by 1.83, then derive a width ruler by
  rotating it and scaling by width divided by length.
  `[FORUM:https://forum.simutrans.com/index.php/topic,2401.msg162208.html#msg162208]`
- The rescaling of the pakset to this system is complete. Guidance that describes it as in
  progress is historical and must not be applied. `[RECOLLECTION:2026-09-19]`

## Oversized images

- Most objects use 128x128 cells. Some aircraft and ships need larger images. The post gives two
  non-standard sizes: 192x192 and 254x254, with 254 the maximum Simutrans supports.
  `[FORUM:https://forum.simutrans.com/index.php/topic,2401.msg162208.html#msg162208]`
- To produce an oversized object, set the Blender render resolution to the size and scale the
  object down by 128 divided by that size (for 192, scale by 0.67), then apply offsets in the
  `.dat` as for road vehicles.
  `[FORUM:https://forum.simutrans.com/index.php/topic,2401.msg162208.html#msg162208]`
- `New/Makefile` has size classes of 192, 224, and 256, which does not match the post's 192 and
  254 and must be reconciled. `[CODE New master @ e36ec2321]`

## Related docs

- [image-layout](graphics/image-layout.md) — read when laying out image sheets.
- [blender-rendering](graphics/blender-rendering.md) — read when producing rendered views.
- [pak-format-and-objects](pak-format-and-objects.md) — read when the offsets and size classes are applied.

## Open questions

- The post gives 192 and 254 as the non-standard sizes; the build has 192, 224, and 256. Which is
  correct, and for which objects?
- Confirm that one tile represents 15 m of length for all non-aircraft and non-ship objects.
- Does the 46 m per tile aircraft scale apply to all aircraft without exception?
