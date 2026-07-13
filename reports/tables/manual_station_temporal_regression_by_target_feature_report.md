# Manual Station-Temporal Regression: By Target And Feature Set

This derived report keeps the original aggregated table unchanged and adds target-feature grouped rankings.

Ranking rule: raw targets use `original_rmse_mean`; log1p targets use `modelscale_rmse_mean`. DummyMedian is kept in ranked tables, while the best summary chooses the best non-dummy model.

## Output Files

- Original aggregated input: `E:\Water Quality Research\Reports\experiment_model_logs\manual_station_temporal_regression_aggregated.csv`
- Ranked all configs: `E:\Water Quality Research\Reports\experiment_model_logs\manual_station_temporal_regression_by_target_feature_ranked.csv`
- Best by target-feature: `E:\Water Quality Research\Reports\experiment_model_logs\manual_station_temporal_regression_best_by_target_feature.csv`
- Excel workbook: `E:\Water Quality Research\Reports\experiment_model_logs\manual_station_temporal_regression_by_target_feature.xlsx`

## Best Non-Dummy Model By Target And Feature Set

| target | feature_set | model | transform | selection_metric_name | select_rmse | select_r2 | select_spearman | orig_rmse | orig_r2 | model_rmse | model_r2 | best_model_including_dummy |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| BOD | S2 only | CatBoost | raw | original_rmse_mean | 0.9108 | -0.6222 | 0.4461 | 0.9108 | -0.6222 | 0.9108 | -0.6222 | DummyMedian |
| BOD | Context only | Ridge | raw | original_rmse_mean | 0.7625 | 0.0749 | 0.3456 | 0.7625 | 0.0749 | 1.0101 | -0.5225 | Ridge |
| BOD | S2 + Context | Ridge | raw | original_rmse_mean | 0.7961 | -0.1514 | 0.4322 | 0.7961 | -0.1514 | 1.0268 | -0.6852 | Ridge |
| DO | S2 only | Ridge | raw | original_rmse_mean | 1.2351 | -0.3115 | 0.2351 | 1.2351 | -0.3115 | 1.2351 | -0.3115 | DummyMedian |
| DO | Context only | ExtraTrees | raw | original_rmse_mean | 1.2911 | -0.4587 | 0.0985 | 1.2911 | -0.4587 | 1.2911 | -0.4587 | DummyMedian |
| DO | S2 + Context | ExtraTrees | raw | original_rmse_mean | 1.2550 | -0.4115 | 0.1789 | 1.2550 | -0.4115 | 1.2550 | -0.4115 | DummyMedian |
| Turbidity | S2 only | ElasticNet | log1p | modelscale_rmse_mean | 0.8116 | 0.3697 | 0.6299 | 52.112 | 0.2093 | 0.8116 | 0.3697 | ElasticNet |
| Turbidity | Context only | Stacking_RidgeMeta | log1p | modelscale_rmse_mean | 1.0271 | 0.0187 | 0.3708 | 57.894 | 0.0579 | 1.0271 | 0.0187 | Stacking_RidgeMeta |
| Turbidity | S2 + Context | RandomForest | log1p | modelscale_rmse_mean | 0.8629 | 0.2977 | 0.5783 | 53.051 | 0.1782 | 0.8629 | 0.2977 | RandomForest |
| SS | S2 only | Ridge | log1p | modelscale_rmse_mean | 0.7062 | 0.2780 | 0.6449 | 47.301 | 0.1956 | 0.7062 | 0.2780 | Ridge |
| SS | Context only | Stacking_RidgeMeta | log1p | modelscale_rmse_mean | 0.8114 | 0.0697 | 0.4286 | 49.013 | 0.1297 | 0.8114 | 0.0697 | Stacking_RidgeMeta |
| SS | S2 + Context | ExtraTrees | log1p | modelscale_rmse_mean | 0.7313 | 0.2370 | 0.5411 | 46.323 | 0.2550 | 0.7313 | 0.2370 | ExtraTrees |
| TCB | S2 only | Stacking_RidgeMeta | log1p | modelscale_rmse_mean | 1.7806 | 0.0086 | 0.3206 | 8,413.61 | -0.0210 | 1.7806 | 0.0086 | Stacking_RidgeMeta |
| TCB | Context only | RandomForest | log1p | modelscale_rmse_mean | 1.7958 | -0.0028 | 0.3241 | 8,442.41 | -0.0112 | 1.7958 | -0.0028 | RandomForest |
| TCB | S2 + Context | CatBoost | log1p | modelscale_rmse_mean | 1.7483 | 0.0432 | 0.3879 | 8,479.12 | -0.0174 | 1.7483 | 0.0432 | CatBoost |
| FCB | S2 only | Stacking_RidgeMeta | log1p | modelscale_rmse_mean | 2.0141 | -0.0524 | 0.1644 | 3,290.71 | -0.1146 | 2.0141 | -0.0524 | Stacking_RidgeMeta |
| FCB | Context only | RandomForest | log1p | modelscale_rmse_mean | 2.0593 | -0.0934 | 0.2407 | 3,198.12 | -0.0544 | 2.0593 | -0.0934 | DummyMedian |
| FCB | S2 + Context | RandomForest | log1p | modelscale_rmse_mean | 2.0305 | -0.0613 | 0.2570 | 3,197.68 | -0.0545 | 2.0305 | -0.0613 | DummyMedian |

