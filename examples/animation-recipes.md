# Animation Recipes (Motion / Framer Motion)

Copy-paste animation patterns với Motion (framer-motion v12+).

---

## Setup

```tsx
import { motion, AnimatePresence, MotionConfig } from "motion/react"

// Wrap app
<MotionConfig 
  transition={{ type: "spring", stiffness: 300, damping: 30 }}
  reducedMotion="user"  // Respects prefers-reduced-motion
>
  <App />
</MotionConfig>
```

---

## 🔤 Text Animations

```tsx
// Fade up text on enter
const fadeUpVariants = {
  hidden: { opacity: 0, y: 20 },
  visible: { 
    opacity: 1, 
    y: 0,
    transition: { duration: 0.5, ease: "easeOut" }
  }
}

<motion.h1 
  variants={fadeUpVariants} 
  initial="hidden" 
  animate="visible"
>
  Title
</motion.h1>

// Stagger words (split text manually)
const words = "Hello Beautiful World".split(" ")

<div className="flex gap-2 overflow-hidden">
  {words.map((word, i) => (
    <motion.span
      key={i}
      initial={{ y: "100%" }}
      animate={{ y: 0 }}
      transition={{ delay: i * 0.1, duration: 0.4, ease: [0.2, 0, 0, 1] }}
    >
      {word}
    </motion.span>
  ))}
</div>
```

---

## 📝 List Animations (Staggered)

```tsx
const container = {
  hidden: { opacity: 0 },
  show: {
    opacity: 1,
    transition: {
      staggerChildren: 0.07,
      delayChildren: 0.1
    }
  }
}

const item = {
  hidden: { opacity: 0, y: 20, filter: "blur(4px)" },
  show: { 
    opacity: 1, 
    y: 0, 
    filter: "blur(0px)",
    transition: { duration: 0.4, ease: "easeOut" }
  }
}

<motion.ul variants={container} initial="hidden" animate="show">
  {items.map(item => (
    <motion.li key={item.id} variants={item}>
      <Card item={item} />
    </motion.li>
  ))}
</motion.ul>
```

---

## 🎭 Modal / Dialog

```tsx
// Backdrop + modal combo
function Modal({ isOpen, onClose, children }) {
  return (
    <AnimatePresence>
      {isOpen && (
        <>
          {/* Backdrop */}
          <motion.div
            key="backdrop"
            className="fixed inset-0 bg-black/50 z-40"
            initial={{ opacity: 0 }}
            animate={{ opacity: 1 }}
            exit={{ opacity: 0 }}
            onClick={onClose}
          />
          
          {/* Modal */}
          <motion.div
            key="modal"
            className="fixed inset-0 z-50 flex items-center justify-center p-4"
            initial={{ opacity: 0, scale: 0.95, y: 20 }}
            animate={{ opacity: 1, scale: 1, y: 0 }}
            exit={{ opacity: 0, scale: 0.95, y: 20 }}
            transition={{ duration: 0.2, ease: "easeOut" }}
          >
            <div className="w-full max-w-md bg-white rounded-2xl shadow-2xl p-6">
              {children}
            </div>
          </motion.div>
        </>
      )}
    </AnimatePresence>
  )
}
```

---

## 🔔 Toast / Notification

```tsx
// Slide in from right
<AnimatePresence>
  {notifications.map(toast => (
    <motion.div
      key={toast.id}
      layout
      initial={{ opacity: 0, x: "100%", scale: 0.95 }}
      animate={{ opacity: 1, x: 0, scale: 1 }}
      exit={{ opacity: 0, x: "100%", scale: 0.95, transition: { duration: 0.15 } }}
      transition={{ type: "spring", stiffness: 400, damping: 30 }}
      className="..."
    >
      {toast.message}
    </motion.div>
  ))}
</AnimatePresence>
```

---

## 🎯 Button Interactions

```tsx
// Satisfying button press
<motion.button
  whileHover={{ scale: 1.03, y: -1 }}
  whileTap={{ scale: 0.97 }}
  transition={{ type: "spring", stiffness: 400, damping: 20 }}
>
  Click me
</motion.button>

// Loading → Success state
function SubmitButton({ onSubmit }) {
  const [status, setStatus] = useState<'idle' | 'loading' | 'success'>('idle')
  
  return (
    <motion.button
      onClick={async () => {
        setStatus('loading')
        await onSubmit()
        setStatus('success')
        setTimeout(() => setStatus('idle'), 2000)
      }}
      animate={{
        backgroundColor: status === 'success' ? '#22c55e' : '#3b82f6',
        width: status === 'loading' ? 48 : 'auto'
      }}
      transition={{ type: "spring", stiffness: 300 }}
    >
      <AnimatePresence mode="wait">
        {status === 'idle' && <motion.span key="label" initial={{ opacity: 0 }} animate={{ opacity: 1 }}>Submit</motion.span>}
        {status === 'loading' && <motion.div key="spin" initial={{ opacity: 0 }} animate={{ opacity: 1 }}><Loader2 className="animate-spin size-4" /></motion.div>}
        {status === 'success' && <motion.div key="check" initial={{ scale: 0 }} animate={{ scale: 1 }}><Check className="size-4" /></motion.div>}
      </AnimatePresence>
    </motion.button>
  )
}
```

