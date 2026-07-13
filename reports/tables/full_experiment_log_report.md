# Full Experiment Log Report: AutoGluon, Baselines, Stacking, Temporal And Station-temporal Tests

Date: 2026-07-13

This report is a complete experiment-log summary. It is not only a best-model summary. The full tables are provided as CSV and Excel files so they can be filtered and sorted for advisor reporting.

## Output files

- `E:\Water Quality Research\Reports\experiment_model_logs\experiment_log_all_results.xlsx`
- `E:\Water Quality Research\Reports\experiment_model_logs\all_experiment_metrics_long.csv`
- `E:\Water Quality Research\Reports\experiment_model_logs\experiment_config_catalog.csv`
- `E:\Water Quality Research\Reports\experiment_model_logs\autogluon_regression_all_configs.csv`
- `E:\Water Quality Research\Reports\experiment_model_logs\autogluon_classification_all_configs.csv`
- `E:\Water Quality Research\Reports\experiment_model_logs\manual_temporal_regression_all_configs.csv`
- `E:\Water Quality Research\Reports\experiment_model_logs\manual_temporal_classification_all_configs.csv`
- `E:\Water Quality Research\Reports\experiment_model_logs\manual_station_temporal_regression_aggregated.csv`
- `E:\Water Quality Research\Reports\experiment_model_logs\manual_station_temporal_classification_aggregated.csv`
- `E:\Water Quality Research\Reports\experiment_model_logs\manual_baseline_stacking_all_folds.csv`
- `E:\Water Quality Research\Reports\experiment_model_logs\latest_final_model_registry.csv`

## Experiment configuration catalog

| experiment_id | experiment_name | notebook_or_run | dataset | split | feature_sets | models | targets | difference_from_others |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| AG_MAIN | AutoGluon main S2 + Context | ag_relaxed_main_best_s2_context_best_quality_20260711_185242 | relaxed, n=390 | temporal 2562-2566 train / 2567-2568 test | S2 + Context | AutoGluon best_quality; WeightedEnsemble_L2/L3 allowed | DO,BOD,Turbidity,SS,TCB,FCB regression; NH3 classification | Full combined feature AutoML benchmark |
| AG_DIAG | AutoGluon diagnostic S2 only and Context only | ag_relaxed_diagnostic_s2_context_only_best_quality_20260711_231732 | relaxed, n=390 | temporal 2562-2566 train / 2567-2568 test | S2 only; Context only | AutoGluon best_quality; WeightedEnsemble_L2/L3 allowed | DO,BOD,Turbidity,SS,TCB,FCB regression; NH3 classification | Tests whether S2 or context carries stronger signal |
| AG_REPORT | AutoGluon report notebook | 03_autogluon_old_runs_result_report.ipynb | uses existing AutoGluon outputs | no new split; report-only | S2 only; Context only; S2 + Context | No new training | Aggregates all AutoGluon metrics and plots | Report/aggregation only, not a model experiment |
| MANUAL_TEMPORAL | Manual baseline/stacking temporal | 04_baseline_stack_station_temporal_final_model.ipynb | relaxed, n=390 | temporal 2562-2566 train / 2567-2568 test | S2 only; Context only; S2 + Context numeric-only | Dummy, Ridge, ElasticNet, RandomForest, ExtraTrees, XGBoost, CatBoost, Stacking_RidgeMeta/Stacking_LogisticMeta | 6 regression targets; NH3_3class; NH3_binary | Manual baseline and stacking comparison against future years |
| MANUAL_STATION_TEMPORAL | Manual baseline/stacking station-temporal | 04_baseline_stack_station_temporal_final_model.ipynb | relaxed, n=390 | 3 station-temporal folds; future years and held-out stations | S2 only; Context only; S2 + Context numeric-only | Same manual baseline and stacking models | 6 regression targets; NH3_3class; NH3_binary | Robustness test for unseen-station and future-year transfer |

## Metric row counts

| experiment_family | experiment_group | split | task | n_metric_rows |
| --- | --- | --- | --- | --- |
| AutoGluon best_quality | AutoGluon diagnostic: S2 only / Context only | temporal | classification | 2 |
| AutoGluon best_quality | AutoGluon diagnostic: S2 only / Context only | temporal | regression | 12 |
| AutoGluon best_quality | AutoGluon main: S2 + Context | temporal | classification | 1 |
| AutoGluon best_quality | AutoGluon main: S2 + Context | temporal | regression | 6 |
| Manual baseline + stacking | Manual baseline/stacking: station-temporal | station_temporal | classification | 126 |
| Manual baseline + stacking | Manual baseline/stacking: station-temporal | station_temporal | regression | 432 |
| Manual baseline + stacking | Manual baseline/stacking: temporal | temporal | classification | 42 |
| Manual baseline + stacking | Manual baseline/stacking: temporal | temporal | regression | 144 |

## Number of models or ensembles tried by target/feature/split

| experiment_family | split | task | target | feature_set | n_models_or_ensembles |
| --- | --- | --- | --- | --- | --- |
| AutoGluon best_quality | temporal | classification | NH3 | Context only | 1 |
| AutoGluon best_quality | temporal | classification | NH3 | S2 + Context | 1 |
| AutoGluon best_quality | temporal | classification | NH3 | S2 only | 1 |
| AutoGluon best_quality | temporal | regression | BOD | Context only | 1 |
| AutoGluon best_quality | temporal | regression | BOD | S2 + Context | 1 |
| AutoGluon best_quality | temporal | regression | BOD | S2 only | 1 |
| AutoGluon best_quality | temporal | regression | DO | Context only | 1 |
| AutoGluon best_quality | temporal | regression | DO | S2 + Context | 1 |
| AutoGluon best_quality | temporal | regression | DO | S2 only | 1 |
| AutoGluon best_quality | temporal | regression | FCB | Context only | 1 |
| AutoGluon best_quality | temporal | regression | FCB | S2 + Context | 1 |
| AutoGluon best_quality | temporal | regression | FCB | S2 only | 1 |
| AutoGluon best_quality | temporal | regression | SS | Context only | 1 |
| AutoGluon best_quality | temporal | regression | SS | S2 + Context | 1 |
| AutoGluon best_quality | temporal | regression | SS | S2 only | 1 |
| AutoGluon best_quality | temporal | regression | TCB | Context only | 1 |
| AutoGluon best_quality | temporal | regression | TCB | S2 + Context | 1 |
| AutoGluon best_quality | temporal | regression | TCB | S2 only | 1 |
| AutoGluon best_quality | temporal | regression | Turbidity | Context only | 1 |
| AutoGluon best_quality | temporal | regression | Turbidity | S2 + Context | 1 |
| AutoGluon best_quality | temporal | regression | Turbidity | S2 only | 1 |
| Manual baseline + stacking | station_temporal | classification | NH3_3class | Context only | 7 |
| Manual baseline + stacking | station_temporal | classification | NH3_3class | S2 + Context | 7 |
| Manual baseline + stacking | station_temporal | classification | NH3_3class | S2 only | 7 |
| Manual baseline + stacking | station_temporal | classification | NH3_binary | Context only | 7 |
| Manual baseline + stacking | station_temporal | classification | NH3_binary | S2 + Context | 7 |
| Manual baseline + stacking | station_temporal | classification | NH3_binary | S2 only | 7 |
| Manual baseline + stacking | station_temporal | regression | BOD | Context only | 8 |
| Manual baseline + stacking | station_temporal | regression | BOD | S2 + Context | 8 |
| Manual baseline + stacking | station_temporal | regression | BOD | S2 only | 8 |
| Manual baseline + stacking | station_temporal | regression | DO | Context only | 8 |
| Manual baseline + stacking | station_temporal | regression | DO | S2 + Context | 8 |
| Manual baseline + stacking | station_temporal | regression | DO | S2 only | 8 |
| Manual baseline + stacking | station_temporal | regression | FCB | Context only | 8 |
| Manual baseline + stacking | station_temporal | regression | FCB | S2 + Context | 8 |
| Manual baseline + stacking | station_temporal | regression | FCB | S2 only | 8 |
| Manual baseline + stacking | station_temporal | regression | SS | Context only | 8 |
| Manual baseline + stacking | station_temporal | regression | SS | S2 + Context | 8 |
| Manual baseline + stacking | station_temporal | regression | SS | S2 only | 8 |
| Manual baseline + stacking | station_temporal | regression | TCB | Context only | 8 |
| Manual baseline + stacking | station_temporal | regression | TCB | S2 + Context | 8 |
| Manual baseline + stacking | station_temporal | regression | TCB | S2 only | 8 |
| Manual baseline + stacking | station_temporal | regression | Turbidity | Context only | 8 |
| Manual baseline + stacking | station_temporal | regression | Turbidity | S2 + Context | 8 |
| Manual baseline + stacking | station_temporal | regression | Turbidity | S2 only | 8 |
| Manual baseline + stacking | temporal | classification | NH3_3class | Context only | 7 |
| Manual baseline + stacking | temporal | classification | NH3_3class | S2 + Context | 7 |
| Manual baseline + stacking | temporal | classification | NH3_3class | S2 only | 7 |
| Manual baseline + stacking | temporal | classification | NH3_binary | Context only | 7 |
| Manual baseline + stacking | temporal | classification | NH3_binary | S2 + Context | 7 |
| Manual baseline + stacking | temporal | classification | NH3_binary | S2 only | 7 |
| Manual baseline + stacking | temporal | regression | BOD | Context only | 8 |
| Manual baseline + stacking | temporal | regression | BOD | S2 + Context | 8 |
| Manual baseline + stacking | temporal | regression | BOD | S2 only | 8 |
| Manual baseline + stacking | temporal | regression | DO | Context only | 8 |
| Manual baseline + stacking | temporal | regression | DO | S2 + Context | 8 |
| Manual baseline + stacking | temporal | regression | DO | S2 only | 8 |
| Manual baseline + stacking | temporal | regression | FCB | Context only | 8 |
| Manual baseline + stacking | temporal | regression | FCB | S2 + Context | 8 |
| Manual baseline + stacking | temporal | regression | FCB | S2 only | 8 |
| Manual baseline + stacking | temporal | regression | SS | Context only | 8 |
| Manual baseline + stacking | temporal | regression | SS | S2 + Context | 8 |
| Manual baseline + stacking | temporal | regression | SS | S2 only | 8 |
| Manual baseline + stacking | temporal | regression | TCB | Context only | 8 |
| Manual baseline + stacking | temporal | regression | TCB | S2 + Context | 8 |
| Manual baseline + stacking | temporal | regression | TCB | S2 only | 8 |
| Manual baseline + stacking | temporal | regression | Turbidity | Context only | 8 |
| Manual baseline + stacking | temporal | regression | Turbidity | S2 + Context | 8 |
| Manual baseline + stacking | temporal | regression | Turbidity | S2 only | 8 |

