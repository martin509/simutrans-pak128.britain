---
status: draft
verified: New master @ 96a2c9593
---
# Factory fields

**Covers**: what every `Obj=factory` `.dat` field does, and what happens if it is omitted.
Reference for industry editing; keyed from [factory](factory.md). Engine semantics come from
Simutrans-Extended master at `d09e920` unless stated otherwise. Factories are parsed as a
factory node plus an embedded building node, so building-level keys also apply.

## Production

- `productivity` is the base production value, an absolute figure, not a percentage. It sets
  `prodbase`, the production per delta, and is the denominator by which storage and
  electricity demand are scaled. If omitted it is 10.
  `[CODE simutrans-extended master @ d09e920]`
- `range` is not a distribution range. It bounds a random variation added to `productivity`
  when the factory is built or upgraded; for city consumer-only industries it is the maximum
  production scaled by the town's relative population. If omitted it is 10.
  `[CODE simutrans-extended master @ d09e920]`
- `expand_minimum`, `expand_range`, `expand_probability` and `expand_times` control random
  production growth when the production counter wraps around: production rises by
  `expand_minimum` plus a random amount up to `expand_range` when the expansion count is
  below `expand_times` and a 1-in-10000 chance under `expand_probability` succeeds. All
  default to 0 if omitted, so a factory with no expansion keys never grows this way.
  `[CODE simutrans-extended master @ d09e920]`
- `distributionweight` is the factory's selection weight. It weights which factories are
  chosen when the world is populated and, inversely, how much the factory counts toward the
  industry-density-to-population ratio. If omitted it is 1; it is separate from the
  building-level `chance`. `[CODE simutrans-extended master @ d09e920]`

## Inputs and outputs

- `inputgood[i]` names the i-th good consumed; the list ends at the first missing entry. If
  omitted (no `inputgood[0]`), the factory has no inputs and is producer-only. A bare
  `inputgood` key is not read. `[CODE simutrans-extended master @ d09e920]`
- `inputcapacity[i]` is the nominal storage for that input. If omitted it is 0. The engine
  scales it by `prodbase/productivity`, divides by the consumption factor, adds the field
  share, and clamps it to the simuconf minimum.
  `[CODE simutrans-extended master @ d09e920]`
- `inputfactor[i]` is a percentage (stored as 256 = 1.0) for the units of input needed per
  unit of production; upstream chain sizing multiplies production by it and storage is
  divided by it. If omitted it is 100 (1.0). In contracts mode it is replaced by 1.0.
  `[CODE simutrans-extended master @ d09e920]`
- `inputsupplier[i]` is how many producer factories of this input the world generator should
  build and link. If omitted it is 0, which the generator treats as "build suppliers until
  consumption is met". `[CODE simutrans-extended master @ d09e920]`
- `outputgood[i]` names the i-th good produced; the list ends at the first missing entry. If
  omitted (no `outputgood[0]`), the factory has no outputs and is consumer-only. A bare
  `outputgood` key is not read. `[CODE simutrans-extended master @ d09e920]`
- `outputcapacity[i]` is the nominal storage for that output. If omitted it is 0, and makeobj
  logs a non-fatal error ("Factory output capacity must be larger than 0"); it is therefore
  effectively required for any factory with an output.
  `[CODE simutrans-extended master @ d09e920]`
- `outputfactor[i]` is a percentage (stored as 256 = 1.0) for how much output one internal
  unit of production yields; it scales produced units, storage and chain capacity. If omitted
  it is 100 (1.0). `[CODE simutrans-extended master @ d09e920]`
- `max_distance_to_supplier` and `max_distance_to_consumer` cap the distance at which supplier
  and consumer links are made. If omitted they are 65535, a sentinel meaning no cap.
  `[CODE simutrans-extended master @ d09e920]`

## Site, climate and region

- `location` is a string selecting the allowed site: `land`, `water`, `city`, `river`,
  `shore`, `forest`, `river_city` or `shore_city`. It controls what terrain the factory may
  be built on: water needs all-water tiles, city needs an adjacent road, shore a shoreline,
  river a river tile, forest a minimum tree count; water factories cannot haul goods over
  land and get an automatic water halt. If omitted it defaults to `land`.
  `[CODE simutrans-extended master @ d09e920]`
- `climates` is a bitmask of allowed climates. If omitted it allows all climates except
  water. `[CODE simutrans-extended master @ d09e920]`
- `regions` is a bitmask of allowed map regions, each value setting bit `1 << value`. If
  omitted it allows all regions. `[CODE simutrans-extended master @ d09e920]`
- `needs_ground` is a flag: when set, the ground below is drawn rather than removed. If
  omitted it is unset. `[CODE simutrans-extended master @ d09e920]`

## Fields (raw-material areas)

- `fields[i]` names a field class image; its presence makes the factory a field-based
  producer that spawns field tiles. If omitted there are no fields and expansion uses the
  `expand_*` path instead. A bare `fields` key is equivalent to `fields[0]`.
  `[CODE simutrans-extended master @ d09e920]`
- `production_per_field[i]` is the production each field adds; if omitted it is 16.
  `storage_capacity[i]` is the storage each field adds; if omitted it is 0.
  `spawn_weight[i]` weights which field class is created; if omitted it is 1000. These are
  only read when a field group exists. `[CODE simutrans-extended master @ d09e920]`
- `probability_to_spawn` is the chance per expansion opportunity of adding a field; if
  omitted it is 10 in 10000. `min_fields`, `start_fields` and `max_fields` bound the field
  count; if omitted they are 5, 5 and 25 respectively.
  `[CODE simutrans-extended master @ d09e920]`
