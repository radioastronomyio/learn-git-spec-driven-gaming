<!--
---
title: "Pre-Flight Repo Review"
description: "Repository quality pass before first commit"
author: "msp4-don"
date: "2026-05-05"
version: "1.0"
status: "Complete"
tags:
  - type: worklog
  - domain: [documentation, specs, infrastructure]
  - tech: [bash, nginx, playwright]
related_documents:
  - "[Preflight Spec](../spec/preflight-review.md)"
  - "[Repository Root](../README.md)"
  - "[Writing Style Guide](../docs/documentation-standards/writing-style-guide.md)"
---
-->

# Pre-Flight Repo Review

## Summary

| Attribute | Value |
|-----------|-------|
| Status | Complete |
| Sessions | 1 |
| Artifacts | 1 script, 14 docs, 1 config |

Objective: Review the repository before first commit, fix writing, metadata, navigation, feature-list, and infrastructure issues, and record the results.

Outcome: Reviewed 40 repo files before creating this report. Applied targeted fixes across documentation, specs, the deploy script, spell-check vocabulary, and feature backlog. No game code was added.

---

## 1. Work Completed

| Task | Description | Result |
|------|-------------|--------|
| Writing standards audit | Scanned live project files for banned prose patterns, placeholder text, stale paths, and bold-title bullet lists. Protected documentation-standard templates were treated as references. | Clean for non-protected project files after fixes. |
| Template and frontmatter audit | Checked Markdown frontmatter presence, author fields, type tags, domain tags, and tech tags against the tagging strategy. | Added frontmatter to AGENTS.md and preflight-review.md. Validation passes for non-protected project files. |
| Feature list review | Verified Round 1 and Round 2 each have 8 features and that both menus say to pick 3 to 5 features near the top and in closing instructions. | Removed direct backlog duplicates from SUGGESTIONS.md and added distinct ideas, leaving 61 suggestions across 7 categories. |
| Cross-reference review | Checked local Markdown links in non-protected project files and compared navigation tables against repo contents. | Local link validation passes. README structure now includes preflight-review.md and repo config files. |
| Infrastructure review | Checked deploy path, agents01 references, tests guidance, and game deploy docs. | Updated deploy.sh to use /opt/agents/www/dev.labby.site and clarified tests prerequisites. |
| General preflight | Checked .gitignore coverage, cspell vocabulary, orphaned pending files, and CLAUDE.md content. | Added Azure terms to cspell and moved the superseded work-logs pending README into recycle with a documented reason. |

---

## 2. Files Changed

| File | Change |
|------|--------|
| [../AGENTS.md](../AGENTS.md) | Added frontmatter and removed bold-title bullets from the toolchain section. |
| [../README.md](../README.md) | Updated the repository structure tree to include current spec and config files. |
| [../SUGGESTIONS.md](../SUGGESTIONS.md) | Removed feature-menu duplicates, removed bold-title bullet formatting, and added distinct backlog items. |
| [../assets/README.md](../assets/README.md) | Removed placeholder asset links and revised convention labels. |
| [../cspell.json](../cspell.json) | Added Azure-related project terms. |
| [../deploy.sh](../deploy.sh) | Updated nginx site root from the stale path to /opt/agents/www/dev.labby.site. |
| [../docs/documentation-standards/README.md](../docs/documentation-standards/README.md) | Removed bold-title bullet formatting in the principles section. |
| [../recycle/README.md](../recycle/README.md) | Documented the recycled pending work-log README. |
| [../recycle/work-logs-README-pending.md](../recycle/work-logs-README-pending.md) | Moved from work-logs/README-pending.md because work-logs/README.md now exists. |
| [../spec/preflight-review.md](../spec/preflight-review.md) | Added frontmatter and removed self-triggering placeholder and banned-pattern examples. |
| [../spec/round-1-features.md](../spec/round-1-features.md) | Added the 3 to 5 selection count to the closing instructions. |
| [../spec/round-2-features.md](../spec/round-2-features.md) | Reworded the intro, removed bold-title option bullets, and added the 3 to 5 selection count to closing instructions. |
| [../staging/README.md](../staging/README.md) | Removed bold-title convention labels. |
| [../tests/README.md](../tests/README.md) | Clarified agents01 Node.js and Playwright prerequisites. |
| [../work-logs/README.md](../work-logs/README.md) | Replaced live placeholder date patterns with concrete examples and removed bold-title labels. |
| [worklog-2026-05-05-preflight-review.md](worklog-2026-05-05-preflight-review.md) | Created this report. |

---

## 3. Issues Encountered

| Issue | Resolution |
|-------|------------|
| ripgrep was not runnable from the Codex Windows app package. | Used native PowerShell and bundled Node.js validation scripts instead. |
| The working copy is not a Git repository yet. | Skipped git status and commit checks, consistent with the pre-first-commit scope. |
| deploy.sh executable bit could not be verified or set on this Windows filesystem. | Recorded this as a human follow-up for agents01. |
| No Playwright test files or package.json exist yet. | Verified test infrastructure documentation only; no test suite was available to run. |
| Protected documentation-standard templates contain literal examples with em dashes and placeholder dates. | Left them unchanged because the spec says to read and enforce those standards without modifying them. |

---

## 4. Next Steps

Handoff: The repository is ready for human review before initialization and first commit, with one platform-specific check remaining for agents01.

1. On agents01, run `chmod +x deploy.sh` if the executable bit is not already set.
2. Initialize Git and make the first commit after human review.

<!-- Source: Codex session, 2026-05-05 -->
