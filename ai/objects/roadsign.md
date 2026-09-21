---
status: stub
verified: none
---
# Signals and signs

**Covers**: `Obj=roadsign` objects; signals and traffic signs.

## Initial facts

- Source folder: `New/ways/`. Examples include `signals.dat` (`retb-board`), `signals-narrow.dat`,
  `signals_maglev.dat`, `speedsignal.dat`, `roadsign.dat` (`OneWay`), and `roadsign-old.dat`.
  `[CODE New master @ e36ec2321]`
- Signalboxes are `Obj=building` objects with `type=signalbox`, not roadsign objects; see
  [public-buildings](buildings/public-buildings.md). `[CODE New master @ e36ec2321]`

## Planned sections

- Signal and sign fields, including signal aspects and speed signs.
- Relationship between signals and signalboxes.

## Open questions

- Which signalling behaviours are supported by Simutrans-Extended, and how should pakset signals
  cover them?
