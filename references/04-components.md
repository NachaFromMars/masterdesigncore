# 04 — Component Design Patterns

> SOURCE: shadcn/ui docs, Radix UI, Material Design 3, Apple HIG

---

## Core Principle
Components phải **composable**, **accessible**, **predictable**. shadcn/ui philosophy: own your code, not a black box.

---

## Rule 1: Button — Variants & States
```tsx
// shadcn/ui Button variants
import { Button } from "@/components/ui/button"

// Primary CTA
<Button>Submit</Button>
<Button variant="default" size="default">

// Secondary actions
<Button variant="outline">Cancel</Button>
<Button variant="secondary">Filter</Button>
<Button variant="ghost">More</Button>

// Destructive
<Button variant="destructive">Delete</Button>

// Link style
<Button variant="link">Learn more →</Button>

// Icon button
<Button size="icon"><PlusIcon /></Button>

// Loading state
<Button disabled>
  <Spinner className="mr-2 size-4" />
  Loading...
</Button>

// With icon (shadcn v5 pattern)
<Button>
  <GitBranchIcon data-icon="inline-start" />
  Create branch
</Button>
```

**State classes (manual):**
```html
<button class="
  bg-blue-600 text-white px-4 py-2 rounded-lg font-medium
  hover:bg-blue-700 
  active:scale-95 active:bg-blue-800
  focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-blue-500 focus-visible:ring-offset-2
  disabled:opacity-50 disabled:cursor-not-allowed
  transition-all duration-150
">
```

---

## Rule 2: Card Component
```tsx
import { Card, CardHeader, CardTitle, CardDescription, CardContent, CardFooter, CardAction } from "@/components/ui/card"

// Standard card
<Card>
  <CardHeader>
    <CardTitle>Analytics Overview</CardTitle>
    <CardDescription>Last 30 days performance</CardDescription>
    <CardAction>
      <Button variant="outline" size="sm">Export</Button>
    </CardAction>
  </CardHeader>
  <CardContent>
    {/* Chart or content */}
  </CardContent>
  <CardFooter>
    <Button variant="ghost" size="sm">View all</Button>
  </CardFooter>
</Card>

// Compact card
<Card size="sm">

// Image card
<Card>
  <img src={img} className="rounded-t-xl object-cover w-full h-48" />
  <CardHeader>
    <CardTitle>Title</CardTitle>
  </CardHeader>
</Card>
```

---

## Rule 3: Form Components
```tsx
// Input with label + error
<div className="space-y-1.5">
  <Label htmlFor="email">Email</Label>
  <Input 
    id="email" 
    type="email" 
    placeholder="you@example.com"
    className="w-full"
  />
  <p className="text-sm text-red-500">Invalid email address</p>
</div>

// Select
<Select>
  <SelectTrigger className="w-full">
    <SelectValue placeholder="Select a plan" />
  </SelectTrigger>
  <SelectContent>
    <SelectItem value="free">Free</SelectItem>
    <SelectItem value="pro">Pro — $9/mo</SelectItem>
  </SelectContent>
</Select>

// Textarea
<Textarea 
  placeholder="Describe your issue..."
  className="min-h-[120px] resize-none"
/>
```

---

## Rule 4: Dialog / Modal
```tsx
<Dialog>
  <DialogTrigger asChild>
    <Button>Open</Button>
  </DialogTrigger>
  <DialogContent className="sm:max-w-lg">
    <DialogHeader>
      <DialogTitle>Confirm Delete</DialogTitle>
      <DialogDescription>
        This action cannot be undone.
      </DialogDescription>
    </DialogHeader>
    <DialogFooter>
      <Button variant="outline">Cancel</Button>
      <Button variant="destructive">Delete</Button>
    </DialogFooter>
  </DialogContent>
</Dialog>
```

---

## Rule 5: Badge / Tag
```tsx
<Badge>New</Badge>
<Badge variant="outline">Beta</Badge>
<Badge variant="secondary">Draft</Badge>
<Badge className="bg-green-100 text-green-700 border-green-200">Active</Badge>
<Badge className="bg-red-100 text-red-700 border-red-200">Error</Badge>
```

---

## Rule 6: Navigation Patterns
```html
<!-- Sidebar nav item -->
<a class="flex items-center gap-3 rounded-lg px-3 py-2 text-sm font-medium
  text-gray-700 hover:bg-gray-100 hover:text-gray-900
  [&.active]:bg-blue-50 [&.active]:text-blue-700
  transition-colors">
  <HomeIcon class="size-4" />
  Dashboard
</a>

<!-- Tab navigation -->
<div class="flex border-b border-gray-200">
  <button class="px-4 py-2 text-sm font-medium text-blue-600 border-b-2 border-blue-600">
    Active Tab
  </button>
  <button class="px-4 py-2 text-sm font-medium text-gray-500 hover:text-gray-700">
    Tab 2
  </button>
</div>
```

---

## Rule 7: Table (Data Display)
```tsx
<Table>
  <TableHeader>
    <TableRow>
      <TableHead>Name</TableHead>
      <TableHead>Status</TableHead>
      <TableHead className="text-right">Amount</TableHead>
    </TableRow>
  </TableHeader>
  <TableBody>
    {data.map(row => (
      <TableRow key={row.id} className="hover:bg-gray-50">
        <TableCell className="font-medium">{row.name}</TableCell>
        <TableCell>
          <Badge variant={row.status === 'active' ? 'default' : 'outline'}>
            {row.status}
          </Badge>
        </TableCell>
        <TableCell className="text-right">${row.amount}</TableCell>
      </TableRow>
    ))}
  </TableBody>
</Table>
```

---

## Rule 8: Toast / Notification
```tsx
import { toast } from "sonner"

// Success
toast.success("Profile updated!")

// Error with action
toast.error("Failed to save", {
  action: { label: "Retry", onClick: () => save() }
})

// Promise
toast.promise(save(), {
  loading: "Saving...",
  success: "Saved!",
  error: "Failed to save"
})
```

---

## Component Sizing Convention
| Size | px equivalent | Use case |
|------|--------------|----------|
| `xs` | ~24px height | Compact tables, inline |
| `sm` | ~32px height | Dense UIs, sidebars |
| `default` | ~40px height | Standard forms |
| `lg` | ~48px height | Hero CTAs, landing pages |
| `icon` | 40×40px | Icon-only buttons |

---

## Anti-Patterns 🚫
- ❌ No hover/focus states → feels broken
- ❌ No loading state → confusing UX
- ❌ Modals without ESC / backdrop click to close
- ❌ Buttons without disabled state during loading
- ❌ Forms without error states
- ❌ No empty states (blank tables look broken)
