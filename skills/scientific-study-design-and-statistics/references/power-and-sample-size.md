# Power And Sample Size

Use this reference when planning sample size, minimum detectable effect, or simulation-based power.

## Core Inputs

```text
Primary endpoint:
Planned test/model:
Independent unit:
Effect size basis:
Alpha:
Target power:
Allocation ratio:
Dropout/unusable rate:
Clustering/ICC:
Multiplicity adjustment:
Power method: closed-form | simulation
```

## Effect Size Choice

Use, in order:

1. Smallest effect size of interest: the effect that would matter scientifically, clinically, or methodologically.
2. Prior or pilot estimate, shrunk or sensitivity-tested because pilot effects are often inflated.
3. Conventional small/medium/large benchmarks only as last resort.

Always report sensitivity across a plausible range when the effect size is uncertain.

## Closed-Form R Examples

```r
if (!requireNamespace("pwr", quietly = TRUE)) install.packages("pwr")

# Two-sample t-test, Cohen's d = 0.5
pwr::pwr.t.test(d = 0.5, power = 0.8, sig.level = 0.05,
                type = "two.sample", alternative = "two.sided")

# One-way ANOVA, Cohen's f = 0.25, 4 groups
pwr::pwr.anova.test(k = 4, f = 0.25, power = 0.8, sig.level = 0.05)

# Correlation, r = 0.3
pwr::pwr.r.test(r = 0.3, power = 0.8, sig.level = 0.05)
```

## Simulation-Based Power Pattern

Use simulation when the planned analysis is a GLM, mixed model, spatial statistic, cluster design, repeated measures, survival model, or custom null.

```r
simulate_power <- function(n, nsim = 2000, alpha = 0.05, seed = 1) {
  set.seed(seed)
  hits <- logical(nsim)
  for (i in seq_len(nsim)) {
    # 1. simulate data under assumed effect
    # 2. fit the planned model/test
    # 3. set hits[i] <- p_value < alpha
  }
  p <- mean(hits)
  se <- sqrt(p * (1 - p) / nsim)
  data.frame(power = p, ci_low = p - 1.96 * se, ci_high = p + 1.96 * se)
}
```

Use at least 1,000 simulations for rough planning and 5,000-10,000 when the result will be reported or is near the decision boundary.

## Adjustments

- Dropout: `n_enroll = ceiling(n_analyzed / (1 - dropout_rate))`.
- Cluster design effect: `DEFF = 1 + (m - 1) * ICC`.
- Multiple testing: power at adjusted alpha or simulate the whole testing procedure.
- Unequal allocation: include allocation ratio.

## Guardrails

- Do not report observed power computed from the observed effect after the study.
- Do not power on cell count when the independent unit is patient/sample/FOV.
- Do not present one sample-size number without assumptions.
- Do not ignore effect-size uncertainty.
