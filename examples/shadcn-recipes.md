# shadcn/ui Recipes

Cấu hình và patterns cho shadcn/ui components.

---

## Setup

```bash
# Init shadcn in Next.js project
pnpm dlx shadcn@latest init

# Add commonly needed components
pnpm dlx shadcn@latest add \
  button card input label badge textarea select \
  dialog sheet drawer \
  dropdown-menu context-menu \
  tabs accordion \
  tooltip popover \
  alert alert-dialog \
  avatar \
  checkbox radio-group switch \
  slider progress \
  separator skeleton \
  table \
  toast (use sonner instead) \
  command \
  calendar date-picker \
  scroll-area
```

---

## 🎨 Theme Configuration

```css
/* globals.css — Custom brand theme */
@import "tailwindcss";

@custom-variant dark (&:where(.dark, .dark *));

@theme {
  --font-sans: 'Inter', system-ui, sans-serif;
  --radius: 0.5rem;
}

:root {
  /* Neutral base */
  --background: oklch(1 0 0);
  --foreground: oklch(0.09 0 0);
  --card: oklch(1 0 0);
  --card-foreground: oklch(0.09 0 0);
  --popover: oklch(1 0 0);
  --popover-foreground: oklch(0.09 0 0);
  
  /* Brand (blue) */
  --primary: oklch(0.55 0.22 262);
  --primary-foreground: oklch(0.98 0 0);
  
  /* Secondary */
  --secondary: oklch(0.96 0 0);
  --secondary-foreground: oklch(0.09 0 0);
  
  /* Muted */
  --muted: oklch(0.96 0 0);
  --muted-foreground: oklch(0.45 0 0);
  
  /* Accents */
  --accent: oklch(0.96 0 0);
  --accent-foreground: oklch(0.09 0 0);
  
  /* Destructive */
  --destructive: oklch(0.63 0.24 25);
  --destructive-foreground: oklch(0.98 0 0);
  
  /* Borders */
  --border: oklch(0.91 0 0);
  --input: oklch(0.91 0 0);
  --ring: oklch(0.55 0.22 262);
  
  /* Border radius */
  --radius-sm: calc(var(--radius) - 4px);
  --radius-md: var(--radius);
  --radius-lg: calc(var(--radius) + 4px);
  --radius-xl: calc(var(--radius) + 8px);
}

.dark {
  --background: oklch(0.09 0 0);
  --foreground: oklch(0.98 0 0);
  --card: oklch(0.13 0 0);
  --card-foreground: oklch(0.98 0 0);
  --popover: oklch(0.13 0 0);
  --popover-foreground: oklch(0.98 0 0);
  --primary: oklch(0.70 0.18 262);
  --primary-foreground: oklch(0.09 0 0);
  --secondary: oklch(0.17 0 0);
  --secondary-foreground: oklch(0.98 0 0);
  --muted: oklch(0.17 0 0);
  --muted-foreground: oklch(0.65 0 0);
  --accent: oklch(0.17 0 0);
  --accent-foreground: oklch(0.98 0 0);
  --destructive: oklch(0.70 0.22 25);
  --border: oklch(1 0 0 / 10%);
  --input: oklch(1 0 0 / 10%);
  --ring: oklch(0.70 0.18 262);
}
```

---

## 🔘 Button Patterns

```tsx
import { Button } from "@/components/ui/button"

// All variants
<Button>Primary (default)</Button>
<Button variant="secondary">Secondary</Button>
<Button variant="outline">Outline</Button>
<Button variant="ghost">Ghost</Button>
<Button variant="link">Link →</Button>
<Button variant="destructive">Delete</Button>

// All sizes
<Button size="sm">Small</Button>
<Button size="default">Default</Button>
<Button size="lg">Large</Button>
<Button size="icon"><Plus className="size-4" /></Button>

// With icon (shadcn v5 pattern)
<Button>
  <Plus data-icon="inline-start" className="size-4" />
  New item
</Button>

// Loading state
<Button disabled>
  <Loader2 className="size-4 mr-2 animate-spin" />
  Saving...
</Button>

// Gradient custom button
<Button className="bg-gradient-to-r from-blue-600 to-violet-600 hover:from-blue-700 hover:to-violet-700 border-0 shadow-lg shadow-blue-500/25">
  Get started
</Button>

// asChild for Next.js Link
<Button asChild>
  <Link href="/dashboard">Go to Dashboard</Link>
</Button>
```

---

## 🃏 Card Layouts

```tsx
import { Card, CardHeader, CardTitle, CardDescription, CardContent, CardFooter, CardAction } from "@/components/ui/card"

// Stat card
<Card>
  <CardHeader>
    <CardDescription>Total Revenue</CardDescription>
    <CardTitle className="text-3xl tabular-nums">$45,231</CardTitle>
    <CardAction>
      <Badge variant="outline" className="text-green-600 border-green-200 bg-green-50">
        +20.1%
      </Badge>
    </CardAction>
  </CardHeader>
</Card>

// Feature card
<Card className="overflow-hidden">
  <div className="h-48 bg-gradient-to-br from-blue-50 to-indigo-100 dark:from-blue-950/30 dark:to-indigo-900/30 flex items-center justify-center">
    <FeatureIcon className="size-12 text-blue-600" />
  </div>
  <CardHeader>
    <CardTitle>Feature Name</CardTitle>
    <CardDescription>Feature description goes here</CardDescription>
  </CardHeader>
  <CardFooter>
    <Button variant="outline" size="sm">Learn more</Button>
  </CardFooter>
</Card>

// Horizontal card (list item)
<Card>
  <div className="flex gap-4 p-4">
    <img className="size-12 rounded-lg object-cover flex-shrink-0" />
    <div className="flex-1 min-w-0">
      <CardTitle className="text-base truncate">Title</CardTitle>
      <CardDescription className="text-xs">subtitle</CardDescription>
    </div>
    <Button variant="ghost" size="icon">
      <MoreHorizontal className="size-4" />
    </Button>
  </div>
</Card>
```

