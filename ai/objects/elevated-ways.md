---
status: stub
verified: none
---
# Elevated ways

**Covers**: `Obj=way` objects that carry traffic above ground level, such as viaducts and
trestles.

## Initial facts

- Elevated ways are `Obj=way` objects (not a distinct object type) distinguished by their
  names, which contain `Elevated`; examples include `brick-viaduct-elevated.dat`,
  `concrete-viaduct-elevated.dat`, `iron-girder-elevated.dat`, `wood-trestle-elevated.dat`, and
  the `-elevated-road` and `-elevated-narrow` variants in `New/ways/`.
  `[CODE New master @ e36ec2321]`
- Each elevated way exists alongside a corresponding `Obj=bridge` object of the same style
  (for example `brick-viaduct.dat` with `brick-viaduct-elevated.dat`).
  `[CODE New master @ e36ec2321]`

## Planned sections

- How elevated ways and bridges relate in the engine.
- Height and pillar conventions.

## Open questions

- What exactly distinguishes an elevated way from a bridge in Simutrans-Extended, and when is
  each required?
