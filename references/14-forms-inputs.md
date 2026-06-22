# 14 — Forms & Inputs Design

> SOURCE: shadcn/ui form patterns, UX form research, accessible form design

---

## Core Principle
Forms are conversations. Make them feel easy, forgiving, and clear about what's expected.

---

## Rule 1: Input Component (Full Featured)
```html
<div class="space-y-1.5">
  <!-- Label: always above, never inside (placeholder ≠ label) -->
  <label for="email" class="block text-sm font-medium text-gray-700 dark:text-gray-300">
    Email address
    <span class="text-red-500 ml-0.5" aria-hidden="true">*</span>
  </label>
  
  <!-- Input with states -->
  <input 
    id="email"
    type="email"
    placeholder="you@example.com"
    autocomplete="email"
    class="
      block w-full rounded-lg
      border border-gray-300 dark:border-gray-700
      bg-white dark:bg-gray-900
      px-3 py-2 text-sm
      text-gray-900 dark:text-gray-100
      placeholder:text-gray-400 dark:placeholder:text-gray-500
      
      /* Focus */
      focus:border-blue-500 dark:focus:border-blue-400
      focus:ring-2 focus:ring-blue-500/20 dark:focus:ring-blue-400/20
      focus:outline-none
      
      /* Error state */
      aria-[invalid=true]:border-red-500
      aria-[invalid=true]:ring-red-500/20
      
      /* Disabled */
      disabled:bg-gray-50 dark:disabled:bg-gray-800
      disabled:cursor-not-allowed disabled:opacity-60
      
      transition-all duration-150
    "
  />
  
  <!-- Helper text OR error -->
  <p class="text-sm text-gray-500" id="email-hint">We'll never share your email.</p>
  <!-- Error replaces helper: -->
  <p class="text-sm text-red-500 flex items-center gap-1" role="alert">
    <AlertCircle class="size-3.5" aria-hidden="true" />
    Please enter a valid email address
  </p>
</div>
```

---

## Rule 2: Form Layout Patterns
```html
<!-- Single column (most forms: mobile + simple) -->
<form class="space-y-4 max-w-md">

<!-- Two column (profile, checkout) -->
<form class="grid grid-cols-1 sm:grid-cols-2 gap-4 max-w-2xl">

<!-- Grouped sections -->
<form class="max-w-2xl space-y-8">
  <section>
    <h3 class="text-base font-semibold text-gray-900 mb-4">Personal Information</h3>
    <div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
      <!-- fields -->
    </div>
  </section>
  
  <hr class="border-gray-200 dark:border-gray-800" />
  
  <section>
    <h3 class="text-base font-semibold text-gray-900 mb-4">Account Security</h3>
    <!-- fields -->
  </section>
</form>
```

---

## Rule 3: Button Groups & CTAs
```html
<!-- Right-align actions (standard form footer) -->
<div class="flex items-center justify-end gap-3 pt-4 border-t dark:border-gray-800">
  <Button variant="ghost">Cancel</Button>
  <Button type="submit">Save changes</Button>
</div>

<!-- Left-align for wizard/multi-step -->
<div class="flex items-center justify-between pt-4">
  <Button variant="outline">← Back</Button>
  <Button type="submit">Continue →</Button>
</div>

<!-- Full width on mobile -->
<div class="flex flex-col sm:flex-row-reverse gap-3">
  <Button class="w-full sm:w-auto" type="submit">Create account</Button>
  <Button class="w-full sm:w-auto" variant="outline">Cancel</Button>
</div>
```

---

## Rule 4: Select / Dropdown
```tsx
// shadcn/ui Select
<div class="space-y-1.5">
  <Label htmlFor="country">Country</Label>
  <Select>
    <SelectTrigger id="country" className="w-full">
      <SelectValue placeholder="Select your country" />
    </SelectTrigger>
    <SelectContent>
      <SelectGroup>
        <SelectLabel>Asia</SelectLabel>
        <SelectItem value="vn">🇻🇳 Vietnam</SelectItem>
        <SelectItem value="jp">🇯🇵 Japan</SelectItem>
      </SelectGroup>
    </SelectContent>
  </Select>
</div>
```

---