## Detailed Rankings

## BOD

### S2 only

Best non-dummy: `CatBoost` using `original_rmse_mean` = 0.9108; selection R2 = -0.6222; selection Spearman = 0.4461.

| model | transform | select_rmse | rank | select_r2 | select_spearman | orig_rmse | orig_mae | orig_r2 | model_rmse | model_r2 | is_dummy |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| DummyMedian | raw | 0.8925 | 1.0000 | -0.1487 |  | 0.8925 | 0.6298 | -0.1487 | 0.8925 | -0.1487 | 1 |
| CatBoost | raw | 0.9108 | 2.0000 | -0.6222 | 0.4461 | 0.9108 | 0.6456 | -0.6222 | 0.9108 | -0.6222 | 0 |
| XGBoost | raw | 0.9157 | 3.0000 | -0.7208 | 0.4514 | 0.9157 | 0.6473 | -0.7208 | 0.9157 | -0.7208 | 0 |
| Stacking_RidgeMeta | raw | 0.9160 | 4.0000 | -0.5311 | 0.4191 | 0.9160 | 0.6602 | -0.5311 | 0.9160 | -0.5311 | 0 |
| RandomForest | raw | 0.9391 | 5.0000 | -0.8480 | 0.4926 | 0.9391 | 0.6544 | -0.8480 | 0.9391 | -0.8480 | 0 |
| Ridge | raw | 0.9613 | 6.0000 | -0.9843 | 0.4506 | 0.9613 | 0.6852 | -0.9843 | 0.9613 | -0.9843 | 0 |
| ElasticNet | raw | 0.9736 | 7.0000 | -1.1210 | 0.4137 | 0.9736 | 0.6997 | -1.1210 | 0.9736 | -1.1210 | 0 |
| ExtraTrees | raw | 1.0226 | 8.0000 | -1.2872 | 0.4172 | 1.0226 | 0.7112 | -1.2872 | 1.0226 | -1.2872 | 0 |

### Context only

Best non-dummy: `Ridge` using `original_rmse_mean` = 0.7625; selection R2 = 0.0749; selection Spearman = 0.3456.

| model | transform | select_rmse | rank | select_r2 | select_spearman | orig_rmse | orig_mae | orig_r2 | model_rmse | model_r2 | is_dummy |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Ridge | raw | 0.7625 | 1.0000 | 0.0749 | 0.3456 | 0.7625 | 0.5837 | 0.0749 | 1.0101 | -0.5225 | 0 |
| CatBoost | raw | 0.8553 | 2.0000 | -0.1380 | 0.1979 | 0.8553 | 0.6229 | -0.1380 | 0.8553 | -0.1380 | 0 |
| Stacking_RidgeMeta | raw | 0.8734 | 3.0000 | -0.2194 | 0.2207 | 0.8734 | 0.6301 | -0.2194 | 0.8740 | -0.2206 | 0 |
| ExtraTrees | raw | 0.8767 | 4.0000 | -0.2142 | 0.1843 | 0.8767 | 0.6260 | -0.2142 | 0.8767 | -0.2142 | 0 |
| RandomForest | raw | 0.8796 | 5.0000 | -0.2630 | 0.2384 | 0.8796 | 0.6372 | -0.2630 | 0.8796 | -0.2630 | 0 |
| XGBoost | raw | 0.8799 | 6.0000 | -0.2636 | 0.1788 | 0.8799 | 0.6325 | -0.2636 | 0.8799 | -0.2636 | 0 |
| DummyMedian | raw | 0.8925 | 7.0000 | -0.1487 |  | 0.8925 | 0.6298 | -0.1487 | 0.8925 | -0.1487 | 1 |
| ElasticNet | raw | 1.2082 | 8.0000 | -2.8589 | 0.2276 | 1.2082 | 0.8943 | -2.8589 | 1.3598 | -3.2744 | 0 |

### S2 + Context

Best non-dummy: `Ridge` using `original_rmse_mean` = 0.7961; selection R2 = -0.1514; selection Spearman = 0.4322.

