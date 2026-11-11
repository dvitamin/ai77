# Data model

The normalized form of a patient's records, independent of where they
came from. Importers (such as [Import from 1177](import-1177.md)) produce
it; every view and later feature reads only this, never source markup.
This keeps the brittle part (reading a particular source) separate from
everything else.

This document describes concepts and their meaning, not a file or
storage format.

## Requirements

### Records

- A set of records belongs to exactly one patient. See
  [Overview](overview.md).
- A set of records **must** be made up of entries.

### Entries

Every entry **must** have:

- a **kind**: one of note, diagnosis, lab result, medication,
  vaccination, care contact, referral, or other. "Other" is for items
  the importer recognized as an entry but couldn't classify, so nothing
  is lost.
- the **original text** exactly as it appeared in the source, so the
  user can always see what the record actually says.
- a **source reference**: which file it came from and where in it.

Every entry **should** have, when the source provides it:

- a **date**, with its precision (exact time, day, month or year). A date
  known only to the month **must not** be shown as a specific day.
- the **care unit** responsible (e.g. a clinic or health centre).
- the **author's role** (e.g. doctor, nurse), as stated in the source.
- **codes**, each with its code system (e.g. ICD-10-SE, KVÅ), the code,
  and the text shown next to it in the source.

### Lab results

A lab result entry **should** also have, as stated in the source:

- the **analyte** (what was measured)
- the **value**, and its **unit**
- the **reference range**
- whether the source **flags** it as outside the range

Values and units **must not** be converted. If the source says
"g/L", the entry says "g/L". If the value can't be read as a number
(e.g. "positive", "<5"), the original text is kept as the value.

### Faithfulness

- Fields the source does not provide **must** be left empty, never
  guessed.
- Interpretation (plain-language explanations, body location, side of
  the body) is not part of an entry as imported. When it's added later,
  it **must** be kept separate from what the source said, so the two
  can never be confused.

## Examples

All examples use synthetic data.

- A lab result reading "Hb 128 g/L (ref 117–153)" from 2024-03-05 becomes
  a lab result entry with analyte "Hb", value 128, unit "g/L", reference
  range 117–153, not flagged, date 2024-03-05 with day precision.
- A diagnosis "J45.9 Astma, ospecificerad" becomes a diagnosis entry with
  one code: system ICD-10-SE, code "J45.9", text "Astma, ospecificerad".
- A note dated only "mars 2019" has a date with month precision.

## Out of scope

- How records are saved to and loaded from the user's own file. To be
  specified separately.
- Enrichment (plain language, anatomy, laterality). To be specified
  separately.

## Open questions

- Is the list of entry kinds right? It should follow what 1177 actually
  contains once the pages have been investigated.
- Should entries that belong together (e.g. a note and the diagnoses set
  at the same care contact) be linked, or just share a date and care
  unit?
- Time zone: are all 1177 times Swedish local time, and should that be
  stated explicitly in the model?