## AutoGluon regression: all configs

| experiment_group | target | feature_set | model | transform | n_features | n_train | n_test | original_rmse | original_r2 | original_spearman_r | modelscale_rmse | modelscale_r2 | modelscale_spearman_r |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| AutoGluon diagnostic: S2 only / Context only | BOD | Context only | WeightedEnsemble_L2 | raw | 107 | 276 | 114 | 0.800 | 0.136 | 0.450 | 0.800 | 0.136 | 0.450 |
| AutoGluon main: S2 + Context | BOD | S2 + Context | WeightedEnsemble_L2 | raw | 139 | 276 | 114 | 0.758 | 0.225 | 0.494 | 0.758 | 0.225 | 0.494 |
| AutoGluon diagnostic: S2 only / Context only | BOD | S2 only | WeightedEnsemble_L3 | raw | 32 | 276 | 114 | 0.726 | 0.290 | 0.517 | 0.726 | 0.290 | 0.517 |
| AutoGluon diagnostic: S2 only / Context only | DO | Context only | WeightedEnsemble_L3 | raw | 107 | 276 | 114 | 0.975 | 0.304 | 0.549 | 0.975 | 0.304 | 0.549 |
| AutoGluon main: S2 + Context | DO | S2 + Context | WeightedEnsemble_L3 | raw | 139 | 276 | 114 | 0.893 | 0.416 | 0.595 | 0.893 | 0.416 | 0.595 |
| AutoGluon diagnostic: S2 only / Context only | DO | S2 only | WeightedEnsemble_L3 | raw | 32 | 276 | 114 | 1.109 | 0.100 | 0.346 | 1.109 | 0.100 | 0.346 |
| AutoGluon diagnostic: S2 only / Context only | FCB | Context only | WeightedEnsemble_L3 | log1p | 107 | 276 | 114 | 3115 | 0.029 | 0.511 | 1.720 | 0.297 | 0.511 |
| AutoGluon main: S2 + Context | FCB | S2 + Context | WeightedEnsemble_L2 | log1p | 139 | 276 | 114 | 3122 | 0.025 | 0.555 | 1.668 | 0.339 | 0.555 |
| AutoGluon diagnostic: S2 only / Context only | FCB | S2 only | WeightedEnsemble_L2 | log1p | 32 | 276 | 114 | 3254 | -0.059 | 0.348 | 1.857 | 0.180 | 0.348 |
| AutoGluon diagnostic: S2 only / Context only | SS | Context only | WeightedEnsemble_L2 | log1p | 107 | 276 | 114 | 59.381 | 0.052 | 0.663 | 0.688 | 0.395 | 0.663 |
| AutoGluon main: S2 + Context | SS | S2 + Context | WeightedEnsemble_L2 | log1p | 139 | 276 | 114 | 56.691 | 0.136 | 0.709 | 0.622 | 0.505 | 0.709 |
| AutoGluon diagnostic: S2 only / Context only | SS | S2 only | WeightedEnsemble_L2 | log1p | 32 | 276 | 114 | 59.908 | 0.035 | 0.660 | 0.701 | 0.371 | 0.660 |
| AutoGluon diagnostic: S2 only / Context only | TCB | Context only | WeightedEnsemble_L2 | log1p | 107 | 276 | 114 | 8246 | 0.109 | 0.632 | 1.474 | 0.379 | 0.632 |
| AutoGluon main: S2 + Context | TCB | S2 + Context | WeightedEnsemble_L2 | log1p | 139 | 276 | 114 | 8362 | 0.084 | 0.640 | 1.462 | 0.389 | 0.640 |
| AutoGluon diagnostic: S2 only / Context only | TCB | S2 only | WeightedEnsemble_L3 | log1p | 32 | 276 | 114 | 8607 | 0.030 | 0.414 | 1.677 | 0.195 | 0.414 |
| AutoGluon diagnostic: S2 only / Context only | Turbidity | Context only | WeightedEnsemble_L3 | log1p | 107 | 276 | 114 | 57.592 | 0.162 | 0.599 | 0.876 | 0.326 | 0.599 |
| AutoGluon main: S2 + Context | Turbidity | S2 + Context | WeightedEnsemble_L2 | log1p | 139 | 276 | 114 | 53.618 | 0.274 | 0.709 | 0.766 | 0.484 | 0.709 |
| AutoGluon diagnostic: S2 only / Context only | Turbidity | S2 only | WeightedEnsemble_L2 | log1p | 32 | 276 | 114 | 58.748 | 0.128 | 0.698 | 0.795 | 0.444 | 0.698 |

## AutoGluon NH3 classification: all configs

| experiment_group | target | feature_set | model | n_features | n_train | n_test | accuracy | balanced_accuracy | macro_f1 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| AutoGluon diagnostic: S2 only / Context only | NH3 | Context only | WeightedEnsemble_L2 | 107 | 276 | 114 | 0.307 | 0.380 | 0.251 |
| AutoGluon main: S2 + Context | NH3 | S2 + Context | WeightedEnsemble_L2 | 139 | 276 | 114 | 0.281 | 0.354 | 0.233 |
| AutoGluon diagnostic: S2 only / Context only | NH3 | S2 only | WeightedEnsemble_L2 | 32 | 276 | 114 | 0.281 | 0.342 | 0.228 |

## Manual temporal regression: all configs

This section lists every manual temporal regression config. The same table is available in `manual_temporal_regression_all_configs.csv` and the Excel workbook.

