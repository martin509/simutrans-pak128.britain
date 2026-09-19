---
status: stub
verified: none
---
# Pakset compatibility

**Covers**: how changes to pakset `.dat` values interact with savegames and network
compatibility, and the restrictions on changing them.

## Notes

- AGENTS.md hard rule 9: do not change `.dat` fields, object capacities, constraints, or other
  save/load-relevant values in a way that breaks savegame or network compatibility without first
  reading the relevant docs and presenting the intended change to the user.
- The engine is the authority on which fields are save-relevant; this project must determine
  that from the engine source rather than assume it. `[UNVERIFIED]`

## Planned sections

- Which `.dat` fields and value changes are save/load-relevant and which are not.
- How existing savegames reference pakset objects (by name, index, or other key).
- Safe procedures for retiring, renaming, or replacing objects.

## Open questions

- Which engine files define savegame compatibility for pakset objects, and how should docs point
  to them?
- What is the safe procedure for changing an object's capacity or constraints without breaking
  existing games?
