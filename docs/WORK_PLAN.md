# Seven-day work plan and task allocation

## Ownership principles

Each member owns one dataset from raw data to PCA results. This avoids duplicated work while keeping the workload balanced. Both members review each other's analysis and jointly write the cross-dataset discussion.

## Nguyễn Hoàng Minh - Wine Quality and integration lead

Primary deliverable: `notebooks/01_wine_quality.ipynb`

- Download and document the red and white Wine Quality files.
- Add the `wine_type` column and integrate the two files.
- Create the Wine Quality data dictionary and feature-type table.
- Audit missing values, duplicates, invalid values, inconsistencies, and outliers.
- Make and justify cleaning decisions; produce the before/after table.
- Calculate numerical summary statistics, covariance, and correlation.
- Analyze `wine_type` and `quality` appropriately.
- Find the strongest feature pair and create the correlation heatmap.
- Standardize the physicochemical input features and apply PCA.
- Produce explained-variance results and the PC1-PC2 plots.
- Write the Wine Quality sections of the report.
- Maintain the repository structure and assemble the final PDF.

## Nguyễn Hoàng Anh - Heart Disease and preprocessing lead

Primary deliverable: `notebooks/02_heart_disease.ipynb`

- Download and document the processed Cleveland Heart Disease data.
- Create the Heart Disease data dictionary and feature-type table.
- Convert missing-value markers to proper null values.
- Audit missing values, duplicates, invalid values, inconsistencies, and outliers.
- Impute numerical and categorical missing values with justified methods.
- Define the analysis label as no disease (`num = 0`) or disease (`num > 0`).
- Produce the before/after-cleaning table.
- Calculate numerical summary statistics, covariance, and correlation.
- Analyze categorical features with frequency tables and an appropriate association measure.
- Find the strongest feature pair and create the correlation heatmap.
- Encode categorical features, standardize numerical features, and apply PCA.
- Produce explained-variance results and the PC1-PC2 plot by disease label.
- Write the Heart Disease sections of the report.

## Shared work

Primary deliverable: `notebooks/03_pca_comparison.ipynb` and the final report.

- Explain PCA methodology, covariance/eigenvector or SVD interpretation, and component selection.
- Compare 2, 3, and 5 components and the 80%, 90%, and 95% cumulative-variance thresholds.
- Compare both datasets in information preservation, dimensionality reduction, interpretability, and visualization.
- Discuss high-variance and low-variance principal components.
- Write the introduction, methodology, discussion, and conclusion.
- Verify that all reported values can be reproduced from the notebooks.
- Review figures, captions, tables, citations, names, and student IDs.
- Render and inspect the final PDF before submission.

## Seven-day schedule

| Day | Nguyễn Hoàng Minh | Nguyễn Hoàng Anh | Shared checkpoint |
|---|---|---|---|
| 1 | Acquire Wine data; create dictionary | Acquire Heart data; create dictionary | Confirm scope, sources, and report outline |
| 2 | Integrate, audit, and clean Wine data | Audit, impute, and clean Heart data | Review cleaning decisions and before/after tables |
| 3 | Wine statistics and correlation | Heart statistics and correlation | Confirm strongest pairs and figure quality |
| 4 | Wine preprocessing and PCA | Heart preprocessing and PCA | Compare preprocessing pipelines |
| 5 | Wine figures and written findings | Heart figures and written findings | Complete comparison notebook and discussion notes |
| 6 | Assemble report and repository | Review report and reproduce results | Export first complete PDF and resolve gaps |
| 7 | Final corrections | Final corrections | PDF inspection, checklist review, and submission |

The first complete report should be produced on Day 6. Day 7 is reserved for verification and submission rather than new analysis.

## Definition of done

- All items in `ASSIGNMENT_REQUIREMENTS.md` are checked.
- Both dataset notebooks run from top to bottom without manual state.
- Figures contain titles, axis labels, legends/color bars, and readable text.
- Tables and report values match notebook outputs.
- Targets are excluded from PCA fitting.
- The report identifies both team members and their student IDs.
- Dataset sources are cited.
- The final PDF opens correctly and contains no clipped figures or tables.

## Suggested Git workflow

- Nguyễn Hoàng Minh: branch `analysis/wine-quality`.
- Nguyễn Hoàng Anh: branch `analysis/heart-disease`.
- Shared comparison and report work: merge into `main` after review.
- Keep dataset-specific commits separate so results can be reviewed easily.

Suggested commit messages:

- `Add Wine Quality cleaning and exploratory analysis`
- `Add Heart Disease preprocessing and statistics`
- `Add PCA explained variance and visualizations`
- `Add cross-dataset discussion and final report`

