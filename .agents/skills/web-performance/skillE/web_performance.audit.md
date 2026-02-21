# Lighthouse Performance Audit Report

**URL:** https://preply.com/en/home  
**Date:** 2026-02-21  
**Lighthouse Version:** 13.0.1  
**Test Conditions:** Chrome with extensions enabled (may impact results)

---

## Overall Scores

| Category        | Score                    | Reasoning |
| --------------- | ------------------------ | --------- |
| **Performance** | **0.27 (27/100)** - Poor | A score below 50 indicates severe performance issues. This score is primarily dragged down by extremely poor LCP (22.9s), TBT (2,520ms), and Speed Index (10.2s). These metrics directly correlate with poor user experience and higher bounce rates. |
| Accessibility   | 0.94 (94/100)            | Good score - the page is mostly accessible, but has minor issues with ARIA and landmarks. |
| Best Practices  | 0.54 (54/100)            | Below average. The score is impacted by deprecated APIs, third-party cookies, missing source maps, and console errors. |
| SEO             | 0.75 (75/100)            | Moderate score. Issues include missing meta description (impacts click-through rates) and non-crawlable links. |

---

## Core Web Vitals

| Metric                             | Value       | Target  | Status            | Reasoning |
| ---------------------------------- | ----------- | ------- | ----------------- | --------- |
| First Contentful Paint (FCP)       | 1.8s        | < 1.8s  | Needs Improvement | At the threshold (1.8s). Users see initial content quickly, but the page still feels slow. Slightly above this would severely impact perceived performance. |
| **Largest Contentful Paint (LCP)** | **22.9s**   | < 2.5s  | **Poor**          | **Critical issue.** LCP measures when the largest content element becomes visible. 22.9s means users stare at a blank/loading screen for nearly 23 seconds. This is often caused by: large hero images not optimized, blocking JS delaying image load, slow server response, or missing image preloads. |
| **Total Blocking Time (TBT)**      | **2,520ms** | < 200ms | **Poor**          | **Critical issue.** TBT measures main thread blocking time during load. 2.5s of blocking severely delays interactivity. Caused by: large JS bundles, main thread work from third-party scripts (analytics, chat widgets), synchronous operations, and insufficient code splitting. |
| Cumulative Layout Shift (CLS)      | 0.192       | < 0.1   | Needs Improvement | Page shifts during load, causing content to move unexpectedly. This frustrates users and can cause accidental clicks. Typically caused by images without dimensions, dynamic content injecting above existing content, or late-loading fonts. |
| **Speed Index (SI)**               | **10.2s**   | < 3.4s  | **Poor**          | **Critical issue.** SI measures visual completeness over time. At 10.2s, the page appears visually incomplete for far too long. This correlates directly with poor LCP and heavy render-blocking resources. |
| Time to Interactive (TTI)          | 38.3s       | < 3.8s  | Poor              | Users cannot reliably interact with the page for over 38 seconds. This is a compounding result of the TBT and JS execution issues. |
| Max Potential FID                  | 820ms       | < 100ms | Poor              | Similar to TBT, this measures input delay. Users trying to click/interact early will experience significant lag. |

---

## Key Issues

### Critical Performance Problems

1. **TBT: 2,520ms** - Heavy JavaScript execution is blocking the main thread for over 2.5 seconds. This indicates:
   - Large JavaScript bundles (main cause based on TBT)
   - Inefficient third-party scripts (likely chat widgets, analytics, A/B testing tools)
   - Missing code splitting (all JS loads upfront instead of on-demand)
   - **Why this matters:** Every millisecond of blocking prevents users from clicking, typing, or interacting. At 2.5s+ blocking, users may think the page is broken and leave.

2. **Speed Index: 10.2s** - Page loads visually very slowly, indicating significant delays in rendering content above the fold.
   - **Why this matters:** Speed Index directly correlates with bounce rates. Users form an opinion about your site within seconds. At 10.2s, most users will have abandoned the page before it even looks complete.

3. **LCP: 22.9s** - The largest content element (likely hero image or text) takes nearly 23 seconds to render.
   - **Why this matters:** LCP is a Google ranking factor and directly impacts user perception. A 22.9s LCP means users see nothing meaningful for almost half a minute.

### Additional Issues Detected (Lighthouse Findings)

