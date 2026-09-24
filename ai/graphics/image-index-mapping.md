---
status: draft
verified: none
---
# Image index mapping by object type

**Covers**: what each image index means for every object type the pakset uses. Index names are as
written in the `.dat`; the engine is the authority. `[CODE simutrans-extended master @ f378cf551]`

## Shared orders

- Eight-point compass order used by vehicle, city car, pedestrian, and ground object:
  `S, W, SW, SE, N, E, NE, NW` (engine direction values 0–7).
- RIBI order used by way, way object, and tunnel, 16 values:
  `-, N, E, NE, S, NS, SE, NSE, W, NW, EW, NEW, SW, NSW, SEW, NSEW`, then the switch slots
  `NSE1, NEW1, NSW1, SEW1, NSEW1, NSE2, NEW2, NSW2, SEW2, NSEW2` (slots 16–25).
- Way slope labels: the `.dat` uses `ImageUp[3]` = north, `[6]` = west, `[9]` = east,
  `[12]` = south. `ImageUp` is the single slope; `ImageUp2` is the double slope.
- Way diagonal order: `NE, SE, NW, SW`.

## Vehicle (`Obj=vehicle`)

- `EmptyImage[dir]` or `EmptyImage[dir][livery]`.
- `FreightImage[dir]`, `FreightImage[dir][livery]`, `FreightImage[type][dir]`, or
  `FreightImage[type][dir][livery]`, where `type` is the index into `FreightImageType[i]`.
- `LiveryType[i]` names the liveries selected by the livery index.
- Directions must be 4 or 8; if any of the second four directions is present, all eight must be.
  A missing direction `dir>3` falls back to `dir-4`. The pakset's rail vehicle example uses 8
  directions with `EmptyImage[S][0]` form and 11 `LiveryType` entries.
  `[CODE New master @ e36ec2321]`

## Building (`Obj=building`)

- `BackImage[l][y][x][h][phase][season]` and `FrontImage[l][y][x][h][phase][season]`.
- `l` = layout, `y` and `x` = tile position within the layout, `h` = height index, `phase` =
  animation frame, `season` = season. With `seasons == 1` the `[season]` index may be omitted.
- Tile order is layout outer, then `y`, then `x`. `Dims=x,y,layouts`; layouts may be 1, 2, 4, 8,
  or 16. Front images may be only one tile high.
- The pakset example `1950s-terminal-building.dat` uses `BackImage[0..3][0][0][0][0][0]` for four
  heights. `[CODE New master @ e36ec2321]`

## Way (`Obj=way`)

- `Image[ribi][season]` and `FrontImage[ribi][season]` use the RIBI order.
- `ImageUp[slope][season]` and `ImageUp2[slope][season]` use the slope labels above.
- `Diagonal[ribi][season]` and `FrontDiagonal[ribi][season]` use the diagonal order.
- A base image (`Image[-]`) is required. Extra switch images use the `NSE1`… slots.
- The pakset example `tram_track.dat` lists all 16 RIBI values, four `ImageUp`, and four
  `ImageUp2`. `[CODE New master @ e36ec2321]`

## Way object (`Obj=way-object`)

- `FrontImage[ribi]` / `BackImage[ribi]`, `FrontImageUp[slope]` / `BackImageUp[slope]`,
  `FrontImageUp2[slope]` / `BackImageUp2[slope]`, and `FrontDiagonal[ribi]` /
  `BackDiagonal[ribi]`, in the same orders as ways.

## Tunnel (`Obj=tunnel`)

- `FrontImage[n|s|e|w][season]` and `BackImage[n|s|e|w][season]`; portal variants add `l`, `r`,
  or `m` (for example `FrontImage[nl]`).
- Underground images: `FrontUndergroundImage[ribi]` / `BackUndergroundImage[ribi]`, plus `Up` and
  `Up2` slope forms and `Diagonal` forms.

## Bridge (`Obj=bridge`)

- `BackImage[ns|ew]`, `FrontImage[ns|ew]`, `BackStart[n|s|e|w]`, `FrontStart[...]`,
  `BackRamp[...]`, `FrontRamp[...]`, `BackPillar[s|w]`, `FrontPillar[...]`, and a second set with
  the same names ending in `2`; optional `[season]`.

## Tree (`Obj=tree`)

- `Image[age][season]`, age 0–4. `seasons=2` gives 0 = summer, 1 = winter; a five-season tree
  orders 0 = summer, 1 = autumn, 2 = winter, 3 = spring.
- The pakset example `tree.dat` uses `Image[0..4][season]`. `[CODE New master @ e36ec2321]`

## City car (`Obj=citycar`)

- `Image[dir]`, eight-point compass order. The pakset example uses `Image[E]=...,-33,14` with
  explicit offsets. `[CODE New master @ e36ec2321]`

## Pedestrian (`Obj=pedestrian`)

- `Image[dir]`, or `Image[dir][frame]` when animated; up to 500 frames per direction.

## Crossing (`Obj=crossing`)

- `OpenImage[ns|ew][i]`, `FrontOpenImage[ns|ew][i]`, `ClosedImage[ns|ew][i]`,
  `FrontClosedImage[ns|ew][i]`, where `i` is the animation phase.

## Road sign (`Obj=roadsign`)

- `Image[0]` upward, up to 48, and the list must stop at a multiple of 4. More than four images
  means the sign is a traffic light. `Cursor` and `Icon` are supported.

## Ground (`Obj=ground`)

- `Image[slope][phase]`, slope 0–127. The pakset's animated water uses `Image[0][0..n]` for its
  animation frames. `[CODE New master @ e36ec2321]`

## Ground object (`Obj=ground_obj`; not currently present)

- Fixed object: `Image[phase][season]`. Moving object (`speed != 0`): `Image[dir][season]`.

## Factory (`Obj=factory`)

- Images come from its associated building (the building `BackImage`/`FrontImage` rules), from a
  `Smoke` object, and from `Fields`. Field images are frames, and with snow the last frame is the
  snow image.

## Pier (`Obj=pier`)

- `BackImage[slope][rotation][season]` and `FrontImage[slope][rotation][season]`, slope 0–80,
  rotation as the object's rotational symmetry. Reserved indices exist for tool icons, cursors,
  parapets, and the way deck.

## Skin, smoke, field, misc

- `Image[i]` sequential frames, no directions. For smoke, the frame shown is selected by the
  engine from the purchase time; for fields, the last frame is snow when snow is present.

## Cursor and icon

- `Cursor` and `Icon` are separate properties for many object types. They are stored as one
  cursor node where index 0 is the cursor and index 1 is the icon.

## Open questions

- Which types require a fixed number of directions in the pakset, and which may be 4 or 8?
- For trees, what is the exact season order for a five-season tree in this pakset?
