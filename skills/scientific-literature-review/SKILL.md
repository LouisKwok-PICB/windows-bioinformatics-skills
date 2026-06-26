---
name: scientific-literature-review
description: Plan, execute, document, and synthesize rigorous scientific literature reviews, scoping reviews, focused paper surveys, and manuscript background searches. Use when Codex needs search strategy design, database selection, inclusion/exclusion criteria, PRISMA-style screening records, thematic synthesis, citation-chaining, evidence-quality notes, or review-ready Markdown outputs for biomedical, omics, computational, or general scientific topics.
---

# Scientific Literature Review

## Core Rule

Treat literature review as an auditable study of prior work, not as a list of convenient citations. Define the question, search sources, screening criteria, evidence extraction fields, and synthesis logic before using papers to support a claim.

Use primary databases and source-backed records. Do not cite a paper from memory when DOI, PMID, PMCID, preprint ID, or publisher page can be checked.

## Review Modes

- `focused lookup`: a small set of papers needed for one claim, method, or figure decision.
- `scoping review`: broad mapping of a field, terminology, methods, datasets, or gaps.
- `systematic-style review`: predefined search strings, inclusion/exclusion criteria, deduplication, screening counts, extraction table, and limitations.
- `citation chaining`: forward and backward search from seed papers to find foundational or recent linked work.

Do not claim a formal systematic review or meta-analysis unless the search, screening, extraction, and quality-assessment records actually meet that standard.

## Reference Routing

- Search design, database choice, Boolean/MeSH strategy, and PRISMA-style records: read `references/search-and-screening.md`.
- Paper extraction, thematic synthesis, evidence-quality notes, and review writing: read `references/synthesis-template.md`.
- Citation accuracy, BibTeX, DOI/PMID conversion, or reference-list QC: use `scientific-citation-management`.
- Current paper, accession, gene, pathway, or database lookup: use `scientific-database-literature-lookup`.
- Manuscript prose from an already established evidence table: use `scientific-manuscript-writer`.

## Minimal Workflow

1. State the review question and review mode.
2. Choose databases that match the domain. For biomedical topics, use PubMed/PMC plus at least one broader index such as OpenAlex, Crossref, Semantic Scholar, or a relevant preprint server when current literature matters.
3. Define inclusion/exclusion criteria before screening.
4. Record exact search strings, dates, databases, filters, result counts, and access URLs.
5. Deduplicate by DOI, PMID/PMCID, arXiv/bioRxiv ID, or normalized title.
6. Screen titles/abstracts, then full text when needed. Record exclusion reasons for systematic-style work.
7. Extract reusable fields into a table: citation, assay/data, sample context, method, comparator, key result, limitations, and relevance to the current project.
8. Synthesize by theme, method, dataset, or evidence role. Avoid one-paper-per-paragraph summaries unless the task explicitly asks for annotated bibliography.
9. State limitations: search coverage, preprint status, access limits, field bias, and whether conclusions rely on indirect evidence.
10. Save or return a compact review record that another agent can reuse without repeating the search.

## Output Standard

Every non-trivial review record should include:

- question and scope;
- databases and exact search strings;
- date searched and date range;
- result counts and deduplication count when available;
- inclusion/exclusion criteria;
- included papers with identifiers;
- synthesis themes;
- evidence-quality or reviewer-risk notes;
- how each result can or cannot support the current project.

## Guardrails

- Do not use citation count alone as proof of truth. Use it only as an influence or discovery signal.
- Do not treat preprints as peer-reviewed evidence without saying so.
- Do not overgeneralize from review papers; follow key claims back to primary studies when they support a manuscript result.
- Do not silently mix human, mouse, organoid, bulk, single-cell, spatial, or protein studies when the biological context matters.
- Do not add AI-generated schematics or figures as a mandatory literature-review output unless the user asks for visual review material.
