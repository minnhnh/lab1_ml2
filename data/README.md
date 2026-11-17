# Data directory

Raw and processed datasets are intentionally excluded from Git. Download the source files locally and keep them in the following locations.

## Wine Quality

Source: <https://archive.ics.uci.edu/dataset/186/wine+quality>

Expected local files:

```text
data/raw/winequality-red.csv
data/raw/winequality-white.csv
```

During integration:

- Add `wine_type = "red"` to the red file.
- Add `wine_type = "white"` to the white file.
- Concatenate both files by rows because they share the same schema.
- Keep `quality` as the target and exclude it from PCA fitting.

## Heart Disease

Source: <https://archive.ics.uci.edu/dataset/45/heart+disease>

Use the processed Cleveland subset with 13 input features and the `num` target.

Expected local file:

```text
data/raw/processed.cleveland.data
```

During preprocessing:

- Convert `?` markers to missing values.
- Preserve the original `num` field.
- Create a binary visualization label where `0` means no disease and values greater than `0` mean disease.
- Exclude both target representations from PCA fitting.

## Reproducibility

Record file names, retrieval dates, row counts, column counts, and cleaning decisions in the notebooks. Do not silently alter raw files.

