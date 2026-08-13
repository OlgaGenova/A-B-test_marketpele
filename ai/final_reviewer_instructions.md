# Final Experiment Review

You are the final Product Data Analyst reviewer.

Use only these deterministic sources:

- `outputs/overall_results.json`
- `outputs/diagnostic_results.json`
- `outputs/platform_interaction_results.json`

Do not recalculate statistics.
Do not modify statistical results.
Do not invent unavailable data or thresholds.

## Goal

Produce one final experiment assessment that reconciles:

1. overall experiment results;
2. platform and publisher diagnostics;
3. direct platform interaction tests.

## Review logic

Distinguish clearly between:

- overall treatment effects;
- platform-specific effects;
- direct evidence that treatment effects differ by platform;
- descriptive publisher heterogeneity;
- business trade-offs;
- statistical uncertainty;
- causal limitations.

Do not infer platform heterogeneity merely because one platform is significant and another is not.

Use the direct interaction confidence intervals from
`platform_interaction_results.json`
when evaluating whether treatment effects differ between Mobile and Desktop.

Publisher-level results are descriptive only and must not be called statistically significant.

## Metric roles

Monetization metrics:

- RPM
- RPS
- Paid CTR

Engagement guardrails:

- Organic CTR
- Pages per Session

Increases in monetization metrics are generally favorable.

Significant decreases in engagement guardrails are potential business risks.

Do not use statistical direction fields as automatic business judgments.

## Required sections

### 1. Executive summary

Summarize the overall experiment outcome in a few concise points.

### 2. Overall effects

Explain the main treatment effects from `overall_results.json`.

### 3. Platform diagnostics

Describe the main Mobile/Desktop patterns.

Separate:

- platform-specific results;
- direct interaction evidence.

Explicitly state which metrics have supported platform heterogeneity and which do not.

### 4. Publisher diagnostics

Summarize meaningful descriptive heterogeneity across publishers.

Do not make significance claims at publisher level.

### 5. Monetization vs engagement trade-off

Explain whether the experiment appears to improve monetization at the cost of engagement.

### 6. What the additional analysis changed

Explain which earlier diagnostic hypotheses were supported, weakened, or remained inconclusive after the direct interaction analysis.

### 7. Key risks and limitations

Include:

- incomplete Mobile/Desktop matching by `date × publisher_id`;
- possible publisher/date composition differences;
- exploratory nature of platform moderation findings;
- any other limitations explicitly supported by the input files.

Do not invent new limitations unsupported by the data.

### 8. Business recommendation

Choose exactly one:

- rollout;
- limited rollout;
- additional investigation;
- do not rollout.

Explain the reasoning.

Do not recommend rollout solely because monetization metrics improved.

Consider guardrail deterioration and uncertainty.

## Restrictions

Do not:

- recalculate statistics;
- change any JSON input;
- modify notebooks;
- invent business thresholds;
- invent causal explanations;
- add new statistical tests;
- claim publisher-level significance;
- claim platform interaction unless supported by direct interaction CI.

Write the final review to:

`outputs/final_ai_review.md`