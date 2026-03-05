# Framework Examples (No External Libraries)
Framework-specific remediation examples (plain patterns, no external libs).
### Shared: minimal focus trap helper (vanilla JS)
```js
const FOCUSABLE =
  'a[href],button:not([disabled]),input:not([disabled]),select:not([disabled]),textarea:not([disabled]),[tabindex]:not([tabindex="-1"])';
export function trapDialogFocus({ dialogEl, onClose }) {
  const items = () => (dialogEl ? Array.from(dialogEl.querySelectorAll(FOCUSABLE)) : []);
  (items()[0] || dialogEl)?.focus?.();
  const onKeyDown = (e) => {
    if (e.key === "Escape") return (e.preventDefault(), onClose());
    if (e.key !== "Tab") return;
    const els = items();
    if (!els.length) return e.preventDefault();
    const first = els[0], last = els[els.length - 1];
    if (!e.shiftKey && document.activeElement === last) return (e.preventDefault(), first.focus());
    if (e.shiftKey && document.activeElement === first) return (e.preventDefault(), last.focus());
  };
  document.addEventListener("keydown", onKeyDown);
  return () => document.removeEventListener("keydown", onKeyDown);
}
```

## React

### Accessible modal/dialog (focus management + attributes)
Uses `trapDialogFocus` to move focus in, trap Tab/Shift+Tab, close on Escape, and restore focus to the opener on cleanup.

```jsx
import { useEffect, useId, useRef, useState } from "react";
// trapDialogFocus helper defined above
export function ExampleDialog() {
  const [open, setOpen] = useState(false);
  const openerRef = useRef(null);
  const dialogRef = useRef(null);
  const titleId = useId();
  const descId = useId();
  useEffect(() => {
    if (!open) return;
    const cleanup = trapDialogFocus({ dialogEl: dialogRef.current, onClose: () => setOpen(false) });
    return () => (cleanup(), openerRef.current?.focus?.());
  }, [open]);
  return (
    <div>
      <button ref={openerRef} onClick={() => setOpen(true)} aria-haspopup="dialog" aria-expanded={open}>Open dialog</button>
      {open && (
        <div role="presentation" onMouseDown={(e) => e.target === e.currentTarget && setOpen(false)}>
          <div ref={dialogRef} role="dialog" aria-modal="true" aria-labelledby={titleId} aria-describedby={descId} tabIndex={-1}>
            <h2 id={titleId}>Confirm action</h2>
            <p id={descId}>This action cannot be undone.</p>
            <button onClick={() => setOpen(false)}>Cancel</button><button onClick={() => setOpen(false)}>Confirm</button>
          </div>
        </div>
      )}
    </div>
  );
}
```

### Form field with label + error association

```jsx
import { useId, useState } from "react";

export function EmailField() {
  const id = useId();
  const errId = `${id}-error`;
  const [v, setV] = useState("");
  const [t, setT] = useState(false);
  const invalid = t && !/^[^@]+@[^@]+\.[^@]+$/.test(v);
  return (
    <div>
      <label htmlFor={id}>Email</label>
      <input id={id} name="email" type="email" value={v} onChange={(e) => setV(e.target.value)} onBlur={() => setT(true)} aria-invalid={invalid} aria-describedby={invalid ? errId : undefined} />
      {invalid && <div id={errId} role="alert">Enter a valid email address.</div>}
    </div>
  );
}
```

Verify:
- Keyboard: Tab/Shift+Tab stay in dialog; Escape closes; focus returns to opener.
- SR: dialog has name/desc; error text is read via `aria-describedby`.

## Vue

### Accessible modal/dialog (focus management + attributes)
Calls `trapDialogFocus` when `open` becomes true; cleanup restores focus to the opener.

