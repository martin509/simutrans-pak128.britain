---
status: draft
verified: none
---
# Liveries and special colours

**Covers**: the engine's special-colour table and transparency, and the livery system the pakset
uses.

## Special colours

The engine defines 31 special colours. A pixel is a special colour only when its 24-bit RGB value
exactly matches one of these; there is no palette-index meaning.
`[CODE simutrans-extended master @ f378cf551]`

| Index | RGB | Meaning |
|---|---|---|
| 0–7 | `0x244B67`, `0x395E7C`, `0x4C7191`, `0x6084A7`, `0x7497BD`, `0x88ABD3`, `0x9CBEE9`, `0xB0D2FF` | Player colour 1, eight shades |
| 8–15 | `0x7B5803`, `0x8E6F04`, `0xA18605`, `0xB49D07`, `0xC6B408`, `0xD9CB0A`, `0xECE20B`, `0xFFF90D` | Player colour 2, eight shades |
| 16 | `0x57656F` | Dark windows, lit yellowish at night |
| 17 | `0x7F9BF1` | Lighter windows, lit bluish at night |
| 18 | `0xFFFF53` | Yellow light |
| 19 | `0xFF211D` | Red light |
| 20 | `0x01DD01` | Green light |
| 21–25 | `0x6B6B6B`, `0x9B9B9B`, `0xB3B3B3`, `0xC9C9C9`, `0xDFDFDF` | Non-darkening greys 1–5 (menus) |
| 26 | `0xE3E3FF` | Nearly white by day, yellowish at night |
| 27 | `0xC1B1D1` | Windows, lit yellow |
| 28 | `0x4D4D4D` | Windows, lit yellow |
| 29 | `0xFF017F` | Purple light |
| 30 | `0x0101FF` | Blue light |

The transparency special colour is `0x00E7FFFF` (the `SPECIAL_TRANSPARENT` constant). Pixels with
an alpha byte at or above 248 are also treated as transparent.
`[CODE simutrans-extended master @ f378cf551]`

Because a special colour is matched exactly, any image that needs one must contain the exact RGB
values above. The Blender render script's `sp_` mask mode was intended for this, but the current
workflow states that it is obsolete and belongs to a different pakset, and it should be ignored.
The current workflow uses alpha transparency, and special colours are needed only for multi-tile
buildings and for objects that use player colours (which this pakset does not).
`[FORUM:https://forum.simutrans.com/index.php/topic,2401.msg162208.html#msg162208]`

## Day/night and night window lighting are not used

This pakset does not use the day/night cycle or night window lighting. The window and light
special colours (dark windows, lighter windows, yellow/red/green/purple/blue light, and the
nearly-white day/night colour, indices 16–20 and 26–30) are therefore not used by this pakset.
The non-darkening greys (21–25) are for menus and are separate. This is consistent with the render
script's `sp_` mask mode being obsolete. `[RECOLLECTION:2026-09-19]`

## Player colours are not used by this pakset

The pakset does not currently use player colours (indices 0–15). It uses Simutrans-Extended's
livery system instead. `[RECOLLECTION:2026-09-19]`

## The livery system

A vehicle declares named liveries with `LiveryType[i]`, and supplies a separate image set for
each livery through the livery index of `EmptyImage[dir][livery]` and
`FreightImage[type][dir][livery]`. The example in `New/trains/4-wheel-1860s.dat` lists 11 liveries
and a separate eight-direction image set for each.
`[CODE New master @ e36ec2321]` `[CODE simutrans-extended master @ f378cf551]`

The pakset also has a `New/livery-trains/` source folder. `[CODE New master @ e36ec2321]`

Liveries are built in the Blender model from separate coloured polygons (planes), or from textures
applied to the model; the pakset graphics guide describes both methods. They are not built from
player colours. `[FORUM:https://forum.simutrans.com/index.php/topic,2401.0/all.html]`

## Standard livery colours

- The authoritative and periodically updated list of standardised livery colours, given as Blender
  HSV values, is the forum post
  https://forum.simutrans.com/index.php/topic,2401.msg140831.html#msg140831
  `[FORUM:https://forum.simutrans.com/index.php/topic,2401.msg140831.html#msg140831]`. Read that
  post at task time.
- It is not copied here, because it is updated periodically; see
  [conventions](../conventions.md) on pointing to changing data rather than duplicating it.
- The rules stated in that post: values are HSV; the value (intensity) is 0.800 unless the entry
  gives another figure; interior windows, and only interior windows, are `fg0,0,0`; any colour
  named "black" should be about `0,0,0.1`; aircraft use textures rather than Blender colours; and
  the list covers standardised liveries only, not non-standard items or non-livery parts such as
  wheels.

## Open questions

- How does Simutrans-Extended's livery system select a livery at runtime, and where is a livery
  scheme defined in pakset data?
- Which special colours (indices 16–30) does this pakset actually use, and for which images?
- Which objects still require special colours, given that only multi-tile buildings now need
  post-processing?
- Should a snapshot of the standard livery colours be kept in the knowledge base, or is reading the
  forum post at task time acceptable?
