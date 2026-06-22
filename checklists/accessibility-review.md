# Accessibility Review Checklist

A11y audit cho mọi page và component.

---

## ✅ Level 1: Critical (Must fix before ship)

### Keyboard Navigation
- [ ] TAB navigates all interactive elements
- [ ] TAB order is logical (top-left to bottom-right)
- [ ] Focus indicator visible on all elements
- [ ] No focus trap outside of dialogs
- [ ] ESC closes dialogs/dropdowns

### Screen Reader
- [ ] All images have alt text
- [ ] Decorative images: `alt=""` or `role="presentation"`
- [ ] Icon-only buttons: `aria-label` set
- [ ] Form inputs have associated `<label>` (via `for`/`id`)
- [ ] Error messages linked with `aria-describedby`

### Color & Contrast
- [ ] Body text contrast ≥ 4.5:1
- [ ] Large text (18px+ or 14px+ bold) contrast ≥ 3:1
- [ ] UI components (inputs, buttons) ≥ 3:1
- [ ] Color not the ONLY indicator (also use icon/text)

---

## ✅ Level 2: Important (Fix before v1.0)

### Semantic HTML
- [ ] `<header>`, `<nav>`, `<main>`, `<footer>` used
- [ ] `<h1>` exists and is unique per page
- [ ] Heading levels sequential (no h1 → h3 skip)
- [ ] Lists use `<ul>`/`<ol>` not div-with-bullets
- [ ] `<button>` for actions, `<a>` for navigation
- [ ] Tables have `<th>` headers with `scope` attribute

### ARIA
- [ ] `aria-expanded` on accordions/dropdowns
- [ ] `aria-selected` on tabs
- [ ] `aria-current="page"` on active nav item
- [ ] `aria-live="polite"` on dynamic content
- [ ] `role="dialog"` + `aria-modal="true"` on modals
- [ ] `aria-hidden="true"` on decorative elements

### Forms
- [ ] Error state = `aria-invalid="true"`
- [ ] Required = `required` + `aria-required="true"`
- [ ] Error message = `role="alert"` or `aria-live`
- [ ] Related fields in `<fieldset>` + `<legend>`
- [ ] `autocomplete` set on common fields

---

## ✅ Level 3: Enhanced (Nice to have)

### Reduced Motion
- [ ] Animations respect `prefers-reduced-motion`
- [ ] `useReducedMotion()` from Motion library used
- [ ] No auto-playing videos (or with mute + controls)

### Skip Links
- [ ] Skip to main content link at top
- [ ] Skip to navigation if complex page

### Focus Management
- [ ] On modal open: focus moves to modal
- [ ] On modal close: focus returns to trigger
- [ ] On route change: focus moves to new content

### High Contrast
- [ ] Works in Windows High Contrast mode
- [ ] Doesn't use CSS background images for content

---

## Testing Tools
```
Chrome DevTools Accessibility Panel
→ Lighthouse audit (Accessibility score)
→ axe DevTools extension (browser)
→ VoiceOver (Mac: Cmd+F5) or NVDA (Windows: free)
→ Keyboard-only navigation test
→ WAVE (wave.webaim.org) — online checker
→ Colour Contrast Analyser (app)
```

---

## Contrast Quick Reference (on white #ffffff)
```
✅ PASS 4.5:1: gray-600 (#4b5563), gray-700, gray-800, gray-900, gray-950
⚠️ BARELY: gray-500 (#6b7280) = 4.6:1 PASS
❌ FAIL: gray-400 (#9ca3af) = 2.5:1 FAIL
❌ FAIL: gray-300 (#d1d5db) = 1.6:1 FAIL

✅ blue-600 on white = 4.9:1 PASS
❌ blue-400 on white = 2.9:1 FAIL
✅ white on blue-600 = 4.9:1 PASS
❌ white on blue-400 = 2.9:1 FAIL
```
