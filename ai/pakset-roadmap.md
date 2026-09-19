---
status: draft
verified: none
---
# Pakset roadmap

**Covers**: the registry of planned pakset work: assets to add, gaps to fill, and changes needed
for new engine features.

## Notes

- Read this when planning what to add in what order. Check it after completing work and close the
  relevant entry ([conventions](conventions.md), "Adding assets and features").
- The project's current long-term priorities are listed in [../../AGENTS.md](../../AGENTS.md):
  supporting the forthcoming 15.x engine version, historical balancing, new vehicles and objects,
  filling gaps, and matching new engine features.

## Planned work

- Convert all remaining graphics from the old special-colour background to anti-aliased alpha
  transparency. Many graphics still use the old system, and the aim is to convert all of them. See
  [image-layout](graphics/image-layout.md) and [blender-rendering](graphics/blender-rendering.md).
  `[RECOLLECTION:2026-09-19]`
- Recreate missing `.blend` source files for existing graphics that lack them, so that those
  graphics can be converted and maintained. This notably applies to most London Underground
  vehicles; there is no `london-underground` folder in the blend repository.
  `[RECOLLECTION:2026-09-19]` `[CODE GitBlends master @ 1c1acf58]`

## Open questions

- What other work items should be entered, and in what order?
