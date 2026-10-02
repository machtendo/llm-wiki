---
type: Attested Computation
title: Monthly Active Users (MAU)
description: Count of distinct users with activity in the current calendar month.
tags: [metric, engagement, saas]
runtime: bigquery
parameters:
  - name: month_start
    type: date
    required: true
  - name: month_end
    type: date
    required: true
executor:
  resource: ../references/skills/run-on-bq.md
  receipt: [job_id, executed_sql, result_value, row_count]
attester:
  resource: ../references/attesters/sql-equality.py
generated:
  by: reference_agent/lumo-v2
  at: 2026-10-01T14:00:00Z
verified:
  - by: human:lrm
    at: 2026-10-01T15:00:00Z
status: stable
stale_after: 2026-10-02T00:00:00Z
sources:
  - id: analytics-schema
    resource: ../../raw_sources/docs/event-tracking-schema.md
    title: Event Tracking Schema Documentation
    author: team:data-platform
    last_modified: 2026-09-10T00:00:00Z
  - id: mau-definition
    resource: https://internal-wiki/product/metrics/mau-definition
    title: MAU Definition Policy
    author: team:product-analytics
    usage_count: 3200
    last_modified: 2026-07-15T00:00:00Z
usage_window:
  from: 2026-09-01T00:00:00Z
  to: 2026-09-30T23:59:59Z
---
# Computation

```sql
SELECT COUNT(DISTINCT user_id) AS mau
FROM analytics.events
WHERE event_timestamp >= @month_start
  AND event_timestamp < @month_end
  AND event_type IN ('page_view', 'click', 'purchase', 'login')
```

The computation filters to meaningful engagement events per the [MAU Definition Policy][1](https://lumo.proton.me/#user-content-fn-mau-definition). Only events with explicit user identification are counted, excluding anonymous sessions.

## Parameter Binding

|Parameter|Type|Description|Example Value|
|---|---|---|---|
|`month_start`|DATE|First day of target month|`2026-10-01`|
|`month_end`|DATE|First day of following month|`2026-11-01`|

## Verification Notes

- SQL must match sanctioned computation exactly (byte-for-byte after whitespace normalization)
- Attester validates `row_count` >= 1 before accepting result
- Staleness: recomputed daily; `stale_after` set to next midnight UTC

## Related Metrics

- [Daily Active Users](https://lumo.proton.me/daily-active-users.md) - Same logic, daily granularity
- [Weekly Active Users](https://lumo.proton.me/weekly-active-users.md) - Rolling 7-day window

---

## Footnotes

1. MAU Definition Policy [↩](https://lumo.proton.me/#user-content-fnref-mau-definition)