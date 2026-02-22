# Preply Web Performance Audit

Human written summary.
See deployed [here](https://zealous-eagle-e27.notion.site/Preply-30ecbccaa2ee807fbe5ac5dd20fb6731?source=copy_link)

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

Provide reasoning for questions based on the audit. Your role is to guide developers to be successful.
Provide helpful recommendations for the future.
