# Overview

## Goal

ai77 lets a person load a set of medical records and explore them
visually, seeing a patient's history (encounters, diagnoses, medications,
lab results and so on) in a form that's easier to grasp than a list of
documents.

It's a playground: a place to try out visualization ideas, not a clinical
product.

## Intended viewer

The viewer is a single patient exploring their own records, not a
clinician and not a cohort analyst. ai77 shows one patient's records at a
time; cohorts and aggregates across patients are out of scope.

Because the viewer is the patient, the records they load are their own
real records. That's allowed on their own device, under the rules in
[Privacy](privacy.md). Real records still never enter the repository.

## Local first

Everything ai77 does with a patient's records happens on the patient's
own device: reading the files, storing them, visualizing them and,
later, answering questions about them with a local language model. The
records are never sent to a server. The patient keeps their own records
file and is responsible for where it's stored. See [Privacy](privacy.md).

Public medical knowledge (what a code means, what an abbreviation stands
for, how to explain a term in plain Swedish) contains no personal data.
It can be prepared ahead of time with any tool and shipped with ai77, so
the work done on the device stays small.

## In scope

- Importing a patient's own records from pages saved from 1177 Journalen
  (Sweden's national health portal). See [Import from 1177](import-1177.md).
- A normalized form of the records that every view reads, independent of
  the source. See [Data model](data-model.md).
- More to be defined. Add each capability here as it's specified, with a
  link to its own spec document.

## Roadmap

Planned capabilities, in rough order. These are not specified yet. Each
one gets its own spec document when work on it starts, and moves to "In
scope" above.

1. Import and inspect: read saved 1177 pages and show what was
   recognized. (Specified.)
2. Timeline and lab result charts.
3. Saving and loading the patient's own records file.
4. Reference data: codes and abbreviations explained in plain Swedish,
   with the body region and side each one concerns.
5. A 3D body showing where operations and other events happened, linked
   to their entries.
6. Questions and answers in Swedish, answered by a local language model
   that cites the entries it used.
7. Plain-language summaries of free-text notes.

## Out of scope

These are permanent boundaries, not deferred work. ai77 is for viewing
records, nothing more.

- Medical advice or clinical decision making. ai77 explains and shows
  what the records say; it never recommends, diagnoses or suggests
  treatment. It's not a medical device and must never present itself as
  a basis for diagnosis or treatment.
- Integration with other systems. ai77 never writes back to, connects
  live to, or exchanges data with health record systems or any other
  service. Records come in only as files the patient provides.
- Storage anywhere but the patient's own device: no accounts, servers,
  sync or cloud storage.
- Multi-user access, and cohorts, aggregates or comparisons across
  patients.
- Real patient data in the repository: code, fixtures, docs and so on.
  See [Privacy](privacy.md).

## Design principle

Simplicity beats configurability. When a decision could be a user setting
or a fixed sane default, choose the fixed default.

## Open questions

- Does ai77 need to accept any input other than saved 1177 pages? (The
  questions about the 1177 pages themselves live in
  [Import from 1177](import-1177.md).)
- Does ai77 run in a browser or as a desktop app? Start in the browser,
  on the developer's own machine. Revisit when local language models
  come in (roadmap step 6), since good Swedish may need a larger model
  than a browser can run.
