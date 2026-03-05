---
name: flutter-best-practices
description: Practical guidance for structuring Flutter apps, choosing state management, handling async and navigation, improving performance, testing, and maintaining consistent style.
---

# Flutter Best Practices

## When to Use
- Starting a new Flutter app and need a baseline architecture.
- Refactoring an existing app with inconsistent patterns.
- Choosing state management for a specific feature or app scale.
- Reviewing performance regressions (jank, rebuilds, startup time).
- Establishing testing strategy and CI checks.

## Capabilities
- Recommend app structure (layers, feature folders) aligned with existing codebase.
- Recommend state management based on constraints (team size, complexity, testability).
- Identify common performance pitfalls and prioritized fixes.
- Provide guidance for async/error handling, navigation, theming, and localization.
- Propose testing pyramid and concrete test cases (unit/widget/integration).
- Suggest linting and formatting conventions to reduce churn.

## Core Workflow
1. Gather constraints: target platforms, app size, team experience, existing patterns.
2. Map current code structure: features, dependencies, navigation, state boundaries.
3. Choose a default architecture and state approach; document exceptions.
4. Define conventions: folder layout, naming, error handling, logging, DI.
5. Create a performance plan: measure first, then optimize in priority order.
6. Add tests and checks: smoke tests, critical flows, lint, and CI gates.

## Example Outputs

```text
State management recommendation

Context:
- App size: medium (10-20 screens), growing
- Team: 3 developers, wants predictable patterns and testability
- Needs: offline caching, background refresh, multiple feature teams

Recommendation:
- Use Riverpod (or Provider if already established) with a feature-first structure.
- Keep UI state local (TextEditingController, focus, animations) in widgets.
- Keep domain state in Notifiers/Controllers per feature; expose immutable state.
- Use repository layer for data sources (network/db) and keep it pure/testable.
- Standardize error handling with a Result/Either type and map to UI states.

Decision notes:
- Prefer one approach across the app; allow exceptions only with rationale.
- Avoid global singletons; inject repositories and services via providers.
```

```text
Performance review checklist

Measurement
- Reproduce on a physical device; record Flutter DevTools timeline.
- Capture frame timings (raster/UI), memory, and CPU; note device + build mode.

Build and rebuild
- Verify const usage where possible; avoid unnecessary rebuilds.
- Check for large widgets rebuilding from high-level setState.
- Add RepaintBoundary for expensive, frequently-changing regions.

Lists and images
- Use ListView.builder/SliverList for long lists; avoid shrinkWrap unless needed.
- Use cached image loading; set appropriate cacheWidth/cacheHeight for thumbnails.

Async and I/O
- Move JSON parsing and heavy work off the UI isolate (compute/isolate).
- Batch disk reads/writes; avoid synchronous I/O on the UI thread.

Startup
- Defer non-critical initialization; show first frame quickly.
- Audit plugins and fonts/assets; remove unused and minimize eager loads.
```
