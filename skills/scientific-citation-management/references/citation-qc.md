# Citation QC

Use this reference before manuscript submission or when cleaning a reference library.

## QC Checklist

```text
Artifact checked:
Reference format:
Total bibliography entries:
Total in-text citation keys:
Entries with DOI/PMID/PMCID/arXiv:
Entries missing required fields:
Duplicate DOI/PMID/title groups:
Cited but missing from bibliography:
Bibliography entries not cited:
Broken DOI/URL:
Preprints with published versions:
Dataset/software citations with version:
Remaining warnings:
```

## Manuscript Citation Checks

For Markdown or LaTeX manuscripts:

- Extract citation keys from patterns such as `[@key]`, `@key`, `\cite{key}`, `\citep{key}`, and `\citet{key}`.
- Compare against BibTeX keys.
- Report missing keys and unused bibliography entries separately.
- If citation rendering produced `[?]`, `??`, or `citation needed`, treat it as blocking.

## Duplicate Detection

Use a tiered rule:

1. Same DOI after lowercase normalization.
2. Same PMID/PMCID.
3. Same arXiv/bioRxiv ID.
4. Same normalized title plus first author plus year.

When duplicates differ in metadata, keep the published version over the preprint unless the manuscript specifically cites the preprint. Preserve dataset/software records separately from article records even when titles are similar.

## Severity

- `blocking`: unresolved citation, missing bibliography entry for a cited key, invalid DOI for a central reference, fabricated or untraceable source.
- `major`: missing required article fields, duplicate cited entries, preprint cited when published article is intended.
- `minor`: style inconsistency, optional field missing, capitalization issue.

## Final Report Template

```text
Citation QC result:
- Checked:
- Passed:
- Blocking issues:
- Major issues:
- Minor warnings:
- Files changed:
- Remaining manual checks:
```
