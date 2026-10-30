# SQL, Python and Machine Learning for Well-Log Data Analysis

## Overview

A hands-on **learning project** demonstrating SQL database queries, exploratory data analysis, and porosity prediction using Python. The notebook starts with a small, manually created sample table in SQLite and progresses to a separate **10-row synthetic/demo well-log dataset** with gamma ray (GR), resistivity, and porosity values. It is **not** a validated model trained on measured reservoir logs.

## Tools

Python · SQLite (`sqlite3`) · Jupyter Notebook · Pandas · NumPy · Matplotlib · scikit-learn · statsmodels

## Repository structure

```text
SQL_Well_Log_Analytics_GitHub/
├── README.md
├── SQL_database_learning.ipynb
├── requirements.txt
├── .gitignore
├── results/
│   └── model_comparison_results.csv
└── images/
    └── model_comparison.png
```

## What the notebook covers

1. **SQLite fundamentals:** Create in-memory `WellSamples` and `SampleDetails` tables with pandas; query them using `SELECT`, `WHERE`, `ORDER BY`, `LIMIT`, `COUNT`, `AVG`, `MIN`, `MAX`, `SUM`, `GROUP BY`, and `HAVING`.
2. **Joins and data quality:** `INNER JOIN`, `LEFT JOIN`, unmatched location checks, and location-level statistics.
3. **Intermediate SQL:** `CASE`, CTEs, `RANK()`, `ROW_NUMBER()`, and windowed averages.
4. **Exploratory analysis:** Descriptive statistics, z-scores, histograms, boxplots, scatterplots, correlations and variance inflation factors (VIF).
5. **Regression models:** Predict porosity from GR and resistivity, comparing Linear Regression and Random Forest using a held-out split and shuffled five-fold cross-validation.

## Model performance

Five-fold cross-validation on 10 manually defined observations (`KFold(n_splits=5, shuffle=True, random_state=42)`):

| Model | Mean MAE | Mean RMSE |
|---|---:|---:|
| Linear Regression | **0.450** | **0.513** |
| Random Forest | 1.248 | 1.446 |

![Model comparison](images/model_comparison.png)

**Interpretation:** Linear Regression shows lower averaged error on this demonstration dataset. The sample is extremely small, and its feature–target relationships were manually specified; these metrics are not evidence of performance on unseen real-world wells. Error metrics use the same numeric units as the porosity target, which was entered as percentage-style numbers (e.g., 8, 10, 13).

## How to run

1. Open Anaconda Navigator and launch Jupyter Notebook or JupyterLab.
2. Install dependencies in the notebook's environment: `pip install -r requirements.txt` (or install through conda).
3. Open `SQL_database_learning.ipynb` and run the cells **in sequence**, reviewing the notes below first.
4. SQL practice tables use an **in-memory database**, so their contents reset when the kernel restarts.
5. The notebook writes `model_comparison_results.csv` and `model_comparison.png` to the **current working directory** when their saving cells run. Copies of those outputs are already stored in this repository's `results/` and `images/` directories.

## Known issues and recommended fixes

The original learning notebook is retained unedited to preserve the work and its progression. Some earlier exploratory cells contain errors or exercises that should be corrected before using **Run All**:

- Column name `prosity_Class` is misspelled, although consistently used in much of the SQL practice. Rename carefully across all references if standardising to `porosity_Class`.
- SQL practice includes a mismatched table name `WellSample` instead of `WellSamples` and `SampleDatails` instead of `SampleDetails`.
- An early cross-validation cell uses `model` vs `models` and `score` vs `scores`; a subsequent cell provides the corrected evaluation.
- A draft SQL category-percentage query is incomplete; a subsequent CTE version completes that calculation.
- A `CASE` categorisation example uses inconsistent boundaries/names relative to the later classification logic.
- SQLite in-memory connection is recreated partway through the notebook, so earlier tables do not persist across that reset.
- The notebook has cells with no saved outputs and may require corrections before a clean top-to-bottom run.

## Limitations and next steps

- Replace demonstration samples with permission-cleared, real well-log data and document provenance, units, depth intervals, and preprocessing.
- Validate missing values, unrealistic values, and correlations; avoid training on any target-derived features.
- Use independent-well or depth-aware validation for field applications rather than random splits alone.
- Tune models inside training folds and report variability across folds; consider additional metrics such as R² where valid.
- Refactor the notebook into clean, reproducible stages and regenerate all outputs.

## Project purpose

An educational portfolio example illustrating SQL querying, data exploration, regression modelling, and communicating model-comparison findings in a geoscience context.
