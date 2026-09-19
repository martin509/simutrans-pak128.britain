---
status: draft
verified: New master @ 7a0a145e1
---
# Goods (`good`)

**Covers**: `Obj=good` objects; goods definitions.

## Definition format

- The pakset defines its goods as `obj=good` blocks in `New/goods/goods-128.dat`.
  `[CODE New master @ e36ec2321]`
- Block keys: `name`, `mapcolor`, `metric` (display unit such as `tonnen`, `head`, `bundles`,
  `cars`, `paletten`), `catg` (category), `number_of_classes`, distance-staged revenue
  `value[i]` with `to_distance[i]`, per-class revenue `class_revenue_percent[i]`,
  `speed_bonus`, and `weight_per_unit` in kilogrammes. `[CODE New master @ 7a0a145e1]`
- Omission defaults: `catg` is 0, `number_of_classes` is 1, `speed_bonus` is 0,
  `weight_per_unit` is 100, `mapcolor` is 255, each `class_revenue_percent[i]` is 100, and
  the unindexed `value` is 0. The staged `value[i]` list is terminated by the first missing
  index; an omitted `to_distance[i]` repeats the previous value (0 for the first). `name` is
  the registry key and is required in practice.
  `[CODE simutrans-extended master @ d09e920]`
- Example, passengers (`name=Passagiere`): `number_of_classes=5`; staged values 55 to 16 km,
  50 to 500, 45 to 2500, 40 to 5000, 35 beyond; class revenue percents 50, 100, 150, 200 and
  300 across the five classes; `weight_per_unit=70`. `[CODE New master @ 7a0a145e1]`
- Example, coal (`name=Kohle`): `metric=tonnen`, `catg=2`, staged values 58 to 32 km, 45 to
  48, 23 to 80, 20 to 240, 0 beyond; `speed_bonus=0`; `weight_per_unit=1000`.
  `[CODE New master @ 7a0a145e1]`

## Categories

- The file header defines categories: 0 unique, 1 piece goods, 2 bulk, 3 oil fluid,
  4 refrigerated piece goods, 5 liquid food, 6 long goods, 7 fabric and lightweight packed
  goods. `[CODE New master @ 7a0a145e1]`
- No current entry uses category 5 or 7. `[CODE New master @ 7a0a145e1]`
- Categories drive which vehicles can carry which goods; see [vehicle](vehicle.md) and the
  per-good `freight=` assignments on vehicles and industries.

## Historical rate sources

- The file header records the rating basis: Ackworth's Liverpool and Manchester Railway per
  ton per mile figures by value class, the later Railway Clearing House classification A to
  V with per-class distance-tapered maxima, and the 1844 Act equivalence of 80 cents per mile
  to 1d at 1900 levels. `[CODE New master @ 7a0a145e1]`
- Freight goods carry their Railway Clearing House class as a comment, for example iron ore
  is annotated class A. `[CODE New master @ 7a0a145e1]`
- For how these rates convert to in-game revenue, see [balancing](../balancing.md).

## Speed values

- `New/config/speedbonus.tab` holds per-waytype values by year. Its header notes that for
  Simutrans-Ex all land-based values should be equal except water transport.
  `[CODE New master @ 7a0a145e1]`
- The Standard speed bonus does not set revenue in Extended; revenue follows goods type,
  quantity, distance, class and comfort.
  `[FORUM:https://forum.simutrans.com/index.php/topic,1959.0.html]`
- The per-good `speed_bonus` key is deprecated in Extended and has no effect on revenue:
  fare calculation (`get_total_fare`) no longer uses it.
  `[CODE simutrans-extended master @ 7655609]`
- Its only remaining engine use is the waiting-too-long discard check in overcrowded stops:
  goods with a zero bonus are never discarded for waiting, and other goods wait at most the
  passenger maximum divided by their bonus.
  `[CODE simutrans-extended master @ 7655609]`

## Open questions

- What is the authoritative list of goods supported by Simutrans-Extended, and how should the
  pakset's list track it?
