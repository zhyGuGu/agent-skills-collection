# State management matrix

Purpose: Compare common Flutter state management options and pick one consistently.

Scope: This matrix compares patterns and tradeoffs. It does NOT assume any package is installed.

## Comparison table

| Option | Best fit | Learning curve | Boilerplate | Testability | Compile-time safety | Community/docs | Notes / watch-outs |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Provider | Small to medium apps; simple DI + ChangeNotifier | Low | Low | Medium | Medium | High | Straightforward and lightweight; can become hard to scale if app grows without clear boundaries. |
| Riverpod | Medium to large apps; explicit state graphs; test-first | Medium | Medium | High | High | High | More explicit than Provider; encourages immutability and separation; adds concepts (providers, scopes, ref/watch). |
| Bloc/Cubit | Large apps; complex flows; teams that want strict structure | Medium to High | High | High | High | High | Very predictable event/state model; more code and patterns; great for feature isolation and reviews. |
| GetX | Small apps or prototypes; fast iteration; opinionated tooling | Low to Medium | Low | Medium | Medium | High | Convenience-focused; can encourage hidden coupling if patterns are not enforced; be strict about boundaries. |

Quick reads of the table:
- If you want minimal ceremony, start with Provider or a small Riverpod setup.
- If your app has complex async flows and many contributors, Bloc/Cubit often pays off.
- If you choose GetX, define constraints early to avoid "everything is global" drift.

## Decision checklist

Use this checklist and pick the simplest option that satisfies the constraints.

- App size and complexity
  - How many screens/features will exist in 3-6 months?
  - How many async workflows (auth, caching, paging, offline, background sync)?
  - Do you need strict feature boundaries (per-feature state) to avoid regressions?
- Team skill and consistency
  - Which patterns does the team already know well?
  - Will new contributors understand the architecture in a day?
  - Can code review reliably enforce the chosen pattern?
- Testability requirements
  - Do you need easy unit tests for state without Flutter bindings?
  - Do you need deterministic state transitions for debugging and replay?
  - Do you need clear dependency injection for mocking services?

## Example recommendations

Example A: Small app (1-2 devs, limited features, low risk)
- Recommendation: Provider (or Riverpod with a minimal provider set).
- Rationale: Lowest overhead; fast to ship; keep state local to widgets/features; add structure only when real complexity appears.

Example B: Large app (multiple squads, long-lived, complex async + many features)
- Recommendation: Riverpod or Bloc/Cubit.
- Rationale: Stronger boundaries and testability; more explicit dependency management; predictable state changes that scale with team size.
