# Platform adaptations

This guide describes how to adapt a Flutter app to platform conventions across iOS, Android, web, and desktop.

## iOS vs Android UI conventions

### Navigation and structure
- Prefer platform-native navigation patterns.
  - iOS: bottom tab bars for top-level sections; hierarchical push navigation; back gesture is common.
  - Android: bottom navigation or navigation rail; top app bar with up button; system back button expectations.
- Keep navigation placement and behavior consistent per platform.
- Mirror platform page transitions where possible; avoid surprising motion.

### Visual density and spacing
- iOS generally favors more whitespace and slightly larger touch targets.
- Android often tolerates denser layouts, but keep touch targets accessible.
- Use consistent typographic hierarchy; avoid mixing Material and Cupertino styling on the same surface unless clearly separated.

### Controls and feedback
- Use platform-appropriate controls where it matters.
  - iOS: segmented controls, switches, date pickers with Cupertino look.
  - Android: Material buttons, menus, and dialogs.
- Use haptics and sound sparingly; do not rely on them for critical feedback.
- Confirm destructive actions in a platform-appropriate way.

### System integrations
- Respect platform permissions flows and phrasing.
- Match share sheets and external intent behaviors.
- Handle safe areas and notches (iOS) and system insets (Android) correctly.

## Web considerations

### Routing and URLs
- Use URL-based navigation that supports deep links and browser controls.
- Ensure Back/Forward buttons work as users expect.
- Prefer meaningful, stable routes; avoid hash-based routing unless required.

### SEO limits and discoverability
- Assume limited SEO for purely client-rendered Flutter web apps.
- If discoverability matters, provide indexable landing content outside the Flutter app or via pre-rendered pages.
- Ensure basic metadata (title, description, social previews) is set, but do not assume it fixes indexing.

### Performance and loading
- Minimize initial bundle size and widget work on first paint.
- Defer non-critical work until after first frame.
- Avoid excessive animations on first load; they can feel laggy in browsers.
- Test on low-end devices and throttled networks; web bottlenecks differ from mobile.

### Input and accessibility
- Support mouse hover, right-click expectations (if applicable), and text selection where appropriate.
- Ensure focus order and keyboard navigation work.
- Validate semantics for screen readers.

## Desktop considerations

### Keyboard shortcuts
- Provide common shortcuts for core actions (copy/paste, find, refresh, navigation).
- Surface shortcuts in menus or tooltips; keep them discoverable.
- Respect platform conventions.
  - macOS: Command-based shortcuts.
  - Windows/Linux: Control-based shortcuts.

### Windowing and resizing
- Design for resizable windows: handle narrow, wide, and short heights.
- Avoid fixed-size dialogs; allow content to reflow.
- Persist window state when appropriate (size, position) if your app owns that behavior.

### Mouse and precision input
- Increase information density where appropriate; desktop users expect more visible controls.
- Add hover states and larger hit regions for small icons.
- Support scroll wheels and trackpads; test scrolling physics and overscroll behavior.

### File system and drag-and-drop
- If your app handles files, support open/save flows consistent with the OS.
- Consider drag-and-drop for files or list items when it improves workflows.

## Checklist: adaptive UI

Use this checklist when validating adaptive behavior.

### Input devices
- Touch: comfortable hit targets, gesture alternatives for critical actions.
- Mouse: hover affordances, cursor changes, precise selection.
- Keyboard: full navigation and activation without a mouse; visible focus.
- Gamepad/remote (if relevant): directional navigation, clear focus.

### Screen sizes and form factors
- Small phones: single-column layouts, concise app bars, minimal clutter.
- Large phones/tablets: consider split views, navigation rail, master-detail.
- Desktop: resizable layouts, multi-column content, persistent navigation.
- Orientation changes: preserve user context and scroll position.

### Layout and typography
- Use responsive breakpoints; do not scale everything uniformly.
- Keep line lengths readable; constrain text width on very wide screens.
- Avoid clipped text: test longer strings and dynamic type where applicable.

### Navigation and platform behavior
- Back behavior matches platform expectations (gesture, system back, browser back).
- Deep links open the correct screen and state.
- Dialogs, sheets, and popovers are appropriate for the platform.

### Accessibility
- Semantics are present for interactive elements.
- Contrast and focus indicators are visible.
- Text scaling does not break critical flows.

### Performance and quality
- Startup feels fast (especially web); avoid heavy synchronous work on first frame.
- Animations are smooth and purposeful; avoid excessive motion.
- Feature parity is explicit: document platform-specific limitations.
