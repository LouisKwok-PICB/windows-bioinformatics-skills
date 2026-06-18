# Scientific Exploration Planning Rules

Use this reference when designing, auditing, or executing a scientific exploration plan, especially when the work may lead to manuscript claims, main/supplement figures, method-validation conclusions, or multimodal biological interpretation.

## Quick Navigation

- Required planning chain: `1. Start From The Scientific Question`
- Data suitability: `2. Judge Data Fit Before Analysis`
- Analysis design: `3. Use Endpoint-Native Readouts`
- Evidence logic: `4. Build A Non-Redundant Evidence Chain`
- Result judgment: `5. Define Outcomes Before Running`
- Figure planning: `6. Convert Evidence To Display Only After Judgment`
- Forbidden actions: `7. Absolute Do-Nots`
- Execution discipline: `8. Ordered Scientific Progression`

## 1. Start From The Scientific Question

Every plan must begin with a named biological or methodological question. Do not begin from:

- an existing plot that looks available;
- a convenient source table;
- a metric that is easy to compute;
- a desire to make the conclusion stronger;
- a need to fill a figure panel.

Write the question in this form:

```text
Does [fixed method output / biological hypothesis / comparator relation] show
[observable behavior] in [data context], under [matched readout or control],
supporting [bounded conclusion] while not claiming [forbidden stronger claim]?
```

For algorithm or method projects, explicitly separate:

- method rationale: what the algorithm is designed to capture;
- biological reason: why that rationale matters in this dataset;
- independent observable: what external data can test the rationale without circular reuse;
- comparator logic: whether the baseline is a negative control, positive comparator, broad related signal, or different organization of the same biology;
- evaluation endpoint: what exact readout judges success.

If these layers are mixed together, fix the plan before executing.

## 2. Judge Data Fit Before Analysis

For each planned question, record what data would be required if the question were tested ideally, then compare that to the available data.

Classify each data layer as:

- `direct`: can directly measure the planned observable;
- `context`: can support interpretation but not prove the main claim;
- `panel-restricted`: can test only covered features or assayed subsets;
- `proxy`: can support a candidate interpretation but not ground truth;
- `blocked`: no linked quantitative endpoint or required metadata is present;
- `not relevant`: present but unrelated to the question.

Do not write that a study "uses all data" unless every available modality or data layer has been assigned one of these roles with a reason. Using all data scientifically can mean direct use, context use, proof of blockage, or explicit exclusion; it does not mean forcing every file into a plot.

If the data are not fit for the desired claim, do one of three things:

- restrict the claim to what the data can test;
- redesign the endpoint around available observables;
- mark the question as untestable with current data.

Do not hide an untestable claim behind a polished figure.

## 3. Use Endpoint-Native Readouts

The readout must match the scientific question. Choose statistics, nulls, thresholds, plots, and comparators because they test the planned construct, not because they are convenient.

Ask before coding:

- What exact quantity is observed?
- What structure must the null or control preserve?
- Is the comparator measured on the same feature universe, samples, labels, and endpoint?
- Does the threshold represent an operational proxy rather than ground truth?
- Would a negative or mixed result still answer the question?
- What alternative explanations remain after this readout?

Examples of endpoint mismatch:

- using global autocorrelation to claim subtle within-label biology without showing module traceability or biological context;
- using overlap or gene count alone to claim functional similarity;
- using source availability, coverage, or QC status as a biological result;
- using image overlays as validation when there is no linked quantitative image endpoint;
- using a broad comparator's biological signal as evidence that the comparator failed.

If the readout does not answer the question, redesign it or record it as diagnostic only.

## 4. Build A Non-Redundant Evidence Chain

Each evidence block must change what the reader can infer. Classify every planned block as:

- `direct evidence`: shows the target observable in the relevant data;
- `matched statistical support`: tests the same readout against a baseline, null, or comparator;
- `biological anchor`: links the observable to markers, pathways, cell states, tissue regions, or known biology;
- `comparator boundary`: shows what the comparator captures and what the new method adds under the same endpoint;
- `robustness`: tests threshold, feature subset, marker-core, sample, label, or context dependence;
- `scope boundary`: shows where the claim does not extend;
- `diagnostic only`: explains a limitation but does not support the biological conclusion.

