# Ketamine clinic survey — analysis repository

Quarto (+ R) documents for analysing multi-rater survey data on ketamine clinics (binary items across clinics and raters). Run analyses from this directory so relative paths (`./data/...`) resolve correctly.

## Included analysis documents

### `inter_rater_reliability.qmd`

Inter-rater reliability (IRR) for four raters: pairwise Cohen’s kappa, three-rater subsets with Fleiss’s kappa, and grouped (e.g., by instrument family, clinic). Includes data preparation for the IRR tables and descriptive summaries. This is the first stage of the analytic workflow described here.

Rendered output: Quarto HTML (self-contained), with folded code chunks.

### `regularized_models.qmd`

Second stage: descriptive **Table 1**–style summaries and penalized regression (cross-validated LASSO by AUC) plus robust Poisson-regression contrasts for the telehealth outcome, using filtered data for one rater. Conceptually follows the IRR work in `inter_rater_reliability.qmd`.

Rendered output: same Quarto HTML pattern as above.

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
