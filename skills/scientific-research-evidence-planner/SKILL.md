---
name: scientific-research-evidence-planner
description: Plan, document, and iteratively execute scientific data-analysis projects around explicit hypotheses, evidence chains, file inventories, experiment attempts, result interpretation, and conservative conclusion boundaries. Use when Codex needs to organize a research project, turn scattered analyses into an ordered reproducible workflow, assess whether results support a target conclusion, or maintain Markdown records of data, scripts, progress, evidence, results, and discussion.
---

# Scientific Research Evidence Planner

## Core Rule

Treat every analysis as a test of a named scientific claim, not as a plot-production task. Before changing scripts or figures, identify:

- the target conclusion;
- the research-purpose alignment: why this analysis is the right experiment for the biological or methodological problem, rather than only a convenient computable statistic;
- the minimum evidence needed to support it;
- the data that can and cannot answer it;
- whether the available data are fit for the experimental or validation purpose;
- the exact experiment being run now;
- how the result will be judged.

Use conservative language when evidence is incomplete. Separate observations, statistical support, biological interpretation, and manuscript-ready claims.

## Purpose-Alignment Gate

Before creating or running an analysis, write or update a compact design-to-interpretation record that answers:

- experimental design: what biological or methodological problem the analysis tests;
- data fit: what observable in the data can answer that problem and what cannot;
- readout logic: why the selected statistic, plot, model, comparator, null, or threshold reflects the research purpose;
- result judgment: what would count as support, partial support, failure, or a diagnostic-only result;
- interpretation boundary: what conclusion is allowed if the analysis succeeds, and what must not be claimed.

After the analysis runs, update the same record with:

- observed result and source files;
- whether the result directly supports the research purpose, only supports a weaker/subordinate purpose, contradicts the purpose, or is merely diagnostic;
- the next decision for the evidence chain.

If an analysis does not have a clear design-to-interpretation path back to the research purpose, do not promote it to a main result. Redesign it, move it to supplementary diagnostics, or drop it.

## Routing

Identify the active task axis before deep work and load only the relevant reference:

- `data audit`, `fit-for-purpose data check`, `documentation`, `file inventory`, `terminology`, or `progress log`: read `references/project-documentation.md`.
- `analysis design`, `experiment planning`, `script ordering`, `result judgment`, or `evidence chain`: read `references/evidence-chain-workflow.md`.
- `reviewer-risk audit`, `claim stress test`, `comparator fairness`, or `pre-submission critique`: read `references/reviewer-risk-routing.md`.
- `manuscript writing`: use `scientific-manuscript-writer`; use this skill only to keep the evidence chain and project records synchronized.
- `figure construction`: use `publication-plot-styler` for single panels and `paper-figure-assembler` for multi-panel assembly; use this skill only to define the panel's inferential role and decision rule.
- `publication packaging`: use `publication-content-packager`; use this skill only to connect the package back to the evidence chain.

When a domain-specific guardrail exists, use it for allowable claims and terminology. This skill controls project-level reasoning and evidence management.

## Defaults

- Maintain a terminology ledger for each project. Record canonical names for methods, datasets, assays, modules, metrics, null models, abbreviations, and comparator labels.
- Respect the project's primary analysis language. If a project is R-based, write analysis, scoring, statistics, and plotting scripts in R by default.
- Use mature domain packages when available. Do not hand-roll specialized statistics, file parsing, image processing, or figure assembly when a maintained library provides the needed behavior.
- For manuscript-facing scientific figures, export finalized and candidate panels as `PDF`, `PNG`, and `TIFF` by default unless the project specifies otherwise.
- Keep source tables for every plotted panel and record package installs, version-sensitive choices, and fallback implementations in project records.

## Minimal Workflow

1. State the claim being tested and what would count as success, partial success, or failure.
2. Audit whether the data are fit for the experimental purpose; identify what they can and cannot answer before designing analyses.
3. Pass the purpose-alignment gate: connect experimental design, data observables, readout logic, result judgment, and interpretation boundary to the research purpose.
4. Define the analysis, comparator, null, threshold, or robustness check needed for the claim.
5. Check whether the current machine can reasonably run the analysis. If hardware or local environment is the blocker, generate a portable server-run script with editable input/output paths rather than weakening the scientific endpoint.
6. Run experiments iteratively and record parameters, outputs, result interpretation, and next decision.
7. Judge the result before making final figures.
8. Promote only supported claims to manuscript-facing status, with limitations stated explicitly.

Do not turn a context-specific result into a universal method ranking. State the endpoint under which a method helps and acknowledge comparator signal that is actually detected.
