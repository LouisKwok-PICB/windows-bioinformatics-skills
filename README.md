# Windows Bioinformatics Skills

This repository contains a focused set of Codex skills for Windows-based bioinformatics, computational biology, and manuscript-oriented research workflows.

The goal is not to replace scientific judgment. The skills help an AI assistant behave like a careful research collaborator: start from explicit scientific questions, check whether available data are fit for the purpose, keep evidence chains auditable, use source-backed literature and database lookups, preflight compute-heavy jobs, write safer Windows commands, generate publication-quality figures, and package manuscript-facing outputs reproducibly.

## Who This Is For

You may find this useful if you:

- run R, Python, PowerShell, ggplot2, ComplexHeatmap, or mixed bioinformatics scripts on Windows;
- want analysis plans to begin with a concrete claim and a fit-for-purpose data audit;
- want literature review, citation management, and public database lookup to be source-backed and reusable;
- want statistical methods to be tied to design, sampling unit, assumptions, effect sizes, and reviewer risks;
- want Markdown task memory and recovery records to stay compact without losing provenance;
- need publication figures that remain readable after journal-size export;
- want source tables, scripts, figures, and manuscript text to stay synchronized;
- need compute-heavy analyses to move from local Windows to a server without weakening the scientific endpoint;
- want reusable rules for safer Windows command execution.

## Included Skills

| Skill | What it helps with |
|---|---|
| `scientific-research-evidence-planner` | Plan analyses and literature reviews around named scientific questions, data-fit audits, endpoint-native designs, evidence chains, external-paper summaries, reusable Markdown plans, recovery records, figure-promotion gates, reviewer risks, and conservative conclusions. |
| `scientific-literature-review` | Plan and document focused, scoping, or systematic-style literature reviews with search strings, database choices, screening criteria, evidence extraction, citation chaining, and thematic synthesis. |
| `scientific-citation-management` | Verify, clean, format, deduplicate, and audit DOI/PMID/PMCID/arXiv identifiers, BibTeX files, reference lists, unresolved manuscript citations, and unused bibliography entries. |
| `scientific-study-design-and-statistics` | Design or audit experiments and statistical analyses, including randomization, blocking, pseudoreplication, test selection, assumptions, effect sizes, multiple testing, power, and reporting. |
| `scientific-manuscript-writer` | Draft or audit Results, Methods, Discussion, figure legends, and reviewer-aware scientific prose from actual evidence. |
| `bioinformatics-enrichment-analysis-guardrails` | Design, audit, interpret, and report defensible ORA, GSEA, GSVA, GO, KEGG, Reactome, MSigDB, and module-enrichment workflows with explicit background universes and panel-coverage limits. |
| `scientific-compute-resource-planner` | Preflight CPU, memory, disk, packages, workers, chunking, progress logging, and server-run strategy for compute-heavy scientific analyses. |
| `scientific-database-literature-lookup` | Plan source-backed paper, gene, protein, pathway, dataset, accession, and public database lookups with retrieval contracts, API examples, count checks, and reproducible provenance. |
| `publication-plot-styler` | Convert supported evidence-chain results into reader-facing single-panel plots, improving terminology, display grammar, legends, color scales, whitespace, heatmaps, dotplots, UMAPs, and journal-style exports. |
| `paper-figure-assembler` | Assemble multi-panel figures from live R objects with panel order, area, and whitespace driven by evidence hierarchy, information density, natural aspect ratio, and journal readability. |
| `publication-content-packager` | Organize manuscript-facing outputs, including figures, source tables, supplementary tables, scripts, upload copies, and closeout QC records. |
| `windows-code-execution` | Use safer PowerShell, Rscript, and Python patterns for paths, quoting, UTF-8, `$` expansion, file operations on Windows, and portable server-run scripts. |
| `markdown-context-curator` | Keep Markdown/YAML task memory, recovery notes, package records, archives, and skill docs concise while preserving information through indexes and archives. |
| `pdf` | Read, create, and visually check PDFs when layout, pagination, or rendered appearance matters. |

## Typical Workflow

These skills are meant to work together:

```text
scientific-research-evidence-planner
-> scientific-literature-review
-> scientific-database-literature-lookup
-> scientific-citation-management
-> bioinformatics-enrichment-analysis-guardrails
-> scientific-study-design-and-statistics
-> publication-plot-styler
-> paper-figure-assembler
-> publication-content-packager
-> scientific-manuscript-writer
```

In practice, the assistant should first state the biological or methodological question, define required data, judge data fit, choose endpoint-native analyses, record evidence roles, update or create recovery records, check relevant literature and databases with reproducible provenance, run the analysis with appropriate compute planning, style only supported plots, assemble only evidence-gated figures, package source files, and finally write manuscript text that matches the evidence.

## Server-Run Scripts

Some bioinformatics analyses are too large for a local Windows machine. In that case, these skills instruct the assistant to treat the problem as an execution-environment limit, not as a reason to weaken the analysis.

Expected output is a portable R or Python script with input paths, output paths, thread counts, seeds, package checks, logging, and major parameters placed at the top so the user can edit and run it directly on a server.

## What This Repository Does Not Do

This repository does not provide private project data, unpublished method details, journal acceptance guarantees, or automatic biological validation. The skills help structure the work, but the user still needs to verify data provenance, statistical design, software versions, ethics requirements, journal instructions, and final scientific claims.

## Repository Layout

```text
windows-bioinformatics-skills/
  README.md
  INSTALL.md
  SKILL_INDEX.md
  SECURITY_AND_SCOPE.md
  LICENSE
  .gitignore
  skills/
    scientific-research-evidence-planner/
    scientific-literature-review/
    scientific-citation-management/
    scientific-study-design-and-statistics/
    scientific-manuscript-writer/
    bioinformatics-enrichment-analysis-guardrails/
    scientific-compute-resource-planner/
    scientific-database-literature-lookup/
    publication-plot-styler/
    paper-figure-assembler/
    publication-content-packager/
    windows-code-execution/
    markdown-context-curator/
    pdf/
```

Each skill is a complete directory. When installing or copying a skill, copy the whole folder, not only `SKILL.md`, because some skills include `references/`, `agents/`, or `assets/`.

## Installation

See [INSTALL.md](INSTALL.md).

## Scope And Safety

See [SECURITY_AND_SCOPE.md](SECURITY_AND_SCOPE.md) for what should and should not be included in this public bundle.

## License

See [LICENSE](LICENSE).
