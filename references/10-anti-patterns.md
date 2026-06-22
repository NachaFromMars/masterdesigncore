# 10 — Anti-Patterns (Những Lỗi UI Phổ Biến)

> SOURCE: Refactoring UI, UX anti-patterns research, common design mistakes

---

## "The Ugly Truth" — Why UIs Look Bad
Most ugly UIs have ONE root cause: **lack of visual hierarchy**. Fix hierarchy → UI looks 10x better instantly.

---

## Anti-Pattern 1: No Visual Hierarchy
**Problem:** Mọi element đều same size, same weight, same color.
```html
<!-- ❌ Bad: flat hierarchy -->
<div class="text-base text-black">Title</div>
<div class="text-base text-black">Description</div>
<div class="text-base text-black">Date</div>

<!-- ✅ Good: clear hierarchy -->
<h3 class="text-lg font-semibold text-gray-950">Title</h3>
<p class="text-sm text-gray-600 mt-1">Description</p>
<span class="text-xs text-gray-400 mt-2 block">March 6, 2025</span>
```

---

## Anti-Pattern 2: Too Many Colors
**Problem:** Dùng 6-8 màu khác nhau → looks chaotic.
**Fix:** Max 1 brand color + gray scale + semantic (red/green).

```html
<!-- ❌ Bad: rainbow UI -->
<button class="bg-blue-500">Save</button>
<button class="bg-green-500">Export</button>
<button class="bg-purple-500">Share</button>
<button class="bg-orange-500">Preview</button>

<!-- ✅ Good: primary + variants -->
<button class="bg-blue-600">Save</button>
<button class="bg-white border border-gray-300 text-gray-700">Export</button>
<button class="bg-white border border-gray-300 text-gray-700">Share</button>
<button class="bg-gray-100 text-gray-700">Preview</button>
```

---

## Anti-Pattern 3: Insufficient Whitespace
**Problem:** Elements tightly packed, no breathing room.
```html
<!-- ❌ Bad: cramped -->
<div class="p-2 border">
  <img class="w-full" />
  <h3 class="text-sm mt-1">Title</h3>
  <p class="text-xs">Description</p>
</div>

<!-- ✅ Good: generous spacing -->
<div class="p-6 border rounded-xl">
  <img class="w-full rounded-lg mb-4" />
  <h3 class="text-base font-semibold text-gray-900 mb-1">Title</h3>
  <p class="text-sm text-gray-600">Description</p>
</div>
```

---

## Anti-Pattern 4: Low Contrast Text
**Problem:** Text chỉ thoáng nhìn đã mờ, không đọc được.
```html
<!-- ❌ Bad: low contrast -->
<p class="text-gray-300 bg-white">Important text</p>  <!-- contrast: 1.6:1 -->
<p class="text-blue-300 bg-white">Link</p>  <!-- contrast: 2.1:1 -->

<!-- ✅ Good: high contrast -->
<p class="text-gray-700 bg-white">Important text</p>  <!-- contrast: 7.6:1 -->
<p class="text-blue-600 bg-white">Link</p>  <!-- contrast: 4.9:1 -->
```

---

## Anti-Pattern 5: Borders Everywhere
**Problem:** Thêm border để "separate" sections → creates prison-bar UI.
**Fix:** Dùng background color difference thay vì borders.

```html
<!-- ❌ Bad: box inside box inside box -->
<div class="border p-4">
  <div class="border p-3">
    <div class="border p-2">Content</div>
  </div>
</div>

<!-- ✅ Good: subtle bg difference -->
<div class="bg-gray-50 rounded-xl p-6">
  <div class="bg-white rounded-lg p-4 shadow-sm">Content</div>
</div>
```

---

## Anti-Pattern 6: Inconsistent Alignment
```html
<!-- ❌ Bad: mixed alignments -->
<div>
  <img class="mx-auto" />
  <h3 class="text-left">Title</h3>
  <p class="text-center">Description</p>
  <button class="ml-2">Action</button>
</div>

<!-- ✅ Good: consistent alignment -->
<div class="text-left">
  <img class="rounded-lg w-full" />
  <h3 class="mt-4 text-lg font-semibold">Title</h3>
  <p class="mt-2 text-gray-600">Description</p>
  <button class="mt-4">Action</button>
</div>
```

