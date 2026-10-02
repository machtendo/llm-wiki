# Agent Workspace Schema

You are the maintainer of this knowledge wiki. Follow these rules strictly when interacting with the knowledge corpus.

## Your Role

- **YOU WRITE**: All content in `wiki/` directory
- **YOU READ**: From both `wiki/` and `raw_sources/` directories
- **YOU NEVER MODIFY**: Files in `raw_sources/` (immutable source material)

**Remember**: The wiki is a compounding asset. Every change should make it richer, more connected, and more trustworthy. You are the librarian; the human is the curator.

---
## OKF v0.2 Compliance

Every concept file you create or edit in `wiki/` MUST have valid YAML frontmatter with:

### Required Fields
```yaml
---
type: <Type name>           # REQUIRED - See Type Catalog below
generated:
  by: <actor>               # REQUIRED - Use "reference_agent/<model-id>" or "human:<id>"
  at: <ISO-8601-timestamp>  # REQUIRED - UTC timezone (Z suffix)
---
````

### Recommended Fields (Add when applicable)

```yaml
title: <display name>
description: <one-line summary>
resource: <canonical URI or bundle-relative path>
tags: [<tag1>, <tag2>]
status: draft | stable | deprecated  # Default: stable
stale_after: <ISO-8601-timestamp>    # Optional staleness deadline
sources:
  - id: <stable-key>
    resource: <URL or bundle-relative path>
    title: <human label>
    author: <optional actor>
    last_modified: <optional ISO-8601 date>
verified:
  - by: <actor>
    at: <ISO-8601-timestamp>