| model | transform | select_rmse | rank | select_r2 | select_spearman | orig_rmse | orig_mae | orig_r2 | model_rmse | model_r2 | is_dummy |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Ridge | raw | 0.7961 | 1.0000 | -0.1514 | 0.4322 | 0.7961 | 0.5997 | -0.1514 | 1.0268 | -0.6852 | 0 |
| CatBoost | raw | 0.8241 | 2.0000 | -0.0971 | 0.3444 | 0.8241 | 0.5792 | -0.0971 | 0.8241 | -0.0971 | 0 |
| XGBoost | raw | 0.8738 | 3.0000 | -0.3420 | 0.3079 | 0.8738 | 0.6232 | -0.3420 | 0.8738 | -0.3420 | 0 |
| ExtraTrees | raw | 0.8837 | 4.0000 | -0.4009 | 0.3432 | 0.8837 | 0.6072 | -0.4009 | 0.8837 | -0.4009 | 0 |
| Stacking_RidgeMeta | raw | 0.8901 | 5.0000 | -0.4078 | 0.3321 | 0.8901 | 0.6203 | -0.4078 | 0.8980 | -0.4231 | 0 |
| DummyMedian | raw | 0.8925 | 6.0000 | -0.1487 |  | 0.8925 | 0.6298 | -0.1487 | 0.8925 | -0.1487 | 1 |
| RandomForest | raw | 0.9053 | 7.0000 | -0.5602 | 0.3356 | 0.9053 | 0.6355 | -0.5602 | 0.9053 | -0.5602 | 0 |
| ElasticNet | raw | 1.1142 | 8.0000 | -2.0092 | 0.3364 | 1.1142 | 0.8720 | -2.0092 | 1.3713 | -2.7925 | 0 |

## DO

### S2 only

Best non-dummy: `Ridge` using `original_rmse_mean` = 1.2351; selection R2 = -0.3115; selection Spearman = 0.2351.

| model | transform | select_rmse | rank | select_r2 | select_spearman | orig_rmse | orig_mae | orig_r2 | model_rmse | model_r2 | is_dummy |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| DummyMedian | raw | 1.2182 | 1.0000 | -0.1980 |  | 1.2182 | 0.9777 | -0.1980 | 1.2182 | -0.1980 | 1 |
| Ridge | raw | 1.2351 | 2.0000 | -0.3115 | 0.2351 | 1.2351 | 0.9766 | -0.3115 | 1.2351 | -0.3115 | 0 |
| ExtraTrees | raw | 1.2488 | 3.0000 | -0.3477 | 0.3147 | 1.2488 | 0.9667 | -0.3477 | 1.2488 | -0.3477 | 0 |
| Stacking_RidgeMeta | raw | 1.2565 | 4.0000 | -0.3413 | 0.1990 | 1.2565 | 0.9879 | -0.3413 | 1.2565 | -0.3413 | 0 |
| ElasticNet | raw | 1.2763 | 5.0000 | -0.4269 | 0.2373 | 1.2763 | 0.9921 | -0.4269 | 1.2763 | -0.4269 | 0 |
| RandomForest | raw | 1.2827 | 6.0000 | -0.4738 | 0.2757 | 1.2827 | 1.0120 | -0.4738 | 1.2827 | -0.4738 | 0 |
| CatBoost | raw | 1.4054 | 7.0000 | -0.8568 | 0.1849 | 1.4054 | 1.1147 | -0.8568 | 1.4054 | -0.8568 | 0 |
| XGBoost | raw | 1.4293 | 8.0000 | -0.8869 | 0.2199 | 1.4293 | 1.1456 | -0.8869 | 1.4293 | -0.8869 | 0 |

### Context only

Best non-dummy: `ExtraTrees` using `original_rmse_mean` = 1.2911; selection R2 = -0.4587; selection Spearman = 0.0985.

| model | transform | select_rmse | rank | select_r2 | select_spearman | orig_rmse | orig_mae | orig_r2 | model_rmse | model_r2 | is_dummy |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| DummyMedian | raw | 1.2182 | 1.0000 | -0.1980 |  | 1.2182 | 0.9777 | -0.1980 | 1.2182 | -0.1980 | 1 |
| ExtraTrees | raw | 1.2911 | 2.0000 | -0.4587 | 0.0985 | 1.2911 | 1.0429 | -0.4587 | 1.2911 | -0.4587 | 0 |
| RandomForest | raw | 1.3547 | 3.0000 | -0.6336 | 0.0957 | 1.3547 | 1.1252 | -0.6336 | 1.3547 | -0.6336 | 0 |
| Stacking_RidgeMeta | raw | 1.3659 | 4.0000 | -0.6368 | 0.1394 | 1.3659 | 1.0711 | -0.6368 | 1.3659 | -0.6368 | 0 |
| XGBoost | raw | 1.3770 | 5.0000 | -0.7357 | 0.1277 | 1.3770 | 1.1139 | -0.7357 | 1.3770 | -0.7357 | 0 |
| CatBoost | raw | 1.3883 | 6.0000 | -0.7542 | 0.1562 | 1.3883 | 1.1344 | -0.7542 | 1.3883 | -0.7542 | 0 |
| Ridge | raw | 2.9288 | 7.0000 | -6.0304 | 0.2730 | 2.9288 | 1.4892 | -6.0304 | 3.6998 | -9.5836 | 0 |
| ElasticNet | raw | 3.6897 | 8.0000 | -10.201 | 0.0676 | 3.6897 | 2.2761 | -10.201 | 4.4010 | -14.821 | 0 |

### S2 + Context

Best non-dummy: `ExtraTrees` using `original_rmse_mean` = 1.2550; selection R2 = -0.4115; selection Spearman = 0.1789.