---

## Anti-Pattern 7: Font Weight Abuse
```html
<!-- ❌ Bad: everything bold -->
<div>
  <p class="font-bold">Title</p>
  <p class="font-bold text-gray-600">Subtitle</p>
  <p class="font-semibold">Body text</p>
  <span class="font-bold text-xs">Caption</span>
</div>

<!-- ✅ Good: weight = hierarchy signal -->
<div>
  <p class="text-xl font-bold text-gray-950">Title</p>
  <p class="text-base font-medium text-gray-700">Subtitle</p>
  <p class="text-sm font-normal text-gray-600">Body text</p>
  <span class="text-xs text-gray-400">Caption</span>
</div>
```

---

## Anti-Pattern 8: Accidental Content Width
```html
<!-- ❌ Bad: text stretches full width on wide screens -->
<p class="text-base">Very long article text that goes all the way across...</p>

<!-- ✅ Good: max-width for readability -->
<p class="text-base max-w-prose leading-relaxed">Content...</p>
<article class="mx-auto max-w-2xl">
```

---

## Anti-Pattern 9: No States (Hover, Focus, Active, Disabled)
```html
<!-- ❌ Dead button (no states) -->
<button class="bg-blue-500 text-white px-4 py-2">Submit</button>

<!-- ✅ Alive button (all states) -->
<button class="
  bg-blue-600 text-white px-4 py-2 rounded-lg
  hover:bg-blue-700 
  active:bg-blue-800 active:scale-[0.98]
  focus-visible:ring-2 focus-visible:ring-blue-500 focus-visible:ring-offset-2 focus-visible:outline-none
  disabled:opacity-50 disabled:cursor-not-allowed disabled:hover:bg-blue-600
  transition-all duration-150
">Submit</button>
```

---

## Anti-Pattern 10: Placeholder = Label
```html
<!-- ❌ Bad: placeholder only -->
<input placeholder="Email address" class="border p-2 w-full" />

<!-- ✅ Good: label + placeholder -->
<div>
  <label for="email" class="block text-sm font-medium text-gray-700 mb-1">
    Email address
  </label>
  <input 
    id="email" 
    placeholder="you@example.com" 
    class="border border-gray-300 rounded-lg p-2 w-full"
  />
</div>
```

---

## Anti-Pattern 11: Same Size = No Hierarchy
```html
<!-- ❌ Bad: card grid all same visual weight -->
<div class="grid grid-cols-4 gap-4">
  <div class="p-4 bg-white rounded">Revenue: $45K</div>
  <div class="p-4 bg-white rounded">Users: 1,234</div>
  <div class="p-4 bg-white rounded">Orders: 89</div>
  <div class="p-4 bg-white rounded">Refunds: 5</div>
</div>

<!-- ✅ Good: differentiated important metric -->
<div class="grid grid-cols-4 gap-4">
  <div class="col-span-2 p-6 bg-blue-600 text-white rounded-xl">
    <p class="text-sm opacity-80">Revenue</p>
    <p class="text-4xl font-bold">$45K</p>
  </div>
  <div class="p-4 bg-white rounded-xl border"><SmallMetric /></div>
  <div class="p-4 bg-white rounded-xl border"><SmallMetric /></div>
</div>
```

---

## Anti-Pattern 12: Table Without Context
```html
<!-- ❌ Bad: raw table, no header, no actions, no pagination info -->
<table>...</table>

<!-- ✅ Good: table with context -->
<div>
  <div class="flex justify-between mb-4">
    <h3>Recent Orders</h3>
    <Button>Export CSV</Button>
  </div>
  <table>...</table>
  <div class="flex justify-between mt-4">
    <p class="text-sm text-gray-500">Showing 1-10 of 47</p>
    <Pagination />
  </div>
</div>
```

---

## Top 5 Quick Wins
1. **Increase whitespace** by 2x — almost always better
2. **Darken body text** to gray-700+ (not gray-400)
3. **Remove borders** between similar elements — use bg color
4. **Add font-semibold** to headings (not just larger font)
5. **Add hover + focus states** to ALL interactive elements
