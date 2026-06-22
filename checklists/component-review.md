# Component Review Checklist

Review từng component trước khi ship.

---

## ✅ All Interactive States Present
- [ ] Default/rest state
- [ ] Hover state (background, color, cursor change)
- [ ] Active/pressed state (scale down, darker bg)
- [ ] Focus-visible state (ring, outline — never hidden)
- [ ] Disabled state (opacity + cursor-not-allowed)
- [ ] Loading state (spinner + disabled)
- [ ] Success/error states (for forms, actions)

## ✅ Sizes & Variants
- [ ] Multiple sizes available? (sm, default, lg)
- [ ] Variants match the use case (primary, secondary, ghost, destructive)
- [ ] Sizes consistent with system (don't invent custom sizes)

## ✅ Accessibility
- [ ] Keyboard accessible (Tab, Enter, Space, Escape)
- [ ] `aria-label` on icon-only components
- [ ] `role` correct when not using semantic HTML
- [ ] Screen reader friendly labels
- [ ] Focus trap in modals/dialogs (use Radix UI)

## ✅ Flexibility
- [ ] Works with dynamic content (long text truncates, not breaks)
- [ ] Works in dark mode
- [ ] Works on mobile (touch targets)
- [ ] `className` prop forwarded for customization

## ✅ Code Quality
- [ ] TypeScript types defined
- [ ] Default props set
- [ ] `forwardRef` used (if ref might be needed)
- [ ] `asChild` pattern if polymorphic

## ✅ Common Mistakes Check
- [ ] No hardcoded colors (use CSS variables)
- [ ] No hardcoded pixel spacing (use Tailwind scale)
- [ ] No `z-index: 9999` (use system z-index)
- [ ] No `!important` unless absolutely needed

---

## Button Specific
```
✅ Has: hover + active + focus + disabled + loading
✅ Icon-only buttons have aria-label
✅ Destructive variant is RED and not casually placed
✅ Submit button inside form (not just onClick)
✅ Loading prevents double-submit
```

## Input Specific
```
✅ Has: focus ring + error border + disabled style
✅ Placeholder is not the only label
✅ Error message shown below (not replacing placeholder)
✅ autoComplete set where applicable
✅ type set correctly (email, password, tel, etc.)
```

## Modal/Dialog Specific
```
✅ ESC key closes it
✅ Clicking backdrop closes it (optional)
✅ Focus moves to dialog on open
✅ Focus returns to trigger on close
✅ aria-labelledby + aria-describedby set
✅ Scrollable when content overflows
```

## Card Specific
```
✅ Content doesn't overflow (long text truncates)
✅ Image has fixed aspect ratio (not distorted)
✅ Hover state if interactive
✅ Empty state defined
```
