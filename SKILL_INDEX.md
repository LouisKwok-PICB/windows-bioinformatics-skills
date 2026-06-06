# Skill Index

## Research Planning

### `scientific-research-evidence-planner`

Use when a project needs a documented evidence chain, external-paper or literature-summary record before figure critique, file inventory, reusable Markdown plan record, active-step recovery record, experiment plan, result interpretation, reviewer-risk audit, or conservative conclusion boundary.

Use with:

- `scientific-manuscript-writer` for manuscript text.
- `markdown-context-curator` when active plans, recovery notes, or package records become buried under completed history.
- `publication-plot-styler` and `paper-figure-assembler` once a result has passed the relevant evidence and panel-promotion gates.
- `publication-content-packager` when outputs are mature enough to organize for submission.

## Manuscript Writing

### `scientific-manuscript-writer`

Use when drafting, restructuring, or auditing Results, Methods, Discussion, figure legends, abstracts, reviewer-risk-aware wording, or full manuscript outlines.

It controls manuscript structure and prose flow. If a separate domain-specific guardrail exists in your own environment, use that guardrail for domain claims and terminology.

## Figures

### `publication-plot-styler`

Use for standalone or source-panel plots: ggplot-style plots, ComplexHeatmap-style heatmaps, UMAPs, dotplots, barplots, alluvial plots, labels, legends, dimensions, and export settings.

### `paper-figure-assembler`

Use when combining live R objects into a publication-ready multi-panel figure. It focuses on object-based assembly, panel geometry, canvas size, export, and avoiding raster distortion.

Common sequence:

```text
scientific-research-evidence-planner
-> publication-plot-styler
-> paper-figure-assembler
-> publication-content-packager
```

## Publication Package

### `publication-content-packager`

Use after analyses and figures are mature enough to organize into a manuscript-facing package. It creates or audits package structure, source tables, supplementary tables, scripts, submission-ready copies, content maps, and closeout QC.

## Execution And Files

### `markdown-context-curator`

Use when Markdown, YAML recovery records, task logs, package docs, or skill files have accumulated enough completed history to hide the active task. It preserves information by moving it to archives, references, or indexes while keeping current recovery files concise.

### `windows-code-execution`

Use before running non-trivial PowerShell, Rscript, or Python commands on Windows. It focuses on quoting, paths, here-string encoding, `$` expansion, and safe file operations.

### `pdf`

Use when reading, creating, or reviewing PDFs where rendering and layout matter.

## Boundary Rules

- Do not use writing skills to invent missing data, statistics, citations, or conclusions.
- Do not use figure skills to decide whether a scientific claim is supported.
- Do not create duplicate plan files when an existing related Markdown plan can be updated with a dated new objective section.
- Do not execute a multi-step plan without recording the current active step, step outcome, and next checkpoint in recovery records.
- Do not use context curation to silently delete unique evidence, manuscript text, parameters, provenance, or reproducibility details; archive and index them instead.
- Do not treat a recovery note, script plan, or draft figure list as permission for final figure assembly; verify panel-level evidence gates first.
- Do not use packaging skills to promote exploratory outputs to manuscript-facing status.
- Always verify target-journal requirements before final submission.
