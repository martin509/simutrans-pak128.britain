---
status: stub
verified: none
---
# Repository map

**Covers**: the workspace tree; which folders are authoritative sources, which are historical or
clutter, and which repositories are in scope.

## Initial facts

- The base workspace ("PakBritain sources") is NOT a git repository. `[CODE base filesystem, 2026-09-19]`
- In-scope git repositories:
  - `New/` — main pakset sources (branch `master`). `[CODE New master @ e36ec2321]`
  - `Git Blends/Pak128.Britain-blends/` — Blender `.blend` meta-sources (branch `master`).
    `[CODE GitBlends master @ 1c1acf58]`
- `.git` directories also exist in `Experimental/`, `Standard/`, `Standard-git/`, and `SVN/`.
  These folders are ordinary folders for this project; do not run git commands in them or
  otherwise interact with those repositories (AGENTS.md). `[CODE base filesystem, 2026-09-19]`
- `New/` object folders are compiled by makeobj into `.pak` files; the folder-to-pak mapping is
  in `New/Makefile`. Top-level object folders include `air/`, `attractions/`, `boats/`, `bus/`,
  `citybuildings/`, `citycars/`, `depots/`, `goods/`, `grounds/`, `gui/`, `hq/`, `industry/`,
  `london-underground/`, `maglev/`, `narrowgauge/`, `pedestrians/`, `piers/`, `signalboxes/`,
  `smokes/`, `stations/`, `townhall/`, `trains/`, `trams/`, `trees/`, and `ways/`.
  `[CODE New master @ e36ec2321]`
- `New/trains/` is subdivided into `carriages/`, `horses/`, `locomotives/`, `railcars/`, and
  `wagons/`. `[CODE New master @ e36ec2321]`
- `New/config/`, `New/text/`, and `New/sound/` are copied directly into the built pakset rather
  than compiled. `[CODE New master @ e36ec2321]`
- The base root contains a large amount of loose clutter (`.blend`, `.zip`, `.7z`, `.pdf`, `.xls`,
  `.csv`, images, and similar). It is not authoritative. Some items may contain useful research or
  balancing material and may be read during a documentation run, but it is otherwise ignored
  unless docs or prompts say otherwise (AGENTS.md). `[CODE base filesystem, 2026-09-19]`

## Planned sections

- A map of which non-authoritative folder holds what kind of historical material worth reading.
- The relationship between files in `New/` and their `.blend` sources in
  `Git Blends/Pak128.Britain-blends/`.

## Open questions

- Which of the historical folders (`Experimental/`, `Standard/`, `Standard-git/`, `SVN/`,
  `Ways-190109/`, `pak/`, `blends/`, `buses/`, `trains/`, `goods/`, `industry/`, `images/`) hold
  material still worth consulting, and for what?
