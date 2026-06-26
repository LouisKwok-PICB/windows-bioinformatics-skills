# Design And Randomization

Use this reference before data collection, when auditing a completed study design, or when planning controls for a validation analysis.

## Design Record

```text
Question:
Treatment/exposure/condition:
Primary endpoint:
Independent unit:
Measurement unit:
Replicate level:
Nuisance factors:
Randomization possible: yes/no
Blocking/stratification factors:
Controls/comparators:
Blinding possible:
Batch/run-order risks:
Allowed claim:
Forbidden claim:
```

## Core Principles

- Randomize treatment assignment when causal inference is intended.
- Replicate at the level where the intervention or exposure varies.
- Block or stratify known nuisance factors such as batch, sample, donor, site, FOV, day, plate, operator, or sequencing lane.
- Randomize processing order so time, plate position, and instrument drift do not align with condition.
- Include concurrent controls whenever time, handling, medium, vehicle, or batch could explain the result.

## Pseudoreplication Check

Ask:

1. What received the intervention or defines the biological condition?
2. What was randomized?
3. What is the smallest unit that can vary independently?
4. Are repeated cells/spots/images/reads from the same sample being counted as independent?
5. Does the model include sample, patient, FOV, batch, or spatial block when needed?

If treatment is assigned at sample level, 10,000 cells from 3 samples usually provide `n = 3` biological replicates for treatment effects, not `n = 10,000`.

## Common Designs

| Design | Use when | Analysis implication |
|---|---|---|
| completely randomized | independent units, no major nuisance factors | group comparison or regression |
| randomized block | known nuisance factor affects endpoint | include block in model |
| paired/repeated measures | same unit measured under conditions/time | paired test or mixed model |
| cluster randomized | treatment applied to groups | cluster is inference unit; account for ICC |
| factorial | multiple factors and interactions matter | model main effects and interactions |
| split plot/nested | factors applied at different unit levels | mixed or hierarchical model |

## Batch And Spatial Data Notes

- In omics, sample/donor and batch often dominate apparent signal. Include them in design, model, or null structure.
- In spatial data, preserve local density, tissue region, FOV/sample, and coordinate graph when constructing null models for spatial aggregation.
- In image-derived measurements, tile-level observations are not independent if they come from the same slide or region.
