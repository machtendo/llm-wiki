# Knowledge Base README

> **Purpose:** Human-agent collaborative workspace following OKF v0.2 and LLM Wiki patterns  
> **Format:** Open Knowledge Format (OKF) v0.2  
> **Agent Rules:** See `AGENTS.md`  
> **Created:** 2026-10-01

---

## Overview

This repository hosts a **structured knowledge workspace** where:

- **Humans** curate, verify, and contribute high-level insights and raw source material.
- **Agents** ingest raw sources, synthesize concepts, maintain provenance, and run computations

Out of the box, this system combines the **LLM Wiki** pattern (incremental wiki-building vs. RAG) with **OKF v0.2** (strict frontmatter, attestation, and trust layers). There is a documented procedure for creating custom spec deviations in a way that preserves the core stack of llm-wiki + okf (see specs/index.md)

### Vanilla LLM Wiki Pattern (Without OKF v0.2)

**The LLM Wiki pattern solves the maintenance bottleneck that kills most personal knowledge bases.** Traditional approaches—whether RAG systems that re-discover knowledge on every query, or manual wikis that decay under upkeep burden—fail because the tedious bookkeeping outweighs the value. LLM Wiki flips this: the agent maintains cross-references, updates summaries when new sources arrive, flags contradictions, and touches 15 files in one pass. The human curates sources, directs analysis, and asks questions; the agent handles everything else. The result is a compounding artifact that grows richer with each ingested source.

**Architecture is deliberately simple: three layers separated by ownership.** Raw sources stay immutable in one folder; the LLM owns all synthesis in the wiki folder; a schema file (AGENTS.md or CLAUDE.md) tells the agent how to structure content and workflows. An index file catalogs available pages, and a log file tracks what happened when. No embedding infrastructure, no vector databases—just markdown files the LLM reads and edits. Obsidian becomes the IDE; the agent becomes the programmer; the wiki becomes the codebase.

**What it lacks without OKF:** No formal trust layer (no `verified` fields distinguishing human-review from agent-guesses), no attestation for computed values, no standard bundle format for sharing across teams, no built-in staleness detection. It's workspace-local rather than portable. For solo or small-team use, this simplicity is a feature. For multi-team, regulated, or enterprise deployments, the missing trust and portability layers become liabilities. That's where OKF v0.2 adds value—without abandoning the core LLM Wiki philosophy of agent-maintained compounding knowledge.

### OKF v0.2 Advantages for LLM Wiki Stack

**OKF v0.2 transforms your LLM Wiki from a convenient notebook into production-grade knowledge infrastructure.** While the LLM Wiki pattern establishes the workflow (human-agent collaboration, incremental synthesis, compounding value), OKF adds the trust layer that makes the knowledge verifiable and portable. The most significant addition is structured provenance: every concept tracks `sources[]` with credibility signals, `generated` metadata (who wrote it and when), and `verified` entries distinguishing human-reviewed claims from machine-generated ones. You can now answer "How much should I trust this?" and "Is it still current?" directly from frontmatter rather than hunting through conversation history.

**Bundle portability enables genuine knowledge sharing across teams and organizations.** An OKF bundle is a self-contained directory of markdown files that requires no SDK or proprietary format—just `git clone` or a tarball. Teams can exchange verified metrics, API documentation, or playbooks without lock-in. A finance team can publish attested computations for revenue and churn; a product team consumes them with built-in trust indicators rather than rebuilding the definitions. Cross-organization dependencies are explicit via `sources[]` links, and conflicts become detectable through frontmatter comparison rather than buried in prose.

**Attestation is the differentiator.** Only OKF v0.2 supports `Attested Computation` concepts that bind a displayed value to a sanctioned execution. When an agent reports "MRR is $4.2M," it can run the approved SQL, produce a receipt, and have an attester verify the result matches. This shifts trust from "the agent says so" to "this was computed deterministically and validated." For regulated domains (finance, healthcare, engineering), this audit trail is essential—not optional.

**Machine-to-machine interoperability follows naturally.** Agents reading other agents' work can calibrate confidence based on `verified.by` fields, route queries by `type`, filter stale content via `stale_after`, and weight sources by `usage_count`. No custom integration needed—the frontmatter speaks the same language across teams, tools, and time. The overhead is minimal once established: agents handle 95% of metadata maintenance automatically. The result is a knowledge base that compounds value while remaining portable, verifiable, and auditable.

---

## Quick Start Guide

### Prerequisites

| Requirement            | Notes                                                           |
| ---------------------- | --------------------------------------------------------------- |
| Obsidian (recommended) | For Properties panel viewing; Source mode works with any editor |
| Git                    | Optional for version control                                    |
| Agent                  | Must support markdown/YAML editing                              |

---

### Step 0: Kickstart Your Workspace

This repo serves as a starting point for an llm-wiki. This is an empty wiki. To get started, clone the repo and point your agent to the AGENT.md file, and skip steps 1-2

```shell
git clone https://github.com/machtendo/llm-wiki
```

### Step 1: Initialize Your Workspace

