---
type: Reference
title: Bundle Acceptance Record - [Bundle Name]
description: Formal record of approved bundle integration into the knowledge base.
tags: [bundle, acceptance, integration]
generated:
  by: human:<approver-id>
  at: YYYY-MM-DDTHH:MM:SSZ
status: stable
sources:
  - id: original-bundle
    resource: ../vendor-name/
    title: [Original Bundle Name]
    author: vendor/contact-name
    last_modified: YYYY-MM-DDT00:00:00Z
  - id: import-request
    resource: ../requests/request-XXX.md
    title: Original Import Request
    author: requester@org.com
    last_modified: YYYY-MM-DDT00:00:00Z
---

# Bundle Acceptance Record

## Bundle Information

| Field | Value |
|-------|-------|
| **Bundle Name** | [Vendor/Product Name] |
| **Source** | [URL or local path where obtained] |
| **Date Received** | YYYY-MM-DD |
| **Date Approved** | YYYY-MM-DD |
| **Requested By** | [Name/Team requesting import] |
| **Approver** | human:<id> |
| **Import Path** | `wiki/<namespace>/` |

---

## Approval Summary

| Metric | Result |
|--------|--------|
| **Decision** | ✅ **Accepted** |
| **Quality Score** | High / Medium / Low |
| **Conflicts Resolved** | N (see section below) |
| **Concepts Imported** | N total (breakdown below) |

### Type Breakdown

| Type | Count | Verified | Stale |
|------|-------|----------|-------|
| Entity | X | X | X |
| Concept | X | X | X |
| Attested Computation | X | X | X |
| Playbook | X | X | X |
| Reference | X | X | X |
| **Total** | **N** | **X** | **X** |

---

## Quality Assurance Results

### Pre-Import Checklist

| Check | Status | Notes |
|-------|--------|-------|
| `okf_version` compatible | ☐ Pass ☐ Fail | <Notes> |
| All files have valid frontmatter | ☐ Pass ☐ Fail | <Notes> |
| No broken cross-links within bundle | ☐ Pass ☐ Fail | <Notes> |
| Trust tier distribution acceptable | ☐ Pass ☐ Fail | <Notes> |
| Staleness dates reviewed | ☐ Pass ☐ Fail | <Notes> |
| Security scan completed | ☐ Pass ☐ Fail | <Notes> |

### Post-Import Checklist

| Check | Status | Notes |
|-------|--------|-------|
| Concepts copied to `wiki/` namespace | ☐ Done | Location: `wiki/<namespace>/` |
| Original `sources[]` preserved | ☐ Done | Attribution intact |
| New `verified` entries added | ☐ Done | By: human:<id> |
| `log.md` updated | ☐ Done | Entry timestamp: YYYY-MM-DD |
| `bundles/index.md` updated | ☐ Done | Status changed to verified |
| Stakeholders notified (if needed) | ☐ Done | Teams: X, Y, Z |

---

## Conflict Resolution

| Conflicting Concept | Nature of Conflict | Resolution | Final Location |
|---------------------|--------------------|------------|----------------|
| `wiki/existing-concept.md` | Duplicate definition | Merged attributes | `wiki/merged-concept.md` |
| `wiki/conflicting-metric.md` | Different computation logic | Kept both; added disambiguation | Both retained with notes |

**Resolution Strategy:** <Wholesale Accept / Selective Adopt / Reference Only>

---

## Trust Calibration

### Imported Trust Distribution

| Tier | Count | Percentage |
|------|-------|------------|
| **Human-Reviewed** | X | X% |
| **Machine-Confirmed** | X | X% |
| **Unverified** | X | X% |

### Our Re-Verification Plan

| Concept Type | Timeline | Owner |
|--------------|----------|-------|
| All computations | Within 7 days | human:<id> |
| Critical metrics | Immediately | human:<id> |
| Remaining concepts | Within 30 days | human:<id> |

---

## Integration Notes

### Namespace Mapping

