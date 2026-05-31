# Evidence-Chain Workflow

Use this reference when planning, executing, or judging scientific data-analysis experiments around a target conclusion.

## 1. Extract The Scientific Target

Write the target as a falsifiable or supportable statement:

```text
We want to test whether [method/condition/module] shows [observable behavior]
in [independent data/context], beyond [baseline/null/comparator], supporting
[bounded biological or methodological conclusion].
```

List what would count as success, partial success, or failure. Identify required comparators, negative controls, null models, and robustness checks early.

For algorithmic or method papers, separate:

- what the method computes;
- why the design should help;
- how the result is evaluated;
- what comparator or ablation isolates the claimed contribution;
- which failure modes, costs, or applicability limits remain.

Before an analysis is allowed into the active workflow, pass the purpose-alignment gate:

- experimental design: state what biological or methodological problem the analysis tests;
- data fit: identify the data observable that can answer the problem and what the data cannot answer;
- readout logic: explain why the statistic, model, plot, comparator, null, or threshold reflects the research purpose rather than only being convenient to compute;
- result judgment: define support, partial support, failure, and diagnostic-only outcomes before seeing the result;
- interpretation boundary: define the conclusion allowed if the result succeeds and the claims that remain forbidden.

After the analysis runs, update the same record with observed results, source files, whether the result directly supports the research purpose or only a weaker/subordinate purpose, and the next evidence-chain decision.

## 2. Audit Data Before Analysis

Inventory files before planning figures. Record the fields in `project-documentation.md`.

Run a fit-for-purpose data audit before choosing the final endpoint. Ask whether the data contain the observables, resolution, coverage, controls, and null structure needed for the intended purpose. If the data are only partially fit, redesign the endpoint or restrict the claim before running analysis code.

For spatial, imaging, targeted-panel, perturbation, or multimodal validation projects, explicitly audit:

- whether coordinates, cell/nucleus boundaries, transcript coordinates, morphology or histology images, region annotations, and cell-type labels are present or absent;
- whether the assay is targeted or full-transcriptome, and the overlap or coverage of discovery features in the validation panel;
- whether image-backed overlays are same-sample/same-platform recomputations or cross-platform registrations;
- whether anatomical-region claims require manual/pathology annotations rather than morphology proxies;
- whether protein or multimodal tables have validated cell-level identifiers before joining them to RNA/spatial cells.

## 3. Build The Evidence Chain

For each proposed panel or analysis, define:

- purpose: what inference this panel or statistic enables;
- research-purpose alignment: why this inference matters for the central biological or methodological question;
- input data and required fields;
- method and comparator;
- primary readout;
- quality control;
- decision rule;
- interpretation boundary;
- manuscript claim if successful;
- fallback or retry plan if unsuccessful.

Each main figure panel should answer a distinct evidence-chain step. Move purely technical diagnostics, parameter sensitivity, and null distributions to supplementary outputs unless they are central to the claim.

For comparator-heavy claims, define the endpoint before ranking methods. A comparator may be biologically meaningful even if the new method provides finer resolution, smaller feature sets, partial-overlap localization, or more interpretable subcomponents. Record when the supported claim is decomposition, prioritization, localization, or resolution rather than universal superiority.

For each claim, require one of the following before promoting it to manuscript-facing status:

- direct measurement;
- matched comparator;
- null or negative control;
- ablation;
- orthogonal annotation;
- robustness check;
- explicit limitation with bounded wording.

If none exists, keep the claim as a hypothesis or discussion point.

## 4. Order Scripts

Name scripts with numeric prefixes once the active workflow is known. Prefer the project's primary analysis language for the active numbered workflow:

```text
00_project_config.R
00_publication_plot_style.R
01_audit_data.*
02_prepare_inputs.R
03_compute_primary_scores.R
04_generate_candidate_panel.R
05_evaluate_quantitative_support.R
06_explore_failure_or_rescue_cases.R
07_select_publication_outputs.R
08_make_manuscript_panels.R
```

Keep exploratory scripts, but label them as `exploratory` in `SCRIPT_REGISTRY.md` until promoted.

If the full analysis cannot run on the current Windows machine because of memory, CPU, disk, wall-time, package, or operating-system constraints, do not redefine the scientific endpoint only to make it locally runnable. Prepare a server-run script that can be copied to a larger machine and run after editing paths at the top of the script.

Server-run scripts should:

- expose input paths, output paths, thread counts, seeds, memory-sensitive parameters, and overwrite behavior in a top configuration block;
- validate required input files and create output directories before heavy computation;
- avoid local private absolute paths, GUI prompts, and interactive choices;
- write logs, session information, parameters, and expected output paths;
- be runnable with one command such as `Rscript script_name.R` or `python script_name.py`;
- be recorded in `SCRIPT_REGISTRY.md` with status, expected runtime, expected hardware, inputs, outputs, and whether outputs have been returned and validated.

## 5. Run Experiments Iteratively

For each experiment attempt, record:

- question tested;
- research-purpose alignment and whether this attempt still tests it;
- script and version/path;
- key parameters;
- inputs and outputs;
- execution environment: local, server, HPC, cloud, or not yet run;
- result summary;
- whether it achieved the experiment purpose;
- whether it strengthens, weakens, or does not affect the evidence chain;
- whether it should remain a main result, move to supplementary diagnostics, be redesigned, or be dropped;
- next decision.

If an attempt fails, first adjust implementation while keeping the same scientific purpose. After about three distinct attempts fail for the same purpose, reassess whether the purpose is unsupported by the data, requires a different data source, or should be removed from the evidence chain.

## 6. Judge Results Before Final Figures

Evaluate each candidate result with these questions:

- Does the result answer the research-purpose question the analysis was designed for?
- Does the visual or statistic directly show the intended phenomenon?
- Is the comparator matched to the same data limitations?
- Are null models and thresholds appropriate for the inference?
- Does the null preserve the spatial, sampling, batch, density, or abundance structure that could otherwise create false positives?
- Could the result be explained by coverage, abundance, tissue geometry, sample imbalance, or preprocessing?
- Is the biological interpretation traceable to genes, annotations, literature, or original evidence?
- Would a skeptical reviewer understand the evidence without relying on the author's intent?

Do not assemble final multi-panel figures until individual panels are judged interpretable.

If a result is statistically valid but does not answer the intended research-purpose question, keep it as a diagnostic or supplementary result. Do not retrofit the research purpose around whatever was easiest to compute.

## 7. Write Conclusions Conservatively

Use a four-level wording discipline:

- Observation: what the data show.
- Analysis support: what the statistical or computational test indicates.
- Biological interpretation: what the pattern is consistent with.
- Claim boundary: what is not proven.

Avoid turning a context-specific result into a universal method ranking. State the endpoint under which the method helps and acknowledge comparator signal that is actually detected.
