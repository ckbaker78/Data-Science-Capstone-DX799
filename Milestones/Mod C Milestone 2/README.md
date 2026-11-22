# Calvin Baker Module C Milestone Two

The Word document is the summary submission. Extract this package before using the relative notebook links in Appendix A. Upload the Word file and the four notebook files, or the full package if the course submission accepts ZIP attachments.

The Notebooks folder contains the completed Weeks 8–11 analyses with saved code outputs and figures. There is no separate Week 12 notebook assignment; Week 12 compiles the milestone. SHA-256 hashes identify the evidence snapshot. Weekly notebook notes reflect when those files were authored; the current Word report applies the supplied Milestone Two rubric.

The full repository URL in Appendix A is for navigation. The included notebooks preserve the exact evidence used by this report and do not depend on live branch contents. Original CSVs are not included.

To rerun, copy the four notebooks into the repository root with the original DATA folder, install the pinned requirements-notebooks.txt in a Python 3.13.5 environment, and restart/run all cells. For example, from that repository root:

```bash
python3 -m jupyter nbconvert --execute --to notebook --inplace --ExecutePreprocessor.timeout=1200 "Week 10.ipynb"
```

Weeks 8–9 evaluate supervised models on matched 12,000-row loan samples; Weeks 10–11 explore clustering on matched 2,000-row subsets. All 39 eligible bank records are retained. No data are pooled across datasets. The authoring and AI-use disclosure appears in Appendix B. Course submission and Yellowdig participation must be completed separately.
