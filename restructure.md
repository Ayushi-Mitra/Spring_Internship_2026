# Restructure Status

## Agreed direction

This project is staying notebook-first.

The goal of the restructure is not to convert the work into a Python package. The goal is to:

- keep the core workflow in notebooks
- organize data, reports, and notebooks cleanly
- make paths portable
- separate EDA from preprocessing, augmentation, and modeling

## Completed in this pass

### Repository hygiene

- Added `.gitignore`
- Added `pyproject.toml`
- Added tracked placeholder files for empty directories

### Folder layout

- Moved the raw dataset to `data/raw/ILPD.csv`
- Created `data/interim/` and `data/processed/`
- Created `notebooks/`, `scripts/`, `src/`, and `reports/`
- Moved report artifacts into `reports/html/` and `reports/docs/`

### Notebook renaming

- `final_EDA.ipynb` -> `notebooks/01_data_preprocessing_and_outlier_handling.ipynb`
- `noisy_dataset(gender).ipynb` -> `notebooks/02_noise_augmentation_by_gender.ipynb`
- `papers_notebooks.ipynb` -> `notebooks/03_modeling_and_paper_notes.ipynb`

### Dedicated EDA notebook

- Added `scripts/eda_univariate_bivariate.ipynb`
- Configured it to read from `data/raw/ILPD.csv`
- Configured it to save diagrams into `reports/figures/eda/`
- Generated the first set of univariate and bivariate plots

## Current structure

```text
Spring_Internship_2026/
├─ .gitignore
├─ pyproject.toml
├─ README.md
├─ LICENSE
├─ NOTICE
├─ data/
│  ├─ raw/
│  │  └─ ILPD.csv
│  ├─ interim/
│  └─ processed/
├─ notebooks/
│  ├─ 01_data_preprocessing_and_outlier_handling.ipynb
│  ├─ 02_noise_augmentation_by_gender.ipynb
│  └─ 03_modeling_and_paper_notes.ipynb
├─ scripts/
│  └─ eda_univariate_bivariate.ipynb
├─ reports/
│  ├─ docs/
│  │  └─ EDA.docx
│  ├─ html/
│  │  ├─ final_EDA.html
│  │  └─ univariate_EDA.html
│  └─ figures/
│     └─ eda/
├─ src/
└─ restructure.md
```

## Notebook responsibilities

### `notebooks/01_data_preprocessing_and_outlier_handling.ipynb`

Use this for:

- dataset loading
- missing-value handling
- encoding
- scaling
- outlier detection
- winsorization or cleaned-dataset preparation

### `scripts/eda_univariate_bivariate.ipynb`

Use this for:

- univariate EDA
- bivariate EDA
- figure generation for distributions and target relationships

This notebook saves outputs to:

- `reports/figures/eda/univariate/`
- `reports/figures/eda/bivariate/`

### `notebooks/02_noise_augmentation_by_gender.ipynb`

Use this for:

- GMM-based augmentation
- rule validation
- density filtering
- noisy or augmented dataset generation

### `notebooks/03_modeling_and_paper_notes.ipynb`

Use this for:

- literature-linked experimentation
- baseline model training
- tuning
- paper summary notes

## EDA outputs created in this pass

The new EDA notebook generated:

- `reports/figures/eda/univariate/categorical_distributions.png`
- `reports/figures/eda/univariate/numeric_histograms.png`
- `reports/figures/eda/univariate/numeric_boxplots.png`
- `reports/figures/eda/bivariate/gender_vs_target.png`
- `reports/figures/eda/bivariate/numeric_vs_target_boxplots.png`
- `reports/figures/eda/bivariate/selected_pairplot.png`
- `reports/figures/eda/bivariate/correlation_heatmap.png`

## Notes on `src/`

`src/` has been created because it was part of the requested folder layout, but it is only a placeholder right now.

For the current direction, no code extraction from notebooks is required unless you later decide that a shared helper layer is worth introducing.

## Next notebook-first cleanup steps

1. Update the existing notebooks to use the new relative paths under `data/raw/` and `reports/`.
2. Remove or de-emphasize EDA sections from `notebooks/01_data_preprocessing_and_outlier_handling.ipynb` now that the dedicated EDA notebook exists.
3. Decide whether cleaned datasets from preprocessing should be saved into `data/interim/` or `data/processed/`.
4. Keep adding notebook-specific dependencies to `pyproject.toml` if the workflow grows.

## What this document replaces

The earlier restructure plan leaned toward extracting reusable Python modules. That is no longer the working direction.

The current structure is centered on a clean, portable, notebook-only research workflow.
