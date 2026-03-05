# Skill Implementation Plan: flutter-best-practices

## Overview
Comprehensive Flutter development patterns covering architecture, state management, UI design, testing, and cross-platform deployment.

## Problem Statement
- Flutter is the fastest-growing cross-platform framework
- Developers struggle with:
  - State management choice paralysis (Provider, Riverpod, Bloc, GetX)
  - Clean architecture implementation
  - Platform-specific UI adaptation
  - Performance optimization
  - Testing strategies
- No comprehensive AI-assisted Flutter guidance exists

## Target Market
- **Primary**: Mobile developers, Flutter developers
- **Secondary**: Cross-platform developers, startups
- **Tertiary**: iOS/Android native developers transitioning to Flutter

## Success Metrics
- Clear state management decision matrix
- Clean architecture implementation guide
- Platform-adaptive UI patterns
- Performance optimization checklist
- Comprehensive testing coverage

---

## Implementation Checklist

### Phase 1: Architecture & Structure (Week 1)

#### 1.1 Create SKILL.md
```yaml
---
name: flutter-best-practices
description: Production-ready Flutter patterns for clean architecture, state management, adaptive UI, performance optimization, and comprehensive testing across mobile, web, and desktop
version: 1.0.0
author: yourusername
tags: [flutter, dart, mobile, cross-platform, ios, android, state-management]
---
```

**Required Sections**:
- `# When to Use` - Trigger conditions
- `# Architecture Patterns` - Clean architecture, layer structure
- `# State Management` - Decision matrix, implementations
- `# UI/UX` - Adaptive design, theming
- `# Performance` - Optimization strategies
- `# Testing` - Unit, widget, integration

#### 1.2 Architecture Patterns
Document:
- Clean Architecture (Domain, Data, Presentation)
- Feature-based folder structure
- Layered architecture
- Monorepo patterns (Melos)
- Dependency injection (GetIt, Injectable)

#### 1.3 Project Structure Templates
Create templates for:
- Small app structure (< 20 screens)
- Medium app structure (20-50 screens)
- Large app structure (50+ screens)
- Package-based modular structure

### Phase 2: State Management (Week 2)

#### 2.1 State Management Decision Matrix
Create `state-management/decision-matrix.md`:
- App size considerations
- Team size factors
- Complexity assessment
- Learning curve comparison
- Performance implications

#### 2.2 Provider Patterns
Create `state-management/provider/`:
- ChangeNotifier implementation
- Multi-provider setup
- Dependency injection
- Testing with Provider

#### 2.3 Riverpod Patterns
Create `state-management/riverpod/`:
- StateNotifier vs StateProvider
- AsyncValue handling
- Family providers
- AutoDispose patterns
- Code generation (riverpod_generator)

#### 2.4 Bloc/Cubit Patterns
Create `state-management/bloc/`:
- Bloc vs Cubit decision
- Event-driven architecture
- State transitions
- Testing with bloc_test

#### 2.5 GetX Patterns
Create `state-management/getx/`:
- State management
- Route management
- Dependency injection
- When to use (and when not to)

### Phase 3: UI/UX & Platform Adaptation (Week 3)

#### 3.1 Adaptive UI Patterns
Create `ui-design/adaptive-patterns.md`:
- Material vs Cupertino detection
- Platform-specific widgets
- Adaptive navigation
- Screen size responsiveness

#### 3.2 Theming Guide
Create `ui-design/theming/`:
- Material 3 theming
- Dark mode implementation
- Custom theme extensions
- Dynamic theming

#### 3.3 Animation Patterns
Create `ui-design/animations/`:
- Implicit animations
- Explicit animations
- Hero animations
- Custom painters
- Lottie integration

#### 3.4 Platform Channels
Create `platform/native-integration.md`:
- MethodChannel usage
- EventChannel for streams
- Platform views
- Federated plugins

### Phase 4: Performance & Testing (Week 4)

#### 4.1 Performance Optimization
Create `performance/`:
- Build optimization
- Memory management
- List optimization (ListView.builder)
- Image optimization (cached_network_image)
- Shader compilation (warm-up)
- Repaint boundaries

