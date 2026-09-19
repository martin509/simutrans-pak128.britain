---
status: draft
verified: none
---
# Pak format and objects

**Covers**: `.dat` object files, `.png` images, makeobj output, and how graphics attach to
objects.

## Pipeline

- The running game never reads `.dat` or `.png`. `makeobj` reads the `.dat` files and the `.png`
  files they reference and writes `.pak` files; the engine loads `.pak` files and turns the
  stored images into 16-bit run-length-encoded pixel data. `[CODE simutrans-extended master @ f378cf551]`
- Each `.dat` declares its object type with an `Obj=...` line. makeobj compiles a whole folder
  into one `.pak`, and the folder-to-pak mapping is in `New/Makefile`, together with the image
  size class passed to makeobj (`PAK32`, `PAK64`, `PAK128`, `PAK192`, `PAK224`, `PAK256`).
  `[CODE New master @ e36ec2321]`
- `New/config/`, `New/text/`, and `New/sound/` are copied into the built pakset directly and are
  not compiled. `[CODE New master @ e36ec2321]`
- The object types the pakset uses are listed in [object-types](object-types.md).

## How graphics attach to a `.dat`

An object lists its images through properties whose names depend on its type. Each value is a
string naming a `.png` file and a cell inside it. The string grammar, the PNG rules, and the
index meaning for every type are in [image-layout](graphics/image-layout.md) and
[image-index-mapping](graphics/image-index-mapping.md).

Examples taken from the pakset:

- Vehicle: `EmptyImage[S][0]=./carriages/lnwr-4wheel-1860s-first_S.0.0`, where the second index
  selects a livery; also `FreightImage[...]` and `LiveryType[i]`.
  `[CODE New master @ e36ec2321]`
- Building: `BackImage[l][y][x][h][phase][season]=...` and `FrontImage[...]`; plus `Icon` and
  `Cursor`. `[CODE New master @ e36ec2321]`
- Way: `Image[ribi][season]`, `ImageUp[slope]`, `ImageUp2[slope]`, `Icon`, `Cursor`.
  `[CODE New master @ e36ec2321]`
- City car: `Image[dir]=./images/austin-light-twelve-blue_E.0.0,-33,14`, with an explicit
  placement offset. `[CODE New master @ e36ec2321]`
- Tree: `Image[age][season]`. `[CODE New master @ e36ec2321]`
- Ground: `Image[slope][phase]`. `[CODE New master @ e36ec2321]`

## Values that are read from the same `.dat`

Besides images, a `.dat` carries the object's economic and behavioural fields. Vehicle
fields are explained in [vehicle fields](objects/vehicle-fields.md); goods fields in
[goods](objects/good.md). Building, factory, way and other fields will be explained in
their per-type docs as those docs are elaborated; some of them are save/load-relevant, so
see [pakset-compatibility](pakset-compatibility.md) before changing them.
`[CODE New master @ e36ec2321]`

## Validation and common errors

makeobj fails or warns in these cases, among others (engine authority):

- PNG width or height not an exact multiple of the cell size: fatal `Invalid image size`.
- A value with no image number, an unreadable file, or a cell outside the sheet: fatal.
- A building front image more than one tile high: error `Frontimage height MUST be one tile
  only!`.
- A vehicle with other than 4 or 8 directions; missing freight images; missing livery types:
  fatal.
- A way without its base image; a crossing without its required images; a tree or ground object
  with a missing season image: fatal. `[CODE simutrans-extended master @ f378cf551]`

## Open questions

- Which object types are compiled with which size class, and why the exceptions (192, 224, 256)?
- Are there fields that makeobj silently ignores, and which are those?
