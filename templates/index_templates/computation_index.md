# Computations Index

> Sanctioned calculations, metrics, and formulas with attestation definitions.

---

## Financial Metrics

| Computation | Runtime | Status | Stale After | Verified By |
|-------------|---------|--------|-------------|-------------|
| [Add Metric Name](./metric-name.md) | <bigquery/dbt/python> | draft/stable | YYYY-MM-DD | human:<id> |

## Operational Metrics

| Computation | Runtime | Status | Stale After | Verified By |
|-------------|---------|--------|-------------|-------------|
| [Add Metric Name](./metric-name.md) | <bigquery/dbt/python> | draft/stable | YYYY-MM-DD | human:<id> |

## Verification Summary

| Total Computations | Verified | Stale | Awaiting Review |
|--------------------|----------|-------|-----------------|
| 0 | 0 | 0 | 0 |

---

## Executor Skills

Available execution runtimes:

* [Run on BigQuery](../references/skills/run-on-bq.md) - SQL query execution
* [Run dbt](../references/skills/run-dbt.md) - Data transformation models

## Attesters

Available verification scripts:

* [SQL Equality Checker](../references/attesters/sql-equality.py) - Validates executed SQL matches sanctioned computation
* [Binding Validator](../references/attesters/binding-validator.py) - Confirms parameter binding integrity

---

### Guidelines for Adding Computations

When creating a new computation page:
1. Use `type: Attested Computation` in frontmatter
2. Define `runtime`, `parameters`, `executor`, and `attester`
3. Include `# Computation` section with sanctioned logic
4. Set `stale_after` based on expected data refresh frequency
5. Link from metric/narrative pages that depend on this value

---

> Last updated: 2026-10-01 | [Return to root](Knowledge%20Base/index.md) | [Back to templates](../)