| target | feature_set | model | transform | n_features | n_train | n_test | original_rmse | original_r2 | original_spearman_r | modelscale_rmse | modelscale_r2 | modelscale_spearman_r | rank_metric |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| BOD | S2 + Context | Stacking_RidgeMeta | raw | 138 | 276 | 114 | 0.770 | 0.200 | 0.438 | 0.770 | 0.200 | 0.438 | 0.770 |
| BOD | S2 + Context | CatBoost | raw | 138 | 276 | 114 | 0.771 | 0.197 | 0.465 | 0.771 | 0.197 | 0.465 | 0.771 |
| BOD | S2 only | ElasticNet | raw | 32 | 276 | 114 | 0.775 | 0.190 | 0.442 | 0.775 | 0.190 | 0.442 | 0.775 |
| BOD | S2 only | Stacking_RidgeMeta | raw | 32 | 276 | 114 | 0.775 | 0.189 | 0.449 | 0.775 | 0.189 | 0.449 | 0.775 |
| BOD | S2 only | Ridge | raw | 32 | 276 | 114 | 0.776 | 0.187 | 0.449 | 0.776 | 0.187 | 0.449 | 0.776 |
| BOD | S2 only | CatBoost | raw | 32 | 276 | 114 | 0.776 | 0.187 | 0.530 | 0.776 | 0.187 | 0.530 | 0.776 |
| BOD | S2 + Context | Ridge | raw | 138 | 276 | 114 | 0.778 | 0.184 | 0.483 | 0.906 | -0.109 | 0.483 | 0.778 |
| BOD | S2 + Context | RandomForest | raw | 138 | 276 | 114 | 0.780 | 0.178 | 0.440 | 0.780 | 0.178 | 0.440 | 0.780 |
| BOD | Context only | ElasticNet | raw | 106 | 276 | 114 | 0.785 | 0.168 | 0.366 | 1.078 | -0.570 | 0.366 | 0.785 |
| BOD | S2 + Context | ElasticNet | raw | 138 | 276 | 114 | 0.791 | 0.155 | 0.466 | 1.028 | -0.425 | 0.466 | 0.791 |
| BOD | S2 + Context | ExtraTrees | raw | 138 | 276 | 114 | 0.793 | 0.152 | 0.433 | 0.793 | 0.152 | 0.433 | 0.793 |
| BOD | Context only | Ridge | raw | 106 | 276 | 114 | 0.796 | 0.146 | 0.408 | 0.989 | -0.320 | 0.408 | 0.796 |
| BOD | S2 only | XGBoost | raw | 32 | 276 | 114 | 0.796 | 0.145 | 0.466 | 0.796 | 0.145 | 0.466 | 0.796 |
| BOD | Context only | Stacking_RidgeMeta | raw | 106 | 276 | 114 | 0.807 | 0.121 | 0.355 | 0.807 | 0.121 | 0.355 | 0.807 |
| BOD | S2 only | RandomForest | raw | 32 | 276 | 114 | 0.808 | 0.119 | 0.465 | 0.808 | 0.119 | 0.465 | 0.808 |
| BOD | S2 + Context | XGBoost | raw | 138 | 276 | 114 | 0.812 | 0.110 | 0.406 | 0.812 | 0.110 | 0.406 | 0.812 |
| BOD | Context only | CatBoost | raw | 106 | 276 | 114 | 0.817 | 0.098 | 0.361 | 0.817 | 0.098 | 0.361 | 0.817 |
| BOD | Context only | RandomForest | raw | 106 | 276 | 114 | 0.818 | 0.096 | 0.345 | 0.818 | 0.096 | 0.345 | 0.818 |
| BOD | Context only | ExtraTrees | raw | 106 | 276 | 114 | 0.829 | 0.073 | 0.386 | 0.829 | 0.073 | 0.386 | 0.829 |
| BOD | Context only | XGBoost | raw | 106 | 276 | 114 | 0.836 | 0.057 | 0.326 | 0.836 | 0.057 | 0.326 | 0.836 |
| BOD | S2 only | ExtraTrees | raw | 32 | 276 | 114 | 0.857 | 0.010 | 0.428 | 0.857 | 0.010 | 0.428 | 0.857 |
| BOD | S2 only | DummyMedian | raw | 32 | 276 | 114 | 0.932 | -0.171 |  | 0.932 | -0.171 |  | 0.932 |
| BOD | Context only | DummyMedian | raw | 106 | 276 | 114 | 0.932 | -0.171 |  | 0.932 | -0.171 |  | 0.932 |
| BOD | S2 + Context | DummyMedian | raw | 138 | 276 | 114 | 0.932 | -0.171 |  | 0.932 | -0.171 |  | 0.932 |
| DO | S2 + Context | RandomForest | raw | 138 | 276 | 114 | 0.890 | 0.420 | 0.593 | 0.890 | 0.420 | 0.593 | 0.890 |
| DO | S2 + Context | CatBoost | raw | 138 | 276 | 114 | 0.900 | 0.407 | 0.604 | 0.900 | 0.407 | 0.604 | 0.900 |
| DO | Context only | RandomForest | raw | 106 | 276 | 114 | 0.901 | 0.406 | 0.596 | 0.901 | 0.406 | 0.596 | 0.901 |
| DO | S2 + Context | XGBoost | raw | 138 | 276 | 114 | 0.909 | 0.395 | 0.581 | 0.909 | 0.395 | 0.581 | 0.909 |
| DO | Context only | CatBoost | raw | 106 | 276 | 114 | 0.918 | 0.382 | 0.571 | 0.918 | 0.382 | 0.571 | 0.918 |
| DO | Context only | XGBoost | raw | 106 | 276 | 114 | 0.928 | 0.368 | 0.579 | 0.928 | 0.368 | 0.579 | 0.928 |
| DO | S2 + Context | ExtraTrees | raw | 138 | 276 | 114 | 0.966 | 0.317 | 0.553 | 0.966 | 0.317 | 0.553 | 0.966 |
| DO | Context only | ExtraTrees | raw | 106 | 276 | 114 | 0.975 | 0.304 | 0.560 | 0.975 | 0.304 | 0.560 | 0.975 |
| DO | S2 only | Stacking_RidgeMeta | raw | 32 | 276 | 114 | 1.046 | 0.198 | 0.512 | 1.046 | 0.198 | 0.512 | 1.046 |
| DO | Context only | Stacking_RidgeMeta | raw | 106 | 276 | 114 | 1.049 | 0.193 | 0.542 | 1.049 | 0.193 | 0.542 | 1.049 |
| DO | S2 only | ExtraTrees | raw | 32 | 276 | 114 | 1.051 | 0.191 | 0.486 | 1.051 | 0.191 | 0.486 | 1.051 |
| DO | S2 only | RandomForest | raw | 32 | 276 | 114 | 1.054 | 0.186 | 0.503 | 1.054 | 0.186 | 0.503 | 1.054 |
| DO | S2 only | CatBoost | raw | 32 | 276 | 114 | 1.055 | 0.184 | 0.474 | 1.055 | 0.184 | 0.474 | 1.055 |
| DO | S2 only | XGBoost | raw | 32 | 276 | 114 | 1.075 | 0.154 | 0.471 | 1.075 | 0.154 | 0.471 | 1.075 |
| DO | S2 + Context | Stacking_RidgeMeta | raw | 138 | 276 | 114 | 1.121 | 0.079 | 0.559 | 1.121 | 0.079 | 0.559 | 1.121 |
| DO | S2 only | ElasticNet | raw | 32 | 276 | 114 | 1.125 | 0.073 | 0.367 | 1.125 | 0.073 | 0.367 | 1.125 |
| DO | S2 only | Ridge | raw | 32 | 276 | 114 | 1.128 | 0.068 | 0.340 | 1.128 | 0.068 | 0.340 | 1.128 |
| DO | S2 only | DummyMedian | raw | 32 | 276 | 114 | 1.190 | -0.038 |  | 1.190 | -0.038 |  | 1.190 |
| DO | Context only | DummyMedian | raw | 106 | 276 | 114 | 1.190 | -0.038 |  | 1.190 | -0.038 |  | 1.190 |
| DO | S2 + Context | DummyMedian | raw | 138 | 276 | 114 | 1.190 | -0.038 |  | 1.190 | -0.038 |  | 1.190 |
| DO | Context only | Ridge | raw | 106 | 276 | 114 | 3.313 | -7.044 | 0.459 | 5.201 | -18.821 | 0.459 | 3.313 |
| DO | Context only | ElasticNet | raw | 106 | 276 | 114 | 3.433 | -7.637 | 0.521 | 5.713 | -22.916 | 0.521 | 3.433 |
| DO | S2 + Context | Ridge | raw | 138 | 276 | 114 | 3.558 | -8.276 | 0.548 | 5.751 | -23.230 | 0.548 | 3.558 |
| DO | S2 + Context | ElasticNet | raw | 138 | 276 | 114 | 3.778 | -9.455 | 0.556 | 6.220 | -27.342 | 0.556 | 3.778 |
| FCB | S2 + Context | ExtraTrees | log1p | 138 | 276 | 114 | 3156 | 0.004 | 0.568 | 1.643 | 0.359 | 0.568 | 1.643 |
| FCB | S2 + Context | CatBoost | log1p | 138 | 276 | 114 | 3058 | 0.065 | 0.571 | 1.658 | 0.346 | 0.571 | 1.658 |
| FCB | S2 + Context | Stacking_RidgeMeta | log1p | 138 | 276 | 114 | 3149 | 0.008 | 0.563 | 1.669 | 0.338 | 0.563 | 1.669 |
| FCB | S2 + Context | XGBoost | log1p | 138 | 276 | 114 | 3134 | 0.018 | 0.574 | 1.673 | 0.334 | 0.574 | 1.673 |
| FCB | S2 + Context | RandomForest | log1p | 138 | 276 | 114 | 3175 | -0.008 | 0.548 | 1.675 | 0.333 | 0.548 | 1.675 |
| FCB | Context only | ExtraTrees | log1p | 106 | 276 | 114 | 3157 | 0.003 | 0.537 | 1.701 | 0.312 | 0.537 | 1.701 |
| FCB | Context only | RandomForest | log1p | 106 | 276 | 114 | 3177 | -0.009 | 0.533 | 1.702 | 0.311 | 0.533 | 1.702 |
| FCB | Context only | XGBoost | log1p | 106 | 276 | 114 | 3177 | -0.009 | 0.545 | 1.715 | 0.301 | 0.545 | 1.715 |
| FCB | Context only | CatBoost | log1p | 106 | 276 | 114 | 3196 | -0.021 | 0.523 | 1.720 | 0.297 | 0.523 | 1.720 |
| FCB | Context only | Stacking_RidgeMeta | log1p | 106 | 276 | 114 | 3213 | -0.032 | 0.498 | 1.741 | 0.280 | 0.498 | 1.741 |
| FCB | S2 only | RandomForest | log1p | 32 | 276 | 114 | 3258 | -0.061 | 0.384 | 1.852 | 0.184 | 0.384 | 1.852 |
| FCB | S2 only | ExtraTrees | log1p | 32 | 276 | 114 | 3233 | -0.045 | 0.357 | 1.862 | 0.176 | 0.357 | 1.862 |
| FCB | S2 only | CatBoost | log1p | 32 | 276 | 114 | 3215 | -0.034 | 0.357 | 1.869 | 0.170 | 0.357 | 1.869 |
| FCB | S2 only | Stacking_RidgeMeta | log1p | 32 | 276 | 114 | 3324 | -0.105 | 0.347 | 1.880 | 0.160 | 0.347 | 1.880 |
| FCB | S2 only | XGBoost | log1p | 32 | 276 | 114 | 3255 | -0.059 | 0.313 | 1.915 | 0.129 | 0.313 | 1.915 |
| FCB | S2 only | Ridge | log1p | 32 | 276 | 114 | 3367 | -0.134 | 0.222 | 1.952 | 0.094 | 0.222 | 1.952 |
| FCB | S2 only | ElasticNet | log1p | 32 | 276 | 114 | 3278 | -0.075 | 0.257 | 1.952 | 0.094 | 0.257 | 1.952 |
| FCB | S2 only | DummyMedian | log1p | 32 | 276 | 114 | 3387 | -0.148 |  | 2.071 | -0.020 |  | 2.071 |
| FCB | Context only | DummyMedian | log1p | 106 | 276 | 114 | 3387 | -0.148 |  | 2.071 | -0.020 |  | 2.071 |
| FCB | S2 + Context | DummyMedian | log1p | 138 | 276 | 114 | 3387 | -0.148 |  | 2.071 | -0.020 |  | 2.071 |
| FCB | Context only | ElasticNet | log1p | 106 | 276 | 114 | 3055 | 0.067 | 0.408 | 2.304 | -0.262 | 0.408 | 2.304 |
| FCB | Context only | Ridge | log1p | 106 | 276 | 114 | 3111 | 0.032 | 0.442 | 2.414 | -0.385 | 0.442 | 2.414 |
| FCB | S2 + Context | ElasticNet | log1p | 138 | 276 | 114 | 2988 | 0.107 | 0.395 | 2.661 | -0.683 | 0.395 | 2.661 |
| FCB | S2 + Context | Ridge | log1p | 138 | 276 | 114 | 2945 | 0.133 | 0.427 | 2.733 | -0.775 | 0.427 | 2.733 |
| SS | S2 + Context | Stacking_RidgeMeta | log1p | 138 | 276 | 114 | 52.404 | 0.262 | 0.695 | 0.619 | 0.510 | 0.695 | 0.619 |
| SS | S2 + Context | RandomForest | log1p | 138 | 276 | 114 | 59.043 | 0.063 | 0.719 | 0.641 | 0.474 | 0.719 | 0.641 |
| SS | S2 + Context | ExtraTrees | log1p | 138 | 276 | 114 | 59.326 | 0.054 | 0.718 | 0.649 | 0.461 | 0.718 | 0.649 |
| SS | S2 + Context | CatBoost | log1p | 138 | 276 | 114 | 59.649 | 0.044 | 0.710 | 0.656 | 0.449 | 0.710 | 0.656 |
| SS | Context only | CatBoost | log1p | 106 | 276 | 114 | 59.533 | 0.047 | 0.684 | 0.677 | 0.414 | 0.684 | 0.677 |
| SS | S2 only | Stacking_RidgeMeta | log1p | 32 | 276 | 114 | 59.547 | 0.047 | 0.685 | 0.677 | 0.414 | 0.685 | 0.677 |
| SS | S2 only | RandomForest | log1p | 32 | 276 | 114 | 59.503 | 0.048 | 0.669 | 0.680 | 0.408 | 0.669 | 0.680 |
| SS | S2 + Context | XGBoost | log1p | 138 | 276 | 114 | 60.356 | 0.021 | 0.690 | 0.682 | 0.405 | 0.690 | 0.682 |
| SS | S2 only | ElasticNet | log1p | 32 | 276 | 114 | 59.252 | 0.056 | 0.682 | 0.683 | 0.402 | 0.682 | 0.683 |
| SS | Context only | Stacking_RidgeMeta | log1p | 106 | 276 | 114 | 58.868 | 0.069 | 0.663 | 0.684 | 0.401 | 0.663 | 0.684 |
| SS | S2 only | Ridge | log1p | 32 | 276 | 114 | 59.489 | 0.049 | 0.685 | 0.687 | 0.396 | 0.685 | 0.687 |
| SS | S2 only | ExtraTrees | log1p | 32 | 276 | 114 | 59.728 | 0.041 | 0.672 | 0.689 | 0.393 | 0.672 | 0.689 |
| SS | Context only | RandomForest | log1p | 106 | 276 | 114 | 60.006 | 0.032 | 0.640 | 0.711 | 0.352 | 0.640 | 0.711 |
| SS | Context only | ExtraTrees | log1p | 106 | 276 | 114 | 60.578 | 0.014 | 0.644 | 0.719 | 0.338 | 0.644 | 0.719 |
| SS | S2 only | CatBoost | log1p | 32 | 276 | 114 | 59.540 | 0.047 | 0.616 | 0.720 | 0.337 | 0.616 | 0.720 |
| SS | Context only | XGBoost | log1p | 106 | 276 | 114 | 60.232 | 0.025 | 0.631 | 0.723 | 0.331 | 0.631 | 0.723 |
| SS | S2 only | XGBoost | log1p | 32 | 276 | 114 | 60.245 | 0.024 | 0.585 | 0.743 | 0.293 | 0.585 | 0.743 |
| SS | S2 only | DummyMedian | log1p | 32 | 276 | 114 | 63.122 | -0.071 |  | 0.902 | -0.042 |  | 0.902 |
| SS | Context only | DummyMedian | log1p | 106 | 276 | 114 | 63.122 | -0.071 |  | 0.902 | -0.042 |  | 0.902 |
| SS | S2 + Context | DummyMedian | log1p | 138 | 276 | 114 | 63.122 | -0.071 |  | 0.902 | -0.042 |  | 0.902 |
| SS | S2 + Context | Ridge | log1p | 138 | 276 | 114 | 8138 | -17800 | 0.609 | 1.331 | -1.269 | 0.609 | 1.331 |
| SS | S2 + Context | ElasticNet | log1p | 138 | 276 | 114 | 32952 | -291843 | 0.555 | 1.690 | -2.655 | 0.555 | 1.690 |
| SS | Context only | ElasticNet | log1p | 106 | 276 | 114 | 161727 | -7030010 | 0.415 | 1.995 | -4.095 | 0.415 | 1.995 |
| SS | Context only | Ridge | log1p | 106 | 276 | 114 | 2462691 | -1630095493 | 0.383 | 2.920 | -9.910 | 0.383 | 2.920 |
| TCB | S2 + Context | CatBoost | log1p | 138 | 276 | 114 | 8476 | 0.059 | 0.656 | 1.442 | 0.406 | 0.656 | 1.442 |
| TCB | S2 + Context | RandomForest | log1p | 138 | 276 | 114 | 8403 | 0.075 | 0.666 | 1.443 | 0.404 | 0.666 | 1.443 |
| TCB | Context only | Stacking_RidgeMeta | log1p | 106 | 276 | 114 | 8337 | 0.090 | 0.642 | 1.446 | 0.402 | 0.642 | 1.446 |
| TCB | S2 + Context | ExtraTrees | log1p | 138 | 276 | 114 | 8566 | 0.039 | 0.646 | 1.451 | 0.398 | 0.646 | 1.451 |
| TCB | S2 + Context | Stacking_RidgeMeta | log1p | 138 | 276 | 114 | 8524 | 0.048 | 0.643 | 1.463 | 0.388 | 0.643 | 1.463 |
| TCB | Context only | XGBoost | log1p | 106 | 276 | 114 | 8351 | 0.087 | 0.655 | 1.465 | 0.386 | 0.655 | 1.465 |
| TCB | Context only | ExtraTrees | log1p | 106 | 276 | 114 | 8530 | 0.047 | 0.641 | 1.469 | 0.383 | 0.641 | 1.469 |
| TCB | Context only | CatBoost | log1p | 106 | 276 | 114 | 8386 | 0.079 | 0.647 | 1.470 | 0.382 | 0.647 | 1.470 |
| TCB | Context only | RandomForest | log1p | 106 | 276 | 114 | 8324 | 0.093 | 0.650 | 1.470 | 0.382 | 0.650 | 1.470 |
| TCB | S2 + Context | XGBoost | log1p | 138 | 276 | 114 | 8379 | 0.080 | 0.632 | 1.482 | 0.371 | 0.632 | 1.482 |
| TCB | S2 only | RandomForest | log1p | 32 | 276 | 114 | 8763 | -0.006 | 0.409 | 1.648 | 0.223 | 0.409 | 1.648 |
| TCB | S2 only | ElasticNet | log1p | 32 | 276 | 114 | 8684 | 0.012 | 0.412 | 1.661 | 0.211 | 0.412 | 1.661 |
| TCB | S2 only | Stacking_RidgeMeta | log1p | 32 | 276 | 114 | 8933 | -0.045 | 0.404 | 1.667 | 0.205 | 0.404 | 1.667 |
| TCB | S2 only | Ridge | log1p | 32 | 276 | 114 | 8930 | -0.044 | 0.362 | 1.676 | 0.197 | 0.362 | 1.676 |
| TCB | S2 only | ExtraTrees | log1p | 32 | 276 | 114 | 8679 | 0.014 | 0.357 | 1.696 | 0.178 | 0.357 | 1.696 |
| TCB | Context only | ElasticNet | log1p | 106 | 276 | 114 | 7321 | 0.298 | 0.476 | 1.734 | 0.140 | 0.476 | 1.734 |
| TCB | S2 only | CatBoost | log1p | 32 | 276 | 114 | 8945 | -0.048 | 0.344 | 1.744 | 0.130 | 0.344 | 1.744 |
| TCB | Context only | Ridge | log1p | 106 | 276 | 114 | 8159 | 0.128 | 0.475 | 1.760 | 0.114 | 0.475 | 1.760 |
| TCB | S2 only | XGBoost | log1p | 32 | 276 | 114 | 8759 | -0.005 | 0.335 | 1.785 | 0.089 | 0.335 | 1.785 |
| TCB | S2 + Context | ElasticNet | log1p | 138 | 276 | 114 | 7748 | 0.214 | 0.453 | 1.805 | 0.068 | 0.453 | 1.805 |
| TCB | S2 + Context | Ridge | log1p | 138 | 276 | 114 | 8360 | 0.085 | 0.459 | 1.840 | 0.032 | 0.459 | 1.840 |
| TCB | S2 only | DummyMedian | log1p | 32 | 276 | 114 | 9202 | -0.109 |  | 1.931 | -0.067 |  | 1.931 |
| TCB | Context only | DummyMedian | log1p | 106 | 276 | 114 | 9202 | -0.109 |  | 1.931 | -0.067 |  | 1.931 |
| TCB | S2 + Context | DummyMedian | log1p | 138 | 276 | 114 | 9202 | -0.109 |  | 1.931 | -0.067 |  | 1.931 |
| Turbidity | S2 + Context | Stacking_RidgeMeta | log1p | 138 | 276 | 114 | 54.053 | 0.262 | 0.697 | 0.770 | 0.480 | 0.697 | 0.770 |
| Turbidity | S2 only | Stacking_RidgeMeta | log1p | 32 | 276 | 114 | 57.306 | 0.170 | 0.679 | 0.797 | 0.442 | 0.679 | 0.797 |
| Turbidity | S2 + Context | CatBoost | log1p | 138 | 276 | 114 | 55.613 | 0.219 | 0.676 | 0.807 | 0.428 | 0.676 | 0.807 |
| Turbidity | S2 only | CatBoost | log1p | 32 | 276 | 114 | 54.007 | 0.263 | 0.667 | 0.808 | 0.426 | 0.667 | 0.808 |
| Turbidity | S2 + Context | RandomForest | log1p | 138 | 276 | 114 | 57.191 | 0.174 | 0.677 | 0.809 | 0.425 | 0.677 | 0.809 |
| Turbidity | S2 only | ElasticNet | log1p | 32 | 276 | 114 | 56.893 | 0.182 | 0.674 | 0.810 | 0.423 | 0.674 | 0.810 |
| Turbidity | S2 only | ExtraTrees | log1p | 32 | 276 | 114 | 56.262 | 0.200 | 0.670 | 0.817 | 0.414 | 0.670 | 0.817 |
| Turbidity | S2 only | Ridge | log1p | 32 | 276 | 114 | 57.856 | 0.154 | 0.664 | 0.825 | 0.403 | 0.664 | 0.825 |
| Turbidity | S2 only | RandomForest | log1p | 32 | 276 | 114 | 57.300 | 0.170 | 0.675 | 0.825 | 0.401 | 0.675 | 0.825 |
| Turbidity | S2 + Context | ExtraTrees | log1p | 138 | 276 | 114 | 58.602 | 0.132 | 0.664 | 0.836 | 0.385 | 0.664 | 0.836 |
| Turbidity | S2 + Context | Ridge | log1p | 138 | 276 | 114 | 169.167 | -6.230 | 0.656 | 0.842 | 0.377 | 0.656 | 0.842 |
| Turbidity | S2 only | XGBoost | log1p | 32 | 276 | 114 | 53.107 | 0.287 | 0.641 | 0.842 | 0.376 | 0.641 | 0.842 |
| Turbidity | Context only | Stacking_RidgeMeta | log1p | 106 | 276 | 114 | 58.663 | 0.131 | 0.580 | 0.853 | 0.361 | 0.580 | 0.853 |
| Turbidity | Context only | CatBoost | log1p | 106 | 276 | 114 | 57.559 | 0.163 | 0.549 | 0.873 | 0.330 | 0.549 | 0.873 |
| Turbidity | S2 + Context | XGBoost | log1p | 138 | 276 | 114 | 55.907 | 0.210 | 0.646 | 0.879 | 0.322 | 0.646 | 0.879 |
| Turbidity | Context only | RandomForest | log1p | 106 | 276 | 114 | 60.513 | 0.075 | 0.551 | 0.891 | 0.302 | 0.551 | 0.891 |
| Turbidity | Context only | XGBoost | log1p | 106 | 276 | 114 | 57.101 | 0.176 | 0.569 | 0.893 | 0.299 | 0.569 | 0.893 |
| Turbidity | Context only | ExtraTrees | log1p | 106 | 276 | 114 | 62.338 | 0.018 | 0.572 | 0.920 | 0.256 | 0.572 | 0.920 |
| Turbidity | Context only | Ridge | log1p | 106 | 276 | 114 | 48.561 | 0.404 | 0.494 | 0.977 | 0.162 | 0.494 | 0.977 |
| Turbidity | S2 + Context | ElasticNet | log1p | 138 | 276 | 114 | 43.439 | 0.523 | 0.542 | 0.980 | 0.157 | 0.542 | 0.980 |
| Turbidity | S2 only | DummyMedian | log1p | 32 | 276 | 114 | 66.887 | -0.130 |  | 1.090 | -0.044 |  | 1.090 |
| Turbidity | Context only | DummyMedian | log1p | 106 | 276 | 114 | 66.887 | -0.130 |  | 1.090 | -0.044 |  | 1.090 |
| Turbidity | S2 + Context | DummyMedian | log1p | 138 | 276 | 114 | 66.887 | -0.130 |  | 1.090 | -0.044 |  | 1.090 |
| Turbidity | Context only | ElasticNet | log1p | 106 | 276 | 114 | 53.306 | 0.282 | 0.387 | 1.201 | -0.268 | 0.387 | 1.201 |