| Original Path | Target Path | Transformation |
|---------------|-------------|----------------|
| `bundles/vendor/entities/` | `wiki/<namespace>/entities/` | Direct copy |
| `bundles/vendor/computations/` | `wiki/<namespace>/computations/` | Direct copy |
| `bundles/vendor/references/` | `wiki/references/<vendor>/` | Sub-namespaced |

### Path Remapping

<If any absolute links were remapped, document here:>

- Old: `/wiki/concepts/old-topic.md` → New: `/wiki/<namespace>/topics/old-topic.md`
- Reason: Avoid collision with existing root concepts

### Special Handling

| File | Action | Reason |
|------|--------|--------|
| `vendor-excluded.md` | Skipped | Outdated, replaced by internal concept |
| `custom-computation.sql` | Tested | Validated against our attester |

---

## Dependencies & Downstream Impact

### Upstream Dependencies

| Dependency | Status | Contact |
|------------|--------|---------|
| Vendor must update quarterly | ☐ Agreed | vendor@company.com |
| Shared metric definitions | ☐ Coordinated | team:finance |

### Downstream Consumers

| Consumer | Notification Sent | Impact Level |
|----------|-------------------|--------------|
| Dashboard: Revenue Overview | ☐ Yes | High |
| Report: Q4 Financials | ☐ Yes | Medium |
| Team: Product Analytics | ☐ Yes | Low |

---

## Ongoing Maintenance

### Update Cadence

| Item | Frequency | Next Due |
|------|-----------|----------|
| Bundle re-import | Quarterly | YYYY-MM-DD |
| Computation attestation | Daily/Per-run | N/A |
| Staleness review | Monthly | YYYY-MM-DD |

### Change Management

| Scenario | Action |
|----------|--------|
| Vendor releases update | Re-run import workflow with version bump |
| Our team modifies imported concept | Add `modified_by` frontmatter entry; document in `log.md` |
| Conflict emerges post-import | Create `conflict-resolution.md` in same namespace |

---

## Related Documents

| Document | Link | Relationship |
|----------|------|--------------|
| Original Request | `../requests/request-XXX.md` | Trigger for approval |
| Rejection Record (if applicable) | `../rejected/vendor-rejection.md` | Previous decline, now resolved |
| Imported Concepts Index | `../../wiki/<namespace>/index.md` | Location of accepted content |
| Internal Replacement Notes | `wiki/<namespace>/notes.md` | Modifications we made |

---

## Sign-Off

| Role | Name | Date | Signature |
|------|------|------|-----------|
| **Primary Approver** | <human:<id>> | YYYY-MM-DD | |
| **Technical Reviewer** | <human:<id>> | YYYY-MM-DD | |
| **Stakeholder Acknowledgment** | <human:<id>> | YYYY-MM-DD | |

---

## Audit Trail

| Timestamp | Event | Actor |
|-----------|-------|-------|
| YYYY-MM-DD HH:MM | Bundle received | process:upload |
| YYYY-MM-DD HH:MM | Import requested | human:requester |
| YYYY-MM-DD HH:MM | Quality check passed | reference_agent/lumo-v2 |
| YYYY-MM-DD HH:MM | Final approval granted | human:<approver-id> |
| YYYY-MM-DD HH:MM | Content integrated | reference_agent/lumo-v2 |

---

> **Note:** This acceptance record is kept permanently for audit purposes. If the bundle is later deprecated or rejected, create a new rejection record in `rejected/` and link here.

---

### Common Acceptance Scenarios (Reference)

Use these templates for consistency:

| Scenario | Strategy | Notes |
|----------|----------|-------|
| **Clean, high-quality bundle** | Wholesale Accept | Minimal changes; preserve all provenance |
| **Mostly good, minor issues** | Selective Adopt | Skip problematic files; keep the rest |
| **Single concept needed** | Reference Only | Import only specific file; link from wiki |
| **Conflicts with existing** | Merge + Disambiguate | Keep both versions with clear differentiation |
| **Requires internal modification** | Fork + Attribute | Modify locally; add `modified_by` entry |

---

> Last updated: YYYY-MM-DD | [Return to bundles index](Knowledge%20Base/index.md)