| model | transform | select_rmse | rank | select_r2 | select_spearman | orig_rmse | orig_mae | orig_r2 | model_rmse | model_r2 | is_dummy |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| DummyMedian | raw | 1.2182 | 1.0000 | -0.1980 |  | 1.2182 | 0.9777 | -0.1980 | 1.2182 | -0.1980 | 1 |
| ExtraTrees | raw | 1.2550 | 2.0000 | -0.4115 | 0.1789 | 1.2550 | 1.0123 | -0.4115 | 1.2550 | -0.4115 | 0 |
| XGBoost | raw | 1.3098 | 3.0000 | -0.5991 | 0.1966 | 1.3098 | 1.0635 | -0.5991 | 1.3098 | -0.5991 | 0 |
| RandomForest | raw | 1.3128 | 4.0000 | -0.5420 | 0.1417 | 1.3128 | 1.0849 | -0.5420 | 1.3128 | -0.5420 | 0 |
| CatBoost | raw | 1.3171 | 5.0000 | -0.5835 | 0.2095 | 1.3171 | 1.0811 | -0.5835 | 1.3171 | -0.5835 | 0 |
| Stacking_RidgeMeta | raw | 1.3890 | 6.0000 | -0.7645 | 0.1911 | 1.3890 | 1.0748 | -0.7645 | 1.3890 | -0.7645 | 0 |
| Ridge | raw | 3.1792 | 7.0000 | -7.1815 | 0.3077 | 3.1792 | 1.5382 | -7.1815 | 4.0002 | -11.433 | 0 |
| ElasticNet | raw | 4.3891 | 8.0000 | -15.144 | 0.1348 | 4.3891 | 2.5441 | -15.144 | 5.2024 | -20.497 | 0 |

## Turbidity

### S2 only

Best non-dummy: `ElasticNet` using `modelscale_rmse_mean` = 0.8116; selection R2 = 0.3697; selection Spearman = 0.6299.

| model | transform | select_rmse | rank | select_r2 | select_spearman | orig_rmse | orig_mae | orig_r2 | model_rmse | model_r2 | is_dummy |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ElasticNet | log1p | 0.8116 | 1.0000 | 0.3697 | 0.6299 | 52.112 | 22.804 | 0.2093 | 0.8116 | 0.3697 | 0 |
| Ridge | log1p | 0.8175 | 2.0000 | 0.3597 | 0.6280 | 53.525 | 23.655 | 0.1719 | 0.8175 | 0.3597 | 0 |
| Stacking_RidgeMeta | log1p | 0.8229 | 3.0000 | 0.3562 | 0.5907 | 53.061 | 22.887 | 0.1856 | 0.8229 | 0.3562 | 0 |
| CatBoost | log1p | 0.8282 | 4.0000 | 0.3548 | 0.5898 | 49.862 | 23.124 | 0.2647 | 0.8282 | 0.3548 | 0 |
| RandomForest | log1p | 0.8330 | 5.0000 | 0.3345 | 0.6148 | 53.054 | 24.221 | 0.1581 | 0.8330 | 0.3345 | 0 |
| ExtraTrees | log1p | 0.8565 | 6.0000 | 0.3045 | 0.5877 | 51.531 | 23.581 | 0.2141 | 0.8565 | 0.3045 | 0 |
| XGBoost | log1p | 0.8828 | 7.0000 | 0.2632 | 0.5547 | 50.687 | 24.399 | 0.2161 | 0.8828 | 0.2632 | 0 |
| DummyMedian | log1p | 1.0936 | 8.0000 | -0.1122 |  | 62.446 | 29.079 | -0.1416 | 1.0936 | -0.1122 | 1 |

### Context only

Best non-dummy: `Stacking_RidgeMeta` using `modelscale_rmse_mean` = 1.0271; selection R2 = 0.0187; selection Spearman = 0.3708.

| model | transform | select_rmse | rank | select_r2 | select_spearman | orig_rmse | orig_mae | orig_r2 | model_rmse | model_r2 | is_dummy |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Stacking_RidgeMeta | log1p | 1.0271 | 1.0000 | 0.0187 | 0.3708 | 57.894 | 28.097 | 0.0579 | 1.0271 | 0.0187 | 0 |
| CatBoost | log1p | 1.0476 | 2.0000 | -0.0226 | 0.2929 | 56.607 | 28.444 | 0.0975 | 1.0476 | -0.0226 | 0 |
| RandomForest | log1p | 1.0517 | 3.0000 | -0.0259 | 0.2611 | 57.906 | 29.136 | 0.0284 | 1.0517 | -0.0259 | 0 |
| ExtraTrees | log1p | 1.0848 | 4.0000 | -0.0919 | 0.2034 | 60.342 | 30.090 | -0.0430 | 1.0848 | -0.0919 | 0 |
| DummyMedian | log1p | 1.0936 | 5.0000 | -0.1122 |  | 62.446 | 29.079 | -0.1416 | 1.0936 | -0.1122 | 1 |
| XGBoost | log1p | 1.1339 | 6.0000 | -0.2009 | 0.2142 | 56.142 | 29.626 | 0.0788 | 1.1339 | -0.2009 | 0 |
| Ridge | log1p | 3.0179 | 7.0000 | -9.6196 | -0.0544 | 17,050,269,099.22 | 2,765,918,941.41 | -131,297,899,659,021,056.00 | 3.0179 | -9.6196 | 0 |
| ElasticNet | log1p | 3.9459 | 8.0000 | -14.144 | -0.1531 | 18,599,501.82 | 3,019,130.24 | -156,027,503,157.52 | 3.9459 | -14.144 | 0 |

