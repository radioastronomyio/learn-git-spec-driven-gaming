<!--
---
title: "Tagging Strategy Guide"
description: "Controlled vocabulary for document classification and hydration guide"
author: "msp4-don"
date: "2026-03-28"
version: "2.1"
tags:
  - type: guide
  - domain: documentation
related_documents:
  - "[Primary README Template](primary-readme-template.md)"
  - "[Interior README Template](interior-readme-template.md)"
  - "[General KB Template](general-kb-template.md)"
  - "[Worklog README Template](worklog-readme-template.md)"
  - "[One-Pager Template](one-pager-template.md)"
  - "[Project Charter Template](project-charter-template.md)"
---
-->

# Tagging Strategy Guide

## 1. Purpose

This guide explains how to build a controlled tag vocabulary for a repository. Consistent tagging enables human navigation and RAG system retrieval. When forking this template, replace the example domain vocabulary with your project's actual content areas.

---

## 2. Why Controlled Vocabulary

Uncontrolled tagging leads to synonyms fragmenting search (`database` vs `db` vs `databases`), inconsistent granularity (`postgres` vs `relational-database`), and tag proliferation that reduces signal. A controlled vocabulary defines allowed values upfront, ensuring consistency across contributors and time.

---

## 3. Tag Categories

Each category answers a different question about the document. Keep categories orthogonal; each captures a distinct dimension.

| Category | Question Answered | Required |
|----------|-------------------|----------|
| `type` | What kind of document is this? | Yes |
| `domain` | What subject area? | Yes |
| `status` | What's the lifecycle state? | Recommended |
| `tech` | What technologies involved? | When applicable |
| `framework` | What compliance framework? | When applicable |

---

## 4. Domain Tags

Domain tags are project-specific. Replace this section with your project's vocabulary.

### Building Your Domain Vocabulary

1. **Inventory content types.** What kinds of content does this repository contain? Group by function, not format.
2. **Define 5-12 domain values.** Cover your content without excessive overlap.
3. **Write boundary definitions.** One sentence per tag clarifying what belongs and what doesn't.

### Domain Vocabulary

```yaml
domain:
  - game              # Breakout game code, canvas rendering, game logic, assets
  - git-workflow      # Git learning materials, references, contributing guides
  - specs             # Spec-driven development specifications and feature menus
  - testing           # Playwright tests, test infrastructure, validation
  - infrastructure    # nginx, deployment scripts, Azure Static Web Apps, DNS
  - documentation     # Templates, standards, meta-content
```

### Boundary Rules

- If a document spans two domains, use the primary one. Multi-value only when genuinely split.
- Define clear boundaries between similar domains (e.g., `deployment` is standing up a service; `infrastructure` is the VM it runs on).

---

## 5. Type Tags

| Tag | Use For |
|-----|---------|
| `project-root` | Repository root README |
| `directory-readme` | Interior README for any directory |
| `worklog` | Work log entries and milestone documentation |
| `charter` | Project charter (frozen scope and architectural commitments) |
| `one-pager` | Ideation capture (portable context unit for AI handoffs) |
| `guide` | Step-by-step procedures and how-to documents |
| `reference` | Lookup information: inventories, schemas, API docs |
| `specification` | Service specs, deployment definitions, formal requirements |
| `report` | Analysis, findings, audit results, summaries |
| `runbook` | Operational procedures for incident response or maintenance |
| `policy` | Governance policies: commitments and principles |
| `procedure` | SOPs: how activities are carried out |

---

## 6. Status Tags

| Tag | Description |
|-----|-------------|
| `draft` | In development, not yet complete |
| `active` | Current, maintained, approved |
| `under-review` | Scheduled or triggered review in progress |
| `deprecated` | Superseded, avoid for new work |
| `archived` | Historical reference only |

---

## 7. Tech Tags

Use canonical names, lowercase, hyphenated. Build this list as your project's stack takes shape. Check for existing coverage before adding new tags.

```yaml
tech:
  - javascript        # Game logic, canvas rendering
  - html              # Game page structure
  - css               # Game styling and effects
  - canvas            # HTML5 Canvas API for game rendering
  - playwright        # Browser-based testing and validation
  - nginx             # Dev server on agents01
  - bash              # Deploy scripts, automation
  - azure-swa         # Azure Static Web Apps for production hosting
```

---

## 8. Framework Tags

Compliance and governance framework references. Use only when a document directly implements or maps to a framework control. Skip this section entirely if your project doesn't involve compliance work.

No compliance frameworks apply to this project.

---

## 9. Implementation

### Standard Frontmatter

```yaml
<!--
---
title: "Document Title"
description: "What this document covers"
author: "msp4-don"
date: "YYYY-MM-DD"
version: "1.0"
status: "Active"
tags:
  - type: guide
  - domain: [your-domain-tag]
  - tech: [relevant-tech]
related_documents:
  - "[Related Doc](path/to/doc.md)"
---
-->
```

### Conventions

- Use lowercase, hyphenated values (`ci-cd` not `CI/CD` or `cicd`)
- Tech tags use canonical names
- One value per line for readability, or array syntax for multi-value
- `related_documents` links use relative paths within the repo

---

## 10. Maintaining the Vocabulary

### Adding New Tags

1. Check if an existing tag covers the concept
2. If not, add the new tag with a boundary definition to this document
3. Backfill existing documents if the new tag applies retroactively

### Governance

- This document is the authoritative source for allowed tag values
- Prefer broader tags over proliferating specific ones
- Review additions for overlap with existing tags

---

## 11. References

| Resource | Description |
|----------|-------------|
| [Primary README Template](primary-readme-template.md) | Shows tag usage in repository root READMEs |
| [Interior README Template](interior-readme-template.md) | Shows tag usage in directory READMEs |
| [General KB Template](general-kb-template.md) | Shows tag usage for standalone docs |
| [Worklog README Template](worklog-readme-template.md) | Shows tag usage for work log entries |
| [One-Pager Template](one-pager-template.md) | Shows tag usage for ideation documents |
| [Project Charter Template](project-charter-template.md) | Shows tag usage for project charters |
