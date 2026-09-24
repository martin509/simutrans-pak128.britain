---
status: stub
verified: none
---
# Ground and water textures (`ground`)

**Covers**: `Obj=ground` objects; ground textures and the animated water texture. Fences and
retaining walls are also ground textures; see [fences](fences.md) and
[retaining-walls](retaining-walls.md).

## Initial facts

- Source folder: `New/grounds/`, plus `New/pak1file/`. `[CODE New master @ e36ec2321]`
- `ground` objects present: `Basement` (`grounds-128.dat`), `Marker` (`marker.dat`),
  `LightTexture` (`TextureGrounds.dat`), `Water` (`water_ani.dat`), `Fence` (`fences.dat`), and
  the outside/base ground object in `New/pak1file/`. `[CODE New master @ e36ec2321]`
- The water ground is animated (`water_ani.dat`). `[CODE New master @ e36ec2321]`

## Related docs

- [fences](fences.md) — read when touching fences.
- [retaining-walls](retaining-walls.md) — read when touching retaining wall textures.

## Planned sections

- Ground texture roles: base ground, markers, foundations/basements, light textures, and water.
- Image conventions for ground textures.

## Open questions

- What distinguishes a ground texture from a ground object in the engine (see
  [ground-object](ground-object.md))?
