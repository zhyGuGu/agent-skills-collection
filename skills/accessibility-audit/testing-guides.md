# Testing Guides

Use this checklist to run quick, repeatable accessibility testing during QA and before release. Manual testing finds issues automation misses; automation prevents regressions.

## Keyboard-Only Testing

Goal: Confirm every interactive task can be completed with keyboard only, with a visible focus indicator and no traps.

Pre-checks:
- Use a fresh browser profile; disable extensions that change focus behavior.
- Do not use a mouse/trackpad during the test.

Steps (with pass/fail criteria):
1. Tab into the page from the browser chrome.
   - Pass: Focus starts at a sensible first target (or a skip link) and is clearly visible.
   - Fail: Focus is lost, invisible, or starts in an unexpected place (e.g., hidden control).
2. Move forward through all interactive elements with Tab.
   - Pass: Focus order matches visual/reading order; nothing essential is skipped.
   - Fail: Focus jumps around, lands on non-interactive elements, or misses key controls.
3. Move backward with Shift+Tab.
   - Pass: Reverse order is logical; you can return to previous controls.
   - Fail: Focus gets stuck or order reverses incorrectly.
4. Activate controls with Enter and Space.
   - Pass: Buttons, links, toggles, and custom controls activate as expected.
   - Fail: Control requires mouse or only one key works inconsistently.
5. Operate menus, tabs, and listboxes with Arrow keys (where applicable).
   - Pass: Arrow keys navigate options; selection is announced/indicated.
   - Fail: Arrow keys do nothing or move page focus unexpectedly.
6. Test focus visibility and contrast.
   - Pass: Focus ring is always visible on every control; not clipped by overflow.
   - Fail: Focus is hidden by sticky headers, modals, or container clipping.
7. Open and close dialogs/popovers.
   - Pass: Focus moves into the dialog; Esc closes if expected; focus returns to opener.
   - Fail: Focus remains behind dialog, escapes to page, or does not restore.
8. Check for keyboard traps.
   - Pass: You can always Tab out (or close) and continue.
   - Fail: Focus is trapped without a keyboard exit.
9. Complete a representative form flow.
   - Pass: You can reach every field, submit, and fix validation errors via keyboard.
   - Fail: Error summaries/fields are unreachable or require mouse to dismiss.

## Screen Reader Smoke Tests

Goal: Confirm basic structure, names, roles, values, and dynamic updates are usable with a screen reader.

Recommended setups (pick at least one):
- NVDA + Firefox (Windows)
- JAWS + Chrome (Windows)
- VoiceOver + Safari (macOS)

Smoke test steps (with pass/fail criteria):
1. Page title and top-level structure
   - Pass: Document has a meaningful title; headings outline the page (single H1 is typical).
   - Fail: Title is generic/empty; headings are missing or used only for styling.
2. Landmarks and navigation
   - Pass: Major regions are identifiable (header/nav/main/footer); main content is reachable.
   - Fail: Everything is one unnamed region; navigation is hard to locate.
3. Links and buttons
   - Pass: Each control has a unique, descriptive accessible name (no "click here").
   - Fail: Repeated ambiguous names; icons read as "button" with no label.
4. Forms and errors
   - Pass: Inputs have labels; required/invalid state is conveyed; errors are announced and associated.
   - Fail: Placeholder-only labeling; errors are visual-only; focus does not move to errors.
5. Images and non-text content
   - Pass: Informative images have useful alt; decorative images are ignored.
   - Fail: Missing alt for meaningful images; filenames/garbage announced.
6. Dialogs and dynamic content
   - Pass: Opening a dialog is announced; focus moves into it; updates (toasts, inline errors) are announced.
   - Fail: Silent UI changes; focus stays behind overlays; content updates are not discoverable.

Notes:
- Keep the scope small: cover at least one end-to-end user journey (e.g., search -> view -> action).
- When you find a failure, capture exact rotor/element output and the key sequence used.

## Automated Checks

Automation is a safety net, not a guarantee. Run these checks on every significant UI change.

1. Lighthouse Accessibility (Chrome DevTools)
   - How: Open DevTools -> Lighthouse -> run "Accessibility".
   - Pass: Score meets your project threshold and no critical issues are reported.
   - Fail: Regressed score or new high-impact findings (names, contrast, labels, ARIA).

2. axe DevTools / axe-core
   - How (manual): Use the axe DevTools browser extension to scan key pages.
   - How (CI): Integrate axe-core into unit/e2e tests for critical flows.
   - Pass: No serious/critical violations; known false-positives are documented.
   - Fail: New violations without an approved exception and tracking ticket.

3. Playwright accessibility snapshot (concept)
   - Idea: In Playwright, capture an accessibility tree snapshot for key components/pages and compare against a reviewed baseline.
   - Pass: Snapshot changes are expected (reviewed) and improve or preserve semantics.
   - Fail: Snapshot shows lost names/roles, missing headings/landmarks, or unintended changes.

4. Skill structure validation
   - How: Run `agentskills validate` from the repo root.
   - Pass: Skill and docs structure validates cleanly.
   - Fail: Missing required files/sections, broken references, or invalid metadata.

## Reporting Template

Use this template for each issue found. Keep it copy/paste friendly.

```md
### Issue Title

**Area:** (page/route/component)
**Type:** (Keyboard / Screen reader / Automated)
**Severity:** (Blocker / High / Medium / Low)
**Environment:** (OS, browser, assistive tech + version)

**Steps to Reproduce:**
1.
2.
3.

**Expected Result:**
-

**Actual Result:**
-

**Pass/Fail Criteria Used:**
- (quote the relevant line from this guide)

**Evidence:**
- Screenshot/video link or console output
- Accessibility tree / SR announcement text (if applicable)

**Suspected Cause:**
- (optional)

**WCAG Reference (if known):**
- (e.g., 2.1.1 Keyboard, 1.3.1 Info and Relationships, 4.1.2 Name/Role/Value)

**Notes / Workarounds:**
-
```
