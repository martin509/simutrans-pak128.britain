---
status: draft
verified: none
---
# Documentation conventions

Rules for this knowledge base. Read before interpreting tags or provenance records, or writing
or updating any doc. Content-architecture rules (what belongs in docs, visibility, size):
[documentation-architecture](documentation-architecture.md).

## Lifecycle

Frontmatter `status:` — `stub` → `draft` → `reviewed`. Stubs hold scope, retrieval key and
planned sections only (plus tagged initial facts). `reviewed` means the user has checked the
content in an interactive walkthrough ([documentation-architecture](documentation-architecture.md)
core rule 8).

## Provenance

Frontmatter `verified:` — the repository, branch and short commit against which the doc's
content was last checked (for example `New master @ e36ec2321`), or `none`. Stubs keep `none`;
initial facts carry their own inline provenance records instead. Update this value on every
substantive update.

## Doc structure

Retrieval keys ("read when") live in exactly one place per doc: top-level docs are keyed in
[index](index.md); nested docs are keyed in their parent doc, chaining up through any number of
layers to the index. An agent must be able to pick the right docs by following these keys from
the index, without speculative opening. Every new top-level doc gets its read-when key added to
the index at creation.

Each doc: Title → **Covers** (files/dirs) → content sections → **Open questions**.
Typical sections: overview and purpose · invariants · known problems and history · coarse
provenance notes. Record the latest correct position only; never record temporally specific or
ephemeral information (for example, "after the last update to..."). Prefer updating over
appending. When updating, take a whole-document view and craft the smallest text that gives the
next reader all necessary information and no unnecessary information. Re-arranging is allowed if
care is taken to preserve all necessary data.

## Mechanics

- Relative markdown links only (Obsidian and GitHub compatible). AGENTS.md uses plain paths.
- Target at most 300 lines per doc; when exceeded, split into multiple linked documents.
- For complex topics, nest documents (for example Index > topic > subtopic 1 | subtopic 2 |
  subtopic 3 > sub-subtopic 1A | sub-subtopic 1B).
- Filenames: lowercase-kebab-case.
- Agents propose doc changes; the user approves before commit (AGENTS.md hard rule 10).
- Do not reference documents by line number or by other details that change as files are edited.
- Prefer an open question over an unverified claim, always.

## Adding assets and features

- Before starting a planned asset or feature, check [pakset-roadmap](pakset-roadmap.md). When
  the work is complete, close its roadmap entry.

## Bugs

- Before investigating a reported or suspected bug, check [known-bugs](known-bugs.md). After
  fixing a bug, DELETE its entry (and any dedicated bug doc) from that doc. HARD RULE: only open
  bugs are listed there; fixed bugs are never kept — fix history lives in `FIX:` commit messages.
- Add every newly discovered open bug (including ones deliberately not fixed) to
  [known-bugs](known-bugs.md) with a priority 0–4. Simple bugs are described inline there;
  complex bugs get their own dedicated doc linked from it.
