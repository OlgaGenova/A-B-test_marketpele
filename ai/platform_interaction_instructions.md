# Platform Interaction Analysis

Maintain the platform interaction analysis in:

`03_platform_interaction.ipynb`

Use the source dataset:

`csv/marketpele_ab_test_data_set.csv`

The source data are already aggregated at:

`date × publisher_id × platform × group_name`

The purpose of this analysis is to test whether treatment effects differ between Mobile and Desktop.

## Metrics

Analyze exactly these five metrics using the same definitions as in the existing analysis:

- RPM = `revenue / pageviews * 1000`
- RPS = `revenue / sessions * 1000`
- Paid CTR = `sponsord_clicks / visible_pageviews * 100`
- Organic CTR = `organic_clicks / visible_pageviews * 100`
- Pages per Session = `pageviews / sessions`

Calculate every metric as a **ratio of sums**, not as a mean of block-level ratios.

Do not change metric definitions.

For Paid CTR and Organic CTR, treatment effects and interactions are expressed in **percentage points**, not relative percentages.

## Data alignment

Align A/B rows within each existing:

`date × publisher_id × platform`

block using `pivot`.

Do not re-aggregate the already aggregated source data.

Each aligned platform block must preserve the A/B pairing.

## Cluster construction

Construct bootstrap clusters at:

`date × publisher_id`

When detecting whether a platform is available in a cluster, use:

`pageviews_A_{platform}`

Do not depend on column ordering such as `VALUE_COLUMNS[0]`.

A cluster may contain:

- both Mobile and Desktop;
- only Mobile;
- only Desktop.

If a platform is unavailable for a cluster, its metric input values may be zero-filled only after its absence has been explicitly identified and validated.

These zeros represent absence of the platform and must contribute zero to numerator and denominator sums.

## Bootstrap methodology

Use:

- bootstrap unit: `date × publisher_id`;
- `n_bootstrap = 10_000`;
- `seed = 42`;
- 95% percentile bootstrap confidence intervals.

Use one common cluster draw within each bootstrap iteration for:

- Mobile and Desktop;
- A and B;
- all five metrics.

Therefore:

- shared Mobile/Desktop clusters must remain together;
- Mobile and Desktop must NOT be resampled independently;
- A/B pairing must remain preserved;
- all available clusters must be used;
- do not restrict the analysis to only fully matched Mobile/Desktop clusters.

Protect against:

- zero denominators;
- non-finite denominators;
- non-finite metric values.

If a bootstrap draw contains an invalid denominator for any required metric/platform/group combination, reject that draw.

Track rejected draws as:

`n_rejected_bootstrap_draws`

Report the rejection count as a diagnostic and include it in the returned results.

Do not silently return `NaN` or infinite values.

## Interaction estimand

For each metric calculate:

`Mobile treatment effect = Metric_B_Mobile - Metric_A_Mobile`

`Desktop treatment effect = Metric_B_Desktop - Metric_A_Desktop`

and evaluate the platform interaction directly as:

`(B - A)_Mobile - (B - A)_Desktop`

The interaction is evaluated on the **absolute metric scale**.

Do not replace it with a difference in relative percentage uplifts.

Do not infer platform interaction from separate Mobile and Desktop significance results.

## Required Python output

For every metric return:

- Metric A Mobile
- Metric B Mobile
- Mobile treatment effect
- Metric A Desktop
- Metric B Desktop
- Desktop treatment effect
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

Do not include the full bootstrap distribution in human-readable outputs or JSON.

## Summary table

Create one compact DataFrame with one row per metric and columns:

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

## Output artifact

After the analysis completes successfully, save the compact scalar results to:

`outputs/platform_interaction_results.json`

The JSON must contain, for every metric:

- metric name;
- Mobile A;
- Mobile B;
- Mobile treatment effect;
- Desktop A;
- Desktop B;
- Desktop treatment effect;
- observed interaction;
- 95% bootstrap CI lower;
- 95% bootstrap CI upper;
- whether the CI crosses zero;
- number of Mobile blocks;
- number of Desktop blocks;
- number of bootstrap iterations;
- number of `date × publisher_id` clusters;
- number of rejected bootstrap draws.

Do not include `bootstrap_interaction` arrays in the JSON.

Do not modify any other files in `outputs/`.

## Validation

Before treating the analysis as complete:

- verify that the notebook executes successfully;
- verify that all five metrics are produced;
- verify that no non-finite metric values are returned;
- verify that rejected bootstrap draws are reported;
- verify that the interaction confidence interval is calculated directly from the bootstrap interaction distribution;
- compare the generated results with the existing validated notebook output and investigate any material discrepancy.

Do not change the statistical methodology merely to force results to match previous values.

## Interpretation

Interpret each platform interaction from its own bootstrap confidence interval.

If the confidence interval includes zero, state that the available data do not provide sufficient evidence that treatment effects differ between platforms for that metric.

If the confidence interval excludes zero, describe the direction of the observed platform heterogeneity.

Do not make causal claims about platform moderation.

Mobile and Desktop are not fully matched by `date × publisher_id`, so observed interactions may partly reflect differences in publisher/date composition.

Therefore, treat statistically supported platform differences as **exploratory evidence of heterogeneity**, not as clean causal estimates of platform moderation.

## Restrictions

Do not:

- add new statistical tests;
- change the bootstrap resampling unit;
- change the confidence interval method;
- change metric formulas;
- change `seed=42`;
- change `n_bootstrap=10_000`;
- add percentage-uplift interaction tests;
- introduce new segmentation dimensions;
- modify `01_overall_ab_test.ipynb`;
- modify `02_platform_diagnostics.ipynb`;
- modify existing AI reviewer files;
- modify any existing JSON output other than:
  `outputs/platform_interaction_results.json`.

When executing this instruction, only modify:

- `03_platform_interaction.ipynb`;
- `outputs/platform_interaction_results.json`.

Before making code changes, briefly confirm:

- the five metric definitions;
- bootstrap unit: `date × publisher_id`;
- one common cluster draw for Mobile and Desktop.