Do not include two panels or analyses that answer the same inferential step unless the second expands scope or tests robustness. Do not promote diagnostic-only outputs as result figures.

For multimodal projects, assign each modality to an evidence-chain role. A modality that only provides context should not be worded as validation.

## 5. Define Outcomes Before Running

Before execution, write a result judgment rule:

- `support`: what result would directly support the planned conclusion;
- `partial support`: what result would support only a selected context, proxy, or subset;
- `mixed`: what result would require narrower wording or additional analysis;
- `failure`: what result would contradict the planned conclusion;
- `diagnostic only`: what result only explains feasibility, data fit, or limitations.

After execution, judge the observed result against this pre-specified rule. Do not retrofit the claim around whatever result looked attractive.

When a result is negative, partial, or blocked, preserve it in the evidence record. The goal of exploration is to learn the truth of the data, not to force a stronger conclusion.

## 6. Convert Evidence To Display Only After Judgment

Only after a result passes the evidence-chain judgment should it become a candidate figure. Decide display type from evidence role:

- spatial observable -> real coordinate map, ROI map, or spatial score map;
- matched statistical support -> observed-vs-background axis, interval, distribution, or calibrated benchmark;
- biological anchor -> gene/pathway/marker score map, expression heatmap, or interpretable dotplot;
- comparator boundary -> paired same-endpoint map/statistic, decomposition behavior, or compactness display;
- robustness -> ablation or sensitivity axis;
- context-only modality -> clearly labeled context heatmap/dotplot with limitations in legend;
- blocked or data-fit result -> text, Methods, or source table, not a figure panel.

Do not produce source-table-like figures. A result figure must show biological behavior or matched statistical behavior directly. Internal gate tables, manifests, QC checks, file inventories, status matrices, source availability, coverage-only plots, gene-set-size-only plots, p/q lists, and blocked-endpoint audits are project controls, not paper figures.

For publication-facing figures, visible labels should be short reader-facing terms. Put definitions, matching rules, p-value calculation, quantile definitions, threshold definitions, coverage caveats, and detailed selection rules in the figure legend, Methods, or source data.

## 7. Absolute Do-Nots

Never do the following in a scientific exploration plan:

- Do not start from "what can I plot?" instead of "what question can the data answer?"
- Do not run many weak analyses and later filter for attractive plots without a recorded evidence role.
- Do not treat a source table, QC gate, manifest, or coverage audit as a biological result.
- Do not use a data layer just because it exists; assign a fit-for-purpose role first.
- Do not claim direct validation from a modality without linked quantitative identifiers and a registered endpoint.
- Do not claim true state, stimulation, causality, temporal order, anatomical ground truth, or universal method superiority from proxy readouts.
- Do not describe a comparator as failed when it detects related biology under the same endpoint.
- Do not weaken the endpoint because the local machine is slow; create a server-run plan when resources are the blocker.
- Do not move matching principles, threshold definitions, or statistical formulas into large in-image text; keep panels visually clean and define methods in legend/Methods/source data.
- Do not leave plan progress only in chat history. Update project records when scientific scope, evidence status, or next action changes.

## 8. Ordered Scientific Progression

Use this order for rigorous project advancement:

1. Recover active project records and identify the current objective.
2. Restate the biological or methodological question and the exact claim being tested.
3. Inventory available data and classify fit for each required observable.
4. Define endpoint-native analyses, comparators, nulls, thresholds, and robustness checks.
5. Define success, partial success, failure, and diagnostic-only outcomes before running.
6. Run the smallest analysis that answers the next evidence-chain question.
7. Judge the result scientifically before plotting or polishing.
8. Decide whether the evidence block is main, supplement, source-only, diagnostic-only, or removed.
9. If a figure is justified, choose a display grammar that matches the evidence role and publication norms.
10. Audit visible terminology and claim boundaries before any manuscript-facing promotion.
11. Update recovery records, plan files, script registry, and source-data paths.
12. Stop at the correct gate if author approval, data fit, endpoint validity, or resource execution is unresolved.

This order is intentionally strict. It prevents projects from drifting into visually polished but scientifically weak outputs.
