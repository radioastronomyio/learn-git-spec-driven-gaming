<!--
---
title: "Pre-Flight Repo Review"
description: "Agent dispatch spec for repository quality review before first commit"
author: "msp4-don"
date: "2026-05-05"
version: "1.0"
status: "Active"
tags:
  - type: specification
  - domain: [documentation, specs, infrastructure]
  - tech: [bash, nginx, playwright]
related_documents:
  - "[Repository Root](../README.md)"
  - "[Writing Style Guide](../docs/documentation-standards/writing-style-guide.md)"
  - "[Tagging Strategy](../docs/documentation-standards/tagging-strategy.md)"
---
-->

## Task: Pre-Flight Repo Review
Branch: `don/preflight-review`
Mode: Code

### Objective

Review and refine the entire `learn-git-breakout` repository before first commit. Verify writing standards, template compliance, feature quality, cross-references, and infrastructure references. Fix everything you find. Leave a report at `work-logs/worklog-2026-05-05-preflight-review.md`.

---

### Context

This is a Git and spec-driven development training repository. Three engineers learn Git by building a Breakout game through spec-driven agent development. The repo has been scaffolded from an MSP4 project template and hydrated with project-specific content. It has never been committed or pushed. You are doing the final quality pass before `git init` and first commit.

The repo will live on the shared coding server at `/opt/agents/repos/learn-git-breakout`. nginx is installed as a systemd service serving from `/opt/agents/www/dev.labby.site`. Certbot handles TLS for the `dev.labby.site` subdomain. The game deploys by copying `game/` contents to the nginx site root.

---

### Scope

**Modify:** Everything in the repo. You have full write access. Fix problems in place.

