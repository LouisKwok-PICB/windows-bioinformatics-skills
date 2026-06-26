# Metadata And BibTeX

Use this reference for identifier-backed citation extraction and BibTeX cleanup.

## Identifier Priority

1. DOI
2. PMID/PMCID for biomedical papers
3. arXiv/bioRxiv/medRxiv ID for preprints
4. DataCite DOI for datasets/software
5. Publisher URL or official repository URL
6. Title + first author + year when no identifier exists

## Metadata Sources

| Identifier | Preferred source |
|---|---|
| DOI | Crossref, publisher DOI page, DataCite for datasets/software |
| PMID/PMCID | PubMed/PMC E-utilities |
| arXiv ID | arXiv API |
| bioRxiv/medRxiv DOI | preprint API or DOI metadata |
| dataset/software DOI | DataCite, Zenodo/Figshare/GitHub release page |

## R Examples

Use R when the project is R-first.

```r
if (!requireNamespace("httr2", quietly = TRUE)) install.packages("httr2")
if (!requireNamespace("jsonlite", quietly = TRUE)) install.packages("jsonlite")

doi <- "10.1038/s41586-021-03819-2"
url <- paste0("https://api.crossref.org/works/", URLencode(doi, reserved = TRUE))
resp <- httr2::request(url) |>
  httr2::req_user_agent("citation-qc mailto:your_email@example.com") |>
  httr2::req_perform()
meta <- httr2::resp_body_json(resp)
item <- meta$message
data.frame(
  title = item$title[[1]],
  journal = item$`container-title`[[1]],
  year = item$issued$`date-parts`[[1]][[1]],
  doi = item$DOI,
  stringsAsFactors = FALSE
)
```

```r
pmids <- c("34265844")
url <- paste0(
  "https://eutils.ncbi.nlm.nih.gov/entrez/eutils/esummary.fcgi?",
  "db=pubmed&id=", paste(pmids, collapse = ","), "&retmode=json"
)
resp <- httr2::request(url) |> httr2::req_perform()
summary <- httr2::resp_body_json(resp)
```

## Shell Examples

```powershell
curl.exe -L "https://api.crossref.org/works/10.1038/s41586-021-03819-2"
curl.exe -L "https://eutils.ncbi.nlm.nih.gov/entrez/eutils/esummary.fcgi?db=pubmed&id=34265844&retmode=json"
```

## BibTeX Skeletons

```bibtex
@article{FirstAuthor2024Keyword,
  author  = {FirstAuthor, A. and SecondAuthor, B.},
  title   = {Article title},
  journal = {Journal Name},
  year    = {2024},
  volume  = {12},
  number  = {3},
  pages   = {123--134},
  doi     = {10.xxxx/yyyy}
}
```

```bibtex
@misc{FirstAuthor2024Preprint,
  author        = {FirstAuthor, A.},
  title         = {Preprint title},
  year          = {2024},
  eprint        = {2401.12345},
  archivePrefix = {arXiv},
  doi           = {10.xxxx/yyyy}
}
```

## Missing Metadata Handling

- DOI missing: search by exact title and first author in Crossref/OpenAlex/PubMed.
- Pages missing: check e-location ID; many journals use article numbers instead of pages.
- Volume/issue missing: check publisher page or Crossref `published-print` / `published-online`.
- Author list too long: preserve full author list in BibTeX unless the target style truncates during rendering.
- Title capitalization: protect biological names, methods, and proper nouns with braces only when needed.
