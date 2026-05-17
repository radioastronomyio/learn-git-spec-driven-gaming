<!--
---
title: "Specifications"
description: "Specs for Breakout game development, organized by round"
author: "msp4-don"
date: "2026-05-05"
version: "1.0"
status: "Active"
tags:
  - type: directory-readme
  - domain: specs
---
-->

# Specifications

Specs for the Breakout game, organized by development round. Each spec defines what the game should do in game terms. The agent figures out implementation.

---

## 1. Contents

```
spec/
├── baseline.md               # Minimum viable Breakout (non-negotiable foundation)
├── round-1-features.md       # Greg's feature menu (pick 3-5)
├── round-2-features.md       # Drew's feature menu (pick 3-5)
├── preflight-review.md       # Pre-commit repo review spec
└── README.md                 # This file
```

---

## 2. Files

| File | Description | Status |
|------|-------------|--------|
| [baseline.md](baseline.md) | What Breakout must be before any features are added | Active |
| [round-1-features.md](round-1-features.md) | Cosmetic and foundational features for Greg | Active |
| [round-2-features.md](round-2-features.md) | Gameplay-focused features for Drew | Active |
| [preflight-review.md](preflight-review.md) | Pre-commit repo review spec for agent dispatch | Active |

---

## 3. How Specs Work Here

The traditional spec format (deliverables, validation pairs, execution environment) still applies. The difference is that validation is playtesting, not automated checks.

A spec for this project describes:

1. What the feature looks like when it's working (in game terms)
2. What "wrong" looks like (edge cases a playtester should watch for)
3. Any constraints (performance, no external dependencies, single-file)

The engineer writes the spec with help from their Claude instance. The agent on agents01 builds it. The engineer playtests. If it's wrong, the spec gets refined and the agent tries again.

---

## 4. Related

| Document | Relationship |
|----------|--------------|
| [Repository Root](../README.md) | Parent directory, round structure |
| [AGENTS.md](../AGENTS.md) | Agent constraints for game implementation |
| [SUGGESTIONS.md](../SUGGESTIONS.md) | Feature backlog for Round 3 and beyond |
| [CONTRIBUTING.md](../CONTRIBUTING.md) | Branch and PR process for submitting completed work |
