---
status: stub
verified: none
---
# Industry (`factory`)

**Covers**: `Obj=factory` objects; industries, and the goods they produce and consume.

## Initial facts

- Source folder: `New/industry/`. Example properties (from `brewery.dat`) include `name`,
  `intro_year`, `intro_month`, `retire_year`, `retire_month`, `copyright`, `level`, and
  `population_and_visitor_demand_capacity`. `[CODE New master @ e36ec2321]`
- Industrial buildings can also be `Obj=building` with `type=ind`; these are distinct from
  factories. See [city-buildings](buildings/city-buildings.md).
  `[CODE New master @ e36ec2321]`
- Goods definitions are a separate object type; see [good](good.md).

## Planned sections

- Factory fields and their meaning.
- Goods chains, production, consumption, and capacities.
- Era coverage and historical realism of industry introduction and retirement.

## Open questions

- Where is the authoritative list of goods and their properties in the engine?
- How should the pakset's goods and factory data stay aligned with engine changes?
