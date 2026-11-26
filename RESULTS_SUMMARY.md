# NAVCO fatality analysis: results summary

**Analysis revision:** `ba65064` (new figures are saved under `output_ba65064/`).  
**Interpretive threshold:** α = 0.05.

## Prompt summary

The notebook cleans the NAVCO fatality data by replacing `-99` with missing values. It displays annual mean log-adjusted peak fatality estimates by final campaign success with confidence intervals, compares 1994 or earlier with after 1994 using a two-tailed test of raw means, and summarizes campaign-level outcomes across flank-response, violent-flank, and campaign-size categories. It also reports pairwise mean comparisons with confidence intervals and Bonferroni-adjusted p-values.

No linear regression over time or ANOVA comparisons are run.

## Data and assumptions

The workbook contains 2,717 campaign-year rows across 384 campaign IDs. Numeric and text `-99` are treated as missing; 907 campaign-year rows have no `fatalities_high` after cleaning. Each analysis excludes records missing its required outcome or grouping variable.

The year comparison uses campaign-year rows and raw `fatalities_high` values; 1994 is in the first period and post-1994 begins in 1995. It uses a two-sided Welch t-test at α = 0.05. The test treats campaign-year rows as independent, although a campaign can appear in multiple years.

For the group analysis, observed annual fatality estimates are averaged within campaign ID, so each campaign contributes one outcome. Each campaign is assigned the mode of its valid category codes for each grouping variable; ties are assigned to the lowest code. Pairwise comparisons use two-sided Welch t-tests on the campaign-level raw mean fatalities. Bonferroni adjustment is applied separately within each grouping factor's family of pairwise comparisons. The distributions in the plots use `log1p(fatalities_high)`; this transformation is for visualization and does not change the raw-scale tests.

## Results by analysis

### Annual estimates by year and final success

The line chart shows each year's mean of `log1p(fatalities_high)` separately for campaigns marked successful and not successful, with 95% bootstrap confidence intervals. There is no fitted regression or slope test. These annual estimates are descriptive: they show how the observed group means vary over time, while the interval width reflects uncertainty in each annual mean. Years with few observations can have wide intervals and sharp changes; the chart does not establish a causal effect or a long-term trend.

### Fatalities before/through 1994 versus after 1994

| Period | Campaign-year n | Mean raw fatalities |
|---|---:|---:|
| 1994 or before | 937 | 7,406.175 |
| After 1994 | 873 | 510.937 |

The difference (before minus after) is 6,895.238 fatalities. The two-tailed Welch test of H0: mean(before) − mean(after) = 0 gives *t* = 2.0353, df = 936.53, *p* = 0.0421008. At α = 0.05, reject the null hypothesis: the observed earlier-period mean is higher.

### Welch tests, explained for an introductory statistics course

A two-sample t-test asks whether the population averages in two groups differ. The null hypothesis here says the mean fatality estimate is the same in both periods. The observed difference in sample means is compared with its standard error: if the difference is large relative to the amount of sampling variation, the resulting t-statistic is farther from zero and the p-value tends to be smaller.

Welch's t-test is designed for two groups that may have different variances or sample sizes. It estimates each group's variance separately and uses an adjusted degrees-of-freedom calculation. A two-tailed p-value accounts for differences in either direction. A p-value of about 0.042 means that, if the null and test assumptions were true, a t-statistic this far from zero or farther would occur about 4.2% of the time. It is not the probability that the null is true. Since 0.042 is below 0.05, the test rejects the null at the chosen threshold.

Welch's test accommodates unequal variances, but it does not account for multiple yearly observations from the same campaign. The raw fatality distribution is also strongly skewed, making means sensitive to unusually large observations. The result should be interpreted with those limits in mind.

### Campaign-level pairwise comparisons

The notebook reports 24 pairwise two-tailed Welch comparisons across the flank-response, violent-flank, and campaign-size groupings. Each comparison includes the first group's mean raw fatalities, the mean difference (first minus second), a 95% Welch confidence interval for that difference, an unadjusted p-value, and a Bonferroni-adjusted p-value.

None of the pairwise comparisons has an adjusted p-value below 0.05. Thus, after accounting for the multiple comparisons within each factor, the results do not provide sufficient evidence to conclude that any particular pair of category means differs. This does not prove the means are equal.

Bonferroni adjustment controls the increased chance of a false positive when many comparisons are made by multiplying each p-value by the number of comparisons in that factor family, with adjusted values capped at 1. The confidence-interval charts plot the raw mean difference and its 95% Welch interval; a zero reference line represents no mean difference. Intervals crossing zero are compatible with no difference at the 95% level.

For the focused comparison of code 1 (no violent flank) versus code 2 (violent flank), campaign-level raw means are 66.176 and 209.023. The unadjusted two-sided Welch p-value is 0.039656, while the Bonferroni-adjusted p-value is 0.118967. This pair does not meet the 0.05 threshold after adjustment. The broader violent-flank grouping also includes code 0 (primarily violent campaign).

## Interpretation limits

These are observational comparisons, not causal estimates. Campaign-level aggregation produces one outcome per ID for the group comparisons, but the campaign average remains skewed and category sizes differ. The year test uses repeated campaign-year rows and may understate uncertainty if observations within a campaign are correlated. Log adjustment is used for plots, while the hypothesis tests compare means on the raw fatality scale. Read p-values alongside sample sizes, mean differences, confidence intervals, and the grouping assumptions above.
