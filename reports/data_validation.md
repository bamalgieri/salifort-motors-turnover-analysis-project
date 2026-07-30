# Data Validation Report

**Reproduction status:** Fresh-kernel rerun passed with Python 3.13.5 on
2026-07-30.

## Source file

- Repository path: `data/raw/HR_comma_sep.csv`
- Upstream dataset: `Hr Analytics Job Prediction`
- Publisher: Faisal Qureshi
- Source: https://www.kaggle.com/datasets/mfaisalqureshi/hr-analytics-and-job-prediction
- License displayed by source: CC0 1.0 — Public Domain
- Repository copy: unchanged
- SHA-256: `af8c4cede39f28b5a67c748a66aa850fe260f908cbeaa226694121e0a9a4e105`
- Validation date: 2026-07-30

## Raw contract results

| Check | Expected | Observed | Result |
|---|---:|---:|---|
| Rows | 14,999 | 14,999 | Pass |
| Columns | 10 | 10 | Pass |
| Missing values | 0 | 0 | Pass |
| Exact duplicate rows | 3,008 | 3,008 | Pass |
| Stayed | 11,428 | 11,428 | Pass |
| Left | 3,571 | 3,571 | Pass |
| Departure rate | 23.8% | 23.8% | Pass |
| SHA-256 | `af8c4cede39f28b5a67c748a66aa850fe260f908cbeaa226694121e0a9a4e105` | `af8c4cede39f28b5a67c748a66aa850fe260f908cbeaa226694121e0a9a4e105` | Pass |

## Column validation

The source columns matched the required legacy schema exactly:

```text
satisfaction_level
last_evaluation
number_project
average_montly_hours
time_spend_company
Work_accident
left
promotion_last_5years
Department
salary
```

The analysis renames legacy columns internally:

| Raw column | Analysis column |
|---|---|
| `number_project` | `number_projects` |
| `average_montly_hours` | `average_monthly_hours` |
| `time_spend_company` | `tenure` |
| `Work_accident` | `work_accident` |
| `Department` | `department` |

## Duplicate-impact analysis

| Stage | Rows | Stayed | Left | Departure rate | Change from raw |
|---|---:|---:|---:|---:|---:|
| Raw | 14,999 | 11,428 | 3,571 | 23.8% | 0.0 percentage points |
| After exact-row deduplication | 11,991 | 10,000 | 1,991 | 16.6% | -7.2 percentage points |

Exact-row deduplication removes 3,008 rows, or approximately 20.1% of the raw data. It reduces the observed positive-class rate materially, so model metrics and descriptive findings are explicitly tied to the deduplicated analytic sample.

## Provenance limitation

The dataset contains no employee identifier or timestamp. Therefore:

- repeated records cannot be linked to a known person,
- legitimate repeated employee states cannot be distinguished from extraction duplicates,
- temporal ordering cannot be verified,
- and exact duplicate provenance cannot be proven.

Removing exact duplicates is a documented analytic assumption, not a confirmed reconstruction of unique employees.

## Execution evidence

The final notebook reran sequentially in a fresh kernel with:

- a Linux execution environment,
- 22 code cells,
- execution counts 1 through 22,
- zero error outputs,
- zero traceback streams,
- strict raw-data assertions,
- and regenerated model metadata and seven image files.

The validated raw CSV is committed unchanged so the analysis can be
reproduced directly from a fresh clone. Dataset provenance and licensing are
documented in `data/raw/README.md`.