## Manual temporal NH3 classification: all configs

| target | feature_set | model | n_features | n_train | n_test | accuracy | balanced_accuracy | macro_f1 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| NH3_3class | Context only | Logistic | 106 | 276 | 114 | 0.447 | 0.424 | 0.425 |
| NH3_3class | S2 + Context | Logistic | 138 | 276 | 114 | 0.447 | 0.420 | 0.418 |
| NH3_3class | S2 + Context | ExtraTrees | 138 | 276 | 114 | 0.482 | 0.435 | 0.368 |
| NH3_3class | Context only | Stacking_LogisticMeta | 106 | 276 | 114 | 0.404 | 0.386 | 0.356 |
| NH3_3class | S2 + Context | Stacking_LogisticMeta | 138 | 276 | 114 | 0.404 | 0.381 | 0.348 |
| NH3_3class | Context only | ExtraTrees | 106 | 276 | 114 | 0.447 | 0.407 | 0.334 |
| NH3_3class | S2 only | ExtraTrees | 32 | 276 | 114 | 0.368 | 0.348 | 0.333 |
| NH3_3class | Context only | RandomForest | 106 | 276 | 114 | 0.447 | 0.408 | 0.329 |
| NH3_3class | S2 only | Logistic | 32 | 276 | 114 | 0.333 | 0.332 | 0.327 |
| NH3_3class | S2 + Context | RandomForest | 138 | 276 | 114 | 0.456 | 0.408 | 0.325 |
| NH3_3class | Context only | XGBoost | 106 | 276 | 114 | 0.439 | 0.400 | 0.324 |
| NH3_3class | S2 only | XGBoost | 32 | 276 | 114 | 0.351 | 0.333 | 0.316 |
| NH3_3class | S2 + Context | XGBoost | 138 | 276 | 114 | 0.421 | 0.384 | 0.315 |
| NH3_3class | S2 only | Stacking_LogisticMeta | 32 | 276 | 114 | 0.325 | 0.310 | 0.306 |
| NH3_3class | Context only | CatBoost | 106 | 276 | 114 | 0.439 | 0.395 | 0.303 |
| NH3_3class | S2 only | RandomForest | 32 | 276 | 114 | 0.333 | 0.310 | 0.296 |
| NH3_3class | S2 + Context | CatBoost | 138 | 276 | 114 | 0.430 | 0.388 | 0.292 |
| NH3_3class | S2 only | CatBoost | 32 | 276 | 114 | 0.360 | 0.322 | 0.255 |
| NH3_3class | S2 only | DummyMostFrequent | 32 | 276 | 114 | 0.360 | 0.333 | 0.176 |
| NH3_3class | Context only | DummyMostFrequent | 106 | 276 | 114 | 0.360 | 0.333 | 0.176 |
| NH3_3class | S2 + Context | DummyMostFrequent | 138 | 276 | 114 | 0.360 | 0.333 | 0.176 |
| NH3_binary | S2 + Context | ExtraTrees | 138 | 276 | 114 | 0.614 | 0.683 | 0.613 |
| NH3_binary | S2 + Context | RandomForest | 138 | 276 | 114 | 0.596 | 0.669 | 0.594 |
| NH3_binary | Context only | ExtraTrees | 106 | 276 | 114 | 0.588 | 0.657 | 0.586 |
| NH3_binary | S2 + Context | Stacking_LogisticMeta | 138 | 276 | 114 | 0.561 | 0.625 | 0.560 |
| NH3_binary | Context only | RandomForest | 106 | 276 | 114 | 0.561 | 0.636 | 0.558 |
| NH3_binary | Context only | Stacking_LogisticMeta | 106 | 276 | 114 | 0.544 | 0.606 | 0.543 |
| NH3_binary | S2 + Context | Logistic | 138 | 276 | 114 | 0.535 | 0.530 | 0.522 |
| NH3_binary | Context only | Logistic | 106 | 276 | 114 | 0.535 | 0.525 | 0.519 |
| NH3_binary | S2 + Context | CatBoost | 138 | 276 | 114 | 0.518 | 0.586 | 0.515 |
| NH3_binary | S2 + Context | XGBoost | 138 | 276 | 114 | 0.500 | 0.561 | 0.498 |
| NH3_binary | Context only | CatBoost | 106 | 276 | 114 | 0.500 | 0.572 | 0.495 |
| NH3_binary | Context only | XGBoost | 106 | 276 | 114 | 0.491 | 0.549 | 0.490 |
| NH3_binary | S2 only | Logistic | 32 | 276 | 114 | 0.491 | 0.469 | 0.468 |
| NH3_binary | S2 only | Stacking_LogisticMeta | 32 | 276 | 114 | 0.465 | 0.465 | 0.455 |
| NH3_binary | S2 only | RandomForest | 32 | 276 | 114 | 0.421 | 0.457 | 0.421 |
| NH3_binary | S2 only | XGBoost | 32 | 276 | 114 | 0.421 | 0.457 | 0.421 |
| NH3_binary | S2 only | CatBoost | 32 | 276 | 114 | 0.421 | 0.462 | 0.421 |
| NH3_binary | S2 only | ExtraTrees | 32 | 276 | 114 | 0.404 | 0.438 | 0.404 |
| NH3_binary | S2 only | DummyMostFrequent | 32 | 276 | 114 | 0.360 | 0.500 | 0.265 |
| NH3_binary | Context only | DummyMostFrequent | 106 | 276 | 114 | 0.360 | 0.500 | 0.265 |
| NH3_binary | S2 + Context | DummyMostFrequent | 138 | 276 | 114 | 0.360 | 0.500 | 0.265 |

