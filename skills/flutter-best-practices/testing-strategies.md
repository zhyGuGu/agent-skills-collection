# Testing strategies

This guide describes a practical testing strategy for Flutter apps that balances confidence, speed, and maintainability.

## Testing pyramid (Flutter)

Aim for a wide base of fast tests and a small number of end-to-end checks.

- Unit tests (most)
  - What: pure Dart logic (parsing, formatting, validation, reducers, services, mappers).
  - Why: fastest feedback; easiest to run on every change.
  - Tools: `package:test`, `mocktail`/`mockito` when needed.

- Widget tests (some)
  - What: one widget or small widget tree (rendering, interaction, navigation within a small scope).
  - Why: verifies UI behavior without a full device/emulator.
  - Tools: `flutter_test`.

- Integration tests (few)
  - What: a full user flow across screens and layers.
  - Why: catches wiring issues (routing, plugins, real async, real frame scheduling).
  - Tools: `integration_test`.

Rule of thumb: keep unit and widget tests fast enough to run on every PR; keep integration tests minimal and high value.

## What to mock vs what to test real

Default to testing real code for your own logic and using fakes/mocks only at boundaries.

### Test real

- Pure functions and domain logic
  - Example: price calculation, form validation, sorting/filtering, mapping API models to domain models.

- View-model/state logic
  - Example: BLoC/Cubit/Notifier behavior, state transitions, error handling.

- Serialization and parsing
  - Prefer real JSON fixtures and real `fromJson`/`toJson` paths.

- Repository/service composition (when feasible)
  - Use in-memory fakes for data sources to test how components work together.

### Mock or fake

- External boundaries
  - HTTP clients, database drivers, platform channels, file system, secure storage, analytics, push notifications.
  - Reason: they are slow, flaky, and harder to control.

- Time and randomness
  - Inject a `Clock`/`DateTimeProvider` and random generator so tests are deterministic.

- Complex collaborators with many failure modes
  - Use a fake that implements the minimal surface area used by the system under test.

### Prefer fakes over mocks when

- You can model behavior simply (in-memory store, deterministic responses).
- You want less brittle tests (fewer interaction assertions).

### Prefer mocks when

- You need to assert an interaction contract ("called once with X").
- The collaborator is expensive to fake and your test is focused on wiring.

### Keep tests stable

- Avoid over-mocking widget trees. Test behavior (visible text, enabled buttons, navigation) rather than implementation details.
- If a test breaks due to harmless refactors (renaming, moving widgets), reduce interaction expectations and assert outcomes.

## Golden tests

Golden tests compare rendered widgets to reference images.

Use goldens when:

- Visual regressions are costly (design-system widgets, complex layouts, custom paint, charts).
- A widget has many visual states that are tedious to assert with text-only expectations.

Avoid goldens when:

- The UI changes frequently (early prototyping) and you will spend time reblessing images.
- The widget depends heavily on network images, platform fonts, or time-based animation.

Practical golden guidance:

- Stabilize rendering
  - Fix surface size (e.g., 375x812) and text scale factor.
  - Use deterministic fonts and ensure the same font assets are available in CI.
  - Disable animations or pump to a stable frame.

- Snapshot the smallest meaningful unit
  - Prefer golden tests for individual components or a single screen state, not the whole app.

- Review changes intentionally
  - Treat golden updates like code changes: review diffs and require design approval when needed.

## CI advice

Split tests by speed and value.

On every PR (fast feedback):

- `flutter analyze`
- Format/lint (if applicable)
- Unit tests
- Widget tests

Nightly or scheduled (slower, higher cost):

- Integration tests on real emulators/devices (or stable hosted runners)
- Golden tests if they are slow or require special setup
- Flaky test detection (rerun failed tests, collect timing)

Tips:

- Cache pub dependencies and (if used) build artifacts to reduce CI time.
- Run tests with a stable Flutter version (pin in CI).
- Keep integration tests isolated from each other (clean state between runs).

## Minimal checklist: adding tests for a new feature

1. Identify the feature's core behaviors and failure cases.
2. Add unit tests for pure logic and state transitions.
3. Add widget tests for critical UI interactions and rendering states.
4. Add one integration test only if the feature crosses layers (routing + persistence + plugins).
5. Decide whether a golden test is warranted (design-system or regression-prone UI).
6. Make dependencies injectable (clock, repositories, clients) to keep tests deterministic.
7. Ensure tests run locally with a single command and are stable (no sleeps, no real network).
