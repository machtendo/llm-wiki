# Bundles Index

> Catalog of imported knowledge bundles and pending import requests.

---

## Imported Bundles

| Bundle | Source | Import Date | Status | Concepts | Owner |
|--------|--------|-------------|--------|----------|-------|
| [Add Bundle Name](./vendor-name/) | <URL or local path> | YYYY-MM-DD | verified/draft | N concepts | human:<id> |

## Pending Imports

| Bundle | Received | Review Priority | Assigned To | Notes |
|--------|----------|-----------------|-------------|-------|
| [Add Bundle Request](import-requests.md) | YYYY-MM-DD | high/medium/low | human:<id> | Brief reason for import |

## Bundle History

| Date | Action | Bundle | Result | Author |
|------|--------|--------|--------|--------|
| — | — | — | — | — |

---

### Guidelines for Importing Bundles

When importing a new OKF bundle:

1. **Inspect**: Read bundle's `index.md` and verify `okf_version` compatibility
2. **Validate**: Run lint check for broken links, missing frontmatter, contradictions
3. **Merge**: Either accept wholesale or selectively adopt concepts
4. **Attribute**: Preserve original `sources[]` entries; add your own `verified` entries
5. **Log**: Document in `log.md` and update this index

### Bundle Lifecycle States

| State | Meaning | Next Action |
|-------|---------|-------------|
| **pending** | Bundle received, awaiting review | Assign reviewer |
| **draft** | Being evaluated, partial acceptance | Continue validation |
| **verified** | Fully accepted, integrated into wiki | Mark complete |
| **rejected** | Declined after review | Archive to `rejected/` |

---

> Last updated: 2026-10-01 | [Return to root](Knowledge%20Base/index.md)
