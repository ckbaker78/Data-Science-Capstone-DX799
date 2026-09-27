# DX799: all datasets in every weekly notebook

Each notebook retains the original assignment instructions and now contains three
independent dataset analyses. Each analysis has its own target definition, data
checks, split, fitted models, comparisons, diagnostics, and conclusions. Common
helper functions reuse code only; fitted preprocessing and models are never
shared between datasets. Every notebook ends with a combined results table and
conclusions that keep the different outcomes and units explicit.

| Notebook | Methods repeated for **each** dataset |
| --- | --- |
| [Week 1](Week%201.ipynb) | Continuous/categorical features; additive, polynomial, and interaction regression; multicollinearity/VIF; residual diagnostics |
| [Week 2](Week%202.ipynb) | OLS, ridge, lasso, elastic net; training-fold scaling; penalty tuning; shrinkage and coefficient paths |
| [Week 3](Week%203.ipynb) | Forward/backward group selection; PCR; PLSR; component selection; comparison with full OLS |
| [Week 4](Week%204.ipynb) | Logistic regression; unscaled/standard/min–max/robust scaling; regularization; threshold selection; ROC, precision–recall, calibration, and confusion matrices |

## Dataset-specific questions

| Dataset | Weeks 1–3 response | Week 4 response | Scope |
| --- | --- | --- | --- |
| `accepted_2007_to_2018Q4.csv` | Issued interest rate (%) | Charged Off versus Fully Paid | Regression: a uniform sample of 24,000 eligible 2015 originations. Classification: a separate uniform sample of resolved 2015, 36-month loans. |
| `Loan_Default.csv` | Observed positive interest rate (%) | Recorded `Status = 1` | Regression samples up to 24,000 records with observed valid rates. Classification uses the original full status dataset and a conservative predictor set. |
| `bank_customers.csv` | Historical account tenure in years | Checking versus savings/CD | 39 date-valid records; account IDs stay together across partitions and CV folds. |

The bank outcomes are defined from observed account fields, **not invented loan
outcomes**. Tenure is calculated from AccountOpened at the explicit reference date
2026-09-26; opening date is excluded from regression predictors. Checking status
is derived from AccountType; AccountType is excluded from classification
predictors. Age/account type predict tenure; age/tenure predict checking status.

Dates after the reference date, invalid or partial birth dates, account openings
before birth, and missing/unrecognized account types are excluded. Reasons can
overlap, and each notebook reconciles the eligible subset with the original 100
rows. No SSNs are loaded, and customer/account identifiers are not displayed or
used as numeric features. Repeated account IDs are conservative grouping keys.
No joins between the unrelated CSV files are assumed.

## Reproduce the analyses

The completed notebooks use Python 3.13.5. Install the recorded package versions:

```bash
python3 -m pip install -r requirements-notebooks.txt
```

Select that Python environment in the notebook editor and use **Restart Kernel →
Run All**. Start from this repository or its parent workspace. Keep these original
files available locally:

```text
DATA/accepted_2007_to_2018Q4.csv
DATA/Loan_Default.csv
DATA/bank_customers.csv
```

Each notebook is independent and reads all three CSVs. The large LendingClub file
is streamed in chunks, and random-priority sampling scans the entire file instead
of taking its first ordered rows. Weeks 1–3 reuse the same per-dataset samples and
partitions for comparison. The seed is 42. The original CSVs are unchanged.

For command-line execution, repeat this command with each week's filename:

```bash
python3 -m jupyter nbconvert --execute --to notebook --inplace --ExecutePreprocessor.timeout=1200 "Week 1.ipynb"
```

Saved markdown conclusions describe the executed inputs and settings. When
changing either, rerun all code and revise the narrative to match the new results.

## How to interpret the results

- Interest-rate errors are **percentage points**, whereas bank-tenure errors are
  **years**. Classification targets are also different. Scores are not a ranking
  of which dataset or business process is inherently better.
- Loan_Default pricing is missing for nearly every Status 1 record. The regression
  therefore describes a selected observed-rate population. Its status definition
  and observation window are not documented; Week 4 does not claim validated
  future-default probabilities.
- LendingClub classification conditions on resolved outcomes. Ongoing/other
  statuses are counted and excluded, never assumed to be fully paid. A historical
  random split does not establish future-year performance.
- The bank split has 24 training, 7 validation, and 8 test records, with differing
  class mixes. Its negative regression R² values and classification AUC of 0.50
  are retained. These are small-sample method demonstrations, not reliable
  population performance estimates. OLS can produce negative tenure predictions;
  their counts are reported without silently clipping them.
- Week 4 retains an encoder warning for a validation home-ownership category
  absent from training. It receives an all-zero indicator block, sharing the
  reference-category encoding; rare-category performance is not established.
- Selection, imputation, scaling, and component transforms are fitted within the
  appropriate training partitions. Independent validation chooses model families
  and thresholds; test results are not used to select another model.
- The analyses are observational. They do not establish causal effects, fairness,
  borrower independence, or operational readiness.

## Verification

All four expanded notebooks were executed from fresh kernels: 104 code cells and
35 saved figures. Notebook format, original instruction preservation, coverage of
all three datasets, final conclusions, and absence of exposed SSNs are checked.
Figures are inspected for readable labels, units, and legends; duplicate figures
are matched by their image hashes.

The earlier full browser layout review was interrupted when the preview browser
became unavailable. Full-page browser review remains incomplete; the numerical
execution, saved figure review, and markdown structure checks are separate from
that limitation. To review the complete layout locally, open the notebooks in the
IDE or export each to HTML:

```bash
python3 -m jupyter nbconvert --to html "Week 1.ipynb"
```

The Milestone One rubric/link mentioned in the assignment text was not supplied.
The named weekly methods are covered; a final grade cannot be guaranteed.
