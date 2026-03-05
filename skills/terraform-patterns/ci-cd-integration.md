# CI/CD Integration (Terraform)

This document describes a minimal, safe Terraform CI/CD pattern for pull requests
and protected deployments. Keep the pipeline small, deterministic, and auditable.

## Minimal pipeline stages

Implement these stages in order. Fail fast and stop the pipeline on any failure.

1. fmt
   - Run `terraform fmt -check -recursive`.
   - Fail if formatting changes are required.

2. validate
   - Run `terraform init` with a read-only or ephemeral backend where possible.
   - Run `terraform validate`.

3. lint
   - Run `tflint` (and optional policy-as-code checks) with pinned versions.
   - Treat new findings as failures for changed code paths.

4. plan
   - Run `terraform plan` using the target environment inputs.
   - Store outputs as build artifacts (plan file + plan summary).

5. approval
   - Require an explicit approval gate for production (and optionally staging).
   - Enforce protected branches/tags and required reviewers.

6. apply
   - Run `terraform apply` using the previously generated plan artifact.
   - Block applies from PR contexts; allow only from protected refs.

## PR workflow guidance

Use PRs to preview changes, not to deploy.

- Plan artifact
  - Generate a binary plan: `terraform plan -out=plan.tfplan`.
  - Export a human-readable summary:
    - `terraform show -no-color plan.tfplan > plan.txt`
    - Optional: `terraform show -json plan.tfplan > plan.json` (for automation)
  - Upload `plan.tfplan` and `plan.txt` as CI artifacts with a short retention.

- Comment output
  - Post a short plan summary back to the PR (truncated if needed):
    - Include counts: add/change/destroy.
    - Include affected workspaces/environments and modules.
    - Link to the full artifact rather than pasting megabytes into comments.
  - Do not post secrets, backend config, or full state-derived values.

- Determinism
  - Pin tool versions (Terraform, providers, linters).
  - Ensure `terraform.lock.hcl` is committed and honored.
  - Avoid time-based or random values that change every run.

## Safety gates

Add explicit gates that detect risky plans and enforce environment scoping.

### Destroy and replace detection

Fail the plan stage (or require elevated approval) if any of these are true:

- Any resource will be destroyed.
- Any resource will be replaced (create_before_destroy still counts as replace).
- Any provider change is detected (provider upgrades can trigger wide diffs).

Implementation options:

- Text parsing (simple)
  - Parse `plan.txt` for patterns like `Plan: .* to destroy` or `must be replaced`.
  - Keep the matcher strict and unit-tested to avoid false negatives.

- JSON parsing (recommended)
  - Parse `plan.json` and fail when any `resource_changes[].change.actions`
    contains `delete` or `delete_create`.

### Environment scoping

Prevent accidental cross-environment changes.

- One environment per pipeline run
  - Require an explicit environment input (e.g., `dev`, `staging`, `prod`).
  - Map the environment to:
    - backend key/prefix
    - workspace name (if using workspaces)
    - variable files and secrets

- Protected environments
  - Only allow `apply` for `prod` from protected refs.
  - Require manual approval and/or change management metadata.

- Least privilege
  - Use separate cloud accounts/subscriptions/projects per environment.
  - Use separate state backends per environment where feasible.

## Secrets handling

Avoid long-lived credentials and never expose secrets in logs.

- Prefer short-lived credentials
  - Use OIDC/workload identity federation to obtain ephemeral cloud credentials.
  - Avoid storing static access keys in CI variables where possible.

- Store secrets in the CI secret manager
  - Store only what is necessary (principle of least privilege).
  - Rotate secrets regularly; treat pipeline failures as potential leak signals.

- Redaction and logging
  - Do not echo secrets.
  - Avoid `set -x` and similar shell debug modes.
  - Use `terraform show -no-color` and sanitize output before commenting.
  - Ensure provider/debug logs are disabled unless debugging and access-limited.

- Separate plan and apply credentials
  - Plan can often run with read permissions.
  - Apply requires write permissions; restrict to protected contexts.

## Rollback guidance

Terraform rollbacks are usually "roll forward" with a corrective change.
Plan for safe recovery rather than assuming an automatic revert.

- Use versioned, immutable modules
  - Pin module versions (tags/SHAs) so you can revert by changing a reference.

- Keep state healthy
  - Use remote state with locking.
  - Back up state (or rely on backend versioning) and restrict access.

- Recovery procedure
  1. Identify the last known good deployment (commit/tag + environment).
  2. Re-run `plan` against the same environment with the corrective change.
  3. Require approval if the plan includes replace/destroy actions.
  4. Apply using the approved plan artifact.

- When rollback is not possible
  - Some changes are inherently destructive (e.g., data deletion).
  - For those, enforce extra gates, backups, and explicit runbooks.

## Implementation checklist

- Pipeline stages: fmt, validate, lint, plan, approval, apply
- PR comments: short summary + artifact links (no secrets)
- Safety gates: destroy/replace detection + environment scoping
- Secrets: OIDC/ephemeral creds, redaction, least privilege
- Rollback: versioned modules, state locking/versioning, recovery procedure
