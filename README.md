# MasterDesignCore — UI/UX Mastery Skill

> Skill để tạo giao diện app siêu đẹp, mượt cho cả web và mobile.
> **Version:** 1.0 | **Updated:** 2025-03 | **Platform:** Next.js + React Native/Expo

---

## 🎯 Trigger
Khi cần:
- Tạo UI/UX cho web app (Next.js, React)
- Tạo mobile app (React Native, Expo)
- Review hoặc cải thiện UI hiện có
- Chọn components, layouts, colors, typography
- Implement animations hoặc micro-interactions

---

## 🚀 Quick Start

```
1. Đọc SKILL.md này (file này)
2. Chọn platform: web / mobile / both
3. Follow Design System Setup bên dưới
4. Apply rules từ references/
5. Chạy checklist trước khi ship
```

---

## ⚡ Core Rules (PHẢI NHỚ — 30 rules vàng)

### Visual Hierarchy
1. **Hierarchy first** — Mọi thứ phải rõ quan trọng hơn cái gì. Text lớn + đậm + tối = quan trọng hơn.
2. **Max 3 focal points** per page. Mắt người không biết nhìn đâu khi có 10 thứ "quan trọng".
3. **Primary CTA = most visually prominent element** on the page. Không được lẫn với secondary actions.

