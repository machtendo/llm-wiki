# Specifications Index

> Catalog of design specifications governing this knowledge workspace.

---

## Base Specifications

| Spec                  | Version | Location                                               | Purpose                                                              |
| --------------------- | ------- | ------------------------------------------------------ | -------------------------------------------------------------------- |
| LLM Wiki Pattern      | n/a     | [`llm-wiki.md`](Knowledge%20Base/specs/llm-wiki.md)                           | Human-agent collaboration workflow and folder architecture           |
| Open Knowledge Format | 0.2     | [`open-knowledge-format.md`](open-knowledge-format.md) | YAML frontmatter structure, provenance, trust, and attestation rules |

---

## Custom Deviations

This section documents any modifications or extensions made to the base specifications for this workspace.

### Bundle Import Workflow Extension

- **Date Introduced**: 2026-10-02
- **Modified Spec**: OKF v0.2 (§3 Bundle Structure) + LLM Wiki (Ingest Workflow)
- **Summary**: Formalized bundle lifecycle management with acceptance/rejection tracking, namespace isolation, and audit trails.
- **Rationale**: Base OKF v0.2 defines bundles but leaves import workflow unspecified; LLM Wiki focuses on raw sources, not bundle validation.
- **Implementation**: Added `bundles/` directory with `requests/`, `accepted/`, `rejected/` subdirectories; new templates for acceptance/rejection records; updated `AGENTS.md` with bundle-specific workflow logic.
- **Last Reviewed**: 2026-10-01

No deviations from base specifications. All content follows OKF v0.2 and LLM Wiki patterns as-is.

---

### Deviation Entry Template

When adding a custom deviation, copy this template:

```markdown
### [Deviation Name]

- **Date Introduced**: YYYY-MM-DD
- **Modified Spec**: <e.g., OKF v0.2 or LLM Wiki>
- **Summary**: One-sentence description of the change.
- **Rationale**: Why this deviation was necessary.
- **Implementation**: Where/how the change manifests (files, folders, rules).
- **Last Reviewed**: YYYY-MM-DD
````

---

## Change Log

|Date|Action|Description|Author|
|---|---|---|---|
|2026-10-01|Initial|Created workspace with base specs|human:lrm|
|—|—|—|—|

---

## Related Configuration Files

|File|Location|Purpose|
|---|---|---|
|Agent Schema|`../AGENTS.md`|Operational rules for wiki-maintaining agents|
|Root Index|`../index.md`|Bundle manifest and category navigation|
|Update Log|`../log.md`|Chronological history of changes|
|Templates|`../templates/`|Scaffold templates for index pages|

---

> Last updated: 2026-10-01 | [Return to root](https://lumo.proton.me/u/4/index.md)
