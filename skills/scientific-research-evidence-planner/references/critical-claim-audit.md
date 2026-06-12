# Critical Claim Audit

Use this reference when a result is close to becoming a manuscript claim, main panel, or reviewer-facing conclusion.

## Claim Type

Classify the statement before judging support:

- `descriptive`: reports what was observed.
- `associational`: links two observed variables.
- `comparative`: ranks methods, groups, modules, or conditions under a specific endpoint.
- `mechanistic`: proposes a biological process or pathway.
- `causal`: says one factor produces another.
- `predictive`: claims performance on future or held-out data.
- `methodological`: claims an algorithmic advantage or limitation.

## Evidence Type

Record whether support is:

- direct independent evidence;
- proxy readout;
- annotation or marker overlay;
- enrichment interpretation;
- null/permutation statistic;
- comparator benchmark;
- simulation;
- external paper or dataset support.

Proxy evidence can support prioritization or interpretation, but not ground truth unless independently validated.

## Validity Checks

Ask:

- Does the observable measure the intended construct?
- Could batch, sample composition, coverage, density, or preprocessing explain it?
- Is the comparator matched to the same universe and endpoint?
- Are cells, samples, donors, fields of view, or repeated measures being treated as independent incorrectly?
- Is the result exploratory or confirmatory?
- Are negative, mixed, or diagnostic results being hidden?

## Alternative Explanations

List plausible alternatives before writing the claim. Common scientific-analysis alternatives include:

- gene panel or assay coverage;
- local tissue density or image mask artifacts;
- threshold or top-tail selection;
- unbalanced cell type composition;
- batch/FOV/sample effects;
- gene-ID mapping loss;
- broad comparator module signal rather than comparator failure;
- visual sharpness without independent biological annotation.

## Wording Calibration

Use:

- `show` for direct and strong evidence;
- `indicate` for well-supported but indirect evidence;
- `suggest` for plausible proxy-supported interpretation;
- `is consistent with` when evidence matches but does not distinguish alternatives;
- `may` or `could` for speculation.

Avoid `prove`, `establish`, `causal`, `specific anatomical niche`, `ground truth`, `universal superiority`, or equivalent wording unless the evidence directly supports it.
