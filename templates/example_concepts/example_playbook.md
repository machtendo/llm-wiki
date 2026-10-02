---
type: Playbook
title: Data Freshness Alert Response
description: Steps to triage and resolve delayed data pipeline alerts.
tags: [oncall, data-platform, incident-response]
generated:
  by: reference_agent/lumo-v2
  at: 2026-10-01T16:00:00Z
verified:
  - by: human:lrm
    at: 2026-10-01T16:30:00Z
status: stable
stale_after: 2027-01-01T00:00:00Z
sources:
  - id: pipeline-sla
    resource: ../../raw_sources/docs/data-pipeline-slas.md
    title: Data Pipeline SLA Documentation
    author: team:data-platform
    last_modified: 2026-08-20T00:00:00Z
  - id: oncall-guide
    resource: https://internal-wiki/oncall/data-alerts
    title: On-Call Guide for Data Alerts
    author: team:sre
    usage_count: 850
    last_modified: 2026-09-05T00:00:00Z
---

# Trigger

Alert fires when any critical table's `last_updated_at` timestamp exceeds its SLA threshold:

| Table | SLA Threshold | Owner Team |
|-------|---------------|------------|
| `analytics.events` | 30 minutes | data-platform |
| `sales.orders` | 1 hour | commerce-engine |
| `finance.daily_revenue` | 2 hours | finance-fpa |

See [Pipeline SLA Documentation][^pipeline-sla] for full list.
## Immediate Actions

1. **Check the alert severity**
   - `low`: 1-2x SLA threshold elapsed
   - `medium`: 2-5x SLA threshold elapsed
   - `high`: >5x SLA threshold elapsed
   - `critical`: >10x SLA threshold elapsed

2. **Open the ingestion job dashboard**
   - URL: https://airflow.internal/dags?status=failed
   - Look for failed DAGs related to the affected table

1. **Review the most recent error logs**

   ```bash
   gcloud logging read "resource.type=cloud_run_resource" \
     "jsonPayload.table_name=<affected_table>" \
     --limit 20 --order desc
	````
	
2. **Determine root cause category**

|Error Type|Likely Cause|Resolution|
|---|---|---|
|`Source unavailable`|Upstream API down|Wait + retry; escalate to upstream owner|
|`Schema mismatch`|Source schema changed|Deploy schema migration|
|`Resource exhausted`|Query timeout/memory|Increase resources; optimize query|
|`Dependency failed`|Predecessor DAG failed|Resolve predecessor first|

## Escalation Paths

### If Source Unavailable (>30 minutes)

Contact upstream service owner:

- Analytics: `team:data-platform` on-call (PagerDuty)
- Commerce: `team:commerce-backend` on-call
- Finance: `team:fpa-data` on-call

### If Schema Mismatch Detected

Engage schema steward:

1. File ticket in #data-schema-changes Slack channel
2. Include: affected table, new schema diff, impact assessment
3. Follow standard migration procedure (see [On-Call Guide][1](https://lumo.proton.me/#user-content-fn-oncall-guide))

## Verification

After remediation:

1. Confirm `last_updated_at` is within SLA threshold
2. Run [Monthly Active Users](https://lumo.proton.me/computations/mau.md) to validate downstream metrics
3. Document incident in `log.md` with root cause and resolution time
4. If >1 hour downtime, schedule blameless post-mortem

## Related Playbooks

- [Pipeline Failure](https://lumo.proton.me/pipeline-complete-failure.md) - When entire pipeline is down
- [Schema Migration Procedure](https://lumo.proton.me/schema-migration-procedure.md) - For structural changes

---

## Footnotes

1. On-Call Guide for Data Alerts [↩](https://lumo.proton.me/#user-content-fnref-oncall-guide)