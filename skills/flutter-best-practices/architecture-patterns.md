# Architecture patterns

This guide describes a pragmatic way to structure Flutter apps so they stay easy to
change as features grow.

## Goals

- Keep UI code simple and testable.
- Isolate business rules from frameworks.
- Make dependencies explicit and replaceable.
- Keep features cohesive and avoid cross-feature coupling.

## Recommended folder structure

Pick the simplest structure that supports your current size. Re-organize when a
single folder starts to become a dumping ground (usually when you have 4-6+
distinct features).

### Small app (single team, few features)

Keep a flat-ish structure and separate by concerns:

```text
lib/
  main.dart
  app/
    app.dart
    routes.dart
    di.dart
  features/
    counter/
      counter_page.dart
      counter_controller.dart
      counter_state.dart
  shared/
    widgets/
    theme/
    utils/
```

Rules:
- `features/` contains user-facing use cases.
- `shared/` contains truly reusable code (avoid putting feature code here).
- Keep each feature small; prefer co-locating the pieces that change together.

### Large app (many features, long-lived)

Use a feature-first structure with layers inside each feature. This keeps
boundaries clear and minimizes cross-feature imports.

```text
lib/
  main.dart
  app/
    app.dart
    bootstrap.dart
    di/
      container.dart
      registrations.dart
    navigation/
      router.dart
      routes.dart
  features/
    auth/
      presentation/
        pages/
        widgets/
        state/
      domain/
        entities/
        use_cases/
        repositories/
      data/
        datasources/
        models/
        repositories/
    payments/
      ...
  shared/
    presentation/
      widgets/
    domain/
      value_objects/
    data/
      network/
      storage/
```

Rules:
- Each feature owns its `presentation/`, `domain/`, and `data/`.
- The app shell (`app/`) wires dependencies, global navigation, and lifecycle.
- Cross-cutting code goes in `shared/` but keep it small and stable.

## Layering guidance (presentation / domain / data)

### Presentation layer

What goes here:
- Widgets, pages, UI state holders (controllers/view-models), UI-only models.
- Mapping domain output into view state.

Guidelines:
- Do not import `data/` from `presentation/`.
- Keep framework-specific code here (Flutter, routing, state management).
- Favor unidirectional flow: user intent -> domain call -> render state.

### Domain layer

What goes here:
- Business rules: use cases, domain services, entities/value objects.
- Repository interfaces (contracts) that describe what the app needs.

Guidelines:
- Domain should have no Flutter imports.
- Prefer small use cases that match a single user goal.
- Make invariants explicit (validation, permissions, state transitions).

### Data layer

What goes here:
- API clients, database adapters, caching, and repository implementations.
- DTO/models and mapping to/from domain entities.

Guidelines:
- Implement domain repository interfaces here.
- Keep mapping at the edge (do not leak DTOs into domain/presentation).
- Make failures explicit (timeouts, parsing, auth, offline).

### Dependency direction

Keep dependencies flowing inward:

```text
presentation -> domain <- data
```

- Presentation depends on domain.
- Data depends on domain (to implement repository contracts).
- Domain depends on nothing else in your app.

## Dependency injection (conceptual)

Goals:
- Build objects in one place (composition root) and pass dependencies in.
- Keep constructors simple and explicit.
- Allow swapping implementations (real vs fake) for tests.

Guidance:
- Define repository interfaces in `domain/`.
- Implement repositories in `data/`.
- In `app/di/`, register concrete implementations and expose a container.
- Presentation requests abstractions (interfaces) instead of concrete classes.
- Avoid service locators inside domain logic; pass dependencies as parameters.

Testing approach:
- Unit test domain use cases with fake repository implementations.
- Widget/UI tests can inject fake controllers or fake repositories.

## Navigation and feature boundaries

Principles:
- Navigation defines feature boundaries; crossing boundaries should be explicit.
- Prefer navigation via route names/typed routes over direct widget imports.

Practical rules:
- `app/navigation/` owns the route table and route parsing.
- A feature should not import another feature's `data/` or `domain/`.
- If Feature A needs something from Feature B, extract a shared domain contract:
  - Put a small interface or value object in `shared/domain/` (or a dedicated
    `core/` domain folder) and depend on that.
- Keep route arguments small and stable: IDs, enums, and simple value objects.
- Keep deep linking in the app shell, not inside feature widgets.

When to split a feature:
- It has multiple independent screens and workflows.
- It owns distinct data sources and domain rules.
- Multiple teams touch it and PRs frequently conflict.

## Architecture review checklist

Use this as a quick PR review guide:

- Layers are respected: presentation does not import data.
- Domain has no Flutter imports and holds business rules.
- Repository interfaces live in domain; implementations live in data.
- DTOs/models do not leak into domain or UI.
- Feature boundaries are enforced (minimal cross-feature imports).
- Navigation is centralized and arguments are simple and stable.
- Dependencies are constructed in one composition root; tests can swap fakes.
