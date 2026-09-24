---
status: stub
verified: none
---
# Releases and versioning

**Covers**: making a release and incrementing the pakset version.

## Initial facts

- `New/Makefile` has an `archives` target that produces `$(DESTFILE).tbz2` and `$(DESTFILE).zip`
  (`DESTFILE ?= simupak128.Britain-Ex`). `[CODE New master @ e36ec2321]`
- `New/readme.txt` records the release history from the early "1.0 (beta)" release of 7th July
  2009 onwards. `[CODE New master @ e36ec2321]`

## Planned sections

- How the version is set and where it appears.
- The release build and archive steps.
- What a release includes and how it is announced.

## Open questions

- Where is the version string currently set, and is `VERSION_STRING` in `New/Makefile` still
  used?
- What is the current release procedure end to end?