#### 4.2 Testing Strategy
Create `testing/`:
- Unit testing (business logic)
- Widget testing (UI components)
- Integration testing (end-to-end)
- Golden testing (visual regression)
- Mocking guide (mockito, mocktail)

#### 4.3 Deployment Guides
Create `deployment/`:
- App Store deployment
- Play Store deployment
- Web deployment
- Desktop deployment (Windows, macOS, Linux)
- CI/CD with Codemagic/GitHub Actions

---

## File Structure

```
flutter-best-practices/
├── README.md
├── SKILL.md
├── CHANGELOG.md
│
├── architecture/
│   ├── clean-architecture.md
│   ├── folder-structure.md
│   ├── dependency-injection.md
│   ├── navigation-patterns.md
│   └── monorepo-with-melos.md
│
├── state-management/
│   ├── decision-matrix.md
│   ├── provider/
│   │   ├── getting-started.md
│   │   ├── advanced-patterns.md
│   │   └── testing-guide.md
│   ├── riverpod/
│   │   ├── getting-started.md
│   │   ├── async-operations.md
│   │   ├── code-generation.md
│   │   └── testing-guide.md
│   ├── bloc/
│   │   ├── getting-started.md
│   │   ├── architecture-patterns.md
│   │   └── testing-guide.md
│   └── getx/
│       ├── getting-started.md
│       └── when-to-use.md
│
├── ui-design/
│   ├── adaptive-patterns.md
│   ├── material-vs-cupertino.md
│   ├── theming/
│   │   ├── material-3-guide.md
│   │   ├── dark-mode.md
│   │   └── custom-themes.md
│   ├── animations/
│   │   ├── implicit-animations.md
│   │   ├── explicit-animations.md
│   │   └── hero-animations.md
│   └── responsive-design.md
│
├── performance/
│   ├── build-optimization.md
│   ├── memory-management.md
│   ├── list-optimization.md
│   ├── image-optimization.md
│   └── startup-performance.md
│
├── testing/
│   ├── unit-testing.md
│   ├── widget-testing.md
│   ├── integration-testing.md
│   ├── golden-testing.md
│   └── mocking-guide.md
│
├── platform/
│   ├── platform-channels.md
│   ├── ios-specifics.md
│   ├── android-specifics.md
│   └── web-considerations.md
│
├── deployment/
│   ├── app-store-guide.md
│   ├── play-store-guide.md
│   ├── web-deployment.md
│   ├── desktop-deployment.md
│   └── ci-cd-setup.md
│
├── examples/
│   ├── counter-app/
│   │   ├── provider-version/
│   │   ├── riverpod-version/
│   │   └── bloc-version/
│   ├── todo-app/
│   ├── ecommerce-app/
│   └── chat-app/
│
└── resources/
    ├── dart-tips.md
    ├── package-recommendations.md
    └── flutter-version-migration.md
```

---

## Content Requirements

### SKILL.md Content Outline

```markdown
# Flutter Best Practices

## When to Use
- Starting a new Flutter project
- Refactoring existing Flutter code
- Choosing state management solution
- Implementing clean architecture
- Optimizing app performance
- Setting up testing strategy
- Deploying to multiple platforms

## Capabilities
1. Architecture pattern selection and implementation
2. State management decision-making and setup
3. Adaptive UI for iOS/Android/Web/Desktop
4. Performance optimization
5. Comprehensive testing strategies
6. Platform-specific integrations
7. Deployment to all Flutter platforms
8. CI/CD pipeline setup

## Quick Start
1. Choose your architecture pattern
2. Select state management solution
3. Set up project structure
4. Implement core features
5. Add tests
6. Optimize performance
7. Deploy

## State Management Decision Tree
[Interactive decision tree to help choose Provider/Riverpod/Bloc/GetX]

## Architecture Patterns
[Clean architecture, feature-based structure, dependency injection]

## UI/UX Guidelines
[Adaptive design, theming, animations, responsive layouts]

## Performance Optimization
[Build optimization, memory management, list optimization]

## Testing
[Unit, widget, integration, golden testing]

## Platform Considerations
[iOS/Android differences, web limitations, desktop features]

## Deployment
[App Store, Play Store, web, desktop distribution]
```

### State Management Decision Matrix

