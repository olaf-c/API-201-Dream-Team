# Digital lab notebook

Dates below use America/New_York. Entries are included only for days with repository or project changes; no entry is added for a day without changes.

## 2026-11-22
### Before the GitHub upload
- Built the analysis as a four-section notebook and matching modular Python script. Added prompt excerpts, code explanations, and explicit assumptions before each section; kept the analysis code free of user-defined functions.
- Pinned package versions and cleaned a local copy of the workbook by replacing numeric and text `-99` sentinels with missing values. The source workbook was kept out of the repository.
- Implemented and ran the requested analyses: separate success-group regressions with 95% confidence bands; the pre/through-1994 versus post-1994 Welch test; campaign-level ANOVAs for flank response, violent-flank status, and campaign size; and all pairwise Welch comparisons with Bonferroni adjustment.
- Generated the charts and pairwise-table image. Refined the editorial styling with colorblind-friendly group colors, right-side legends, quartile lines, white-circle means, and translucent jittered observations. Ran the script to confirm it completed and produced the figures.
- Prepared the notebook and eight PNG outputs for the repository, checking that source data was not included.

### GitHub upload
- Initialized the GitHub repository with its license, then uploaded the NAVCO fatality-analysis notebook and eight generated PNG outputs. The notebook records the analysis prompt, code assumptions, statistical comparisons, and chart outputs. No workbook/source data was committed.

## 2026-11-25
- Added `AGENTS.md` with repository-specific AI rules, this digital lab notebook, and `RESULTS_SUMMARY.md`.
- Moved the eight existing root-level PNGs into `output_17246b2/`. This folder name identifies the repository revision that held the images before this organizational change.
- No analysis code or source data was changed.