## Rule 5: Checkbox & Radio Groups
```tsx
// Checkbox with label
<div class="flex items-start gap-3">
  <Checkbox 
    id="terms" 
    className="mt-0.5"
  />
  <div>
    <label htmlFor="terms" className="text-sm font-medium text-gray-900">
      Accept terms and conditions
    </label>
    <p className="text-sm text-gray-500">
      By checking, you agree to our <a href="#" className="text-blue-600 underline">Terms</a>.
    </p>
  </div>
</div>

// Radio group (plan selection)
<RadioGroup defaultValue="pro">
  {plans.map(plan => (
    <div key={plan.id} className={cn(
      "flex items-start gap-3 p-4 rounded-lg border cursor-pointer",
      "hover:border-blue-300 hover:bg-blue-50/50",
      "data-[state=checked]:border-blue-500 data-[state=checked]:bg-blue-50"
    )}>
      <RadioGroupItem value={plan.id} id={plan.id} className="mt-1" />
      <label htmlFor={plan.id} className="cursor-pointer">
        <p className="font-medium">{plan.name}</p>
        <p className="text-sm text-gray-500">{plan.description}</p>
      </label>
    </div>
  ))}
</RadioGroup>
```

---

## Rule 6: File Upload
```tsx
// Drop zone pattern
<div
  onDragOver={handleDragOver}
  onDrop={handleDrop}
  className={cn(
    "relative flex flex-col items-center justify-center",
    "rounded-xl border-2 border-dashed p-12 text-center",
    "cursor-pointer transition-colors",
    isDragging 
      ? "border-blue-500 bg-blue-50 dark:bg-blue-950/20" 
      : "border-gray-300 dark:border-gray-700 hover:border-gray-400"
  )}
>
  <Upload className="size-8 text-gray-400 mb-3" />
  <p className="text-sm font-medium text-gray-900 dark:text-gray-100">
    Drop files here or <span className="text-blue-600">browse</span>
  </p>
  <p className="text-xs text-gray-500 mt-1">PNG, JPG, PDF up to 10MB</p>
  <input type="file" className="absolute inset-0 opacity-0 cursor-pointer" />
</div>
```

---

## Rule 7: Input Addons / Affixes
```html
<!-- Prefix (URL) -->
<div class="flex rounded-lg overflow-hidden border border-gray-300 focus-within:ring-2 focus-within:ring-blue-500">
  <span class="flex items-center px-3 bg-gray-50 dark:bg-gray-800 border-r border-gray-300 text-sm text-gray-500">
    https://
  </span>
  <input type="text" placeholder="yoursite.com" class="flex-1 px-3 py-2 text-sm bg-white dark:bg-gray-900 outline-none" />
</div>

<!-- Suffix (icon or action) -->
<div class="relative">
  <input type="search" class="w-full pl-10 pr-4 py-2 rounded-lg border text-sm" />
  <Search class="absolute left-3 top-1/2 -translate-y-1/2 size-4 text-gray-400" />
</div>

<!-- Password visibility toggle -->
<div class="relative">
  <input type={showPass ? "text" : "password"} class="w-full pr-10 pl-3 py-2 rounded-lg border text-sm" />
  <button type="button" onClick={togglePass} class="absolute right-3 top-1/2 -translate-y-1/2 text-gray-400 hover:text-gray-600">
    {showPass ? <EyeOff class="size-4" /> : <Eye class="size-4" />}
  </button>
</div>
```

---

## Rule 8: Form Validation UX
```tsx
// React Hook Form + Zod (recommended)
import { useForm } from 'react-hook-form'
import { zodResolver } from '@hookform/resolvers/zod'
import { z } from 'zod'

const schema = z.object({
  email: z.string().email('Invalid email address'),
  password: z.string().min(8, 'Password must be at least 8 characters'),
})

// Validate on blur, show errors inline
// Don't submit to server for validation that can be done client-side
// Preserve entered data on errors
// Clear errors as user types corrections
```

---

## Rule 9: Multi-Step Forms
```tsx
// Progress indicator
<div class="flex items-center gap-2 mb-8">
  {steps.map((step, i) => (
    <>
      <div class={cn(
        "flex items-center justify-center size-8 rounded-full text-sm font-medium",
        i < currentStep ? "bg-blue-600 text-white" :
        i === currentStep ? "bg-blue-100 text-blue-700 border-2 border-blue-600" :
        "bg-gray-100 text-gray-400"
      )}>
        {i < currentStep ? <Check class="size-4" /> : i + 1}
      </div>
      {i < steps.length - 1 && (
        <div class={cn("flex-1 h-0.5", i < currentStep ? "bg-blue-600" : "bg-gray-200")} />
      )}
    </>
  ))}
</div>
```

---

## Anti-Patterns 🚫
- ❌ Placeholder as only label (hides on type)
- ❌ Validate on every keystroke (annoying)
- ❌ Clear form on error
- ❌ Disable submit without explaining why
- ❌ Generic "An error occurred" messages
- ❌ Require phone number format (no +, no dashes, etc.)
- ❌ CAPTCHAs without fallback
- ❌ Auto-advance between fields
- ❌ No password visibility toggle
