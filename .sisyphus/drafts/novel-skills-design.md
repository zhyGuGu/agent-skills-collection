# Novel Agent Skills - Design Specifications

## Skill 1: accessibility-audit
**Category**: Security & Compliance  
**Install Command**: `npx skills add yourusername/accessibility-audit`

### Problem Statement
Web accessibility (a11y) is legally required (ADA, WCAG) but developers lack AI-assisted tools to audit and fix accessibility issues. Existing tools are expensive or manual.

### Unique Value Proposition
- Automated WCAG 2.1 AA/AAA compliance checking
- AI-powered remediation suggestions with code examples
- Screen reader simulation and testing guidance
- Keyboard navigation testing
- Color contrast analysis

### Target Users
- Frontend developers
- QA engineers
- Product managers
- Compliance officers

### Implementation Approach

#### Files Structure
```
accessibility-audit/
├── SKILL.md                    # Main skill file
├── wcag-checklist.md           # WCAG 2.1 guidelines
├── aria-patterns.md            # Common ARIA patterns
├── remediation-examples/       # Before/after code examples
│   ├── forms.md
│   ├── navigation.md
│   ├── modals.md
│   ├── images.md
│   └── tables.md
├── testing-guides/
│   ├── keyboard-testing.md
│   ├── screen-reader-testing.md
│   └── automated-testing.md
└── examples/
    ├── react-example.md
    ├── vue-example.md
    └── vanilla-js-example.md
```

#### SKILL.md Template
```yaml
---
name: accessibility-audit
description: Comprehensive web accessibility auditing with WCAG compliance checking, automated remediation suggestions, and testing guidance for inclusive web experiences
---

# Accessibility Audit Skill

## When to Use
- Auditing websites for WCAG compliance
- Fixing accessibility violations
- Implementing inclusive design patterns
- Testing with assistive technologies

## Capabilities
1. WCAG 2.1 Level A/AA/AAA compliance checking
2. Automated accessibility scanning
3. Remediation code generation
4. Screen reader testing guidance
5. Keyboard navigation verification
6. Color contrast analysis
7. ARIA implementation patterns
8. Focus management strategies

## Audit Checklist

### Perceivable (WCAG Principle 1)
- [ ] Text alternatives for images
- [ ] Captions/transcripts for media
- [ ] Color not sole information carrier
- [ ] Text resizable to 200%
- [ ] Images of text avoided

### Operable (WCAG Principle 2)
- [ ] All functionality keyboard accessible
- [ ] No keyboard traps
- [ ] Skip links present
- [ ] Focus indicators visible
- [ ] Page titles descriptive

### Understandable (WCAG Principle 3)
- [ ] Language specified
- [ ] Input errors identified
- [ ] Error suggestions provided
- [ ] Consistent navigation
- [ ] Form labels associated

### Robust (WCAG Principle 4)
- [ ] Valid HTML markup
- [ ] ARIA used correctly
- [ ] Name/role/value available

## Common Patterns

### Modal Dialogs
```
Requirements:
- aria-modal="true"
- Focus trapped within modal
- Escape key closes
- Focus returns to trigger
- aria-labelledby for title
```

### Navigation Menus
```
Requirements:
- aria-expanded for toggles
- aria-current for active page
- Keyboard arrow navigation
- Skip to main content link
```

## Testing Procedures
[Detailed testing guides for keyboard, screen readers, etc.]
```

### Integration Points
- Works with browser dev tools
- Can analyze HTML/CSS/JS files
- Suggests specific code changes
- Provides severity ratings (Critical/High/Medium/Low)

---

## Skill 2: data-science-patterns
**Category**: Data Science & ML  
**Install Command**: `npx skills add yourusername/data-science-patterns`

### Problem Statement
Data scientists waste time on repetitive EDA, feature engineering, and model evaluation tasks. No AI-assisted skill exists for data science workflows.

### Unique Value Proposition
- Structured EDA (Exploratory Data Analysis) workflows
- Automated feature engineering suggestions
- Model selection guidance
- Statistical test recommendations
- Visualization best practices
- ML pipeline architecture patterns

### Target Users
- Data scientists
- ML engineers
- Data analysts
- Researchers

### Implementation Approach

