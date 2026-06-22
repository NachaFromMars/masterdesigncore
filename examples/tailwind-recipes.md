# Tailwind CSS v4 Recipes

Copy-paste Tailwind patterns được kiểm chứng thực tế.

---

## 🎨 Color & Background

```html
<!-- Gradient backgrounds -->
<div class="bg-gradient-to-br from-indigo-50 via-white to-purple-50 dark:from-gray-950 dark:via-gray-900 dark:to-indigo-950">

<div class="bg-gradient-to-r from-blue-600 to-violet-600 text-white">

<!-- Glassmorphism -->
<div class="bg-white/10 backdrop-blur-xl backdrop-saturate-150 border border-white/20">

<!-- Noise texture overlay (modern trend) -->
<div class="relative">
  <div class="absolute inset-0 opacity-30" style="background-image: url('/noise.png')"/>
</div>

<!-- Subtle dot grid background -->
<div class="bg-[radial-gradient(#e5e7eb_1px,transparent_1px)] [background-size:16px_16px]">

<!-- Dark gradient -->
<div class="bg-gradient-to-b from-gray-900 to-gray-950">
```

---

## 📝 Typography

```html
<!-- Display heading (hero) -->
<h1 class="text-5xl sm:text-6xl lg:text-7xl font-bold tracking-tighter text-gray-950 [text-wrap:balance]">

<!-- Gradient text -->
<span class="bg-gradient-to-r from-blue-600 to-violet-600 bg-clip-text text-transparent font-bold">

<!-- Eyebrow label -->
<p class="text-xs font-semibold uppercase tracking-[0.15em] text-blue-600">

<!-- Prose body -->
<p class="text-base text-gray-700 dark:text-gray-300 leading-relaxed max-w-prose">

<!-- Muted caption -->
<span class="text-xs text-gray-400 dark:text-gray-500">

<!-- Monospace code -->
<code class="text-sm font-mono bg-gray-100 dark:bg-gray-800 rounded px-1.5 py-0.5 text-gray-900 dark:text-gray-100">
```

---

## 🔲 Cards

```html
<!-- Standard card -->
<div class="rounded-xl border border-gray-200 dark:border-gray-800 bg-white dark:bg-gray-900 shadow-sm p-6">

<!-- Hover card (interactive) -->
<div class="rounded-xl border border-gray-200 dark:border-gray-800 bg-white dark:bg-gray-900 p-6 
  hover:shadow-lg hover:border-gray-300 dark:hover:border-gray-700 
  cursor-pointer transition-all duration-200">

<!-- Feature card with gradient border -->
<div class="rounded-xl p-px bg-gradient-to-br from-blue-500 to-purple-500">
  <div class="rounded-[11px] bg-white dark:bg-gray-900 p-6">
    Content
  </div>
</div>

<!-- Highlighted stat card -->
<div class="rounded-xl bg-gradient-to-br from-blue-600 to-indigo-700 text-white p-6 shadow-lg shadow-blue-500/20">

<!-- Glass card -->
<div class="rounded-2xl bg-white/80 dark:bg-gray-900/80 backdrop-blur-sm border border-gray-200/80 dark:border-gray-800/80 shadow-xl p-6">
```

---

## 🔘 Buttons

```html
<!-- Primary button -->
<button class="inline-flex items-center justify-center px-4 py-2 rounded-lg bg-blue-600 hover:bg-blue-700 active:bg-blue-800 active:scale-[0.98] text-white text-sm font-medium transition-all duration-150 focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-blue-500 focus-visible:ring-offset-2 disabled:opacity-50 disabled:cursor-not-allowed shadow-sm">

<!-- Outline button -->
<button class="inline-flex items-center px-4 py-2 rounded-lg border border-gray-300 dark:border-gray-700 bg-transparent hover:bg-gray-50 dark:hover:bg-gray-800 text-gray-700 dark:text-gray-300 text-sm font-medium transition-colors focus-visible:ring-2 focus-visible:ring-gray-400 focus-visible:outline-none">

<!-- Ghost button -->
<button class="inline-flex items-center px-3 py-2 rounded-lg text-gray-600 dark:text-gray-400 hover:bg-gray-100 dark:hover:bg-gray-800 hover:text-gray-900 dark:hover:text-white text-sm font-medium transition-colors focus-visible:ring-2 focus-visible:outline-none">

<!-- Gradient CTA button -->
<button class="px-6 py-3 rounded-xl bg-gradient-to-r from-blue-600 to-violet-600 hover:from-blue-700 hover:to-violet-700 text-white font-semibold shadow-lg shadow-blue-500/25 hover:shadow-blue-500/40 transition-all duration-200 active:scale-[0.98]">

<!-- Icon button -->
<button class="size-9 rounded-lg flex items-center justify-center text-gray-500 hover:bg-gray-100 dark:hover:bg-gray-800 hover:text-gray-700 dark:hover:text-gray-300 transition-colors focus-visible:ring-2 focus-visible:outline-none">

<!-- Pill button -->
<button class="px-4 py-1.5 rounded-full text-sm font-medium bg-blue-100 dark:bg-blue-900/30 text-blue-700 dark:text-blue-300 hover:bg-blue-200 dark:hover:bg-blue-900/50 transition-colors">
```

