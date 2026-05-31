---
name: publication-content-packager
description: Package manuscript-ready scientific figure publication content from analysis outputs. Use when Codex needs to organize or audit a journal figure package, mimic an existing publication figure structure, prepare Results/Methods/legends/source tables/submission-ready files, create content maps and closeout QC reports, or keep evidence-chain and claim-boundary records for a manuscript figure.
---

# Publication Content Packager

## Purpose

Create a reproducible, manuscript-facing publication package for one scientific figure or figure family. The package should connect analysis outputs to figure panels, manuscript text, source tables, scripts, submission copies, and explicit claim boundaries.

For a concrete directory template, read `references/figure-publication-package-template.md`.

Treat the package as a claim-to-artifact map. A reader or reviewer should be able to trace every panel-level statement to the exact figure file, source table, script, dataset, statistic, and limitation.

Use this skill after analyses and figures are mature enough to organize into a publication-facing package. Use `scientific-research-evidence-planner` first when the evidence chain is still being designed, `publication-plot-styler` or `paper-figure-assembler` when figure visuals are still being built, and manuscript/domain guardrails when claims or wording need revision. This skill packages and audits; it should not promote unsupported exploratory outputs to manuscript status.

## Workflow

1. **Read context first.** Identify the target figure, current scientific claim, active data, current scripts, current result tables, figure candidates, journal requirements, and any existing package to mimic. Treat older drafts as historical unless they are explicitly revalidated.
2. **Define the evidence chain.** Write the central claim, panel-level claims, required evidence, current support, limitations, and unsupported claims before finalizing the manuscript wording.
3. **Create the publication package.** Use a figure-specific directory such as `publication/<figure-id>/` with subdirectories for manuscript text, main figures, standalone panels, supplementary figures, source tables, formal supplementary tables, scripts, logs, and submission-ready copies.
4. **Copy or regenerate active artifacts only.** Include only current, traceable results. Keep archived or exploratory outputs out of the active package unless clearly labeled as historical context.
5. **Write publication-facing records.** At minimum create or update:
   - `README.md`
   - `<FIGURE>_PUBLICATION_CONTENT_MAP.md`
   - `manuscript/<Figure>_<Journal>_manuscript_text.md` or journal-equivalent manuscript text
   - `<FIGURE>_CLOSEOUT_QC_REPORT.md`
   - `submission_ready/README.md` when final upload copies are not yet complete
   - a source-data or data-availability map when the figure relies on external, generated, controlled-access, or reused datasets.
6. **Preserve reproducibility.** Copy active scripts in ordered execution form. Prefer a numbered workflow and a run-all script only after the chain is stable. Do not create a misleading run-all file that claims to rebuild outputs that are still pending.
7. **Close only what is actually closed.** Mark final assembled figures, upload TIFFs, supplementary tables, and QC as `pending` until they exist and have been checked.
8. **Update project documentation.** Update the project index, current task, progress log, results/discussion record, file-change log, and memory/state file if the project has them.

## Required Package Structure

Use this structure unless the project has a stronger existing convention:

```text
publication/<figure-id>/
  README.md
  <FIGURE>_PUBLICATION_CONTENT_MAP.md
  <FIGURE>_CLOSEOUT_QC_REPORT.md
  manuscript/
  figures/
    main/
    main/standalone_panels/
    supplementary/
  tables/
    source/
    supplementary/
  scripts/
  logs/
  submission_ready/
    figures/
    tables/
```

If a component is not complete, keep the directory and add a short status file explaining what remains.

## Manuscript Content Rules

Write figure-specific manuscript content with these sections when applicable:

- Results text: what the figure demonstrates and how each panel contributes.
- Main figure legend: panel-by-panel descriptions, statistical definitions, abbreviations, and sample/data context.
- Supplementary figure legends: evidence role, inputs, and interpretation boundaries.
- Methods: inputs, preprocessing, scoring/statistics, thresholds, null models, software, parameters, and source-output locations.
- Reviewer-facing limitations: what the figure cannot prove.
- Data and code availability notes: where plotted source data, raw or processed inputs, scripts, and reusable code are expected to live.

Use conservative language. A publication package should distinguish:

- observed result versus interpretation;
- primary evidence versus supporting enrichment or marker evidence;
- comparator result versus universal method ranking;
- operational labels, thresholds, or proxies versus ground-truth biology;
- same-sample, same-platform, and cross-platform analyses.

When a statistical null or comparator is central to a figure, include enough detail in either the Results, figure legend, or supplementary legend for a reviewer to see why the comparison is valid. Do not rely on Methods alone for fragile points such as spatially constrained permutations, batch-preserving label shuffles, matched feature universes, or high-overlap comparator interpretation.

