# ai77: Specifications

ai77 is a playground for visualizing medical records.

These specs describe **what** ai77 does and the **contracts** an
implementation must satisfy. They intentionally say nothing about
frameworks, languages or libraries, so the implementation can change
without the behavior changing.

Implementations live in their own top-level directories and must conform
to these documents. If an implementation needs to deviate from a spec,
update the spec first. Code is never the source of truth for behavior.

## Documents

- [Overview](overview.md): product scope, goals and non-goals
- [Privacy](privacy.md): what data may enter the repo and the app, and how
  it's handled
- [Accessibility](accessibility.md): readable, colorblind-safe
  visualizations everywhere
- [Import from 1177](import-1177.md): reading pages saved from 1177
  Journalen, safely and without silently dropping anything
- [Data model](data-model.md): the normalized form of the records that
  every view reads

New documents start from [`_template.md`](_template.md).

## Conventions

- One topic per document. A new area gets a new document rather than being
  bent into an existing one.
- Each document ends with an **Open questions** section. Unresolved
  decisions live there, not as guesses in code.
- Use "must" for hard requirements and "should" for strong defaults.
  Every "must" should be testable.