## Manual station-temporal regression: aggregated all configs

The station-temporal table aggregates 3 folds. Lower RMSE is better. For log1p targets, model-scale RMSE is the main ranking metric.

| target | feature_set | model | transform | n_test_sum | original_rmse_mean | original_rmse_std | original_r2_mean | original_spearman_r_mean | modelscale_rmse_mean | modelscale_r2_mean | modelscale_spearman_r_mean | rank_metric_mean |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| BOD | Context only | Ridge | raw | 114 | 0.763 | 0.115 | 0.075 | 0.346 | 1.010 | -0.523 | 0.346 | 0.763 |
| BOD | S2 + Context | Ridge | raw | 114 | 0.796 | 0.033 | -0.151 | 0.432 | 1.027 | -0.685 | 0.432 | 0.796 |
| BOD | S2 + Context | CatBoost | raw | 114 | 0.824 | 0.148 | -0.097 | 0.344 | 0.824 | -0.097 | 0.344 | 0.824 |
| BOD | Context only | CatBoost | raw | 114 | 0.855 | 0.180 | -0.138 | 0.198 | 0.855 | -0.138 | 0.198 | 0.855 |
| BOD | Context only | Stacking_RidgeMeta | raw | 114 | 0.873 | 0.135 | -0.219 | 0.221 | 0.874 | -0.221 | 0.221 | 0.873 |
| BOD | S2 + Context | XGBoost | raw | 114 | 0.874 | 0.098 | -0.342 | 0.308 | 0.874 | -0.342 | 0.308 | 0.874 |
| BOD | Context only | ExtraTrees | raw | 114 | 0.877 | 0.159 | -0.214 | 0.184 | 0.877 | -0.214 | 0.184 | 0.877 |
| BOD | Context only | RandomForest | raw | 114 | 0.880 | 0.120 | -0.263 | 0.238 | 0.880 | -0.263 | 0.238 | 0.880 |
| BOD | Context only | XGBoost | raw | 114 | 0.880 | 0.131 | -0.264 | 0.179 | 0.880 | -0.264 | 0.179 | 0.880 |
| BOD | S2 + Context | ExtraTrees | raw | 114 | 0.884 | 0.122 | -0.401 | 0.343 | 0.884 | -0.401 | 0.343 | 0.884 |
| BOD | S2 + Context | Stacking_RidgeMeta | raw | 114 | 0.890 | 0.104 | -0.408 | 0.332 | 0.898 | -0.423 | 0.332 | 0.890 |
| BOD | Context only | DummyMedian | raw | 114 | 0.892 | 0.271 | -0.149 |  | 0.892 | -0.149 |  | 0.892 |
| BOD | S2 + Context | DummyMedian | raw | 114 | 0.892 | 0.271 | -0.149 |  | 0.892 | -0.149 |  | 0.892 |
| BOD | S2 only | DummyMedian | raw | 114 | 0.892 | 0.271 | -0.149 |  | 0.892 | -0.149 |  | 0.892 |
| BOD | S2 + Context | RandomForest | raw | 114 | 0.905 | 0.143 | -0.560 | 0.336 | 0.905 | -0.560 | 0.336 | 0.905 |
| BOD | S2 only | CatBoost | raw | 114 | 0.911 | 0.139 | -0.622 | 0.446 | 0.911 | -0.622 | 0.446 | 0.911 |
| BOD | S2 only | XGBoost | raw | 114 | 0.916 | 0.169 | -0.721 | 0.451 | 0.916 | -0.721 | 0.451 | 0.916 |
| BOD | S2 only | Stacking_RidgeMeta | raw | 114 | 0.916 | 0.119 | -0.531 | 0.419 | 0.916 | -0.531 | 0.419 | 0.916 |
| BOD | S2 only | RandomForest | raw | 114 | 0.939 | 0.201 | -0.848 | 0.493 | 0.939 | -0.848 | 0.493 | 0.939 |
| BOD | S2 only | Ridge | raw | 114 | 0.961 | 0.249 | -0.984 | 0.451 | 0.961 | -0.984 | 0.451 | 0.961 |
| BOD | S2 only | ElasticNet | raw | 114 | 0.974 | 0.284 | -1.121 | 0.414 | 0.974 | -1.121 | 0.414 | 0.974 |
| BOD | S2 only | ExtraTrees | raw | 114 | 1.023 | 0.252 | -1.287 | 0.417 | 1.023 | -1.287 | 0.417 | 1.023 |
| BOD | S2 + Context | ElasticNet | raw | 114 | 1.114 | 0.377 | -2.009 | 0.336 | 1.371 | -2.792 | 0.336 | 1.114 |
| BOD | Context only | ElasticNet | raw | 114 | 1.208 | 0.500 | -2.859 | 0.228 | 1.360 | -3.274 | 0.228 | 1.208 |
| DO | Context only | DummyMedian | raw | 114 | 1.218 | 0.190 | -0.198 |  | 1.218 | -0.198 |  | 1.218 |
| DO | S2 + Context | DummyMedian | raw | 114 | 1.218 | 0.190 | -0.198 |  | 1.218 | -0.198 |  | 1.218 |
| DO | S2 only | DummyMedian | raw | 114 | 1.218 | 0.190 | -0.198 |  | 1.218 | -0.198 |  | 1.218 |
| DO | S2 only | Ridge | raw | 114 | 1.235 | 0.095 | -0.312 | 0.235 | 1.235 | -0.312 | 0.235 | 1.235 |
| DO | S2 only | ExtraTrees | raw | 114 | 1.249 | 0.145 | -0.348 | 0.315 | 1.249 | -0.348 | 0.315 | 1.249 |
| DO | S2 + Context | ExtraTrees | raw | 114 | 1.255 | 0.090 | -0.412 | 0.179 | 1.255 | -0.412 | 0.179 | 1.255 |
| DO | S2 only | Stacking_RidgeMeta | raw | 114 | 1.256 | 0.115 | -0.341 | 0.199 | 1.256 | -0.341 | 0.199 | 1.256 |
| DO | S2 only | ElasticNet | raw | 114 | 1.276 | 0.108 | -0.427 | 0.237 | 1.276 | -0.427 | 0.237 | 1.276 |
| DO | S2 only | RandomForest | raw | 114 | 1.283 | 0.081 | -0.474 | 0.276 | 1.283 | -0.474 | 0.276 | 1.283 |
| DO | Context only | ExtraTrees | raw | 114 | 1.291 | 0.128 | -0.459 | 0.098 | 1.291 | -0.459 | 0.098 | 1.291 |
| DO | S2 + Context | XGBoost | raw | 114 | 1.310 | 0.152 | -0.599 | 0.197 | 1.310 | -0.599 | 0.197 | 1.310 |
| DO | S2 + Context | RandomForest | raw | 114 | 1.313 | 0.136 | -0.542 | 0.142 | 1.313 | -0.542 | 0.142 | 1.313 |
| DO | S2 + Context | CatBoost | raw | 114 | 1.317 | 0.114 | -0.584 | 0.210 | 1.317 | -0.584 | 0.210 | 1.317 |
| DO | Context only | RandomForest | raw | 114 | 1.355 | 0.151 | -0.634 | 0.096 | 1.355 | -0.634 | 0.096 | 1.355 |
| DO | Context only | Stacking_RidgeMeta | raw | 114 | 1.366 | 0.235 | -0.637 | 0.139 | 1.366 | -0.637 | 0.139 | 1.366 |
| DO | Context only | XGBoost | raw | 114 | 1.377 | 0.206 | -0.736 | 0.128 | 1.377 | -0.736 | 0.128 | 1.377 |
| DO | Context only | CatBoost | raw | 114 | 1.388 | 0.133 | -0.754 | 0.156 | 1.388 | -0.754 | 0.156 | 1.388 |
| DO | S2 + Context | Stacking_RidgeMeta | raw | 114 | 1.389 | 0.144 | -0.765 | 0.191 | 1.389 | -0.765 | 0.191 | 1.389 |
| DO | S2 only | CatBoost | raw | 114 | 1.405 | 0.178 | -0.857 | 0.185 | 1.405 | -0.857 | 0.185 | 1.405 |
| DO | S2 only | XGBoost | raw | 114 | 1.429 | 0.133 | -0.887 | 0.220 | 1.429 | -0.887 | 0.220 | 1.429 |
| DO | Context only | Ridge | raw | 114 | 2.929 | 2.106 | -6.030 | 0.273 | 3.700 | -9.584 | 0.273 | 2.929 |
| DO | S2 + Context | Ridge | raw | 114 | 3.179 | 2.250 | -7.182 | 0.308 | 4.000 | -11.433 | 0.308 | 3.179 |
| DO | Context only | ElasticNet | raw | 114 | 3.690 | 2.865 | -10.201 | 0.068 | 4.401 | -14.821 | 0.068 | 3.690 |
| DO | S2 + Context | ElasticNet | raw | 114 | 4.389 | 3.353 | -15.144 | 0.135 | 5.202 | -20.497 | 0.135 | 4.389 |
| FCB | S2 only | Stacking_RidgeMeta | log1p | 114 | 3291 | 633.284 | -0.115 | 0.164 | 2.014 | -0.052 | 0.164 | 2.014 |
| FCB | Context only | DummyMedian | log1p | 114 | 3346 | 647.359 | -0.151 |  | 2.029 | -0.062 |  | 2.029 |
| FCB | S2 + Context | DummyMedian | log1p | 114 | 3346 | 647.359 | -0.151 |  | 2.029 | -0.062 |  | 2.029 |
| FCB | S2 only | DummyMedian | log1p | 114 | 3346 | 647.359 | -0.151 |  | 2.029 | -0.062 |  | 2.029 |
| FCB | S2 + Context | RandomForest | log1p | 114 | 3198 | 564.007 | -0.055 | 0.257 | 2.031 | -0.061 | 0.257 | 2.031 |
| FCB | S2 only | RandomForest | log1p | 114 | 3250 | 594.461 | -0.090 | 0.158 | 2.034 | -0.071 | 0.158 | 2.034 |
| FCB | S2 + Context | CatBoost | log1p | 114 | 3184 | 567.968 | -0.048 | 0.220 | 2.055 | -0.087 | 0.220 | 2.055 |
| FCB | Context only | RandomForest | log1p | 114 | 3198 | 570.448 | -0.054 | 0.241 | 2.059 | -0.093 | 0.241 | 2.059 |
| FCB | S2 only | Ridge | log1p | 114 | 3317 | 606.151 | -0.134 | 0.104 | 2.070 | -0.125 | 0.104 | 2.070 |
| FCB | S2 + Context | ExtraTrees | log1p | 114 | 3225 | 497.747 | -0.077 | 0.149 | 2.070 | -0.100 | 0.149 | 2.070 |
| FCB | Context only | CatBoost | log1p | 114 | 3229 | 555.790 | -0.076 | 0.167 | 2.077 | -0.107 | 0.167 | 2.077 |
| FCB | S2 only | ElasticNet | log1p | 114 | 3277 | 523.356 | -0.112 | 0.135 | 2.077 | -0.135 | 0.135 | 2.077 |
| FCB | S2 + Context | Stacking_RidgeMeta | log1p | 114 | 3178 | 605.496 | -0.039 | 0.139 | 2.117 | -0.147 | 0.139 | 2.117 |
| FCB | S2 only | ExtraTrees | log1p | 114 | 3225 | 554.320 | -0.076 | 0.110 | 2.122 | -0.180 | 0.110 | 2.122 |
| FCB | S2 + Context | XGBoost | log1p | 114 | 3169 | 561.297 | -0.041 | 0.203 | 2.126 | -0.162 | 0.203 | 2.126 |
| FCB | Context only | ExtraTrees | log1p | 114 | 3217 | 521.932 | -0.070 | 0.100 | 2.129 | -0.157 | 0.100 | 2.129 |
| FCB | Context only | XGBoost | log1p | 114 | 3181 | 543.575 | -0.044 | 0.181 | 2.148 | -0.194 | 0.181 | 2.148 |
| FCB | S2 only | XGBoost | log1p | 114 | 3253 | 601.709 | -0.092 | 0.089 | 2.188 | -0.244 | 0.089 | 2.188 |
| FCB | S2 only | CatBoost | log1p | 114 | 3261 | 611.537 | -0.098 | 0.094 | 2.198 | -0.254 | 0.094 | 2.198 |
| FCB | Context only | Stacking_RidgeMeta | log1p | 114 | 3305 | 654.459 | -0.123 | -0.079 | 2.289 | -0.335 | -0.079 | 2.289 |
| FCB | Context only | Ridge | log1p | 114 | 1881181 | 3253456 | -794949 | 0.009 | 3.955 | -4.574 | 0.010 | 3.955 |
| FCB | S2 + Context | Ridge | log1p | 114 | 470070 | 808211 | -49250 | -0.037 | 4.242 | -4.655 | -0.037 | 4.242 |
| FCB | S2 + Context | ElasticNet | log1p | 114 | 2230769 | 3763493 | -1082075 | -0.085 | 4.578 | -4.761 | -0.085 | 4.578 |
| FCB | Context only | ElasticNet | log1p | 114 | 1520407 | 1963778 | -380262 | -0.140 | 4.800 | -5.440 | -0.140 | 4.800 |
| SS | S2 only | Ridge | log1p | 114 | 47.301 | 44.895 | 0.196 | 0.645 | 0.706 | 0.278 | 0.645 | 0.706 |
| SS | S2 only | ElasticNet | log1p | 114 | 47.411 | 44.388 | 0.183 | 0.614 | 0.723 | 0.245 | 0.614 | 0.723 |
| SS | S2 + Context | ExtraTrees | log1p | 114 | 46.323 | 45.898 | 0.255 | 0.541 | 0.731 | 0.237 | 0.541 | 0.731 |
| SS | S2 + Context | RandomForest | log1p | 114 | 46.180 | 45.465 | 0.253 | 0.539 | 0.741 | 0.214 | 0.539 | 0.741 |
| SS | S2 only | Stacking_RidgeMeta | log1p | 114 | 48.264 | 44.433 | 0.137 | 0.576 | 0.747 | 0.193 | 0.576 | 0.747 |
| SS | S2 + Context | CatBoost | log1p | 114 | 47.572 | 45.329 | 0.180 | 0.518 | 0.749 | 0.200 | 0.518 | 0.749 |
| SS | S2 only | RandomForest | log1p | 114 | 48.476 | 43.698 | 0.098 | 0.551 | 0.760 | 0.154 | 0.551 | 0.760 |
| SS | S2 + Context | Stacking_RidgeMeta | log1p | 114 | 46.794 | 45.701 | 0.225 | 0.505 | 0.764 | 0.169 | 0.505 | 0.764 |
| SS | S2 only | ExtraTrees | log1p | 114 | 48.241 | 44.813 | 0.125 | 0.520 | 0.787 | 0.094 | 0.520 | 0.787 |
| SS | S2 + Context | XGBoost | log1p | 114 | 47.504 | 45.579 | 0.178 | 0.443 | 0.806 | 0.071 | 0.443 | 0.806 |
| SS | S2 only | CatBoost | log1p | 114 | 48.469 | 45.060 | 0.124 | 0.439 | 0.809 | 0.063 | 0.439 | 0.809 |
| SS | Context only | Stacking_RidgeMeta | log1p | 114 | 49.013 | 45.365 | 0.130 | 0.429 | 0.811 | 0.070 | 0.429 | 0.811 |
| SS | Context only | ExtraTrees | log1p | 114 | 48.718 | 45.126 | 0.144 | 0.387 | 0.813 | 0.069 | 0.387 | 0.813 |
| SS | S2 only | XGBoost | log1p | 114 | 49.282 | 43.685 | 0.050 | 0.425 | 0.831 | -0.001 | 0.425 | 0.831 |
| SS | Context only | CatBoost | log1p | 114 | 49.042 | 45.229 | 0.130 | 0.375 | 0.838 | 0.009 | 0.375 | 0.838 |
| SS | Context only | RandomForest | log1p | 114 | 49.771 | 43.857 | 0.065 | 0.326 | 0.846 | -0.014 | 0.326 | 0.846 |
| SS | Context only | XGBoost | log1p | 114 | 49.265 | 45.086 | 0.116 | 0.303 | 0.870 | -0.066 | 0.303 | 0.870 |
| SS | Context only | DummyMedian | log1p | 114 | 52.479 | 43.406 | -0.099 |  | 0.920 | -0.198 |  | 0.920 |
| SS | S2 + Context | DummyMedian | log1p | 114 | 52.479 | 43.406 | -0.099 |  | 0.920 | -0.198 |  | 0.920 |
| SS | S2 only | DummyMedian | log1p | 114 | 52.479 | 43.406 | -0.099 |  | 0.920 | -0.198 |  | 0.920 |
| SS | S2 + Context | Ridge | log1p | 114 | 650.737 | 546.080 | -361.483 | 0.208 | 1.936 | -4.328 | 0.207 | 1.936 |
| SS | S2 + Context | ElasticNet | log1p | 114 | 3729 | 3907 | -22620 | 0.123 | 2.762 | -9.773 | 0.126 | 2.762 |
| SS | Context only | Ridge | log1p | 114 | 2148 | 3243 | -1344 | -0.049 | 2.907 | -11.825 | -0.043 | 2.907 |
| SS | Context only | ElasticNet | log1p | 114 | 22712 | 38100 | -1617852 | 0.025 | 3.321 | -14.746 | 0.033 | 3.321 |
| TCB | S2 + Context | CatBoost | log1p | 114 | 8479 | 3453 | -0.017 | 0.388 | 1.748 | 0.043 | 0.388 | 1.748 |
| TCB | S2 only | Stacking_RidgeMeta | log1p | 114 | 8414 | 3045 | -0.021 | 0.321 | 1.781 | 0.009 | 0.321 | 1.781 |
| TCB | S2 + Context | RandomForest | log1p | 114 | 8532 | 3451 | -0.031 | 0.342 | 1.794 | 0.001 | 0.342 | 1.794 |
| TCB | S2 only | ElasticNet | log1p | 114 | 8364 | 2835 | -0.024 | 0.323 | 1.795 | -0.036 | 0.323 | 1.795 |
| TCB | Context only | RandomForest | log1p | 114 | 8442 | 3400 | -0.011 | 0.324 | 1.796 | -0.003 | 0.324 | 1.796 |
| TCB | Context only | CatBoost | log1p | 114 | 8357 | 3298 | 0.006 | 0.266 | 1.803 | -0.007 | 0.266 | 1.803 |
| TCB | S2 only | Ridge | log1p | 114 | 8514 | 3047 | -0.047 | 0.282 | 1.838 | -0.067 | 0.282 | 1.838 |
| TCB | S2 + Context | XGBoost | log1p | 114 | 8912 | 3062 | -0.154 | 0.373 | 1.844 | -0.066 | 0.373 | 1.844 |
| TCB | S2 + Context | ExtraTrees | log1p | 114 | 8581 | 3187 | -0.057 | 0.234 | 1.859 | -0.065 | 0.234 | 1.859 |
| TCB | S2 only | RandomForest | log1p | 114 | 8341 | 3429 | 0.014 | 0.199 | 1.869 | -0.092 | 0.199 | 1.869 |
| TCB | Context only | DummyMedian | log1p | 114 | 8853 | 3242 | -0.127 |  | 1.876 | -0.088 |  | 1.876 |
| TCB | S2 + Context | DummyMedian | log1p | 114 | 8853 | 3242 | -0.127 |  | 1.876 | -0.088 |  | 1.876 |
| TCB | S2 only | DummyMedian | log1p | 114 | 8853 | 3242 | -0.127 |  | 1.876 | -0.088 |  | 1.876 |
| TCB | Context only | XGBoost | log1p | 114 | 8473 | 3558 | -0.011 | 0.340 | 1.879 | -0.106 | 0.340 | 1.879 |
| TCB | Context only | ExtraTrees | log1p | 114 | 8596 | 3180 | -0.061 | 0.138 | 1.933 | -0.144 | 0.138 | 1.933 |
| TCB | S2 only | CatBoost | log1p | 114 | 8372 | 3514 | 0.012 | 0.187 | 1.959 | -0.217 | 0.187 | 1.959 |
| TCB | S2 only | ExtraTrees | log1p | 114 | 8378 | 3321 | -0.001 | 0.158 | 1.967 | -0.220 | 0.158 | 1.967 |
| TCB | S2 + Context | Stacking_RidgeMeta | log1p | 114 | 9485 | 5030 | -0.235 | 0.139 | 1.989 | -0.223 | 0.139 | 1.989 |
| TCB | S2 only | XGBoost | log1p | 114 | 8201 | 3572 | 0.054 | 0.130 | 2.026 | -0.286 | 0.130 | 2.026 |
| TCB | Context only | Stacking_RidgeMeta | log1p | 114 | 10417 | 6120 | -0.495 | -0.010 | 2.316 | -0.699 | -0.010 | 2.316 |
| TCB | S2 + Context | Ridge | log1p | 114 | 8073191 | 13966724 | -1519625 | 0.031 | 3.364 | -3.390 | 0.031 | 3.364 |
| TCB | Context only | Ridge | log1p | 114 | 2040584 | 3521839 | -96778 | -0.067 | 3.687 | -4.893 | -0.066 | 3.687 |
| TCB | S2 + Context | ElasticNet | log1p | 114 | 25476771 | 43796578 | -15007341 | -0.065 | 4.237 | -5.131 | -0.065 | 4.237 |
| TCB | Context only | ElasticNet | log1p | 114 | 12919966 | 11752233 | -5913994 | -0.205 | 5.234 | -8.418 | -0.204 | 5.234 |
| Turbidity | S2 only | ElasticNet | log1p | 114 | 52.112 | 28.744 | 0.209 | 0.630 | 0.812 | 0.370 | 0.630 | 0.812 |
| Turbidity | S2 only | Ridge | log1p | 114 | 53.525 | 29.262 | 0.172 | 0.628 | 0.818 | 0.360 | 0.628 | 0.818 |
| Turbidity | S2 only | Stacking_RidgeMeta | log1p | 114 | 53.061 | 28.663 | 0.186 | 0.591 | 0.823 | 0.356 | 0.591 | 0.823 |
| Turbidity | S2 only | CatBoost | log1p | 114 | 49.862 | 28.591 | 0.265 | 0.590 | 0.828 | 0.355 | 0.590 | 0.828 |
| Turbidity | S2 only | RandomForest | log1p | 114 | 53.054 | 26.349 | 0.158 | 0.615 | 0.833 | 0.335 | 0.615 | 0.833 |
| Turbidity | S2 only | ExtraTrees | log1p | 114 | 51.531 | 28.976 | 0.214 | 0.588 | 0.856 | 0.305 | 0.588 | 0.856 |
| Turbidity | S2 + Context | RandomForest | log1p | 114 | 53.051 | 26.687 | 0.178 | 0.578 | 0.863 | 0.298 | 0.578 | 0.863 |
| Turbidity | S2 only | XGBoost | log1p | 114 | 50.687 | 26.223 | 0.216 | 0.555 | 0.883 | 0.263 | 0.555 | 0.883 |
| Turbidity | S2 + Context | CatBoost | log1p | 114 | 53.742 | 27.873 | 0.153 | 0.574 | 0.884 | 0.270 | 0.574 | 0.884 |
| Turbidity | S2 + Context | Stacking_RidgeMeta | log1p | 114 | 53.704 | 29.509 | 0.173 | 0.514 | 0.890 | 0.259 | 0.514 | 0.890 |
| Turbidity | S2 + Context | ExtraTrees | log1p | 114 | 55.299 | 29.230 | 0.109 | 0.484 | 0.917 | 0.212 | 0.484 | 0.917 |
| Turbidity | S2 + Context | XGBoost | log1p | 114 | 51.689 | 28.352 | 0.212 | 0.489 | 0.932 | 0.187 | 0.489 | 0.932 |
| Turbidity | Context only | Stacking_RidgeMeta | log1p | 114 | 57.894 | 31.627 | 0.058 | 0.371 | 1.027 | 0.019 | 0.371 | 1.027 |
| Turbidity | Context only | CatBoost | log1p | 114 | 56.607 | 30.589 | 0.098 | 0.293 | 1.048 | -0.023 | 0.293 | 1.048 |
| Turbidity | Context only | RandomForest | log1p | 114 | 57.906 | 29.026 | 0.028 | 0.261 | 1.052 | -0.026 | 0.261 | 1.052 |
| Turbidity | Context only | ExtraTrees | log1p | 114 | 60.342 | 31.590 | -0.043 | 0.203 | 1.085 | -0.092 | 0.203 | 1.085 |
| Turbidity | Context only | DummyMedian | log1p | 114 | 62.446 | 30.236 | -0.142 |  | 1.094 | -0.112 |  | 1.094 |
| Turbidity | S2 + Context | DummyMedian | log1p | 114 | 62.446 | 30.236 | -0.142 |  | 1.094 | -0.112 |  | 1.094 |
| Turbidity | S2 only | DummyMedian | log1p | 114 | 62.446 | 30.236 | -0.142 |  | 1.094 | -0.112 |  | 1.094 |
| Turbidity | Context only | XGBoost | log1p | 114 | 56.142 | 28.112 | 0.079 | 0.214 | 1.134 | -0.201 | 0.214 | 1.134 |
| Turbidity | S2 + Context | Ridge | log1p | 114 | 2843 | 4783 | -3514 | 0.206 | 2.059 | -3.539 | 0.206 | 2.059 |
| Turbidity | S2 + Context | ElasticNet | log1p | 114 | 10007401 | 17332339 | -45227741613 | -0.003 | 2.774 | -6.553 | 0.007 | 2.774 |
| Turbidity | Context only | Ridge | log1p | 114 | 17050269099 | 29531932162 | -131297899659021056 | -0.059 | 3.018 | -9.620 | -0.054 | 3.018 |
| Turbidity | Context only | ElasticNet | log1p | 114 | 18599502 | 32182079 | -156027503158 | -0.164 | 3.946 | -14.144 | -0.153 | 3.946 |