If the user asks for only figure-specific content, do not claim that the entire manuscript is submission-ready. Instead, mark article-level sections such as Ethics, Funding, Competing interests, Author contributions, References, and full Data Availability as outside the figure package unless they were explicitly prepared.

## Figure And Table Rules

- Export manuscript-facing plots as `PDF`, `PNG`, and `TIFF` by default unless the user or journal specifies otherwise.
- For PLOS-style packages, prepare flattened RGB or grayscale TIFFs at 300-600 dpi, keep figures within the journal box, and record file size/dimension checks. For other journals, verify the target journal's current figure specifications before final upload copies.
- Verify upload TIFFs are single-frame, RGB or grayscale, have no alpha channel, use lossless compression when available, and meet journal DPI/size limits. Record these checks in a manifest.
- Assemble final multi-panel figures from source plot objects or source tables when possible. Do not assemble a final manuscript figure from low-resolution screenshots or already-compressed raster previews.
- Keep standalone panels alongside the assembled figure so visual problems can be diagnosed panel by panel.
- Keep source tables separate from formal supplementary tables. Source tables support traceability; formal supplementary tables are manuscript-numbered upload files.
- Add a manifest when there are many figures or tables. Include output path, evidence role, source input, allowed claim, and claim boundary.
- Keep formal supplementary figure numbering consistent across manuscript citations, legends, upload filenames, manifests, content maps, and closeout reports. If a conceptual figure is split for upload, use explicit labels such as `S4C1` and `S4C2` everywhere rather than mixing them with `S4C`.
- Ensure figure captions and article titles are not embedded inside figure image files unless the journal explicitly asks for that layout.

## Data Availability And Source Data

For every publication package, inventory the data behind the figure:

- newly generated raw data;
- processed matrices or objects;
- figure source tables;
- statistical output tables;
- images or segmentation masks;
- reused public datasets and accessions;
- restricted or third-party data;
- scripts and software needed to regenerate the outputs.

Classify each item as `public repository`, `controlled access`, `within paper/supplement`, `reused public source`, `third-party restricted`, `available on justified request`, or `not applicable`. Do not invent repository identifiers, DOIs, licenses, embargo dates, or access committees. Flag weak `available upon request` wording unless a specific legal, ethical, commercial, or third-party restriction exists.

Keep source tables separate from formal supplementary tables. Source tables should be complete enough to audit plotted values, while formal supplementary tables should match manuscript numbering and upload requirements.

## Script And Environment Rules

- Follow the analysis language already used by the project. If the workflow is R-first, keep new analysis and figure scripts in R unless a specific file format or library makes another language necessary.
- Use established packages for specialized tasks when available. Install missing routine packages when the environment allows it, and record package use in Methods, session info, or logs.
- Keep scripts ordered and named by workflow stage. Avoid unnumbered one-off scripts in the active publication path.
- Include session information or environment metadata for computational reproducibility.
- If any manuscript-facing output depends on a script that could not run on the local Windows machine because of hardware or environment limits, include the server-run script in the package. The script should have user-editable input/output paths and major parameters at the top, create output directories, validate required inputs, write logs/session info, and be runnable with a single command on the target server.
- Mark server-run outputs as pending until the returned files exist, match the expected paths, and pass source-table or figure regeneration checks. Do not package locally downsampled substitutes as final results unless they are explicitly part of the manuscript design.

## Closeout QC

Before calling a package complete, check:

- All main and supplementary figure files exist in the expected formats.
- Upload copies exist in `submission_ready/` with journal-compliant names.
- Source tables and supplementary tables are traceable to scripts and figures.
- Manuscript text, legends, and Methods match the final panels and table numbering.
- Claims in README, content map, Results, legends, and closeout report are consistent.
- Unsupported or failed exploratory claims are documented as limitations or diagnostics, not promoted as results.
- The closeout report states residual risks and whether the figure is truly closed.

Also check:

- the latest generated images, upload copies, and manifests have matching timestamps or documented reasons for differences;
- file-level QC includes dimensions, DPI, file size, color mode, compression, alpha-channel status when relevant, and journal box limits;
- all supporting figures named in text have corresponding upload files and source tables;
- any figure-specific manuscript package is labeled as such, without implying full-paper completion when article-level declarations remain pending.
- every plotted claim has a source-data path and every reused dataset has an accession, DOI, citation, or explicit unresolved field.

## Status Language

Use explicit status labels:

- `draft`: content exists but is not yet reviewed.
- `candidate`: evidence is generated, but panel selection or visual QC remains.
- `publication-facing`: content is organized for manuscript review, but final upload files may still be pending.
- `submission-ready`: final files exist, journal QC has passed, and upload copies are in place.
- `closed`: no required figure-specific work remains except broader manuscript integration or explicit new analysis.

Do not use `submission-ready` or `closed` for a figure whose assembled main figure, legends, source tables, or upload copies are still pending.