---

## 📋 Inputs

```html
<!-- Standard input -->
<input class="block w-full rounded-lg border border-gray-300 dark:border-gray-700 bg-white dark:bg-gray-900 px-3 py-2 text-sm text-gray-900 dark:text-gray-100 placeholder:text-gray-400 dark:placeholder:text-gray-500 focus:border-blue-500 dark:focus:border-blue-400 focus:ring-2 focus:ring-blue-500/20 outline-none transition-all">

<!-- Search input with icon -->
<div class="relative">
  <svg class="absolute left-3 top-1/2 -translate-y-1/2 size-4 text-gray-400" />
  <input class="pl-9 pr-4 h-10 w-full rounded-lg border border-gray-300 dark:border-gray-700 bg-white dark:bg-gray-900 text-sm focus:outline-none focus:ring-2 focus:ring-blue-500 dark:focus:ring-blue-400">
</div>

<!-- Error state input -->
<input class="block w-full rounded-lg border border-red-300 dark:border-red-700 bg-white dark:bg-gray-900 px-3 py-2 text-sm text-gray-900 focus:ring-2 focus:ring-red-500/20 focus:border-red-500 outline-none">
```

---

## 🏷️ Badges

```html
<!-- Status badges -->
<span class="inline-flex items-center gap-1.5 rounded-full px-2.5 py-0.5 text-xs font-medium bg-green-100 dark:bg-green-900/30 text-green-700 dark:text-green-400 ring-1 ring-inset ring-green-600/20">
  <span class="size-1.5 rounded-full bg-green-500"></span>
  Active
</span>

<span class="rounded-full px-2.5 py-0.5 text-xs font-medium bg-yellow-100 dark:bg-yellow-900/30 text-yellow-700 dark:text-yellow-400">
  Pending
</span>

<span class="rounded-full px-2.5 py-0.5 text-xs font-medium bg-red-100 dark:bg-red-900/30 text-red-600 dark:text-red-400">
  Error
</span>

<span class="rounded-full px-2.5 py-0.5 text-xs font-medium bg-gray-100 dark:bg-gray-800 text-gray-600 dark:text-gray-400">
  Draft
</span>
```

---

## 📊 Layout

```html
<!-- App shell with sidebar -->
<div class="flex h-screen bg-gray-50 dark:bg-gray-950 overflow-hidden">
  <aside class="hidden md:flex flex-col w-64 border-r border-gray-200 dark:border-gray-800 bg-white dark:bg-gray-900">
    Sidebar
  </aside>
  <main class="flex-1 overflow-y-auto">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-8">
      Content
    </div>
  </main>
</div>

<!-- Sticky nav -->
<nav class="sticky top-0 z-50 h-16 border-b border-gray-200 dark:border-gray-800 bg-white/80 dark:bg-gray-900/80 backdrop-blur-sm flex items-center px-4">

<!-- Centered auth page -->
<div class="min-h-screen flex items-center justify-center bg-gray-50 dark:bg-gray-950 px-4">
  <div class="w-full max-w-md">
    Card
  </div>
</div>

<!-- Responsive grid -->
<div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4 gap-4 sm:gap-6">

<!-- Dashboard 2/3 + 1/3 split -->
<div class="grid grid-cols-1 lg:grid-cols-3 gap-6">
  <div class="lg:col-span-2">Main</div>
  <div>Sidebar</div>
</div>
```

---

## 🌊 Dividers

```html
<!-- Standard divider -->
<hr class="border-gray-200 dark:border-gray-800">

<!-- With text -->
<div class="relative flex items-center">
  <div class="flex-1 border-t border-gray-200 dark:border-gray-800"></div>
  <span class="mx-4 text-xs text-gray-400 dark:text-gray-500">OR</span>
  <div class="flex-1 border-t border-gray-200 dark:border-gray-800"></div>
</div>

<!-- Vertical divider -->
<div class="h-6 w-px bg-gray-200 dark:bg-gray-700 mx-2"></div>
```

---

## 💡 Useful Utilities

```html
<!-- Truncate long text -->
<p class="truncate">Very long text that might overflow...</p>

<!-- Multi-line clamp -->
<p class="line-clamp-2">...</p>
<p class="line-clamp-3">...</p>

<!-- Visually hidden (screen reader only) -->
<span class="sr-only">Screen reader text</span>

<!-- No select (copy prevention) -->
<div class="select-none">

<!-- Smooth scroll -->
<html class="scroll-smooth">

<!-- Tabular numbers (for data) -->
<span class="tabular-nums font-mono">1,234,567</span>

<!-- Balance text wrap (headings) -->
<h1 class="[text-wrap:balance]">Heading that wraps nicely</h1>

<!-- Pretty text wrap (body) -->
<p class="[text-wrap:pretty]">Body text that wraps better</p>
```
