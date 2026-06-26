---
name: scientific-citation-management
description: Verify, clean, format, deduplicate, and audit scientific citations, BibTeX files, DOI/PMID/PMCID/arXiv identifiers, reference lists, and manuscript citation usage. Use when Codex needs citation metadata extraction, Crossref/PubMed/arXiv lookup, BibTeX quality control, missing-field repair, duplicate detection, unresolved citation checks, unused reference checks, or journal-ready bibliography hygiene.
---

# Scientific Citation Management

## Core Rule

Never let citation metadata be the weakest part of a manuscript. Prefer identifier-backed metadata from DOI, PMID/PMCID, arXiv/bioRxiv, publisher, PubMed, Crossref, or DataCite records over hand-written references.

## Reference Routing

- DOI/PMID/arXiv metadata extraction and BibTeX templates: read `references/metadata-and-bibtex.md`.
- Manuscript/reference-list QC, missing citations, duplicates, and unused entries: read `references/citation-qc.md`.
- Literature search strategy: use `scientific-literature-review`.
- Database/API source routing: use `scientific-database-literature-lookup`.

## Minimal Workflow

1. Identify the citation artifact: manuscript, reference list, BibTeX, DOI list, PMID list, or mixed identifiers.
2. Normalize identifiers. Preserve DOI, PMID, PMCID, arXiv/bioRxiv ID, accession, software DOI, and dataset DOI when available.
3. Fetch or verify metadata from authoritative sources.
4. Deduplicate by DOI first, then PMID/PMCID, then normalized title plus first author and year.
5. Check required fields by entry type.
6. Repair missing fields from source records or publisher pages. If a field is genuinely unavailable, add a note rather than inventing it.
7. Check manuscript usage: unresolved citation keys, cited-but-missing entries, and unused bibliography entries.
8. Report remaining risks before declaring the bibliography clean.

## Required Fields

| Entry type | Required | Usually needed |
|---|---|---|
| journal article | author, title, journal, year | volume, issue, pages or e-location, DOI, PMID |
| preprint | author, title, repository, year | DOI, preprint ID, version/date |
| dataset/software | author/creator, title, year, repository/publisher | DOI, version, URL, access date |
| book/chapter | author/editor, title, publisher, year | edition, chapter, pages, DOI/ISBN |
| conference paper | author, title, venue/booktitle, year | pages, DOI, location |

## Output Standard

For non-trivial citation work, report:

- input artifact;
- number of entries checked;
- identifiers used;
- metadata sources;
- duplicates removed or suspected;
- missing/invalid fields fixed;
- unresolved manuscript citations;
- unused entries;
- remaining warnings.

## Guardrails

- Do not scrape Google Scholar aggressively or rely on it as the only metadata source.
- Do not expose API keys or email values used for polite API access.
- Do not rewrite citation style manually when a structured BibTeX or CSL workflow is available.
- Do not use citation count as a replacement for evidence quality.
- Do not cite an unpublished or preprint version when a peer-reviewed version is the intended source, unless the preprint is specifically relevant.
