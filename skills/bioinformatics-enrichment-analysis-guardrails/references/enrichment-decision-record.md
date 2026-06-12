# Enrichment Decision Record

Use this compact record before promoting enrichment to a figure, table, or manuscript claim.

## Required Fields

| Field | Required content |
|---|---|
| Claim | The biological interpretation the enrichment is meant to support. |
| Input | Gene list, ranked table, expression matrix, module genes, or protein list. |
| Selection rule | Threshold, top N, module membership, score cutoff, or full ranking. |
| Universe | All genes/proteins that could have entered the input under the assay and upstream filter. |
| Coverage | Number and percent of input genes represented in the universe and library. |
| IDs | Organism, identifier type, mapping package/database, duplicate/unmapped handling. |
| Method | ORA, GSEA, GSVA/ssGSEA, marker scoring, or diagnostic annotation. |
| Libraries | GO/KEGG/Reactome/MSigDB/etc. with version or access date. |
| Statistics | Test, ranking statistic, permutations if any, FDR method, cutoff. |
| Display rule | How representative terms were selected and redundancy reduced. |
| Result judgment | Supports claim, weak support, diagnostic only, contradicted, or not interpretable. |
| Boundary | What cannot be concluded from this enrichment alone. |

## Reviewer Risks

- Wrong background universe inflates significance.
- Panel-restricted assays cannot support full-genome pathway claims.
- Short lists can be underpowered; very long lists lose specificity.
- Redundant GO terms can exaggerate breadth.
- Enrichment is not proof of causal mechanism, cell state, or signaling direction.
- Comparator modules must be analyzed under matched feature coverage before claiming superiority.