If you're starting fresh, create this structure:

```bash
mkdir -p
_wiki/bundles/{requests,rejected},_wiki/{raw_sources/{articles,papers,transcripts,assets},specs,templates/{index_templates,example_concepts},wiki/{entities,concepts,computations,playbooks,references/{skills,attesters}}}
```

### Step 2: Populate Foundation Files

Copy these files into their respective locations:

|File|Destination|Purpose|
|---|---|---|
|`AGENTS.md`|`_wiki/`|Agent operational schema|
|`index.md`|`_wiki/`|Root manifest|
|`log.md`|`_wiki/`|Update history tracker|
|`llm-wiki.md`|`_wiki/specs/`|LLM Wiki specification|
|`open-knowledge-format.md`|`_wiki/specs/`|OKF v0.2 specification|
|`index.md`|`_wiki/specs/`|Specifications catalog|
|5 index templates|`_wiki/templates/index_templates/`|Category scaffolding|
|4 example concepts|`_wiki/templates/example_concepts/`|Agent training examples|

### Step 3: Configure Obsidian (Optional)

To reduce frontmatter warnings:

1. **Install "Nested Frontmatter Properties"** plugin (if available in Community Plugins)  
    _Enables rendering of nested YAML in the Properties panel_
    
2. **OR install "YAML Properties"** plugin  
    _Replaces Properties panel with syntax-highlighted YAML editing_
    
3. **OR ignore warnings**  
    _The data is valid; Obsidian just doesn't support nested structures natively_
    

### Step 4: Your First Ingest

1. **Drop a source file** into `raw_sources/articles/` (e.g., `article-about-topic.md`)
    
2. **Ask your agent:**
    
    > "Read [filename] from raw_sources and ingest it into the wiki following AGENTS.md. Create appropriate entity/concept pages, populate sources[] with provenance, set status to draft, and update log.md."
    
3. **Review** the generated page(s) in `wiki/`
    
4. **Verify** by updating the frontmatter:
    

```yaml
   verified:
     - by: human:(name)
       at: YYYY-MM-DDTHH:MM:SSZ
   status: stable
```

5. **Log the change** in `log.md`

---

## Directory Structure

```card
_wiki/
├── AGENTS.md                     # Agent rules & constraints
├── index.md                      # Root manifest (OKF-compliant)
├── log.md                        # Chronological update history
│
├── raw_sources/                  # INPUT: Immutable source material
│   ├── articles/                 # Clipped web articles, blog posts
│   ├── papers/                   # Research papers, whitepapers
│   ├── transcripts/              # Slack, Zoom, email threads
│   └── assets/                   # Downloaded images, PDFs
│
├── specs/                        # SYSTEM: Design specifications
│   ├── index.md                  # Specification catalog
│   ├── llm-wiki.md               # LLM Wiki pattern
│   └── open-knowledge-format.md  # OKF v0.2 spec
│
├── templates/                    # SCAFFOLDING: Agent tooling
│   ├── index_templates/          # Category index templates
│   │   ├── entity_index.md
│   │   ├── concept_index.md
│   │   ├── computation_index.md
│   │   ├── playbook_index.md
│   │   └── reference_index.md
│   └── example_concepts/         # Training examples
│       ├── example_entity.md
│       ├── example_concept.md
│       ├── example_computation.md
│       └── example_playbook.md
│
└── wiki/                     # OUTPUT: Living knowledge base
    ├── entities/             # People, companies, products (type: Entity)
    ├── concepts/             # Methodologies, theories (type: Concept)
    ├── computations/         # Metrics, formulas (type: Attested Computation)
    ├── playbooks/            # Procedures, incident response (type: Playbook)
    └── references/           # Skills, attesters, mirrors (type: Reference)
```

---

## OKF v0.2 Compliance

Every concept file in `wiki/` must include this **minimum frontmatter**:

```yaml
---
type: <Type name>
generated:
  by: <actor>
  at: <ISO-8601-timestamp>
---
```

### Type Catalog

|Type|Location|Purpose|
|---|---|---|
|`Entity`|`wiki/entities/`|People, companies, products|
|`Concept`|`wiki/concepts/`|Abstract ideas, methodologies|
|`Attested Computation`|`wiki/computations/`|Metrics, formulas with verification|
|`Playbook`|`wiki/playbooks/`|Operational procedures|
|`Reference`|`wiki/references/`|Skills, attesters, external docs|

### Recommended Fields (Add When Applicable)

```yaml
title: <display name>
description: <one-line summary>
tags: [<tag1>, <tag2>]
status: draft | stable | deprecated
stale_after: <ISO-8601-timestamp>
sources:
  - id: <stable-key>
    resource: <URL or relative path>
    title: <human label>
    author: <optional>
    last_modified: <optional ISO-8601>
verified:
  - by: <actor>
    at: <ISO-8601-timestamp>
```

### Actor Convention