#### Files Structure
```
data-science-patterns/
├── SKILL.md
├── eda-workflows/
│   ├── structured-eda.md
│   ├── missing-data-analysis.md
│   ├── outlier-detection.md
│   └── correlation-analysis.md
├── feature-engineering/
│   ├── numerical-features.md
│   ├── categorical-features.md
│   ├── text-features.md
│   └── datetime-features.md
├── model-selection/
│   ├── classification-guide.md
│   ├── regression-guide.md
│   ├── clustering-guide.md
│   └── time-series-guide.md
├── evaluation/
│   ├── metrics-selection.md
│   ├── cross-validation.md
│   ├── hyperparameter-tuning.md
│   └── model-interpretability.md
├── visualization/
│   ├── plot-selection-guide.md
│   ├── matplotlib-seaborn-patterns.md
│   └── plotly-dash-patterns.md
└── pipelines/
    ├── sklearn-pipelines.md
    ├── preprocessing-patterns.md
    └── model-deployment.md
```

#### Key Capabilities
1. **EDA Automation**: Systematic data profiling, distribution analysis, correlation matrices
2. **Feature Engineering**: Automated suggestions based on data types and distributions
3. **Model Matching**: Recommends algorithms based on problem type, data size, constraints
4. **Evaluation Framework**: Proper train/test splits, cross-validation, metric selection
5. **Visualization**: Chart type selection, color schemes, accessibility

---

## Skill 3: terraform-patterns
**Category**: DevOps & Infrastructure  
**Install Command**: `npx skills add yourusername/terraform-patterns`

### Problem Statement
Infrastructure as Code (IaC) adoption is growing but developers struggle with Terraform best practices, state management, and modular design.

### Unique Value Proposition
- Modular Terraform architecture patterns
- State management strategies
- Multi-environment deployment patterns
- Security best practices for IaC
- Cost optimization patterns
- CI/CD integration

### Target Users
- DevOps engineers
- Platform engineers
- SREs
- Cloud architects

### Implementation Approach

#### Files Structure
```
terraform-patterns/
├── SKILL.md
├── architecture/
│   ├── monolithic-vs-modular.md
│   ├── workspace-strategies.md
│   └── terragrunt-patterns.md
├── modules/
│   ├── module-design-principles.md
│   ├── reusable-module-patterns.md
│   └── module-testing.md
├── state/
│   ├── remote-state-setup.md
│   ├── state-locking.md
│   ├── state-migration.md
│   └── drift-detection.md
├── security/
│   ├── secrets-management.md
│   ├── iam-best-practices.md
│   └── compliance-as-code.md
├── multi-cloud/
│   ├── aws-patterns.md
│   ├── gcp-patterns.md
│   ├── azure-patterns.md
│   └── multi-cloud-strategies.md
└── workflows/
    ├── ci-cd-integration.md
    ├── plan-review-process.md
    └── disaster-recovery.md
```

#### Key Capabilities
1. **Module Design**: Proper input/output patterns, versioning, documentation
2. **State Management**: Remote backends, locking, workspace strategies
3. **Security**: Secret management, least privilege IAM, encryption
4. **Testing**: Terratest, plan validation, policy as code (OPA)
5. **Workflows**: GitOps, approval gates, automated drift detection

---

## Skill 4: flutter-best-practices
**Category**: Mobile Development  
**Install Command**: `npx skills add yourusername/flutter-best-practices`

### Problem Statement
Flutter is growing rapidly but developers lack comprehensive AI-assisted guidance for architecture, state management, and platform-specific considerations.

### Unique Value Proposition
- State management decision trees (Provider, Riverpod, Bloc, GetX)
- Clean architecture patterns for Flutter
- Platform-specific UI adaptation (iOS vs Android)
- Performance optimization
- Testing strategies (unit, widget, integration)
- Flutter Web/Desktop considerations

### Target Users
- Mobile developers
- Flutter developers
- Cross-platform developers
- Startups building mobile apps

### Implementation Approach

