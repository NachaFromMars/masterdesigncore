# Layout Templates

Full layout patterns với code — copy và customize.

---

## 1. App Shell (Sidebar + Content)

```tsx
// app/layout.tsx
export default function AppLayout({ children }: { children: React.ReactNode }) {
  return (
    <div className="flex h-screen bg-gray-50 dark:bg-gray-950 overflow-hidden">
      {/* Desktop Sidebar */}
      <Sidebar className="hidden md:flex" />
      
      {/* Main area */}
      <div className="flex flex-1 flex-col overflow-hidden">
        {/* Top bar (mobile only) */}
        <MobileHeader className="md:hidden" />
        
        {/* Content */}
        <main className="flex-1 overflow-y-auto">
          <div className="mx-auto max-w-7xl px-4 sm:px-6 lg:px-8 py-6">
            {children}
          </div>
        </main>
      </div>
    </div>
  )
}

// components/sidebar.tsx
function Sidebar({ className }: { className?: string }) {
  const pathname = usePathname()
  
  const navItems = [
    { href: "/dashboard", icon: Home, label: "Dashboard" },
    { href: "/analytics", icon: BarChart2, label: "Analytics" },
    { href: "/users", icon: Users, label: "Users" },
    { href: "/settings", icon: Settings, label: "Settings" },
  ]
  
  return (
    <aside className={cn(
      "flex flex-col w-64 border-r border-gray-200 dark:border-gray-800 bg-white dark:bg-gray-900 py-4",
      className
    )}>
      {/* Logo */}
      <div className="px-6 mb-8">
        <Logo />
      </div>
      
      {/* Nav */}
      <nav className="flex-1 space-y-1 px-3">
        {navItems.map(item => {
          const isActive = pathname.startsWith(item.href)
          return (
            <Link
              key={item.href}
              href={item.href}
              className={cn(
                "flex items-center gap-3 rounded-lg px-3 py-2 text-sm font-medium transition-colors",
                isActive
                  ? "bg-blue-50 text-blue-700 dark:bg-blue-950/30 dark:text-blue-300"
                  : "text-gray-700 dark:text-gray-300 hover:bg-gray-100 dark:hover:bg-gray-800 hover:text-gray-900 dark:hover:text-white"
              )}
            >
              <item.icon className={cn("size-4 flex-shrink-0", isActive ? "text-blue-600" : "text-gray-400")} />
              {item.label}
            </Link>
          )
        })}
      </nav>
      
      {/* User footer */}
      <div className="px-3 mt-4 border-t border-gray-200 dark:border-gray-800 pt-4">
        <UserMenu />
      </div>
    </aside>
  )
}
```

---

## 2. Dashboard Page

```tsx
// app/dashboard/page.tsx
export default function DashboardPage() {
  return (
    <div className="space-y-6">
      {/* Page header */}
      <div className="flex items-center justify-between">
        <div>
          <h1 className="text-2xl font-bold text-gray-950 dark:text-white">Dashboard</h1>
          <p className="text-sm text-gray-500 mt-1">Welcome back, here's your overview</p>
        </div>
        <div className="flex items-center gap-3">
          <DateRangePicker />
          <Button>
            <Plus className="size-4 mr-2" />
            New report
          </Button>
        </div>
      </div>
      
      {/* KPI Stats */}
      <div className="grid grid-cols-1 sm:grid-cols-2 xl:grid-cols-4 gap-4">
        {stats.map(stat => (
          <Card key={stat.label}>
            <CardHeader>
              <CardDescription>{stat.label}</CardDescription>
              <CardTitle className="text-3xl tabular-nums">{stat.value}</CardTitle>
              <CardAction>
                <span className={cn("text-sm font-medium", stat.trend > 0 ? "text-green-600" : "text-red-600")}>
                  {stat.trend > 0 ? "+" : ""}{stat.trend}%
                </span>
              </CardAction>
            </CardHeader>
          </Card>
        ))}
      </div>
      
      {/* Charts row */}
      <div className="grid grid-cols-1 lg:grid-cols-3 gap-6">
        <Card className="lg:col-span-2">
          <CardHeader>
            <CardTitle>Revenue over time</CardTitle>
            <CardDescription>Monthly revenue for the last 12 months</CardDescription>
          </CardHeader>
          <CardContent>
            <RevenueChart />
          </CardContent>
        </Card>
        
        <Card>
          <CardHeader>
            <CardTitle>Top sources</CardTitle>
          </CardHeader>
          <CardContent>
            <SourcesDonut />
          </CardContent>
        </Card>
      </div>
      
      {/* Recent data table */}
      <Card>
        <CardHeader>
          <CardTitle>Recent orders</CardTitle>
          <CardAction>
            <Button variant="ghost" size="sm" asChild>
              <Link href="/orders">View all →</Link>
            </Button>
          </CardAction>
        </CardHeader>
        <CardContent className="p-0">
          <OrdersTable />
        </CardContent>
      </Card>
    </div>
  )
}
```

