# Multi-cloud patterns (Terraform)

Multi-cloud usually means one of:
- Same product deployed to multiple clouds.
- Different parts of a system living in different clouds.
- Migration phase where both clouds run in parallel.

Treat multi-cloud as a product decision first, then a code-organization decision.

## Goals

- Standardize what can be standardized (interfaces, naming, metadata).
- Isolate what must differ (provider APIs, IAM, networking primitives).
- Keep blast radius and cognitive load low.

## Common abstractions to standardize

Use the same vocabulary everywhere. The goal is consistent inputs/outputs even when implementations differ.

### Naming and IDs

- Resource name pattern: `<org>-<app>-<env>-<region>-<component>` (keep under each provider's limits).
- Environment keys: `dev`, `staging`, `prod` (avoid `production` vs `prod` drift).
- Stable identifiers: prefer explicit `name`/`id` variables over string concatenation in many places.
- Randomness: if needed, centralize (one `random_id` per component) to avoid churn.

### Tags / labels / metadata

Standard tag set (map of strings) carried through every module:

- `org`
- `app`
- `env`
- `owner`
- `cost_center`
- `managed_by` = `terraform`
- `repo`
- `data_classification` (or similar governance key)

Implementation:
- AWS: map -> `tags`
- Azure: map -> `tags`
- GCP: split: labels/metadata depending on resource; keep a translation layer.

### Regions / zones

- Normalize region variable names: `region`, `zones` (list), `primary_zone` (optional).
- Keep a provider-specific map for availability zones/regions when names diverge.
- Do not assume 1:1 parity (example: 3 AZs available in one region vs 2 zones elsewhere).

### IAM concepts (normalize the model)

Define a cloud-agnostic intent model in variables/outputs, then adapt:

- Identity: `principal` (human or workload)
- Scope: `scope` (project/subscription/account + optional resource path)
- Permission set: `roles` (list of role identifiers in a canonical namespace)
- Separation of duties: `admin_roles` vs `runtime_roles`

Recommended practice:
- Keep canonical roles in your repo (example: `roles/runtime.read`, `roles/runtime.write`).
- Use per-provider mapping tables to translate canonical roles to AWS/GCP/Azure roles.

## Provider-specific gotchas (short list)

Keep these as quick checks during reviews.

### AWS

- Provider regions are per-provider block; cross-region resources often require provider aliases.
- IAM is eventually consistent; plan/apply ordering can be flaky right after creating roles/policies.
- Some services enforce unique global names (S3 bucket names are global).
- Tag propagation is inconsistent across services; confirm which resources actually support tags.

### GCP

- Many resources are tied to a `project`; multi-project setups need explicit project wiring.
- APIs must be enabled per project; missing `google_project_service` can cause apply failures.
- Labels differ from metadata; label key rules are stricter than typical tag keys.
- IAM is policy-based; be careful with authoritative vs additive bindings to avoid role clobbering.

### Azure

- Resources usually live in a resource group; lifecycle of the RG affects everything.
- Provider features and defaults can change behavior; pin provider versions and set features explicitly.
- Naming constraints vary widely; storage accounts have strict lowercase/length rules.
- Role assignments can race due to eventual consistency; may need retries or explicit dependencies.

## Recommended directory layout for multi-cloud repos

Pick a layout that makes intent obvious and keeps provider differences contained.

Minimal, scalable layout:

```text
.
├─ modules/
│  ├─ core/
│  │  ├─ naming/
│  │  ├─ tagging/
│  │  └─ identity-model/
│  ├─ aws/
│  │  ├─ network/
│  │  ├─ compute/
│  │  └─ data/
│  ├─ gcp/
│  │  ├─ network/
│  │  ├─ compute/
│  │  └─ data/
│  └─ azure/
│     ├─ network/
│     ├─ compute/
│     └─ data/
├─ stacks/
│  ├─ dev/
│  │  ├─ aws/us-east-1/app1/
│  │  ├─ gcp/us-central1/app1/
│  │  └─ azure/eastus/app1/
│  ├─ staging/
│  └─ prod/
├─ policies/
│  ├─ roles-canonical/
│  └─ provider-maps/
├─ scripts/
└─ README.md
```

Notes:
- `modules/core` contains provider-agnostic helpers only (naming, tag standardization, canonical IAM model).
- Provider modules live under `modules/<provider>` and implement the real cloud resources.
- `stacks/` is where you compose modules into deployable units (one stack per env/provider/region/app).

## Decision guide: shared modules vs per-provider modules

Decision rule: share the interface, not the implementation.

Use a shared module (provider-agnostic) when:

- It is pure logic/data (naming, tag normalization, role mapping tables).
- It composes only other modules and can delegate provider work to adapters.
- The outputs are identical across clouds (example: internal naming convention, not a cloud resource ID).

Keep separate per-provider modules when:

- The underlying primitives differ (VPC vs VNet vs VPC Network; LB and firewall models).
- The security model differs in ways that change behavior (IAM policy vs RBAC vs bindings).
- The operational knobs are meaningfully different (autoscaling behavior, managed DB parameters).
- You need provider-specific workarounds or lifecycle handling.

Practical pattern (recommended):

- Define a canonical input contract in docs and variables (example: `network_cidr`, `subnets`, `private_dns_enabled`).
- Implement `modules/aws/network`, `modules/gcp/network`, `modules/azure/network` with the same variable names.
- In stacks, select the provider module explicitly (no runtime switching inside a module).

Avoid these anti-patterns:

- One mega-module with `if provider == "aws"` branching.
- Passing provider blocks deeply through unrelated modules without clear ownership.
- Mixing state for multiple clouds in one state file unless the lifecycle is truly coupled.

## Quick checks before you standardize

- Decide the unit of state: per env/provider/region is the common default.
- Pin provider versions; align Terraform versions across teams.
- Make naming and tag standards testable (lint/policy checks) so drift is caught early.
