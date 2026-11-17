# Assignment requirements

This document converts the T1 PCA brief into an implementation checklist. It is a working summary, not a replacement for the original assignment PDF.

## Submission rules

- Complete the labwork within seven days after the lab session.
- Submit a PDF report of at least two pages through Google Classroom using the link in Moodle.
- Include figures, tables, discussion, and analysis.
- Including source code in the report is optional.
- Pair work is allowed.
- Include the full name and student ID of each team member.

## Part 1 - Study the datasets

- [ ] Select two public datasets, each containing more than six usable features.
- [ ] Briefly describe the purpose, source, size, features, and target of each dataset.
- [ ] Classify features as discrete/continuous, quantitative/qualitative, and numerical/categorical where applicable.
- [ ] Identify missing values, duplicates, invalid values, inconsistencies, and outliers.
- [ ] Explain how the identified quality issues may affect the analysis.
- [ ] Perform appropriate cleaning and explain every cleaning decision.
- [ ] Compare the datasets before and after cleaning.
- [ ] Evaluate whether data integration is necessary or beneficial.
- [ ] Perform integration when applicable and discuss its difficulties.
- [ ] Apply and justify normalization, standardization, or categorical encoding as appropriate.
- [ ] Identify the target and the possible machine-learning task for each dataset.
- [ ] Calculate mean, variance, covariance, and correlation for suitable variables.
- [ ] Analyze categorical variables with suitable measures such as frequency tables, contingency tables, chi-square, or Cramer's V.
- [ ] Identify the strongest non-self feature correlation in each dataset using absolute correlation.
- [ ] Visualize both correlation matrices and discuss the results.
- [ ] Summarize how cleaning, integration, and transformation affect analytical quality and reliability.

## Part 2 - Principal Component Analysis

- [ ] Apply PCA separately to both datasets.
- [ ] Explain the preprocessing required before PCA.
- [ ] Explain how principal components are computed and selected.
- [ ] Analyze the explained variance of every component.
- [ ] Compare components with high and low explained variance.
- [ ] Test multiple component counts and explain the information-versus-dimensionality trade-off.
- [ ] Report the number of components needed for selected cumulative-variance thresholds, such as 80%, 90%, and 95%.
- [ ] Plot PC1 against PC2 for each dataset.
- [ ] Distinguish observations by their labels where available.
- [ ] Discuss visible patterns, clusters, overlaps, and outliers.
- [ ] Compare the original and PCA-transformed representations.
- [ ] Discuss information preservation, interpretability, visualization benefits, and PCA limitations.

## Important analytical decisions

- Identifier columns and target variables must not be included in PCA.
- Numerical features must be standardized before PCA when scales or units differ.
- Nominal categorical variables must be encoded before inclusion in PCA.
- Self-correlations on the correlation-matrix diagonal must be excluded when finding the strongest pair.
- A low-variance component is not automatically useless; PCA preserves variance, not predictive relevance.
- No classification or regression model is required by the assignment.

## Minimum report evidence

1. Two dataset-description tables.
2. Two feature-type tables.
3. A before/after-cleaning table for each dataset.
4. Statistical summaries and covariance results.
5. Two correlation heatmaps.
6. The strongest feature pair for each dataset.
7. Two explained-variance or scree plots.
8. A table comparing different PCA component counts.
9. Two PC1-PC2 scatter plots.
10. A final comparison and conclusion.

