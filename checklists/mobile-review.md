# Mobile Review Checklist

Review đặc biệt cho mobile app (React Native / Expo) và mobile web.

---

## ✅ Touch & Interaction
- [ ] All touch targets ≥ 44px height/width
- [ ] Primary CTA in bottom thumb zone
- [ ] No hover-only interactions (hover không tồn tại trên touch)
- [ ] Swipe gestures implemented where expected
- [ ] Long press menus nếu cần context actions

## ✅ Layout
- [ ] Safe area insets respected (notch, home indicator)
- [ ] Bottom tab bar (không phải top hamburger) cho main nav
- [ ] No horizontal scroll (trừ intentional carousels)
- [ ] Content không bị keyboard che khuất (KeyboardAvoidingView)
- [ ] Portrait AND landscape đều OK (hoặc locked to portrait)

## ✅ Typography (Mobile)
- [ ] Body text ≥ 16px (iOS default: 17px)
- [ ] Minimum tap area for text links: 44px
- [ ] Dynamic Type support (iOS)
- [ ] Text không bị clipped on small devices (SE, Mini)

## ✅ Navigation (React Native / Expo Router)
- [ ] Back button/gesture works
- [ ] Deep links handled
- [ ] Tab bar icons + labels legible
- [ ] Active tab clearly indicated
- [ ] Max 5 tabs in bottom nav

## ✅ Platform-Specific
- [ ] iOS: 
  - [ ] Uses SF Symbols / Ionicons (not Material icons)
  - [ ] Large title navigation pattern
  - [ ] Swipe-back from left edge works
  - [ ] Haptic feedback on important actions
- [ ] Android:
  - [ ] Back button (hardware) works
  - [ ] Ripple effect on touchable items
  - [ ] Status bar color set correctly

## ✅ Performance (Mobile)
- [ ] FlatList (không phải ScrollView + map) cho lists
- [ ] Images optimized (use expo-image, not Image)
- [ ] No unnecessary re-renders (useMemo, useCallback)
- [ ] Animations run on UI thread (useNativeDriver: true)

## ✅ React Native Specific
- [ ] `StyleSheet.create()` for repeated styles
- [ ] Platform.OS checks for platform-specific code
- [ ] Expo constants for device dimensions
- [ ] Font loaded before rendering (expo-font)

## ✅ Testing Devices
- [ ] Small: iPhone SE (375×667)
- [ ] Standard: iPhone 14 (390×844)
- [ ] Large: iPhone 14 Plus (430×932)
- [ ] Android: Pixel 7 (412×915)
- [ ] Tablet (optional): iPad (768×1024)

---

## Quick Mobile Gut Check
1. Can I use this one-handed on a phone?
2. Is the most important action easy to reach?
3. Does it feel like a native app?
4. Is text large enough to read without glasses?

If NO → fix before shipping.
