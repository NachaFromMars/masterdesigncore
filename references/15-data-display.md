# 15 — Data Display: Tables, Charts, Dashboards

> SOURCE: Dashboard design research, data visualization principles, shadcn/ui table patterns

---

## Core Principle
Data display = **clarity over cleverness**. The goal is insight, not impressive charts.

---

## Rule 1: Stats/KPI Cards
```html
<!-- KPI Card Pattern -->
<div class="grid grid-cols-1 sm:grid-cols-2 xl:grid-cols-4 gap-4">

  <!-- Simple metric card -->
  <div class="rounded-xl border bg-white dark:bg-gray-900 dark:border-gray-800 p-6">
    <div class="flex items-center justify-between mb-3">
      <p class="text-sm font-medium text-gray-500 dark:text-gray-400">Total Revenue</p>
      <div class="rounded-lg bg-blue-50 dark:bg-blue-950/30 p-2">
        <DollarSign class="size-4 text-blue-600 dark:text-blue-400" />
      </div>
    </div>
    <p class="text-2xl font-bold text-gray-950 dark:text-white tabular-nums">$45,231.89</p>
    <p class="mt-1 text-sm text-green-600 flex items-center gap-1">
      <TrendingUp class="size-3.5" />
      +20.1% from last month
    </p>
  </div>

  <!-- Highlighted/featured metric -->
  <div class="rounded-xl bg-blue-600 text-white p-6 sm:col-span-2">
    <p class="text-sm font-medium text-blue-200">Monthly Recurring Revenue</p>
    <p class="text-4xl font-bold mt-2 tabular-nums">$12,453</p>
    <div class="mt-4 h-16">
      <SparklineChart data={data} /> <!-- Inline mini chart -->
    </div>
  </div>
</div>
```

---

## Rule 2: Table Design
```tsx
// Full-featured data table
<div class="rounded-xl border overflow-hidden dark:border-gray-800">
  
  {/* Table header with search/filter */}
  <div class="flex items-center justify-between px-6 py-4 border-b bg-white dark:bg-gray-900 dark:border-gray-800">
    <div>
      <h3 class="font-semibold text-gray-950 dark:text-white">Orders</h3>
      <p class="text-sm text-gray-500">47 total orders</p>
    </div>
    <div class="flex items-center gap-2">
      <div class="relative">
        <Search class="absolute left-3 top-1/2 -translate-y-1/2 size-4 text-gray-400" />
        <input placeholder="Search orders..." 
          class="pl-9 pr-4 h-9 text-sm border rounded-lg w-64 dark:bg-gray-800 dark:border-gray-700" />
      </div>
      <Button variant="outline" size="sm">
        <Filter class="size-4 mr-2" />
        Filter
      </Button>
      <Button size="sm">Export</Button>
    </div>
  </div>
  
  {/* Table */}
  <table class="w-full">
    <thead class="bg-gray-50 dark:bg-gray-800/50">
      <tr>
        <th class="px-6 py-3 text-left text-xs font-semibold text-gray-500 uppercase tracking-wide">
          Customer
        </th>
        <th class="px-6 py-3 text-left text-xs font-semibold text-gray-500 uppercase tracking-wide">
          Status
        </th>
        <th class="px-6 py-3 text-right text-xs font-semibold text-gray-500 uppercase tracking-wide">
          Amount
        </th>
        <th class="px-6 py-3 w-12" /> {/* Actions column */}
      </tr>
    </thead>
    <tbody class="divide-y divide-gray-100 dark:divide-gray-800">
      {orders.map(order => (
        <tr class="group bg-white dark:bg-gray-900 hover:bg-gray-50 dark:hover:bg-gray-800/50 transition-colors">
          <td class="px-6 py-4">
            <div class="flex items-center gap-3">
              <img src={order.avatar} class="size-8 rounded-full flex-shrink-0" />
              <div>
                <p class="text-sm font-medium text-gray-900 dark:text-white">{order.name}</p>
                <p class="text-xs text-gray-500">{order.email}</p>
              </div>
            </div>
          </td>
          <td class="px-6 py-4">
            <StatusBadge status={order.status} />
          </td>
          <td class="px-6 py-4 text-right text-sm font-medium tabular-nums text-gray-900 dark:text-white">
            ${order.amount.toFixed(2)}
          </td>
          <td class="px-6 py-4">
            <DropdownMenu>
              <DropdownMenuTrigger asChild>
                <Button variant="ghost" size="icon" class="opacity-0 group-hover:opacity-100 size-8">
                  <MoreHorizontal class="size-4" />
                </Button>
              </DropdownMenuTrigger>
              <DropdownMenuContent align="end">
                <DropdownMenuItem>View details</DropdownMenuItem>
                <DropdownMenuItem>Download invoice</DropdownMenuItem>
                <DropdownMenuSeparator />
                <DropdownMenuItem class="text-red-600">Refund</DropdownMenuItem>
              </DropdownMenuContent>
            </DropdownMenu>
          </td>
        </tr>
      ))}
    </tbody>
  </table>
  
  {/* Pagination */}
  <div class="flex items-center justify-between px-6 py-4 border-t bg-gray-50/50 dark:bg-gray-800/30 dark:border-gray-800">
    <p class="text-sm text-gray-500">Showing 1-10 of 47 results</p>
    <div class="flex items-center gap-1">
      <Button variant="outline" size="sm" disabled={page === 1}>← Prev</Button>
      <Button variant="outline" size="sm" class="w-9">1</Button>
      <Button size="sm" class="w-9">2</Button>  {/* active */}
      <Button variant="outline" size="sm" class="w-9">3</Button>
      <Button variant="outline" size="sm">Next →</Button>
    </div>
  </div>
</div>
```

