# 12 — Design Systems

> SOURCE: shadcn/ui docs, Radix UI, Material Design 3, Apple HIG, Tailwind v4

---

## Core Principle
Design system = tập hợp decisions được document và shared. Không cần reinvent mỗi component.

---

## Rule 1: shadcn/ui — The Modern Standard

### Philosophy:
- **Own your code** — copy components vào project, không phải dependency
- **Open code** — LLMs can read and modify
- **Composable** — consistent API across all components
- **Beautiful defaults** — looks good out of the box

### Setup (Next.js + Tailwind v4):
```bash
pnpm create next-app my-app --typescript
pnpm dlx shadcn@latest init
pnpm dlx shadcn@latest add button card input label
```

### Directory structure:
```
src/
  components/
    ui/          ← shadcn/ui components (owned, editable)
      button.tsx
      card.tsx
      input.tsx
    features/    ← your custom components
    layout/      ← layout components
```

---

## Rule 2: CSS Variables System (shadcn/ui)

```css
/* globals.css */
@import "tailwindcss";

@theme {
  /* shadcn/ui tokens as Tailwind theme vars */
  --color-background: var(--background);
  --color-foreground: var(--foreground);
  --color-primary: var(--primary);
  --color-primary-foreground: var(--primary-foreground);
  --color-muted: var(--muted);
  --color-muted-foreground: var(--muted-foreground);
  --color-border: var(--border);
  --color-card: var(--card);
  --color-destructive: var(--destructive);
  --radius-sm: var(--radius-sm);
  --radius-md: var(--radius-md);
  --radius-lg: var(--radius-lg);
}

:root {
  --background: oklch(1 0 0);
  --foreground: oklch(0.145 0 0);
  --card: oklch(1 0 0);
  --primary: oklch(0.205 0 0);
  --primary-foreground: oklch(0.985 0 0);
  --secondary: oklch(0.97 0 0);
  --secondary-foreground: oklch(0.205 0 0);
  --muted: oklch(0.961 0 0);
  --muted-foreground: oklch(0.556 0 0);
  --accent: oklch(0.961 0 0);
  --border: oklch(0.922 0 0);
  --input: oklch(0.922 0 0);
  --ring: oklch(0.708 0 0);
  --destructive: oklch(0.577 0.245 27.325);
  --radius-sm: 0.25rem;
  --radius-md: 0.375rem;
  --radius-lg: 0.5rem;
  --radius-xl: 0.75rem;
  --radius-2xl: 1rem;
}

.dark {
  --background: oklch(0.145 0 0);
  --foreground: oklch(0.985 0 0);
  --card: oklch(0.205 0 0);
  --primary: oklch(0.922 0 0);
  --primary-foreground: oklch(0.205 0 0);
  --muted: oklch(0.269 0 0);
  --muted-foreground: oklch(0.708 0 0);
  --border: oklch(1 0 0 / 10%);
  --ring: oklch(0.556 0 0);
}
```

---

## Rule 3: Radix UI Primitives
shadcn/ui is built on Radix UI — unstyled, accessible primitives.

```tsx
// Radix provides:
// ✅ Keyboard navigation
// ✅ Focus management
// ✅ ARIA attributes
// ✅ Composable API

import * as Popover from '@radix-ui/react-popover'
import * as Select from '@radix-ui/react-select'
import * as Tooltip from '@radix-ui/react-tooltip'
import * as AlertDialog from '@radix-ui/react-alert-dialog'
import * as DropdownMenu from '@radix-ui/react-dropdown-menu'
import * as Sheet from '@radix-ui/react-dialog'  // re-exported as Sheet

// Available primitives:
// Accordion, AlertDialog, AspectRatio, Avatar, Checkbox
// Collapsible, ContextMenu, Dialog, DropdownMenu
// Form, HoverCard, Label, Menubar, NavigationMenu
// Popover, Progress, RadioGroup, ScrollArea, Select
// Separator, Slider, Switch, Tabs, Toast, Toggle
// ToggleGroup, Toolbar, Tooltip
```

---

## Rule 4: Material Design 3 Concepts

### Color roles (M3):
```
Primary — main color, key components
On-Primary — text/icons on primary
Primary Container — less prominent, backgrounds
On-Primary Container — text on primary container

Secondary — supporting color
Tertiary — accent color
Error — error states
Surface — backgrounds
Surface Variant — slightly different surface
Outline — borders
```

