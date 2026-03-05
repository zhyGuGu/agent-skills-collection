# Module design principles

This document is a practical checklist for designing Terraform modules that are
predictable to consume, easy to review, and safe to upgrade.

## Module boundary rules

Use these rules to decide what belongs inside a module vs in the caller (root
module or another module).

Module owns:
- A cohesive capability with a single responsibility (one "thing" well).
- The resources and data sources required to implement that capability.
- The internal naming conventions, defaults, and wiring between resources.
- Opinionated implementation details that callers should not need to know.
- Exposed outputs that are stable integration points for callers.

Caller owns:
- Environment-specific policy and placement (account/project, region, VPC,
  subnets, DNS zones, org folders, etc.).
- Cross-cutting conventions (tags/labels, naming prefixes, budgets, logging) if
  they must be consistent across many modules.
- Decisions that change frequently (feature flags, scale settings, instance
  sizes) unless the module's responsibility is to encapsulate them.
- Orchestration between modules (wiring outputs from one to inputs of another).

Boundary guidelines:
- Do not embed provider configuration inside reusable modules.
- Avoid hidden dependencies on implicit provider behavior; make assumptions
  explicit via inputs or documented constraints.
- Prefer one module per lifecycle boundary. If two resources are frequently
  created/destroyed together, they can belong together.
- Avoid giant "platform" modules. Split by capability, then compose.

## Inputs and outputs

### Input guidelines

Types:
- Always specify `type` for variables. Prefer object types for structured input.
- Use `nullable = false` for required values to fail early.
- Prefer `map(object({ ... }))` for sets of similar items keyed by stable IDs.

Defaults:
- Provide defaults only when they are safe in all expected environments.
- Avoid defaults that create resources unexpectedly (surprising side effects).

Validation:
- Add `validation` blocks for constraints that cannot be represented by types.
- Validate mutual exclusivity and required-together fields.
- Fail with clear, actionable error messages.

Sensitivity:
- Mark secrets as `sensitive = true` on variables and outputs.
- Avoid passing secrets through outputs unless required for integration.
- Do not log or template secrets into user-data where possible.

Ergonomics:
- Keep variable names consistent: `name`, `labels`, `tags`, `description`.
- Prefer fewer, higher-level inputs over many low-level toggles.
- Document each input with behavior, not implementation.

### Output guidelines

Stability:
- Outputs are part of the module API; avoid changing their meaning.
- Prefer outputs that represent identifiers used for wiring (IDs, ARNs, names).

Scope:
- Do not output entire resources unless needed. Prefer the specific attributes.
- If outputting collections, use stable keys so callers can index reliably.

Sensitivity:
- Mark outputs as `sensitive = true` if they contain secrets or derived secrets.

## for_each and count

Prefer `for_each` over `count` for collections so resource addresses are stable.

Stable keys:
- Use keys that are intrinsic identifiers (e.g., "app", "db", "public").
- Do not key by list index, random values, or computed ordering.
- If accepting a list from callers, convert to a map with explicit keys.

Guidance:
- Use `count` only for 0/1 style toggles when there is no natural key.
- When changing keys, treat it as a breaking change; it can force recreation.
- Keep the `for_each` expression simple and deterministic.

## Versioning and upgrades

Treat the module as a versioned product with an API.

Versioning:
- Use semantic versioning for published modules.
- Patch: bug fixes, internal refactors with no behavior change.
- Minor: backward-compatible features or new outputs.
- Major: breaking changes to inputs/outputs, resource addresses, or behavior.

Upgrade notes:
- Maintain a `CHANGELOG` (or release notes) for every published version.
- For breaking changes, document the migration steps with example diffs.
- Call out changes that might force resource replacement.
- If possible, provide a transitional path (accept old and new input forms for
  one minor release) and deprecate with clear warnings.

Compatibility:
- Pin minimum Terraform version and required provider versions.
- Avoid using experimental features in shared modules.
- Consider adding tests that run against supported Terraform versions.

## Review checklist

Use this checklist in code review for modules.

Module boundary:
- The module has a single responsibility and a clear lifecycle boundary.
- No provider configuration is embedded in the module.
- Cross-cutting concerns are not duplicated unnecessarily across modules.

Inputs/outputs:
- All variables have explicit types, descriptions, and sensible nullability.
- Validation exists for non-trivial constraints and edge cases.
- Sensitive inputs/outputs are marked `sensitive = true`.
- Outputs are stable, minimal, and keyed predictably for collections.

Address stability:
- `for_each` keys are stable and not derived from ordering.
- Changing keys or structure is treated as a breaking change.

Upgrades:
- Versioning strategy is clear; breaking changes are documented.
- Upgrade notes describe expected plan changes and migration steps.

Maintainability:
- Naming is consistent; locals are used to avoid duplication.
- The module is readable without external context; assumptions are documented.
