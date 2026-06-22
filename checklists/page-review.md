# Page Review Checklist — Before Shipping

Run this checklist trước khi ship bất kỳ page nào.

---

## ✅ Visual Hierarchy
- [ ] H1 > H2 > H3 > body — rõ ràng không?
- [ ] Heading font weight: bold/semibold
- [ ] Body text: đủ contrast (gray-700+ on white)
- [ ] Primary CTA nổi bật nhất trên trang
- [ ] Không có 2 elements cùng visual weight khi chúng không bằng nhau

## ✅ Typography
- [ ] Font size hợp lý (body ≥ 14px, phần lớn là 16px)
- [ ] Line-height body: `leading-relaxed` (1.6+)
- [ ] Heading line-height: `leading-tight` (1.2)
- [ ] Max-width cho prose: `max-w-prose` hoặc `max-w-2xl`
- [ ] Không có text quá dài (> 80 chars/line) 

## ✅ Color & Contrast
- [ ] Text trên background: contrast ≥ 4.5:1
- [ ] Large text: contrast ≥ 3:1
- [ ] UI components (borders, icons): ≥ 3:1
- [ ] Không dùng màu sắc làm signal duy nhất

## ✅ Spacing
- [ ] Consistent spacing scale (multiples of 4px)
- [ ] Generous whitespace — không cramped
- [ ] Related items gần nhau, unrelated items xa nhau
- [ ] Sections có padding đủ (py-12 minimum for sections)

## ✅ Dark Mode
- [ ] Mọi màu đều có `dark:` variant
- [ ] Background: `dark:bg-gray-950` hoặc `dark:bg-gray-900`
- [ ] Text: `dark:text-white` hoặc `dark:text-gray-100`
- [ ] Borders: `dark:border-gray-800`
- [ ] Cards: `dark:bg-gray-900`
- [ ] Shadows invisible in dark? → Use ring instead

## ✅ Responsive
- [ ] Tested at: 375px (iPhone SE), 768px (iPad), 1280px (desktop)
- [ ] No horizontal scroll on mobile
- [ ] Navigation accessible on mobile
- [ ] Text readable on small screens
- [ ] Touch targets ≥ 44px on mobile

## ✅ Interactive States
- [ ] Buttons: hover + active + focus + disabled
- [ ] Links: hover + visited (if needed) + focus
- [ ] Inputs: focus + error + disabled + placeholder
- [ ] All focus states visible (not just removed)

## ✅ Loading & Empty States
- [ ] Loading state implemented (skeleton or spinner)
- [ ] Empty state with message + optional CTA
- [ ] Error state with message + retry option
- [ ] Skeleton matches actual content shape

## ✅ Accessibility
- [ ] Skip navigation link at top
- [ ] Heading levels sequential (h1 → h2 → h3, no skipping)
- [ ] All images have alt text
- [ ] Icon buttons have aria-label
- [ ] Form inputs have labels
- [ ] Color not the only indicator

## ✅ Performance
- [ ] Images have width/height set (prevents layout shift)
- [ ] Images are properly sized (not 5MB hero images)
- [ ] No layout shift (CLS) during loading
- [ ] Fonts loaded (no FOUT — flash of unstyled text)

## ✅ Content
- [ ] Page title set (`<title>`)
- [ ] Meta description set
- [ ] OG image set (for social sharing)
- [ ] Actual content (no lorem ipsum in production)
- [ ] Dates formatted consistently
- [ ] Numbers formatted (1234 → 1,234)

---

## Quick Visual Scan (30 second check)
Look at the page from arm's length. Ask:
1. Do I immediately know what this page is about?
2. Is the primary CTA obvious?
3. Does anything hurt my eyes?
4. Does it look professional?

If NO to any → find the problem.
