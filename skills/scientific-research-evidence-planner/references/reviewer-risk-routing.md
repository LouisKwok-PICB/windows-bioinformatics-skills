# Reviewer Risk Routing

Use this reference when a planned or completed analysis needs a skeptical pre-submission audit.

## When To Run

Run this audit before promoting a result to manuscript-facing status, especially when a claim depends on:

- a comparator or baseline;
- proxy labels, thresholds, or high-tail/module-high calls;
- enrichment, marker, or annotation interpretation;
- sparse, rare, or heterogeneous subsets;
- targeted-panel, spatial, image-derived, or multimodal validation;
- missing or incomplete source-data/code availability;
- a result that might be interpreted as universal method superiority.

## Attack-Surface Checklist

Ask whether the current evidence handles:

- unmatched baseline inputs, feature universes, parameters, or endpoints;
- proxy labels or thresholds being overstated as ground-truth biology;
- broad group summaries hiding within-group heterogeneity;
- enrichment or marker annotations being treated as primary proof rather than interpretation support;
- missing source-data maps, code availability, package versions, or exact parameters;
- targeted-panel coverage explaining an apparent failure or success;
- null models that fail to preserve spatial, sampling, batch, density, or abundance structure;
- high overlap with a comparator being framed as failure rather than possible redundancy or shared signal;
- marker-defined context, image-derived masks, or morphology proxies being overstated as ground-truth anatomy or biology;
- failed or weak branches being promoted as conclusions instead of documented as diagnostics.

## Handling Rules

- If a defense requires one or two sentences, add it near the first relevant Results or figure-legend mention rather than burying it only in Methods.
- If a concern requires new data or analysis, mark it as `needs analysis`.
- If a concern is inherent to the study design, mark it as `limitation` and write bounded claims.
- If a claim has no supporting evidence, mark it as `unsupported claim` and remove or downgrade it.
- Do not invent reviewer concerns from habit alone; use concerns that follow from supplied data, methods, figures, or missing controls.

## Three-Pass Review

For a full pre-submission review, use three emphasis passes over the same fact base:

1. Technical soundness: controls, nulls, comparators, statistics, reproducibility.
2. Contribution and significance: novelty, prior-work contrast, scope, field value.
3. Readability and reproducibility: terminology, figure clarity, Methods readability, data/code availability.

Synthesize shared risks rather than inventing reviewer personas, institutions, or editorial decisions.
