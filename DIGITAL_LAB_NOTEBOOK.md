# Digital lab notebook

Dates below use America/New_York and follow the dated activity in the chat log. Entries appear only for days with project or repository changes.

## 2026-11-20
- Started the NAVCO fatality-analysis deliverables using the supplied workbook and codebook.
- Created the analysis notebook, matching modular Python script, and repository archive. Added data loading, cleaning, requested group comparisons, and initial charts; ran the analysis to produce outputs.

## 2026-11-21
- Revised the saved notebook and script in response to the analysis and visualization requests, then refreshed the repository archive.
- Reviewed the editorial chart direction and palette using the supplied visual references.

## 2026-11-22
- Before upload, organized the notebook into four code sections and added the relevant prompt excerpts, code explanations, and explicit assumptions. Kept the script modular and without user-defined functions.
- Pinned package versions and replaced numeric and text `-99` sentinels with missing values in a cleaned copy of the workbook; retained the original locally and excluded source data from GitHub.
- Implemented and ran the requested analyses: separate success-group regressions with 95% confidence bands; the pre/through-1994 versus post-1994 Welch test; campaign-level ANOVAs for flank response, violent-flank status, and campaign size; and pairwise Welch comparisons with Bonferroni adjustment.
- Generated the charts and pairwise-table image. Refined the editorial styling with colorblind-friendly group colors, right-side legends, quartile lines, white-circle means, and translucent jittered points. Confirmed the script completed and produced the figures.
- Prepared the notebook and eight PNG outputs for upload, checking that the workbook/source data was not included.
- Initialized the GitHub repository with its license and uploaded the NAVCO fatality-analysis notebook and eight generated PNG outputs. No source workbook or raw data was committed.

## 2026-11-25
- Added `AGENTS.md` with repository-specific AI rules, this digital lab notebook, and `RESULTS_SUMMARY.md`.
- Moved the eight PNGs from the repository root into `output_17246b2/`. This folder name identifies the repository revision that held the images before this organizational change.
- No analysis code or source data was changed.
