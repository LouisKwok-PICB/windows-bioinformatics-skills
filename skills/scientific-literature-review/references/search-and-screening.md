# Search And Screening

Use this reference when designing a literature search or screening record.

## Search Design Record

```text
Review question:
Review mode: focused lookup | scoping review | systematic-style review | citation chaining
Domain:
Core concepts:
Synonyms/acronyms:
Species/tissue/disease/context:
Date range:
Study types to include:
Study types to exclude:
Databases:
Search date:
```

## Database Routing

| Need | Preferred sources |
|---|---|
| Biomedical papers | PubMed, PMC, Europe PMC when available |
| Broad scholarly coverage | OpenAlex, Crossref, Semantic Scholar |
| Preprints | bioRxiv, medRxiv, arXiv |
| Full text/open access | PMC, Unpaywall, CORE, publisher page |
| Citation chaining | Semantic Scholar, OpenAlex, article reference lists |
| Method/software behavior | official documentation, release notes, source repository |
| Dataset provenance | GEO, SRA, ENA, ArrayExpress, Zenodo, Figshare, official project repository |

Use at least two complementary sources for broad review questions. A single PubMed search is acceptable only for a narrow biomedical lookup.

## Query Construction

1. Split the question into 2-4 concepts.
2. For each concept, list synonyms, spelling variants, abbreviations, and controlled terms.
3. Combine synonyms with `OR`, concepts with `AND`, and exclusions with `NOT` only when they are specific.
4. Use field tags when available:
   - PubMed title/abstract: `[Title/Abstract]`
   - PubMed MeSH: `[MeSH Terms]`
   - PubMed publication type: `[Publication Type]`
   - PubMed date: `[Publication Date]`
5. Pilot the query and inspect top hits. Revise if results are mostly off-target or if obvious seed papers are missing.

## Screening Record

```text
Database:
Search string:
Filters:
Date searched:
Raw count:
Export file/path:
Deduplication rule:
Unique count:
Title/abstract included:
Full-text assessed:
Final included:
Main exclusion reasons:
Limitations:
```

For systematic-style work, preserve raw exports and a screening table. For focused lookup, a compact record with query, top candidates, and selected sources is enough.

## Citation Chaining

- Backward chaining: inspect references of key papers for foundational methods, datasets, or mechanisms.
- Forward chaining: search papers citing key papers for recent validations, critiques, or extensions.
- Track seed paper, direction, database, date, and reason each chained paper was included.

## Quality And Bias Checks

- Prefer primary studies for factual claims and review papers for field orientation.
- Mark preprints, reviews, editorials, protocols, and computational-only studies explicitly.
- Record sample size, assay, species, tissue, disease context, comparator, and validation endpoint when they affect applicability.
- Note publication bias, database indexing bias, language limits, and inaccessible full text.
