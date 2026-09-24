---
status: draft
verified: New master @ f8859c42d
---
# Coupling constraints

**Covers**: which vehicles may be coupled to which in a convoy: the `Constraint[Prev]` and
`Constraint[Next]` lists, the `none` and `any` keywords, and the compiled head/tail placement
flags. Keyed from [vehicle](vehicle.md).

## List syntax

- Each `Constraint[Prev][i]` names one vehicle that may sit ahead of this one;
  each `Constraint[Next][i]` names one vehicle that may sit behind it. Multiple indices are
  alternatives. makeobj resolves each name to a vehicle at compile time.
  `[CODE simutrans-extended master @ 7655609]`
- `none` as the single entry means the end is closed: `Constraint[Prev][0]=none` allows the
  vehicle only at the front of a convoy, and `Constraint[Next][0]=none` disallows any
  followers. `[CODE simutrans-extended master @ 7655609]`
- `any` as the single entry means that end is free, and must not be combined with other
  entries. `[CODE simutrans-extended master @ 7655609]`
- With no entries at all, the end is likewise free, with placement flags derived from cabs,
  power and direction flags as described below. `[CODE simutrans-extended master @ d09e920]`

## Placement flags

- At compile time makeobj derives per-end placement flags: `can_be_head` (may lead),
  `can_be_tail` (may trail), `unconnectable` (closed end that still allows the vehicle
  itself at that end position), and `intermediate_unique` (a single named neighbour,
  mid-consist only). Combined values give `only_at_front` and `only_at_end`.
  `[CODE simutrans-extended master @ 7655609]`
- The game derives the same flags at load for old pak data through `fix_basic_constraint`,
  and the convoy assembler enforces them when coupling.
  `[CODE simutrans-extended master @ 7655609]`

## Direction flags and cabs

- `bidirectional` marks vehicles that can operate in either direction; at compile time it
  grants tail placement on an open front end, and with power it grants head placement on an
  open rear end. `[CODE simutrans-extended master @ 7655609]`
- `can_lead_from_rear` marks vehicles that can lead a convoy from its rear. It is obsolete
  and is folded into the rear placement flags; at load, a vehicle with it set but without
  `bidirectional` gains `bidirectional`. `[CODE simutrans-extended master @ 7655609]`
- `has_front_cab` and `has_rear_cab` grant head placement on the respective end. Left
  unspecified (255), they default from the other flags: an unpowered bidirectional vehicle
  without rear-lead loses head placement on an open rear end (the brake-van rule), and a
  non-bidirectional vehicle without rear-lead likewise cannot lead from that end.
  `[CODE simutrans-extended master @ 7655609]`
- Example: `BR-Class43(FGW1)` in `New/livery-trains/br-cl43-a-fgw1.dat` sets
  `Constraint[Prev][0]=none` so it only ever leads, and names same-livery coaches behind it.
  `[CODE New master @ f8859c42d]`

## Open questions

- None.
