# Dataset provenance and validation

## Source

- Dataset: **Hr Analytics Job Prediction**
- Publisher: **Faisal Qureshi**
- Source: https://www.kaggle.com/datasets/mfaisalqureshi/hr-analytics-and-job-prediction
- Repository file: `data/raw/HR_comma_sep.csv`
- Source filename: `HR_comma_sep.csv`
- Source checked: 2026-07-30
- Repository copy: unchanged

## License

Kaggle lists this dataset as **CC0 1.0 Universal — Public Domain**.

CC0 permits copying, modification, and redistribution without asking
permission. Attribution is not required by CC0, but the source is documented
here for provenance, transparency, and reproducibility.

This repository's licensing assessment is based on the license displayed by
Kaggle on the date above and is not legal advice. CC0 provides no warranty and
does not necessarily remove third-party privacy, publicity, patent, trademark,
or other rights.

## SHA-256

`af8c4cede39f28b5a67c748a66aa850fe260f908cbeaa226694121e0a9a4e105`

The notebook stops before analysis if the file does not match the expected
schema, dimensions, target counts, duplicate count, missing-value count, and
SHA-256 fingerprint.

## Validated raw contract

| Check | Expected |
|---|---:|
| Rows | 14,999 |
| Columns | 10 |
| Missing values | 0 |
| Exact duplicate rows | 3,008 |
| Stayed (`left = 0`) | 11,428 |
| Left (`left = 1`) | 3,571 |
| Departure rate | 23.8% |

## Analytical sample after exact-row deduplication

| Check | Observed |
|---|---:|
| Rows | 11,991 |
| Stayed | 10,000 |
| Left | 1,991 |
| Departure rate | 16.6% |

Because the dataset has no employee identifier or timestamp, exact duplicate
provenance cannot be verified. Removing exact duplicates is a documented
analytical assumption rather than a confirmed reconstruction of unique
employees.
