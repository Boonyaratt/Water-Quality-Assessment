# Validation Design

## Temporal Split

Train on observations from 2562-2566 and test on observations from 2567-2568.

This evaluates future-year performance.

## Station-Temporal Split

Hold out station patterns and future years in station-temporal folds.

This evaluates robustness under a stricter setting. It is expected to be harder than temporal testing because the model must transfer to unseen station-year patterns.

## Metrics

Regression:

- MAE
- RMSE
- R2
- Pearson r
- Spearman r
- Bias

Classification:

- Accuracy
- Balanced accuracy
- Macro F1
- Confusion matrix

For skewed targets transformed with `log1p`, report both original-scale and model-scale metrics.