## Manual station-temporal NH3 classification: aggregated all configs

| target | feature_set | model | n_test_sum | accuracy_mean | balanced_accuracy_mean | macro_f1_mean | macro_f1_std |
| --- | --- | --- | --- | --- | --- | --- | --- |
| NH3_3class | S2 + Context | Stacking_LogisticMeta | 114 | 0.447 | 0.415 | 0.412 | 0.049 |
| NH3_3class | S2 + Context | XGBoost | 114 | 0.456 | 0.457 | 0.404 | 0.141 |
| NH3_3class | Context only | ExtraTrees | 114 | 0.456 | 0.427 | 0.360 | 0.125 |
| NH3_3class | Context only | XGBoost | 114 | 0.430 | 0.425 | 0.356 | 0.148 |
| NH3_3class | Context only | Stacking_LogisticMeta | 114 | 0.395 | 0.431 | 0.355 | 0.122 |
| NH3_3class | S2 + Context | ExtraTrees | 114 | 0.491 | 0.438 | 0.352 | 0.046 |
| NH3_3class | Context only | Logistic | 114 | 0.386 | 0.380 | 0.344 | 0.088 |
| NH3_3class | S2 + Context | RandomForest | 114 | 0.447 | 0.402 | 0.327 | 0.033 |
| NH3_3class | Context only | RandomForest | 114 | 0.412 | 0.374 | 0.312 | 0.025 |
| NH3_3class | S2 + Context | Logistic | 114 | 0.342 | 0.322 | 0.312 | 0.033 |
| NH3_3class | S2 only | Stacking_LogisticMeta | 114 | 0.351 | 0.333 | 0.311 | 0.086 |
| NH3_3class | Context only | CatBoost | 114 | 0.439 | 0.394 | 0.305 | 0.041 |
| NH3_3class | S2 only | Logistic | 114 | 0.333 | 0.299 | 0.304 | 0.038 |
| NH3_3class | S2 only | ExtraTrees | 114 | 0.377 | 0.347 | 0.299 | 0.039 |
| NH3_3class | S2 + Context | CatBoost | 114 | 0.439 | 0.396 | 0.295 | 0.062 |
| NH3_3class | S2 only | XGBoost | 114 | 0.351 | 0.340 | 0.282 | 0.093 |
| NH3_3class | S2 only | CatBoost | 114 | 0.377 | 0.343 | 0.263 | 0.034 |
| NH3_3class | S2 only | RandomForest | 114 | 0.333 | 0.304 | 0.249 | 0.037 |
| NH3_3class | Context only | DummyMostFrequent | 114 | 0.360 | 0.333 | 0.175 | 0.029 |
| NH3_3class | S2 + Context | DummyMostFrequent | 114 | 0.360 | 0.333 | 0.175 | 0.029 |
| NH3_3class | S2 only | DummyMostFrequent | 114 | 0.360 | 0.333 | 0.175 | 0.029 |
| NH3_binary | S2 + Context | ExtraTrees | 114 | 0.632 | 0.694 | 0.627 | 0.043 |
| NH3_binary | S2 + Context | Stacking_LogisticMeta | 114 | 0.605 | 0.637 | 0.601 | 0.031 |
| NH3_binary | Context only | ExtraTrees | 114 | 0.579 | 0.653 | 0.576 | 0.066 |
| NH3_binary | S2 + Context | RandomForest | 114 | 0.570 | 0.631 | 0.568 | 0.066 |
| NH3_binary | Context only | RandomForest | 114 | 0.570 | 0.647 | 0.568 | 0.053 |
| NH3_binary | S2 + Context | CatBoost | 114 | 0.544 | 0.597 | 0.543 | 0.118 |
| NH3_binary | Context only | CatBoost | 114 | 0.544 | 0.615 | 0.542 | 0.054 |
| NH3_binary | S2 + Context | XGBoost | 114 | 0.544 | 0.582 | 0.539 | 0.059 |
| NH3_binary | Context only | Stacking_LogisticMeta | 114 | 0.535 | 0.577 | 0.533 | 0.017 |
| NH3_binary | Context only | XGBoost | 114 | 0.526 | 0.583 | 0.525 | 0.053 |
| NH3_binary | S2 + Context | Logistic | 114 | 0.535 | 0.538 | 0.522 | 0.056 |
| NH3_binary | S2 only | Logistic | 114 | 0.535 | 0.543 | 0.517 | 0.011 |
| NH3_binary | Context only | Logistic | 114 | 0.518 | 0.549 | 0.514 | 0.058 |
| NH3_binary | S2 only | Stacking_LogisticMeta | 114 | 0.474 | 0.481 | 0.461 | 0.057 |
| NH3_binary | S2 only | XGBoost | 114 | 0.430 | 0.487 | 0.425 | 0.086 |
| NH3_binary | S2 only | ExtraTrees | 114 | 0.430 | 0.466 | 0.419 | 0.099 |
| NH3_binary | S2 only | RandomForest | 114 | 0.421 | 0.459 | 0.407 | 0.042 |
| NH3_binary | S2 only | CatBoost | 114 | 0.412 | 0.477 | 0.404 | 0.059 |
| NH3_binary | Context only | DummyMostFrequent | 114 | 0.360 | 0.500 | 0.263 | 0.043 |
| NH3_binary | S2 + Context | DummyMostFrequent | 114 | 0.360 | 0.500 | 0.263 | 0.043 |
| NH3_binary | S2 only | DummyMostFrequent | 114 | 0.360 | 0.500 | 0.263 | 0.043 |

