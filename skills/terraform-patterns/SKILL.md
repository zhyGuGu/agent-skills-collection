---
name: terraform-patterns
description: "Practical, repeatable patterns for authoring and reviewing Terraform code: module design, state/backends, providers, naming/tagging, IAM boundaries, safe refactors, and plan/apply workflows. Focus on predictable diffs, least privilege, composable modules, environment separation, and operational safety."
---

# Terraform Patterns

## When to Use
- Writing or refactoring Terraform modules and wanting consistent structure and interfaces.
- Reviewing Terraform changes and needing a checklist for safety, drift, and blast radius.
- Standardizing provider configuration, state/backends, and environment layouts.
- Designing naming/tagging conventions and enforcing them across resources.
- Planning migrations (moved blocks, import, state mv) without disrupting production.
- Creating runbooks for plan/apply (local or CI) with approvals and safeguards.

## Capabilities
- Propose module boundaries, inputs/outputs, and versioning strategy.
- Identify anti-patterns (implicit dependencies, hidden provider config, unsafe lifecycle).
- Recommend state/backend layout (workspaces vs separate state, locking, encryption).
- Produce review checklists tailored to a repo (security, cost, drift, testing).
- Outline safe change workflows (plan review, apply gates, rollbacks, state ops).
- Provide examples for moved/import blocks and low-risk refactors.

## Core Principles
- Prefer small, composable modules with explicit inputs/outputs.
- Keep provider configuration centralized; avoid module-level provider surprises.
- Minimize diff noise; stabilize ordering, names, and computed attributes where possible.
- Separate environments explicitly (folders/accounts/subscriptions); avoid accidental cross-env coupling.
- Treat state as critical data (locking, encryption, backups, least-privileged access).
- Make destructive actions intentional (prevent_destroy, requires-replace awareness, approvals).
- Document invariants (naming, tagging, IAM boundaries) and enforce via validation where feasible.

## Example Outputs

```text
Module review checklist

Scope and interface
- Module purpose is narrow and documented
- Inputs have types, descriptions, and sensible defaults (if any)
- Validation blocks exist for critical invariants (CIDRs, names, enums)
- Outputs are minimal, stable, and avoid leaking sensitive values

Providers and dependencies
- Provider requirements are pinned (constraints are intentional)
- No unexpected provider configuration inside the module
- Dependencies are explicit (no hidden ordering via count/index hacks)

State and safety
- Resource addressing is stable (for_each keys are stable identifiers)
- Changes that force replacement are called out with blast radius
- Lifecycle meta-arguments are justified (create_before_destroy, ignore_changes)
- prevent_destroy used for truly critical resources (and documented)

Security and compliance
- IAM is least privilege; wildcards are justified and bounded
- Sensitive inputs/outputs are marked sensitive
- Tags/labels meet org requirements (owner, env, cost center)

Operations
- README includes usage example and upgrade notes
- Plan output is reviewed for destroy/replace and high-cost deltas
```

```text
Plan/apply workflow outline

1) Pre-flight
- Select the target environment (account/project/subscription, region)
- Ensure backend is configured (locking enabled, encryption enabled)
- Confirm the workspace or state key matches the environment

2) Initialize
- terraform init (with backend config as needed)
- terraform validate

3) Plan
- terraform plan -out=tfplan
- Review the plan for:
  - destroys
  - force-replace changes
  - provider/version drift
  - unexpected resource count changes
  - high-cost resources

4) Approvals
- Require review/approval for any destroy/replace
- Capture the plan artifact (tfplan) for the approved change

5) Apply
- terraform apply tfplan
- Monitor provider/API errors and partial applies

6) Post-apply
- Re-run terraform plan to confirm no drift
- Record change notes (what changed, why, rollback notes)

7) Rollback strategy (when applicable)
- Prefer reverting code and re-applying
- For state/address refactors, use moved/import/state mv only with a written procedure
```
