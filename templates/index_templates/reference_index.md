# References Index

> External documentation mirrors, code samples, and skill definitions.

---

## Skills (Executors)

Instructions for running computations:

| Skill | Runtime | Parameters | Last Updated |
|-------|---------|------------|--------------|
| [Run on BigQuery](./skills/run-on-bq.md) | bigquery | <list params> | YYYY-MM-DD |
| [Run dbt](./skills/run-dbt.md) | dbt | <list params> | YYYY-MM-DD |

## Attesters

Deterministic verification scripts:

| Attester | Purpose | Language | Last Updated |
|----------|---------|----------|--------------|
| [SQL Equality Checker](./attesters/sql-equality.py) | Verify executed SQL matches sanctioned | python | YYYY-MM-DD |
| [Binding Validator](./attesters/binding-validator.py) | Confirm parameter binding integrity | python | YYYY-MM-DD |

## External Mirrors

Cached copies of critical external documentation:

| Document | Original URL | Mirror Purpose | Cached Date |
|----------|--------------|----------------|-------------|
| [Add Document](./external-doc-name.md) | https://... | why this was mirrored | YYYY-MM-DD |

---

### Guidelines for Adding References

When creating a new reference page:
1. Use `type: Reference` in frontmatter
2. For skills: Include `# Execution` section with command syntax
3. For attesters: Include `# Interface` section with input/output expectations
4. For mirrors: Store original URL in `sources[]` and summarize changes
5. Set `stale_after` if the external source updates regularly

---

> Last updated: 2026-10-01 | [Return to root](Knowledge%20Base/index.md) | [Back to templates](../)
