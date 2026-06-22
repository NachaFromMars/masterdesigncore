# 16 — Icons & Imagery

> SOURCE: Lucide React, icon design guidelines, imagery principles

---

## Core Principle
Icons nói thay lời. Nhưng icons không rõ ràng = worse than text. Always pair with text when ambiguous.

---

## Rule 1: Icon Library (Lucide React — recommended)
```bash
pnpm add lucide-react
```

```tsx
// Import only what you need (tree-shaking)
import { 
  Home, Search, Bell, Settings, User, 
  Plus, Minus, X, Check, ChevronRight, ChevronDown,
  ArrowRight, ArrowLeft, Upload, Download,
  Edit, Trash2, Copy, Eye, EyeOff,
  Star, Heart, Bookmark, Share2,
  Mail, Phone, Globe, Lock, Unlock,
  BarChart2, TrendingUp, Activity,
  AlertCircle, AlertTriangle, Info, CheckCircle,
  Loader2, RefreshCw, Zap
} from 'lucide-react'

// Usage
<Search className="size-4" />
<Search className="size-5 text-gray-400" />
<Search className="size-6 stroke-2" />
```

---

## Rule 2: Icon Sizes
```html
<!-- Size system -->
size-3   = 12px — Very small (badge indicator)
size-4   = 16px — Small (inline text, input addons, table)
size-5   = 20px — Default (buttons, nav items)
size-6   = 24px — Medium (feature icons, empty states)
size-8   = 32px — Large (section icons)
size-10  = 40px — Hero icons
size-12  = 48px — Feature highlights
size-16  = 64px — Empty state illustrations

<!-- Icon in button: match text size -->
<Button size="sm">  <!-- text-sm = 14px → icon size-4 -->
  <Plus className="size-4 mr-1.5" />
  Add item
</Button>

<Button>  <!-- default = 16px → icon size-4 -->
  <Upload className="size-4 mr-2" />
  Upload
</Button>

<Button size="lg">  <!-- large = 18px → icon size-5 -->
  <Download className="size-5 mr-2" />
  Download all
</Button>
```

---

## Rule 3: Icon Colors
```html
<!-- Interactive icon: inherit from parent text -->
<button class="text-gray-600 hover:text-gray-900">
  <Settings class="size-5" /> <!-- inherits color -->
</button>

<!-- Semantic icon colors -->
<AlertCircle class="size-4 text-red-500" />    <!-- Error -->
<CheckCircle class="size-4 text-green-500" />  <!-- Success -->
<AlertTriangle class="size-4 text-yellow-500" /> <!-- Warning -->
<Info class="size-4 text-blue-500" />          <!-- Info -->

<!-- Icon in colored container -->
<div class="rounded-lg bg-blue-100 dark:bg-blue-950/30 p-2">
  <Mail class="size-4 text-blue-600 dark:text-blue-400" />
</div>

<!-- Muted supporting icon -->
<div class="flex items-center gap-2 text-gray-400">
  <MapPin class="size-3.5" />
  <span class="text-sm">San Francisco, CA</span>
</div>
```

---

## Rule 4: Icon + Text Alignment
```html
<!-- Always vertically center icon with text -->
<span class="flex items-center gap-2">
  <Check class="size-4 text-green-500" />
  Feature included
</span>

<!-- Inline icon in text (use current color) -->
<p>
  Click <kbd class="inline-flex items-center gap-1 px-1.5 py-0.5 text-xs border rounded">
    <Command class="size-3" /> K
  </kbd> to open
</p>

<!-- Navigation with active state -->
<a class="flex items-center gap-3 rounded-lg px-3 py-2">
  <BarChart2 class="size-4 flex-shrink-0 text-gray-400" />
  <span class="text-sm font-medium">Analytics</span>
</a>
```

---

