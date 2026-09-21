---
status: draft
verified: New master @ f8859c42d
---
# Way constraints

**Covers**: which vehicles may use which ways: the permissive and prohibitive constraint
system and the exact meaning of each constraint index in this pakset. Keyed from
[vehicle](vehicle.md).

## Matching rule

- Constraints are an 8-bit mask on each side. A vehicle may use a way exactly when every
  permissive bit the vehicle carries is also present on the way, and every prohibitive bit
  the way carries is also held by the vehicle. In short: if the vehicle needs it, the way
  must have it; if the way demands it, the vehicle must have it.
  `[CODE simutrans-extended master @ 7655609]`
- An empty mask always matches, so unconstrained vehicles run on unconstrained ways and
  neither side restricts the other. If the `way_constraint_permissive` or
  `way_constraint_prohibitive` keys are omitted entirely, makeobj uses an out-of-range
  sentinel and sets no bits, giving the empty mask; see
  [vehicle-fields](vehicle-fields.md). `[CODE simutrans-extended master @ d09e920]`

## Track electrification (permissive)

- Index 0, DC third rail: `DCThirdRail`, and combined with catenary or fourth rail in
  `DCThirdRailDCCCatenary`, `DCThirdRailACCCatenary` and `DCFourthRail`, all in
  `New/ways/electrification.dat`. `[CODE New master @ f8859c42d]`
- Index 1, DC catenary: `750VDCRailCatenary`, `DCRailCatenary`, and `TramElectrification`
  on tram track; electric trams carry permissive index 1.
  `[CODE New master @ f8859c42d]`
- Index 2, AC catenary: `ACHighSpeedCatenary`, and combined with third rail in
  `DCThirdRailACCCatenary`. `[CODE New master @ f8859c42d]`
- Index 3, fourth rail: `DCFourthRail` together with index 0; tube stock carries permissive
  index 3, for example `New/london-underground/1938-tube-stock.dat`.
  `[CODE New master @ f8859c42d]`
- Index 5, DLR third rail: `DLRThirdRail`; DLR stock carries permissive index 5, for
  example `New/london-underground/dlr-b07.dat`. `[CODE New master @ f8859c42d]`
- Indices 4, 6 and 7 are unused on track. `[CODE New master @ f8859c42d]`

## Track loading gauge (prohibitive)

- Index 1, tube tunnels: `LT_Tunnel` and `LT_Tunnel_Fast` in `New/ways/tube-tunnel.dat`
  demand it; tube stock holds prohibitive indices 1 and 2.
  `[CODE New master @ f8859c42d]`
- Index 2, light rail: `LightRailTunnelConcrete` in `New/ways/tunnels.dat` demands it; DLR
  stock holds prohibitive index 2. `[CODE New master @ f8859c42d]`
- Ordinary rail vehicles carry no prohibitive bits and therefore cannot enter tube or
  light-rail tunnels. `[CODE New master @ f8859c42d]`

## Tramways (prohibitive)

- Index 0 on tram track: every `TramTrack*` way in `New/ways/tram_track.dat` demands
  prohibitive index 0, and tram vehicles hold it, for example `New/trams/1-deck-closed.dat`
  with `way_constraint_prohibitive[0]=0`. `[CODE New master @ f8859c42d]`

## Waterways

- Permissive index 4 marks usable waterway on every canal, river and aqueduct.
  `[CODE New master @ f8859c42d]`
- Prohibitive indices grade waters by vessel size: 2 barge, 3 tub, 4 narrow, 5 ship,
  6 large ship, as commented in the way files. Each vessel holds the set of waters it can
  use: a horse-drawn boat holds 2 through 6 and runs anywhere, while a large ship holding
  only index 6 is limited to large-ship waters such as `CanalLargeShip` and `River3`.
  `[CODE New master @ f8859c42d]`
- Rivers grade from `River1` (index 2) through `River2` (index 5) to `River3` (index 6);
  canals grade from barge (`Canal`, index 2) through tub (`CanalTub`, index 3) and narrow
  (`CanalNarrow`, index 4) to ship (`CanalShip`, index 5) and large ship
  (`CanalLargeShip`, index 6), with matching aqueducts and canal tunnels.
  `[CODE New master @ f8859c42d]`
- Both hulls and their holds carry the vessel's bits, for example `BrigHull` and the
  `BrigAdd*` holds in `New/boats/brig.dat` and `New/boats/holds/brig-holds.dat`.
  `[CODE New master @ f8859c42d]`

## Road, air, maglev and narrow gauge

- Road, air and maglev ways carry no constraints, and neither do narrow-gauge ways.
  `[CODE New master @ f8859c42d]`
- Narrow-gauge horse vehicles carry a prohibitive index 0 that no narrow-gauge way demands,
  so it has no effect. `[CODE New master @ f8859c42d]`

## Open questions

- None.
