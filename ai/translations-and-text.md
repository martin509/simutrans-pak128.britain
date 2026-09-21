---
status: stub
verified: none
---
# Translations and text

**Covers**: user-facing text: `text/` `.tab` files, city name lists, simutranslator, and object
names.

## Initial facts

- `New/text/` contains translation `.tab` files (for example `be.tab`, `ca.tab`) and city name
  lists (`citylist_*.txt`, with a `citylists/` subfolder). These are copied into the built pakset
  rather than compiled. `[CODE New master @ e36ec2321]`
- The `simutranslator` target in `New/Makefile` packages `.dat` and `.png` files into zips for
  upload to simutranslator. `[CODE New master @ e36ec2321]`

## Planned sections

- How object names and texts are translated and uploaded.
- City name list conventions and variants.
- Program texts and `simutranslator` workflow.

## Open questions

- What is the current simutranslator workflow for this pakset?
