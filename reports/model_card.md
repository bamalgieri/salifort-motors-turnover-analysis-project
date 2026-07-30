# Model Card: Salifort Motors Turnover Classifier

**Reproduction status:** Fresh-kernel rerun passed with Python 3.13.5 on
2026-07-30.

## Model overview

- Champion: **XGBoost — base**
- Feature set: **Base**
- Threshold: **0.265**
- Selection metric: Validation average precision
- Threshold objective: Validation F2
- Practical-tie tolerance: 0.002 average-precision points
- Binary model file included: No
- Metadata file: `models/salifort_turnover_model_metadata.json`

## Intended use

This model accompanies a public analytical case study demonstrating:

- reproducible classification workflow design,
- imbalanced-class evaluation,
- validation-based threshold selection,
- practical-tie reasoning,
- interpretability and calibration checks,
- and responsible communication in an HR-style use case.

Appropriate use is limited to aggregate investigation and methodological
review within this case study.

## Non-intended use

The model must not be used to:

- automate adverse employment decisions,
- rank or discipline individual employees,
- infer causal reasons for departure,
- replace employee feedback or HR review,
- claim protected-class fairness,
- or forecast future real-world turnover without new validation.

## Training data

The raw dataset contained 14,999 rows. After removing 3,008 exact duplicates, 11,991 rows remained.

- Training: 7,194 rows, 16.6% departure rate
- Validation: 2,398 rows, 16.6% departure rate
- Test: 2,399 rows, 16.6% departure rate

The split was stratified and reproducible with random state 42.

## Base predictors

- `satisfaction_level`
- `last_evaluation`
- `number_projects`
- `average_monthly_hours`
- `tenure`
- `work_accident`
- `promotion_last_5years`
- `department`
- `salary`

`salary_numeric` is not used. Salary appears exactly once as a categorical predictor.

## Model comparison and tie policy

Validation average precision:

| Model | Feature set | Average precision | F2 | Threshold |
|---|---|---:|---:|---:|
| XGBoost — engineered | engineered | 0.9710 | 0.9394 | 0.460 |
| XGBoost — base | base | 0.9698 | 0.9369 | 0.265 |
| Random forest — engineered | engineered | 0.9692 | 0.9350 | 0.370 |

The three models were within 0.002 average-precision points of the validation leader. The base XGBoost model was selected to reduce engineered assumptions while retaining essentially equivalent ranking performance.

## Held-out test metrics

| Metric | Estimate | 95% bootstrap interval |
|---|---:|---:|
| Precision | 0.9515 | 0.9306–0.9711 |
| Recall | 0.9372 | 0.9119–0.9579 |
| F1 | 0.9443 | 0.9280–0.9593 |
| F2 | 0.9400 | 0.9180–0.9582 |
| ROC-AUC | 0.9839 | 0.9754–0.9911 |
| Average precision | 0.9679 | 0.9535–0.9789 |
| Brier score | 0.0146 | 0.0107–0.0190 |

Confusion matrix:

| | Predicted stayed | Predicted left |
|---|---:|---:|
| Actual stayed | 1982 | 19 |
| Actual left | 25 | 373 |

## Interpretability

Top source-feature permutation importance:

1. `satisfaction_level` — 0.3722
2. `tenure` — 0.1149
3. `number_projects` — 0.0618
4. `average_monthly_hours` — 0.0392
5. `last_evaluation` — 0.0346

Permutation importance describes dependence of this fitted model's test performance on each feature. It is not a causal effect estimate.

## Limitations

- Educational, simplified dataset.
- No employee ID or timestamp.
- Duplicate provenance cannot be confirmed.
- No future-period validation.
- No manager, role level, location, or departure reason.
- Voluntary and involuntary exits are combined.
- Satisfaction and evaluation timing may be target-adjacent.
- Protected-class fairness cannot be evaluated.
- Random splitting may overstate future operational performance.

## Ethical safeguards

- Keep public outputs aggregate-only.
- Require human review for any internal use.
- Do not expose individual probabilities broadly.
- Do not use the model for discipline, termination, promotion denial, or compensation decisions.
- Pair any risk analysis with employee feedback and prospective policy testing.
