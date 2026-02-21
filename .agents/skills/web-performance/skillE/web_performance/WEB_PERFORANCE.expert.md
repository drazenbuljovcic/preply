# Preply Web Performance Audit

Human written summary.
See deployed on

## Performance Audit

### Large Static Assets

- https://static.preply.com/space/preply-space.089a4cd025eae9979649.js

### Question: Loading the `agora` sdk at the homepage?

- https://static.preply.com/space/scripts/agora-rtm-2.2.3.min.js
- (Don't need it during calls only?)

---

**Preply** as an application is a CLS (Client side rendered) app. And only affects the browser path so some of these issues are common.

- Optimizing **browser caches** and **deferring scripts** recommended.

## Future Opportunities

### Improve rendering path

- Reduce CLS
- Optimize loading `<scripts `

### The pattern of **graphql** loading is interesting

- Causes the above layout shifts.

## Conclusion

Asset loading audit.
Overall looks good.
LCP is looking acceptable (~1.5s) on stable networks. But throttling affects the results drastically.

---

## Glossary

| Term | Description              |
| ---- | ------------------------ |
| CLS  | Cumulative Layout Shift  |
| LCP  | Largest Contentful Paint |

---

Update: 17:41 Sat 21. Feb 2026

Find the [web_performance.audit.md](./web_performance.audit.md) here.

Provide reasoning for questions based on the audit. Your role is to guide developers to be successful.
Provide helpful recommendations for the future.
