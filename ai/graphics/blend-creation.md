---
status: draft
verified: none
---
# AI .blend creation: status and failure record

**Covers**: the current status of AI-authored `.blend` work, the recorded failure modes of AI
geometry creation, and the verification doctrine that follows from them. Read before any task
that creates or reshapes `.blend` geometry, and before relying on any AI reading of a render
or screenshot. Parent: [graphics-pipelines](../graphics-pipelines.md); pipeline procedure:
[ai-pipeline](ai-pipeline.md).

## Current status

Per user direction, 2026-09-27 `[RECOLLECTION:2026-09-27]`:

- **Novel `.blend` creation is unstable.** From-scratch geometry, and freeform reshaping of
  existing geometry, are not currently workable unattended.
- **Minor `.blend` changes are workable**: simple livery or texture substitutions,
  re-rendering, and bounded numeric edits to existing models.
- **The pipeline from `.blend` to `.pak` is workable**: rendering, offsets, `.dat` writing,
  makeobj, and the map-generation smoke test are demonstrated end to end on two assets (the
  S69 and the DC-8-10).

## What is demonstrated to work

- **Donor inheritance** (DC-8-10): the blend is the 707 model rotated, rescaled to the 46 m
  rule, and re-liveried with 2D artwork on the existing UV layout; offsets were derived by
  silhouette cross-correlation against the shipped 707 sprites (IoU 0.90–0.96). The AI
  contributed execution only; the form was inherited from a human-made, shipped donor. See
  [aircraft-notes](aircraft-notes.md). `[EXECUTION-VERIFIED:2026-09-24]`
- **Bounded edits with human review gates** (S69 Belpaire transplant and smokebox fix).
  `[EXECUTION-VERIFIED:2026-09-23]`
- **Human-authored delta plus AI fan-out** (S69 five liveries): the user authored the
  correction by eye on the golden file; the AI applied a recorded list of named-object
  operations across the siblings with assertions (`s69_assert.py`). No visual inference in the
  fan-out. `[RECOLLECTION:2026-09-27]`
- **Scripted construction from constants** (B12/3 front-board prism, `b12_board.py`): geometry
  derived from numbers succeeded where moving vertices on a donor mesh failed. Rule: derive,
  never manipulate. `[RECOLLECTION:2026-09-27]`

## Failure record

From the 2026-09-26/27 sessions (S69 first attempt; B12/3 rebuild attempt)
`[RECOLLECTION:2026-09-27]` unless noted:

1. **Internal incoherence, not coarseness**: parts placed with no shared spatial logic
   (overlapping wheels, buffer beam halfway down the boiler, a part inside the boiler). A
   crude blockout is approximate and refines away; these were self-contradictory.
2. **Non-propagation**: the asset was handled as a bag of independent objects; a change to one
   part did not move the parts that depend on it (boiler lengthened, frames and handrail not).
3. **Materials bound by datablock, not by role**: one `Vermillion`-lineage material served
   both connecting rods and buffer beam, so a correct livery rule blackened the wrong part.
4. **Conceptual shapes stored as mesh**: the B12/3 frame profile is a polyline in (length,
   height); attempting it by moving vertices produced a mangled mesh.
5. **The recogniser does not fire**: text reported that did not exist; descriptions
   contradicted by measurement; re-rendering did not converge because misreadings recurred.
6. **Corrections applied but not reliably correct**: correcting an error requires the
   capability that failed.
7. **Circular verification**: golden values were read off the model being checked. State
   assertions cannot see a wrong-but-coherent model; dependency assertions can.

### Live recognition tests, 2026-09-27

`[EXECUTION-VERIFIED:2026-09-27]`

- Shown mangled-lineage vs golden-lineage screenshots (B12/3 vs S69) and asked which was
  mangled: file selection correct but arrived at through contaminated channels (legible
  window titles, prior records). The diagnosis was wrong on both sides: a false positive
  (healthy wheels reported as overlapping — parallax misread) and a false negative (the
  actually mangled frames not identified).
- Shown the pre-user-fix S69 and asked nothing specific: a nine-item candidate-defect list,
  of which the user falsified four outright (chimney reported absent — present; cab windows
  reported as black-void defect — correct openings; frames reported missing — present; a
  "brass rod" reported — no such object). Zero confirmed correct feature-level identifications
  across the session.
- **Mechanism**: priming + ambiguity + forced narration. Every false positive was an ambiguous
  image region (parallax, contrast, depth) resolved silently toward the primed expectation and
  narrated as a finding; confidence labels did not prevent it. Every false negative was a
  spec-comparison failure: correctness is not a perceptual property, and no camera angle
  supplies the spec. More angles resolved the ambiguities for the human observer; there is no
  instance of an additional view improving the AI's reading.

### External corroboration (retrieved 2026-09-27)

- BlenderGym (CVPR 2025, arxiv.org/abs/2504.01786): a code-based Blender editing benchmark
  with rendered feedback and verifier loops; from the abstract, "even the state-of-the-art
  VLM system struggles with tasks relatively easy for human Blender users." The failure
  replicates under controlled, well-tooled conditions and is not specific to this workspace.
