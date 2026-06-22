# 08 — Dark Mode Design

> SOURCE: Tailwind CSS dark mode docs, Apple HIG dark mode, accessible dark mode guidelines

---

## Core Principle
Dark mode không phải là "invert colors". Nó là một carefully crafted color system song song với light mode.

---

## Rule 1: Setup (Tailwind v4)
```css
/* globals.css */
@import "tailwindcss";

/* Method 1: OS preference (default) */
/* dark: variant automatically uses prefers-color-scheme */

/* Method 2: Manual class toggle (recommended for apps) */
@custom-variant dark (&:where(.dark, .dark *));
```

```js
// Toggle dark mode
document.documentElement.classList.toggle('dark', isDark)
localStorage.setItem('theme', isDark ? 'dark' : 'light')

// On page load (prevent FOUC - in <head>)
const isDark = localStorage.theme === 'dark' ||
  (!('theme' in localStorage) && window.matchMedia('(prefers-color-scheme: dark)').matches)
document.documentElement.classList.toggle('dark', isDark)
```

---

## Rule 2: Dark Color Palette Rules
**NOT just inverting!** Dark mode colors follow different rules:

| Element | Light | Dark | Rule |
|---------|-------|------|------|
| Page bg | `gray-50` | `gray-950` | NOT black — dark gray |
| Surface | `white` | `gray-900` | Slightly lighter than bg |
| Surface raised | `gray-50` | `gray-800` | Each elevation = lighter |
| Border | `gray-200` | `gray-800` | Very subtle |
| Text primary | `gray-950` | `gray-50` | NOT pure white |
| Text secondary | `gray-600` | `gray-400` | Mid-gray |
| Text muted | `gray-400` | `gray-600` | Reversed! |

```html
<!-- Every element needs dark: variant -->
<div class="bg-white dark:bg-gray-900 border border-gray-200 dark:border-gray-800">
  <h1 class="text-gray-950 dark:text-white">Title</h1>
  <p class="text-gray-600 dark:text-gray-400">Description</p>
</div>
```

---

## Rule 3: Elevation in Dark Mode
In light mode: shadows show elevation.
In dark mode: lighter backgrounds show elevation.

```html
<!-- Light: shadow creates depth -->
<div class="bg-white shadow-md">Card</div>

<!-- Dark: lighter bg creates depth (not shadow!) -->
<div class="dark:bg-gray-800">Card</div>  <!-- slightly lighter than gray-900 bg -->
<div class="dark:bg-gray-750">Raised card</div>
```

**shadcn/ui handles this with CSS vars:**
```css
.dark {
  --background: oklch(0.145 0 0);   /* Very dark */
  --card: oklch(0.205 0 0);          /* Slightly lighter */
  --popover: oklch(0.205 0 0);
}
```

---

## Rule 4: Reduce Saturation in Dark
Vivid colors on dark bg can feel aggressive/neon.
Use lighter, slightly desaturated variants:

```html
<!-- Light mode: saturated -->
<div class="bg-blue-600 text-white">Primary</div>

<!-- Dark mode: lighter, less saturated -->
<div class="bg-blue-600 dark:bg-blue-400 text-white dark:text-gray-950">
```

**Accent colors in dark:**
- Light: `blue-600` → Dark: `blue-400`
- Light: `green-600` → Dark: `green-400`
- Light: `red-600` → Dark: `red-400`

---

## Rule 5: Shadows in Dark Mode
```html
<!-- Shadows invisible in dark → use ring/border instead -->
<div class="shadow-lg dark:shadow-none dark:ring-1 dark:ring-white/10 rounded-xl">

<!-- Or subtle colored shadow -->
<div class="shadow-lg shadow-black/5 dark:shadow-black/30 rounded-xl">
```

---

## Rule 6: Images & Media
```html
<!-- Images: often need slight dim in dark mode -->
<img class="opacity-100 dark:opacity-90 rounded-lg" />

<!-- SVG icons: switch fill color -->
<svg class="fill-gray-900 dark:fill-gray-100" />

<!-- Logos: provide dark variant or use brightness filter -->
<img class="dark:brightness-0 dark:invert" src="logo-light.svg" />
```

---

## Rule 7: Form Elements in Dark
```html
<input class="
  bg-white dark:bg-gray-900
  border border-gray-300 dark:border-gray-700
  text-gray-900 dark:text-gray-100
  placeholder:text-gray-400 dark:placeholder:text-gray-500
  focus:border-blue-500 dark:focus:border-blue-400
  focus:ring-2 focus:ring-blue-500/20 dark:focus:ring-blue-400/20
  rounded-lg px-3 py-2 text-sm
  outline-none transition
">
```

---

## Rule 8: Glassmorphism (Dark Mode Special)
```html
<!-- Glass effect: works best on dark -->
<div class="
  backdrop-blur-xl backdrop-saturate-150
  bg-white/10 dark:bg-white/5
  border border-white/20 dark:border-white/10
  rounded-2xl
  shadow-xl shadow-black/20
">
  Glass panel
</div>
```

---

## Rule 9: Color-scheme Meta
```html
<!-- Tells browser to use dark scrollbars, inputs, etc. -->
<meta name="color-scheme" content="dark light" />

<!-- Or in CSS -->
:root { color-scheme: light dark; }
.dark { color-scheme: dark; }
```

---

## Dark Mode Component Quick Reference
```html
<!-- Page bg -->
<body class="bg-gray-50 dark:bg-gray-950">

<!-- Card -->
<div class="bg-white dark:bg-gray-900 border border-gray-200 dark:border-gray-800 rounded-xl">

<!-- Button primary -->
<button class="bg-blue-600 hover:bg-blue-700 dark:bg-blue-500 dark:hover:bg-blue-400 text-white">

<!-- Badge success -->
<span class="bg-green-100 text-green-700 dark:bg-green-900/30 dark:text-green-400 text-sm px-2 py-0.5 rounded-full">

<!-- Divider -->
<hr class="border-gray-200 dark:border-gray-800">

<!-- Code block -->
<pre class="bg-gray-100 dark:bg-gray-800 text-gray-900 dark:text-gray-100 rounded-lg p-4">

<!-- Overlay/backdrop -->
<div class="bg-black/20 dark:bg-black/50">
```

---

## Anti-Patterns 🚫
- ❌ Pure black (#000) background → use gray-950 or gray-900
- ❌ Pure white (#fff) text on dark → use gray-50
- ❌ Same shadow values for both modes
- ❌ Full saturation colors as dark mode accents
- ❌ No color-scheme meta (browser inputs look wrong)
- ❌ Images not adjusted for dark (too bright)
- ❌ Forgetting dark: variant on ANY colored element
