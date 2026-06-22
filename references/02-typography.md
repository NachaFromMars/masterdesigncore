# 02 — Typography

> SOURCE: Tailwind CSS v4 font-size docs, Apple HIG Typography, Refactoring UI, Google Fonts

---

## Core Principle
Typography là 90% của design. Nếu type hierarchy đúng → UI trông professional dù màu sắc bình thường.

---

## Rule 1: Type Scale cố định (không invent sizes)
**Tailwind v4 scale:**

| Class | Size | Line-height | Use case |
|-------|------|-------------|----------|
| `text-xs` | 12px | 1.33 | Captions, badges, timestamps |
| `text-sm` | 14px | 1.43 | Body small, labels, helper text |
| `text-base` | 16px | 1.5 | Body text |
| `text-lg` | 18px | 1.56 | Subheadings, lead text |
| `text-xl` | 20px | 1.4 | Section titles |
| `text-2xl` | 24px | 1.33 | H3 |
| `text-3xl` | 30px | 1.2 | H2 |
| `text-4xl` | 36px | 1.11 | H1 |
| `text-5xl` | 48px | 1.0 | Display headings |

**Anti-pattern:** Custom sizes mỗi element (text-[15px], text-[17px]) → không consistent.

---

## Rule 2: Font Hierarchy (Weight + Size + Color)
```html
<!-- H1: Large + Bold -->
<h1 class="text-4xl font-bold text-gray-950 tracking-tight">
  Page Title
</h1>

<!-- H2: Medium-large + Semibold -->
<h2 class="text-2xl font-semibold text-gray-900">
  Section Title
</h2>

<!-- Body: Base + Normal -->
<p class="text-base text-gray-700 leading-relaxed">
  Body text content
</p>

<!-- Caption: Small + Muted -->
<span class="text-sm text-gray-500">
  Helper text
</span>

<!-- Label: Small + Medium -->
<label class="text-sm font-medium text-gray-700">
  Input Label
</label>
```

---

## Rule 3: Font Pairing Recipes

**Option A: Inter (Universal Pro)**
```css
/* globals.css */
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap');

@theme {
  --font-sans: 'Inter', system-ui, sans-serif;
}
```
→ Clean, modern, excellent legibility. Works for everything.

**Option B: Geist (Vercel/Next.js)**
```js
// Next.js app
import { Geist } from 'next/font/google'
const geist = Geist({ subsets: ['latin'] })
```

**Option C: System fonts (fastest)**
```css
@theme {
  --font-sans: ui-sans-serif, system-ui, -apple-system, BlinkMacSystemFont, sans-serif;
  --font-mono: ui-monospace, 'Cascadia Code', Menlo, monospace;
}
```

**Display + Body Pairing:**
- `Playfair Display` (serif) + `Inter` (sans) → Editorial
- `Space Grotesk` + `Inter` → Tech/SaaS
- `Cabinet Grotesk` + `Satoshi` → Modern startup

---

## Rule 4: Line-height & Spacing
```html
<!-- Body text: relaxed spacing -->
<p class="text-base leading-relaxed">  <!-- 1.625 -->

<!-- Headings: tight spacing -->
<h1 class="text-4xl leading-tight">   <!-- 1.25 -->

<!-- Monospace: normal -->
<code class="text-sm leading-normal"> <!-- 1.5 -->
```

**Golden rule:** Body text cần `leading-relaxed` (1.6-1.7). Headings cần `leading-tight` (1.1-1.25).

---

## Rule 5: Letter Spacing
```html
<!-- Headings: slightly tight -->
<h1 class="tracking-tight">          <!-- -0.025em -->

<!-- All-caps labels: wide -->
<span class="text-xs uppercase tracking-widest font-medium text-gray-500">
  CATEGORY
</span>

<!-- Large display: very tight -->
<h1 class="text-6xl tracking-tighter font-black">
```

---

## Rule 6: Font Smoothing (macOS/iOS)
```html
<!-- Apply globally via Tailwind antialiased -->
<body class="antialiased">
```
Renders text with `-webkit-font-smoothing: antialiased` → thinner, crisper on retina.

---

## Rule 7: Readable Line Length (Measure)
- **Optimal:** 45-75 characters per line
- **Tailwind:** `max-w-prose` = 65ch (perfect)

```html
<article class="max-w-prose mx-auto text-base leading-relaxed text-gray-700">
  Article content...
</article>
```

---

## Rule 8: Text Color Hierarchy
Dùng opacity levels thay vì nhiều màu khác nhau:
```html
<h2 class="text-gray-950">Primary heading</h2>
<p class="text-gray-700">Body text</p>
<span class="text-gray-500">Secondary text</span>
<small class="text-gray-400">Disabled/placeholder</small>
```

---

## Anti-Patterns 🚫
- ❌ Quá nhiều font weights trong 1 page (max 3)
- ❌ Text-justify trên web → uneven letter spacing
- ❌ Uppercase full body text
- ❌ Font size < 12px trong production
- ❌ Colored text trên colored bg (kiểm tra contrast!)
- ❌ Centered text cho paragraphs > 2 lines
- ❌ Line height = 1 cho body text (quá tight)
