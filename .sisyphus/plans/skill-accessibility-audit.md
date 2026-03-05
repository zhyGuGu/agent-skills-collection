# Skill Implementation Plan: accessibility-audit

## Overview
A comprehensive web accessibility auditing skill for AI agents, focusing on WCAG 2.1 compliance, automated remediation, and testing guidance.

## Problem Statement
- 96% of websites have accessibility violations (WebAIM Million 2024)
- Legal requirements (ADA, Section 508, EAA) mandate compliance
- Developers lack AI-assisted accessibility tooling
- Manual audits are time-consuming and error-prone
- Existing tools (axe, Lighthouse) provide limited remediation guidance

## Target Market
- **Primary**: Frontend developers, QA engineers
- **Secondary**: Product managers, compliance officers
- **Tertiary**: Designers, content creators

## Success Metrics
- Accurate WCAG 2.1 Level AA violation detection
- Actionable remediation code for 80%+ of issues
- Support for React, Vue, Angular, vanilla HTML/CSS
- Screen reader testing guidance
- Keyboard navigation verification

---

## Implementation Checklist

### Phase 1: Core Skill Structure (Week 1)

#### 1.1 Create SKILL.md
```yaml
---
name: accessibility-audit
description: Comprehensive web accessibility auditing with WCAG 2.1 AA/AAA compliance checking, automated remediation suggestions, and testing guidance for inclusive web experiences
version: 1.0.0
author: yourusername
tags: [accessibility, wcag, a11y, compliance, audit]
---
```

**Required Sections**:
- `# When to Use` - Trigger conditions
- `# Capabilities` - What the skill can do
- `# Audit Checklist` - WCAG principles breakdown
- `# Common Patterns` - ARIA patterns, focus management
- `# Testing Procedures` - Step-by-step testing
- `# Remediation Examples` - Before/after code

#### 1.2 WCAG Guidelines Reference
Create `wcag-reference.md` with:
- All 78 WCAG 2.1 success criteria
- Severity ratings (Critical/High/Medium/Low)
- Test procedures for each criterion
- Code examples (pass/fail)

#### 1.3 ARIA Pattern Library
Create `aria-patterns.md` covering:
- Modal dialogs
- Navigation menus
- Accordions
- Tabs
- Form validation
- Live regions
- Data tables
- Carousels

### Phase 2: Remediation Code Library (Week 2)

#### 2.1 Create remediation-examples/
Each file contains:
- Problem description
- WCAG criterion reference
- Before code (non-compliant)
- After code (compliant)
- Explanation of changes

**Files needed**:
- `forms.md` - Labels, error messages, required fields
- `navigation.md` - Skip links, breadcrumbs, menus
- `modals.md` - Focus trapping, escape handling
- `images.md` - Alt text, decorative images, complex graphics
- `tables.md` - Headers, captions, scope attributes
- `buttons-links.md` - Proper use, focus states
- `color-contrast.md` - Ratio calculations, color independence

#### 2.2 Framework-Specific Examples
Create examples for:
- React (using JSX, hooks)
- Vue (templates, composables)
- Angular (components, directives)
- Svelte
- Vanilla HTML/CSS/JS

### Phase 3: Testing Guides (Week 3)

#### 3.1 Keyboard Testing Guide
`testing-guides/keyboard-testing.md`:
- Tab order verification
- Focus indicator visibility
- Keyboard trap detection
- Shortcut key testing
- Form navigation

#### 3.2 Screen Reader Testing Guide
`testing-guides/screen-reader-testing.md`:
- NVDA (Windows) setup and usage
- JAWS (Windows) basics
- VoiceOver (macOS) navigation
- TalkBack (Android) testing
- Common screen reader shortcuts

#### 3.3 Automated Testing Guide
`testing-guides/automated-testing.md`:
- axe-core integration
- Lighthouse accessibility
- Playwright accessibility testing
- Jest-axe for unit tests
- CI/CD integration

### Phase 4: Integration & Validation (Week 4)

#### 4.1 Integration Points
Document how the skill integrates with:
- Browser DevTools
- VSCode extensions
- CI/CD pipelines
- Testing frameworks

#### 4.2 Validation Checklist
- [ ] All 78 WCAG 2.1 criteria documented
- [ ] Minimum 50 remediation examples
- [ ] 5+ framework examples
- [ ] Complete testing guides
- [ ] Peer review completed
- [ ] Tested with Claude Code
- [ ] Tested with OpenCode

---

## File Structure

```
accessibility-audit/
├── README.md
├── SKILL.md                          # Main skill entry point
├── wcag-reference.md                 # Complete WCAG 2.1 reference
├── aria-patterns.md                  # Common ARIA implementations
│
├── remediation-examples/
│   ├── forms.md
│   ├── navigation.md
│   ├── modals.md
│   ├── images.md
│   ├── tables.md
│   ├── buttons-links.md
│   └── color-contrast.md
│
├── framework-examples/
│   ├── react/
│   │   ├── accessible-modal.jsx
│   │   ├── form-validation.jsx
│   │   └── navigation-menu.jsx
│   ├── vue/
│   │   ├── AccessibleModal.vue
│   │   ├── FormValidation.vue
│   │   └── NavigationMenu.vue
│   ├── angular/
│   │   ├── accessible-modal.component.ts
│   │   ├── form-validation.component.ts
│   │   └── navigation-menu.component.ts
│   └── vanilla/
│       ├── accessible-modal.html
│       ├── form-validation.html
│       └── navigation-menu.html
│
├── testing-guides/
│   ├── keyboard-testing.md
│   ├── screen-reader-testing.md
│   └── automated-testing.md
│
├── checklists/
│   ├── pre-launch-a11y-checklist.md
│   ├── component-review-checklist.md
│   └── audit-report-template.md
│
└── resources/
    ├── wcag-quickref.md
    ├── aria-cheat-sheet.md
    └── tools-comparison.md
```

