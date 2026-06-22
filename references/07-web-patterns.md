# 07 — Web UI Patterns

> SOURCE: Refactoring UI, Tailwind UI, Vercel design system, web best practices 2025

---

## Core Principle
Web UI = phải đẹp trên mọi viewport, fast to load, và không cần scroll quá nhiều để hiểu nội dung chính.

---

## Rule 1: Page Structure Hierarchy
```html
<!-- Standard app layout -->
<div class="min-h-screen bg-gray-50 dark:bg-gray-950">
  <!-- Top nav -->
  <header class="sticky top-0 z-50 h-16 border-b bg-white/80 backdrop-blur-sm
    dark:bg-gray-900/80 dark:border-gray-800 flex items-center px-4">
    <nav>...</nav>
  </header>
  
  <!-- Main content area -->
  <main class="mx-auto max-w-7xl px-4 sm:px-6 lg:px-8 py-8">
    <!-- Page header -->
    <div class="mb-8">
      <h1 class="text-3xl font-bold text-gray-950 dark:text-white">Dashboard</h1>
      <p class="mt-1 text-gray-500">Welcome back, here's your overview.</p>
    </div>
    
    <!-- Content -->
  </main>
</div>
```

---

## Rule 2: Hero Section (Landing Page)
```html
<section class="relative overflow-hidden px-6 py-24 sm:py-32 lg:px-8">
  <!-- Background gradient -->
  <div class="absolute inset-0 -z-10 bg-gradient-to-br from-indigo-50 via-white to-purple-50
    dark:from-gray-950 dark:via-gray-900 dark:to-indigo-950" />
  
  <div class="mx-auto max-w-4xl text-center">
    <!-- Eyebrow label -->
    <div class="mb-4 inline-flex items-center gap-2 rounded-full border bg-white/60
      px-3 py-1 text-sm text-gray-600 backdrop-blur-sm dark:bg-gray-900/60">
      <span class="size-2 rounded-full bg-green-500" />
      New: Feature X just launched
    </div>
    
    <h1 class="text-5xl font-bold tracking-tight text-gray-950 sm:text-7xl
      dark:text-white [text-wrap:balance]">
      Build beautiful UIs <span class="text-indigo-600">faster</span>
    </h1>
    
    <p class="mx-auto mt-6 max-w-2xl text-lg text-gray-600 dark:text-gray-400 leading-relaxed">
      Description text here.
    </p>
    
    <div class="mt-10 flex items-center justify-center gap-4">
      <Button size="lg">Get started free</Button>
      <Button variant="ghost" size="lg">
        Watch demo <ArrowRight class="ml-1 size-4" />
      </Button>
    </div>
  </div>
</section>
```

---

## Rule 3: Card Grid (Dashboard)
```html
<!-- Stats grid -->
<div class="grid grid-cols-1 gap-4 sm:grid-cols-2 xl:grid-cols-4">
  <div class="rounded-xl border bg-white p-6 dark:bg-gray-900 dark:border-gray-800">
    <div class="flex items-center justify-between">
      <p class="text-sm font-medium text-gray-500">Total Revenue</p>
      <div class="rounded-lg bg-green-50 p-2 dark:bg-green-950">
        <TrendingUp class="size-4 text-green-600" />
      </div>
    </div>
    <p class="mt-2 text-3xl font-bold text-gray-950 dark:text-white">$45,231</p>
    <p class="mt-1 text-sm text-green-600">+20.1% from last month</p>
  </div>
</div>
```

---

## Rule 4: Sidebar Navigation
```html
<aside class="w-60 flex flex-col border-r bg-white dark:bg-gray-950 dark:border-gray-800 py-4">
  <!-- Logo -->
  <div class="px-4 mb-6">
    <Logo class="h-8" />
  </div>
  
  <!-- Nav groups -->
  <nav class="flex-1 space-y-1 px-3">
    <p class="px-2 mb-1 text-xs font-semibold uppercase tracking-widest text-gray-400">
      Overview
    </p>
    <a href="/dashboard" class="flex items-center gap-3 rounded-lg px-3 py-2 text-sm
      font-medium text-gray-700 hover:bg-gray-100 hover:text-gray-900
      dark:text-gray-300 dark:hover:bg-gray-800 dark:hover:text-white
      transition-colors duration-150">
      <Home class="size-4 text-gray-400" />
      Dashboard
    </a>
    <!-- Active state -->
    <a href="/analytics" class="flex items-center gap-3 rounded-lg px-3 py-2 text-sm
      font-medium bg-indigo-50 text-indigo-700 dark:bg-indigo-950 dark:text-indigo-300">
      <BarChart2 class="size-4" />
      Analytics
    </a>
  </nav>
  
  <!-- Footer -->
  <div class="border-t pt-4 px-4 dark:border-gray-800">
    <UserAvatarMenu />
  </div>
</aside>
```

---

## Rule 5: Table with Actions
```html
<div class="rounded-xl border overflow-hidden dark:border-gray-800">
  <div class="flex items-center justify-between px-6 py-4 border-b dark:border-gray-800">
    <h3 class="font-semibold text-gray-950 dark:text-white">Transactions</h3>
    <div class="flex items-center gap-2">
      <Input placeholder="Search..." class="w-64 h-8 text-sm" />
      <Button variant="outline" size="sm">Filter</Button>
      <Button size="sm">Export</Button>
    </div>
  </div>
  <Table>
    <!-- ... -->
  </Table>
  <div class="flex items-center justify-between px-6 py-4 border-t dark:border-gray-800">
    <p class="text-sm text-gray-500">Showing 1-10 of 100</p>
    <Pagination />
  </div>
</div>
```

---

## Rule 6: Empty States
```html
<!-- Always provide empty states! -->
<div class="flex flex-col items-center justify-center py-16 text-center">
  <div class="mb-4 rounded-full bg-gray-100 p-4 dark:bg-gray-800">
    <Inbox class="size-8 text-gray-400" />
  </div>
  <h3 class="mb-1 text-lg font-semibold text-gray-900 dark:text-white">
    No notifications yet
  </h3>
  <p class="mb-6 text-sm text-gray-500 max-w-xs">
    When you get notifications, they'll appear here.
  </p>
  <Button variant="outline" size="sm">Browse</Button>
</div>
```

---

## Rule 7: Loading States
```html
<!-- Skeleton loading -->
<div class="animate-pulse">
  <div class="h-4 bg-gray-200 rounded w-3/4 mb-2 dark:bg-gray-800" />
  <div class="h-4 bg-gray-200 rounded w-1/2 dark:bg-gray-800" />
</div>

<!-- Inline spinner -->
<div class="flex items-center gap-2 text-gray-500">
  <Loader2 class="size-4 animate-spin" />
  <span class="text-sm">Loading...</span>
</div>
```

---

## Rule 8: Sticky Header Pattern
```html
<header class="
  sticky top-0 z-50
  h-16 
  bg-white/80 dark:bg-gray-900/80 
  backdrop-blur-md backdrop-saturate-150
  border-b border-gray-200/80 dark:border-gray-800/80
  flex items-center
">
```

---

## Anti-Patterns 🚫
- ❌ Cluttered navbars with 10+ items
- ❌ No loading/empty states
- ❌ Modal overflow without scroll lock
- ❌ Fixed px widths that break on mobile
- ❌ No max-width on content (100% width text = unreadable)
- ❌ Hover-only interactions (no keyboard access)
- ❌ Long forms without sections/steps
