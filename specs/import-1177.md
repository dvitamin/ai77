# Import from 1177

How ai77 reads a patient's own records from pages saved from 1177
Journalen (Sweden's national health portal) and turns them into the
normalized records described in [Data model](data-model.md).

1177 offers no official export format. The input is HTML pages the
patient has saved from their own logged-in session. The page structure is
not a published contract and can change without notice, so the importer
is the one deliberately brittle part of ai77. Everything after import
depends only on the normalized data model, never on 1177 markup.

## Requirements

### Getting files in

- The user **must** be able to add saved 1177 pages by dragging and
  dropping them onto the app and by choosing them with a file picker.
- The user **must** be able to add several files in one go, and to add
  more files later to an existing set of records.
- ai77 **must not** log in to 1177 or fetch anything from it. The patient
  saves the pages; ai77 only reads files it is given.

### Handling the HTML safely

- Saved pages **must** be treated as untrusted input. They are parsed for
  their content and **must never** be displayed as-is: no scripts run, no
  styles apply and no external resources (images, fonts, trackers) load.
- Parsing **must** happen entirely on the user's device. See
  [Privacy](privacy.md).

### Output

- Each recognized item on a page **must** become one entry in the data
  model, keeping its original text exactly as it appeared and a
  reference back to the file it came from.
- The importer **must not** invent data. Codes, dates, values and units
  are taken as they appear in the source or left empty. Interpreting or
  enriching them is a separate, later step.
- Importing the same item twice (e.g. the same page saved twice, or two
  overlapping saves) **must not** create duplicate entries.

### Failing loudly

- After each import the user **must** see an import report listing:
  - how many entries of each kind were recognized
  - every part of a page that was not recognized, or was recognized but
    could not be read, with the reason
  - files that were not recognized as 1177 pages at all
- Nothing may be dropped silently. If the importer skips something, it
  appears in the report.
- A file that isn't recognized **must not** stop the other files in the
  same import from being read.
- The import report is shown only to the user on their device. It
  **must not** be written to logs, which follow the rules in
  [Privacy](privacy.md).

### Change over time

- Each import **should** record which version of the importer read it, so
  that records read by an older importer can be told apart after 1177
  changes its pages.

## Known source structure

How 1177 pages are laid out, in prose: sections, headings, how one item
is delimited, where dates, care units, codes and values appear. This is
the parsing knowledge, written down independently of any implementation.
Fill it in as the pages are investigated; each claim here should have a
synthetic fixture that shows it.

- To be filled in.

## Examples

All examples use synthetic data.

- A synthetic page with three lab results and one note gives four
  entries: three lab results and one note. The report says "3 lab
  results, 1 note, nothing skipped".
- The same page dropped twice gives the same four entries, not eight.
- A synthetic page containing an item of an unknown kind gives the known
  entries, and the report lists the unknown item as not recognized.
- A plain HTML file that isn't a 1177 page is reported as "not a
  recognized 1177 page", and the other files in the same drop are still
  imported.

## Out of scope

- Logging in to 1177, or a browser extension or other tool that saves the
  pages for the user. These may be specified later.
- PDFs, printouts and other export formats.
- Interpreting what the records mean (plain-language explanations, body
  locations). That's a later enrichment step with its own spec.

## Open questions

- Which Journalen sections exist and which come first? (Likely
  candidates: notes, diagnoses, lab results, medications, vaccinations,
  care contacts, referrals.)
- How do the pages arrive: one page per section, one per entry, or one
  long page? Are they saved as plain HTML or as "complete page" with a
  folder of assets? Should ai77 accept a whole folder?
- Do operations and diagnoses carry codes (KVÅ, ICD-10-SE) in the page,
  or only text?
- How are two saves of the same item recognized as the same item? Is
  there a stable identifier on the page, or must it be inferred from
  date, care unit and content?
- How should the personnummer on the pages be handled: kept, masked in
  the view, or dropped at import?
