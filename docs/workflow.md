# Workflow

## 1. Data Preparation

Prepare field observations, Sentinel-2 features, water masking, and context features.

Current included notebook:

- `notebooks/01_data_preparation_colab/03_make_rswq_context_feature.ipynb`

Not included yet:

- `CAL_make_gg_ee_rswq_clean_2562_2568.ipynb`
- `merge_rswq.ipynb`

These notebooks can be added later when the owner exports the Colab versions.

## 2. Dataset Assembly

Build model-ready tabular datasets from:

- Ground observation targets
- Sentinel-2 features
- Context features

Included notebooks:

- `notebooks/02_dataset_assembly/01_build_tabular_go_wq.ipynb`
- `notebooks/02_dataset_assembly/02_make_rswq_tabular_dataset_assembly.ipynb`

## 3. Modeling

Included notebooks:

- `notebooks/03_modeling_local/01_train_autogluon_local_relaxed.ipynb`
- `notebooks/03_modeling_local/02_baseline_stack_station_temporal_final_model.ipynb`
- `notebooks/03_modeling_local/03_autogluon_old_runs_result_report.ipynb`
- `notebooks/03_modeling_local/05_random_split_diagnostic_baseline.ipynb`

The random-split notebook is a diagnostic comparison with easier literature-style validation settings. Temporal and station-temporal validation remain the main research evidence.

## 4. Reporting

Curated reports are stored in:

- `reports/tables/`
- `reports/slides/`
- `reports/figures/`