---

## 📋 Form with React Hook Form + Zod

```tsx
"use client"
import { useForm } from "react-hook-form"
import { zodResolver } from "@hookform/resolvers/zod"
import { z } from "zod"
import { Form, FormControl, FormDescription, FormField, FormItem, FormLabel, FormMessage } from "@/components/ui/form"
import { Input } from "@/components/ui/input"
import { Button } from "@/components/ui/button"

const formSchema = z.object({
  email: z.string().email("Invalid email address"),
  password: z.string().min(8, "At least 8 characters"),
})

export function LoginForm() {
  const form = useForm<z.infer<typeof formSchema>>({
    resolver: zodResolver(formSchema),
    defaultValues: { email: "", password: "" }
  })

  function onSubmit(values: z.infer<typeof formSchema>) {
    console.log(values)
  }

  return (
    <Form {...form}>
      <form onSubmit={form.handleSubmit(onSubmit)} className="space-y-4">
        <FormField
          control={form.control}
          name="email"
          render={({ field }) => (
            <FormItem>
              <FormLabel>Email</FormLabel>
              <FormControl>
                <Input placeholder="you@example.com" type="email" {...field} />
              </FormControl>
              <FormDescription>We'll never share your email.</FormDescription>
              <FormMessage /> {/* Auto-shows error */}
            </FormItem>
          )}
        />
        
        <FormField
          control={form.control}
          name="password"
          render={({ field }) => (
            <FormItem>
              <FormLabel>Password</FormLabel>
              <FormControl>
                <Input type="password" {...field} />
              </FormControl>
              <FormMessage />
            </FormItem>
          )}
        />
        
        <Button type="submit" className="w-full" disabled={form.formState.isSubmitting}>
          {form.formState.isSubmitting ? (
            <><Loader2 className="size-4 mr-2 animate-spin" />Signing in...</>
          ) : "Sign in"}
        </Button>
      </form>
    </Form>
  )
}
```

---

## 🎛️ Dialog Patterns

```tsx
// Confirmation dialog
<AlertDialog>
  <AlertDialogTrigger asChild>
    <Button variant="destructive">Delete account</Button>
  </AlertDialogTrigger>
  <AlertDialogContent>
    <AlertDialogHeader>
      <AlertDialogTitle>Are you absolutely sure?</AlertDialogTitle>
      <AlertDialogDescription>
        This action cannot be undone. This will permanently delete your account.
      </AlertDialogDescription>
    </AlertDialogHeader>
    <AlertDialogFooter>
      <AlertDialogCancel>Cancel</AlertDialogCancel>
      <AlertDialogAction className="bg-red-600 hover:bg-red-700">
        Delete
      </AlertDialogAction>
    </AlertDialogFooter>
  </AlertDialogContent>
</AlertDialog>

// Sheet (right panel)
<Sheet>
  <SheetTrigger asChild>
    <Button variant="outline">Settings</Button>
  </SheetTrigger>
  <SheetContent className="sm:max-w-md">
    <SheetHeader>
      <SheetTitle>Settings</SheetTitle>
      <SheetDescription>Manage your account settings.</SheetDescription>
    </SheetHeader>
    <div className="py-4">
      {/* Settings form */}
    </div>
    <SheetFooter>
      <Button>Save changes</Button>
    </SheetFooter>
  </SheetContent>
</Sheet>
```

---

## 🔔 Toast Notifications (Sonner)

```tsx
// Install: pnpm add sonner
// In layout: <Toaster />
import { toast } from "sonner"

// Types
toast("Default message")
toast.success("Saved successfully!")
toast.error("Something went wrong")
toast.warning("This might cause issues")
toast.info("Here's some info")

// With description
toast.success("Profile updated", {
  description: "Your profile has been saved."
})

// With action
toast.error("Failed to save", {
  action: {
    label: "Retry",
    onClick: () => save()
  }
})

// Promise (most useful!)
toast.promise(saveData(), {
  loading: "Saving...",
  success: "Data saved!",
  error: "Failed to save"
})
```

---

## 🔍 Command Palette

```tsx
import { Command, CommandDialog, CommandInput, CommandList, CommandEmpty, CommandGroup, CommandItem, CommandSeparator, CommandShortcut } from "@/components/ui/command"

function CommandPalette() {
  const [open, setOpen] = useState(false)
  
  useEffect(() => {
    const down = (e: KeyboardEvent) => {
      if (e.key === "k" && (e.metaKey || e.ctrlKey)) {
        e.preventDefault()
        setOpen(prev => !prev)
      }
    }
    document.addEventListener("keydown", down)
    return () => document.removeEventListener("keydown", down)
  }, [])

  return (
    <CommandDialog open={open} onOpenChange={setOpen}>
      <CommandInput placeholder="Type a command or search..." />
      <CommandList>
        <CommandEmpty>No results found.</CommandEmpty>
        <CommandGroup heading="Navigation">
          <CommandItem onSelect={() => { router.push('/dashboard'); setOpen(false) }}>
            <Home className="size-4 mr-2" />
            Dashboard
            <CommandShortcut>⌘D</CommandShortcut>
          </CommandItem>
        </CommandGroup>
        <CommandSeparator />
        <CommandGroup heading="Actions">
          <CommandItem onSelect={createNew}>
            <Plus className="size-4 mr-2" />
            Create new
          </CommandItem>
        </CommandGroup>
      </CommandList>
    </CommandDialog>
  )
}
```
