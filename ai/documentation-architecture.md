---
status: draft
verified: none
---
# Documentation architecture

Content-architecture constraints for this knowledge base. Mechanics (tags, provenance records,
links, lifecycle) live in [conventions](conventions.md). Read before authoring or restructuring
any doc.

## Core rules

1. **Document systems, not volatile details.** Docs describe stable structures, mechanisms and
   invariants; per-object, per-version detail belongs to the `.dat` and `.png` files and rots in
   docs. Example: [balancing](balancing.md) documents the calibration method and the sources of
   realism; it never lists every vehicle's current price, speed or intro date.
2. **Point, don't duplicate.** Prefer symbol anchors (file plus object or property name) over
   copied `.dat` listings. Never use line-number anchors — line numbers shift and silently
   mislead.
3. **Visibility rule.** Cross-cutting facts an agent might not know to look for go in
   [project-notes](project-notes.md) — short, and read on most tasks — not only in a domain doc,
   which a reader consults only if they already suspect the constraint applies.
4. **One canonical location per fact.** Mandatory invariants → [pakset-compatibility](pakset-compatibility.md)
   and [pak-format-and-objects](pak-format-and-objects.md); narrative/history/origin →
   [project-overview](project-overview.md); planned work and status → [pakset-roadmap](pakset-roadmap.md).
   Everything else cross-links; never copies.
5. **Size limits.** Small docs; at most 300 lines ([conventions](conventions.md)). When a
   domain's doc exceeds the limit, split into a `New/ai/<topic>/` subfolder and update
   [index](index.md).
6. **Provenance.** Every claim tagged per [conventions](conventions.md); prefer open questions
   over unverified claims, always.
7. **No transient or git-derivable data.** Docs must NOT record asset counts, file or line
   counts, current version values, branch-tip hashes, or "as of" statements. Record stable
   structure and interpretation instead; agents derive live numbers from the files at task time.
8. **Reviews are interactive.** A doc reaches `reviewed` only after the agent has walked the user
   through it in a structured question session, in batches: presenting claims for confirmation or
   correction, asking about the doc's open questions, and recording answers with
   `[RECOLLECTION:<date>]` tags. Agent-side checking alone never sets `reviewed`.
9. **Lazy elaboration.** Stubs are fleshed out only when real work needs them. Docs that the
   current work programme makes mandatory reading are elaborated proactively; other domain docs
   stay stubs until a first task in that domain requires detail. Do not generate detail
   speculatively.

## Inventory policy

- Top-level docs get an index key at creation; nested docs get their read-when keys from their
  parent doc, chaining up to the index. Stubs start with Covers plus planned sections only.
- Stubs may contain tagged initial facts; drafts contain verified system descriptions;
  `reviewed` means the user has checked the content in an interactive walkthrough (core rule 8).
