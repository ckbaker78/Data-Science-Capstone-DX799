# Comparative financial modeling: a recruiter review guide

**Calvin Baker · Boston University DX799 · Academic modeling studies**

[Rendered regression case](https://calvin-baker-data-science.netlify.app/projects/regression-and-regularization/) · [Repository](https://github.com/ckbaker78/Data-Science-Capstone-DX799)

## Question and contribution

How much model complexity is useful once validation, data quality and an independent test set are considered? I configured regression, regularization, subset/component selection, logistic models, SVM kernels and tree ensembles, keeping each dataset's target, preprocessing and evaluation separate.

## Read by method

| Study | Notebook | What to inspect |
| --- | --- | --- |
| Regression | [Regression notebook](https://github.com/ckbaker78/Data-Science-Capstone-DX799/blob/main/Week%201.ipynb) | Polynomial/interaction terms, baseline comparison, residual diagnostics |
| Regularization | [Ridge, lasso and elastic net](https://github.com/ckbaker78/Data-Science-Capstone-DX799/blob/main/Week%202.ipynb) | Training-fold preprocessing, CV, coefficient paths, bootstrap comparison |
| Feature selection | [Selection, PCR and PLSR](https://github.com/ckbaker78/Data-Science-Capstone-DX799/blob/main/Week%203.ipynb) | Group selection and component tuning; cases where compression is not helpful |
| Probability modeling | [Logistic regression](https://github.com/ckbaker78/Data-Science-Capstone-DX799/blob/main/Week%204.ipynb) | Scaling, C selection, calibration, PR/ROC and threshold tradeoffs |
| Kernel models | [SVM comparison](https://github.com/ckbaker78/Data-Science-Capstone-DX799/blob/main/Week%205.ipynb) | Kernel/C/gamma choices and training-to-validation overfit |
| Tree ensembles | [Trees and forests](https://github.com/ckbaker78/Data-Science-Capstone-DX799/blob/main/Week%206.ipynb) | Depth/leaf/pruning constraints, forests and matched logistic benchmarks |

Original notebook filenames remain unchanged so existing citations keep working.

## Selected saved results

- LendingClub pricing: selected regression test RMSE **3.064 percentage points** versus **4.299 pp** for a mean-only baseline, a **28.7%** reduction; test n=4,800.
- Lasso retains **26/27** expanded terms and essentially matches OLS test error. The paired-bootstrap MAE-difference interval includes zero.
- Feature selection retains **11/12** original predictor groups. PCR selects all **24** encoded components; PLSR selects **12**.
- Logistic study: LendingClub test ROC AUC **0.674**, log loss **0.387** versus a **0.410** baseline. Its procedure differs from the later SVM/ensemble comparison.
- SVM study: LendingClub RBF training/validation AUC **0.857/0.525**, illustrating overfit.
- Matched tree/ensemble study: Loan_Default forest test AUC **0.646** versus fixed-logistic **0.591**; LendingClub forest/logistic both round to **0.633**.

These are separate study-specific results, not a single leaderboard.

## Reproduction

The existing repository README provides full target definitions and sampling details. Saved outputs can be reviewed without executing the notebooks. For execution, use the repository's recorded Python **3.13.5** environment and pinned `requirements-notebooks.txt`:

```bash
git clone https://github.com/ckbaker78/Data-Science-Capstone-DX799.git
cd Data-Science-Capstone-DX799
python3 -m venv .venv
source .venv/bin/activate
python -m pip install -r requirements-notebooks.txt
```

Keep the original inputs locally under `DATA/`: `accepted_2007_to_2018Q4.csv`, `Loan_Default.csv`, and `bank_customers.csv`. The large original files are required for execution; saved notebook outputs do not require them. Open a notebook, select the environment, restart the kernel and run all cells. Seed 42 is used. Large-file scans, CV and SVM searches can be expensive. Do not substitute a different dataset while presenting the saved results as unchanged.

## Limits

Historical random splits do not establish future-cohort performance. Loan_Default's status definition/window is undocumented. The bank exercise has only 39 date-valid records and is a methods demonstration. Pricing errors are percentage points, not default accuracy; AUC is ranking quality, not a selected operating rule. The portfolio update does not rerun model training or claim client deployment.

---

## Original course and reproduction documentation

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
| [Week 5](Week%205.ipynb) | Linear, degree-two polynomial and RBF support vector machines; kernel geometry; C/gamma tuning; support vectors; threshold trade-offs |
| [Week 6](Week%206.ipynb) | Decision trees; depth/leaf/pruning regularization; random forests; tree visualization; held-out permutation importance |

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


## Weeks 5 and 6: matched classification experiments

Both new notebooks analyze **all three datasets** independently and retain Week
4's target definitions and conservative predictor sets. Each is self-contained.
To make exact kernel SVM cross-validation practical, both use the same uniform
12,000-row sample of Loan_Default and the same random-priority 12,000-row sample
of eligible resolved 2015 36-month LendingClub loans. They scan the full source
when constructing the LendingClub sample. All 39 eligible bank records are kept.
The loan splits contain 7,200 training, 2,400 validation and 2,400 test records;
bank account groups remain separated across partitions and CV folds.

These sampling choices differ from Week 4. Compare Week 5 and Week 6 methods on
their matched populations; do not attribute Week 4 versus Week 5 score changes
solely to the model family. The new notebooks use full one-hot encoding for
categories, which avoids arbitrary reference-level distances for SVM kernels.

Three-fold training CV tunes parameters by ROC AUC; independent validation AUC
selects the family. Validation F1 selects an illustrative operating cutoff. The
training-fitted model is frozen without a development refit, preserving the score
scale used for threshold selection. Test metrics are reported for prespecified
models without selecting another winner. SVM scores are margins, not calibrated
probabilities. Both weeks include fixed-C logistic and prevalence baselines,
ranking and decision metrics, confusion counts, and conditional bootstrap AUC
intervals for loan samples. No reliable bank population interval is claimed.

Week 5 also includes an explicitly exploratory training/validation-only balanced-class
penalty check, added after the initial run. It does not replace the original
selection or reuse test outcomes to evaluate another candidate.

The saved interpretations are generated from executed results. Top summaries
record the delivered run; if changing data or settings, regenerate those static
summaries as well as running all cells. The new notebooks retain the original
weekly instructions and the missing-rubric limitation. No submission or external
publication is performed.


### Weeks 5–6 verification

Both notebooks were executed top to bottom from fresh kernels: **68 code cells
and 39 saved figures**, with saved tables,
figures, computed interpretations and data-specific conclusions. Input source and
split code is matched across the two notebooks. Execution and notebook structure
are checked separately from the plots. Saved figures are visually reviewed and
long titles/dense diagnostics were revised for readability. HTML previews were
exported; the browser tool reported that both in-app and Chrome browsers were
unavailable, so full browser layout inspection could not be completed. Open the
notebooks in the IDE to review the complete interactive notebook layout.


## Weeks 8 and 9: neighbors and gradient boosting

[Week 8: K-Nearest Neighbors](Week%208.ipynb) and
[Week 9: Gradient boosting](Week%209.ipynb) each analyze all three datasets
independently. Loading, cohort construction, seed-42 sampling, predictors and
partitions match Week 6: 12,000 rows per loan dataset (7,200 train / 2,400
validation / 2,400 test), and 39 eligible bank records (24 / 7 / 8), with bank
account groups separated across partitions and CV folds. The bank reference date
remains September 26, 2026 for comparability.

- **Week 8:** Manhattan and Euclidean distance, training-fold numeric scaling,
  full one-hot encoding, k selection, uniform/distance votes, a controlled fixed-k
  scaling comparison and validation-to-training neighborhood distances.
- **Week 9:** gradient boosting with binary log loss; learning rate, estimator
  count and tree depth; paired leaf-size/subsampling regularization profiles;
  stage-wise training/validation loss; validation permutation importance.
  The two regularization profiles change leaf size and subsampling together,
  so their individual effects cannot be separated.

Training CV tunes parameters by ROC AUC. Week 8 validation AUC selects the
distance family; Week 9 has one prespecified boosting family. Validation F1
selects each illustrative cutoff. Models remain frozen at their training fits;
test results do not select another model. Both notebooks include fixed-C logistic
and training-prevalence baselines, ranking/decision metrics, log loss, Brier score,
confusion counts and conditional bootstrap AUC intervals for the loan samples.
The stage-wise plots are diagnostic and do not retune the selected tree count.

| Dataset | Week 8 model | Week 8 test AUC | Week 9 test AUC | Matched logistic AUC |
| --- | --- | ---: | ---: | ---: |
| Loan_Default | Euclidean KNN | 0.609 | 0.647 | 0.591 |
| LendingClub resolved 2015 36-month loans | Euclidean KNN | 0.620 | 0.635 | 0.633 |
| Bank checking-account demonstration | Manhattan KNN | 0.333 | 0.333 | 0.583 |

These are descriptive results, not significance claims or a test-selected
leaderboard. Scaling improved fixed-k Loan_Default CV AUC (0.561 to 0.581), but
reduced LendingClub CV AUC (0.608 to 0.594). Stage-wise loss curves illustrate
that training improvement can accompany validation deterioration. Bank estimates
are unstable and do not support population or credit-risk conclusions.

Both notebooks ran top to bottom from fresh kernels: **68 code cells and 42
saved figures**, with no runtime errors. Notebook structure, matched data/split
code, confusion-count totals and reported F1 values were checked. All saved
figures were visually reviewed; HTML previews were generated, and the Week 8
summary and chart placement were inspected in Safari. A complete Week 9 browser
layout review was not completed because the user resumed activity in Safari;
its saved figures were reviewed separately. Review previews are local under
`../.analysis-work/weeks8-9/`.

Use the existing pinned requirements and reproduction command with `Week 8.ipynb`
or `Week 9.ipynb`. Each notebook includes source links, computed takeaways,
method-specific interpretations and Milestone Two synthesis notes. Static
summaries describe this saved run and should be revised if settings change.
The Milestone Two rubric was not included with the supplied assignment text.
Week 9 is prepared for **9.3 Peer Review: Week 9 Jupyter Notebook**; no course
submission or external publication was performed.
