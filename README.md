# Preply

Inverview prep.
Letter of motivation.

---

See detailed usage guide on
[Notion](https://zealous-eagle-e27.notion.site/Preply-30ecbccaa2ee807fbe5ac5dd20fb6731)

---

## skillE - AI Native Agent System

skillE is an AI Native Agentic Engineering system that provides specialized expertise for web performance analysis and optimization. (https://agentskills.io/home)

<img src="./Screenshot 2026-02-21 at 18.26.25.png" alt="Opencode" />

### What is skillE?

skillE is an agentic AI system that uses specialized experts to analyze and improve web performance. It leverages large language models with domain-specific knowledge to audit websites, identify performance issues, and provide actionable recommendations.

### Quick Start for Developers New to AI Native Agentic Engineering

If you're unfamiliar with AI Native Agentic Engineering, follow these steps to get started:

#### 1. Install opencode (Recommended AI Harness)

opencode is an interactive CLI tool that helps you work with AI Native Agentic Systems like skillE. It provides a smooth onboarding experience for developers new to agentic engineering.

```bash
# Install opencode via npm
npm install -g opencode

# Or via Homebrew on macOS
brew install opencode
```

#### 2. Verify Installation

```bash
opencode --version
```

#### 3. Run skillE

Once opencode is installed, you can interact with skillE:

```bash
opencode

$ /web_performance <Prompt>

```

Then describe what you need help with, for example:
"Analyze the web performance of https://example.com and save the results to WEB_PERFORMANCE.expert.md"

### Available Skills

- **Web Performance**: Analyzes website performance metrics, identifies bottlenecks, and provides optimization recommendations

### Project Structure

```
.agents/
├── skills/
│   └── web-performance/
│       ├── SKILL.md           # Skill definition
│       └── skillE/
│           └── web_performance/
│               ├── WEB_PERFORMANCE.expert.md    # Expert knowledge base
│               └── web_performance.audit.md      #
```

Audit results:

```
# Lighthouse Performance Audit Report
**URL:** https://preply.com/en/home  **Date:** 2026-02-21  **Lighthouse Version:** 13.0.1
---
## Overall Scores
| Category | Score ||----------|-------|| **Performance** | **0.27 (27/100)** - Poor || Accessibility | 0.94 (94/100) || Best Practices | 0.54 (54/100) || SEO | 0.75 (75/100) |
---
## Core Web Vitals
| Metric | Value | Target | Status ||--------|-------|--------|--------|| First Contentful Paint (FCP) | 1.8s | < 1.8s | Needs Improvement || **Largest Contentful Paint (LCP)** | **22.9s** | < 2.5s | Poor || **Total Blocking Time (TBT)** | **2,520ms** | < 200ms | Poor || Cumulative Layout Shift (CLS) | 0.192 | < 0.1 | Needs Improvement || **Speed Index (SI)** | **10.2s** | < 3.4s | Poor || Time to Interactive (TTI) | 38.3s | < 3.8s | Poor || Max Potential FID | 820ms | < 100ms | Poor |
---
## Key Issues
### Critical Performance Problems
1. **LCP: 22.9s** - The largest content element takes extremely long to render. This is likely caused by:   - Large images not being optimized   - Slow server response time   - Render-blocking resources
2. **TBT: 2,520ms** - Heavy JavaScript execution is blocking the main thread for over 2.5 seconds. This indicates:   - Large JavaScript bundles   - Inefficient third-party scripts   - Missing code splitting
3. **Speed Index: 10.2s** - Page loads visually very slowly, indicating significant delays in rendering content above the fold.
4. **Time to Interactive: 38.3s** - Users cannot interact with the page for over 38 seconds.
### Additional Issues Detected
- Browser errors logged to console- Uses deprecated APIs- Uses third-party cookies- Missing source maps for large JavaScript- Elements use prohibited ARIA attributes- Document does not have a main landmark- Document does not have a meta description- Links do not have descriptive text- Links are not crawlable- Page prevented back/forward cache restoration
---
## Recommendations
### High Priority
1. **Reduce JavaScript Execution Time**   - Implement code splitting to load only required code   - Tree-shake unused code   - Defer non-critical JavaScript
2. **Optimize LCP**   - Use modern image formats (WebP, AVIF)   - Implement lazy loading for below-fold images   - Preload hero images   - Optimize server response time
3. **Eliminate Render-Blocking Resources**   - Defer non-critical CSS   - Async/defer JavaScript loading   - Inline critical CSS
### Medium Priority
4. **Reduce DOM Size**   - Minimize nested elements   - Remove unnecessary wrappers
5. **Optimize Third-Party Scripts**   - Delay non-essential third-party scripts   - Use intersection observer for lazy loading   - Audit third-party script necessity
6. **Improve CLS**   - Add explicit width/height to images   - Reserve space for dynamic content
### Low Priority
7. **Add Semantic HTML**   - Add main landmark   - Add meta description
8. **Fix Link Text**   - Use descriptive link text
---
## Run Warnings
> Chrome extensions negatively affected this page's load performance. Try auditing the page in incognito mode or from a Chrome profile without extensions.
> There may be stored data affecting loading performance in this location: IndexedDB. Audit this page in an incognito window to prevent those resources from affecting your scores.
---
*Note: This audit was run with Chrome extensions enabled, which may have negatively impacted performance scores. Re-audit in incognito mode for more accurate results.*

```

### Tips for Success

1. **Start with clear goals**: When asking skillE to analyze something, be specific about what you want to achieve
2. **Iterate**: AI agents work best through iterative refinement - start with a broad analysis, then dive deeper into specific areas
3. **Review outputs**: Always review the generated expert files and audits for accuracy
4. **Use opencode**: The opencode CLI provides an interactive experience that guides you through working with AI agents