- `field_output_divider` divides the summed field production before it is added to
  `productivity`. If omitted it is 1. `[CODE simutrans-extended master @ d09e920]`

## Electricity, passengers and mail

- `electricity_amount` is the power demand in MW; the alias `electricity_demand` overrides it
  and sets the same field. If omitted, the value is 65535, a sentinel meaning unspecified,
  and legacy demand is derived from `electricity_percent` instead. When specified it is
  scaled by `prodbase/productivity`. `[CODE simutrans-extended master @ d09e920]`
- `electricity_percent` (default 17 if omitted) is only used when `electricity_amount` is the
  sentinel; it sets demand as a percentage of production. Its inverse field is computed but
  unused. `[CODE simutrans-extended master @ d09e920]`
- `electricity_boost` is a per-mille production boost ceiling at full power (1000 = 1.0). If
  omitted it is 1000, i.e. doubling the production factor.
  `[CODE simutrans-extended master @ d09e920]`
- `passenger_boost` and `mail_boost` are per-mille production boost ceilings when visitors
  arrive, proportional to arrivals against demand. If omitted they are 0, so no boost.
  `[CODE simutrans-extended master @ d09e920]`

## Staffing and demand (building-level)

- `population_and_visitor_demand_capacity` is, for residential buildings, the population and
  otherwise the visitor demand. If omitted it is 65535, a sentinel meaning derive from level
  and the simuconf per-level rates. A producer with no output and this value zero is treated
  as an ordinary consumer rather than visitor driven.
  `[CODE simutrans-extended master @ d09e920]`
- `employment_capacity` is the number of jobs. If omitted it takes the `passenger_demand`
  default: 0 for residential, otherwise 65535 (derive from level and the simuconf per-level
  jobs rate). `[CODE simutrans-extended master @ d09e920]`
- `passenger_demand` is a legacy key: it is only read as the default for
  `employment_capacity` and overrides nothing when `employment_capacity` is present.
  `[CODE simutrans-extended master @ d09e920]`
- `mail_demand` is the mail capacity; `mail_demand_and_production_capacity` is the current
  name and overrides it when both are present, but both set the same field. If omitted it is
  65535, a sentinel meaning derive from level and the simuconf per-level mail rate.
  `[CODE simutrans-extended master @ d09e920]`
- `class_proportion[j]` and `class_proportion_jobs[j]` are per-class lists giving the
  proportions of passengers and of jobs by class. If omitted, the engine splits demand
  equally across classes. `[CODE simutrans-extended master @ d09e920]`
- `enables_pax` and `enables_post` are service bit flags, not capacities: they mark a building
  as able to handle passengers and mail at any halt built from it, alongside the freight bit
  factories always set. If omitted they are 0.
  `[CODE simutrans-extended master @ d09e920]`
- `pax_level` overrides the building `level` for legacy per-level passenger, visitor and mail
  figures. Current paksets leave it unset; the engine then uses the building-level figures.
  `[CODE simutrans-extended master @ d09e920]`

## Appearance, sound and timeline

- `mapcolor` is the colour index used on the minimap and factory legend. It is mandatory:
  if omitted, makeobj aborts with an error that the object is missing its identification
  colour. `[CODE simutrans-extended master @ d09e920]`
- `copyright` is a display-only credit shown in the information windows; if omitted it is
  empty. `[CODE simutrans-extended master @ d09e920]`
- `intro_year`/`intro_month` and `retire_year`/`retire_month` set timeline availability; a
  retired factory is closed or upgraded in the monthly update. If omitted they default to the
  engine's 1492 introduction and 2999 retirement, with month 1.
  `[CODE simutrans-extended master @ d09e920]`
- `smoke` names the smoke image shown when producing; if omitted there is no smoke.
  `smoketile` (default 0,0 if omitted) is the tile offset and `smokeoffset` (default 0,0) the
  pixel offset within it. `[CODE simutrans-extended master @ d09e920]`
- `sound` is the production sound, by filename or legacy numeric id; if omitted there is no
  sound. `sound_interval` is the nominal repetition in milliseconds (default 10000 if
  omitted), though a code comment notes the interval is not honoured after the first play.
  `[CODE simutrans-extended master @ d09e920]`
- `dims=x,y,layouts` is the building footprint and number of layouts. If omitted the
  footprint is 1x1 with one layout; an explicit zero dimension is a fatal makeobj error.
  `[CODE simutrans-extended master @ d09e920]`
- `level` is the building level; factories increment it by one internally, so a factory with
  `level` omitted ends at level 2. It is the fallback for capacity figures left at the
  sentinel. `[CODE simutrans-extended master @ d09e920]`
- `chance` is the building-level selection weight, distinct from the factory's
  `distributionweight`. If omitted it is 100.
  `[CODE simutrans-extended master @ d09e920]`
- `upgrade[i]` names successor factory types for the industrial upgrade and obsolescence
  system. If omitted there is no upgrade chain. A bare `upgrade` key is not read.
  `[CODE simutrans-extended master @ d09e920]`

## Pier and substructure keys

- `pier_sub_1_mask` and `pier_sub_2_mask` are 32-bit masks controlling which pier
  substructures the building may be placed on or within. If omitted they are 0; they are
  unused by ordinary land factories. `[CODE simutrans-extended master @ d09e920]`

## Keys with no engine effect

- `smokeheight` is not read anywhere in the engine or makeobj; omitting it changes nothing.
  `[CODE simutrans-extended master @ d09e920]`
- `smokespeed` is written by makeobj but discarded by the engine reader, which has no field
  for it; it has no engine effect. `[CODE simutrans-extended master @ d09e920]`

## Open questions

- Which of the two forms, `electricity_amount` or `electricity_percent`, should pakset
  factories use going forward?