### S2 + Context

Best non-dummy: `RandomForest` using `modelscale_rmse_mean` = 0.8629; selection R2 = 0.2977; selection Spearman = 0.5783.

| model | transform | select_rmse | rank | select_r2 | select_spearman | orig_rmse | orig_mae | orig_r2 | model_rmse | model_r2 | is_dummy |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| RandomForest | log1p | 0.8629 | 1.0000 | 0.2977 | 0.5783 | 53.051 | 25.190 | 0.1782 | 0.8629 | 0.2977 | 0 |
| CatBoost | log1p | 0.8838 | 2.0000 | 0.2697 | 0.5744 | 53.742 | 25.307 | 0.1530 | 0.8838 | 0.2697 | 0 |
| Stacking_RidgeMeta | log1p | 0.8903 | 3.0000 | 0.2590 | 0.5145 | 53.704 | 24.913 | 0.1728 | 0.8903 | 0.2590 | 0 |
| ExtraTrees | log1p | 0.9173 | 4.0000 | 0.2117 | 0.4836 | 55.299 | 26.083 | 0.1093 | 0.9173 | 0.2117 | 0 |
| XGBoost | log1p | 0.9317 | 5.0000 | 0.1866 | 0.4888 | 51.689 | 25.834 | 0.2118 | 0.9317 | 0.1866 | 0 |
| DummyMedian | log1p | 1.0936 | 6.0000 | -0.1122 |  | 62.446 | 29.079 | -0.1416 | 1.0936 | -0.1122 | 1 |
| Ridge | log1p | 2.0589 | 7.0000 | -3.5385 | 0.2060 | 2,843.31 | 495.810 | -3,513.89 | 2.0589 | -3.5385 | 0 |
| ElasticNet | log1p | 2.7737 | 8.0000 | -6.5534 | 0.0074 | 10,007,400.95 | 1,623,512.30 | -45,227,741,612.71 | 2.7737 | -6.5534 | 0 |

## SS

### S2 only

Best non-dummy: `Ridge` using `modelscale_rmse_mean` = 0.7062; selection R2 = 0.2780; selection Spearman = 0.6449.

| model | transform | select_rmse | rank | select_r2 | select_spearman | orig_rmse | orig_mae | orig_r2 | model_rmse | model_r2 | is_dummy |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Ridge | log1p | 0.7062 | 1.0000 | 0.2780 | 0.6449 | 47.301 | 19.359 | 0.1956 | 0.7062 | 0.2780 | 0 |
| ElasticNet | log1p | 0.7233 | 2.0000 | 0.2454 | 0.6138 | 47.411 | 19.356 | 0.1834 | 0.7233 | 0.2454 | 0 |
| Stacking_RidgeMeta | log1p | 0.7470 | 3.0000 | 0.1927 | 0.5757 | 48.264 | 20.103 | 0.1368 | 0.7470 | 0.1927 | 0 |
| RandomForest | log1p | 0.7604 | 4.0000 | 0.1544 | 0.5511 | 48.476 | 20.390 | 0.0977 | 0.7604 | 0.1544 | 0 |
| ExtraTrees | log1p | 0.7871 | 5.0000 | 0.0942 | 0.5196 | 48.241 | 20.097 | 0.1251 | 0.7871 | 0.0942 | 0 |
| CatBoost | log1p | 0.8089 | 6.0000 | 0.0635 | 0.4388 | 48.469 | 20.747 | 0.1238 | 0.8089 | 0.0635 | 0 |
| XGBoost | log1p | 0.8313 | 7.0000 | -0.0010 | 0.4253 | 49.282 | 21.091 | 0.0496 | 0.8313 | -0.0010 | 0 |
| DummyMedian | log1p | 0.9197 | 8.0000 | -0.1975 |  | 52.479 | 23.176 | -0.0990 | 0.9197 | -0.1975 | 1 |

### Context only

Best non-dummy: `Stacking_RidgeMeta` using `modelscale_rmse_mean` = 0.8114; selection R2 = 0.0697; selection Spearman = 0.4286.

