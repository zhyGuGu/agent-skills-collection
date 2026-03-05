# Model Selection (Classification/Regression)

Purpose: pick a model family quickly, establish a baseline, then iterate with constraints.

## Baseline-First Rule

1. Define a metric and validation scheme that matches deployment (see "IID vs Time Series").
2. Train the simplest baseline that is (a) cheap, (b) hard to beat, and (c) easy to debug.
3. Only upgrade model complexity if the baseline fails on a concrete error mode.

## Quick Baseline Table

| Problem type | Data shape | Suggested baselines (start here) |
|---|---|---|
| Binary classification | tabular, IID | Logistic regression (L2), linear SVM, LightGBM/XGBoost (shallow) |
| Multi-class classification | tabular, IID | Multinomial logistic regression, LightGBM/XGBoost |
| Regression | tabular, IID | Ridge/Lasso/ElasticNet, Random Forest, LightGBM/XGBoost |
| Ranking / propensity scoring | tabular, IID | Logistic regression + calibration, LightGBM with monotone constraints (if needed) |
| Text classification | short/medium text | TF-IDF + linear model (logreg/linear SVM); then small transformer |
| Image classification | images | Linear probe on pretrained embeddings; then fine-tune pretrained CNN/ViT |
| Time series forecasting | univariate/multivariate | Naive/seasonal naive; ETS/ARIMA; gradient boosting on lag features |
| Anomaly detection | time series / logs | Simple thresholds + moving stats; isolation forest / one-class SVM (IID) |

## Decision Tree / Checklist

Work top-down. Stop as soon as you have a defensible choice.

### 0) Frame the objective

- Task: classification or regression? (If "predict next value" see time series.)
- Output needs: probability, calibrated probability, or point estimate + intervals?
- Metric: choose ONE primary metric; define minimum acceptable performance.

### 1) Identify data regime

- Mostly tabular features (numeric/categorical): start with linear and tree ensembles.
- High-dimensional sparse (bag-of-words, n-grams): start with linear models.
- Unstructured (text/images/audio): start with pretrained embeddings, then fine-tune.
- Mixed modalities: baseline each modality separately, then late-fuse (stacking).

### 2) Pick the validation scheme (do this before model choice)

- IID data: random split or stratified K-fold.
- Grouped data (users, sessions, devices): group-aware split (GroupKFold).
- Time-ordered data: time-based split; never shuffle across time.

### 3) Start with the simplest baseline that matches the metric

- Classification:
  - Need calibrated probabilities: logistic regression + calibration (Platt/isotonic).
  - Highly non-linear boundaries: gradient boosting (LightGBM/XGBoost/CatBoost).
- Regression:
  - Linear-ish relationship: Ridge/ElasticNet.
  - Strong interactions / non-linearity: gradient boosting or random forest.

### 4) Check data size and feature quality

- Small data (<=10k rows) / noisy labels:
  - Prefer simpler models; regularize; avoid deep nets.
- Medium to large data (>=100k rows):
  - Tree boosting scales well for tabular; consider neural nets if features are dense.
- High-cardinality categoricals:
  - Consider CatBoost or target encoding (with leakage-safe CV).

### 5) Choose model family (classification/regression)

- Linear models (logistic/linear regression):
  - Use when you need interpretability, fast inference, stable training.
- Tree ensembles (GBDT / Random Forest):
  - Use for tabular non-linearities, mixed feature types, strong baseline accuracy.
- Kernel methods (SVM/RBF, SVR):
  - Use for small/medium data with complex boundaries; watch scaling.
- Neural nets (MLP for tabular, transformers/CNNs for unstructured):
  - Use when representation learning matters or pretrained transfer is available.

### 6) Sanity checks before upgrading complexity

- Data leakage: target leakage, time leakage, duplicate entities across splits.
- Feature drift: training vs serving distributions differ.
- Label noise: inconsistent annotation; ambiguous classes.
- Calibration: probability outputs match observed frequencies.
- Error analysis: which slices dominate loss (by segment, time, geography, etc.).

## IID vs Time Series Notes

Treat time as a first-class feature and constraint.

### IID (independent and identically distributed)

- Random/stratified splits are acceptable if entities do not repeat across splits.
- Feature engineering can use the entire dataset distribution (scalers/encoders) only
  inside each CV fold to avoid leakage.

### Time series / temporal data

- Use forward-chaining evaluation (train on past, validate on future).
- Baselines are not optional:
  - Naive: y_hat(t)=y(t-1)
  - Seasonal naive: y_hat(t)=y(t-s)
- Common leakage sources:
  - Using future information in rolling statistics
  - Target-derived features computed on the full series
- Model family choices:
  - Classical: ETS/ARIMA for univariate with clear trend/seasonality.
  - ML: gradient boosting on lag/rolling features for many covariates.
  - Deep: sequence models when you have lots of series and want shared patterns.

## Constraints (Decide Early)

### Latency / throughput

- Tight latency (ms): linear models, small GBDT, distilled embeddings; avoid large LLMs.
- Batch inference allowed: larger GBDT or neural nets are viable.

### Interpretability / governance

- High requirement: linear models, GAMs, monotonic GBDT constraints; keep features human.
- Medium requirement: tree ensembles + SHAP; document feature stability.
- Low requirement: deep models; add post-hoc explanations as needed.

### Training cost / iteration speed

- Need fast iteration: linear models, small GBDT, CPU training.
- Budget for tuning: GBDT with Bayesian/early-stop tuning; feature selection.
- High compute available: deep models, large-scale hyperparameter searches.

## Practical Defaults

- If tabular and you do not know where to start: LightGBM/XGBoost + a linear model.
- If sparse text: TF-IDF + logistic regression.
- If images/audio/text with transfer learning: pretrained embeddings + linear head first.
- If time series forecasting: seasonal naive baseline, then lag-feature GBDT.

## Exit Criteria (Stop Iterating When)

- You meet the metric threshold on a validation split that matches deployment.
- Remaining errors are dominated by data quality or missing features, not model choice.
- A more complex model violates constraints (latency, interpretability, cost).