#### Files Structure
```
flutter-best-practices/
├── SKILL.md
├── architecture/
│   ├── clean-architecture.md
│   ├── layered-architecture.md
│   ├── feature-based-structure.md
│   └── monorepo-patterns.md
├── state-management/
│   ├── decision-matrix.md
│   ├── provider-patterns.md
│   ├── riverpod-patterns.md
│   ├── bloc-patterns.md
│   └── getx-patterns.md
├── ui-design/
│   ├── material-vs-cupertino.md
│   ├── responsive-design.md
│   ├── theming-guide.md
│   └── animation-patterns.md
├── performance/
│   ├── build-optimization.md
│   ├── memory-management.md
│   ├── list-optimization.md
│   └── image-optimization.md
├── testing/
│   ├── unit-testing.md
│   ├── widget-testing.md
│   ├── integration-testing.md
│   └── mocking-guide.md
├── platform/
│   ├── platform-channels.md
│   ├── native-integration.md
│   ├── ios-specifics.md
│   └── android-specifics.md
└── deployment/
    ├── app-store-guide.md
    ├── play-store-guide.md
    └── ci-cd-setup.md
```

#### Key Capabilities
1. **Architecture**: MVVM, Clean Architecture, feature-based organization
2. **State Management**: Decision trees, implementation patterns, best practices
3. **UI/UX**: Adaptive design, platform conventions, accessibility
4. **Performance**: Build optimization, lazy loading, image caching
5. **Testing**: Comprehensive testing pyramid for Flutter

---

## Skill 5: audio-production
**Category**: Audio & Music  
**Install Command**: `npx skills add yourusername/audio-production`

### Problem Statement
Podcasters, musicians, and content creators need AI-assisted guidance for audio editing, production workflows, and quality optimization.

### Unique Value Proposition
- Audio editing workflow optimization
- Noise reduction and cleanup
- EQ and compression guidance
- Podcast production best practices
- Music production fundamentals
- Voice processing for content creators
- Audio format optimization

### Target Users
- Podcasters
- Content creators
- Musicians
- Voiceover artists
- Video creators

### Implementation Approach

#### Files Structure
```
audio-production/
├── SKILL.md
├── recording/
│   ├── microphone-techniques.md
│   ├── room-acoustics.md
│   └── recording-best-practices.md
├── editing/
│   ├── daw-workflows.md
│   ├── cutting-techniques.md
│   └── crossfades-transitions.md
├── processing/
│   ├── eq-fundamentals.md
│   ├── compression-guide.md
│   ├── noise-reduction.md
│   └── reverb-delay.md
├── podcast/
│   ├── podcast-workflow.md
│   ├── intro-outro-creation.md
│   ├── interview-editing.md
│   └── show-notes-guide.md
├── music/
│   ├── mixing-basics.md
│   ├── mastering-overview.md
│   ├── arrangement-tips.md
│   └── beat-making.md
├── voice/
│   ├── voice-optimization.md
│   ├── audiobook-production.md
│   └── voiceover-guide.md
├── formats/
│   ├── export-settings.md
│   ├── loudness-standards.md
│   └── platform-requirements.md
└── tools/
    ├── audacity-guide.md
    ├── garageband-guide.md
    ├── audition-guide.md
    ├── logic-pro-guide.md
    └── pro-tools-guide.md
```

#### Key Capabilities
1. **Recording Setup**: Microphone selection, room treatment, gain staging
2. **Editing Workflows**: Non-destructive editing, time-saving techniques
3. **Audio Processing**: EQ, compression, noise reduction fundamentals
4. **Podcast Production**: End-to-end podcast creation workflow
5. **Format Optimization**: Export settings for different platforms

---

## Implementation Priority Matrix

| Skill | Scarcity | Demand | Complexity | Impact |
|-------|----------|--------|------------|--------|
| accessibility-audit | Very High | High | Medium | Very High |
| data-science-patterns | Very High | High | High | High |
| terraform-patterns | High | High | Medium | High |
| flutter-best-practices | High | Medium | Medium | Medium |
| audio-production | High | Medium | Low | Medium |

## Recommended Development Order

1. **accessibility-audit** - Highest impact, clear compliance value
2. **terraform-patterns** - Strong DevOps demand, well-defined patterns
3. **data-science-patterns** - Growing field, substantial content
4. **flutter-best-practices** - Mobile growth area
5. **audio-production** - Content creator market
