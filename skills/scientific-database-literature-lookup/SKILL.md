---
name: scientific-database-literature-lookup
description: Plan and perform source-backed scientific literature, gene, pathway, dataset, accession, and public database lookups for biomedical analysis. Use when Codex needs PubMed/PMC/bioRxiv/arXiv/OpenAlex/Crossref/Semantic Scholar searches, GEO/SRA/ENA dataset checks, gene or protein annotation, Reactome/KEGG/STRING/GO/UniProt/HPA/Open Targets context, citation verification, paper summaries, or manuscript background with links and exact source provenance.
---

# Scientific Database Literature Lookup

## Core Rule

Use primary, source-backed records for scientific facts that may affect analysis, manuscript claims, citations, or data provenance. Do not rely on memory for current package versions, public dataset files, author claims, gene annotations, pathway membership, or journal requirements when the source can be checked.

When browsing or querying external sources, return enough provenance for another agent to reproduce the lookup: database, endpoint or URL, query string, date, identifier, and source status.

## Source Selection

- Use PubMed/PMC for biomedical papers and full text when available.
- Use Crossref, DOI, or publisher pages for citation metadata.
- Use GEO/SRA/ENA for sequencing dataset accessions and file availability.
- Use UniProt, Ensembl, NCBI Gene, HGNC, or HPA for gene/protein annotation.
- Use Reactome, KEGG, GO/QuickGO, STRING, BioGRID, or MSigDB for pathway and interaction context.
- Use Open Targets, ClinVar, COSMIC, cBioPortal, or GWAS Catalog only when disease or variant context is needed.
- Use official package documentation for software behavior and version-sensitive APIs.

Read `references/source-selection.md` for a compact routing table.

## Literature Summary Gate

For any paper that will influence figure design, method wording, or biological interpretation, create a summary record before using it as evidence:

- citation and DOI/PMID/PMCID or official URL;
- source status: abstract only, full text, PDF, supplementary files, or dataset page;
- scientific question and assay;
- datasets and species/tissue context;
- main claim and validation endpoints;
- relevant figures/tables;
- limitations or reviewer risks;
- how it does or does not apply to the current project.

## Output Rules

- Provide links for sources used.
- Distinguish direct source facts from inference.
- Do not overquote source text.
- Prefer primary sources over blogs or secondary summaries.
- For recommendations that could change, verify current status.
- For data downloads, record exact accession, file name, size if available, and download URL.
- For manuscript use, retain citation identifiers and access dates in the project record.