### M3 Component hierarchy:
- **FAB** (Floating Action Button) — most important action
- **Button** types: Filled > Filled Tonal > Outlined > Text
- **Card** types: Elevated > Filled > Outlined

### M3 Type scale:
```
Display Large: 57sp
Display Medium: 45sp  
Display Small: 36sp
Headline Large: 32sp
Headline Medium: 28sp
Headline Small: 24sp
Title Large: 22sp — Section headers
Title Medium: 16sp — Component titles
Title Small: 14sp
Body Large: 16sp — Primary body
Body Medium: 14sp — Secondary body
Body Small: 12sp — Captions
Label Large: 14sp — Buttons
Label Medium: 12sp — Badges
Label Small: 11sp — Overlines
```

---

## Rule 5: Apple HIG Principles (distilled)

### Core principles:
1. **Clarity** — Text legible at every size, icons precise and lucid
2. **Deference** — UI helps people understand and interact without competing
3. **Depth** — Visual layers and realistic motion convey hierarchy

### Apple design numbers:
- Navigation bar height: 44pt (+ safe area)
- Tab bar height: 49pt (+ safe area)
- Standard margin: 20pt
- Body text: 17pt (San Francisco)
- Corner radius iOS: 10-13pt (modal), 8pt (cell)

### SF Symbols for React Native (expo/vector-icons):
```tsx
import { Ionicons } from '@expo/vector-icons'
// iOS-style icons
<Ionicons name="home" size={22} color={color} />
<Ionicons name="search" size={22} color={color} />
<Ionicons name="notifications" size={22} color={color} />
<Ionicons name="person" size={22} color={color} />
```

---

## Rule 6: Design Tokens
```css
/* Token hierarchy: Global → Semantic → Component */

/* Level 1: Global tokens (raw values) */
@theme {
  --color-blue-500: oklch(0.62 0.214 259.8);
  --spacing-4: 1rem;
  --radius-lg: 0.5rem;
}

/* Level 2: Semantic tokens (purpose) */
@layer base {
  :root {
    --color-action-primary: var(--color-blue-600);
    --color-action-primary-hover: var(--color-blue-700);
    --spacing-component-padding: var(--spacing-4);
  }
}

/* Level 3: Component tokens */
.btn-primary {
  background: var(--color-action-primary);
  padding: var(--spacing-component-padding);
}
```

---

## Rule 7: Component API Patterns
```tsx
// Good component API (shadcn/ui style)
interface ButtonProps extends React.ButtonHTMLAttributes<HTMLButtonElement> {
  variant?: 'default' | 'outline' | 'ghost' | 'destructive' | 'secondary' | 'link'
  size?: 'default' | 'sm' | 'lg' | 'icon'
  asChild?: boolean
  loading?: boolean
}

// asChild pattern (polymorphic)
<Button asChild>
  <Link href="/dashboard">Go to Dashboard</Link>
</Button>

// Compound components
<Card>
  <CardHeader>...</CardHeader>
  <CardContent>...</CardContent>
  <CardFooter>...</CardFooter>
</Card>
```

---

## Rule 8: Class Variance Authority (CVA)
shadcn/ui uses CVA for component variants:
```tsx
import { cva, type VariantProps } from "class-variance-authority"

const buttonVariants = cva(
  // Base classes
  "inline-flex items-center justify-center rounded-md font-medium transition-colors focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-ring disabled:pointer-events-none disabled:opacity-50",
  {
    variants: {
      variant: {
        default: "bg-primary text-primary-foreground hover:bg-primary/90",
        destructive: "bg-destructive text-destructive-foreground hover:bg-destructive/90",
        outline: "border border-input bg-background hover:bg-accent",
        ghost: "hover:bg-accent hover:text-accent-foreground",
      },
      size: {
        default: "h-10 px-4 py-2",
        sm: "h-9 px-3 text-sm",
        lg: "h-11 px-8",
        icon: "size-10",
      },
    },
    defaultVariants: {
      variant: "default",
      size: "default",
    },
  }
)
```

---

## Design System Quick Setup
```bash
# 1. Install shadcn/ui
pnpm dlx shadcn@latest init

# 2. Add core components
pnpm dlx shadcn@latest add button card input label badge \
  dialog sheet tabs select textarea switch checkbox \
  dropdown-menu tooltip popover separator skeleton \
  table pagination alert avatar progress

# 3. Add icons
pnpm add lucide-react

# 4. Add animations
pnpm add motion

# 5. Add notifications  
pnpm add sonner
```