---

## 📜 Scroll Animations

```tsx
// Fade in on scroll (most common)
<motion.section
  initial={{ opacity: 0, y: 60 }}
  whileInView={{ opacity: 1, y: 0 }}
  viewport={{ once: true, margin: "-100px" }}
  transition={{ duration: 0.6, ease: "easeOut" }}
>
  Section content
</motion.section>

// Scroll progress bar
import { useScroll, useSpring } from "motion/react"

function ProgressBar() {
  const { scrollYProgress } = useScroll()
  const scaleX = useSpring(scrollYProgress, { stiffness: 100, damping: 30 })
  
  return (
    <motion.div
      className="fixed top-0 left-0 right-0 h-1 bg-blue-600 origin-left z-50"
      style={{ scaleX }}
    />
  )
}

// Parallax
import { useScroll, useTransform } from "motion/react"

function ParallaxHero() {
  const { scrollY } = useScroll()
  const y = useTransform(scrollY, [0, 500], [0, -150])
  const opacity = useTransform(scrollY, [0, 300], [1, 0])
  
  return (
    <div className="relative overflow-hidden h-screen">
      <motion.div className="absolute inset-0" style={{ y }}>
        <img className="w-full h-full object-cover" />
      </motion.div>
      <motion.div className="relative z-10 text-center" style={{ opacity }}>
        <h1>Hero Text</h1>
      </motion.div>
    </div>
  )
}
```

---

## 📐 Layout Animations

```tsx
// Expandable card
function ExpandableCard({ title, children }) {
  const [isOpen, setIsOpen] = useState(false)
  
  return (
    <motion.div
      layout
      className="rounded-xl border cursor-pointer overflow-hidden"
      onClick={() => setIsOpen(!isOpen)}
    >
      <motion.div layout className="flex items-center justify-between p-4">
        <span className="font-medium">{title}</span>
        <motion.div animate={{ rotate: isOpen ? 180 : 0 }}>
          <ChevronDown className="size-4" />
        </motion.div>
      </motion.div>
      
      <AnimatePresence>
        {isOpen && (
          <motion.div
            initial={{ height: 0, opacity: 0 }}
            animate={{ height: "auto", opacity: 1 }}
            exit={{ height: 0, opacity: 0 }}
            transition={{ duration: 0.3, ease: "easeInOut" }}
          >
            <div className="p-4 pt-0 border-t">{children}</div>
          </motion.div>
        )}
      </AnimatePresence>
    </motion.div>
  )
}

// Tabs with sliding indicator
function AnimatedTabs({ tabs }) {
  const [active, setActive] = useState(0)
  
  return (
    <div className="flex space-x-1 relative">
      {tabs.map((tab, i) => (
        <button
          key={i}
          className={cn("relative px-4 py-2 text-sm font-medium z-10",
            active === i ? "text-white" : "text-gray-600 hover:text-gray-900")}
          onClick={() => setActive(i)}
        >
          {active === i && (
            <motion.div
              layoutId="tab-indicator"
              className="absolute inset-0 bg-blue-600 rounded-lg -z-10"
              transition={{ type: "spring", stiffness: 400, damping: 30 }}
            />
          )}
          {tab.label}
        </button>
      ))}
    </div>
  )
}
```

---

## 🎪 Page Transitions (Next.js)

```tsx
// app/layout.tsx
"use client"
import { AnimatePresence, motion } from "motion/react"
import { usePathname } from "next/navigation"

export default function Layout({ children }) {
  const pathname = usePathname()
  
  return (
    <AnimatePresence mode="wait">
      <motion.div
        key={pathname}
        initial={{ opacity: 0, y: 8 }}
        animate={{ opacity: 1, y: 0 }}
        exit={{ opacity: 0, y: -8 }}
        transition={{ duration: 0.2 }}
      >
        {children}
      </motion.div>
    </AnimatePresence>
  )
}
```

---

## ✨ Micro-Interactions

```tsx
// Heart like animation
const [liked, setLiked] = useState(false)

<motion.button
  onClick={() => setLiked(!liked)}
  whileTap={{ scale: 1.2 }}
>
  <motion.div
    animate={liked ? { 
      scale: [1, 1.5, 0.8, 1.1, 1],
      rotate: [0, -15, 15, -5, 0]
    } : {}}
    transition={{ duration: 0.4 }}
  >
    <Heart className={cn("size-5", liked ? "fill-red-500 text-red-500" : "text-gray-400")} />
  </motion.div>
</motion.button>

// Toggle switch
<motion.button
  onClick={() => setOn(!on)}
  className={cn("relative w-12 h-6 rounded-full transition-colors",
    on ? "bg-blue-600" : "bg-gray-200")}
>
  <motion.span
    className="absolute top-0.5 left-0.5 size-5 bg-white rounded-full shadow-sm"
    animate={{ x: on ? 24 : 0 }}
    transition={{ type: "spring", stiffness: 500, damping: 30 }}
  />
</motion.button>
```
