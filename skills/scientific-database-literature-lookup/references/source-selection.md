# Source Selection

Use the narrowest primary source that answers the question.

| Need | Preferred source |
|---|---|
| Biomedical paper metadata | PubMed, Crossref, publisher DOI page |
| Biomedical full text | PMC, publisher page, article PDF |
| Preprint | bioRxiv, medRxiv, arXiv official record |
| Dataset accession/files | GEO, SRA, ENA, Zenodo, Figshare, official project repository |
| Gene identity and aliases | HGNC, NCBI Gene, Ensembl |
| Protein function | UniProt |
| Tissue/protein expression | Human Protein Atlas, GTEx |
| Pathway membership | Reactome, KEGG, GO/QuickGO, MSigDB |
| Protein/gene interactions | STRING, BioGRID |
| Disease/target context | Open Targets, ClinVar, OMIM, GWAS Catalog |
| Package/API behavior | Official package documentation or release notes |
| Journal requirements | Official journal author guidelines |

## Lookup Record

```text
Question:
Database/source:
URL or endpoint:
Query:
Date checked:
Identifiers:
Result:
Limitations:
How used in project:
```

## Guardrails

- Use exact identifiers before names when possible.
- Check organism and gene symbol casing.
- Record when only abstracts or snippets were available.
- Do not treat database association as mechanism without independent support.
- For public datasets, distinguish series-level pages from actual downloadable files.
