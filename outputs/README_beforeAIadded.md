# A/B Test Analysis — Marketpele Feed Ranking

This analysis evaluates an experiment that changed the order of paid and organic elements in a content feed.

- **Group A**: organic content shown before paid elements
- **Group B**: paid elements moved higher in the feed

The goal was to check whether the new layout increases monetization without causing unacceptable deterioration in user engagement.

## Report

**[View the full A/B test report](./AB_test_Marketpele_Olga_Genova.pdf)**

## Project structure

```text
.
├── 01_overall_ab_test.ipynb
├── 02_platform_diagnostics.ipynb
├── AB_test_Marketpele_Olga_Genova.pdf
├── csv/
└── svg/
```

## Data source

The dataset comes from an A/B experiment conducted on the **Marketpele Feed** platform, which helps publishers monetize their content through advertising.

The feed contains:

* **Paid elements** — advertisements that generate revenue when users click through to the advertiser’s page
* **Organic elements** — publisher content that redirects users to another article from the same publisher

The dataset contains aggregated experiment results for comparing different ordering strategies for paid and organic content.

## Metrics

The analysis focuses on ratio metrics:

- **RPM** — revenue per 1,000 pageviews
- **RPS** — revenue per 1,000 sessions
- **Visible Paid CTR** — paid clicks / visible pageviews
- **Visible Organic CTR** — organic clicks / visible pageviews
- **Pages per Session** — pageviews / sessions

## Methodology

The data is aggregated by:

```text
date × publisher_id × platform × group_name
```

Because A and B observations are matched by date, publisher and platform, the main analysis uses a **paired Poisson bootstrap** for ratio metrics.

Additional diagnostics were performed by:

- platform: `Mobile` vs `Desktop`
- publisher_id: descriptive comparison only, without statistical significance testing

## Key findings

Group B significantly improves monetization-related metrics overall:

- RPM increased
- RPS increased
- Visible Paid CTR increased

However, guardrail metrics deteriorated:

- Visible Organic CTR decreased significantly
- Pages per Session decreased significantly

Platform diagnostics show that monetization uplift is mainly driven by **Mobile**. On Desktop, RPM and RPS growth is not statistically confirmed, although Paid CTR increases.

Publisher-level diagnostics show heterogeneous effects across publishers. Since each publisher has only a small number of matched blocks, this part is used as descriptive diagnostics rather than statistical testing.

## Business conclusion

Version B improves paid engagement and monetization, but it also reduces organic engagement and session depth.

A full rollout of such an aggressive layout change is risky. A better next step would be to test a softer ranking strategy, for example placing fewer paid elements above organic content.

## Tools used

- Python
- pandas
- NumPy
- matplotlib
- seaborn
- Jupyter Notebook
- paired Poisson bootstrap



AI diagnostic → hypothesis about platform heterogeneity
→ AI-generated implementation
→ methodological review
→ corrected cluster bootstrap
→ validated interaction analysis