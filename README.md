# Ketamine clinic survey — analysis repository

Quarto (+ R) documents for analysing multi-rater survey data on ketamine clinics (binary items across clinics and raters). Run analyses from this directory so relative paths (`./data/...`) resolve correctly.

## Pre-rendered HTML (self-contained)

This repository includes **`inter_rater_reliability.html`** and **`regularized_models.html`**, produced with Quarto’s self-contained option so each file bundles styles, scripts, and the rendered content. If you **download** one of these files (or clone the repo) and **open it in a web browser**, you can review the full report offline: **all tables and figures appear as generated from the data used in that render**, without running R or Quarto.

## Included analysis documents

### `inter_rater_reliability.qmd`

Inter-rater reliability (IRR) for four raters: pairwise Cohen’s kappa, three-rater subsets with Fleiss’s kappa, and grouped (e.g., by instrument family, clinic). Includes data preparation for the IRR tables and descriptive summaries. This is the first stage of the analytic workflow described here.

Rendered output: `inter_rater_reliability.html` (self-contained; see above).

### `regularized_models.qmd`

Second stage: descriptive **Table 1**–style summaries and penalized regression (cross-validated LASSO by AUC) plus robust Poisson-regression contrasts for the telehealth outcome, using filtered data for one rater. Conceptually follows the IRR work in `inter_rater_reliability.qmd`.

Rendered output: `regularized_models.html` (self-contained; see above).

## Data files (`data/`)

| File | Role |
|------|------|
| `ketamine data all rater .xlsx` | Primary multi-rater spreadsheet: clinic names, `rater` id, timestamps and **disagreement** columns stripped in code; used for IRR and reshaping logic in `inter_rater_reliability.qmd`. |
| `KETAMINE_updated.xlsx` | Derived/updated workbook with the same broad layout; used where the IRR document builds majority-rule (`data_d`) and single-rater (`data_3`) analytic sets, and by `regularized_models.qmd` (rater `3` corresponds to **rater column value 3**, documented in the notebook as **rater 4** in plain language). |

Place both spreadsheets under `data/` as shown. If `KETAMINE_updated.xlsx` is absent, chunks that depend on it will fail at render time.

## Suggested rendering

From R or the terminal (with Quarto installed):

```sh
quarto render inter_rater_reliability.qmd
quarto render regularized_models.qmd
```

## Dependencies

Typical R packages used in the notebooks include: `tidyverse`, `readxl`, `janitor`, `irr`, `formattable`, `arsenal`, `glmnet`, `pROC`, `robustbase`, `Hmisc`, `kableExtra`, and supporting packages declared in each document’s setup chunk.