---

## 3. Auth Page (Sign In / Sign Up)

```tsx
// app/(auth)/sign-in/page.tsx
export default function SignInPage() {
  return (
    <div className="min-h-screen grid grid-cols-1 lg:grid-cols-2">
      {/* Left: Form */}
      <div className="flex items-center justify-center px-6 py-12">
        <div className="w-full max-w-sm">
          {/* Logo */}
          <Link href="/" className="flex items-center gap-2 mb-8">
            <Logo className="size-8" />
            <span className="font-semibold text-gray-900 dark:text-white">AppName</span>
          </Link>
          
          {/* Heading */}
          <div className="mb-6">
            <h1 className="text-2xl font-bold text-gray-950 dark:text-white">Welcome back</h1>
            <p className="text-gray-500 mt-1">Sign in to your account</p>
          </div>
          
          {/* Social login */}
          <div className="space-y-3 mb-6">
            <Button variant="outline" className="w-full" onClick={signInWithGoogle}>
              <GoogleIcon className="size-4 mr-2" />
              Continue with Google
            </Button>
            <Button variant="outline" className="w-full" onClick={signInWithGithub}>
              <Github className="size-4 mr-2" />
              Continue with GitHub
            </Button>
          </div>
          
          {/* Divider */}
          <div className="relative flex items-center mb-6">
            <div className="flex-1 border-t border-gray-200 dark:border-gray-800" />
            <span className="mx-4 text-xs text-gray-400">Or continue with email</span>
            <div className="flex-1 border-t border-gray-200 dark:border-gray-800" />
          </div>
          
          {/* Email form */}
          <LoginForm />
          
          {/* Footer */}
          <p className="text-sm text-gray-500 text-center mt-6">
            Don't have an account?{" "}
            <Link href="/sign-up" className="text-blue-600 hover:underline font-medium">
              Sign up
            </Link>
          </p>
        </div>
      </div>
      
      {/* Right: Visual/Marketing */}
      <div className="hidden lg:flex bg-gradient-to-br from-blue-600 to-violet-700 items-center justify-center p-12">
        <div className="text-white text-center max-w-sm">
          <h2 className="text-3xl font-bold mb-4">Build faster, ship better</h2>
          <p className="text-blue-100">The platform for modern web applications.</p>
          {/* Testimonials, features, etc */}
        </div>
      </div>
    </div>
  )
}
```

---

## 4. Settings Page

