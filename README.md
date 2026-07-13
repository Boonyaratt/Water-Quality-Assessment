# Water Quality Assessment With Remote Sensing And Machine Learning

This repository contains notebooks, experiment summaries, and reporting artifacts for a Thai water quality remote sensing and tabular machine learning workflow.

The current repository is designed to preserve the reproducible workflow without uploading raw data, large satellite outputs, or AutoGluon model folders.

## Project Scope

The workflow combines:

- Field water quality observations
- Sentinel-2 tabular features extracted around monitoring stations
- Context features such as rainfall, ERA5-Land hourly weather variables, season, and temporal indicators
- Tabular machine learning and AutoML models

The current modeling stage is tabular ML/AutoML. CNN image-patch models have not been trained in this repository stage.

## Target Framing

Targets are grouped carefully:

- Optical-related targets: Turbidity, SS
- Indirect proxy or risk-screening targets: DO, BOD, TCB, FCB, NH3-N

Sentinel-2 does not directly measure DO, BOD, microbial indicators, or NH3-N. Results for those targets should be interpreted as proxy prediction or risk-screening evidence.

## Repository Structure

```text
notebooks/
  01_data_preparation_colab/
  02_dataset_assembly/
  03_modeling_local/
docs/
reports/
  slides/
  tables/
  figures/
data/
experiments/
resources/
```

## Notebook Workflow

1. Data preparation and context features
   - `notebooks/01_data_preparation_colab/03_make_rswq_context_feature.ipynb`
   - The main CAL Google Earth Engine notebook is intentionally not included yet and will be added later.

2. Dataset assembly
   - `notebooks/02_dataset_assembly/01_build_tabular_go_wq.ipynb`
   - `notebooks/02_dataset_assembly/02_make_rswq_tabular_dataset_assembly.ipynb`

3. Local tabular modeling
   - `notebooks/03_modeling_local/01_train_autogluon_local_relaxed.ipynb`
   - `notebooks/03_modeling_local/02_baseline_stack_station_temporal_final_model.ipynb`
   - `notebooks/03_modeling_local/03_autogluon_old_runs_result_report.ipynb`

4. Reporting
   - Summary tables are stored in `reports/tables/`
   - Consultation slides are stored in `reports/slides/`

## Validation Design

The experiments use:

- Temporal split: train on 2562-2566 and test on 2567-2568
- Station-temporal split: held-out station and future-year robustness testing

Temporal results measure future-year prediction. Station-temporal results are stricter and measure transferability to unseen station patterns.

## Models Tested

- Dummy baselines: Dummy Median, Dummy Most Frequent
- Linear models: Ridge, ElasticNet, Logistic Regression
- Tree ensembles: Random Forest, ExtraTrees
- Gradient boosting: XGBoost, CatBoost
- Stacking ensembles: Stacking_RidgeMeta, Stacking_LogisticMeta
- AutoML benchmark: AutoGluon Tabular WeightedEnsemble_L2/L3

## Data Policy

Raw data, processed full datasets, AutoGluon model outputs, image patches, and large geospatial files are not tracked in Git. See `data/README.md` for expected external data locations.

