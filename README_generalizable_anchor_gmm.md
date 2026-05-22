# Generalizable Anchor-Based GMM Notebook

This folder contains a generalized, AI-based re-adaptation of code originally made for genetic data. The original genetic-data code cannot be shared, so this version is structured as a reusable template with a synthetic dummy dataset.

## Files

- `generalizable_anchor_gmm.ipynb` — reusable notebook for anchor-based Gaussian Mixture Model classification.
- `dummy_anchor_gmm_dataset.csv` — synthetic example dataset that can be used to test the notebook without private or restricted data.

## What the notebook does

The notebook uses two known anchor groups to initialize a two-component Gaussian Mixture Model, then classifies all rows as more similar to one anchor or the other. In the current example, the anchors are:

- `A2` — treated as anchor A
- `B2` — treated as anchor B

The notebook also creates PCA plots and CSV summaries of row-level and group-level assignments.

## How to run the dummy example

1. Put `generalizable_anchor_gmm.ipynb` and `dummy_anchor_gmm_dataset.csv` in the same folder.
2. Open the notebook.
3. In the **Load data** cell, change:

```python
INPUT_FILE = "simple_universal_live_dead_combined.csv"
```

to:

```python
INPUT_FILE = "dummy_anchor_gmm_dataset.csv"
```

4. Run the notebook from top to bottom.

## How to adapt it to another dataset

### 1. Change the input file

Update `INPUT_FILE` to point to your new CSV file:

```python
INPUT_FILE = "your_dataset.csv"
```

### 2. Check the group/anchor column

The notebook searches for common group-column names, including:

```python
["WELL LABEL", "well", "well_label", "Well", "Sample", "sample", "group", "Group"]
```

For a different dataset, either rename your group column to one of those names or add your column name to `GROUP_COLUMN_CANDIDATES`.

### 3. Adjust filters

The filter block is optional. Set a filter value to `None` or remove it if it does not apply:

```python
FILTERS = {
    "time_hr": [48, 72],
    "temperature_c": [4, 22],
}
```

For a dataset without time or temperature, use:

```python
FILTERS = {}
```

### 4. Pick anchor groups

Change these values to two known reference groups in your dataset:

```python
anchor_A = "A2"
anchor_B = "B2"
```

The anchor labels can represent any two categories, controls, treatments, states, or reference samples.

### 5. Choose features

You can either manually list features:

```python
REQUESTED_FEATURES = [
    "feature_1",
    "feature_2",
    "feature_3",
]
```

or let the notebook automatically use numeric columns:

```python
REQUESTED_FEATURES = None
```

When using automatic features, review the printed feature list before trusting the result.

## Dummy dataset details

The dummy dataset is fully synthetic. It includes:

- `WELL LABEL`
- `time_hr`
- `temperature_c`
- `FOV`
- `T`
- Live-like measurement columns
- Dead-like measurement columns

It is designed only to demonstrate the workflow and should not be interpreted as real biological, genetic, imaging, or experimental data.

## Outputs

The notebook saves files using the input filename as the prefix. For the dummy dataset, expected outputs include:

- `dummy_anchor_gmm_dataset_simple_gmm_anchor_results.csv`
- `dummy_anchor_gmm_dataset_gmm_well_level_group_summary.csv`
- `dummy_anchor_gmm_dataset_gmm_row_level_group_list.csv`
- `dummy_anchor_gmm_dataset_gmm_anchor_pca_plot.png`
- `dummy_anchor_gmm_dataset_gmm_group_counts.png`
- `dummy_anchor_gmm_dataset_gmm_assignments_by_well.png`

## Notes

This notebook is meant as a flexible starting point, not a final statistical analysis pipeline. Always inspect the selected features, anchors, filtering steps, PCA plot, and classification probabilities before drawing conclusions.