---

## Content Requirements

### SKILL.md Content Outline

```markdown
# Accessibility Audit

## When to Use
- User mentions accessibility, a11y, WCAG
- Code review of UI components
- Pre-launch website auditing
- Compliance requirement checking
- User reports screen reader issues

## Capabilities
1. WCAG 2.1 AA/AAA compliance assessment
2. Automated issue detection
3. Remediation code generation
4. Screen reader testing guidance
5. Keyboard navigation verification
6. Color contrast analysis
7. ARIA implementation review
8. Focus management strategies

## Quick Start
1. Share your HTML/CSS/JS code
2. I'll audit for accessibility violations
3. Receive prioritized remediation list
4. Get before/after code examples

## Audit Framework

### Perceivable
[Detailed guidelines for text alternatives, time-based media, adaptable content, distinguishable content]

### Operable
[Keyboard accessibility, enough time, seizures, navigable]

### Understandable
[Readable, predictable, input assistance]

### Robust
[Compatible with assistive technologies]

## Common Issues & Fixes
[Top 20 issues with quick fixes]

## Testing Checklist
[Copy-paste checklist for manual testing]

## Resources
[Links to official WCAG, tools, further reading]
```

---

## Quality Standards

### Accuracy Requirements
- 100% alignment with WCAG 2.1 specifications
- All code examples must be tested and working
- Screen reader commands must be current (2024)
- Browser support must reflect current market share

### Completeness Requirements
- Cover all 4 WCAG principles
- Address all 3 conformance levels (A, AA, AAA)
- Include mobile accessibility considerations
- Address both web and web app scenarios

### Usability Requirements
- Clear, jargon-free explanations
- Actionable remediation steps
- Copy-paste ready code examples
- Visual diagrams where helpful

---

## Testing Strategy

### Unit Testing
Test individual patterns:
- Modal focus trapping
- Form label association
- ARIA attribute correctness

### Integration Testing
Test complete workflows:
- Full page audit
- Component accessibility
- Screen reader navigation flow

### User Testing
Validate with:
- Actual screen reader users
- Keyboard-only users
- Developers implementing fixes
- QA engineers doing audits

---

## Maintenance Plan

### Quarterly Updates
- Update for new browser versions
- Refresh screen reader compatibility
- Add new framework examples
- Review and update WCAG interpretations

### Community Contributions
- Accept PRs for new patterns
- Add examples in more frameworks
- Expand testing guides
- Translate to other languages

---

## Marketing Positioning

### Key Messages
1. "Make your website accessible to everyone"
2. "WCAG compliance made actionable"
3. "AI-powered accessibility auditing"
4. "From detection to remediation"

### Differentiators
- Only comprehensive AI-assisted accessibility skill
- Framework-specific code examples
- Screen reader testing guidance
- Continuously updated with latest standards

### Target Keywords
accessibility, a11y, WCAG, ADA compliance, screen reader, keyboard navigation, inclusive design, web accessibility audit

---

## GitHub Repository Setup

### Repository Structure
```
yourusername/accessibility-audit/
├── .github/
│   └── workflows/
│       └── validate.yml       # Validate skill structure
├── skills/
│   └── accessibility-audit/   # All skill files
├── tests/
│   └── validation.test.js     # Automated tests
├── CONTRIBUTING.md
├── LICENSE (Apache 2.0)
└── README.md
```

### README.md Sections
1. Overview & Value Proposition
2. Installation (`npx skills add yourusername/accessibility-audit`)
3. Usage Examples
4. Features
5. Supported Standards
6. Framework Support
7. Contributing
8. License

### GitHub Topics
`accessibility`, `wcag`, `a11y`, `screen-reader`, `inclusive-design`, `agent-skill`, `claude-skill`, `opencode-skill`

---

## Implementation Timeline

| Week | Deliverable | Owner |
|------|-------------|-------|
| 1 | SKILL.md + WCAG reference | Developer |
| 1 | ARIA patterns library | Developer |
| 2 | Remediation examples (HTML) | Developer |
| 2 | Remediation examples (CSS) | Developer |
| 3 | Framework examples (React) | Developer |
| 3 | Framework examples (Vue) | Developer |
| 3 | Testing guides | Developer |
| 4 | Integration docs | Developer |
| 4 | QA & validation | QA Engineer |
| 4 | GitHub repo setup | Developer |

---

## Success Criteria Checklist

- [ ] Repository created and public
- [ ] SKILL.md complete with all sections
- [ ] Minimum 50 code examples
- [ ] All 78 WCAG criteria documented
- [ ] Testing guides complete
- [ ] Validated with Claude Code
- [ ] Validated with OpenCode
- [ ] README with installation instructions
- [ ] Published to skills.sh
- [ ] 100+ installs in first month