- Successful LLM+3D systems route around fabrication: SceneCraft (ICLR 2024,
  arxiv.org/abs/2403.01248) does scene assembly via planning and asset retrieval; LL3M
  (arxiv.org/abs/2508.08228) writes Blender Python with a multi-agent team plus refinement;
  BlenderLLM is a model fine-tuned specifically for Blender CAD scripts. None use a
  general-purpose LLM for unattended metric fabrication from references.

## Verification doctrine

- **Query, don't view.** Facts about a `.blend` are fully determined in the file; rendering
  them into an image manufactures ambiguity. Query the scene graph for facts.
- **Never verify by AI description of an image**, at any granularity. Prose description of
  images is unreliable (three recorded instances plus the 2026-09-27 tests); pixel arithmetic
  between registered images is deterministic and is not what failed.
- **Prefer dependency assertions** ("did everything downstream of this change move?") over
  state assertions ("does it match these numbers?"): state assertions cannot see
  wrong-but-coherent models, and golden values rot when read off the model being checked.
- **Where a human-corrected golden exists, diff against the golden** (object lists, bounding
  boxes, materials) instead of describing renders.
- When rendering for comparison, include a ground reference in frame: floating parts are
  undetectable without one (a camera-placement problem, not a limit of renders).
- **The human gate**: one approval per asset, judged on final renders at sprite scale.
  Correctness is required at final rendered scale, with sub-threshold detail ignored; colour
  and pattern must be correct at render scale and liveries must match the in-pakset tables.
  `[RECOLLECTION:2026-09-27]`

## Scope conclusions

- Pakset blends are hand-built low-poly assemblies with variant parts held on scene layers
  (survey: [blender-rendering](blender-rendering.md), the ger-claud roundtrip record). There
  is no high-poly or retopology stage: form and detail must both be correct in the final mesh
  in one pass, because nothing downstream absorbs error. `[EXECUTION-VERIFIED:2026-09-26]`
- **Colour is never taken from a reference image**; in-pakset tables only (see
  [liveries-and-special-colours](liveries-and-special-colours.md)). A reference may inform
  which part is which, never what colour it is. `[RECOLLECTION:2026-09-27]`
- A reference image's residual roles are **qualitative character** (what dimensions do not
  state) and **cross-validating the data channel**. Scale comes from the data channel plus
  class constants (gauge, buffer height, wheel diameters), never from measuring an image.
  `[RECOLLECTION:2026-09-27]`
- Low render resolution **forgives donor type-substitution** (a 707 and a DC-8-10 differ by a
  few pixels at 128 px = 46 m) but **does not forgive placement errors**: silhouette and
  relative part placement are what survive at sprite scale.
  `[EXECUTION-VERIFIED:2026-09-24]` (donor half); the placement half is inference from the
  failure record. `[UNVERIFIED]`
- References are mixed media (B&W photo, colour photo, line drawing, vector drawing, text);
  class constants are permitted as scale anchors. `[RECOLLECTION:2026-09-27]`

## Verification tooling environment

Measured 2026-09-27 on the maintainer's machine `[EXECUTION-VERIFIED:2026-09-27]`:

- Blender 2.79 bundles Python 3.5.3 with numpy 1.10.1; Blender 2.81 bundles Python 3.7.4 with
  numpy 1.17.0. Neither bundles scipy or PIL. The `python` on PATH is 2.7.17.
- Matte-render recipe for probes (2.79): `use_shadeless` is on the **Material**, set via
  `render.layers[0].material_override`; `use_sky = False`; all lamps deleted. 2.79 has no
  `film_transparent`; `use_pass_material_index` and `use_pass_object_index` do exist.
- Matte render at 128×128 costs ~6 ms for one object and ~58 ms for 120 objects / ~26k
  polygons; cost tracks object count more than polygon count.
- **Tooling bug**: the shipped views are 30° elevation (the render script sets camera
  X-rotation 60°, i.e. 30° below horizontal). `vision_render.py` computes `radians(90 − elev)`,
  so its `--elev 30` reproduces the shipped views; its docstring's claim that `--elev 60`
  reproduces them is wrong, and comparisons made at `--elev 60` were taken from the wrong
  angle.

## Open questions

- Reference images are not documented as an input category anywhere in this knowledge base.
  What form should that record take (per-asset source lists, allowed uses, disallowed uses)?
- Would a blind, unprimed, multi-view protocol change the measured AI recognition failure
  rate? Current evidence gives no reason to expect so, but it has not been measured cleanly.
- What concrete form should the predicate battery take (per-class invariant tables, or a
  shared assertion library)?
- Under what demonstrated conditions, if any, could AI-authored novel geometry be committed in
  future? See also the acceptance open question in [ai-pipeline](ai-pipeline.md).
- Visual consistency across assets is only partially documented (brightness guidance in
  [blender-rendering](blender-rendering.md)); is a fuller treatment needed, and where should
  it live?
