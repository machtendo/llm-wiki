# Bundle Import Requests

> Track incoming bundles awaiting review and approval.

---

## Pending Requests

| Bundle Name | Submitted By | Date Received | Priority | Reason | Decision |
|-------------|--------------|---------------|----------|--------|----------|
| [Request #1](./requests/request-001.md) | external-contact@vendor.com | 2026-10-XX | medium | Need financial metrics definitions | pending |

---

### Request Entry Template

When receiving a new bundle, create a request entry:

```markdown
## Request #001 - [Bundle Name]

- **Submitted By**: contact@vendor.com
- **Date Received**: YYYY-MM-DD
- **Priority**: high/medium/low
- **Reason for Request**: Why do we need this bundle?
- **Expected Benefits**: What concepts/values will it provide?
- **Dependencies**: Any existing bundles this depends on?
- **Risk Assessment**: Low/medium/high (security, IP, conflicts)
- **Assigned Reviewer**: human:<id>
- **Decision Deadline**: YYYY-MM-DD
- **Notes**: Additional context for reviewers
````

### Decision Criteria

|Factor|Considerations|
|---|---|
|**Quality**|Does it have complete `sources[]` and `verified` entries?|
|**Relevance**|Does it fill a documented knowledge gap?|
|**Conflicts**|Will it contradict existing wiki concepts?|
|**Maintenance**|Who updates this bundle over time?|
|**IP/Rights**|Are there licensing or attribution requirements?|

---
> Last updated: 2026-10-01 | [Return to root]