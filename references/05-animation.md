# 05 — Animation & Motion Design

> SOURCE: Motion (Framer Motion v12) docs, motion.dev, micro-interaction principles

---

## Core Principle
Animation có mục đích: **Feedback**, **Transition** (spatial context), **Delight**. Không phải show-off.
> "Animation should feel earned, not gratuitous." — Motion team

---

## Rule 1: Motion Hierarchy
1. **Instant (0ms):** Trạng thái boolean (checked/unchecked indicators)
2. **Fast (100-150ms):** Hover states, tooltips, button press feedback
3. **Medium (200-300ms):** Expand/collapse, dropdowns, modals
4. **Slow (400-600ms):** Page transitions, hero entrances
5. **Very slow (>600ms):** Only for decorative/ambient animations

---

## Rule 2: Import & Setup
```tsx
import { motion, AnimatePresence, MotionConfig } from "motion/react"
// Package name: motion (previously framer-motion)

// Wrap app with MotionConfig for global defaults
<MotionConfig transition={{ duration: 0.3, ease: "easeOut" }}>
  <App />
</MotionConfig>
```

---

## Rule 3: Basic Animations
```tsx
// Fade in on mount
<motion.div
  initial={{ opacity: 0 }}
  animate={{ opacity: 1 }}
  transition={{ duration: 0.3 }}
/>

// Slide up + fade
<motion.div
  initial={{ opacity: 0, y: 20 }}
  animate={{ opacity: 1, y: 0 }}
  transition={{ duration: 0.4, ease: "easeOut" }}
/>

// Scale in (modal, popup)
<motion.div
  initial={{ opacity: 0, scale: 0.95 }}
  animate={{ opacity: 1, scale: 1 }}
  exit={{ opacity: 0, scale: 0.95 }}
  transition={{ duration: 0.2 }}
/>
```

---

## Rule 4: Gesture Animations (Interactive Feel)
```tsx
// Button press feedback
<motion.button
  whileHover={{ scale: 1.02 }}
  whileTap={{ scale: 0.97 }}
  transition={{ type: "spring", stiffness: 400, damping: 25 }}
>
  Submit
</motion.button>

// Card hover lift
<motion.div
  className="cursor-pointer"
  whileHover={{ y: -4, boxShadow: "0 20px 40px rgba(0,0,0,0.12)" }}
  transition={{ duration: 0.2 }}
>

// Icon rotation
<motion.div whileHover={{ rotate: 15 }}>
  <StarIcon />
</motion.div>
```

---

## Rule 5: AnimatePresence (Enter/Exit)
```tsx
// Modal with exit animation
<AnimatePresence>
  {isOpen && (
    <motion.div
      key="modal"
      initial={{ opacity: 0, scale: 0.95, y: 10 }}
      animate={{ opacity: 1, scale: 1, y: 0 }}
      exit={{ opacity: 0, scale: 0.95, y: 10 }}
      transition={{ duration: 0.2, ease: "easeOut" }}
    >
      <Modal />
    </motion.div>
  )}
</AnimatePresence>

// List items
<AnimatePresence>
  {items.map(item => (
    <motion.li
      key={item.id}
      layout
      initial={{ opacity: 0, x: -20 }}
      animate={{ opacity: 1, x: 0 }}
      exit={{ opacity: 0, x: 20 }}
      transition={{ duration: 0.2 }}
    />
  ))}
</AnimatePresence>
```

---

## Rule 6: Stagger Children
```tsx
const containerVariants = {
  hidden: { opacity: 0 },
  visible: {
    opacity: 1,
    transition: {
      staggerChildren: 0.08,  // delay between each child
      delayChildren: 0.1,     // delay before first child
    }
  }
}

const itemVariants = {
  hidden: { opacity: 0, y: 20 },
  visible: { opacity: 1, y: 0, transition: { duration: 0.4 } }
}

// Usage
<motion.ul variants={containerVariants} initial="hidden" animate="visible">
  {items.map(item => (
    <motion.li key={item.id} variants={itemVariants}>
      {item.name}
    </motion.li>
  ))}
</motion.ul>
```

---

## Rule 7: Scroll Animations
```tsx
// Fade in when scrolled into view
<motion.div
  initial={{ opacity: 0, y: 40 }}
  whileInView={{ opacity: 1, y: 0 }}
  viewport={{ once: true, margin: "-100px" }}
  transition={{ duration: 0.5, ease: "easeOut" }}
/>

// Scroll-linked parallax
import { useScroll, useTransform } from "motion/react"

function ParallaxSection() {
  const { scrollY } = useScroll()
  const y = useTransform(scrollY, [0, 500], [0, -150])
  
  return <motion.div style={{ y }}>Parallax content</motion.div>
}
```

---

## Rule 8: Transition Types
```tsx
// Spring (feels physical, responsive)
transition={{ type: "spring", stiffness: 300, damping: 30 }}

// Tween with custom easing
transition={{ duration: 0.3, ease: [0.4, 0, 0.2, 1] }}  // Material easing

// Bounce spring (fun interactions)
transition={{ type: "spring", stiffness: 400, damping: 15, bounce: 0.4 }}

// No animation (instant)
transition={{ duration: 0 }}
```

**Named easings:**
- `"easeOut"` — Snappy, feels fast: most UI animations
- `"easeInOut"` — Smooth: page transitions
- `"linear"` — Consistent: progress bars, rotations
- `[0.4, 0, 0.2, 1]` — Material Design standard easing

---

## Rule 9: Layout Animations
```tsx
// Animate layout changes automatically
<motion.div layout>
  {isExpanded ? <FullContent /> : <Preview />}
</motion.div>

// Shared element transitions
<motion.img
  layoutId="hero-image"
  src={img}
/>
// In another component with same layoutId → smooth transition!
```

---

## Rule 10: Performance Best Practices
```tsx
// Only animate transform + opacity (GPU accelerated)
// GOOD:
animate={{ x: 100, opacity: 0 }}

// BAD (triggers layout/repaint):
animate={{ left: 100, width: 200 }}

// For background-color etc, add willChange:
<motion.div style={{ willChange: "transform, opacity" }}>

// Reduce motion for accessibility
import { useReducedMotion } from "motion/react"

function Component() {
  const shouldReduceMotion = useReducedMotion()
  return (
    <motion.div
      animate={{ scale: shouldReduceMotion ? 1 : 1.1 }}
    />
  )
}
```

---

## Micro-Interaction Recipes
```tsx
// Like button bounce
<motion.button
  onClick={() => setLiked(!liked)}
  animate={liked ? { scale: [1, 1.4, 1] } : {}}
  transition={{ duration: 0.3 }}
>
  {liked ? "❤️" : "🤍"}
</motion.button>

// Toggle switch
<motion.div
  className="w-12 h-6 rounded-full"
  style={{ background: isOn ? "#3b82f6" : "#e5e7eb" }}
  animate={{ background: isOn ? "#3b82f6" : "#e5e7eb" }}
>
  <motion.div
    className="w-5 h-5 bg-white rounded-full m-0.5"
    animate={{ x: isOn ? 24 : 0 }}
    transition={{ type: "spring", stiffness: 500, damping: 35 }}
  />
</motion.div>
```

---

## Anti-Patterns 🚫
- ❌ Animate on EVERY element → epileptic, distracting
- ❌ Duration > 500ms cho UI feedback → feels slow/laggy
- ❌ Animate width/height instead of transform (layout thrashing)
- ❌ No `viewport={{ once: true }}` → re-animates on scroll back up
- ❌ Spring + bounce on utility actions (delete, save)
- ❌ Forgetting `useReducedMotion` for accessibility
