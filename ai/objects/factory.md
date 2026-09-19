---
status: draft
verified: New master @ 96a2c9593
---
# Industry (`factory`)

**Covers**: `Obj=factory` objects; industries, and the goods they produce and consume.

## Overview

- Source folder: `New/industry/`. Each factory combines a factory node with an embedded
  building node, so both factory fields and building fields apply.
  `[CODE New master @ f8859c42d]`
- A factory declares the goods it consumes (`inputgood`) and produces (`outputgood`) with
  factors and capacities, its `productivity`, its `location` siting rule, optional
  `fields` for raw-material areas, and staff and visitor demand. Full field-by-field
  explanation: [factory-fields](factory-fields.md).
- Industrial buildings can also be `Obj=building` with `type=ind`; these are distinct from
  factories. See [city-buildings](buildings/city-buildings.md).
  `[CODE New master @ e36ec2321]`
- Goods definitions are a separate object type; see [good](good.md).
- For how production is calibrated against the time system and town size, see
  [balancing](../balancing.md).

## Open questions

- Where is the authoritative list of goods and their properties in the engine?
- How should the pakset's goods and factory data stay aligned with engine changes?
