# Platform Interaction Analysis

Generalize and maintain the platform interaction analysis in:

`03_platform_interaction.ipynb`

Do not rewrite the notebook from scratch.

The source data are already aggregated at:

`date × publisher_id × platform × group_name`

The purpose of this notebook is to test whether treatment effects differ between Mobile and Desktop for the experiment metrics.

## Core methodology

Preserve the following methodology:

- A/B values are aligned within each available `date × publisher_id × platform` block;
- the bootstrap resampling unit is `date × publisher_id`;
- one common cluster draw is reused for Mobile and Desktop within each bootstrap iteration;
- when a sampled cluster contains both Mobile and Desktop, both platform blocks must be included together;
- when a sampled cluster contains only one platform, only the available platform contributes;
- Mobile and Desktop must NOT be resampled independently;
- A/B pairing must remain preserved;
- all available data must be used;
- do not restrict the main analysis to only fully matched Mobile/Desktop clusters;
- ratio metrics must be calculated as ratio of sums, not as means of block-level ratios.

The interaction must be evaluated directly as:

`(B - A)_Mobile - (B - A)_Desktop`

Do not infer platform interaction from separate Mobile and Desktop significance results.

## Metrics

Run the interaction analysis for exactly these five metrics:

1. RPM
2. RPS
3. Paid CTR
4. Organic CTR
5. Pages per Session

Use the same metric definitions as in the existing analysis notebooks.

Do not invent or change metric formulas.

Use the following configurations:

- RPM = `revenue / pageviews * 1000`
- RPS = `revenue / sessions * 1000`
- Paid CTR = `sponsord_clicks / visible_pageviews * 100`
- Organic CTR = `organic_clicks / visible_pageviews * 100`
- Pages per Session = `pageviews / sessions`

For each metric, calculate the value as a ratio of sums within the bootstrap sample.

## Platform-block alignment

Align the existing A/B rows using `pivot`, not a new aggregation step.

Do not re-aggregate the already aggregated source data.

The aligned block level must remain:

`date × publisher_id × platform`

## Cluster construction

Construct bootstrap clusters at:

`date × publisher_id`

When detecting whether a platform is present in a cluster, use an explicit stable column:

`pageviews_A_{platform}`

Do not use an implicit expression such as `VALUE_COLUMNS[0]`, because its value depends on column ordering.

Missing values for an unavailable platform may be zero-filled only after platform presence has been explicitly identified and validated.

The zero-filled values must represent absence of that platform from the cluster and must contribute zero to both numerator and denominator sums.

## Bootstrap implementation

Use:

- `n_bootstrap = 10_000`
- `seed = 42`
- 95% percentile bootstrap confidence intervals

Reuse one common bootstrap draw of `date × publisher_id` clusters for:

- both platforms;
- both experiment groups;
- all five metrics.

This common draw must preserve the existing dependence for clusters where Mobile and Desktop are both available.

Add protection against:

- zero denominators;
- non-finite denominators;
- non-finite metric values.

Do not silently return `NaN` or infinite values.

If a generated bootstrap draw has an invalid denominator for any required metric/platform/group combination, reject that draw.

Track the total number of rejected bootstrap draws in:

`n_rejected_bootstrap_draws`

Report this diagnostic clearly after the bootstrap finishes and include it in the returned metadata/results.

The rejection count is diagnostic only. Do not alter the statistical interpretation based on it unless the number of rejected draws is unexpectedly large.

Do not keep unused intermediate variables such as `bootstrap_effects` if they are not referenced by the implementation.

## Primary estimand

For each metric, calculate:

### Mobile treatment effect

`Metric_B_Mobile - Metric_A_Mobile`

### Desktop treatment effect

`Metric_B_Desktop - Metric_A_Desktop`

### Platform interaction

`Mobile treatment effect - Desktop treatment effect`

The primary interaction is evaluated on the absolute metric scale.

Do not replace this with a difference in relative percentage uplifts.

Relative percentage changes may be reported separately as descriptive information, but they must not replace the primary interaction estimand.

For Paid CTR and Organic CTR, because the multiplier is `100`, absolute treatment effects and interaction estimates are expressed in **percentage points**, not relative percentages.

## Required output

For every metric return:

- Metric A Mobile
- Metric B Mobile
- Mobile treatment effect `(B - A)`
- Metric A Desktop
- Metric B Desktop
- Desktop treatment effect `(B - A)`
- observed interaction
- 95% bootstrap CI lower
- 95% bootstrap CI upper
- whether the CI crosses zero
- number of Mobile blocks
- number of Desktop blocks
- number of bootstrap iterations
- number of `date × publisher_id` clusters
- number of rejected bootstrap draws

Keep the full bootstrap interaction distribution available in the returned Python object as:

`bootstrap_interaction`

Do not include the full distribution in the human-readable summary table.

## Summary table

Create one compact DataFrame with one row per metric and the following columns:

- Metric
- Mobile A
- Mobile B
- Mobile effect
- Desktop A
- Desktop B
- Desktop effect
- Interaction
- CI lower
- CI upper
- CI crosses zero

## Validation

The generalized implementation must reproduce the previously validated RPM result approximately:

- RPM A Mobile ≈ `1.485335`
- RPM B Mobile ≈ `1.831176`
- Mobile treatment effect ≈ `0.345842`
- RPM A Desktop ≈ `1.688332`
- RPM B Desktop ≈ `1.766317`
- Desktop treatment effect ≈ `0.077985`
- observed interaction ≈ `0.267856`
- 95% CI approximately `[-0.0067, 0.5950]`

Small Monte Carlo differences are acceptable.

If the RPM result changes materially, stop and investigate the implementation instead of continuing.

## Interpretation

Interpret interaction directly from its bootstrap confidence interval.

Do not use separate platform significance results as evidence that platform effects differ.

The current validated results should be interpreted as follows:

- RPS shows evidence of a stronger positive treatment effect on Mobile than on Desktop;
- Paid CTR shows evidence of a stronger positive treatment effect on Mobile than on Desktop;
- Organic CTR shows evidence of a stronger negative treatment effect on Mobile than on Desktop;
- RPM does not provide sufficient evidence of a platform difference because the interaction CI includes zero;
- Pages per Session does not provide sufficient evidence of a platform difference because the interaction CI includes zero.

For Paid CTR and Organic CTR, report treatment effects and interactions in percentage points.

Do not make causal claims.

Mobile and Desktop are not fully matched by `date × publisher_id`, so observed interactions may partly reflect publisher/date composition differences between the platform samples.

Therefore, treat the results as exploratory evidence of platform heterogeneity for some metrics, not as clean causal estimates of platform moderation.

## Restrictions

Do not:

- add new statistical tests;
- change the bootstrap resampling unit;
- resample Mobile and Desktop independently;
- change the confidence interval method;
- change metric formulas;
- change `seed=42`;
- change `n_bootstrap=10_000`;
- add percentage-uplift interaction tests;
- introduce new segmentation dimensions;
- modify `01_overall_ab_test.ipynb`;
- modify `02_platform_diagnostics.ipynb`;
- modify existing JSON outputs;
- modify existing AI reviewer files.

Only modify `03_platform_interaction.ipynb` when executing this instruction.

Before making code changes, briefly explain the planned implementation and confirm the metric configuration and bootstrap resampling unit.