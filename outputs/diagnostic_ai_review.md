### 1. Platform findings

- RPM increased significantly on Mobile by 23.28%, while the Desktop increase of 4.62% was not significant.
- RPS increased significantly on Mobile by 18.79%, while Desktop showed a non-significant decrease of 1.16%.
- Paid CTR increased significantly on both Mobile and Desktop: +26.85% and +15.64%, respectively.
- Organic CTR decreased significantly on both platforms: −46.86% on Mobile and −48.51% on Desktop.
- Pages per Session decreased significantly on both platforms: −3.64% on Mobile and −5.52% on Desktop.

The platform pattern is heterogeneous for RPM and RPS, but broadly consistent for Paid CTR and the engagement guardrails. Differences between platform effect sizes were not themselves tested in the provided results.

### 2. Monetization diagnostics

The RPM and RPS results indicate that the overall monetization uplift is concentrated primarily in Mobile: both metrics show significant increases on Mobile, whereas neither Desktop result is significant.

Paid CTR is different: it increased significantly on both platforms. The relative increase is larger on Mobile (+26.85%) than on Desktop (+15.64%), but the provided diagnostics do not establish that this difference is statistically significant.

Therefore, the monetization pattern is not uniformly platform-wide. Mobile is the main contributor to the RPM and RPS pattern, while Paid CTR improvement is present across both platforms.

### 3. Guardrail diagnostics

Engagement deterioration is consistent across platforms:

- Organic CTR decreased significantly by 46.86% on Mobile and 48.51% on Desktop.
- Pages per Session decreased significantly by 3.64% on Mobile and 5.52% on Desktop.

The Organic CTR decline is therefore not concentrated in only one platform. Pages per Session declined more on Desktop descriptively, but no formal comparison of the platform effect sizes is provided.

### 4. Publisher heterogeneity

Publisher-level results are descriptive only; statistical significance was not evaluated because the number of matched blocks per publisher is small. They should not be used to make publisher-specific rollout decisions.

Notable descriptive patterns include:

- RPM increased for all eight publishers, ranging from +0.67% to +38.66%. The largest increase was observed for publisher 700; publisher 101 showed almost no change.
- RPS increased for five publishers and decreased for three. The decreases were observed for publishers 101, 111, and 373, while publisher 700 had the largest descriptive increase (+32.75%).
- Paid CTR increased for seven publishers and was approximately unchanged for publisher 101 (−0.18%). The largest descriptive increases were for publishers 373 (+44.79%) and 259 (+39.18%).
- Organic CTR decreased for every publisher, ranging from −34.50% to −66.61%. The largest descriptive declines were for publishers 111 and 700.
- Pages per Session decreased for every publisher, ranging from −1.73% to −6.52%. The largest descriptive decline was for publisher 106.

The consistent direction of guardrail deterioration across publishers is notable, while the variation in monetization changes suggests possible publisher-level heterogeneity that requires stronger evidence.

### 5. Hypotheses to investigate

- Hypothesis: the treatment interacts differently with Mobile traffic, producing stronger RPM and RPS gains there than on Desktop. The diagnostics show the pattern but do not establish why it occurs.
- Hypothesis: Paid CTR can improve across platforms even where aggregate revenue-per-session or revenue-per-pageview gains are not confirmed on Desktop.
- Hypothesis: publisher context may influence the size of monetization gains, given the wide descriptive range in RPM, RPS, and Paid CTR changes.
- Hypothesis: the treatment creates a broad engagement cost because Organic CTR and Pages per Session decline across both platforms and all publishers in the descriptive results.
- Hypothesis: the largest publisher-level monetization gains may be associated with larger engagement losses, but this relationship has not been tested by the provided diagnostics.

These are hypotheses, not established explanations.

### 6. Recommended next analyses

- Conduct a formal platform-by-treatment interaction analysis. This would test whether the Mobile and Desktop treatment effects truly differ, rather than relying on separate significance results.
- Decompose RPM and RPS by platform into their underlying revenue and traffic/session components. This would identify which components account for the stronger Mobile monetization result.
- Analyze the relationship between publisher-level monetization changes and guardrail changes descriptively, with appropriate caution about the small number of blocks. This would test whether larger monetization gains tend to coincide with larger engagement losses.
- Extend the matched-block analysis by date and platform. This would test whether the Mobile monetization uplift and cross-platform guardrail declines are stable over time.
- Investigate publisher-level results with a method that pools information across blocks or uses shrinkage/partial pooling. This would provide more reliable estimates of heterogeneity than the current descriptive ratios.

### 7. Diagnostic conclusion

The diagnostics refine the overall A/B-test result. They indicate that the RPM and RPS uplift is mainly associated with Mobile, while Paid CTR improves on both platforms. In contrast, Organic CTR and Pages per Session deteriorate consistently across Mobile and Desktop, and the same adverse direction is visible descriptively across all publishers.

Thus, the diagnostic evidence does not remove the engagement concern from the overall experiment. It suggests that further investigation should focus on the Mobile monetization pattern, formal platform interaction testing, and whether a less aggressive treatment could preserve monetization gains while reducing the broad guardrail deterioration.
