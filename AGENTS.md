# AI repository rules

## Scope and change control
- Keep analysis code as a modular, straight-line script. Do not add user-defined functions unless the user explicitly asks.
- Make the smallest change that fulfills the request. Do not refactor unrelated code or broaden edits across code blocks.
- Do not modify existing documents, notebooks, prompts, or figures without explicit user permission. Add or update a document only when the user specifically requests it.
- Do not commit source data, including the NAVCO workbook or raw/intermediate data files.

## Analysis and documentation
- Document assumptions about cleaning, campaign/year grouping, category coding, summary statistics, missing values, and the independence of observations.
- State each hypothesis, test type and tail, alpha, reported statistic, p-value, confidence interval method, and any multiple-comparison adjustment.
- Use pairwise Welch comparisons with Bonferroni adjustment when requested; explain adjusted p-values and confidence intervals.
- Do not add ANOVA comparisons or regression analyses unless the user explicitly requests them.
- Preserve descriptive labels for coded categories. Do not add significance stars without an explicitly requested test and stated threshold.

## Notebook and visual conventions
- Preserve the four notebook code sections: data upload/package installation, cleaning, analysis by year, and analysis by group.
- Keep notebook code aligned with the modular script when both are present. Pin package versions in the requirements file.
- Replace numeric and text -99 sentinels with missing values before analysis.
- Preserve the established restrained, colorblind-friendly palette, consistent group colors, right-side legends, white-circle mean markers, quartile lines, and readable jittered observations unless the user requests a change.
- Keep assumptions and code explanations in prose before each notebook section. Do not add helper functions to make the notebook less editable.
- Save newly generated figures and tables under a new versioned output directory named `output_<base-commit-short-sha>/`; preserve existing output directories as historical artifacts.

## Validation
- After code changes, check syntax and run the analysis script from the repository root with the pinned dependencies and required input file available. Confirm that expected figures are generated.
- Do not add or claim tests that were not run. For documentation-only changes, check links, paths, and consistency with the current analysis outputs.
