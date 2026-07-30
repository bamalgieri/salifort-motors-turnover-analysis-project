# Executive Summary

**Reproduction status:** Fresh-kernel rerun passed with Python 3.13.5 on
2026-07-30.

## Objective

Analyze workforce patterns associated with employee departure in the Salifort
Motors educational HR dataset, compare several classification approaches, and
document the results with clear methodological and responsible-use
limitations.

## Data

The supplied CSV contained 14,999 rows, 10 columns, no missing values, and 3,008 exact duplicates. The raw departure rate was 23.8%. After exact-row deduplication, the analytic sample contained 11,991 rows and a 16.6% departure rate.

Because the dataset has no employee IDs or timestamps, duplicate provenance cannot be verified. The class-balance shift is therefore reported prominently rather than treated as a routine cleaning detail.

## Main descriptive findings

The strongest descriptive patterns were associated with:

- low satisfaction,
- very low or very high project counts,
- high monthly hours,
- the 4–5 year tenure window,
- and lower salary bands.

Department-level differences were present but smaller than the strongest workload, satisfaction, tenure, and salary patterns.

## Modeling

Seven model/feature-set combinations were compared using stratified 60/20/20 training, validation, and test splits. Preprocessing was fitted inside pipelines. Thresholds were selected on validation data by maximizing F2, and average precision was the primary ranking metric.

The top validation models were practically tied within 0.002 average-precision points. The selected model was **XGBoost — base** using the base source features because it remained inside the tie band while avoiding additional engineered assumptions.

## Held-out result

The validation-selected threshold was **0.265**.

| Metric | Test value |
|---|---:|
| Accuracy | 98.2% |
| Precision | 95.2% |
| Recall | 93.7% |
| F1 | 94.4% |
| F2 | 94.0% |
| ROC-AUC | 0.9839 |
| Average precision | 0.9679 |
| Brier score | 0.0146 |

The test confusion matrix contained 1982 true negatives, 19 false positives, 25 false negatives, and 373 true positives.

## Interpretation

The high performance reflects strong predictive structure in this educational dataset. It does not demonstrate production readiness or causal explanation. Missing timestamps, identifiers, role information, manager information, locations, and departure reasons limit both validity and responsible use.

## Recommended business actions

- Investigate extreme project loads and sustained high-hours patterns.
- Review the 4–6 year tenure window for career-progression friction.
- Compare compensation and promotion access within comparable roles.
- Use aggregate monitoring and employee feedback.
- Test supportive interventions prospectively.
- Do not automate adverse employment decisions or publish row-level risk scores.
