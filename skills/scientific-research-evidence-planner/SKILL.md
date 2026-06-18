---
name: scientific-research-evidence-planner
description: Plan, document, and iteratively execute scientific data-analysis projects around explicit hypotheses, evidence chains, fit-for-purpose data audits, scientific exploration plans, experiment attempts, external-paper or literature figure reviews, result interpretation, and conservative conclusion boundaries. Use when Codex needs to organize a research project, design or audit a scientific exploration plan, turn scattered analyses or papers into an ordered reproducible workflow, assess whether results support a target conclusion, or maintain Markdown records of data, papers, scripts, progress, evidence, results, and discussion.
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

## Scientific Exploration Planning Gate

Before planning or running exploratory scientific analyses, explicitly pass the planning chain:

> biological or methodological question -> required data -> data-fit judgment -> endpoint-native analysis -> evidence-chain role -> result judgment rule -> display or reporting route -> allowed claim -> forbidden claim.

If this chain is missing, do not run analysis, draw figures, or create a new plan file. First repair the plan. Use `references/scientific-exploration-planning-rules.md` whenever the task involves exploratory validation, multimodal data use, algorithm-rationale testing, evidence-chain restructuring, deciding what can become a main/supplement figure, or the user challenges whether the plan is scientifically meaningful.

## Recovery And Handoff Rule

When you create or substantially revise a scientific project plan, create or update two recovery records at the project root unless the repository already defines equivalent active files:

- `AGENT_MEMORY.yaml`: compact machine-readable memory for another agent to resume the project.
- `docs/CURRENT_TASK.md`: human-readable active task record with the current goal, plan, progress, outputs, decisions, blockers, and next steps.

Initialize these files during planning, not only at the end. After each completed task or meaningful workflow checkpoint, update both files before the final response. If the user already has active versions, preserve their structure and append/update the current state rather than overwriting older project memory. If a project is read-only, report that the recovery records could not be written and include the same handoff content in the final response.

When the user asks to make a plan, first search the repository for existing related Markdown plan records before creating a new file. Prioritize active project docs, `docs/`, publication/package docs, and files with names such as `*PLAN*.md`, `*CURRENT*.md`, `*AUDIT*.md`, `*WORKFLOW*.md`, or task-specific keywords. If a similar plan file exists, preserve its history and add or update a dated section for the new plan objective, decision rules, execution steps, outputs, and next checkpoint. Do not create a duplicate standalone plan file merely because the new request is phrased differently. Create a new descriptive `docs/<TASK>_PLAN.md` only when no similar plan record exists or when the existing file is clearly obsolete/inapplicable; then link the new plan from `AGENT_MEMORY.yaml` and `docs/CURRENT_TASK.md`.

When executing a multi-step plan, extract the specific current step before starting work and record it in the recovery records with the plan file, step identifier, objective, start timestamp, expected output, and next checkpoint. At the end of that step, or before changing to another step, update the same records with the outcome, files changed or inspected, whether the step achieved its purpose, and the next active step. If exploration shows the plan cannot answer the user's stated objective, update the plan file with a dated adjustment section before continuing, and record that adjustment in `AGENT_MEMORY.yaml` and `docs/CURRENT_TASK.md`. Do not leave multi-step progress implicit in chat history only.

## Recovery Update Trigger Rule

Update `AGENT_MEMORY.yaml` and `docs/CURRENT_TASK.md` when the next agent's first action would otherwise be ambiguous. Required triggers:

- starting or resuming a multi-step scientific task after context recovery;
- switching phases, such as planning -> execution, external-paper review -> synthesis, analysis -> figure design, candidate figure -> manuscript/package sync, or audit -> implementation;
- completing a meaningful checkpoint, such as validated inputs, downloaded/cached papers, one paper or figure review, an analysis run, figure generation/QC, manuscript audit, package update, or final plan;
- receiving a user decision that changes scope, claim boundary, figure route, promotion status, or next action;
- discovering a blocker, failed endpoint, diagnostic-only result, missing asset, changed provenance, or unsupported claim;
- before the final response for any non-trivial task that inspected or changed scientific evidence, plans, scripts, figures, manuscripts, packages, or source records.

Do not update recovery records for trivial reads or exploratory commands that do not change the active objective, evidence state, next action, or guardrails. Each update should be compact and include: status, active step, source-of-truth paths, key files inspected or changed, current conclusion, next checkpoint, and "do not" guardrails. If these records begin to accumulate long history or repeated completed logs, invoke `markdown-context-curator` and split details into indexed plan, review, package, or archive files.

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

## Critical Claim Audit Gate

Before promoting any result to a main figure, manuscript claim, or reviewer-facing conclusion, classify the claim and stress-test it:

- claim type: descriptive, associational, comparative, mechanistic, causal, predictive, or methodological;
- evidence type: direct observable, proxy readout, annotation overlay, enrichment support, statistical pattern, simulation, or external validation;
- validity risks: construct validity, internal validity, external validity, statistical conclusion validity, and data-fit limitations;
- alternative explanations: batch, coverage, annotation, sample composition, local density, feature-panel restriction, threshold choice, or comparator mismatch;
- proportional wording: what verbs are allowed and what stronger wording would overclaim.

If the result only supports a proxy or indirect readout, state the proxy explicitly and keep anatomy, mechanism, causality, universality, and superiority claims out of the main conclusion unless independently supported. Use `references/critical-claim-audit.md` when a skeptical-review or claim-boundary record is needed.

## Figure Assembly Gate

Before creating a final figure assembly script, publication package, manuscript-facing figure panel, or upload-ready figure file, do not treat a recovery file's `next_action` or an existing script plan as sufficient authorization. First verify that a current panel-level gate record exists, or create one.

For every proposed final or manuscript-facing panel, the gate record must state:

