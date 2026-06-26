# Statistical Analysis Checklist

Use this reference when selecting tests, running statistical analysis, or writing methods/results.

## Test Selection

| Question | Outcome | Design | Typical method |
|---|---|---|---|
| two independent groups | continuous | independent | t-test/Welch test or linear model |
| two paired groups | continuous | paired | paired t-test or paired model |
| 3+ independent groups | continuous | independent | ANOVA/Welch ANOVA or linear model |
| non-normal ordinal/continuous | ranks | independent/paired | Mann-Whitney, Wilcoxon, Kruskal-Wallis, Friedman |
| categorical association | counts | independent | chi-square or Fisher exact |
| association | continuous-continuous | independent | Pearson/Spearman, regression |
| binary outcome | binary | independent/covariates | logistic regression |
| counts/rates | count | exposure/time | Poisson/negative binomial model |
| repeated/nested observations | any | clustered | mixed model or cluster-robust inference |
| time-to-event | survival | censored | Kaplan-Meier, Cox model |

When in doubt, model the design directly rather than forcing the data into a simple test.

## Assumptions And Diagnostics

Check as applicable:

- independence or modeled dependence;
- distribution/residual shape;
- variance homogeneity;
- linearity and link function;
- influential observations;
- missing-data mechanism;
- overdispersion for count data;
- proportional hazards for Cox models;
- spatial or temporal autocorrelation.

## Effect Sizes

Report effect sizes where possible:

- mean difference or standardized mean difference;
- odds ratio/risk ratio;
- correlation coefficient;
- regression coefficient;
- hazard ratio;
- enrichment odds ratio;
- difference in Moran's I or spatial coherence statistic;
- confidence interval or credible interval.

P-values alone are not enough for manuscript interpretation.

## Multiple Testing

Apply or justify correction when testing many genes, modules, pathways, regions, pairwise contrasts, thresholds, or spatial neighborhoods.

Common choices:

- Benjamini-Hochberg FDR for many related hypotheses;
- Bonferroni/Holm for small families where family-wise error matters;
- permutation-derived empirical p-values for non-standard statistics;
- hierarchical testing when primary endpoints are prespecified.

## Reporting Template

```text
We tested [question] using [test/model] because [outcome/design reason].
The independent unit was [unit], with [blocking/random effects/covariates] included for [reason].
Assumptions were assessed by [diagnostics].
P-values were adjusted by [method] across [family of tests].
Effect sizes are reported as [metric] with [CI/credible interval].
Analyses were performed in [software/package/version].
```

## Reviewer-Risk Checks

- Is the null model matched to the sampling design?
- Are cells/spots/images treated as independent when they are nested?
- Are threshold choices justified or sensitivity-tested?
- Are missing data and outliers handled before seeing desired significance?
- Does the statistical result support the biological wording, or only a proxy?