## Latest final selected registry from manual notebook

| task | target | feature_set | model | transform | n_train_final |
| --- | --- | --- | --- | --- | --- |
| regression | BOD | S2 + Context | CatBoost | raw | 390 |
| regression | DO | S2 + Context | CatBoost | raw | 390 |
| regression | FCB | S2 + Context | CatBoost | log1p | 390 |
| regression | SS | S2 + Context | RandomForest | log1p | 390 |
| regression | TCB | S2 + Context | CatBoost | log1p | 390 |
| regression | Turbidity | S2 only | Stacking_RidgeMeta | log1p | 390 |
| classification | NH3_3class | S2 + Context | ExtraTrees | label | 390 |
| classification | NH3_binary | S2 + Context | ExtraTrees | label | 390 |

## Main interpretation

- AutoGluon main and diagnostic are actual AutoGluon training experiments. AutoGluon report is aggregation only, not a new training experiment.
- AutoGluon WeightedEnsemble_L2/L3 should be treated as temporal-best model candidates because they often perform strongly on the temporal test.
- The latest manual baseline/stacking notebook adds station-temporal robustness evidence that old AutoGluon runs do not yet have.
- For final advisor reporting, separate two concepts: temporal-best models and station-temporal robust models.
- Turbidity and SS remain the strongest remote-sensing targets. DO has useful proxy signal but weaker unseen-station transfer. TCB, FCB, and NH3 should be framed as proxy/risk targets rather than direct measurement.
- NH3 binary classification is more usable than NH3 3-class classification in the latest experiment logs.