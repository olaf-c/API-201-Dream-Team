# NAVCO fatality analysis: results summary

**Analysis revision:** `17246b2` (the repository snapshot whose notebook and figures were organized under `output_17246b2/`).  
**Interpretive threshold:** α = 0.05.

## Prompt summary

The notebook analyzes NAVCO campaign fatality estimates. It replaces `-99` missing-value codes, plots log-adjusted peak fatalities over year by final campaign success with separate linear regressions and 95% confidence bands, compares 1994 or earlier with post-1994 campaign-years using a two-tailed mean test, summarizes fatalities by campaign-level flank-response/status/campaign-size groups with one-way ANOVAs, and reports pairwise Welch tests with Bonferroni adjustment.

## Data and assumptions

The workbook contains 2,717 campaign-year rows across 384 campaign IDs. Numeric and text `-99` are treated as missing; 907 campaign-year rows have no `fatalities_high` after cleaning. Analyses exclude records missing the variables they require.

The year comparison uses campaign-year rows and raw `fatalities_high` values; 1994 is in the first period and post-1994 begins in 1995. Its Welch t-test allows unequal variances but treats rows as independent even though a campaign can appear in multiple years.

For the group analysis, observed annual fatality estimates are averaged within campaign ID. Each campaign is assigned the modal valid code for each grouping variable; ties are assigned to the lowest code. ANOVAs use campaign-level average raw fatalities. Pairwise comparisons are two-sided Welch t-tests on the raw scale, with Bonferroni adjustment applied separately within each factor family. The plots use `log1p` of the fatality measure; these log-scale plots do not change the test scale.

## Tests explained (intro statistics)

### Welch two-sample t-test

A two-sample t-test asks whether the population means of two groups differ. Here, the null hypothesis is that the earlier and later periods have the same mean raw fatality estimate: H0: μ_before − μ_after = 0. The two-tailed alternative allows the difference to go in either direction.

The test starts with the observed difference between sample means and divides it by its estimated standard error. That gives a t-statistic: a difference that is large relative to its standard error produces a larger absolute t-statistic. Welch's version calculates the standard error from each group's own sample variance and sample size, so it does not require the two groups to have equal variances. It also uses an adjusted degrees-of-freedom calculation.

The p-value is the probability, assuming H0 and the test's assumptions are true, of getting a t-statistic at least as far from zero as the one observed. It is not the probability that H0 is true. Because this is a two-tailed test, unusually large positive and negative differences both count as evidence against H0. A small p-value such as one below 0.05 leads us to reject H0; a larger p-value means we fail to reject it, not that we have proved the means equal.

Welch's test still assumes independent observations within and across the two groups. It accommodates unequal variances, but it does not correct for repeated campaign-year observations from the same campaign. Fatality counts are also highly skewed, which makes the raw-scale means sensitive to a few very large values.

### One-way ANOVA

A one-way analysis of variance (ANOVA) tests whether the population means are the same across three or more groups. For each factor here, H0 says that all category means in that factor are equal. For example, the flank-response ANOVA compares the mean campaign-level fatality estimate across the observed flank-response categories.

ANOVA forms an F-statistic by comparing how far the group means are spread apart with how much observations vary within groups. If the group means are far apart relative to the within-group variation, F tends to be larger and the p-value smaller. A significant omnibus result supports the conclusion that at least one group mean differs; it does not say which groups differ or that every group differs.

The classical one-way ANOVA assumes independent observations, roughly normal outcomes within groups, and similar variances across groups. Here, campaigns are the analysis units after aggregation, but the fatality averages remain skewed and group sizes differ, so the ANOVA findings are best treated as exploratory. The pairwise comparisons use Welch tests to allow unequal variances. Bonferroni adjustment multiplies each p-value by the number of comparisons in that factor family (capped at 1), reducing false-positive risk when many pairs are tested.

## Results by analysis

### Fatality trends by year and final success

Separate linear regressions of `log1p(fatalities_high)` on year show negative slopes for both final outcome groups:

