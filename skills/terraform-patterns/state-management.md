# Terraform State Management Strategies

Purpose: define how Terraform state is stored, protected, operated on, and recovered.

## Remote state backends and locking

Procedure:
1. Prefer a remote backend for any shared environment. Local state is only acceptable for throwaway sandboxes.
2. Require state locking to prevent concurrent applies.
3. Store state in a durable object store; store locks in a strongly consistent system.
4. Enable versioning on the state object store and retain versions long enough to cover incident response.

Common patterns:

- S3 + DynamoDB (locking)
  - Locking: DynamoDB table with a primary key of `LockID`
  - Storage: S3 bucket with versioning + SSE enabled
- GCS + Terraform state locking (via GCS preconditions)
  - Storage: GCS bucket with object versioning + CMEK if required
- AzureRM Storage (blob leases)
  - Storage: Storage account + container; locking via blob lease
- Terraform Cloud / Enterprise
  - Storage + locking are provided; use workspace policies and RBAC

Backend configuration checks (minimum bar):
- Locking is enabled and verified by a parallel apply test.
- The backend is reachable from CI runners and approved operator networks.
- Versioning is enabled on the bucket/container.
- Encryption is enabled (provider-managed or customer-managed as required).

## Workspace vs separate state decision

Goal: isolate blast radius while keeping operations simple.

Decision procedure:
1. Identify isolation boundary: environment (dev/stage/prod), region, tenant/customer, or account/subscription/project.
2. Default to separate state files for isolation boundaries that change IAM, network, or data-plane risk.
3. Use workspaces only when all workspaces share the same:
   - Credentials / account context
   - Backend configuration
   - Lifecycle controls and access model
   - Failure domain and compliance requirements

Recommended defaults:
- Separate state per environment (dev/stage/prod): yes.
- Separate state per account/subscription/project: yes.
- Separate state per region when regional failure domain matters: usually yes.
- Workspaces for ephemeral stacks (PR environments) in the same account: acceptable.

Avoid:
- Mixing prod and non-prod via workspaces in one state backend path.
- Sharing a state across teams with different change windows or ownership.

Naming convention (example):
- Backend key/prefix: `<org>/<app>/<env>/<region>/<stack>.tfstate`

## State operations runbook

General rules:
- Never edit state files by hand.
- Always run state operations from a clean git tree and a pinned Terraform version.
- Capture evidence: command, plan output, and before/after resource addresses.
- Prefer `-refresh-only` and narrow targets for safety during incident response.

### Import

Use when:
- A real resource exists but is not tracked by Terraform.

Procedure:
1. Confirm the resource should be managed by this module and state (ownership check).
2. Add configuration first (resource block, arguments, lifecycle).
3. Run `terraform plan` to confirm Terraform wants to create the resource.
4. Run `terraform import <address> <id>`.
5. Run `terraform plan` until it is no-op or only expected diffs remain.

Pitfalls:
- Importing into the wrong module path/address.
- Importing a resource that is partially managed elsewhere (split ownership).

### Move (state mv)

Use when:
- Refactoring module structure, renaming resources, or changing `for_each` keys.

Procedure:
1. Make the code change that introduces the new address.
2. Run `terraform state mv <old_address> <new_address>`.
3. Run `terraform plan` and confirm no destroy/recreate occurs unless intended.
4. Apply during a controlled window for prod.

Notes:
- For large refactors, script the mv operations and review the generated list.

### Remove (state rm)

Use when:
- A resource should no longer be managed by Terraform but must remain in the provider.

Procedure:
1. Remove or disable the resource configuration (or add `lifecycle { prevent_destroy = true }` if keeping).
2. Run `terraform state rm <address>`.
3. Run `terraform plan` and confirm Terraform does not plan to recreate it.

Warnings:
- `state rm` does not delete the real resource. It only removes tracking.
- If config still exists, Terraform may attempt to recreate the resource.

### Drift detection and response

Detect drift:
1. Run `terraform plan -refresh-only` on a schedule in CI.
2. Alert on non-empty drift and attach the diff output.

Respond to drift (procedure):
1. Classify drift: expected manual change, emergency change, or unauthorized change.
2. If expected: update code to match reality, then apply.
3. If emergency: capture the change record, then decide whether to codify or roll back.
4. If unauthorized: revoke access if needed, revert change, and consider state recovery if corrupted.

## Backup and recovery checklist

Backups (preventive):
- Enable object versioning on state storage.
- Enable lifecycle retention for old versions (do not delete immediately).
- Export periodic snapshots (at least daily for prod) to a separate backup location/account.
- Store backend config and state key naming in repo docs so operators can find the right state.

Recovery (when state is lost or corrupted):
1. Stop automation that runs Terraform against the affected state.
2. Identify the correct backend location and state key/prefix.
3. Restore the last known good state version (or snapshot) to the original object key.
4. Run `terraform init -reconfigure` to ensure the backend points to the restored object.
5. Run `terraform plan -refresh-only` to validate state vs reality.
6. If resources are missing from state, import them explicitly (do not guess addresses).
7. After recovery, run a normal `terraform plan` and apply only intentional changes.
8. Post-incident: add guardrails (RBAC, versioning, approvals, CI restrictions).

Integrity checks:
- Verify state JSON is valid and readable by the pinned Terraform version.
- Confirm locking works before re-enabling CI applies.

## Security considerations

Encryption:
- Require encryption at rest for state storage (SSE or provider equivalent).
- Prefer customer-managed keys (KMS/CMEK/Key Vault) for regulated environments.
- Require TLS for all backend access.

Access control:
- Treat state as sensitive: it can contain resource IDs, ARNs, IPs, and sometimes secrets.
- Grant least privilege: read-only for auditors, read/write only for deploy roles.
- Separate prod state access from non-prod access.
- Use short-lived credentials (OIDC) for CI; avoid long-lived static keys.

Change control:
- Restrict who can delete or overwrite state objects.
- Enable bucket/container-level logs (access logs, CloudTrail/Audit Logs) and alert on deletes.
- Require code review for backend changes (state key, backend type, encryption settings).

Secret handling:
- Avoid putting secrets in state by design (use secret managers and data sources).
- If a secret is known to have landed in state, treat it as compromised and rotate it.
