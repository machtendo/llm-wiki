---
type: Reference
title: Bundle Rejection Record - [Bundle Name]
description: Formal record of why this bundle was declined for integration.
tags: [bundle, rejection, archive]
generated:
  by: human:<reviewer-id>
  at: YYYY-MM-DDTHH:MM:SSZ
status: stable
sources:
  - id: original-bundle
    resource: ../vendor-name/
    title: [Original Bundle Name]
    author: vendor/contact-name
    last_modified: YYYY-MM-DDT00:00:00Z
---

# Bundle Rejection Record

## Bundle Information

| Field | Value |
|-------|-------|
| **Bundle Name** | [Vendor/Product Name] |
| **Source** | [URL or local path where obtained] |
| **Date Received** | YYYY-MM-DD |
| **Date Rejected** | YYYY-MM-DD |
| **Requested By** | [Name/Team requesting import] |
| **Reviewer** | human:<id> |

## Decision Summary

| Decision | Reason Category | Severity |
|----------|-----------------|----------|
| ❌ **Rejected** | <Quality / Conflict / Security / Redundancy / Other> | <Low / Medium / High> |

---

## Detailed Reason for Rejection

### Primary Reason

<Write a clear, specific explanation of why this bundle was declined. Be factual and actionable.>

### Contributing Factors

<If multiple issues contributed to the decision, list them here.>

---

## Technical Issues (If Applicable)

| Issue Type | Details | Fixable? |
|------------|---------|----------|
| **Missing Frontmatter** | <e.g., "3 files lack `type` field"> | Yes / No |
| **Broken Links** | <e.g., "5 cross-bundle links point outside scope"> | Yes / No |
| **Missing Attestations** | <e.g., "Computed values lack executor/attester contracts"> | Yes / No |
| **Conflicting Definitions** | <e.g., "Revenue metric disagrees with wiki/finance/revenue.md"> | Partial |
| **Staleness** | <e.g., "All `stale_after` dates in past"> | Yes |
| **Other** | <Describe> | <Yes / No> |

---

## Security & Compliance Review

| Concern | Status |
|---------|--------|
| **License Compatible** | ☐ Yes ☐ No ☐ Not Assessed |
| **No PII/Sensitive Data** | ☐ Yes ☐ No ☐ Not Assessed |
| **Verified Source Authority** | ☐ Yes ☐ No ☐ Not Assessed |
| **No Malicious Content** | ☐ Yes ☐ No ☐ Not Assessed |

---

## Alternative Actions Taken

| Action | Description | Date |
|--------|-------------|------|
| <Action Type> | <What was done instead> | YYYY-MM-DD |

Examples:
- Built equivalent concepts internally
- Found existing bundle with overlapping content
- Waited for vendor to resolve identified issues
- Requested modified subset of content

---

## Appeal Process

If this rejection should be reconsidered:

| Step | Action | Owner |
|------|--------|-------|
| 1 | Address primary reason above | human:<id> |
| 2 | Submit revised bundle or partial import | requester@org.com |
| 3 | Re-evaluation timeline | YYYY-MM-DD |

---

## Related Documents

| Document | Link | Notes |
|----------|------|-------|
| Original Request | `../requests/request-XXX.md` | Initial import request |
| Correspondence | [Email/Slack Thread] | Discussion trail |
| Similar Accepted Bundle | `../vendor-good/` | Better alternative |
| Internal Replacement | `wiki/<replacement>.md` | If we built our own |

---

## Sign-Off

| Role | Name | Date | Signature |
|------|------|------|-----------|
| **Primary Reviewer** | <human:<id>> | YYYY-MM-DD | |
| **Secondary Approver** (if required) | <human:<id>> | YYYY-MM-DD | |

---

> **Note:** This rejection record is kept permanently for audit purposes. Do not delete. If the bundle is later accepted, move this file to `archives/` and update `bundles/index.md` accordingly.

---

### Common Rejection Reasons (Reference)

Use these categories for consistency:

| Category | Definition | Example |
|----------|------------|---------|
| **Quality** | Missing required fields, poor provenance tracking | "No `verified` entries on any computation" |
| **Conflict** | Contradicts existing wiki concepts | "Revenue formula disagrees with our definition" |
| **Security** | Unauthorized source, suspicious content | "Cannot verify bundle origin authenticity" |
| **Redundancy** | Existing bundle covers same ground | "We already have vendor-X metrics bundle" |
| **Staleness** | Outdated content beyond acceptable threshold | "`stale_after` dates from 2024, no updates" |
| **Scope** | Content outside our domain needs | "Bundle focuses on HR; we need finance only" |
| **Compliance** | Licensing/legal barriers | "Proprietary license restricts redistribution" |

---

> Last updated: YYYY-MM-DD | [Return to bundles index](Knowledge%20Base/index.md)