| Actor Type | Format                       | Example                      |
| ---------- | ---------------------------- | ---------------------------- |
| Agents     | `reference_agent/<model-id>` | `reference_agent/agent-name` |
| Humans     | `human:<id>`                 | `human:name`                 |
| Processes  | `process:<name>`             | `process:nightly-lint`       |

---

## Workflow Overview

### 📥 Ingest → 🧹 Synthesize → ✅ Verify → 🔗 Cross-Link

#### Phase A: Ingestion

|Step|Who|Action|
|---|---|---|
|1|Human|Drops source file into `raw_sources/`|
|2|Agent|Reads source, extracts key information|
|3|Agent|Creates draft concept in `wiki/` with `status: draft`|
|4|Agent|Populates `sources[]` with provenance|
|5|Agent|Updates `log.md` and relevant `index.md` files|

#### Phase B: Query & Synthesis

| Step | Who   | Action                                        |
| ---- | ----- | --------------------------------------------- |
| 1    | Human | Asks complex question                         |
| 2    | Agent | Searches `wiki/` for relevant pages           |
| 3    | Agent | Runs attested computations (if needed)        |
| 4    | Agent | Verifies receipts via attester scripts        |
| 5    | Agent | Answers with citations and verified data      |
| 6    | Agent | Offers to create new wiki pages from insights |

#### Phase C: Maintenance

|Check|Frequency|Agent Action|
|---|---|---|
|Staleness|Daily|Flag pages past `stale_after` date|
|Orphans|Weekly|Find pages with no inbound links|
|Contradictions|Weekly|Compare claims across linked pages|
|Broken Links|Weekly|Detect missing target files|

---

## Command Cheat Sheet

|Task|Command|
|---|---|
|View root index|Open `index.md`|
|Check recent changes|Open `log.md`|
|Search for a concept|Use Obsidian global search or agent query|
|Run lint check|"Perform health check on wiki folder"|
|Request ingestion|"Ingest [filename] from raw_sources"|
|Update an entity|"Update [concept-name] with new information from [source]"|

---

## Troubleshooting

|Issue|Likely Cause|Solution|
|---|---|---|
|Obsidian warns "invalid properties"|Nested YAML not supported|Install plugin OR ignore (data is valid)|
|Agent creates duplicate pages|Missing cross-reference check|Review `AGENTS.md` deduplication rules|
|Broken internal links|Relative path errors|Use absolute paths (`/wiki/concepts/topic.md`)|
|Computation fails|Missing executor/attester|Verify `references/skills/` and `attesters/` exist|
|No index entries populated|Template not copied|Copy from `templates/index_templates/`|

---

## Contributing Guidelines

### For Humans

1. **Verify** draft content before setting `status: stable`
2. **Link** to existing concepts when referencing them
3. **Document** deviations in `specs/index.md`
4. **Log** significant changes in `log.md`

### For Agents

1. **Never modify** `raw_sources/` (read-only)
2. **Preserve unknown frontmatter fields** (don't strip them)
3. **Cite every claim** with footnotes matching `sources[].id`
4. **Log every action** in `log.md`
5. **Escalate** when uncertain about type classification or broken links

---

## Deviations from Base Specs

Customizations beyond the vanilla llm-wiki and OKF stacks are listed here.
### Bundle Import Workflow Extension

- **Date Introduced**: 2026-10-02
- **Modified Spec**: OKF v0.2 (§3 Bundle Structure) + LLM Wiki (Ingest Workflow)
- **Summary**: Formalized bundle lifecycle management with acceptance/rejection tracking, namespace isolation, and audit trails.
- **Rationale**: Base OKF v0.2 defines bundles but leaves import workflow unspecified; LLM Wiki focuses on raw sources, not bundle validation.
- **Implementation**: Added `bundles/` directory with `requests/`, `accepted/`, `rejected/` subdirectories; new templates for acceptance/rejection records; updated `AGENTS.md` with bundle-specific workflow logic.
- **Last Reviewed**: 2026-10-01

This and any future modifications should be documented in `specs/index.md` under "Custom Deviations."

---

## Related Resources

| Resource                                     | URL                                                               |
| -------------------------------------------- | ----------------------------------------------------------------- |
| Gist - LLM Wiki by Andrej Karpathy           | https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f |
| GoogleCloudPlatform - OKF v0.2 Specification | https://github.com/GoogleCloudPlatform/open-knowledge-format      |
| Agent Schema                                 | `AGENTS.md`                                                       |
|                                              |                                                                   |

---

## License & Credits

- **Specs:** LLM Wiki (Andrej Karpathy) & OKF v0.2 (GoogleCloudPlatform)
- **Workspace:** Human-curated, agent-maintained
- **Last Updated:** 2026-10-01

---

## Next Steps After Setup

|Goal|Starting Point|Estimated Time|
|---|---|---|
|First real ingest|`raw_sources/articles/` + agent query|5 min|
|Build out entity catalog|`wiki/entities/`|30 min|
|Create your first metric|`wiki/computations/`|15 min|
|Document a procedure|`wiki/playbooks/`|20 min|

---

> **Ready?** Drop a source file into `raw_sources/` and begin your first ingest.
