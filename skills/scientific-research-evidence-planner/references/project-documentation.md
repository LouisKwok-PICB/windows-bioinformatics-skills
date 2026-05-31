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

## Fit-For-Purpose Data Audit

Before designing analyses or figures, explicitly judge whether the available data can answer the intended experimental or validation purpose. This is a gate, not a formatting step.

For each target conclusion or experiment, record:

- intended purpose: discovery, validation, benchmarking, robustness, replication, mechanism support, visualization, or manuscript source-data generation;
- required observables: measurements, labels, metadata, time points, spatial coordinates, perturbations, controls, replicates, or outcome variables needed to test the claim;
- available observables: which required fields exist in the current data and which are absent, derived, low coverage, or uncertain;
- resolution match: whether the data are at the needed level, such as cell, sample, subject, tissue region, gene, pathway, image, or pseudobulk level;
- population and condition coverage: whether the relevant cell types, conditions, batches, donors, samples, or comparison groups are present and sufficiently represented;
- feature coverage: whether the genes, proteins, markers, variables, pathways, or annotations needed for the analysis are measured or recoverable;
- control and null feasibility: whether appropriate negative controls, comparator inputs, randomization units, or null-preserving structures exist;
- confounding risk: batch, abundance, sampling, dropout, spatial density, annotation uncertainty, preprocessing, or missing-data patterns that could explain the result;
- decision: `fit`, `partially fit`, `not fit`, or `fit only for exploratory use`;
- consequence: proceed, redesign endpoint, restrict claim, seek another dataset, move to exploratory status, or stop the analysis.

Do not promote an analysis to manuscript-facing status until the data-purpose fit is documented. If the data are only partially fit, state exactly which claim is still allowed and which claim is not supported.

## Project-State Hygiene

- Keep active, supporting, exploratory, and archived files visually distinct in docs.
- Do not silently overwrite an existing script's purpose; rename it or update `SCRIPT_REGISTRY.md`.
- Update project records after changing file layout, script order, figure numbering, manuscript claims, or current conclusions.
- If README files conflict with more recent memory, registry, or current-task records, prefer the explicitly current records and mark stale files.
