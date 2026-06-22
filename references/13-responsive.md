# 13 — Responsive Design

> SOURCE: Tailwind CSS v4 responsive docs, mobile-first principles, modern responsive patterns

---

## Core Principle
**Mobile-first**: Design for smallest screen first, then progressively enhance for larger screens.

---

## Rule 1: Tailwind v4 Breakpoints
```
sm:  ≥ 40rem  (640px)   — large phones, small tablets
md:  ≥ 48rem  (768px)   — tablets, portrait iPad
lg:  ≥ 64rem  (1024px)  — laptops, landscape iPad
xl:  ≥ 80rem  (1280px)  — desktops
2xl: ≥ 96rem  (1536px)  — large monitors
```

**Custom breakpoints:**
```css
@theme {
  --breakpoint-xs: 30rem;      /* 480px */
  --breakpoint-3xl: 120rem;    /* 1920px */
}
```

---

## Rule 2: Mobile-First Mindset
```html
<!-- BASE = mobile. Add variants for larger. -->

<!-- ✅ Correct: mobile first -->
<div class="text-base md:text-lg lg:text-xl">

<!-- ❌ Wrong: trying to "target mobile" with sm: -->
<div class="lg:text-xl md:text-lg sm:text-base">  <!-- sm: means 640px+ not "small" -->

<!-- Grid: 1 col mobile → 2 → 3 → 4 -->
<div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4 gap-4">

<!-- Stack on mobile, row on desktop -->
<div class="flex flex-col md:flex-row gap-4">

<!-- Hide on mobile, show on desktop -->
<div class="hidden md:block">Desktop only</div>
<div class="md:hidden">Mobile only</div>
```

---

## Rule 3: Responsive Typography
```html
<!-- Fluid heading (scales with viewport) -->
<h1 class="text-3xl sm:text-4xl md:text-5xl lg:text-6xl font-bold tracking-tight">

<!-- Body stays readable -->
<p class="text-base leading-relaxed max-w-prose">

<!-- Card grid text adaptation -->
<div class="grid grid-cols-1 sm:grid-cols-2">
  <div>
    <h3 class="text-lg font-semibold">Title</h3>
    <p class="text-sm text-gray-600 mt-1">Description</p>
  </div>
</div>
```

---

## Rule 4: Responsive Navigation Patterns
```tsx
// Desktop: sidebar | Mobile: bottom tab bar

// Pattern 1: Collapsible sidebar
<aside className={cn(
  "fixed inset-y-0 left-0 z-40 w-72 bg-white border-r transition-transform",
  sidebarOpen ? "translate-x-0" : "-translate-x-full",
  "md:relative md:translate-x-0 md:w-64"
)}>

// Pattern 2: Mobile bottom nav
<nav class="fixed bottom-0 left-0 right-0 border-t bg-white md:hidden">
  <div class="flex justify-around h-16 pb-safe">
    <NavItem href="/" icon={Home} label="Home" />
    <NavItem href="/search" icon={Search} label="Search" />
    <NavItem href="/profile" icon={User} label="Profile" />
  </div>
</nav>

// Pattern 3: Hamburger → slide menu (mobile)
<header class="flex items-center justify-between h-16 px-4 border-b md:hidden">
  <Logo />
  <button onClick={toggleMenu}><Menu class="size-5" /></button>
</header>
```

---

## Rule 5: Responsive Container System
```html
<!-- Full-bleed background, contained content -->
<section class="w-full bg-gray-50">
  <div class="mx-auto max-w-7xl px-4 sm:px-6 lg:px-8">
    <!-- Content -->
  </div>
</section>

<!-- Dashboard content area -->
<main class="flex-1 overflow-y-auto">
  <div class="p-4 sm:p-6 lg:p-8">
    <!-- Page content -->
  </div>
</main>

<!-- Article / form: constrained width -->
<div class="mx-auto max-w-2xl px-4 py-8 sm:py-12">
```

---

## Rule 6: Responsive Images
```html
<!-- Responsive hero image -->
<img 
  class="w-full object-cover h-48 sm:h-64 md:h-80 lg:h-96 rounded-xl"
  src="hero.jpg"
  alt="Hero"
/>

<!-- Aspect ratio preserved -->
<div class="aspect-video w-full overflow-hidden rounded-lg">
  <img class="w-full h-full object-cover" />
</div>

<!-- Avatar sizes responsive -->
<img class="size-8 sm:size-10 md:size-12 rounded-full" />
```

---

## Rule 7: Responsive Tables
Tables break on mobile. Solutions:

```html
<!-- Option 1: Horizontal scroll -->
<div class="overflow-x-auto -mx-4 sm:mx-0">
  <div class="min-w-[640px] sm:min-w-0">
    <table class="w-full">...</table>
  </div>
</div>

<!-- Option 2: Card layout on mobile -->
<div class="hidden sm:block">
  <table>...</table>  <!-- Table on desktop -->
</div>
<div class="sm:hidden space-y-4">
  {items.map(item => (
    <div class="bg-white rounded-lg p-4 border">  <!-- Cards on mobile -->
      <div class="flex justify-between">
        <span class="font-medium">{item.name}</span>
        <Badge>{item.status}</Badge>
      </div>
      <p class="text-sm text-gray-500 mt-1">{item.date}</p>
    </div>
  ))}
</div>
```

---

## Rule 8: Responsive Forms
```html
<!-- Full width on mobile, limited on desktop -->
<form class="max-w-2xl mx-auto px-4 sm:px-0">
  
  <!-- Stack on mobile, side-by-side on desktop -->
  <div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
    <div>
      <Label>First Name</Label>
      <Input />
    </div>
    <div>
      <Label>Last Name</Label>
      <Input />
    </div>
  </div>

  <!-- CTA: full width on mobile -->
  <Button class="w-full sm:w-auto mt-6">Submit</Button>
</form>
```

---

## Rule 9: Container Queries (Advanced)
```css
/* Component-level responsiveness */
@container (min-width: 480px) {
  .card-grid {
    grid-template-columns: repeat(2, 1fr);
  }
}
```

```html
<div class="@container">
  <div class="grid @sm:grid-cols-2 @lg:grid-cols-3 gap-4">
```

---

## Rule 10: Viewport-based Units
```html
<!-- Full viewport sections -->
<section class="min-h-screen flex items-center">
<section class="h-screen overflow-hidden">

<!-- Dynamic viewport (mobile browser chrome aware) -->
<div class="min-h-dvh">  <!-- dynamic viewport height -->
```

---

## Responsive Breakpoint Decision Guide
```
Mobile (< 640px): 
  - Single column layouts
  - Bottom navigation
  - Large touch targets (44px+)
  - Stacked forms
  - Collapsed sidebars

Tablet (640-1024px):
  - 2-column grids
  - Visible but compact navigation  
  - Hybrid top + sidebar nav

Desktop (1024px+):
  - Multi-column grids (3-4)
  - Persistent sidebar (240-280px)
  - Hover states enhanced
  - Compact density OK

Wide (1280px+):
  - Max-width container (1280-1536px)
  - Wider sidebars
  - More visible context panels
```

---

## Anti-Patterns 🚫
- ❌ `sm:` prefix for "mobile styles" (it means 640px+)
- ❌ Fixed px widths on containers
- ❌ Horizontal overflow without scroll
- ❌ Text that doesn't scale down on mobile
- ❌ Hover-only actions on touch devices
- ❌ Modal dialogs that overflow viewport on mobile
