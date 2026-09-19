---
status: stub
verified: none
---
# Building objects

**Covers**: `Obj=building` objects and their subtypes, keyed by the `type=` property in the
`.dat`.

## Initial facts

- `type=` values present: `res`, `signalbox`, `stop`, `com`, `cur`, `depot`, `ind`, `extension`,
  `mon`, `tow`, `habour`, and `hq`. `[CODE New master @ e36ec2321]`
- Source folders include `New/stations/` (stop), `New/depots/` (depot), `New/attractions/`
  (`cur`, `mon`), `New/citybuildings/` (`res`, `com`, `ind`), `New/signalboxes/` (signalbox),
  `New/townhall/` (`tow`), `New/hq/` (`hq`), and `New/piers/` (piers, a separate object type).
  `[CODE New master @ e36ec2321]`

## Child docs

- [city-buildings](buildings/city-buildings.md) — read when touching residential, commercial, or industrial city buildings (`res`, `com`, `ind`).
- [public-buildings](buildings/public-buildings.md) — read when touching stops and stations, station extensions, depots, signalboxes, attractions, monuments, harbours, or headquarters.
- [townhalls](buildings/townhalls.md) — read when touching town halls.

## Open questions

- Which building subtypes should eventually have their own docs rather than being grouped?
- How does the engine distinguish a building's subtype and its behaviour?
