# Pipeline architecture

This document describes a reference ML pipeline with clear stage boundaries,
versioning expectations, parity rules, and operational monitoring.

## Reference pipeline (ASCII)

```
      +--------+   +----------+   +---------+   +-------+   +------+   +---------+   +--------+   +---------+
      | ingest |-->| validate |-->| feature |-->| train |-->| eval |-->| package |-->| deploy |-->| monitor |
      +--------+   +----------+   +---------+   +-------+   +------+   +---------+   +--------+   +---------+

Key artifacts per stage:
- ingest: raw data snapshot (immutable)
- validate: schema + quality report
- feature: feature store tables + feature definitions
- train: model weights + training metadata
- eval: evaluation reports + thresholds/decision
- package: model bundle (weights + code + config)
- deploy: serving endpoint + rollout record
- monitor: dashboards + alerts + incident log
```

## Stage contracts (inputs/outputs)

Keep each stage deterministic given its declared inputs.

1. ingest
   - Input: external sources (DB, events, files)
   - Output: immutable snapshot (partitioned, timestamped)
2. validate
   - Input: snapshot
   - Output: pass/fail + validation report (schema, missingness, ranges)
3. feature
   - Input: snapshot + feature definitions
   - Output: feature tables (training set) + feature computation manifest
4. train
   - Input: feature tables + labels + hyperparams + seed
   - Output: model + training metadata
5. eval
   - Input: model + eval dataset
   - Output: metrics, slices, calibration, threshold decision
6. package
   - Input: approved model + code + config
   - Output: versioned model bundle + signature
7. deploy
   - Input: model bundle
   - Output: deployed version + rollout plan/record
8. monitor
   - Input: serving logs + ground truth (when available)
   - Output: alerts and reports for drift/performance/latency

## Rules for train/serve parity

Goal: the same transformations and assumptions apply in training and serving.

- Single source of truth for features: define features once (code or DSL) and
  reuse for both offline (training) and online (serving).
- Same preprocessing path: avoid duplicated logic in notebooks vs service code.
  Prefer shared library/package used by both.
- Same input schema: validate request schema in serving and match training
  schema (types, ranges, missing-value policy).
- Same defaults: missing handling, clipping, encoding, and bucket boundaries
  must be identical.
- Same time semantics:
  - Training uses point-in-time correct joins (no label leakage).
  - Serving uses only data available at request time.
- Same model signature: enforce a stable input/output contract (feature names,
  order if applicable, units).
- Same dependency versions: pin library versions for both training and serving.
- Reproducibility gate: a sample batch scored offline should match online
  scores within tolerance for the same model bundle.

## Data and versioning checklist

Capture enough metadata to reproduce a run and trace any deployment.

Required per training run:
- Data snapshot:
  - Snapshot id (path/table + partition/time window)
  - Extraction query (or job id) and timestamp
  - Label source version and delay assumptions
- Code version:
  - Git commit SHA for training code
  - Git commit SHA for feature definitions
- Config:
  - Full config file(s) or serialized config blob (not just diffs)
  - Environment variables that affect behavior (explicit allowlist)
- Seeds:
  - Global RNG seed(s) (python/numpy/framework)
  - Data split seed and method
  - Any sampler/shuffle seeds
- Dependencies:
  - Lockfile or container image digest
  - Hardware/accelerator info if relevant
- Outputs:
  - Model artifact id
  - Metrics report id
  - Promotion decision and approver (human or automated rule)

Required per deployment:
- Model bundle version (immutable id)
- Serving config version (traffic split, thresholds, feature flags)
- Rollout record (time, scope, canary criteria, rollback plan)

## Monitoring signals

Track both data health and user-facing behavior.

- Data drift (features):
  - Distribution shift vs training baseline (PSI/KS, mean/variance)
  - Missingness changes, out-of-range rate, new categories
- Label drift / target shift:
  - Label prevalence changes
  - Label delay/backfill anomalies
- Performance (when labels arrive):
  - Primary metric (AUC/F1/RMSE/etc.) overall and by key slices
  - Calibration (ECE, reliability curves)
  - Business metric proxy where applicable
- Latency and reliability:
  - p50/p95/p99 latency
  - error rate/timeouts
  - throughput and saturation

Alerting guidance:
- Prefer two-tier alerts: early warnings (drift) + hard failures (SLO breach).
- Always include: metric name, threshold, time window, and links to dashboards.

## Minimal runbook: metric drops

When an important metric drops (offline eval or online monitored metric):

1. Confirm the drop is real
   - Check time window, sample size, label completeness, and recent deploys.
   - Compare to control group or previous stable period.
2. Triage by category
   - Latency/error spike: treat as serving incident first.
   - Data drift spike: suspect upstream data change or feature pipeline issue.
   - Performance drop with stable data: suspect model bug, leakage removal,
     or concept shift.
3. Identify scope
   - Slice metrics by region, product, cohort, device, and key features.
   - Determine if impact is global or localized.
4. Mitigate
   - Roll back to last known-good model bundle if deploy-related.
   - Disable risky feature(s) via config/feature flag if available.
   - Switch to fallback heuristic if model is unsafe.
5. Root cause and fix
   - Inspect data validation report deltas.
   - Diff feature definitions and training config between good/bad runs.
   - Reproduce scoring parity check (offline vs online) for the bundle.
6. Prevent recurrence
   - Add validation rules, add/adjust alerts, document the incident and the fix.
