# 01 — Color Theory & Systems

> SOURCE: Tailwind CSS v4 docs, Material Design 3, Apple HIG, Refactoring UI principles

---

## Core Principle
Color có 3 mục đích: **Hierarchy** (nhấn mạnh), **Meaning** (semantic), **Mood** (cảm xúc). Đừng dùng quá 3 màu chính.

---

## Rule 1: Dùng Palette có Scale đầy đủ (50-950)
**Why:** Scale rộng giúp tạo variations tự nhiên (hover, active, disabled, bg, border, text) mà không cần tính tay.

**Tailwind v4 approach:**
```css
/* Define custom brand color */
@theme {
  --color-brand-50: oklch(0.97 0.02 250);
  --color-brand-100: oklch(0.93 0.04 250);
  --color-brand-500: oklch(0.55 0.15 250);
  --color-brand-900: oklch(0.20 0.06 250);
}
```

**Usage:** `bg-brand-500`, `text-brand-100`, `border-brand-200`

**Anti-pattern:** Dùng 1 màu hex hardcode khắp nơi → không consistent, không responsive.

---

## Rule 2: Semantic Color Roles (không hardcode màu cụ thể)
**Why:** Dễ switch theme, dark mode, accessible.

| Role | Light | Dark | Usage |
|------|-------|------|-------|
| `background` | gray-50 | gray-950 | Page bg |
| `surface` | white | gray-900 | Cards, panels |
| `muted` | gray-100 | gray-800 | Subtle bg |
| `border` | gray-200 | gray-700 | Dividers |
| `text-primary` | gray-950 | gray-50 | Main text |
| `text-muted` | gray-500 | gray-400 | Secondary text |
| `primary` | brand-600 | brand-400 | CTAs |
| `destructive` | red-600 | red-400 | Errors |
| `success` | green-600 | green-400 | Confirmations |

**shadcn/ui CSS variables:**
```css
:root {
  --background: oklch(1 0 0);
  --foreground: oklch(0.145 0 0);
  --primary: oklch(0.205 0 0);
  --primary-foreground: oklch(0.985 0 0);
  --muted: oklch(0.961 0 0);
  --muted-foreground: oklch(0.556 0 0);
  --border: oklch(0.922 0 0);
  --destructive: oklch(0.577 0.245 27.325);
}
```

---

## Rule 3: 60-30-10 Ratio
- **60%** Neutral/Background — gray shades
- **30%** Secondary — muted variants, surfaces
- **10%** Accent/Primary — CTA, highlight

**Anti-pattern:** Trang quá nhiều màu → visually noisy, unprofessional.

---

## Rule 4: Contrast Ratio (WCAG)
- Normal text: **≥ 4.5:1** (AA), **≥ 7:1** (AAA)
- Large text (18px+ bold): **≥ 3:1**
- UI components: **≥ 3:1**

**Quick test:** white text on blue-500 → OK. white text on blue-300 → FAIL.

```html
<!-- Good: high contrast -->
<button class="bg-blue-600 text-white">Submit</button>

<!-- Bad: low contrast -->
<button class="bg-blue-300 text-white">Submit</button>

<!-- Good dark mode -->
<div class="bg-gray-950 text-gray-50 dark:bg-gray-950 dark:text-gray-50">
```

---

## Rule 5: Hue Shifts trong Scale
Tailwind v4 dùng **OKLCH** — perceptually uniform. Khi tạo custom palette, giữ lightness gradient đều, adjust chroma và hue nhẹ ở extremes.

```css
@theme {
  /* OKLCH: L C H */
  --color-violet-50:  oklch(0.969 0.016 293.756);
  --color-violet-500: oklch(0.606 0.25  292.717);
  --color-violet-950: oklch(0.221 0.091 295.815);
}
```

---

## Rule 6: Opacity cho Overlays (không tạo màu mới)
```html
<!-- Overlay button -->
<button class="bg-black/20 hover:bg-black/30 text-white">
<!-- Subtle border -->
<div class="border border-gray-950/10 dark:border-white/10">
<!-- Shadow color -->
<div class="shadow-lg shadow-blue-500/25">
```

---

## Color Combos đẹp (proven palettes)
| Style | Background | Accent | Text |
|-------|-----------|--------|------|
| Minimal | gray-50 | indigo-600 | gray-900 |
| Dark Pro | gray-950 | violet-500 | gray-100 |
| Warm | stone-50 | amber-600 | stone-900 |
| Teal Modern | slate-50 | teal-600 | slate-900 |
| Purple Dark | zinc-950 | purple-500 | zinc-100 |

---

## Anti-Patterns 🚫
- ❌ Rainbow interfaces — quá nhiều màu, loạn mắt
- ❌ Pure black (#000000) — dùng gray-950 thay thế
- ❌ Pure white background + colored text dày đặc
- ❌ Red/green only cho success/error (colorblind issue)
- ❌ Saturated colors làm background chính
- ❌ Quá nhạt → không đủ contrast, mờ nhạt
