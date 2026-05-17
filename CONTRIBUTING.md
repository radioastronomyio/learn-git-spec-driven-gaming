<!--
---
title: "Contributing"
description: "Branch naming, commit messages, and PR process"
author: "radioastronomyio"
date: "2026-05-17"
version: "2.0"
status: "Active"
tags:
  - type: guide
  - domain: git-workflow
---
-->

# Contributing

This document defines how participants work together in this repository. Read it once before your first commit. Reference it when you forget a convention.

---

## 1. Branch Naming

All work happens on branches. Never commit directly to `main`.

Format: `<your-name>/<short-description>`

Examples:

```
alex/baseline-breakout
sam/power-ups
jordan/gravity-physics
alex/fix-paddle-clipping
```

Keep descriptions short, lowercase, hyphenated. The name prefix tells everyone whose work it is at a glance.

---

## 2. Commit Messages

Present tense, imperative mood. Describe what the commit does, not what you did.

```
add particle effects on brick break
fix ball speed reset between levels
update baseline spec with sound requirements
```

First line stays under 72 characters. If you need more detail, leave a blank line and add a body:

```
add multi-hit brick mechanic

Bricks start with the intact sprite, swap to broken_1 after one hit,
broken_2 after two, and break on the third. Color-matched damage
sprites from the Pixeltier asset pack.
```

---

## 3. The PR Workflow

This is the workflow for every change. No exceptions.

### Making Changes

1. Pull the latest `main`: `git pull origin main`
2. Create your branch: `git checkout -b your-name/feature-description`
3. Do your work (write specs, have the AI build, playtest locally)
4. Stage your changes: `git add .`
5. Commit: `git commit -m "your message here"`
6. Push your branch: `git push origin your-name/feature-description`
7. Open a PR on GitHub (web UI or `gh pr create`)

### Reviewing a PR

When someone assigns you as a reviewer:

1. Pull their branch locally: `git fetch origin` then `git checkout their-name/feature-description`
2. Open `game/index.html` in your browser
3. Play the game
4. If something is wrong, leave a comment on the PR describing what you experienced (not what's wrong in the code)
5. If it plays well, approve the PR

### Merging

The PR author merges after receiving the required approvals. Round 1 and Round 2 PRs require one approval. Round 3 PRs (if applicable) require approval from all previous participants.

After merging, delete the branch (GitHub offers a button for this).

---

## 4. Review Standards

You are reviewing the game, not the code. Your job is to play it and report what you find.

Good review comments:

- "The ball clips through the left edge of the paddle when it hits near the corner"
- "Power-ups spawn too frequently, I had 4 multi-balls within 10 seconds"
- "The speed ramp feels good through level 3 but level 4 is impossible"
- "Sound effects work but the brick-break sound is too loud relative to the paddle hit"

These are specific, testable, and grounded in gameplay experience. They go back to the spec, the AI fixes them, and you playtest again.

---

## 5. Conflict Resolution

If two people edit the same file on different branches, Git will flag a merge conflict. This will happen eventually (especially since the game is primarily one file). When it does:

1. Don't panic
2. Pull main into your branch: `git pull origin main`
3. Git will mark the conflicted sections in the file
4. Edit the file to keep the right content
5. Stage and commit the resolution
6. Ask for help from your teammates if you're unsure

See `GIT-REFERENCE.md` for the specific commands.

---

## 6. What Goes Where

| Content | Location |
|---------|----------|
| Game source | `game/index.html` |
| Game assets (in use) | `game/assets/` |
| Asset packs (source) | `assets/` |
| Specs and feature menus | `spec/` |
| Tests | `tests/` |
| Documentation | `docs/` |
| Work session notes | `work-logs/` |
| Feature ideas | `SUGGESTIONS.md` |