---
```

### Type Catalog

|Type|Purpose|Location|
|---|---|---|
|`Entity`|Person, company, product, organization|`wiki/entities/`|
|`Concept`|Abstract idea, methodology, theory|`wiki/concepts/`|
|`Attested Computation`|Sanctioned formula/metric|`wiki/computations/`|
|`Playbook`|Operational procedure, incident response|`wiki/playbooks/`|
|`Reference`|External documentation mirror|`wiki/references/`|

### Actor Convention

- Agents: `reference_agent/<model-id>` (e.g., `reference_agent/lumo-v2`)
- Humans: `human:<your-id>` (e.g., `human:lrm`)
- Processes: `process:<name>` (e.g., `process:nightly-lint`)

## Working Patterns

### Ingesting a New Source

1. Read the source file from `raw_sources/`
2. Extract key information and create/update wiki pages
3. Populate `sources[]` with the source file reference
4. Set `status: draft` until human review
5. Append entry to `log.md`
6. Update relevant `index.md` files

### Updating Existing Pages

1. Check if newer sources supersede old claims
2. Flag contradictions explicitly in the body
3. Update `sources[]` when adding new provenance
4. Keep `generated.at` current on edits
5. Log changes in `log.md`

### Linting (Health Checks)

Run these checks periodically:

- [ ]  Any `stale_after` dates in the past?
- [ ]  Any pages with no inbound links (orphans)?
- [ ]  Broken links (target doesn't exist)?
- [ ]  Missing `sources[]` on claim-heavy pages?
- [ ]  Any concepts lacking their own page despite frequent mentions?
- [ ]  Contradictions between linked pages?

### Cross-Linking Rules

- Use absolute paths (`/wiki/concepts/topic.md`) for stability
- Footnotes for claim attribution: `[^source-id]` matching `sources[].id`
- Do NOT create links to non-existent pages without discussion

## Reserved Filenames

Do NOT use these for concepts:

- `index.md` (directory listing)
- `log.md` (update history)

## Output Formats for Responses

Depending on the query, answers may be formatted as:

- Plain markdown page (file into wiki if valuable)
- Comparison table
- Chart (Vega-Lite for numeric trends)
- Code snippet

## Critical Constraints

1. **Never fabricate verification**: Only add `verified` entries when a human has confirmed content
2. **Never edit raw sources**: All modifications go through `wiki/` only
3. **Preserve unknown fields**: If reading files with unrecognized frontmatter keys, keep them intact
4. **Tolerate missing optional fields**: Don't reject documents for lacking optional metadata
5. **Log everything**: Every ingest, update, or lint pass gets a `log.md` entry

## Escalation

If uncertain about:

- Type classification → Ask the human
- Link targets that don't exist → Propose creating them first
- Conflicting source claims → Flag explicitly in the page body
- Computation execution requirements → Request executor/attester setup

---
## Template System

Use templates from the `templates/` folder when creating new index or example files.

| Template          | Location                                         | Purpose                                   |
| ----------------- | ------------------------------------------------ | ----------------------------------------- |
| Entity Index      | `templates/index_templates/entity_index.md`      | Scaffold for `wiki/entities/index.md`     |
| Concept Index     | `templates/index_templates/concept_index.md`     | Scaffold for `wiki/concepts/index.md`     |
| Computation Index | `templates/index_templates/computation_index.md` | Scaffold for `wiki/computations/index.md` |
| Playbook Index    | `templates/index_templates/playbook_index.md`    | Scaffold for `wiki/playbooks/index.md`    |
| Reference Index   | `templates/index_templates/reference_index.md`   | Scaffold for `wiki/references/index.md`   |

When creating a new category index:
1. Copy the appropriate template from `templates/index_templates/`
2. Fill in actual entries (no template markers in final output)
3. Save to the target subdirectory in `wiki/` (e.g., `wiki/entities/index.md`)
4. Update root `index.md` and `log.md` to reflect the change

---
## Example Learning

Before ingesting new content, review the example concepts in `templates/example_concepts/`:

| Example | Purpose | What to Learn |
|---------|---------|---------------|
| `example_entity.md` | Person/company entity | Proper frontmatter, biographical structure, cross-linking |
| `example_concept.md` | Abstract methodology | Comparative tables, per-claim attribution, nuance handling |
| `example_computation.md` | Attested computation | Executor/attester contract, parameter definitions, verification notes |
| `example_playbook.md` | Operational procedure | Trigger conditions, numbered steps, escalation paths |

When creating new concepts, match the structure, frontmatter completeness, and citation patterns shown in these examples.

---
## System Files

The following locations contain **non-concept** files that should NOT be ingested into the wiki:

- `specs/` — Design specifications and reference documents
- `templates/` — Scaffold templates
- `bundles/` — Imported knowledge bundles (use bundle workflow, not standard ingest)
- `AGENTS.md`, `index.md`, `log.md` — System configuration and logs

These are operational files, not knowledge content.

---
## Bundle Import Workflow

When encountering content in the `bundles/` directory, use this workflow instead of standard ingest:

### Distinguishing Source Types

| Path | Type | Workflow |
|------|------|----------|
| `raw_sources/*` | Unprocessed documents | Standard ingest: extract → synthesize → create new wiki pages |
| `bundles/*/*.md` | OKF concepts | Validation: preserve existing frontmatter, optionally merge |
| `bundles/*/` | Complete bundles | Import workflow: inspect → validate → integrate |

### Bundle Ingestion Steps

1. **Inspect Structure**
   - Check `index.md` for `okf_version` declaration
   - Verify all `.md` files have valid frontmatter
   - Identify concept types and counts

2. **Run Health Check**
   - Check for broken cross-links
   - Flag orphan pages (no inbound links)
   - Detect `stale_after` dates in the past
   - Surface trust tier distribution (unverified/machine/human)

3. **Conflict Detection**
   - Cross-reference existing `wiki/` concepts by `type` + `title`
   - If duplicates found: flag with `CONFLICT_WITH: <existing-concept>` comment
   - Present conflict summary to human for resolution

4. **Merge Strategy Selection**
   - **Wholesale Accept**: Copy all concepts to `wiki/` (preserve original `sources[]`)
   - **Selective Adopt**: Choose specific concepts based on human guidance
   - **Reference Only**: Keep in `bundles/`, add links from `wiki/` (no merge)

5. **Attribution Chain**
   - Keep original `sources[].resource` pointing to bundle location
   - Add new `generated` entry: `{ by: reference_agent/lumo-v2, at: <timestamp> }`
   - Clear previous `status: draft` until human confirms: `verified: { by: human:lrm, at: <timestamp> }`

6. **Update Index**
   - Update `bundles/index.md` with import date and concept count
   - Update `log.md` with bundle import entry
   - Optionally update root `index.md` if adding new categories

### Example Bundle Import Log Entry

```markdown
## 2026-10-XX

* **Bundle Import**: Ingested [Finance Metrics Bundle] from vendor-team
  - Concepts imported: 12 (3 Entity, 5 Computation, 2 Concept, 2 Playbook)
  - Conflicts detected: 1 (revenue.md - resolved via merge)
  - Trust level: 8 human-verified, 4 machine-confirmed
  - Author: human:lrm
````

### Post-Import Actions

- [ ]  Update `bundles/index.md` (status → verified)
- [ ]  Run full workspace lint (check for new orphans/broken links)
- [ ]  Notify relevant stakeholders if new computations affect downstream metrics
- [ ]  Schedule re-validation before `stale_after` dates expire

**Remember:** Bundles contain pre-synthesized knowledge. The goal is **validation**, not re-processing. Preserve original provenance and attribution chains.

---

## Bundle Exclusion List

The following bundles should **not** be ingested:

|Bundle|Reason|Alternative Action|
|---|---|---|
|`bundles/rejected/*`|Previously declined|Keep archived for reference only|
|`bundles/pending/*`|Awaiting human decision|Do not process until approved|

## Bundle Lifecycle Management

- **Pending**: Bundles awaiting review → `bundles/pending/`
- **Accepted**: Bundles approved and integrated → `bundles/accepted/`
- **Rejected**: Bundles declined (kept for audit) → `bundles/rejected/`
- **Archived**: Deprecated bundles (historical only) → `bundles/archive/`

Agents MUST use the appropriate acceptance/rejection template (templates/bundle_lifecycle) when finalizing bundle decisions.

---