| model | transform | select_rmse | rank | select_r2 | select_spearman | orig_rmse | orig_mae | orig_r2 | model_rmse | model_r2 | is_dummy |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Stacking_RidgeMeta | log1p | 0.8114 | 1.0000 | 0.0697 | 0.4286 | 49.013 | 21.271 | 0.1297 | 0.8114 | 0.0697 | 0 |
| ExtraTrees | log1p | 0.8129 | 2.0000 | 0.0695 | 0.3865 | 48.718 | 21.363 | 0.1444 | 0.8129 | 0.0695 | 0 |
| CatBoost | log1p | 0.8381 | 3.0000 | 0.0090 | 0.3751 | 49.042 | 21.904 | 0.1296 | 0.8381 | 0.0090 | 0 |
| RandomForest | log1p | 0.8463 | 4.0000 | -0.0143 | 0.3255 | 49.771 | 22.218 | 0.0655 | 0.8463 | -0.0143 | 0 |
| XGBoost | log1p | 0.8701 | 5.0000 | -0.0665 | 0.3031 | 49.265 | 22.347 | 0.1156 | 0.8701 | -0.0665 | 0 |
| DummyMedian | log1p | 0.9197 | 6.0000 | -0.1975 |  | 52.479 | 23.176 | -0.0990 | 0.9197 | -0.1975 | 1 |
| Ridge | log1p | 2.9067 | 7.0000 | -11.825 | -0.0433 | 2,148.30 | 396.558 | -1,343.85 | 2.9067 | -11.825 | 0 |
| ElasticNet | log1p | 3.3206 | 8.0000 | -14.746 | 0.0326 | 22,712.49 | 6,908.75 | -1,617,852.41 | 3.3206 | -14.746 | 0 |

### S2 + Context

Best non-dummy: `ExtraTrees` using `modelscale_rmse_mean` = 0.7313; selection R2 = 0.2370; selection Spearman = 0.5411.

| model | transform | select_rmse | rank | select_r2 | select_spearman | orig_rmse | orig_mae | orig_r2 | model_rmse | model_r2 | is_dummy |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| ExtraTrees | log1p | 0.7313 | 1.0000 | 0.2370 | 0.5411 | 46.323 | 19.449 | 0.2550 | 0.7313 | 0.2370 | 0 |
| RandomForest | log1p | 0.7413 | 2.0000 | 0.2136 | 0.5386 | 46.180 | 19.579 | 0.2530 | 0.7413 | 0.2136 | 0 |
| CatBoost | log1p | 0.7495 | 3.0000 | 0.2004 | 0.5183 | 47.572 | 19.945 | 0.1804 | 0.7495 | 0.2004 | 0 |
| Stacking_RidgeMeta | log1p | 0.7639 | 4.0000 | 0.1692 | 0.5053 | 46.794 | 20.081 | 0.2251 | 0.7639 | 0.1692 | 0 |
| XGBoost | log1p | 0.8058 | 5.0000 | 0.0714 | 0.4433 | 47.504 | 20.722 | 0.1785 | 0.8058 | 0.0714 | 0 |
| DummyMedian | log1p | 0.9197 | 6.0000 | -0.1975 |  | 52.479 | 23.176 | -0.0990 | 0.9197 | -0.1975 | 1 |
| Ridge | log1p | 1.9359 | 7.0000 | -4.3280 | 0.2071 | 650.737 | 171.332 | -361.483 | 1.9359 | -4.3280 | 0 |
| ElasticNet | log1p | 2.7621 | 8.0000 | -9.7729 | 0.1256 | 3,728.84 | 984.791 | -22,619.67 | 2.7621 | -9.7729 | 0 |

## TCB

### S2 only

Best non-dummy: `Stacking_RidgeMeta` using `modelscale_rmse_mean` = 1.7806; selection R2 = 0.0086; selection Spearman = 0.3206.

| model | transform | select_rmse | rank | select_r2 | select_spearman | orig_rmse | orig_mae | orig_r2 | model_rmse | model_r2 | is_dummy |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Stacking_RidgeMeta | log1p | 1.7806 | 1.0000 | 0.0086 | 0.3206 | 8,413.61 | 4,615.16 | -0.0210 | 1.7806 | 0.0086 | 0 |
| ElasticNet | log1p | 1.7949 | 2.0000 | -0.0361 | 0.3231 | 8,363.84 | 4,884.69 | -0.0240 | 1.7949 | -0.0361 | 0 |
| Ridge | log1p | 1.8378 | 3.0000 | -0.0668 | 0.2824 | 8,514.00 | 4,705.93 | -0.0474 | 1.8378 | -0.0668 | 0 |
| RandomForest | log1p | 1.8693 | 4.0000 | -0.0924 | 0.1988 | 8,340.90 | 4,628.55 | 0.0141 | 1.8693 | -0.0924 | 0 |
| DummyMedian | log1p | 1.8764 | 5.0000 | -0.0876 |  | 8,853.46 | 4,549.54 | -0.1269 | 1.8764 | -0.0876 | 1 |
| CatBoost | log1p | 1.9591 | 6.0000 | -0.2168 | 0.1866 | 8,372.01 | 4,655.86 | 0.0124 | 1.9591 | -0.2168 | 0 |
| ExtraTrees | log1p | 1.9669 | 7.0000 | -0.2197 | 0.1583 | 8,378.03 | 4,689.05 | -0.0007 | 1.9669 | -0.2197 | 0 |
| XGBoost | log1p | 2.0262 | 8.0000 | -0.2865 | 0.1305 | 8,200.72 | 4,764.10 | 0.0539 | 2.0262 | -0.2865 | 0 |

### Context only

