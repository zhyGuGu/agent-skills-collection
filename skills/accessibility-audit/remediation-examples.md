# Remediation Examples (Before/After)

## 1) Alt text
Problem: Informative images lack meaningful alternative text, so screen reader users miss the content.

```html
<!-- Before: missing/incorrect alt -->
<img src="team.jpg">
<img src="chart.png" alt="image">
```

```html
<!-- After: descriptive alt, or empty alt for decorative images -->
<img src="team.jpg" alt="Our support team in the office">
<img src="divider.png" alt="" role="presentation">
```

Verify:
- With a screen reader, confirm the first image is announced meaningfully.
- Confirm decorative images are skipped (no redundant announcements).

## 2) Form labels
Problem: Inputs rely on placeholder text or nearby text that is not programmatically associated.

```html
<!-- Before: no label association -->
<input type="email" placeholder="Email">
<div>Password</div>
<input type="password">
```

```html
<!-- After: explicit labels or aria-label when appropriate -->
<label for="email">Email</label>
<input id="email" type="email" autocomplete="email">

<label for="password">Password</label>
<input id="password" type="password" autocomplete="current-password">
```

Verify:
- Click each label and confirm focus moves to the matching input.
- With a screen reader, confirm each input announces its label.

## 3) Focus visible
Problem: Focus indicators are removed or too subtle, so keyboard users cannot see where they are.

```css
/* Before: removes focus ring */
button:focus { outline: none; }
```

```css
/* After: ensure a strong visible focus style */
:focus-visible {
  outline: 3px solid #0b5fff;
  outline-offset: 2px;
}
```

Verify:
- Use Tab/Shift+Tab and confirm the focused control is clearly visible.
- Confirm mouse clicks do not show the focus ring (when supported) while keyboard does.

## 4) Keyboard trap
Problem: Focus enters a widget but cannot leave it using the keyboard.

```html
<!-- Before: a custom dropdown that traps Tab -->
<div id="menu" tabindex="0" aria-label="Actions menu">Actions</div>
<script>
  const menu = document.getElementById('menu');
  menu.addEventListener('keydown', (e) => {
    if (e.key === 'Tab') e.preventDefault();
  });
</script>
```

```html
<!-- After: do not block Tab; provide Escape to close when applicable -->
<div id="menu" tabindex="0" aria-label="Actions menu" aria-expanded="false">Actions</div>
<script>
  const menu = document.getElementById('menu');
  menu.addEventListener('keydown', (e) => {
    if (e.key === 'Escape') {
      menu.setAttribute('aria-expanded', 'false');
      menu.blur();
    }
  });
</script>
```

Verify:
- Tab into the widget, then Tab again and confirm focus moves to the next control.
- Press Escape and confirm the widget closes/defocuses if it has an open state.

## 5) Color contrast
Problem: Text/background contrast is too low, making content hard to read.

```css
/* Before: low contrast (light gray on white) */
.hint { color: #bdbdbd; background: #ffffff; }
```

```css
/* After: increase contrast (example values; confirm with a contrast checker) */
.hint { color: #4a4a4a; background: #ffffff; }
```

Verify:
- Check contrast ratio for normal text meets WCAG AA (>= 4.5:1).
- Verify hover/disabled states still meet contrast requirements for their use.

## 6) Modal focus management
Problem: When a modal opens, focus is not moved into it and can move behind it; focus is not restored on close.

```html
<!-- Before: modal opens visually but focus stays on the page -->
<button id="open">Open dialog</button>
<div id="dialog" hidden>
  <h2>Dialog</h2>
  <button id="close">Close</button>
</div>
<script>
  open.onclick = () => dialog.hidden = false;
  close.onclick = () => dialog.hidden = true;
</script>
```

```html
<!-- After: move focus into modal, trap focus, restore on close -->
<button id="open">Open dialog</button>
<div id="dialog" role="dialog" aria-modal="true" aria-labelledby="dlg-title" hidden>
  <h2 id="dlg-title">Dialog</h2>
  <button id="close">Close</button>
</div>
<script>
  const openBtn = document.getElementById('open');
  const dialog = document.getElementById('dialog');
  const closeBtn = document.getElementById('close');
  let lastActive = null;

  function getFocusable(root) {
    return Array.from(root.querySelectorAll('a,button,input,select,textarea,[tabindex]:not([tabindex="-1"])'))
      .filter(el => !el.hasAttribute('disabled') && !el.getAttribute('aria-hidden'));
  }

  function onTrap(e) {
    if (e.key !== 'Tab') return;
    const focusables = getFocusable(dialog);
    const first = focusables[0];
    const last = focusables[focusables.length - 1];
    if (e.shiftKey && document.activeElement === first) { e.preventDefault(); last.focus(); }
    else if (!e.shiftKey && document.activeElement === last) { e.preventDefault(); first.focus(); }
  }

  openBtn.addEventListener('click', () => {
    lastActive = document.activeElement;
    dialog.hidden = false;
    closeBtn.focus();
    document.addEventListener('keydown', onTrap);
  });

  closeBtn.addEventListener('click', () => {
    dialog.hidden = true;
    document.removeEventListener('keydown', onTrap);
    if (lastActive) lastActive.focus();
  });
</script>
```

Verify:
- Open the modal and confirm focus moves to the first interactive element inside.
- Press Tab/Shift+Tab and confirm focus cycles within the modal.
- Close the modal and confirm focus returns to the opener.