| Final campaign outcome | Slope (log points/year) | R² | Regression p-value |
|---|---:|---:|---:|
| Not successful | -0.0346 | 0.0422 | 1.47e-17 |
| Successful | -0.0738 | 0.1127 | 0.0001564 |

Both estimated slopes are statistically different from zero at the 0.05 level; the plotted confidence bands describe uncertainty around the fitted mean trend. The small R² values show that year alone explains little of the variation in log fatality estimates. These are descriptive associations, not causal effects. Repeated observations within campaigns may also make ordinary regression p-values too optimistic if within-campaign dependence is not modeled.

### Fatalities before/through 1994 versus after 1994

| Period | Campaign-year n | Mean raw fatalities |
|---|---:|---:|
| 1994 or before | 937 | 7,406.175 |
| After 1994 | 873 | 510.937 |

The difference (before minus after) is 6,895.238 fatalities. The specified two-tailed Welch test of H0: mean(before) - mean(after) = 0 gives *t* = 2.0353, df = 936.53, *p* = 0.0421008. At α = 0.05, reject the null: the observed mean is higher in the earlier period. In intro-statistics terms, if the two period means were truly equal, a t-statistic at least this far from zero would be uncommon under the test model. The p-value does not measure the probability that the null is true. Because fatality counts are highly skewed and campaign-years are repeated within campaigns, the result should be read cautiously; Welch's test addresses unequal variances, not dependence between repeated campaign-years. The box and violin figures show `log1p` values for shape and spread, while the test compares raw-scale means.

### Campaign-level one-way ANOVAs

The null for each test is equality of average raw fatality estimates across all observed categories in that grouping.

| Grouping | Campaigns | F | p-value | Decision at α = 0.05 |
|---|---:|---:|---:|---|
| Flank response | 146 | 4.737 | 0.00351974 | Reject equal-means null (**). At least one category mean differs. |
| Violent-flank status | 348 | 0.759 | 0.468882 | Fail to reject; no evidence of an overall mean difference. |
| Campaign size | 342 | 1.311 | 0.258601 | Fail to reject; no evidence of an overall mean difference. |

The flank-response result means the observed spread among category means is large relative to within-category variation under the equal-means model. It is evidence that at least one mean differs, not proof that all flank-response groups differ. The two other tests do not provide enough evidence to reject equal means; that is not proof that their population means are exactly equal.

The individual pairwise tests do not show any contrast surviving Bonferroni adjustment at 0.05. The stars in the notebook mark the omnibus ANOVA threshold only: `*` p < .05, `**` p < .01, `***` p < .001, and `ns` p ≥ .05. A star is not an effect-size or causal claim.

### Focused comparison: no violent flank versus violent flank

For the focused codes 1 (no violent flank) and 2 (violent flank), the campaign-level raw means are 66.176 and 209.023, respectively. The corresponding unadjusted two-sided Welch comparison has *p* = 0.039656, but its Bonferroni-adjusted *p* = 0.118967. Thus, this contrast does not meet the 0.05 threshold after adjustment. The focused violin figure is descriptive; the primary violent-flank ANOVA also includes code 0 (primarily violent campaign).

### Pairwise comparisons

The notebook reports 24 pairwise two-sided Welch comparisons across the three factors. Each row includes the first group's raw mean, the raw mean difference (first minus second), the unadjusted p-value, and Bonferroni-adjusted p-value within that factor. No pairwise comparison has an adjusted p-value below 0.05. A few unadjusted comparisons are below 0.05; interpreting those alone would ignore the multiple comparisons. The adjustment is like requiring stronger evidence for each individual comparison when several opportunities to find a low p-value are being considered.

## Limitations

These comparisons are observational. The tests rely on campaign-level independence for ANOVA and Welch pairwise comparisons; fatality distributions are strongly skewed and group sizes differ. The year test instead uses repeated campaign-year rows and may understate uncertainty. The logarithm is used for visualization, not to redefine the raw-scale null hypotheses. Interpret p-values alongside group sizes, means, the plotted distributions, and the stated aggregation rules.
