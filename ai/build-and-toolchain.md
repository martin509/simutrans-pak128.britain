---
status: draft
verified: New master @ 92c7b701c
---
# Build and toolchain

**Covers**: how the pakset is compiled from `New/`, the build files, and makeobj.

## Initial facts

- Canonical build: run GNU make from inside `New/` via Git Bash / MSYS2. `New/mkpak.sh` runs
  `make clean DESTDIR=../../simutrans-extended-sources/simutrans; make DESTDIR=... -j12`.
  `[CODE New master @ e36ec2321]`
- `New/Makefile` uses `MAKEOBJ ?= ./makeobj-extended` and `DESTDIR ?= .`; the pakset is written
  to `$(DESTDIR)/pak128.Britain-Ex`. `[CODE New master @ e36ec2321]`
- Each source folder is compiled as one `.pak` with a size class: `PAK32`, `PAK64`, `PAK128`,
  `PAK192`, `PAK224`, `PAK256` (the folder-to-size mapping is in the `DIRS32`/`DIRS64`/`DIRS128`
  and similar variables in `New/Makefile`). `[CODE New master @ e36ec2321]`
- The `copy` target copies `config/`, `text/`, `sound/`, `demo.sve`, `licence.txt`, `compat.tab`,
  and `symbol.BigLogo.pak` into the built pakset; these are used directly and not compiled.
  `[CODE New master @ e36ec2321]`
- `New/makeALL.mos` (MOScript, run with mose.py) is an alternative build; `New/parameter.mos`
  defines the absolute makeobj path and output directory. `New/pak128Britain.bat` is a further
  Windows alternative. `[CODE New master @ e36ec2321]`
- Several makeobj builds are present in `New/` (for example `Makeobj-Extended.exe`,
  `Makeobj-Extended-ex-15.exe`, `makeobj-extended`). makeobj binaries are ignored by
  `New/.gitignore`. `[CODE New master @ e36ec2321]`
- `New/Makefile` also has a `simutranslator` target that packages `.dat` and `.png` files into
  zips for upload to simutranslator. `[CODE New master @ e36ec2321]`

## Build destination and engine workspace

- `New/mkpak.sh` passes `DESTDIR=../../simutrans-extended-sources/simutrans` for both `make
  clean` and `make -j12`. The destination is the engine workspace in the directory adjacent to
  this base directory. `[CODE New master @ 92c7b701c]`
- `New/Makefile` defaults `DESTDIR` to the current directory and writes the pakset to the
  `pak128.Britain-Ex` subdirectory of the destination. `[CODE New master @ 92c7b701c]`
- `New/parameter.mos` defines the `!makeobj` executable path and the `!OUTPUT` directory as
  absolute paths inside the same engine workspace. `[CODE New master @ 92c7b701c]`

## Alternative builds and observed differences

- `New/makeALL.mos` declares `!mose min_version 3` and sets `!size` per folder. Its copy set
  includes `readme.txt` in addition to the `New/Makefile` copy set of `config/`, `text/`,
  `sound/`, `demo.sve`, `licence.txt`, `compat.tab`, and `symbol.BigLogo.pak`.
  `[CODE New master @ 92c7b701c]`
- `New/pak128Britain.bat` takes a destination argument and a source argument. It compiles the
  `config/` folder into `BritConfig-Ex`, while `New/Makefile` copies `config/` directly without
  compiling. Its `PAK32` step writes `Holds256-Ex` from `boats/holds/`.
  `[CODE New master @ 92c7b701c]`
- `New/.gitignore` excludes `makeobj-extended*`, `*.exe`, `*.pak`, and `*.sve`. The makeobj
  binaries present in `New/` are therefore untracked. `[CODE New master @ 92c7b701c]`

## Planned sections

- Which makeobj build is correct for which engine branch/version, and how that is determined.
- Known build pitfalls.

## Open questions

- Which makeobj executable is authoritative for current engine work, and how should its version
  be matched to the engine?
- Is the canonical build the `make` path, or should it be documented differently for releases?
