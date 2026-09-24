---
status: stub
verified: none
---
# Program text and dummy info objects

**Covers**: `Obj=program_text` and `Obj=dummy_info` objects; support objects for translations
and for extra translation entries that have no object of their own.

## Initial facts

- Source folder: `New/simutranslator/`. Files include `catg_text_for_translator.dat`
  (`program_text` category names), `program-texts.dat` (`program_text` direction names),
  and `factory_details.dat` (`dummy_info` factory detail entries).
  `[CODE New master @ e36ec2321]`
- These objects exist to supply translatable text and are handled by the simutranslator
  workflow; see [translations-and-text](../translations-and-text.md).
  `[CODE New master @ e36ec2321]`

## Planned sections

- How `program_text` and `dummy_info` objects are used by Simutrans-Extended.
- The simutranslator packaging workflow.

## Open questions

- What is the complete set of program text keys the engine expects?
