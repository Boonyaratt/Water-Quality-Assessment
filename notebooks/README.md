# Notebooks

Notebook order:

1. `01_data_preparation_colab/`
   - Context feature generation and Colab/GEE-related preprocessing.
   - The CAL Sentinel-2 extraction notebook is not included yet and should be added later by the project owner.

2. `02_dataset_assembly/`
   - Merge field observations, Sentinel-2 tabular features, and context features into model-ready datasets.

3. `03_modeling_local/`
   - Train AutoGluon and manual baseline/stacking models.
   - Summarize old AutoGluon runs and model comparison results.

Avoid storing generated CSV outputs or trained model folders in the notebook directories.