## Rule 5: Loading & State Icons
```tsx
// Spinning loader
<Loader2 className="size-4 animate-spin text-blue-600" />

// Loading button
<Button disabled>
  <Loader2 className="size-4 mr-2 animate-spin" />
  Saving...
</Button>

// Pulse for skeleton (use animate-pulse on container)
<div className="animate-pulse flex items-center gap-3">
  <div className="size-10 rounded-full bg-gray-200" />
  <div className="flex-1 space-y-2">
    <div className="h-4 bg-gray-200 rounded w-3/4" />
    <div className="h-3 bg-gray-200 rounded w-1/2" />
  </div>
</div>

// Success/error transition
<AnimatePresence mode="wait">
  {status === 'loading' && <motion.div key="load"><Loader2 className="animate-spin" /></motion.div>}
  {status === 'success' && <motion.div key="ok" initial={{ scale: 0 }} animate={{ scale: 1 }}><Check /></motion.div>}
  {status === 'error' && <motion.div key="err"><X className="text-red-500" /></motion.div>}
</AnimatePresence>
```

---

## Rule 6: Avatar System
```html
<!-- Avatar sizes -->
<img class="size-6 rounded-full" />   <!-- Tiny (comment threads) -->
<img class="size-8 rounded-full" />   <!-- Small (tables, lists) -->
<img class="size-10 rounded-full" />  <!-- Default (nav, cards) -->
<img class="size-12 rounded-full" />  <!-- Medium (profile) -->
<img class="size-16 rounded-full" />  <!-- Large (profile header) -->

<!-- Avatar with fallback initials -->
<div class="size-10 rounded-full bg-blue-100 dark:bg-blue-900 flex items-center justify-center">
  <span class="text-sm font-semibold text-blue-600 dark:text-blue-300">JD</span>
</div>

<!-- Avatar group (stacked) -->
<div class="flex -space-x-2">
  {users.slice(0, 5).map(user => (
    <img key={user.id} class="size-8 rounded-full border-2 border-white dark:border-gray-900 object-cover" />
  ))}
  {users.length > 5 && (
    <div class="size-8 rounded-full border-2 border-white dark:border-gray-900 bg-gray-100 dark:bg-gray-800 flex items-center justify-center">
      <span class="text-xs font-medium text-gray-600">+{users.length - 5}</span>
    </div>
  )}
</div>
```

---

## Rule 7: Images & Thumbnails
```html
<!-- Responsive image with aspect ratio -->
<div class="aspect-video w-full overflow-hidden rounded-lg">
  <img class="w-full h-full object-cover hover:scale-105 transition-transform duration-300" />
</div>

<!-- Card thumbnail -->
<div class="aspect-[4/3] overflow-hidden rounded-t-lg">
  <img class="w-full h-full object-cover" />
</div>

<!-- Profile cover image -->
<div class="h-32 sm:h-48 overflow-hidden rounded-xl">
  <img class="w-full h-full object-cover object-center" />
</div>

<!-- Background image (hero) -->
<div class="relative h-[60vh]">
  <img class="absolute inset-0 w-full h-full object-cover" />
  <div class="absolute inset-0 bg-gradient-to-b from-transparent to-black/60" />
  <div class="relative z-10 p-8 text-white">...</div>
</div>
```

---

## Rule 8: Favicon & App Icons
```html
<!-- Next.js favicon (app/icon.tsx) -->
export const size = { width: 32, height: 32 }
export const contentType = 'image/png'

export default function Icon() {
  return new ImageResponse(
    <div style={{ fontSize: 24, background: '#3b82f6', borderRadius: 8,
      width: '100%', height: '100%', display: 'flex', alignItems: 'center', justifyContent: 'center' }}>
      ⚡
    </div>
  )
}
```

---

## Illustration Sources
- **Undraw** (undraw.co) — Free SVG illustrations, customizable colors
- **Storyset** (storyset.com) — Animated illustrations
- **Lucide** — Icons as illustrations (enlarge, colorize)
- **Heroicons** (heroicons.com) — Tailwind team icons
- **Phosphor Icons** (phosphoricons.com) — Multiple weights
- **Tabler Icons** (tabler.io/icons) — 5000+ icons

---

## Anti-Patterns 🚫
- ❌ Icon-only actions without aria-label or tooltip
- ❌ Mixing icon styles (outline + filled + flat)
- ❌ Icons larger than 24px inside buttons
- ❌ Images without alt text
- ❌ Pixelated images (serve 2x for retina)
- ❌ Stock photos that look obviously fake
- ❌ Decorative images with alt text (use alt="")
- ❌ Animate every icon (motion should be intentional)