**Reference (read but do not modify):**
- `docs/documentation-standards/writing-style-guide.md` (the writing rules you're enforcing)
- `docs/documentation-standards/tagging-strategy.md` (the tag vocabulary you're validating against)
- `docs/documentation-standards/code-commenting-dual-audience.md` (commenting standards)
- All templates in `docs/documentation-standards/` (the patterns documents should follow)

---

### Deliverables & Validation

1. **Writing standards audit and fix**
   - [ ] No em dashes anywhere in the repo. Replace with commas, colons, semicolons, parentheses, or restructured sentences.
   - [ ] No theatrical negation parallelism that contrasts X with Y instead of stating the point directly.
   - [ ] No inflated significance words or phrases called out by the writing style guide.
   - [ ] No editorializing prefaces called out by the writing style guide.
   - [ ] No overused transition crutches called out by the writing style guide. Occasional use is fine; repeated use in the same document is not.
   - [ ] No trailing -ing clauses that add hollow commentary ("ensuring accessibility," "highlighting the importance").
   - [ ] No bold-title bullet list pattern (bolded keyword + colon + sentence restating the keyword).
   - [ ] Sentence length varies within and between paragraphs. No uniform-length sentence blocks.
   - [ ] Read the full writing style guide at `docs/documentation-standards/writing-style-guide.md` before starting. It is the authoritative source.

2. **Template and frontmatter compliance**
   - [ ] Every Markdown file (except CLAUDE.md and files in internal-files/) has YAML frontmatter in an HTML comment block.
   - [ ] All `type` tags use values from the tagging strategy's Type Tags table (section 5).
   - [ ] All `domain` tags use values from the tagging strategy's Domain Vocabulary (section 4): `game`, `git-workflow`, `specs`, `testing`, `infrastructure`, `documentation`.
   - [ ] All `tech` tags use values from the tagging strategy's Tech Tags list (section 7).
   - [ ] All `author` fields read `"msp4-don"`. No organization URL appears in place of the author name.
   - [ ] All repo URL references point to `https://github.com/MSP4-LLC/learn-git-breakout`.
   - [ ] Directory READMEs follow the interior-readme-template pattern (Contents tree, Files table, Subdirectories table, Related table).
   - [ ] Semantic section numbering is consistent. Omitted sections preserve their number gap (1, 2, 4 is correct if 3 is omitted; never renumber).
   - [ ] The `code-commenting-dual-audience.md` file has no YAML frontmatter. This is the one exception in `docs/documentation-standards/`. Leave it as-is.

3. **Feature list review and refinement**
   - [ ] `spec/round-1-features.md` has 8 features. Verify each is distinct, well-described, and appropriately scoped for a first round (visual polish and foundational improvements, not gameplay overhauls).
   - [ ] `spec/round-2-features.md` has 8 features. Verify each is distinct, gameplay-focused, and builds on the Round 1 foundation. Check that the "watch for" sections account for interactions with Round 1 features.
   - [ ] `SUGGESTIONS.md` has 50+ features across 7 categories. Verify no duplicates between SUGGESTIONS.md and the round feature menus. Verify no duplicates within SUGGESTIONS.md. Each feature should be distinct enough to stand on its own as a branch/PR.
   - [ ] If you find thin descriptions, flesh them out. If you find features that are too similar, merge or differentiate them. If you see obvious gaps in the feature space, add new features.
   - [ ] Every feature in every file is described in game terms, not code terms. "The ball curves based on where it hits the paddle" is correct. "Modify the velocity vector based on paddle hit offset" is not.
   - [ ] Round 1 instructions say "pick 3 to 5." Round 2 instructions say "pick 3 to 5." Verify these counts appear in both the heading area and the closing instructions section of each file.

4. **Cross-reference integrity**
   - [ ] Every Markdown link using a local path resolves to an actual file in the repo.
   - [ ] The root README's Repository Structure tree matches the actual directory tree.
   - [ ] The docs/README.md Contents tree matches the actual contents of `docs/`.
   - [ ] The spec/README.md file table lists all spec files that exist.
   - [ ] Related tables in directory READMEs point to files that exist.

5. **Infrastructure references**
   - [ ] `deploy.sh` uses `/opt/agents/www/dev.labby.site` as the site root to match the actual nginx configuration on agents01.
   - [ ] Any reference to the repo path on agents01 should use `/opt/agents/repos/learn-git-breakout`.
   - [ ] `AGENTS.md` mentions the agents01 IP correctly (`69.87.191.16:9278` if referenced).
   - [ ] `tests/README.md` prerequisites section is accurate for the agents01 environment.
   - [ ] The `game/README.md` deploy instructions are consistent with `deploy.sh`.

6. **AGENTS.md and CLAUDE.md sanity check**
   - [ ] `AGENTS.md` context loading order is logical and references files that exist.
   - [ ] `AGENTS.md` architectural constraints are consistent with the baseline spec.
   - [ ] `CLAUDE.md` contains only "See AGENTS.md for all agent context." and nothing else.
   - [ ] The constraint "single HTML file, no frameworks" appears in both `AGENTS.md` and `spec/baseline.md` and they agree.

7. **General pre-flight**
   - [ ] `.gitignore` covers `recycle/`, `internal-files/`, `node_modules/`, Playwright output directories, and IDE config files.
   - [ ] `cspell.json` word list includes project-relevant terms (breakout, canvas, playwright, nginx, labby, certbot, codex).
   - [ ] No orphaned files (files that exist but are not referenced or reachable from any README or navigation).
   - [ ] No placeholder text remains from the template set.
   - [ ] `deploy.sh` is executable (`chmod +x` if not already set; note this in your report if the filesystem doesn't support it).

8. **Pre-flight report**
   - [ ] `work-logs/worklog-2026-05-05-preflight-review.md` created using the worklog template from `docs/documentation-standards/worklog-readme-template.md`.
   - [ ] Report includes: total files reviewed, issues found by category, fixes applied, features added or refined, and any items that need human decision (flag these clearly).

---

### Constraints

- Do not modify any file in `docs/documentation-standards/` that is a template (files with `template` in the name, plus `tagging-strategy.md`, `writing-style-guide.md`, `code-commenting-dual-audience.md`). These are reference standards. Read them, enforce them, do not change them.
- Do not create new directories. The directory structure is final.
- Do not touch `.vscode/settings.json` or `.markdownlint.json`.
- The game placeholder at `game/index.html` is intentionally minimal. Do not add game code.
- When adding or refining features in SUGGESTIONS.md or the round feature menus, write in game terms only. No code, no implementation details, no framework references.
- Follow the writing style guide yourself. Your own output (the report, any refined feature descriptions) must also pass the writing standards.

---

**Environment:**
- Executor: Codex (GPT-5.5) or Claude Code
- Platform: Ubuntu 24.04 (agents01)
- Working directory: `/opt/agents/repos/learn-git-breakout`
- nginx site root: `/opt/agents/www/dev.labby.site`
- Certbot TLS: configured for `dev.labby.site`
- Shell: bash
- Node.js and Playwright available for test infrastructure verification
- Git is available but do not commit. This is a pre-commit review.