Best non-dummy: `RandomForest` using `modelscale_rmse_mean` = 1.7958; selection R2 = -0.0028; selection Spearman = 0.3241.

| model | transform | select_rmse | rank | select_r2 | select_spearman | orig_rmse | orig_mae | orig_r2 | model_rmse | model_r2 | is_dummy |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| RandomForest | log1p | 1.7958 | 1.0000 | -0.0028 | 0.3241 | 8,442.41 | 4,439.83 | -0.0112 | 1.7958 | -0.0028 | 0 |
| CatBoost | log1p | 1.8031 | 2.0000 | -0.0069 | 0.2661 | 8,356.71 | 4,494.11 | 0.0060 | 1.8031 | -0.0069 | 0 |
| DummyMedian | log1p | 1.8764 | 3.0000 | -0.0876 |  | 8,853.46 | 4,549.54 | -0.1269 | 1.8764 | -0.0876 | 1 |
| XGBoost | log1p | 1.8786 | 4.0000 | -0.1063 | 0.3401 | 8,473.14 | 4,670.07 | -0.0111 | 1.8786 | -0.1063 | 0 |
| ExtraTrees | log1p | 1.9325 | 5.0000 | -0.1440 | 0.1383 | 8,596.10 | 4,579.39 | -0.0608 | 1.9325 | -0.1440 | 0 |
| Stacking_RidgeMeta | log1p | 2.3160 | 6.0000 | -0.6994 | -0.0101 | 10,416.91 | 6,161.95 | -0.4949 | 2.3160 | -0.6994 | 0 |
| Ridge | log1p | 3.6866 | 7.0000 | -4.8931 | -0.0657 | 2,040,583.98 | 981,347.45 | -96,777.78 | 3.6866 | -4.8931 | 0 |
| ElasticNet | log1p | 5.2344 | 8.0000 | -8.4176 | -0.2039 | 12,919,965.57 | 4,837,590.31 | -5,913,994.12 | 5.2344 | -8.4176 | 0 |

### S2 + Context

Best non-dummy: `CatBoost` using `modelscale_rmse_mean` = 1.7483; selection R2 = 0.0432; selection Spearman = 0.3879.

| model | transform | select_rmse | rank | select_r2 | select_spearman | orig_rmse | orig_mae | orig_r2 | model_rmse | model_r2 | is_dummy |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| CatBoost | log1p | 1.7483 | 1.0000 | 0.0432 | 0.3879 | 8,479.12 | 4,545.86 | -0.0174 | 1.7483 | 0.0432 | 0 |
| RandomForest | log1p | 1.7945 | 2.0000 | 0.0014 | 0.3415 | 8,532.26 | 4,557.02 | -0.0310 | 1.7945 | 0.0014 | 0 |
| XGBoost | log1p | 1.8442 | 3.0000 | -0.0662 | 0.3727 | 8,911.51 | 5,031.51 | -0.1543 | 1.8442 | -0.0662 | 0 |
| ExtraTrees | log1p | 1.8593 | 4.0000 | -0.0652 | 0.2345 | 8,581.09 | 4,610.62 | -0.0566 | 1.8593 | -0.0652 | 0 |
| DummyMedian | log1p | 1.8764 | 5.0000 | -0.0876 |  | 8,853.46 | 4,549.54 | -0.1269 | 1.8764 | -0.0876 | 1 |
| Stacking_RidgeMeta | log1p | 1.9892 | 6.0000 | -0.2233 | 0.1390 | 9,484.89 | 5,329.24 | -0.2352 | 1.9892 | -0.2233 | 0 |
| Ridge | log1p | 3.3637 | 7.0000 | -3.3903 | 0.0310 | 8,073,190.56 | 2,678,025.47 | -1,519,624.87 | 3.3637 | -3.3903 | 0 |
| ElasticNet | log1p | 4.2370 | 8.0000 | -5.1313 | -0.0648 | 25,476,770.98 | 9,070,373.60 | -15,007,340.53 | 4.2370 | -5.1313 | 0 |

## FCB

### S2 only

Best non-dummy: `Stacking_RidgeMeta` using `modelscale_rmse_mean` = 2.0141; selection R2 = -0.0524; selection Spearman = 0.1644.

| model | transform | select_rmse | rank | select_r2 | select_spearman | orig_rmse | orig_mae | orig_r2 | model_rmse | model_r2 | is_dummy |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Stacking_RidgeMeta | log1p | 2.0141 | 1.0000 | -0.0524 | 0.1644 | 3,290.71 | 1,559.44 | -0.1146 | 2.0141 | -0.0524 | 0 |
| DummyMedian | log1p | 2.0294 | 2.0000 | -0.0624 |  | 3,345.98 | 1,571.83 | -0.1513 | 2.0294 | -0.0624 | 1 |
| RandomForest | log1p | 2.0344 | 3.0000 | -0.0707 | 0.1580 | 3,250.16 | 1,578.68 | -0.0901 | 2.0344 | -0.0707 | 0 |
| Ridge | log1p | 2.0698 | 4.0000 | -0.1245 | 0.1037 | 3,317.22 | 1,584.11 | -0.1336 | 2.0698 | -0.1245 | 0 |
| ElasticNet | log1p | 2.0772 | 5.0000 | -0.1349 | 0.1351 | 3,276.79 | 1,649.43 | -0.1124 | 2.0772 | -0.1349 | 0 |
| ExtraTrees | log1p | 2.1223 | 6.0000 | -0.1796 | 0.1100 | 3,225.33 | 1,589.88 | -0.0760 | 2.1223 | -0.1796 | 0 |
| XGBoost | log1p | 2.1879 | 7.0000 | -0.2437 | 0.0887 | 3,253.23 | 1,665.76 | -0.0920 | 2.1879 | -0.2437 | 0 |
| CatBoost | log1p | 2.1985 | 8.0000 | -0.2540 | 0.0943 | 3,261.41 | 1,645.38 | -0.0976 | 2.1985 | -0.2540 | 0 |

