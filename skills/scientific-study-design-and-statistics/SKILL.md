---
name: scientific-study-design-and-statistics
description: Design defensible scientific studies and statistical analyses, including experimental design, randomization, blocking, pseudoreplication checks, test selection, assumption diagnostics, effect sizes, multiple-testing correction, power/sample-size reasoning, simulation-based power, and manuscript-ready statistical reporting. Use when Codex needs to choose or audit statistical tests, plan controls and comparators, assess study design validity, or write reviewer-facing statistical methods.
---

# Scientific Study Design And Statistics

## Core Rule

Statistical analysis must match the scientific question, sampling unit, design, and data-generating structure. No test can rescue a confounded, underpowered, or pseudoreplicated design. Before running or reporting statistics, identify the independent unit, endpoint, comparator, null hypothesis, covariates, multiplicity, and limitations.

## Reference Routing

- Experimental design, randomization, blocking, batch layout, and pseudoreplication: read `references/design-and-randomization.md`.
- Test selection, assumptions, effect sizes, multiple testing, and reporting: read `references/statistical-analysis-checklist.md`.
- Power/sample size or minimum detectable effect: read `references/power-and-sample-size.md`.
- Compute/resource constraints for permutations, bootstraps, or large models: use `scientific-compute-resource-planner`.
- Figure/manuscript claim boundaries: use `scientific-research-evidence-planner` and `scientific-manuscript-writer`.

## Minimal Workflow

1. State the scientific question and whether the analysis is exploratory or confirmatory.
2. Define the unit of independence. For nested data, the biological or experimental unit is often not the number of cells, spots, images, reads, or repeated measurements.
3. Identify design structure: groups, pairing, blocking, batches, repeated measures, clusters, strata, longitudinal time points, or spatial neighborhoods.
4. Choose the primary endpoint and comparator before selecting a test.
5. Select a test/model that matches outcome type, design, distribution, and independence structure.
6. Check assumptions and diagnostics before interpreting p-values.
7. Report effect size with confidence or credible intervals whenever possible.
8. Apply multiplicity control when multiple hypotheses, modules, genes, terms, regions, or pairwise contrasts are tested.
9. Run sensitivity or robustness checks for fragile choices such as thresholds, null models, transformations, and outlier handling.
10. Write methods with enough detail to reproduce the statistic, software, versions, thresholds, and null model.

## Defaults

- Prefer R for R-first projects unless a mature Python package is clearly better for the task.
- Prefer established packages over hand-written statistics.
- Use seeded randomization, permutations, bootstraps, and simulations.
- For spatial, single-cell, and omics analyses, document whether inference is per sample, per patient, per FOV, per cell, per gene, or per module.
- Treat p-values from pseudoreplicated cell-level tests as descriptive unless the model accounts for sample/subject/FOV structure.

## Guardrails

- Do not interpret non-significance as evidence of no effect without power or interval evidence.
- Do not report observed/post-hoc power from the observed effect as if it were informative.
- Do not switch tests until one is significant without labeling the analysis exploratory.
- Do not collapse biological replicates into technical replicates or vice versa.
- Do not claim causality from observational associations unless the design supports it.
