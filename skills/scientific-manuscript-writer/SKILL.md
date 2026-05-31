---
name: scientific-manuscript-writer
description: Draft, restructure, or audit evidence-first scientific manuscript text from claims, figures, results, methods, limitations, reviewer risks, or Chinese research notes. Use when Codex needs to write Results, Methods, Discussion, figure legends, abstracts, response-aware claim wording, manuscript outlines, paragraph flow repairs, or publication-facing scientific prose without domain-specific overclaiming.
---

# Scientific Manuscript Writer

## Core Rule

Write the argument before writing sentences. Every manuscript paragraph must connect a bounded claim to visible evidence, methods, or limitations. Do not invent results, mechanisms, sample sizes, statistics, citations, novelty, or reviewer-facing defenses.

Use this skill for general manuscript writing. If a domain-specific guardrail skill exists, use both: this skill controls manuscript structure, and the domain skill controls allowable claims.

For a structured pre-submission or skeptical-review pass, read `references/reviewer-risk-audit.md`.

## Coordination

Use this skill for general manuscript architecture, paragraph flow, Methods/Results/Discussion drafting, figure legends, and evidence-calibrated wording. When a domain-specific guardrail exists, use it for allowable claims and terminology. Use `scientific-research-evidence-planner` for deciding whether the evidence is sufficient, `publication-content-packager` for organizing a figure/publication package, and plot/assembly skills for visual implementation. Do not use this skill to invent missing results, citations, statistics, or method-specific claims.

## Intake

Before drafting or revising, identify:

- section: Abstract, Introduction, Results, Methods, Discussion, figure legend, response text, or full outline;
- paper type: research, methods, algorithmic/tool, resource, review, or mixed;
- one-sentence argument: what is shown, by what approach, with what evidence, and with what boundary;
- evidence base: figures, source tables, statistical tests, datasets, baselines, ablations, controls, or author notes;
- terminology ledger: canonical method names, abbreviations, dataset labels, modules, metrics, and notation;
- claim boundary: what the current evidence does not prove;
- target journal or formatting constraints if provided.

If the core claim, evidence, or boundary is missing, expose the gap. You may draft a scaffold, but mark missing evidence explicitly rather than filling it in.

## Manuscript Workflow

1. **Build the one-sentence argument.**
   Use this form: `In [system/problem], we show [advance] using [approach], supported by [evidence], with [boundary].`

2. **Choose section architecture.**
   Results should move from validation to main result, comparator, mechanism or ablation, robustness, then limitation. Methods should move from task formulation to pipeline overview, per-module details, implementation parameters, and assumptions. Discussion should separate implication, comparison, limitation, and future work.

   For algorithmic or methods papers, preserve this argument chain: task definition and scope -> system or method design -> design rationale -> evaluation endpoint -> matched comparator or ablation -> failure modes and cost -> applicability boundary.

3. **Assign one job per paragraph.**
   Each paragraph should do one of: context, gap, approach, result, comparison, mechanism, implication, limitation, or transition. Split paragraphs that mix several jobs.

4. **Draft from evidence outward.**
   Keep claims close to the figure, table, statistic, or method that supports them. Avoid front-loading broad claims and only supplying evidence later.

5. **Calibrate verbs.**
   Use `show` or `demonstrate` only for direct, strong evidence. Use `indicate` or `suggest` for indirect, trend-level, or proxy evidence. Use `may` or `could` for plausible mechanisms that are not directly tested.

6. **Remove unsupported reach.**
   Sweep for words such as `first`, `unique`, `unprecedented`, `comprehensive`, `complete`, `always`, and `never`. Keep them only when the supplied evidence and literature support them.

7. **Run reviewer-risk checks.**
   Ask what a skeptical reviewer could attack: missing control, unmatched baseline, weak null, proxy labels, insufficient sample size, unclear data availability, unsupported mechanism, or inflated novelty. Address fragile points in Results, legends, Methods, or limitations.

8. **Return prose plus audit notes.**
   Provide ready-to-use text, then a short note listing assumptions, missing inputs, claim boundaries, and any items that require author confirmation.

## Section Rules

### Results

- Start each subsection with the result claim, then provide data support.
- State dataset, condition, comparator, metric, threshold, and statistical test when relevant.
- Keep observation and interpretation distinct.
- If a major claim lacks comparison, ablation, control, or stress-test evidence, flag it rather than drafting around the weakness.
- Put technical diagnostics in supplementary text unless they are required to understand the main claim.

### Methods

- Make the method reproducible: inputs, preprocessing, algorithm steps, parameters, thresholds, software/packages, versions if available, and output locations.
- For each pipeline module, write motivation, mechanism/design, technical advantage, and role in the evidence chain. Describe the forward process as input -> steps -> output before discussing why the module helps.
- Replace vague phrases such as `standard methods`, `routine analysis`, or `validated statistically` with actual procedures.
- State how null models, randomization, batch handling, and multiple testing were implemented when they support a claim.

### Discussion

- Separate the supported contribution from biological or technical interpretation.
- Name failure modes and data limitations revealed by the analyses.
- Avoid turning a context-specific advantage into universal superiority.
- End with the bounded significance of what is now supported, not with new unsupported claims.

### Figure Legends

- Describe what each panel shows, the sample/data context, the plotted quantity, statistics, thresholds, abbreviations, and source table when relevant.
- For null models or high-risk controls, state what structure was preserved.
- Do not hide claim boundaries only in Methods if the figure itself invites overinterpretation.

## Chinese Author Notes

When the user provides Chinese or mixed Chinese-English notes:

- preserve the scientific meaning first, not literal word order;
- keep canonical English terms consistent with the terminology ledger;
- output manuscript-ready English when requested, plus concise Chinese audit notes when useful;
- flag places where Chinese notes contain an intended claim but not the supporting evidence.

## Output Pattern

For substantial drafting, use:

```text
Detected task
- Section:
- Paper type:
- One-sentence argument:
- Evidence used:
- Claim boundary:

Draft
[manuscript-ready text]

Audit notes
- Assumptions:
- Missing inputs:
- Reviewer risks:
- Suggested next edits:
```

For small edits, keep the answer concise but still preserve claim boundaries.
