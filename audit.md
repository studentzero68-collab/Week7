# Responsiveness Audit — Mzansi Eats

**Audited by:** Mukelani N. Sindana  
**Date:** 12 June 2026  
**Page audited:** index.html — Mzansi Eats Food Delivery  
**Screen sizes tested:** 375px (mobile), 768px (tablet), 1280px (desktop)

---

## Issue 1 — Hero image has a fixed width of 1200px

**Where:** `.hero img`  
**Screen sizes affected:** 375px, 768px  
**What happens:** The image overflows the viewport on mobile and tablet, causing horizontal scrolling across the whole page.

**Current code:**
```css
.hero img { width: 1200px; height: 400px; }
```

**Fix applied:**
```css
.hero img { width: 100%; height: 400px; object-fit: cover; }
```

**Why this works:** Setting width to 100% makes the image scale with the viewport instead of sitting at a fixed 1200px.

---

## Issue 2 — Card grid uses fixed column widths

**Where:** `.card-grid`  
**Screen sizes affected:** 375px, 768px  
**What happens:** The grid forces 4 columns of 250px each which is 1000px total. On smaller screens the cards overflow and get cut off.

**Current code:**
```css
.card-grid { grid-template-columns: repeat(4, 250px); }
```

**Fix applied:**
```css
.card-grid { grid-template-columns: repeat(auto-fit, minmax(220px, 1fr)); }
```

**Why this works:** `auto-fit` with `minmax` lets the grid decide how many columns fit based on the available space — 4 on desktop, 2 on tablet, 1 on mobile.

---

## Issue 3 — Contact section has a fixed width of 800px

**Where:** `.contact-inner`  
**Screen sizes affected:** 375px, 768px  
**What happens:** The contact form container is always 800px wide so it overflows the screen on mobile and causes horizontal scrolling.

**Current code:**
```css
.contact-inner { width: 800px; margin: 0 auto; }
```

**Fix applied:**
```css
.contact-inner { width: 100%; max-width: 800px; margin: 0 auto; padding: 0 20px; }
```

**Why this works:** `max-width` keeps the 800px cap on large screens but lets it shrink on smaller ones. The padding stops content from touching the screen edges.

---

## Issue 4 — Contact grid stays 2 columns on mobile

**Where:** `.contact-grid`  
**Screen sizes affected:** 375px  
**What happens:** The form and contact details sit side by side even on small screens making both columns too narrow to read or use comfortably.

**Current code:**
```css
.contact-grid { grid-template-columns: 1fr 1fr; }
```

**Fix applied:**
```css
.contact-grid { grid-template-columns: 1fr 1fr; }

@media (max-width: 600px) {
  .contact-grid { grid-template-columns: 1fr; }
}
```

**Why this works:** On screens under 600px the two columns stack into one so the form takes full width and is actually usable on a phone.

---

## Issue 5 — Header and footer have fixed horizontal padding

**Where:** `header`, `footer`  
**Screen sizes affected:** 375px  
**What happens:** Both header and footer have `padding: 16px 40px` which leaves very little room for content on a small screen. The nav links wrap awkwardly and the logo text gets cramped.

**Current code:**
```css
header { padding: 16px 40px; }
footer { padding: 24px 40px; }
```

**Fix applied:**
```css
@media (max-width: 600px) {
  header { padding: 12px 16px; flex-direction: column; gap: 10px; }
  footer { padding: 16px; flex-direction: column; gap: 8px; text-align: center; }
}
```

**Why this works:** Reducing padding on small screens gives content more room and stacking the header and footer vertically stops the content from getting squashed.

---

## Summary of fixes

| Issue | Element | Fix |
|---|---|---|
| Hero image overflow | `.hero img` | Changed to `width: 100%` |
| Card grid overflow | `.card-grid` | Used `auto-fit` with `minmax` |
| Contact container overflow | `.contact-inner` | Changed to `max-width` with padding |
| Contact grid too narrow | `.contact-grid` | Added media query to stack on mobile |
| Header and footer cramped | `header`, `footer` | Added mobile media query with reduced padding |