### Context only

Best non-dummy: `RandomForest` using `modelscale_rmse_mean` = 2.0593; selection R2 = -0.0934; selection Spearman = 0.2407.

| model | transform | select_rmse | rank | select_r2 | select_spearman | orig_rmse | orig_mae | orig_r2 | model_rmse | model_r2 | is_dummy |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| DummyMedian | log1p | 2.0294 | 1.0000 | -0.0624 |  | 3,345.98 | 1,571.83 | -0.1513 | 2.0294 | -0.0624 | 1 |
| RandomForest | log1p | 2.0593 | 2.0000 | -0.0934 | 0.2407 | 3,198.12 | 1,527.84 | -0.0544 | 2.0593 | -0.0934 | 0 |
| CatBoost | log1p | 2.0768 | 3.0000 | -0.1074 | 0.1668 | 3,228.89 | 1,557.55 | -0.0762 | 2.0768 | -0.1074 | 0 |
| ExtraTrees | log1p | 2.1290 | 4.0000 | -0.1573 | 0.1000 | 3,217.28 | 1,578.19 | -0.0703 | 2.1290 | -0.1573 | 0 |
| XGBoost | log1p | 2.1479 | 5.0000 | -0.1942 | 0.1806 | 3,180.62 | 1,583.82 | -0.0444 | 2.1479 | -0.1942 | 0 |
| Stacking_RidgeMeta | log1p | 2.2894 | 6.0000 | -0.3350 | -0.0790 | 3,305.19 | 1,692.60 | -0.1229 | 2.2894 | -0.3350 | 0 |
| Ridge | log1p | 3.9552 | 7.0000 | -4.5744 | 0.0101 | 1,881,180.69 | 914,603.26 | -794,948.77 | 3.9552 | -4.5744 | 0 |
| ElasticNet | log1p | 4.8002 | 8.0000 | -5.4405 | -0.1395 | 1,520,406.67 | 645,833.27 | -380,261.61 | 4.8002 | -5.4405 | 0 |

### S2 + Context

Best non-dummy: `RandomForest` using `modelscale_rmse_mean` = 2.0305; selection R2 = -0.0613; selection Spearman = 0.2570.

| model | transform | select_rmse | rank | select_r2 | select_spearman | orig_rmse | orig_mae | orig_r2 | model_rmse | model_r2 | is_dummy |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| DummyMedian | log1p | 2.0294 | 1.0000 | -0.0624 |  | 3,345.98 | 1,571.83 | -0.1513 | 2.0294 | -0.0624 | 1 |
| RandomForest | log1p | 2.0305 | 2.0000 | -0.0613 | 0.2570 | 3,197.68 | 1,544.39 | -0.0545 | 2.0305 | -0.0613 | 0 |
| CatBoost | log1p | 2.0548 | 3.0000 | -0.0866 | 0.2200 | 3,184.16 | 1,599.92 | -0.0480 | 2.0548 | -0.0866 | 0 |
| ExtraTrees | log1p | 2.0702 | 4.0000 | -0.1001 | 0.1491 | 3,225.19 | 1,581.38 | -0.0774 | 2.0702 | -0.1001 | 0 |
| Stacking_RidgeMeta | log1p | 2.1172 | 5.0000 | -0.1469 | 0.1392 | 3,177.89 | 1,560.31 | -0.0393 | 2.1172 | -0.1469 | 0 |
| XGBoost | log1p | 2.1265 | 6.0000 | -0.1624 | 0.2035 | 3,168.89 | 1,635.27 | -0.0411 | 2.1265 | -0.1624 | 0 |
| Ridge | log1p | 4.2423 | 7.0000 | -4.6554 | -0.0375 | 470,069.57 | 190,002.38 | -49,249.93 | 4.2423 | -4.6554 | 0 |
| ElasticNet | log1p | 4.5783 | 8.0000 | -4.7606 | -0.0850 | 2,230,768.66 | 765,994.65 | -1,082,075.05 | 4.5783 | -4.7606 | 0 |

## Interpretation Note

Turbidity and SS are optically related targets. DO, BOD, TCB, and FCB are indirect proxy models, so these tables should be reported as station-temporal robustness evidence rather than proof of direct satellite measurement.
