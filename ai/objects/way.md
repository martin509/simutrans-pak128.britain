---
status: stub
verified: none
---
# Way objects

**Covers**: `Obj=way` objects; the track, road, tram, water, air, and power ways on which
vehicles run.

## Initial facts

- `waytype=` values present: `track`, `road`, `narrowgauge_track`, `water`, `air`, `tram_track`,
  `power`, and `maglev_track`. `[CODE New master @ e36ec2321]`
- Source folder: `New/ways/`. `[CODE New master @ e36ec2321]`
- Elevated ways are also `Obj=way` objects distinguished by their name; see
  [elevated-ways](elevated-ways.md). `[CODE New master @ e36ec2321]`

## Child docs

- [elevated-ways](elevated-ways.md) — read when touching ways built above ground level. Elevated ways are a subtype of `Obj=way`, so this doc is keyed here rather than from [object-types](../object-types.md).

## Related docs

- [bridge](bridge.md) — read when touching bridges.
- [tunnel](tunnel.md) — read when touching tunnels.
- [crossing](crossing.md) — read when touching level crossings.
- [way-object](way-object.md) — read when touching way-attached objects such as electrification.

## Planned sections

- Common way fields (speed, weight limits, maintenance, electrification).
- Relationship between way types and vehicle constraints.

## Open questions

- Which engine fields govern way behaviour and wear in Simutrans-Extended?