| Factor | Provider | Riverpod | Bloc | GetX |
|--------|----------|----------|------|------|
| Learning Curve | Low | Medium | Medium | Low |
| Boilerplate | Low | Low | Medium | Very Low |
| Testability | Good | Excellent | Excellent | Fair |
| Performance | Good | Excellent | Good | Good |
| Compile Safety | No | Yes | Yes | No |
| Best For | Small-Medium | All Sizes | Large Complex | Quick Prototypes |

### Code Example Requirements

Every pattern must include:
- Complete, runnable code examples
- Explanation of key concepts
- Testing examples
- Common pitfalls and solutions
- Performance considerations

---

## Testing Strategy

### Unit Testing
- Business logic testing
- Repository testing
- Use case testing
- Mocking external dependencies

### Widget Testing
- Individual widget testing
- Screen/page testing
- Interaction testing
- Golden file comparison

### Integration Testing
- End-to-end user flows
- Navigation testing
- State persistence testing
- Platform integration testing

### Performance Testing
- Startup time measurement
- Memory usage profiling
- Frame rate monitoring
- Bundle size analysis

---

## Performance Optimization

### Build Performance
- Const constructors
- const vs final usage
- Widget rebuild optimization
- Keys usage (ValueKey, GlobalKey)

### Runtime Performance
- ListView.builder for long lists
- RepaintBoundary usage
- Image caching
- Lazy loading

### Memory Management
- Image disposal
- Stream cancellation
- Controller disposal
- Memory leak detection

### Startup Performance
- Deferring initialization
- Splash screen optimization
- Shader warm-up
- Lazy loading strategies

---

## Platform-Specific Considerations

### iOS
- Human Interface Guidelines compliance
- Cupertino widgets
- Platform-specific plugins
- App Store requirements

### Android
- Material Design compliance
- Material widgets
- Platform channels
- Play Store requirements

### Web
- SEO considerations
- URL routing
- Performance optimization
- Browser compatibility

### Desktop
- Window management
- Keyboard shortcuts
- Menu bars
- Platform-specific UX

---

## GitHub Repository Setup

### Repository Structure
```
yourusername/flutter-best-practices/
├── .github/
│   ├── workflows/
│   │   ├── validate.yml
│   │   └── publish.yml
│   └── CODEOWNERS
├── skills/
│   └── flutter-best-practices/
├── examples/
│   ├── counter_app/
│   ├── todo_app/
│   └── ecommerce_app/
├── tests/
│   └── test-coverage-report.md
├── CONTRIBUTING.md
├── LICENSE (MIT or Apache 2.0)
└── README.md
```

### README.md Sections
1. Overview & Value Proposition
2. Installation (`npx skills add yourusername/flutter-best-practices`)
3. Quick Start with Examples
4. State Management Comparison
5. Architecture Patterns
6. Performance Tips
7. Testing Strategies
8. Contributing Guidelines

### GitHub Topics
`flutter`, `dart`, `mobile`, `cross-platform`, `ios`, `android`, `state-management`, `clean-architecture`, `agent-skill`

---

## Implementation Timeline

| Week | Deliverable | Owner |
|------|-------------|-------|
| 1 | SKILL.md + Architecture patterns | Flutter Developer |
| 1 | Project structure templates | Flutter Developer |
| 2 | Provider patterns + examples | Flutter Developer |
| 2 | Riverpod patterns + examples | Flutter Developer |
| 3 | Bloc patterns + examples | Flutter Developer |
| 3 | UI/UX guides | UI/UX Designer |
| 4 | Performance optimization | Flutter Developer |
| 4 | Testing guides | QA Engineer |
| 5 | Platform-specific guides | Flutter Developer |
| 5 | Deployment guides | DevOps Engineer |
| 6 | Example apps + validation | Flutter Developer |

---

## Success Criteria Checklist

- [ ] Repository created and public
- [ ] SKILL.md complete with all sections
- [ ] State management decision matrix
- [ ] Minimum 4 state management implementations
- [ ] Clean architecture guide
- [ ] Performance optimization checklist
- [ ] Testing guides (unit/widget/integration)
- [ ] Platform-specific considerations
- [ ] Working example apps
- [ ] Validated with Claude Code
- [ ] Validated with OpenCode
- [ ] Published to skills.sh