| Issue | Reasoning |
| ----- | --------- |
| Preconnect tags not set | Missing `link rel="preconnect"` for critical third-party origins (e.g., CDNs, analytics, fonts). This delays connection setup, adding latency to subsequent resource requests. |
| Browser errors logged to console | Indicates JavaScript runtime errors that may affect functionality and waste main thread time on error handling. |
| Uses deprecated APIs | May cause compatibility issues with future browser versions and often have performance inefficiencies. |
| Uses third-party cookies | Chrome is phasing out third-party cookies; this affects privacy compliance and future browser support. |
| Missing source maps for large JavaScript | Makes debugging difficult in production; source maps help identify performance issues in minified code. |
| Elements use prohibited ARIA attributes | Accessibility compliance issue; invalid ARIA can confuse screen readers. |
| Document does not have a main landmark | Accessibility issue; screen reader users cannot easily navigate to main content. |
| Document does not have a meta description | SEO issue; missing meta descriptions reduce click-through rates from search results. |
| Links do not have descriptive text | Accessibility and SEO issue; users/screen readers cannot understand link purpose. |
| Links are not crawlable | SEO issue; search engines cannot properly index all page content. |
| Page prevented back/forward cache restoration | Performance issue; users experience slower navigation when using browser back/forward buttons. |

---

## Recommendations

### High Priority

1. **Reduce JavaScript Execution Time**
   - **Why:** TBT of 2,520ms is the primary performance blocker. Every 100ms of JS reduction improves TBT directly.
   - **How:**
     - Implement code splitting to load only required code (reduce initial bundle)
     - Tree-shake unused code (use ES modules, remove dead code)
     - Defer non-critical JavaScript (use `defer`/`async` attributes)
     - **Expected impact:** Could reduce TBT by 50-80% based on current severity.

2. **Optimize LCP**
   - **Why:** LCP at 22.9s is catastrophic for user experience and SEO. Fixing this alone could improve the overall performance score significantly.
   - **How:**
     - Use modern image formats (WebP, AVIF) - 30-50% smaller than JPEG/PNG
     - Implement lazy loading for below-fold images (saves bandwidth, speeds initial render)
     - Preload hero images using `<link rel="preload" as="image">` 
     - Optimize server response time (critical path optimization, CDN, caching)
     - **Expected impact:** Could bring LCP under 3s if hero image is properly optimized and preloaded.

3. **Eliminate Render-Blocking Resources**
   - **Why:** Render-blocking resources delay FCP and LCP. Each blocking resource adds to the time before anything visible appears.
   - **How:**
     - Defer non-critical CSS (load after initial paint)
     - Async/defer JavaScript loading (non-blocking script execution)
     - Inline critical CSS (inline styles needed for above-fold content in HTML)
     - **Expected impact:** Improves FCP, LCP, and Speed Index simultaneously.

### Medium Priority

4. **Optimize Third-Party Scripts**
   - **Why:** Third-party scripts (chat, analytics, A/B testing) often cause massive TBT spikes. They run on your page but you don't control them.
   - **How:**
     - Delay non-essential third-party scripts (load after user interaction)
     - Use intersection observer for lazy loading (only load when scrolled into view)
     - Audit third-party script necessity (question every script - do you really need it?)
     - **Expected impact:** Could reduce TBT by 30-60% if heavy third-party scripts are delayed.

5. **Improve CLS**
   - **Why:** Layout shifts frustrate users and cause accidental clicks. Google considers CLS in rankings.
   - **How:**
     - Add explicit width/height to all images (reserve space before image loads)
     - Reserve space for dynamic content (use min-height, skeleton loaders)
     - Use `font-display: swap` or optional to prevent font-induced shifts
     - **Expected impact:** Could bring CLS under 0.1 with these fixes.

### Low Priority

6. **Add Semantic HTML & SEO Improvements**
   - **Why:** Accessibility and SEO issues don't impact performance scores directly but affect user experience and search rankings.
   - **How:**
     - Add main landmark (`<main>` element)
     - Add meta description
     - Fix link text (use descriptive anchor text)
     - Ensure links are crawlable (avoid `rel="nofollow"` unless necessary)

---

## Run Warnings

> Chrome extensions negatively affected this page's load performance. Try auditing the page in incognito mode or from a Chrome profile without extensions.

> There may be stored data affecting loading performance in this location: IndexedDB. Audit this page in an incognito window to prevent those resources from affecting your scores.

---

_Note: This audit was run with Chrome extensions enabled, which may have negatively impacted performance scores. Re-audit in incognito mode for more accurate results._
