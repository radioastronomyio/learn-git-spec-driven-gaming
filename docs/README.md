<!--
---
title: "Documentation"
description: "Project documentation, guides, and reference materials"
author: "radioastronomyio"
date: "2026-05-17"
version: "2.0"
status: "Active"
tags:
  - type: directory-readme
  - domain: documentation
---
-->

# Documentation

Guides, design documents, and standards for the project. Start with `getting-started.md` if you're new. The `documentation-standards/` subdirectory contains the template library and guidelines that govern all documentation in the repository.

---

## 1. Contents

```
docs/
├── documentation-standards/        # Template library and guidelines
│   ├── primary-readme-template.md
│   ├── interior-readme-template.md
│   ├── general-kb-template.md
│   ├── worklog-readme-template.md
│   ├── one-pager-template.md
│   ├── project-charter-template.md
│   ├── code-commenting-dual-audience.md
│   ├── writing-style-guide.md
│   ├── tagging-strategy.md
│   ├── script-header-python.md
│   ├── script-header-shell.md
│   ├── script-header-powershell.md
│   └── README.md
├── ai-instructions.md               # Behavioral guidelines for AI assistants
├── ai-setup.md                      # How to connect an AI assistant to the project
├── game-design-document.md          # Learning experience design: thesis, rounds, outcomes
├── getting-started.md               # Step-by-step walkthrough from fork to first PR
└── README.md                        # This file
```

---

## 2. Files

| File | Description | Status |
|------|-------------|--------|
| [getting-started.md](getting-started.md) | Step-by-step walkthrough: fork, clone, orient, branch, build, PR, merge | Active |
| [ai-setup.md](ai-setup.md) | How to connect an AI assistant to the project and what to give it | Active |
| [ai-instructions.md](ai-instructions.md) | Behavioral guidelines: the AI's role, how it should interact with participants | Active |
| [game-design-document.md](game-design-document.md) | Learning experience design: thesis, round structure, what gets learned | Active |

---

## 3. Subdirectories

| Directory | Description |
|-----------|-------------|
| [documentation-standards/](documentation-standards/README.md) | Template library for READMEs, KB articles, charters, one-pagers, script headers, and guidelines |

---

## 4. Related

| Document | Relationship |
|----------|--------------|
| [Repository Root](../README.md) | Parent directory |
| [AGENTS.md](../AGENTS.md) | AI assistant context, references these docs |
| [CONTRIBUTING.md](../CONTRIBUTING.md) | Branch and PR process |
| [GIT-REFERENCE.md](../GIT-REFERENCE.md) | Git command cheat sheet |
