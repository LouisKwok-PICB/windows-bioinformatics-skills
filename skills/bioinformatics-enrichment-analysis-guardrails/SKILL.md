---
name: bioinformatics-enrichment-analysis-guardrails
description: Design, audit, interpret, and report defensible bioinformatics enrichment analyses for gene lists, ranked genes, network/co-expression modules, spatial panels, proteomics hits, marker genes, or pathway scores. Use when Codex needs to choose ORA vs GSEA/GSVA/ssGSEA, define the correct background universe, check gene-ID mapping, avoid panel-universe bias, reduce redundant GO terms, make enrichment figures or tables, or write manuscript methods/limitations for GO, KEGG, Reactome, MSigDB, Hallmark, Enrichr, g:Profiler, clusterProfiler, fgsea, GSVA, or similar enrichment workflows.
---

# Bioinformatics Enrichment Analysis Guardrails

## Core Rule

Treat enrichment as biological interpretation support, not primary proof. An enrichment result is only defensible when the gene universe, gene IDs, method, directionality, multiple-testing correction, and assay coverage match the scientific claim.

Respect the project's primary analysis language. For R-first projects, use R packages such as `clusterProfiler`, `fgsea`, `msigdbr`, `ReactomePA`, `GSVA`, `gprofiler2`, `AnnotationDbi`, `org.Hs.eg.db`, or project-approved equivalents before switching to Python.

## Decision Workflow

1. Define the input: discrete gene list, ranked gene table, expression matrix, module genes, module weights, proteomics hits, or marker genes.
2. Define the tested universe before running statistics. Use all genes that could have been selected by the assay or upstream analysis, such as detected spatial-panel genes, tested DE genes, module-discovery genes, or proteomics-detected proteins. Do not default to the whole genome.
3. Choose the method:
   - Use ORA for a thresholded hit list.
   - Use preranked GSEA for all tested genes with a signed ranking statistic.
   - Use GSVA/ssGSEA when estimating per-sample or per-cell pathway activity.
   - Use marker/pathway scoring when the question is visualization, not enrichment significance.
4. Map gene identifiers explicitly. Record symbol, Ensembl, Entrez, organism, casing, duplicates, and unmapped genes.
5. Select a small number of libraries that answer the biological question. Prefer Hallmark for broad themes, GO:BP for processes, Reactome/KEGG/WikiPathways for curated pathways, and immune/cell-type libraries only when relevant.
6. Apply multiple-testing correction and report adjusted values, gene-set size, overlap or leading-edge genes, and library version/date.
7. Collapse redundant terms before manuscript display. Do not show many near-duplicate GO terms as independent biology.
8. Judge whether the result supports the intended claim, supports only a weaker interpretation, or is diagnostic only.

## Panel And Targeted-Assay Rule

For targeted spatial transcriptomics, proteomics panels, or any restricted assay, state the feature-overlap universe before interpreting enrichment. A pathway result from a 1K/6K panel tests enrichment within that panel, not across all discovery genes.

When comparing co-expression, network, loading-based, or other module methods, match the universe:

- module genes detected in the validation assay;
- module genes eligible for the comparator;
- genes that entered the original module discovery;
- genes that were unassigned, grey, filtered, or below coverage.

Do not claim a module lacks biology because a restricted panel misses most of its genes. Report coverage and demote unsupported interpretations.

## Reporting Requirements

Every enrichment table or manuscript paragraph should include:

- input gene set or ranked statistic and selection rule;
- background universe and why it is valid;
- organism and gene-ID mapping rule;
- method, package, database/library, version or access date;
- FDR method and cutoff;
- displayed-term selection rule;
- limitation when the result is panel-restricted, exploratory, or low-overlap.

Use `references/enrichment-decision-record.md` when documenting an analysis plan or audit record.