### Color
4. **60-30-10 rule**: 60% neutral, 30% secondary, 10% accent. Không rainbow.
5. **Never use pure black** (#000). Dùng `gray-950` hoặc `gray-900`.
6. **Contrast ≥ 4.5:1** cho normal text, ≥ 3:1 cho large text và UI components.
7. **Semantic colors**: success = green, error = red, warning = yellow, info = blue. Consistent everywhere.

### Typography
8. **Body text ≥ 16px**, `leading-relaxed` (1.6). Không bao giờ < 14px trong production.
9. **Heading: `leading-tight` + `tracking-tight`**. Body: `leading-relaxed`.
10. **Max-width prose**: `max-w-prose` (65ch) cho article/readable content.
11. **Font hierarchy**: Bold (700) heading → Semibold (600) subtitle → Regular (400) body → Light (300) NEVER in body.

### Spacing
12. **4pt/8pt grid** — mọi spacing phải là bội số 4px. Tailwind scale là perfect.
13. **Generous whitespace** — khi nghi ngờ, thêm padding/margin. Hầu hết UIs quá cramped.
14. **Related items gần, unrelated items xa** — Gestalt proximity.

### Components
15. **Every interactive element có đủ states**: hover, active, focus-visible, disabled, loading.
16. **Focus styles KHÔNG BAO GIỜ bị xóa**. `outline: none` mà không có replacement là A11y bug.
17. **Touch targets ≥ 44px** trên mobile (cả web mobile và React Native).
18. **Loading/Empty/Error states** phải có cho mọi async content.

### Dark Mode
19. **Dark ≠ invert**. Background: `gray-950`. Surface: `gray-900`. Card: `gray-800`. Text: `gray-50`.
20. **Elevation = lighter bg** trong dark mode (không phải darker shadow).
21. Mọi màu cần `dark:` variant. Không hardcode hex.

### Animation
22. **Animate only transform + opacity** (GPU accelerated). Không animate width/height/left/top.
23. **Duration**: hover = 150ms, feedback = 200ms, transitions = 300ms, entrances = 400-500ms.
24. **Spring physics cho interactive** (buttons, toggles). Tween cho page transitions.
25. **Respect `prefers-reduced-motion`** — dùng `useReducedMotion()` từ Motion.

### Responsive
26. **Mobile-first**: Base styles = mobile. Thêm `md:` `lg:` cho larger screens.
27. `sm:` prefix KHÔNG phải "small screens" — nó là "≥640px". Mobile = no prefix.
28. **Bottom nav trên mobile**, sidebar chỉ show từ `md:` trở lên.

### Accessibility
29. **Semantic HTML first** — `<button>` cho actions, `<a>` cho links, heading levels đúng.
30. **Color không phải signal duy nhất** — luôn thêm icon/text với màu.

---

## 🛠️ Design System Setup

### Web (Next.js + Tailwind v4 + shadcn/ui)
```bash
# 1. Tạo project
pnpm create next-app my-app --typescript

# 2. shadcn/ui (tự setup Tailwind v4)
pnpm dlx shadcn@latest init

# 3. Core components
pnpm dlx shadcn@latest add button card input label badge \
  dialog sheet alert-dialog \
  dropdown-menu tooltip \
  tabs separator skeleton

# 4. Icons
pnpm add lucide-react

# 5. Animations
pnpm add motion

# 6. Notifications
pnpm add sonner

# 7. Forms (optional but recommended)
pnpm add react-hook-form @hookform/resolvers zod
```

### Mobile (Expo + NativeWind)
```bash
# Create Expo app
pnpm create expo-app my-app --template

# NativeWind (Tailwind for React Native)
pnpm add nativewind
pnpm add -D tailwindcss

# Navigation
pnpm add expo-router

# Gestures
pnpm add react-native-gesture-handler react-native-reanimated

# Safe area
pnpm add react-native-safe-area-context

# Icons  
pnpm add @expo/vector-icons
# Or:
pnpm add lucide-react-native
```

---

## 🎨 Color System
→ Xem: `references/01-color-theory.md`

**Quick reference:**
```css
/* Light mode palette */
background: white / gray-50
surface: white / gray-50
border: gray-200
text-primary: gray-950
text-body: gray-700
text-muted: gray-500
primary: blue-600  (or brand color)
success: green-600
error: red-600
warning: amber-600

/* Dark mode shifts */
background → gray-950
surface → gray-900
border → gray-800
text-primary → gray-50
primary → blue-400 (lighter, less saturated)
```

---

## ✍️ Typography
→ Xem: `references/02-typography.md`

**Quick reference:**
```html
Display: text-5xl/6xl/7xl font-bold tracking-tighter
H1: text-4xl font-bold tracking-tight
H2: text-2xl/3xl font-semibold
H3: text-xl font-semibold
Body: text-base leading-relaxed
Small: text-sm
Caption: text-xs text-gray-500
Label: text-sm font-medium
```

**Recommended font:** Inter (`pnpm add @fontsource/inter` or Google Fonts)

---

## 📐 Spacing & Layout
→ Xem: `references/03-spacing-layout.md`

**Quick reference:**
```
Component padding: p-4 (16px) default, p-6 (24px) cards, p-8 (32px) sections
Section padding: py-12 sm:py-16 lg:py-24
Container: max-w-7xl mx-auto px-4 sm:px-6 lg:px-8
Content max-width: max-w-2xl (articles), max-w-4xl (wide), max-w-7xl (app)
Gap: gap-4 (default), gap-6 (sections), gap-8 (large sections)
```

---

## 🔲 Components
→ Xem: `references/04-components.md`

**Go-to components:** Button, Card, Input, Select, Dialog, Badge, Table, Toast (Sonner)

**shadcn/ui is the default**. Custom components chỉ khi shadcn không có.

---

## 🌊 Animation
→ Xem: `references/05-animation.md`
→ Code: `examples/animation-recipes.md`

**Quick patterns:**
```tsx
// Fade in on mount
initial={{ opacity: 0, y: 20 }} animate={{ opacity: 1, y: 0 }}

// Scroll-triggered
whileInView={{ opacity: 1 }} viewport={{ once: true }}

// Button press
whileHover={{ scale: 1.02 }} whileTap={{ scale: 0.97 }}

// Modal/overlay
initial={{ opacity: 0, scale: 0.95 }} animate={{ opacity: 1, scale: 1 }}
```

---

## 🌙 Dark Mode
→ Xem: `references/08-dark-mode.md`

**Setup:**
```css
@custom-variant dark (&:where(.dark, .dark *));
```
```js
// Toggle (in <head> to avoid FOUC)
document.documentElement.classList.toggle('dark', isDark)
```

---

## ♿ Accessibility
→ Xem: `references/09-accessibility.md`
→ Checklist: `checklists/accessibility-review.md`

**Minimum viable A11y:**
- `alt=""` on images
- `aria-label` on icon buttons
- Visible focus rings
- Semantic HTML
- Contrast ≥ 4.5:1

---

## 📱 Platform-Specific

### Web (Next.js)
```
Primary nav: Sidebar (desktop) + Top bar (mobile)
Breakpoints: sm(640) md(768) lg(1024) xl(1280) 2xl(1536)
Container: max-w-7xl
Cards: rounded-xl border shadow-sm
Inputs: rounded-lg, h-10
Buttons: rounded-lg, h-10 (default)
```

### Mobile (React Native / Expo)
```
Primary nav: Bottom tab bar (max 5 tabs)
Touch target: min 44px height
Safe area: useSafeAreaInsets()
Long lists: FlatList (not map in ScrollView)
Modals: Bottom sheet (gorhom/bottom-sheet)
Fonts: System font (SF Pro iOS / Roboto Android)
```

---

## ✅ Checklists

| Scenario | Checklist |
|----------|-----------|
| Shipping a page | `checklists/page-review.md` |
| Shipping a component | `checklists/component-review.md` |
| Mobile app | `checklists/mobile-review.md` |
| A11y audit | `checklists/accessibility-review.md` |

---

## 💻 Code Recipes

| Topic | File |
|-------|------|
| Tailwind patterns (colors, cards, buttons, layout) | `examples/tailwind-recipes.md` |
| shadcn/ui components (forms, dialogs, commands) | `examples/shadcn-recipes.md` |
| Motion animations (modal, scroll, stagger, gestures) | `examples/animation-recipes.md` |
| Full page layouts (dashboard, auth, landing, settings) | `examples/layout-templates.md` |

---

## 📚 Reference Library

| Topic | File |
|-------|------|
| Color theory, palettes, contrast | `references/01-color-theory.md` |
| Typography scale, font pairing | `references/02-typography.md` |
| Spacing, grid, layout | `references/03-spacing-layout.md` |
| Component design patterns | `references/04-components.md` |
| Motion design, animations | `references/05-animation.md` |
| iOS HIG + Material mobile patterns | `references/06-mobile-patterns.md` |
| Web UI best practices | `references/07-web-patterns.md` |
| Dark mode design rules | `references/08-dark-mode.md` |
| A11y essentials | `references/09-accessibility.md` |
| UI anti-patterns (avoid!) | `references/10-anti-patterns.md` |
| Beautiful app analysis | `references/11-app-analysis.md` |
| shadcn/ui, Radix, Material | `references/12-design-systems.md` |
| Responsive design mastery | `references/13-responsive.md` |
| Form design best practices | `references/14-forms-inputs.md` |
| Tables, charts, dashboards | `references/15-data-display.md` |
| Icons, avatars, imagery | `references/16-icons-imagery.md` |

---

## 🚨 Anti-Patterns (ĐỪNG làm)

1. **No visual hierarchy** — mọi text cùng size/weight/color
2. **Too many colors** — quá 3 brand colors là too much
3. **Cramped spacing** — no breathing room
4. **Low contrast text** — gray-400 on white = fail
5. **Borders everywhere** — dùng bg color difference thay thế
6. **No states** — button không có hover/focus/disabled
7. **No loading/empty states** — blank content area confuses users
8. **Placeholder = label** — không bao giờ dùng placeholder thay label
9. **Hamburger menu on mobile** — dùng bottom tab bar
10. **No dark mode** — 2025 dark mode là requirement, không optional

---

## 🎯 Mental Model

Khi nhìn vào một UI, ask:
1. "Mắt tôi đi đâu đầu tiên?" → Primary action phải rõ nhất
2. "Tôi có thể đọc tất cả text không?" → Contrast check
3. "Nếu keyboard-only, tôi có dùng được không?" → A11y
4. "Trên điện thoại, tôi có cần zoom không?" → Responsive
5. "Sau 5 giây, tôi biết trang này là về gì chưa?" → Clarity

---

*MasterDesignCore v1.0 — Research-based, production-tested, AI-optimized.*
*Sources: Material Design 3, Apple HIG, Tailwind CSS v4, shadcn/ui, Motion, WCAG 2.1, Refactoring UI*
