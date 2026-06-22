# 09 — Accessibility (A11y)

> SOURCE: WCAG 2.1 guidelines, WAI-ARIA, Motion accessibility, inclusive design principles

---

## Core Principle
A11y không phải thêm vào sau — nó là một phần của good design. Accessible = usable by everyone.
"Accessibility is the right thing to do AND makes your product better."

---

## Rule 1: Keyboard Navigation
```html
<!-- Every interactive element must be keyboard accessible -->

<!-- Focus styles: NEVER remove outline without replacement -->
<!-- Bad: -->
button { outline: none; } /* ❌ */
.no-focus:focus { outline: none; } /* ❌ */

<!-- Good: Custom focus ring -->
<button class="
  focus-visible:outline-none 
  focus-visible:ring-2 
  focus-visible:ring-blue-500 
  focus-visible:ring-offset-2
">
```

**Tab order:** Should follow logical reading order. Don't use `tabindex > 0`.

```html
<!-- Skip link (screen reader + keyboard) -->
<a href="#main-content" 
   class="sr-only focus:not-sr-only focus:absolute focus:z-50 focus:px-4 focus:py-2 focus:bg-white focus:top-4 focus:left-4">
  Skip to main content
</a>
<main id="main-content">...</main>
```

---

## Rule 2: Screen Reader Support (ARIA)
```html
<!-- Images: always alt text -->
<img src="avatar.jpg" alt="John Smith's profile photo" />
<img src="decorative.png" alt="" role="presentation" />  <!-- decorative -->

<!-- Icon buttons: need aria-label -->
<button aria-label="Close dialog">
  <XIcon class="size-4" aria-hidden="true" />
</button>

<!-- Status messages -->
<div role="status" aria-live="polite">
  <!-- Dynamic content updates read by screen readers -->
  {message && <p>{message}</p>}
</div>

<!-- Loading indicator -->
<div role="status" aria-label="Loading content">
  <Spinner aria-hidden="true" />
</div>

<!-- Form labeling -->
<label htmlFor="email">Email address</label>
<input id="email" type="email" aria-describedby="email-hint" />
<p id="email-hint" class="text-sm text-gray-500">We'll never share your email.</p>

<!-- Required fields -->
<input required aria-required="true" />

<!-- Error messages -->
<input aria-invalid={hasError} aria-describedby="email-error" />
{hasError && (
  <p id="email-error" role="alert" class="text-sm text-red-500">
    Please enter a valid email
  </p>
)}
```

---

## Rule 3: Color Contrast (Critical!)
**WCAG AA minimum:**
- Normal text (< 18px): **4.5:1 ratio**
- Large text (18px+ or 14px+ bold): **3:1 ratio**
- UI components (borders, icons): **3:1 ratio**

**Common failures:**
```html
<!-- Bad: white on blue-400 (2.9:1) ❌ -->
<button class="bg-blue-400 text-white">Submit</button>

<!-- Good: white on blue-600 (5.9:1) ✅ -->
<button class="bg-blue-600 text-white">Submit</button>

<!-- Bad: gray-400 text on white (2.5:1) ❌ -->
<p class="text-gray-400">Description</p>

<!-- Good: gray-600 on white (5.9:1) ✅ -->
<p class="text-gray-600">Description</p>
```

**Quick reference (on white bg):**
- `text-gray-950` → 20:1 ✅
- `text-gray-700` → 7.6:1 ✅
- `text-gray-500` → 4.6:1 ✅ (barely passing)
- `text-gray-400` → 2.5:1 ❌

---

## Rule 4: Semantic HTML
```html
<!-- Use semantic elements! -->
<header> <nav> <main> <section> <article> <aside> <footer>
<h1>...<h6>  <!-- proper heading hierarchy, never skip levels -->
<button>     <!-- for actions, NOT <div onclick> -->
<a href="">  <!-- for navigation -->
<ul>/<ol>    <!-- for lists -->
<table>      <!-- with <th> headers for data tables -->

<!-- Bad: div soup -->
<div class="nav-container" onclick="navigate()">
  <div class="nav-item">Home</div>
</div>

<!-- Good: semantic -->
<nav aria-label="Main navigation">
  <a href="/home">Home</a>
</nav>
```

---

## Rule 5: Dialogs & Modals (Focus Trap)
```tsx
// Radix UI Dialog handles this automatically
import * as Dialog from '@radix-ui/react-dialog'

// What it does:
// ✅ Traps focus inside dialog
// ✅ Returns focus to trigger when closed
// ✅ Closes on Escape key
// ✅ Aria-modal="true"
// ✅ aria-labelledby, aria-describedby

<Dialog.Root>
  <Dialog.Trigger asChild>
    <Button>Open</Button>
  </Dialog.Trigger>
  <Dialog.Portal>
    <Dialog.Overlay />
    <Dialog.Content aria-describedby="dialog-description">
      <Dialog.Title>Title</Dialog.Title>
      <p id="dialog-description">Description</p>
      <Dialog.Close />
    </Dialog.Content>
  </Dialog.Portal>
</Dialog.Root>
```

---

## Rule 6: Reduce Motion
```tsx
// Motion library
import { useReducedMotion } from "motion/react"

function AnimatedCard({ children }) {
  const shouldReduce = useReducedMotion()
  return (
    <motion.div
      initial={shouldReduce ? false : { opacity: 0, y: 20 }}
      animate={{ opacity: 1, y: 0 }}
      transition={shouldReduce ? { duration: 0 } : { duration: 0.4 }}
    >
      {children}
    </motion.div>
  )
}

// CSS only approach
@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after {
    animation-duration: 0.01ms !important;
    transition-duration: 0.01ms !important;
  }
}
```

---

## Rule 7: Forms Accessibility Checklist
```html
<!-- Every input needs a label -->
<div>
  <label for="username" class="text-sm font-medium">Username</label>
  <input 
    id="username"
    type="text"
    autocomplete="username"
    aria-required="true"
    aria-describedby="username-requirements"
  />
  <p id="username-requirements" class="text-sm text-gray-500">
    3-20 characters, letters and numbers only
  </p>
</div>

<!-- Group related fields -->
<fieldset>
  <legend class="text-base font-medium">Shipping address</legend>
  <!-- address fields -->
</fieldset>
```

---

## Rule 8: Color Not the Only Signal
```html
<!-- Bad: status shown by color only -->
<span class="text-red-500">Error</span>

<!-- Good: color + icon + text -->
<span class="flex items-center gap-1 text-red-600">
  <AlertCircle class="size-4" aria-hidden="true" />
  Error: Invalid email
</span>

<!-- Success/error form fields -->
<input class="border-red-500 focus:ring-red-500" aria-invalid="true" />
<input class="border-green-500 focus:ring-green-500" aria-valid="true" />
```

---

## Quick A11y Audit Checklist
- [ ] All images have alt text
- [ ] All icon buttons have aria-label
- [ ] Contrast ratio ≥ 4.5:1 for text
- [ ] Focus styles visible (not removed)
- [ ] Keyboard-navigable (Tab through everything)
- [ ] Screen reader tested (VoiceOver / NVDA)
- [ ] Semantic HTML used
- [ ] Forms have labels
- [ ] Error messages programmatically linked
- [ ] prefers-reduced-motion respected

---

## Anti-Patterns 🚫
- ❌ `outline: none` without replacement
- ❌ Click handlers on `<div>` (use `<button>`)
- ❌ Color-only information
- ❌ Placeholder as only label (disappears on type)
- ❌ Auto-playing audio/video
- ❌ Content reflow at 400% zoom
- ❌ Touch targets < 44px
