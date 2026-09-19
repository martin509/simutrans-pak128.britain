---
status: stub
verified: none
---
# Vehicle objects

**Covers**: `Obj=vehicle` objects; trains, buses, trams, boats, and aircraft, including their
`.dat` definitions, images, and constraints.

## Initial facts

- `Obj=vehicle` is the most numerous object type in the pakset. `waytype=` values present are
  `track`, `road`, `air`, `water`, `tram_track`, `narrowgauge_track`, and `maglev_track`.
  `[CODE New master @ e36ec2321]`
- Vehicle source folders include `New/trains/` (subdivided into `carriages/`, `horses/`,
  `locomotives/`, `railcars/`, `wagons/`), `New/bus/`, `New/trams/`, `New/boats/`, `New/air/`,
  `New/maglev/`, `New/narrowgauge/`, `New/london-underground/`, and `New/livery-trains/`.
  `[CODE New master @ e36ec2321]`
- Vehicles use Simutrans-Extended's livery system; player colours are not currently used. See
  [liveries-and-special-colours](../graphics/liveries-and-special-colours.md).
  `[RECOLLECTION:2026-09-19]`
- Goods vehicles carry loaded-state image sets (empty, and one per cargo), indexed in the
  `.dat`; see [image-layout](../graphics/image-layout.md). `[RECOLLECTION:2026-09-19]`

## Related docs

- [liveries-and-special-colours](../graphics/liveries-and-special-colours.md) — read when adding or changing a livery.
- [image-layout](../graphics/image-layout.md) — read when indexing images, including loaded states.

## Planned sections

- Common vehicle fields and their meaning.
- Rail vehicles: consists, coupling constraints, and liveries.
- Road vehicles, trams, boats, and aircraft.
- Naming, intro and retire dates, and era coverage.

## Open questions

- Which engine fields govern vehicle behaviour in Simutrans-Extended (physics, wear, comfort),
  and where are they documented?
- Should this doc eventually be split into one doc per `waytype`?
