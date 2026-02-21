# Lighthouse Performance Audit Report

**URL:** https://preply.com/en/home  
**Date:** 2026-02-21  
**Lighthouse Version:** 13.0.1

---

## Overall Scores

| Category | Score |
|----------|-------|
| **Performance** | **0.27 (27/100)** - Poor |
| Accessibility | 0.94 (94/100) |
| Best Practices | 0.54 (54/100) |
| SEO | 0.75 (75/100) |

---

## Core Web Vitals

| Metric | Value | Target | Status |
|--------|-------|--------|--------|
| First Contentful Paint (FCP) | 1.8s | < 1.8s | Needs Improvement |
| **Largest Contentful Paint (LCP)** | **22.9s** | < 2.5s | Poor |
| **Total Blocking Time (TBT)** | **2,520ms** | < 200ms | Poor |
| Cumulative Layout Shift (CLS) | 0.192 | < 0.1 | Needs Improvement |
| **Speed Index (SI)** | **10.2s** | < 3.4s | Poor |
| Time to Interactive (TTI) | 38.3s | < 3.8s | Poor |
| Max Potential FID | 820ms | < 100ms | Poor |

---

## Key Issues

### Critical Performance Problems

1. **LCP: 22.9s** - The largest content element takes extremely long to render. This is likely caused by:
   - Large images not being optimized
   - Slow server response time
   - Render-blocking resources

2. **TBT: 2,520ms** - Heavy JavaScript execution is blocking the main thread for over 2.5 seconds. This indicates:
   - Large JavaScript bundles
   - Inefficient third-party scripts
   - Missing code splitting

3. **Speed Index: 10.2s** - Page loads visually very slowly, indicating significant delays in rendering content above the fold.

4. **Time to Interactive: 38.3s** - Users cannot interact with the page for over 38 seconds.

### Additional Issues Detected

- Browser errors logged to console
- Uses deprecated APIs
- Uses third-party cookies
- Missing source maps for large JavaScript
- Elements use prohibited ARIA attributes
- Document does not have a main landmark
- Document does not have a meta description
- Links do not have descriptive text
- Links are not crawlable
- Page prevented back/forward cache restoration

---

## Recommendations

### High Priority

1. **Reduce JavaScript Execution Time**
   - Implement code splitting to load only required code
   - Tree-shake unused code
   - Defer non-critical JavaScript

2. **Optimize LCP**
   - Use modern image formats (WebP, AVIF)
   - Implement lazy loading for below-fold images
   - Preload hero images
   - Optimize server response time

3. **Eliminate Render-Blocking Resources**
   - Defer non-critical CSS
   - Async/defer JavaScript loading
   - Inline critical CSS

### Medium Priority

4. **Reduce DOM Size**
   - Minimize nested elements
   - Remove unnecessary wrappers

5. **Optimize Third-Party Scripts**
   - Delay non-essential third-party scripts
   - Use intersection observer for lazy loading
   - Audit third-party script necessity

6. **Improve CLS**
   - Add explicit width/height to images
   - Reserve space for dynamic content

### Low Priority

7. **Add Semantic HTML**
   - Add main landmark
   - Add meta description

8. **Fix Link Text**
   - Use descriptive link text

---

## Run Warnings

> Chrome extensions negatively affected this page's load performance. Try auditing the page in incognito mode or from a Chrome profile without extensions.

> There may be stored data affecting loading performance in this location: IndexedDB. Audit this page in an incognito window to prevent those resources from affecting your scores.

---

*Note: This audit was run with Chrome extensions enabled, which may have negatively impacted performance scores. Re-audit in incognito mode for more accurate results.*