```vue
<template>
  <button ref="opener" type="button" @click="open = true" aria-haspopup="dialog" :aria-expanded="String(open)">Open dialog</button>
  <div v-if="open" role="presentation" @mousedown.self="close"><div ref="dialog" role="dialog" aria-modal="true" aria-labelledby="dlgTitle" aria-describedby="dlgDesc" tabindex="-1">
    <h2 id="dlgTitle">Confirm action</h2><p id="dlgDesc">This action cannot be undone.</p>
    <button type="button" @click="close">Cancel</button><button type="button" @click="close">Confirm</button>
  </div></div>
</template>

<script setup>
import { nextTick, onBeforeUnmount, ref, watch } from "vue";
// trapDialogFocus helper defined above
const open = ref(false);
const dialog = ref(null);
const opener = ref(null);
let cleanup = null;
const close = () => (open.value = false);
watch(open, async (isOpen) => {
  if (isOpen) return (await nextTick(), (cleanup = trapDialogFocus({ dialogEl: dialog.value, onClose: close })));
  cleanup?.();
  cleanup = null;
  opener.value?.focus?.();
});
onBeforeUnmount(() => cleanup?.());
</script>
```

### Form field with label + error association

```vue
<template>
  <label for="email">Email</label>
  <input id="email" name="email" type="email" v-model="v" @blur="t = true" :aria-invalid="String(invalid)" :aria-describedby="invalid ? 'emailError' : null" />
  <div v-if="invalid" id="emailError" role="alert">Enter a valid email address.</div>
</template>

<script setup>
import { computed, ref } from "vue";
const v = ref("");
const t = ref(false);
const invalid = computed(() => t.value && !/^[^@]+@[^@]+\.[^@]+$/.test(v.value));
</script>
```

Verify:
- Keyboard: focus moves into dialog and returns to opener; Escape closes.
- SR: dialog announced; error associated via `aria-describedby`.

## Angular

### Accessible modal/dialog (focus management + attributes)
Opens the dialog, then calls `trapDialogFocus`; closing runs cleanup and returns focus to the opener.

```ts
import { Component, ElementRef, ViewChild } from "@angular/core";
// trapDialogFocus helper defined above
@Component({
  selector: "app-example-dialog",
  template: `
    <button #opener type="button" (click)="openDialog()" aria-haspopup="dialog" [attr.aria-expanded]="open">Open dialog</button>
    <div *ngIf="open" role="presentation" (mousedown)="onBackdrop($event)"><div #dialog role="dialog" aria-modal="true" aria-labelledby="dlgTitle" aria-describedby="dlgDesc" tabindex="-1">
      <h2 id="dlgTitle">Confirm action</h2><p id="dlgDesc">This action cannot be undone.</p>
      <button type="button" (click)="closeDialog()">Cancel</button><button type="button" (click)="closeDialog()">Confirm</button>
    </div></div>
  `,
})
export class ExampleDialogComponent {
  open = false;
  private cleanup: any = null;
  @ViewChild("dialog") dialogRef?: ElementRef<HTMLElement>;
  @ViewChild("opener") openerRef?: ElementRef<HTMLButtonElement>;
  openDialog() {
    this.open = true;
    setTimeout(() => (this.cleanup = trapDialogFocus({ dialogEl: this.dialogRef?.nativeElement, onClose: () => this.closeDialog() })));
  }
  closeDialog() {
    this.open = false;
    this.cleanup?.();
    this.cleanup = null;
    this.openerRef?.nativeElement?.focus?.();
  }
  onBackdrop(e: MouseEvent) {
    if (e.target === e.currentTarget) this.closeDialog();
  }
}
```

### Form field with label + error association

```html
<label for="email">Email</label>
<input id="email" name="email" type="email" [(ngModel)]="value" (blur)="touched = true"
  [attr.aria-invalid]="invalid" [attr.aria-describedby]="invalid ? 'emailError' : null" />
<div *ngIf="invalid" id="emailError" role="alert">Enter a valid email address.</div>
```

```ts
import { Component } from "@angular/core";
@Component({ selector: "app-email-field", templateUrl: "./email-field.component.html" })
export class EmailFieldComponent {
  value = "";
  touched = false;
  get invalid() {
    return this.touched && !/^[^@]+@[^@]+\.[^@]+$/.test(this.value);
  }
}
```

Verify:
- Keyboard: focus trap works; Escape closes; focus returns to opener.
- SR: dialog label/desc present; error is announced and linked.
