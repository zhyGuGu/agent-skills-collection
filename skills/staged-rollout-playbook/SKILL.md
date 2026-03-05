---
name: staged-rollout-playbook
description: A safe rollout and rollback playbook for shipping changes behind flags, with ramp schedules, health metrics, alert thresholds, and a copy/paste release checklist.
---

# Staged Rollout Playbook

Use this skill to ship changes with controlled risk: progressive rollout, monitoring, and fast rollback.

## When to Use
- A change has high blast radius (auth, payments, infra, core UX).
- You are migrating a backend, schema, or client behavior.
- You need a repeatable release checklist shared across teams.

## Inputs
Ask for:
- Target surface: backend service, web client, mobile app.
- Rollout mechanism: feature flags, canary, weighted routing, app store phased release.
- Key health metrics: error rate, latency, conversion, crashes.
- Rollback options and time-to-rollback constraints.

## Workflow
1. Define health signals and thresholds
2. Implement rollout controls (flag/canary) and guardrails
3. Run a pre-release checklist (migrations, backwards compatibility)
4. Ramp in stages with hold points
5. Declare success criteria and deprecate old paths

## Outputs

### Rollout Checklist
```text
Release: <name>

Pre-flight
- [ ] Backward compatible changes only (new readers before new writers)
- [ ] Rollback path confirmed (how + who)
- [ ] Dashboards and alerts ready

Ramp plan
- [ ] Stage 0: internal/test users
- [ ] Stage 1: 1% for 30-60 min
- [ ] Stage 2: 10% for 2-24 hours
- [ ] Stage 3: 50%
- [ ] Stage 4: 100%

Hold criteria
- [ ] Error rate < <threshold>
- [ ] P95 latency < <threshold>
- [ ] Conversion/crash regression < <threshold>

Rollback
- [ ] Trigger conditions defined
- [ ] Steps documented
- [ ] Post-rollback verification steps
```

## Differentiator
This skill explicitly couples rollout stages to measurable hold criteria and rollback triggers, so "ship" is an operational decision, not just a merge.