- method-native premise;
- biological or validation question;
- independent observable;
- matched readout;
- result judgment;
- allowed claim;
- forbidden claim;
- promotion status.

If any proposed panel is `diagnostic_only`, `exploratory_only`, `failed_original_claim`, `needs_redesign`, or otherwise not clearly supported, do not proceed to final assembly until the user accepts demotion, redesign, or explicit limitation wording. Update `AGENT_MEMORY.yaml` and `docs/CURRENT_TASK.md` so future agents do not skip this gate.

## External Literature Review Gate

When external papers, PDFs, article pages, preprints, or figure benchmarks are used as evidence or design references, do not jump directly to figure-layout critique. First create or update a compact paper-summary record that future agents can read quickly.

For each paper, record:

- citation, DOI or official URL, local PDF/cache path, and source status;
- scientific question, method premise, datasets, assay/platform, species or tissue context;
- main claim, validation endpoints, comparators, and key result boundary;
- limitations or reviewer-risk notes relevant to the current project;
- which figures are likely relevant and why.

After the paper summary exists, analyze figures one at a time. For each selected figure, append a separate figure-learning record with source checked, figure title/caption role, panel map, tissue or biological context, quantitative support, legend/color design, layout structure, evidence chain, transferable lessons, what not to copy, and status. If interrupted, resume from the first paper or figure whose summary/figure record is missing.

Use validated local PDFs and cached figure assets as the default source record after provenance is established. Do not repeatedly re-download or re-query the same paper unless the cache is missing, unreadable, outdated for the task, or the user asks for source re-verification.

## Routing

Identify the active task axis before deep work and load only the relevant reference:

- `data audit`, `fit-for-purpose data check`, `documentation`, `file inventory`, `terminology`, or `progress log`: read `references/project-documentation.md`.
- `scientific exploration planning`, `analysis design`, `experiment planning`, `script ordering`, `result judgment`, `evidence chain`, `multimodal validation planning`, `algorithm-rationale validation`, or `figure-evidence planning`: read `references/scientific-exploration-planning-rules.md` first, then `references/evidence-chain-workflow.md` if implementation ordering is needed.
- `claim classification`, `proxy vs direct evidence`, `alternative explanations`, `bias/confounding`, or `overclaim audit`: read `references/critical-claim-audit.md`.
- `external paper review`, `literature summary`, `PDF-backed figure benchmark`, or `published figure evidence-chain learning`: apply the External Literature Review Gate; use `pdf` when rendering or visually checking PDFs.
- `reviewer-risk audit`, `claim stress test`, `comparator fairness`, or `pre-submission critique`: read `references/reviewer-risk-routing.md`.
- `manuscript writing`: use `scientific-manuscript-writer`; use this skill only to keep the evidence chain and project records synchronized.
- `figure construction`: use `publication-plot-styler` for single panels and `paper-figure-assembler` for multi-panel assembly; use this skill only to define the panel's inferential role and decision rule.
- `publication packaging`: use `publication-content-packager`; use this skill only to connect the package back to the evidence chain.

When a domain-specific guardrail exists, use it for allowable claims and terminology. This skill controls project-level reasoning and evidence management.

## Defaults

- Maintain a terminology ledger for each project. Record canonical names for methods, datasets, assays, modules, metrics, null models, abbreviations, and comparator labels.
- Respect the project's primary analysis language. If a project is R-based, write analysis, scoring, statistics, and plotting scripts in R by default.
- Use mature domain packages when available. Do not hand-roll specialized statistics, file parsing, image processing, or figure assembly when a maintained library provides the needed behavior.
- Before long, memory-heavy, or permutation-heavy analyses, perform a resource preflight and record CPU, memory, disk, package availability, planned workers, chunking, seeds, progress logging, and restart strategy. If the local machine is inadequate, produce a portable server-run script rather than weakening the scientific endpoint.
- For manuscript-facing scientific figures, export finalized and candidate panels as `PDF`, `PNG`, and `TIFF` by default unless the project specifies otherwise.
- Keep source tables for every plotted panel and record package installs, version-sensitive choices, and fallback implementations in project records.

## Minimal Workflow

1. State the claim being tested and what would count as success, partial success, or failure.
2. Search for existing related Markdown plan records. Update the closest active plan with a dated new objective section when possible; create a new `docs/<TASK>_PLAN.md` only if no suitable plan exists. Then create or update `AGENT_MEMORY.yaml` and `docs/CURRENT_TASK.md` with the active goal, plan file, current step, known files, decision rules, and recovery notes.
3. If external papers are part of the evidence, pass the External Literature Review Gate before detailed figure critique: create/update the paper-summary record, then review figures one by one.
4. Audit whether the data are fit for the experimental purpose; identify what they can and cannot answer before designing analyses.
5. Pass the purpose-alignment gate: connect experimental design, data observables, readout logic, result judgment, and interpretation boundary to the research purpose.
6. Define the analysis, comparator, null, threshold, or robustness check needed for the claim.
7. Check whether the current machine can reasonably run the analysis. If hardware or local environment is the blocker, generate a portable server-run script with editable input/output paths rather than weakening the scientific endpoint.
8. Run experiments iteratively and record parameters, outputs, result interpretation, and next decision.
9. Judge the result before making final figures, and apply the Figure Assembly Gate before any manuscript-facing panel assembly or publication package.
10. Promote only supported claims to manuscript-facing status, with limitations stated explicitly.
11. Before the final response, update `AGENT_MEMORY.yaml` and `docs/CURRENT_TASK.md` with completed work, changed files, current conclusions, remaining tasks, and any blockers.

Do not turn a context-specific result into a universal method ranking. State the endpoint under which a method helps and acknowledge comparator signal that is actually detected.
