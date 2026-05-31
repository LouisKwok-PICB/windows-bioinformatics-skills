# Project Documentation Records

Use this reference when a scientific data-analysis project needs durable Markdown records, file inventories, progress logs, or terminology ledgers.

## Core Records

Create or update a small set of Markdown files in the project docs folder. Prefer these names unless the repository already has equivalent active files:

- `PROJECT_PURPOSE.md`: scientific question, target conclusion, scope, non-goals, and claim boundaries.
- `DATA_STRUCTURE.md`: data inventory, origin, format, key fields, coverage, quality caveats, and whether each file is active, supporting, historical, or unusable.
- `SCRIPT_REGISTRY.md`: ordered scripts, purpose, inputs, outputs, status, expected runtime, and whether each script is active or exploratory.
- `EVIDENCE_CHAIN.md`: claim-to-evidence table with required analyses, current status, strength, caveats, and next action.
- `PROJECT_PLAN.md` or figure-specific plan: staged workflow from data audit to manuscript outputs.
- `PROGRESS_LOG.md`: dated log of analyses, parameters, outputs, decisions, failures, retries, and user-provided file changes.
- `RESULTS_AND_DISCUSSION.md`: current results, interpretation, limitations, and manuscript-facing wording candidates.
- `TERMINOLOGY_LEDGER.md`: canonical names, abbreviations, aliases seen in files, and terms that must not be used as biological ground truth.

Keep historical exploratory files if useful, but mark them as prior context rather than active workflow.

## Terminology Ledger

Maintain one canonical name for each recurring object:

- methods, algorithms, models, packages, and workflows;
- datasets, assays, cohorts, samples, annotations, and external references;
- modules, labels, metrics, thresholds, null models, and comparator names;
- abbreviations and first-use expansions;
- mathematical notation and symbols.

Use the ledger across scripts, figure legends, manuscript text, and documentation. If a user renames a term, update every occurrence and record the change.

## Data Inventory Fields

For important input and output files, record:

- path and short description;
- source, accession, DOI, version, or date accessed when known;
- format and approximate size;
- key entities, dimensions, and fields;
- relationship to the target analysis;
- whether it contains raw measurements, processed objects, metadata, annotations, coordinates, images, or statistical outputs;
- caveats such as missing fields, unmatched identifiers, preprocessing, coverage limits, or sample ambiguity.

Do not assume a processed object contains raw data. Check the object structure or associated flat files.

## Project-State Hygiene

- Keep active, supporting, exploratory, and archived files visually distinct in docs.
- Do not silently overwrite an existing script's purpose; rename it or update `SCRIPT_REGISTRY.md`.
- Update project records after changing file layout, script order, figure numbering, manuscript claims, or current conclusions.
- If README files conflict with more recent memory, registry, or current-task records, prefer the explicitly current records and mark stale files.
