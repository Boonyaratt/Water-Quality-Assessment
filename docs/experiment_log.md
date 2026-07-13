# Experiment Log

The experiment summaries are stored in `reports/tables/`.

Main groups:

| Experiment | Split | Feature sets | Models | Purpose |
| --- | --- | --- | --- | --- |
| AutoGluon temporal | Temporal | S2 only, Context only, S2 + Context | WeightedEnsemble_L2/L3 | AutoML benchmark |
| Manual temporal | Temporal | S2 only, Context only, S2 + Context | Ridge, ElasticNet, RandomForest, ExtraTrees, XGBoost, CatBoost, Stacking | Reproducible baseline comparison |
| Manual station-temporal | Station + Temporal | S2 only, Context only, S2 + Context | Same manual models | Robustness and transferability test |

See:

- `reports/tables/full_experiment_log_report.md`
- `reports/tables/experiment_log_all_results.xlsx`
- `reports/tables/manual_station_temporal_regression_by_target_feature_report.md`

