# Reviewer-Risk Audit For Scientific Manuscripts

## Scope

Use this reference when auditing a manuscript, figure package, or result section before submission. It is journal-general and should be adapted to the target journal. Do not invent missing experiments, reviewer identities, citations, or field-specific objections that are not implied by the supplied text, figures, methods, or data.

## Build The Fact Base First

Before writing critique or revisions, extract:

- manuscript type and submission posture;
- central claim;
- key evidence presented;
- claimed significance and intended audience;
- datasets, baselines, controls, ablations, statistics, and source tables actually shown;
- visible limitations and missing information;
- terms, abbreviations, and notation that need consistency.

If evidence is incomplete, mark the assessment boundary rather than filling it in. Useful labels are `not assessable from provided material`, `author input needed`, `needs analysis`, `needs wording`, `limitation`, and `unsupported claim`.

## Review Axes

Audit the manuscript across these axes:

- **Technical soundness:** Does the evidence establish the claim under the stated data, baseline, null model, threshold, and statistical design?
- **Originality and contribution:** Is the advance distinguished from prior work and from standard workflows without inflated novelty language?
- **Significance and scope:** Is the claim important for the target field, and is its scope bounded to the demonstrated evidence?
- **Comparator and control fairness:** Are baselines matched to the same input, endpoint, feature universe, and limitations? Are detected comparator signals acknowledged?
- **Reproducibility:** Are inputs, preprocessing, parameters, software, source tables, and code/data availability sufficient for an experienced reader to reproduce the analysis?
- **Readability:** Can a non-specialist or adjacent-field reader understand what was done, what the data show, and what remains unproven?

For algorithmic or methods papers, also audit:

- task definition and target failure mode;
- method mechanism versus design rationale versus evaluation result;
- ablations or matched comparisons that isolate the claimed contribution;
- failure modes, cost, sensitivity, and applicability boundary.

## Three-Pass Pattern

When a rigorous pre-submission review is useful, use three reviewer emphases over the same fact base:

1. **Technical reviewer:** focuses on controls, nulls, comparators, statistics, reproducibility, and unsupported mechanisms.
2. **Contribution reviewer:** focuses on novelty, relation to prior work, significance, and whether the claim is more than incremental.
3. **Reader-facing reviewer:** focuses on clarity, terminology, figure-legibility, Methods readability, and whether broad claims are understandable.

Then synthesize:

- shared strengths;
- shared technical concerns;
- significance or framing concerns;
- readability or terminology concerns;
- highest-priority fixes before submission.

Do not create fictional reviewer biographies, institutions, or final editorial decisions.

## Common Attack Surfaces

Check whether the manuscript handles:

- proxy labels being overstated as ground truth;
- broad group means hiding within-group heterogeneity;
- unbalanced module, class, or sample sizes;
- unmatched baseline inputs or unfair parameter choices;
- weak null models that do not preserve sampling, batch, spatial, or abundance structure;
- enrichment being used as primary proof rather than interpretation support;
- high overlap with a comparator being framed as failure rather than possible redundancy or shared signal;
- overclaiming universal method superiority from one endpoint;
- missing source data, code availability, package versions, or exact parameter values;
- figure legends that omit statistics, thresholds, abbreviations, or source-data references.

## Output Pattern

For an audit, lead with issues:

```text
Reviewer-risk audit

Blocking or high-priority risks
- [risk]: [why it matters] -> [needed fix]

Moderate risks
- [risk]: [why it matters] -> [needed fix]

Handled or low-risk items
- [item]: [why current text/evidence is acceptable]

Claim-boundary edits
- [specific wording change or principle]

Missing information
- [author input needed or not assessable]
```

For a manuscript revision task, convert the audit into concrete edits in Results, Methods, legends, Discussion, or availability statements, but keep the audit trail concise.
