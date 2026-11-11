# Working in this repository

ai77 is spec driven: the specification in [`specs/`](specs/README.md) is
the source of truth for behavior, and implementations conform to it. This
keeps behavior independent of any one technology choice, so an
implementation can be rewritten, or a second one added, and still behave
the same way.

## Rule: specs first

Any new requirement (a new feature, a changed behavior, a new constraint)
must be added to or updated in `specs/` in the same change, before or
alongside touching any implementation.

- A purely technical change with no user-visible or contract-level
  difference (swapping a library, refactoring) does not need a spec
  change.
- If you're unsure whether something is a spec-level requirement or an
  implementation detail, put it in `specs/`. It's cheap to document and
  expensive to lose track of.
- Never let an implementation be the only place a behavior is defined. If
  you find behavior in code that `specs/` doesn't describe, fix it by
  updating the spec, not by leaving it undocumented.
- Specs describe **what** and **why**, never frameworks, languages or
  libraries.
- When a spec is ambiguous, don't guess in code. Record the question in
  that spec's "Open questions" section and ask.
- When adding a spec document, link it from the list in
  [`specs/README.md`](specs/README.md).

## Rule: test behavior, not mocks

Every requirement in `specs/` should have a test that verifies the
requirement itself, not an implementation detail.

- No mocking libraries. Test against real collaborators (a real in-memory
  store, a pure function fed real input) instead of a mock told what to
  return. A passing test should mean the requirement works, not that a
  mock was configured correctly.
- If code is hard to test without mocks, it's usually doing too much.
  Extract the pure, testable logic instead of reaching for a mock.
- When you add or change a requirement in `specs/`, add or update the test
  that covers it in the same change.
- Test fixtures use synthetic data only. See
  [`specs/privacy.md`](specs/privacy.md).

## Rule: no real medical data, ever

Medical records are among the most sensitive data there is. This repo only
ever contains synthetic or fully de-identified public data. See
[`specs/privacy.md`](specs/privacy.md) for the details. This rule applies
to code, fixtures, screenshots, docs, issues and PR descriptions alike.

## Rule: Conventional Commits

Commit messages follow [Conventional Commits](https://www.conventionalcommits.org/):
`feat:`, `fix:`, `docs:`, `chore:`, `ci:`, `refactor:`, `test:`, with an
optional scope, e.g. `feat(timeline): group encounters by year`. This keeps
history readable and lets a changelog be generated from it later.

## Rule: agents don't commit; a human reviews

For now, every change is reviewed by a human, who also does all version
control and triage.

- Agents **never** commit, push, create branches or open pull requests.
  Leave all changes uncommitted in the working tree for review.
- Agents don't triage issues on their own. Triage happens only when a
  human explicitly asks for it.
- When handing over a change, summarize what changed and which specs and
  tests it touches, and suggest a Conventional Commit message the
  reviewer can use.
- If the change is user-visible, provide a screenshot of the affected view
  rendered from synthetic data, so the reviewer can attach it to the PR.
- If the change adds or changes a feature, update the user-facing docs
  (once they exist) in the same change, so they never go stale.

## Layout

- `specs/`: what ai77 does, independent of any implementation.
- Implementations: one top-level directory each, added when one exists.