```tsx
export default function SettingsPage() {
  return (
    <div className="max-w-4xl mx-auto">
      <div className="mb-8">
        <h1 className="text-2xl font-bold">Settings</h1>
        <p className="text-gray-500 mt-1">Manage your account and preferences</p>
      </div>
      
      {/* Settings tabs */}
      <div className="grid grid-cols-1 md:grid-cols-[200px_1fr] gap-8">
        {/* Left nav */}
        <nav className="space-y-1">
          {settingsSections.map(section => (
            <Link
              key={section.id}
              href={`#${section.id}`}
              className="flex items-center gap-3 px-3 py-2 rounded-lg text-sm font-medium text-gray-600 hover:bg-gray-100 hover:text-gray-900"
            >
              <section.icon className="size-4" />
              {section.label}
            </Link>
          ))}
        </nav>
        
        {/* Right content */}
        <div className="space-y-6">
          {/* Profile section */}
          <Card id="profile">
            <CardHeader>
              <CardTitle>Profile</CardTitle>
              <CardDescription>Update your personal information</CardDescription>
            </CardHeader>
            <CardContent>
              <ProfileForm />
            </CardContent>
          </Card>
          
          {/* Danger zone */}
          <Card className="border-red-200 dark:border-red-900/30" id="danger">
            <CardHeader>
              <CardTitle className="text-red-600">Danger Zone</CardTitle>
              <CardDescription>Irreversible and destructive actions</CardDescription>
            </CardHeader>
            <CardContent>
              <div className="flex items-center justify-between">
                <div>
                  <p className="font-medium">Delete account</p>
                  <p className="text-sm text-gray-500">Permanently delete your account and all data</p>
                </div>
                <DeleteAccountButton />
              </div>
            </CardContent>
          </Card>
        </div>
      </div>
    </div>
  )
}
```

---

## 5. Landing Page Hero

```tsx
export function HeroSection() {
  return (
    <section className="relative overflow-hidden bg-white dark:bg-gray-950">
      {/* Background */}
      <div className="absolute inset-0 -z-10">
        <div className="absolute inset-0 bg-gradient-to-b from-blue-50/50 dark:from-blue-950/20" />
        <div className="absolute top-0 left-1/2 -translate-x-1/2 w-[800px] h-[800px] 
          rounded-full bg-blue-100/30 dark:bg-blue-900/10 blur-3xl -translate-y-1/2" />
      </div>
      
      <div className="mx-auto max-w-7xl px-4 sm:px-6 lg:px-8 pt-20 pb-32 text-center">
        {/* Badge */}
        <motion.div
          initial={{ opacity: 0, y: 20 }}
          animate={{ opacity: 1, y: 0 }}
          transition={{ duration: 0.5 }}
          className="inline-flex items-center gap-2 rounded-full border border-blue-200 dark:border-blue-900 
            bg-blue-50 dark:bg-blue-950/50 px-4 py-1.5 mb-8 text-sm text-blue-700 dark:text-blue-300"
        >
          <Zap className="size-3.5" />
          New: AI-powered features →
        </motion.div>
        
        {/* Headline */}
        <motion.h1
          initial={{ opacity: 0, y: 20 }}
          animate={{ opacity: 1, y: 0 }}
          transition={{ duration: 0.5, delay: 0.1 }}
          className="text-5xl sm:text-6xl lg:text-7xl font-bold tracking-tight text-gray-950 dark:text-white [text-wrap:balance] mb-6"
        >
          Build beautiful apps
          <br />
          <span className="bg-gradient-to-r from-blue-600 to-violet-600 bg-clip-text text-transparent">
            10x faster
          </span>
        </motion.h1>
        
        {/* Description */}
        <motion.p
          initial={{ opacity: 0, y: 20 }}
          animate={{ opacity: 1, y: 0 }}
          transition={{ duration: 0.5, delay: 0.2 }}
          className="text-xl text-gray-600 dark:text-gray-400 max-w-2xl mx-auto mb-10 leading-relaxed"
        >
          The complete design system for building modern web and mobile applications.
        </motion.p>
        
        {/* CTA */}
        <motion.div
          initial={{ opacity: 0, y: 20 }}
          animate={{ opacity: 1, y: 0 }}
          transition={{ duration: 0.5, delay: 0.3 }}
          className="flex flex-col sm:flex-row items-center justify-center gap-4"
        >
          <Button size="lg" className="w-full sm:w-auto text-base px-8 h-12 shadow-lg shadow-blue-500/25">
            Get started free
            <ArrowRight className="size-4 ml-2" />
          </Button>
          <Button variant="ghost" size="lg" className="w-full sm:w-auto text-base h-12">
            View docs
          </Button>
        </motion.div>
        
        {/* Social proof */}
        <motion.div
          initial={{ opacity: 0 }}
          animate={{ opacity: 1 }}
          transition={{ duration: 0.5, delay: 0.5 }}
          className="mt-12 flex items-center justify-center gap-6 text-sm text-gray-500"
        >
          <span>Trusted by 10,000+ developers</span>
          <span>★★★★★ 4.9/5</span>
        </motion.div>
      </div>
    </section>
  )
}
```

---

## 6. Empty State Template

```tsx
function EmptyState({
  icon: Icon = Inbox,
  title,
  description,
  action
}: {
  icon?: LucideIcon
  title: string
  description: string
  action?: { label: string; onClick: () => void }
}) {
  return (
    <div className="flex flex-col items-center justify-center py-16 px-8 text-center">
      <div className="mb-4 rounded-full bg-gray-100 dark:bg-gray-800 p-4">
        <Icon className="size-8 text-gray-400" />
      </div>
      <h3 className="text-lg font-semibold text-gray-900 dark:text-white mb-2">{title}</h3>
      <p className="text-sm text-gray-500 dark:text-gray-400 max-w-sm leading-relaxed mb-6">{description}</p>
      {action && (
        <Button onClick={action.onClick}>
          <Plus className="size-4 mr-2" />
          {action.label}
        </Button>
      )}
    </div>
  )
}

// Usage
<EmptyState
  icon={FolderOpen}
  title="No projects yet"
  description="Get started by creating your first project."
  action={{ label: "Create project", onClick: () => setOpen(true) }}
/>
```
