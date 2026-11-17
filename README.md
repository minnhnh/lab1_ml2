# Lab 1 - Principal Component Analysis

Repository for the T1 Principal Component Analysis labwork.

## Team members

| Student | Main responsibility |
|---|---|
| Nguyễn Hoàng Minh | Wine Quality dataset, project integration, final repository and report assembly |
| Nguyễn Hoàng Anh | Heart Disease dataset, categorical preprocessing, report review |

Both members are responsible for the common PCA methodology, cross-dataset comparison, final discussion, and quality assurance.

## Project objective

The project studies two public datasets, performs data-quality analysis and preprocessing, and applies Principal Component Analysis (PCA) to evaluate how much information can be retained after dimensionality reduction.

The selected datasets are:

1. **Wine Quality** - physicochemical measurements and wine-quality scores. The red and white wine files will be integrated into one dataset with an additional `wine_type` column.
2. **Heart Disease (Cleveland)** - clinical measurements and a heart-disease target, including numerical and categorical features and missing values.

Official sources:

- [UCI Wine Quality](https://archive.ics.uci.edu/dataset/186/wine+quality)
- [UCI Heart Disease](https://archive.ics.uci.edu/dataset/45/heart+disease)

## Main workflow

```text
Raw data
  -> data-quality audit
  -> cleaning and integration
  -> statistical and correlation analysis
  -> encoding and standardization
  -> PCA and explained-variance analysis
  -> 2D visualization
  -> comparison and discussion
```

The target variables are not included when fitting PCA. They are retained only for interpretation and visualization.

## Repository structure

```text
lab1_ml2/
|-- data/
|   |-- raw/                 # downloaded source files (not committed)
|   `-- processed/           # cleaned data files (not committed)
|-- docs/
|   |-- ASSIGNMENT_REQUIREMENTS.md
|   `-- WORK_PLAN.md
|-- notebooks/
|   |-- 01_wine_quality.ipynb
|   |-- 02_heart_disease.ipynb
|   `-- 03_pca_comparison.ipynb
|-- report/
|   |-- figures/
|   |-- tables/
|   `-- final_report.pdf
|-- .gitignore
|-- README.md
`-- requirements.txt
```

Notebook and report outputs will be added as the analysis is completed. See [docs/WORK_PLAN.md](docs/WORK_PLAN.md) for ownership, deliverables, and the seven-day schedule. Nguyễn Hoàng Minh's detailed execution checklist is available in [docs/MINH_CHECKLIST.md](docs/MINH_CHECKLIST.md).

## Required outputs

- Dataset descriptions and feature-type tables.
- Data-quality audit covering missing values, duplicates, invalid values, inconsistencies, and outliers.
- Before/after-cleaning comparison.
- Data-integration and data-transformation discussion.
- Mean, variance, covariance, and correlation analysis.
- Appropriate analysis of categorical variables.
- Correlation heatmap and strongest feature pair for each dataset.
- PCA preprocessing and methodology.
- Explained and cumulative variance results.
- Comparison of multiple component counts.
- Two-dimensional PCA visualization for each dataset.
- Comparison of original and PCA-transformed representations.
- Final PDF report containing both students' full names and student IDs.

## Local setup

Create and activate a Python virtual environment, then install the dependencies:

```bash
python -m venv .venv
pip install -r requirements.txt
```

Start Jupyter:

```bash
jupyter lab
```

## Working agreement

- Do not commit raw datasets, generated caches, local environments, or temporary files.
- Commit source notebooks, report text, selected figures, and compact result tables.
- Each statistical claim in the report must be reproducible from a notebook.
- Use descriptive commit messages and review the other member's section before final submission.
