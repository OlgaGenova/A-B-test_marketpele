# Final Experiment Review

## 1. Executive summary

The treatment improved all three monetization metrics overall: RPM increased by 15.51%, RPS by 10.47%, and Paid CTR by 22.14%. At the same time, both engagement guardrails deteriorated: Organic CTR decreased by 47.58% and Pages per Session by 4.36%. All five overall effects are statistically significant in the provided results.

The additional platform analysis shows that treatment effects differ between Mobile and Desktop for RPS, Paid CTR, and Organic CTR. It does not provide sufficient evidence of a platform difference for RPM or Pages per Session. The overall result therefore represents a meaningful monetization–engagement trade-off with material rollout risk.

## 2. Overall effects

Across 63 matched blocks, the treatment produced statistically significant changes in every metric:

- RPM increased by 0.2425, or 15.51%.
- RPS increased by 0.2881, or 10.47%.
- Paid CTR increased by 1.3330 percentage points, or 22.14%.
- Organic CTR decreased by 9.8253 percentage points, or 47.58%.
- Pages per Session decreased by 0.0767, or 4.36%.

The positive monetization effects are consistent with the treatment increasing paid engagement and revenue-related outcomes. The negative Organic CTR and Pages per Session results indicate broad deterioration in the engagement guardrails.

## 3. Platform diagnostics

### Platform-specific effects

The separate platform estimates show:

- RPM increased significantly on Mobile by 23.28%; Desktop increased by 4.62% but was not statistically significant.
- RPS increased significantly on Mobile by 18.79%; Desktop decreased by 1.16% but was not statistically significant.
- Paid CTR increased significantly on both Mobile (+26.85%) and Desktop (+15.64%).
- Organic CTR decreased significantly on both Mobile (−46.86%) and Desktop (−48.51%).
- Pages per Session decreased significantly on both Mobile (−3.64%) and Desktop (−5.52%).

These estimates describe effects within each platform. They do not, by themselves, establish that the effects differ between platforms.

### Direct interaction evidence

The direct interaction confidence intervals provide the appropriate comparison:

- RPM: interaction +0.2679, 95% CI [−0.0067, 0.5950]. The interval crosses zero; there is insufficient evidence of a platform difference.
- RPS: interaction +0.5155, 95% CI [0.0644, 1.0647]. The treatment effect is higher on Mobile.
- Paid CTR: interaction +0.9500 percentage points, 95% CI [0.3919, 1.5708]. The treatment effect is higher on Mobile.
- Organic CTR: interaction −1.0124 percentage points, 95% CI [−1.9773, −0.0465]. The negative treatment effect is stronger on Mobile.
- Pages per Session: interaction +0.0383, 95% CI [−0.0347, 0.1500]. The interval crosses zero; there is insufficient evidence of a platform difference.

## 4. Publisher diagnostics

Publisher results are descriptive only; statistical significance was not evaluated because the number of matched blocks per publisher is small.

RPM increased descriptively for all eight publishers, ranging from +0.67% for publisher 101 to +38.66% for publisher 700. RPS increased for five publishers and decreased for publishers 101, 111, and 373; publisher 700 had the largest descriptive increase at +32.75%. Paid CTR increased for seven publishers and was approximately unchanged for publisher 101 (−0.18%), with the largest increases for publishers 373 (+44.79%) and 259 (+39.18%).

Organic CTR decreased for every publisher, from −34.50% to −66.61%, with the largest decline for publisher 111. Pages per Session also decreased for every publisher, from −1.73% to −6.52%, with the largest decline for publisher 106.

The consistent guardrail deterioration across publishers is notable, while the variation in monetization effects indicates descriptive heterogeneity that is not sufficiently supported for publisher-specific decisions.

## 5. Monetization vs engagement trade-off

The experiment appears to improve monetization at the cost of engagement. RPM, RPS, and Paid CTR all improved significantly, while Organic CTR and Pages per Session both declined significantly. The Organic CTR decline is especially large in relative terms.

The platform results do not remove this concern: both platforms show deterioration in both engagement guardrails. The direct interaction results indicate that the Organic CTR loss is stronger on Mobile, while Pages per Session declines do not differ reliably by platform.

## 6. What the additional analysis changed

The earlier hypothesis that monetization effects vary by platform was partly supported, but it became more specific after direct testing. RPS shows supported Mobile-over-Desktop heterogeneity, whereas the apparent RPM difference from separate platform significance results is not confirmed by the direct interaction interval. Paid CTR improves on both platforms and also has a larger treatment effect on Mobile.

The earlier concern that engagement losses are broad rather than isolated to one platform remains supported. Direct testing adds that the Organic CTR decline is somewhat stronger on Mobile in absolute percentage-point terms. Pages per Session declines on both platforms, but the interaction test is inconclusive about a difference in effect size.

Publisher-level variation remains descriptive, and the available results do not establish whether larger monetization gains are systematically associated with larger engagement losses. Time stability is also not assessed by these inputs.

## 7. Key risks and limitations

- Mobile and Desktop are not fully matched by `date × publisher_id` in the interaction analysis.
- Observed platform interactions may partly reflect differences in publisher/date composition between the platform samples.
- Platform moderation findings are exploratory evidence of heterogeneity, not clean causal estimates of platform moderation.
- Publisher-level results use small numbers of matched blocks and are descriptive only; they should not be treated as statistically significant publisher effects.
- The analysis shows statistical evidence of the observed changes, but the provided inputs do not define acceptable business thresholds for the engagement guardrails.

## 8. Business recommendation

**Additional investigation**

Do not proceed directly to a full rollout.

The experiment shows statistically significant and sizeable improvements in the monetization metrics, but these gains coincide with statistically significant declines in both engagement guardrails. The available inputs do not define business thresholds that would establish whether the monetization gains are sufficient to justify those engagement losses.

The platform interaction analysis adds useful evidence of heterogeneity for RPS, Paid CTR, and Organic CTR, but it does not identify a platform segment where the monetization benefit is clearly achieved without engagement deterioration.

The next step should be to investigate alternative treatment variants that may retain part of the monetization benefit while reducing the engagement cost, and to define explicit guardrail thresholds before making a rollout decision.