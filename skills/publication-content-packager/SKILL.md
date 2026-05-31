---
name: publication-content-packager
description: Package manuscript-ready scientific figure publication content from analysis outputs. Use when Codex needs to organize or audit a journal figure package, mimic an existing publication figure structure, prepare Results/Methods/legends/source tables/submission-ready files, create content maps and closeout QC reports, or keep evidence-chain and claim-boundary records for a manuscript figure.
---

# Publication Content Packager

## Core Rule

Create a reproducible, manuscript-facing publication package for one scientific figure or figure family. Treat the package as a claim-to-artifact map: every panel-level statement should trace to the exact figure file, source table, script, dataset, statistic, and limitation.

Use this skill after analyses and figures are mature enough to organize into a publication-facing package. Use `scientific-research-evidence-planner` first when the evidence chain or panel promotion status is still unresolved, `publication-plot-styler` or `paper-figure-assembler` when visuals are still being built, and manuscript/domain guardrails when claims or wording need revision.

This skill packages and audits. It must not promote unsupported exploratory outputs, diagnostic-only results, or failed original claims to manuscript status.

## Reference Routing

Load only the reference needed for the current packaging task:

- Directory tree, content-map sections, manuscript-file template, closeout report sections, submission-ready directory, evidence manifest columns, and common packaging failures: `references/figure-publication-package-template.md`.
- Figure/table export rules, source-data inventory, script/environment requirements, closeout QC, and status labels: `references/package-qc-rules.md`.

## Workflow

1. Identify the target figure, central claim, active data, scripts, result tables, figure candidates, journal requirements, and any existing package to mimic.
2. Check the evidence chain before packaging. Record central claim, panel-level claims, support, limitations, and unsupported claims.
3. Create or update a figure-specific directory such as `publication/<figure-id>/`.
4. Copy or regenerate only active, traceable artifacts. Treat older drafts as historical unless explicitly revalidated.
5. Write publication-facing records. At minimum this usually includes:
   - `README.md`
   - `<FIGURE>_PUBLICATION_CONTENT_MAP.md`
   - `manuscript/<Figure>_<Journal>_manuscript_text.md` or journal-equivalent text
   - `<FIGURE>_CLOSEOUT_QC_REPORT.md`
   - `submission_ready/README.md` when final upload copies are pending
   - a source-data or data-availability map when external, generated, controlled-access, or reused data are involved.
6. Preserve reproducibility with ordered active scripts, logs, session/environment information, and source tables. Prefer a run-all script only after the workflow is stable.
7. Keep incomplete outputs explicitly pending. Do not mark assembled figures, upload TIFFs, supplementary tables, or QC as complete until the files exist and have been checked.
8. Update project documentation and recovery records when the package state changes.

## Claim And Content Rules

- Distinguish observed result, statistical support, interpretation, and limitation.
- Keep source tables separate from formal supplementary tables.
- Include enough null/comparator detail in Results, legends, or supplementary legends for reviewers to judge fragile claims.
- Do not imply a whole manuscript is submission-ready when only figure-specific content has been prepared. Mark article-level declarations as outside scope unless they were explicitly handled.
- Use the project's existing analysis language and script naming conventions.
- Include server-run scripts when final outputs depend on analyses that cannot run on the local machine; mark returned outputs pending until they exist and pass checks.

## Completion Rule

Use explicit package status: `draft`, `candidate`, `publication-facing`, `submission-ready`, or `closed`. Do not use `submission-ready` or `closed` while the assembled figure, legends, source tables, upload copies, or required QC are still pending.
