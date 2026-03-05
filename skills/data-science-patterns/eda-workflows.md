# EDA Workflows

Purpose: run a repeatable exploratory data analysis (EDA) pass before modeling.

## EDA Checklist (Step-by-Step)

### 0) Frame The Problem
1. Write down: prediction target, prediction time, and unit of prediction (entity + granularity).
2. Confirm: what rows represent (one row per user/day/transaction/etc.).
3. Define evaluation metric and baseline (so EDA focuses on what matters).

### 1) Load + Basic Sanity
1. Record dataset version, extraction date, and row filters applied.
2. Check row count and distinct entity counts (e.g., users, accounts).
3. Verify key uniqueness for the intended grain.
4. Check obvious invalid values (negative ages, impossible dates, etc.).

### 2) Schema And Types
1. List columns with inferred dtypes vs expected dtypes.
2. For each column:
   - Confirm type (numeric, categorical, boolean, timestamp, text).
   - Confirm units and scale (cents vs dollars, seconds vs ms).
   - Identify encoded sentinels (e.g., -1, 9999, "unknown").
3. Normalize column names and categories only after documenting the raw state.

### 3) Missingness
1. Compute missing count and missing rate per column.
2. Identify non-standard missing representations (empty string, "N/A", 0-as-missing).
3. Compare missingness by:
   - target (if supervised)
   - key segments (region, channel, plan)
   - time (if time-based)
4. Decide: drop column, impute, create missing indicator, or fix upstream.

### 4) Univariate Distributions
1. Numeric columns:
   - min/median/max, percentiles (p1/p5/p50/p95/p99)
   - heavy tails and outliers; zero inflation
   - log/clip/winsorize candidates (document decision)
2. Categorical columns:
   - cardinality, top-k frequencies, rare categories
   - whitespace/case issues; category drift over time
3. Timestamp columns:
   - range, gaps, duplicates, timezone consistency

### 5) Target (If Supervised)
1. Define label generation logic in one place; validate it with spot checks.
2. Check target prevalence and class imbalance.
3. For regression targets:
   - distribution, extreme values, and whether target is censored/truncated
4. Check label quality by auditing a small sample end-to-end (source -> label).

### 6) Bivariate Relationships (Quick Signal)
1. Correlations for numeric-numeric (use robust checks; watch for leakage).
2. Target vs feature:
   - numeric: group by quantiles; compare mean target / lift
   - categorical: group by category; compare target rate / mean
3. Identify features with suspiciously high predictive power; investigate leakage.

### 7) Segments (Coverage + Performance)
1. Define 3-8 operationally meaningful segments (not too many).
2. Compute: segment size, target rate, and baseline metric per segment.
3. Flag small segments with unstable estimates.
4. Check whether any segment is systematically missing key features.

### 8) Data Splits (Plan Early)
1. Decide split strategy (random, group-based, time-based) based on use case.
2. Ensure splits respect entity boundaries (no same entity in train and test if needed).
3. Ensure splits respect time (no future information in training).

## Time-Based Data Guidance

Use this when the prediction happens at time T and features/labels come from events.

### Leakage Checks
1. For each feature, document the latest timestamp it can use relative to T.
2. Confirm feature windows exclude events after T.
3. Validate joins:
   - use as-of joins where appropriate
   - avoid joining on aggregates computed using future data
4. Run a "canary" check: train a simple model; investigate any near-perfect AUC/R2.

### Stability Over Time
1. Plot (or compute) feature summaries by time bucket (week/month):
   - missing rate
   - mean/median for numeric
   - top category share for categorical
2. Track target rate by time bucket; note seasonality and regime changes.
3. Compute simple drift indicators:
   - PSI (if available) or
   - change-in-mean / change-in-missingness thresholds
4. Validate that historical training periods are representative of deployment.

## Minimal Reporting Templates

### Missingness Summary

| column | dtype | missing_count | missing_rate | notes |
|---|---|---:|---:|---|
| example_feature | float | 123 | 0.045 | empty string treated as missing |

### Segment Performance Snapshot

| segment | segment_def | n_rows | target_rate | metric_baseline | notes |
|---|---|---:|---:|---:|---|
| new_users | signup_age_days <= 30 | 10234 | 0.031 | 0.500 | small lift vs overall |

## Stop Conditions (Pause And Fix Data)

Stop EDA and fix upstream data (or label logic) when any of these are true:

1. Key grain is not consistent (duplicates where unique keys are required).
2. Target definition cannot be validated with concrete source examples.
3. Any feature uses information after prediction time (confirmed leakage).
4. Missingness is high and non-random in ways that change business conclusions.
5. Schema/types are unstable across extracts (columns appear/disappear or change meaning).
6. Segment coverage is too sparse to support reliable evaluation.
