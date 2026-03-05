# Feature engineering patterns

Goal: produce stable, reproducible features that are available at prediction time.

## General rules
- Separate fit-time from transform-time (fit scalers/encoders on train only).
- Define an as-of timestamp and enforce it for every join and window.
- Prefer monotonic, bounded transforms when the model or domain benefits.
- Treat missingness explicitly; do not let it vary by library defaults.
- Keep feature names deterministic (no auto-generated column order dependence).

## Numeric

### Scaling
- Standardization: (x - mean) / std; good default for linear models, kNN, NN.
- Robust scaling: (x - median) / IQR; better with heavy tails/outliers.
- Min-max scaling: (x - min) / (max - min); use only if bounds are stable.

### Transforms
- Log: log1p(x) for non-negative skew; document how zeros/negatives are handled.
- Power transforms: Yeo-Johnson (handles negatives) or Box-Cox (positive only).
- Quantile transform: map to uniform/normal; can help but may reduce interpretability.

### Clipping and outliers
- Winsorize: clip to percentile bounds (for example p1/p99) computed on train.
- Domain clipping: clip to known physical bounds; safer than percentile clipping.
- Cap extreme ratios: add epsilon and cap numerator/denominator to avoid blow-ups.

### Derived numeric features
- Binning: fixed bins or quantile bins fit on train; keep bin edges versioned.
- Interactions: x*y, x/y, x-y when domain suggests effects are relative.
- Aggregates: per-entity mean/sum/std with strict time cutoffs (see Datetime).

## Categorical

### Cleaning
- Normalize case/whitespace; standardize placeholders ("", "NA", "unknown").
- Collapse equivalent values using a mapping table; keep mapping under version control.

### Encoding
- One-hot: good for low/medium cardinality; set handle_unknown behavior.
- Ordinal: only when there is a true order; document the order source.
- Frequency/count encoding: encode category count or frequency from train.
- Hashing: fixed-dimensional, stateless; good for very high cardinality.

### Rare category handling
- Rare bucket: group categories below a threshold into "__RARE__" (threshold from train).
- Top-K: keep top K categories by train frequency, map others to "__OTHER__".

### Target-related encodings (high leakage risk)
- Mean/impact encoding: use out-of-fold computation on train; never use full-train target
  stats directly on the same rows.
- Time-aware target encoding: compute stats using only past data relative to each row.

## Datetime

### Parsing and normalization
- Parse with explicit timezone; convert to a standard timezone (often UTC).
- Validate monotonicity where expected (events per entity) and handle duplicates.

### Calendar parts
- Extract: hour, day_of_week, day_of_month, week_of_year, month, quarter, is_weekend.
- Holiday features: use a fixed holiday calendar for the relevant locale(s).

### Cyclical encoding
- For periodic fields (hour, day_of_week):
  - sin = sin(2*pi*k/period)
  - cos = cos(2*pi*k/period)
- Use raw k as well only if the model can learn wrap-around.

### Time windows (rolling / trailing)
- Lags: value at t-1, t-7, etc. for time series or repeated measurements.
- Rolling windows: trailing mean/sum/std/min/max over 1d/7d/30d with an as-of cutoff.
- Expanding windows: cumulative stats up to t (exclusive) to avoid peeking.
- Recency: time since last event, time since first event, time since status change.

### Join-time rules (anti-leakage)
- Use point-in-time joins: for each row at time t, only join records with time <= t.
- For aggregates, compute using (entity_id, timestamp) ordering and strict (<= t) filters.

## Text

### Basic preprocessing
- Normalize: lowercase (if appropriate), strip control chars, normalize whitespace.
- Keep original text length features: char_len, word_count, unique_word_ratio.

### Tokenization and vectorization
- Bag-of-words / n-grams (word or char); prefer char n-grams for noisy text.
- TF-IDF for linear models; keep vocabulary fit on train only.
- Hashing vectorizer for streaming or very large vocab; fixed dimension.

### Leakage cautions for text
- Remove obvious label artifacts (for example "approved", "fraud") if they are only
  present because of a downstream process.
- Be careful with templated communications that embed outcomes or timestamps.
- If text is produced after the prediction time, do not use it.

## Leakage checklist
- Prediction time defined: what timestamp represents "now" for each row.
- Availability confirmed: every source field existed at prediction time.
- Split strategy aligned: random vs group vs time split matches deployment reality.
- Aggregations are point-in-time: windows and joins use <= as-of time, not full history.
- Encoders/scalers fit on train only; target-based encodings are out-of-fold.
- No future-derived labels: features do not include post-outcome updates.
- No proxy IDs: features do not directly encode target, outcome workflow, or manual review.
- Monitoring plan: watch drift and missingness for features likely to change.

## Feature spec template
```text
Name:
Owner:
Status: draft | active | deprecated

Entity / Grain:
Prediction time definition:

Raw sources (tables/fields):
Upstream update cadence:
Availability constraint (must be true at prediction time):

Feature type: numeric | categorical | datetime | text | boolean
Transformation (exact):
Training-time fit state (if any):
Missing handling:
Outlier handling:

Leakage risks and mitigations:
Validation tests (unit/data tests):

Expected directionality / sanity checks:
Monitoring (drift, missingness, bounds):
Versioning notes (mappings, bin edges, vocab):
```
