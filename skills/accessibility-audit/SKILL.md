---
name: accessibility-audit
description: Procedural accessibility audit checklist and report template that maps findings to WCAG 2.1 principles, assigns severity, and suggests concrete remediations.
---

# Accessibility Audit
Use this skill to run a structured accessibility review of a UI. Capture reproducible findings, assign severity, and provide fixes that can be implemented and verified.

## When to Use
- Before release, after major UI changes, or after design system updates
- When users report keyboard, screen reader, or readability issues
- When you need a consistent, auditable report format for tracking remediation work

## Capabilities
- Perform a page-by-page audit with keyboard and basic screen reader checks
- Identify issues across WCAG 2.1 principles (Perceivable, Operable, Understandable, Robust)
- Produce a prioritized findings list with clear reproduction steps and expected behavior
- Recommend fixes with verification steps (how to confirm the fix is complete)

## Severity Rubric
- Critical: Blocks task completion for a major user group (keyboard-only, screen reader)
- High: Makes key flows difficult or error-prone; no reasonable workaround
- Medium: Impacts comprehension or efficiency; workaround exists
- Low: Minor friction or polish; does not materially block usage

## WCAG 2.1 Checklist
### Perceivable
- Text alternatives exist for meaningful images; decorative images are ignored
- Color is not the only way to convey meaning; contrast meets expected thresholds
- Content reflows and remains readable at zoom and larger text sizes

### Operable
- All interactive elements are reachable and usable with keyboard only
- Focus order is logical and focus is always visible
- No keyboard traps; users can enter and exit components (menus, dialogs) reliably

### Understandable
- Labels, instructions, and errors are clear and programmatically associated
- Navigation and control behavior is consistent across pages and states
- Inputs provide helpful constraints (format hints) and validate with actionable messages

### Robust
- Semantics are correct (headings, landmarks, buttons, links) for assistive tech
- Name/role/value are exposed for custom components (ARIA only when needed)
- Dynamic updates announce appropriately without breaking screen reader flow

## Common Violations and Fixes
- Alt text missing or incorrect: Add meaningful `alt` for informative images; use empty `alt` for decorative images.
- Form fields missing labels: Add associated `<label>`/`for` (or equivalent) and ensure the accessible name is correct.
- Focus not visible: Ensure a high-contrast focus indicator is present for all focusable controls.
- Keyboard trap: Fix focus handling so `Tab`/`Shift+Tab` and `Esc` allow leaving components.
- Insufficient contrast: Adjust foreground/background colors to meet contrast expectations for text and controls.
- Modal focus management: Move focus into the modal on open, trap focus within, and restore focus to the trigger on close.

## Manual Testing Quick Checks
- Keyboard: Tab through the full page; verify no dead ends; verify visible focus on every stop
- Zoom: Test 200% zoom and increased text size; verify no clipped content and no horizontal scrolling for common layouts
- Errors: Trigger form errors; verify the error is announced/visible and tied to the field
- Headings: Check heading levels are meaningful and not skipped for styling purposes
- Controls: Verify buttons are buttons, links navigate, and clickable divs are avoided or fixed

## Example Audit Reports
```text
Audit: Checkout - Shipping (scope: /checkout/shipping)
1) Critical - Keyboard trap in address autocomplete - Repro: Tab into results, Shift+Tab out fails - Fix: correct focus handling; add Esc to close.
2) High - Error message not associated to field - Repro: submit empty form - Fix: connect error text via describedby/id.
3) Medium - Focus indicator too subtle on primary button - Repro: Tab to primary button - Fix: visible high-contrast outline distinct from hover.
```
```text
Audit: Marketing - Pricing (scope: /pricing)
1) High - Color-only status indicators in plan comparison - Repro: review included markers - Fix: add text labels and accessible icon names.
2) Medium - Heading structure not semantic - Repro: navigate by headings - Fix: use proper heading elements for hierarchy.
3) Low - Decorative hero image announced - Repro: read top of page - Fix: empty alt and remove redundant accessible name.
```
