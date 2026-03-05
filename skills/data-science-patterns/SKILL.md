---
name: data-science-patterns
description: Procedural patterns for scoping, exploring, modeling, evaluating, and communicating data science work with repeatable checklists and report outlines.
---

# Data Science Patterns

## When to Use
- You need a repeatable workflow for EDA, feature work, modeling, and evaluation.
- You are translating a business question into measurable targets and decision criteria.
- You must produce clear artifacts (notebooks/reports) that others can review and rerun.
- You are diagnosing model/data issues (leakage, drift, bias, poor calibration).
- You are standardizing how metrics, baselines, and experiments are documented.

## Capabilities
- Problem framing: objective, target definition, constraints, success metrics, baselines.
- Data checks: schema, missingness, duplicates, outliers, data quality rules.
- EDA patterns: univariate/bivariate summaries, segmentation, time and cohort views.
- Modeling patterns: train/val/test splits, cross-validation, leakage prevention.
- Evaluation patterns: metric selection, thresholding, calibration, error analysis.
- Experiment documentation: assumptions, configs, seeds, and reproducibility notes.
- Communication: concise narratives, tables/figures lists, and decision-ready summaries.

## Core Workflow
1. Scope
   - Define the decision to be made and who makes it.
   - Define the target label and prediction time (avoid peeking).
   - Choose primary metric(s) and acceptable trade-offs (latency, cost, risk).
   - Establish baselines (heuristic, existing model, naive predictor).
2. Data Inventory
   - Identify sources, joins, and time windows.
   - Record schema, units, and known quirks.
   - Validate row-level grain and key uniqueness.
3. Data Quality Checks
   - Missingness by feature and segment; confirm handling policy.
   - Duplicates, impossible values, and distribution shifts over time.
   - Label integrity: prevalence, noise indicators, and collection process.
4. EDA
   - Summarize target distribution and key segments.
   - Explore feature distributions and relationships to the target.
   - Identify leakage candidates and proxies (future information).
5. Split Strategy
   - Pick split that matches deployment (time-based for temporal problems).
   - Freeze a test set; use CV/validation for iteration.
   - Ensure all transforms are fit on training data only.
6. Feature & Model Iteration
   - Start simple (linear/tree baseline), then iterate.
   - Track experiments with config, data version, and random seed.
   - Add features only when they improve a relevant metric and pass sanity checks.
7. Evaluation & Error Analysis
   - Report metrics with uncertainty (CI, fold variance) when feasible.
   - Slice performance by key segments; inspect worst-case behavior.
   - Perform threshold analysis and calibration checks if probabilistic.
8. Decision & Handoff
   - Summarize whether the model is better than baseline for the decision.
   - Document limitations, monitoring signals, and retraining triggers.
   - Provide reproducible run instructions and artifacts.

## Common Pitfalls
- Label leakage (using post-outcome features, improper aggregation windows).
- Incorrect split (random split for time series, user leakage across folds).
- Metric mismatch (optimizing AUC when decision needs precision at k).
- Overfitting via repeated test-set peeking or untracked hyperparameter search.
- Data quality issues hidden by global metrics (segment regressions).
- Non-reproducible results (missing seeds, unpinned dependencies, changing data).
- Misleading plots/tables (no denominators, no sample sizes, cherry-picked slices).

## Example Outputs
```text
EDA Summary Outline
- Objective and target definition
- Dataset overview
  - Sources and joins
  - Row count, grain, date range
  - Key entities and uniqueness checks
- Data quality
  - Missingness (overall and by segment)
  - Duplicates and invalid values
  - Outliers and distribution notes
- Target analysis
  - Prevalence and stability over time
  - Segment breakdowns
- Feature exploration
  - Top features by correlation/importance proxy
  - Notable nonlinearities and interactions
  - Leakage/proxy checks
- Initial hypotheses and next steps
```

```text
Model Evaluation Report Outline
- Problem statement and decision context
- Data and split strategy
  - Train/validation/test definitions
  - Leakage controls and preprocessing boundaries
- Baselines
  - Naive/heuristic baseline results
  - Existing model comparison (if applicable)
- Metrics
  - Primary metric(s) and rationale
  - Secondary metrics and constraints
- Overall results
  - Point estimates and uncertainty (CV variance/CI)
  - Confusion matrix at selected thresholds (if classification)
- Calibration and thresholding
  - Reliability curve notes
  - Threshold trade-off table (precision/recall/cost)
- Error analysis
  - Top error slices and examples
  - Segment performance table with sample sizes
- Risks and limitations
  - Known failure modes
  - Fairness/bias considerations (as applicable)
- Recommendation
  - Go/no-go criteria
  - Monitoring plan and retraining triggers
  - Reproducibility details (code, config, data version, seeds)
```