---

## Rule 3: Chart Design Principles

### Chart type selection:
```
Compare categories → Bar chart (horizontal for long names)
Show trends over time → Line chart
Part of whole → Donut/Pie (max 5 segments)
Correlation → Scatter plot
Distribution → Histogram
Progress → Progress bar / Gauge
Single KPI → Big number + sparkline
```

### Color rules for charts:
```
- Max 5-6 colors (more = hard to read legend)
- Use brand color for primary series
- Gray for reference/comparison
- Red/green for negative/positive
- Same hue, different lightness for related series
```

### Recharts (most popular with React):
```tsx
import { LineChart, Line, XAxis, YAxis, CartesianGrid, Tooltip, ResponsiveContainer } from 'recharts'

<ResponsiveContainer width="100%" height={300}>
  <LineChart data={data}>
    <CartesianGrid strokeDasharray="3 3" stroke="#f0f0f0" />
    <XAxis 
      dataKey="month" 
      tick={{ fontSize: 12, fill: '#9ca3af' }}
      axisLine={false}
      tickLine={false}
    />
    <YAxis 
      tick={{ fontSize: 12, fill: '#9ca3af' }}
      axisLine={false}
      tickLine={false}
      tickFormatter={(v) => `$${v}K`}
    />
    <Tooltip 
      contentStyle={{ 
        border: '1px solid #e5e7eb',
        borderRadius: '8px',
        boxShadow: '0 4px 6px -1px rgb(0 0 0 / 0.1)'
      }}
    />
    <Line 
      type="monotone" 
      dataKey="revenue" 
      stroke="#3b82f6" 
      strokeWidth={2}
      dot={false}
      activeDot={{ r: 5 }}
    />
  </LineChart>
</ResponsiveContainer>
```

---

## Rule 4: Dashboard Layout
```html
<!-- Dashboard structure -->
<div class="space-y-6 p-6">
  
  <!-- Stats row -->
  <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-4 gap-4">
    <StatCard />
    <StatCard />
    <StatCard />
    <StatCard />
  </div>
  
  <!-- Charts row -->
  <div class="grid grid-cols-1 lg:grid-cols-3 gap-4">
    <!-- Wide chart -->
    <div class="lg:col-span-2 rounded-xl border bg-white dark:bg-gray-900 p-6">
      <h3 class="font-semibold mb-4">Revenue Over Time</h3>
      <RevenueChart />
    </div>
    
    <!-- Narrow chart/breakdown -->
    <div class="rounded-xl border bg-white dark:bg-gray-900 p-6">
      <h3 class="font-semibold mb-4">By Category</h3>
      <DonutChart />
    </div>
  </div>
  
  <!-- Table -->
  <div class="rounded-xl border bg-white dark:bg-gray-900">
    <DataTable />
  </div>
</div>
```

---

## Rule 5: List Patterns (Feed, Activity, Notifications)
```html
<!-- Activity feed -->
<div class="space-y-0 divide-y divide-gray-100 dark:divide-gray-800">
  {activities.map(activity => (
    <div class="flex items-start gap-4 py-4 px-6 hover:bg-gray-50 dark:hover:bg-gray-800/50">
      <!-- Avatar with status dot -->
      <div class="relative flex-shrink-0">
        <img class="size-9 rounded-full" src={activity.user.avatar} />
        <span class="absolute -bottom-0.5 -right-0.5 size-3.5 rounded-full border-2 border-white bg-green-500" />
      </div>
      
      <div class="flex-1 min-w-0">
        <p class="text-sm text-gray-900 dark:text-gray-100">
          <span class="font-medium">{activity.user.name}</span>{' '}
          {activity.action}
        </p>
        <p class="text-xs text-gray-500 mt-0.5">{activity.time}</p>
      </div>
      
      {activity.preview && (
        <div class="flex-shrink-0 text-xs text-gray-500 bg-gray-100 dark:bg-gray-800 
          rounded px-2 py-1 max-w-[120px] truncate">
          {activity.preview}
        </div>
      )}
    </div>
  ))}
</div>
```

---

## Rule 6: Numbers & Data Formatting
```tsx
// Always use tabular-nums for numbers in tables/charts
<span class="tabular-nums font-medium">$12,345.67</span>

// Percentage with color coding
<span class={cn("text-sm font-medium tabular-nums", 
  value > 0 ? "text-green-600" : "text-red-600")}>
  {value > 0 ? "+" : ""}{value.toFixed(1)}%
</span>

// Large number abbreviation
const formatNumber = (n: number) => {
  if (n >= 1_000_000) return `${(n/1_000_000).toFixed(1)}M`
  if (n >= 1_000) return `${(n/1_000).toFixed(1)}K`
  return n.toString()
}
```

---

## Anti-Patterns 🚫
- ❌ 3D charts (just use 2D, cleaner)
- ❌ Pie charts with > 5 segments
- ❌ Dual y-axis (confusing)
- ❌ Numbers without formatting (45231 → $45,231)
- ❌ Chart colors same as status colors (green chart ≠ success)
- ❌ Tables without pagination/virtualization on large data
- ❌ No empty/loading/error states for charts
- ❌ Dense dashboards with 10+ charts on one page
