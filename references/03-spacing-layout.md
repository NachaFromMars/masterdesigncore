# 03 — Spacing & Layout

> SOURCE: Tailwind CSS v4 padding/spacing docs, Refactoring UI, 8pt Grid System

---

## Core Principle
Spacing tạo **rhythm** và **hierarchy**. Consistent spacing = professional UI. Inconsistent spacing = amateur.

---

## Rule 1: 4pt/8pt Spacing System
Tailwind's `--spacing` base = **0.25rem (4px)**. Mọi giá trị spacing đều là bội số của 4px.

| Class | Value | Pixels |
|-------|-------|--------|
| `p-1` | 0.25rem | 4px |
| `p-2` | 0.5rem | 8px |
| `p-3` | 0.75rem | 12px |
| `p-4` | 1rem | 16px |
| `p-5` | 1.25rem | 20px |
| `p-6` | 1.5rem | 24px |
| `p-8` | 2rem | 32px |
| `p-10` | 2.5rem | 40px |
| `p-12` | 3rem | 48px |
| `p-16` | 4rem | 64px |
| `p-20` | 5rem | 80px |
| `p-24` | 6rem | 96px |

**Anti-pattern:** Dùng arbitrary values `p-[13px]`, `p-[7px]` → breaks rhythm.

---

## Rule 2: Component Internal Spacing Recipes
```html
<!-- Compact button -->
<button class="px-3 py-1.5 text-sm">Small</button>

<!-- Default button -->
<button class="px-4 py-2 text-sm">Default</button>

<!-- Large button -->
<button class="px-6 py-3 text-base">Large</button>

<!-- Card -->
<div class="p-6"> <!-- mobile -->
<div class="p-8"> <!-- desktop -->

<!-- Section padding -->
<section class="px-4 py-12 md:px-8 md:py-24">

<!-- Navigation item -->
<a class="px-4 py-2">Nav item</a>
```

---

## Rule 3: Space Between Related vs Unrelated Items
**Gestalt Proximity:** Liên quan → gần nhau. Không liên quan → xa nhau.

```html
<!-- Good: heading closer to its content -->
<div class="mt-12">
  <h2 class="text-2xl font-bold mb-3">Section Title</h2>  <!-- mb-3 close -->
  <p class="text-gray-600 mb-8">Description...</p>        <!-- mb-8 far -->
</div>

<!-- Form fields: related group -->
<div class="space-y-4">     <!-- between fields -->
  <div class="space-y-1.5"> <!-- label → input: tight -->
    <label>Email</label>
    <input />
  </div>
</div>
```

---

## Rule 4: Layout Grid (12-column)
```html
<!-- 12-col responsive grid -->
<div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">

<!-- Sidebar + content -->
<div class="grid grid-cols-1 lg:grid-cols-[240px_1fr] gap-8">

<!-- Dashboard layout -->
<div class="grid grid-cols-1 md:grid-cols-2 xl:grid-cols-4 gap-4">
```

---

## Rule 5: Container + Max Width
```html
<!-- Standard container -->
<div class="mx-auto max-w-7xl px-4 sm:px-6 lg:px-8">

<!-- Narrow content (articles, forms) -->
<div class="mx-auto max-w-2xl px-4">

<!-- Full-bleed hero -->
<section class="w-full px-4 md:px-8 lg:px-16">
```

**Max widths reference:**
- `max-w-sm` (384px) — Small cards, narrow modals
- `max-w-md` (448px) — Forms, auth pages
- `max-w-lg` (512px) — Dialogs
- `max-w-2xl` (672px) — Articles, docs
- `max-w-4xl` (896px) — Wide content
- `max-w-7xl` (1280px) — App container
- `max-w-screen-2xl` — Full wide layouts

---

## Rule 6: Flexbox Patterns
```html
<!-- Horizontal center -->
<div class="flex items-center justify-between">

<!-- Vertical stack -->
<div class="flex flex-col gap-4">

<!-- Icon + text inline -->
<div class="flex items-center gap-2">
  <Icon class="size-4" />
  <span>Label</span>
</div>

<!-- Card with footer pinned bottom -->
<div class="flex flex-col h-full">
  <div class="flex-1">Content</div>
  <div class="mt-auto">Footer</div>
</div>
```

---

## Rule 7: Whitespace là vũ khí
Thêm padding/margin nhiều hơn bạn nghĩ cần. UIs thường quá crowded, không đủ breathing room.

```html
<!-- Section spacing: generous -->
<section class="py-16 md:py-24 lg:py-32">

<!-- Hero: very generous -->
<div class="py-20 md:py-32 lg:py-40">
```

---

## Rule 8: Negative Space cho Premium Feel
Apple, Linear, Notion đều dùng negative space rộng rãi. Hãy kháng sự cám dỗ fill mọi pixel.

---

## Common Layout Patterns
```html
<!-- App shell -->
<div class="min-h-screen flex flex-col">
  <header class="h-16 border-b">Nav</header>
  <div class="flex flex-1 overflow-hidden">
    <aside class="w-60 border-r overflow-y-auto hidden md:block">Sidebar</aside>
    <main class="flex-1 overflow-y-auto p-6">Content</main>
  </div>
</div>

<!-- Dashboard cards grid -->
<div class="grid grid-cols-1 sm:grid-cols-2 xl:grid-cols-4 gap-4 mb-8">

<!-- Auth page center -->
<div class="min-h-screen flex items-center justify-center bg-gray-50">
  <div class="w-full max-w-md p-8 bg-white rounded-xl shadow-lg">
```

---

## Anti-Patterns 🚫
- ❌ Inconsistent spacing (16px here, 18px there)
- ❌ 0px padding — elements touching edges
- ❌ Overcrowded — no breathing room
- ❌ Inconsistent gap trong cùng một list
- ❌ Justify content giữa 2 items trên 1 hàng (dùng gap thay)
