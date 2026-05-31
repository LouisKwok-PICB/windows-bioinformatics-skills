# Figure Publication Package Template

Use this template when a user asks to organize one figure or one figure family for manuscript submission.

## Minimal Directory Tree

```text
publication/<figure-id>/
  README.md
  <FIGURE>_PUBLICATION_CONTENT_MAP.md
  <FIGURE>_CLOSEOUT_QC_REPORT.md
  manuscript/
    <Figure>_<Journal>_manuscript_text.md
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
    README.md
    figures/
    tables/
```

## README.md

Include:

- Current central claim.
- What the package contains.
- Main entry points.
- Current status: draft, candidate, publication-facing, submission-ready, or closed.
- Recommended main panels.
- Supplementary evidence roles.
- Reproduction instructions.
- Naming and terminology rules.
- Explicit claims that the package does not support.

## Publication Content Map

Use these sections:

1. Central claim.
2. Main figure table with columns: panel, manuscript role, evidence shown, interpretation, status.
3. Supplementary figure table with columns: supplement, role, why it stays supplementary.
4. Source table inventory with a short role for each table.
5. Methods reproducibility coverage.
6. Required wording boundaries.
7. Comparator or alternative-method summary when relevant.

## Manuscript Text

Create a figure-specific manuscript file with:

- Results subsection title.
- Results draft paragraphs in manuscript style.
- Main figure legend.
- Supplementary figure legends.
- Methods subsection.
- Source data and reproducibility note.
- Limitations and claim boundaries.

Keep figure-specific text separate from whole-paper declarations unless the user asks for full manuscript integration.

## Closeout QC Report

Use these sections:

1. Date and package status.
2. Publication files.
3. Reproducibility entry point.
4. Journal technical QC.
5. Visual QC.
6. Manuscript QC.
7. Archive and cleanup notes.
8. Residual risks.
9. Closeout status.

If final figures or submission copies do not exist, state that directly and list what remains.

## Submission-Ready Directory

Before final closeout, include `submission_ready/README.md` explaining:

- which final upload files are present;
- which files are pending;
- naming conventions for expected upload files;
- which script will create them once final assembly is approved.

After closeout, include:

- journal-renamed main figure files;
- journal-renamed supplementary figure files;
- formal supplementary tables;
- manifests recording dimensions, dpi, file size, and source file.

## Evidence Manifest Columns

For complex packages, create a CSV manifest with columns like:

```text
item_id,panel_or_table,role,source_input,output_pdf,output_png,output_tiff,allowed_claim,claim_boundary,status
```

This is especially useful when multiple supplementary figures are generated from shared source tables.

## Common Failure Modes

- Calling a figure closed before the assembled main figure exists.
- Moving exploratory outputs into the active publication package without labeling them.
- Writing stronger biological claims than the actual evidence supports.
- Treating comparator methods as failed controls when they show related signal.
- Losing traceability between panels, source tables, scripts, and manuscript text.
- Creating final upload copies from low-resolution raster previews.
- Forgetting to update project memory or documentation after changing package status.
