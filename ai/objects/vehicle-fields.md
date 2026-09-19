---
status: draft
verified: New master @ f8859c42d
---
# Vehicle fields

**Covers**: what every `Obj=vehicle` `.dat` field does. Reference for all vehicle editing;
keyed from [vehicle](vehicle.md). Engine semantics below come from Simutrans-Extended master
at `7655609` unless stated otherwise.

## Identity and dates

- `name` is the savegame identity of the vehicle; renames need a `compat.tab` entry (see
  [pakset-compatibility](../pakset-compatibility.md)). `copyright` records authorship.
  `[CODE New master @ f8859c42d]`
- `intro_year` and `intro_month` open availability for new purchase; `retire_year` and
  `retire_month` close it. Retirement ends production only: the engine's retired check is
  documented as "no longer in production", existing vehicles keep running, and upgrades to
  a retired type stop being offered. `[CODE simutrans-extended master @ 7655609]`
- The timeline must be on for dates to apply; this pakset runs `use_timeline = 3` from
  `starting_year = 1750`. `[CODE New master @ f8859c42d]`

## Economics

- `cost` is the purchase price. `runningcost` is the per-kilometre cost.
  `fixed_cost` is the monthly cost. `[CODE simutrans-extended master @ 7655609]`
- `fixed_maintenance` is the original Extended name for the monthly cost and is still read;
  older entries use it instead of `fixed_cost`.
  `[CODE simutrans-extended master @ 7655609]`
- For how these values are calibrated, see [balancing](../balancing.md).

## Physics and running

- `speed` is the maximum speed in km/h. `power` is engine power in kW. `gear` multiplies
  power and tractive effort, with 64 meaning 100 percent. `tractive_effort` is starting
  tractive effort in kN. `[CODE simutrans-extended master @ 7655609]`
- `brake_force` is vehicle braking force in kN, meaning the force stopping the vehicle, not
  the force of the brakes on the wheels. `[CODE simutrans-extended master @ 7655609]`
- `weight` is in kilogrammes. `axles` counts axles. `axle_load` is the load of the heaviest
  axle; routing compares the convoy's highest axle load against each way's limit, slowing
  or refusing overweight convoys. `[CODE simutrans-extended master @ 7655609]`
- `length` is in eighths of a tile, so 8 is half a tile.
  `[CODE simutrans-extended master @ 7655609]`
- `waytype` selects the way system: `track`, `road`, `tram_track`, `water`, `air`,
  `narrowgauge_track`, `maglev_track`. `[CODE New master @ f8859c42d]`
- `engine_type` selects traction: steam, diesel, electric, bio, sail, fuel_cell, hydrogene,
  battery, petrol or turbine. `[CODE simutrans-extended master @ 7655609]`
- `freight` names the good carried, as defined in `New/goods/goods-128.dat` (see
  [goods](good.md)). `[CODE New master @ f8859c42d]`
- `air_resistance` and `rolling_resistance` are the drag coefficients in physics
  calculations. `[CODE simutrans-extended master @ 7655609]`
- `range` is the maximum kilometres between stops, used by aircraft and some road vehicles.
  `minimum_runway_length` gates aircraft by airfield size.
  `[CODE simutrans-extended master @ 7655609]`
- `way_wear_factor` is the wear the vehicle inflicts on ways, in standard 8-tonne axle
  loads times 10,000, applied on every tile traversed; the default is 1.
  `[CODE simutrans-extended master @ 7655609]`
- `is_tall` marks vehicles barred from restricted-height bridges: routing treats
  height-restricted tiles as land for tall convoys. Rail vehicles default to tall.
  `[CODE simutrans-extended master @ 7655609]`
- `is_tilting` marks tilting trains, which take corners at higher speeds.
  `[CODE simutrans-extended master @ 7655609]`
- `override_way_speed` frees the vehicle from the underlying way's speed limit, intended
  for fly boats. `[CODE simutrans-extended master @ 7655609]`
- `is_sidewalker` appears on `New/bus/man_on_bicycle.dat` and `New/bus/post-boy.dat` but
  matches no code in Extended master or its makeobj writer, so it has no effect as far as
  can be determined. `[CODE simutrans-extended master @ 7655609]`
  `[CODE New master @ f8859c42d]`

## Capacity, comfort and loading

- `payload[i]` is capacity per accommodation class index, and `comfort[i]` its comfort
  rating; see [class](../class.md). `overcrowded_capacity` is standing capacity.
  `mixed_load_prohibition` forbids mixing another good in the same car.
  `[CODE simutrans-extended master @ 7655609]`
- `catering_level` is 0 for no catering, higher for better catering; see
  [class](../class.md). `[CODE simutrans-extended master @ 7655609]`
- `min_loading_time` and `max_loading_time` bound loading time with few versus full
  boardings. Unspecified, they default by waytype: 2000 ticks road and tram, 4000 rail,
  narrow gauge and maglev, 20000 water, 30000 air.
  `[CODE simutrans-extended master @ 7655609]`

## Operation, cabs and upgrades

- `bidirectional`, `can_lead_from_rear`, `has_front_cab` and `has_rear_cab` feed the
  coupling placement flags; see [coupling-constraints](coupling-constraints.md).
- `sound` names the running sound; -1 means none.
  `[CODE simutrans-extended master @ 7655609]`
- `smoke` names the exhaust smoke object shown while running.
  `[CODE simutrans-extended master @ 7655609]`
- `upgrade[i]` names successor vehicle types, with `upgrade_price` as the upgrade cost;
  `upgrade_cost`, where present, overrides it. `None` means the vehicle cannot be upgraded.
  `available_only_as_upgrade` blocks new purchase, leaving the type obtainable only by
  upgrading. The variant key `available_as_upgrade_only`, used in
  `New/trains/gwr-aberdare-superheated.dat`, is not read by makeobj and has no effect.
  `[CODE simutrans-extended master @ 7655609]` `[CODE New master @ f8859c42d]`

## Obsolescence

- Maintenance rises from `increase_maintenance_after_years` after the retirement date (or a
  settings default), by `increase_maintenance_by_percent`, reaching its maximum over
  `years_before_maintenance_max_reached` years.
  `[CODE simutrans-extended master @ 7655609]`

## Constraints, liveries and images

- Coupling lists and direction flags: [coupling-constraints](coupling-constraints.md).
- Way access bits: [way-constraints](way-constraints.md).
- Livery and image indexing: [liveries-and-special-colours](../graphics/liveries-and-special-colours.md)
  and [image-layout](../graphics/image-layout.md).

## Open questions

- None.
