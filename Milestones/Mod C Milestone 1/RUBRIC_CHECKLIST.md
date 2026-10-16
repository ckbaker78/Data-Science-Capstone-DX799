# Milestone One rubric mapping

This is a coverage and verification record, not a predicted grade. Page numbers refer to the rendered final Word document.

| Criterion | Points | Evidence in report |
| --- | ---: | --- |
| Problem statement and description | 5 | Page 1 states project, stakeholder value, research questions, independent datasets, targets, and EDA consequences. |
| Conclusions depth | 30 | Pages 4–8 explicitly examine Weeks 5–6, kernels, penalties, grids, held-out results, pruning, forests, model limitations, and cutoff failures. Figures 3–6 support the discussion. |
| Conclusions breadth | 30 | Pages 2–3 cover polynomial/interactions, ridge/lasso/elastic net, forward/backward selection, PCR/PLSR, logistic regression/scaling. Pages 4–8 cover SVMs and trees/forests. Figures 1–2 reconcile the earlier weeks. |
| Overfitting | 10 | Training-only CV, fold-specific preprocessing, held-out validation, SVM controls, constrained tree designs, and quantitative training–validation gaps. Page 6/Figure 4 directly contrasts unrestricted and tuned trees. |
| Metrics and hyperparameter tuning | 5 | Pages 2–9 explain penalties, component/subset selection, C, gamma, tree depth, leaf size, pruning alpha, forest feature sampling, ranking versus decisions, RMSE, MAE, R², log loss, AUC, AP, and F1. |
| Expected and unexpected results | 5 | Small shrinkage gains and limited compression on pages 2–3; SVM ranking/cutoff failures on page 5; expected tree overfitting on page 6; dataset-dependent forest benefit and bank reversal on pages 7–9. |
| EDA | 5 | Page 1 explains skew, redundant predictors, status-linked missingness, bank date validity. Page 9 discusses VIF coding and permutation-importance limits. |
| AI appendix and citations | 5 | In-text author/date citations, references on page 10, explicit substantial AI assistance disclosure on page 12. External source discussion prepared but YellowDig participation remains a student action. |
| Communication | 5 | Consistent target definitions, units, within-dataset comparisons, six captioned body figures, and conclusions qualified by sample and provenance limits. |

## Format verification

- Summary: pages 1–10, including references. Appendix A begins on page 11; Appendix B begins on page 12.
- Word format: DOCX, Letter portrait, one-inch margins.
- Styles: 12-point Times New Roman with double spacing; figure-containing paragraphs use normal image placement. Captions are 12-point Times New Roman and double spaced.
- Figure count: six numbered body figures, including two tables. No page has more than one numbered figure. Images are 6.5 inches wide and 2.7–3.0 inches high.
- No substantive figures are relegated to an appendix.
- Appendix A supplies the full GitHub repository URL, six clickable notebook links, and accompanying notebook files.
- Final DOCX was rendered with the packaged document renderer. The PDF confirms actual Times New Roman font embedding. Every page was visually inspected; unchanged page images were matched by hash after final revisions. A chart legend collision and long appendix URL overflow were repaired before final delivery.
- All six saved notebook snapshots were checked against their SHA-256 hashes, with 172 executed code cells and zero saved errors. Saved values, not newly rerun models, support the report.

## Limits and pending action

- YellowDig sharing and discussion cannot be completed or verified through the local files; prepared text is provided in Appendix B.
- Course AI policy was not supplied. The substantial AI contribution is disclosed for the author to review against that policy.
- No course submission or external posting was performed. The project’s missing target-timing documentation, resolved-only LendingClub cohort, possible borrower dependence, repeated historical comparisons, and tiny bank sample remain substantive limitations.
