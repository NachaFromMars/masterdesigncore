# 06 — Mobile Patterns

> SOURCE: Apple Human Interface Guidelines, Material Design 3, React Native / Expo best practices

---

## Core Principle
Mobile design = **thumb-friendly**, **content-first**, **platform-native feel**. Context khác desktop.

---

## Rule 1: Touch Target Size (Critical!)
- Minimum: **44×44px** (Apple HIG) / **48×48dp** (Material)
- Preferred: 48-56px height for primary actions

```html
<!-- Web mobile button -->
<button class="min-h-[44px] min-w-[44px] px-4 flex items-center justify-center">

<!-- React Native -->
<TouchableOpacity style={{ minHeight: 44, padding: 12 }}>

<!-- Expo -->
<Pressable style={{ minHeight: 48, paddingHorizontal: 16 }}>
```

**Anti-pattern:** Icon buttons < 24px, link text only, no touch area expansion.

---

## Rule 2: Thumb Zone Optimization
```
Phone screen thumb zones:
┌─────────────────┐
│  ☠️ Hard reach   │  ← Avoid critical actions
│  ⚠️ Medium reach │  ← Secondary actions OK
│  ✅ Easy reach   │  ← Primary actions here!
│  ✅ Easy reach   │
│  ✅ Easy reach   │
└─────────────────┘
         ▲ Bottom = golden zone
```

**Rules:**
- Primary actions (FAB, CTA button) → bottom of screen
- Navigation → bottom tab bar (not top hamburger)
- Destructive actions → NOT in thumb zone (need intention)

---

## Rule 3: iOS vs Android Patterns

### iOS (Apple HIG)
- Navigation: Back button top-left + swipe from edge
- Tab bar: 49px height, max 5 tabs
- Safe area: respect `safeAreaInsets` (`pb-safe` in Expo)
- Typography: SF Pro system font
- Modals: slide up from bottom
- List: swipe to delete, right chevron →

### Android (Material Design 3)
- Navigation: Bottom nav OR Navigation Rail (tablet)
- FAB: bottom-right for primary action
- Typography: Google Sans / Roboto
- Dialogs: centered overlay
- Cards: 12dp corner radius

### React Native / Expo cross-platform:
```tsx
import { Platform, StyleSheet } from 'react-native'

const styles = StyleSheet.create({
  button: {
    height: Platform.OS === 'ios' ? 44 : 48,
    paddingHorizontal: 16,
    borderRadius: Platform.OS === 'ios' ? 10 : 12,
  }
})
```

---

## Rule 4: Safe Areas (Expo)
```tsx
import { SafeAreaView } from 'react-native-safe-area-context'
import { useSafeAreaInsets } from 'react-native-safe-area-context'

// Simple
<SafeAreaView className="flex-1 bg-white">
  <Content />
</SafeAreaView>

// Manual insets (NativeWind)
function BottomSheet() {
  const insets = useSafeAreaInsets()
  return (
    <View style={{ paddingBottom: insets.bottom + 16 }}>
      <ActionButton />
    </View>
  )
}
```

---

## Rule 5: Typography Mobile Scale
```
iOS Dynamic Type reference:
- Caption 2: 11px
- Caption 1: 12px  
- Footnote: 13px
- Subheadline: 15px
- Callout: 16px
- Body: 17px ← default body
- Headline: 17px semibold
- Title 3: 20px
- Title 2: 22px
- Title 1: 28px
- Large Title: 34px
```

**NativeWind / Expo equivalent:**
```tsx
<Text className="text-base">Body (16-17px)</Text>
<Text className="text-lg font-semibold">Headline</Text>
<Text className="text-2xl font-bold">Title</Text>
<Text className="text-sm text-gray-500">Caption</Text>
```

---

## Rule 6: Gestures
```
Common gesture patterns:
- Swipe left/right: navigation, dismiss, actions
- Swipe up/down: scroll, bottom sheet
- Long press: context menu, select mode
- Pinch: zoom
- Double tap: like, zoom-to-fit

Expo Gesture Handler:
```
```tsx
import { Gesture, GestureDetector } from 'react-native-gesture-handler'

const swipe = Gesture.Pan()
  .onEnd(({ translationX }) => {
    if (translationX < -100) navigateNext()
    if (translationX > 100) navigatePrev()
  })

<GestureDetector gesture={swipe}>
  <Animated.View>{content}</Animated.View>
</GestureDetector>
```

---

## Rule 7: Bottom Sheet Pattern
```tsx
// @gorhom/bottom-sheet
import BottomSheet, { BottomSheetView } from '@gorhom/bottom-sheet'

const snapPoints = useMemo(() => ['25%', '50%', '90%'], [])

<BottomSheet
  ref={bottomSheetRef}
  snapPoints={snapPoints}
  enablePanDownToClose={true}
  backgroundStyle={{ backgroundColor: '#fff' }}
>
  <BottomSheetView className="px-4 pb-safe">
    <SheetContent />
  </BottomSheetView>
</BottomSheet>
```

---

## Rule 8: Navigation (Expo Router)
```tsx
// Tab navigation
// app/(tabs)/_layout.tsx
import { Tabs } from 'expo-router'
import { House, Search, Bell, User } from 'lucide-react-native'

<Tabs screenOptions={{ tabBarActiveTintColor: '#3b82f6' }}>
  <Tabs.Screen name="index" options={{
    title: 'Home',
    tabBarIcon: ({ color }) => <House size={22} color={color} />
  }} />
</Tabs>

// Stack navigation with shared element
import { Stack } from 'expo-router'
<Stack>
  <Stack.Screen name="[id]" options={{ headerShown: false }} />
</Stack>
```

---

## Rule 9: Lists & Virtualization
```tsx
// FlatList (always for long lists)
<FlatList
  data={items}
  keyExtractor={item => item.id}
  renderItem={({ item }) => <ItemCard item={item} />}
  contentContainerStyle={{ paddingBottom: insets.bottom + 16 }}
  ItemSeparatorComponent={() => <View className="h-px bg-gray-100" />}
  onEndReached={loadMore}
  onEndReachedThreshold={0.5}
/>
```

---

## Anti-Patterns 🚫
- ❌ Top navigation bar only (hard to reach)
- ❌ Touch targets < 44px
- ❌ No safe area handling (content under notch/home indicator)
- ❌ Tap = hover (mobile has no hover!)
- ❌ Desktop navigation patterns (hamburger menu → use tabs)
- ❌ Scroll inside scroll (nested scrollviews)
- ❌ Dense tables without wrapping/truncation
