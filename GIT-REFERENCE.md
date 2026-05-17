<!--
---
title: "Git Reference"
description: "Command cheat sheet for the Git workflow used in this project"
author: "radioastronomyio"
date: "2026-05-17"
version: "2.0"
status: "Active"
tags:
  - type: reference
  - domain: git-workflow
---
-->

# Git Reference

Quick lookup for the commands you'll use in this project. This is not a tutorial. Read `CONTRIBUTING.md` first to understand the workflow, then come back here when you forget the syntax.

---

## 1. First Time Setup

Fork the repo on GitHub, then clone your fork:

```bash
git clone https://github.com/your-username/learn-git-spec-driven-gaming.git
cd learn-git-spec-driven-gaming
```

Set your identity (once per machine):

```bash
git config user.name "Your Name"
git config user.email "your-email@example.com"
```

---

## 2. Starting Work

Always start from a clean, up-to-date main:

```bash
git checkout main
git pull origin main
git checkout -b your-name/feature-description
```

---

## 3. Checking Status

See what's changed:

```bash
git status
```

See the actual changes line by line:

```bash
git diff
```

See the log of recent commits:

```bash
git log --oneline -10
```

---

## 4. Committing

Stage all changes:

```bash
git add .
```

Stage specific files:

```bash
git add game/index.html
git add spec/round-1-features.md
```

Commit with a message:

```bash
git commit -m "add particle effects on brick break"
```

---

## 5. Pushing

Push your branch to GitHub:

```bash
git push origin your-name/feature-description
```

First push of a new branch (sets upstream tracking):

```bash
git push -u origin your-name/feature-description
```

---

## 6. Pull Requests

Open a PR from the command line (requires `gh` CLI):

```bash
gh pr create --title "Add particle effects" --body "Bricks now burst with colored particles when hit." --reviewer teammate-username
```

Or open a PR on GitHub: go to the repo page, click "Compare & pull request" after pushing your branch.

List open PRs:

```bash
gh pr list
```

Check out someone's PR branch to playtest it:

```bash
git fetch origin
git checkout their-name/feature-description
```

---

## 7. Merging

After PR approval, merge on GitHub (click the merge button) or from the command line:

```bash
gh pr merge --merge
```

Then update your local main:

```bash
git checkout main
git pull origin main
```

Delete the merged branch locally:

```bash
git branch -d your-name/feature-description
```

---

## 8. Merge Conflicts

When Git tells you there's a conflict after pulling:

```bash
git pull origin main
# Git reports a conflict
```

Open the conflicted file. Look for the markers:

```
<<<<<<< HEAD
your version of the code
=======
their version of the code
>>>>>>> main
```

Edit the file to keep what's correct. Remove all the markers. Then:

```bash
git add .
git commit -m "resolve merge conflict in game/index.html"
```

---

## 9. Undo Mistakes

Discard all uncommitted changes (careful, this is permanent):

```bash
git checkout -- .
```

Unstage a file you accidentally added:

```bash
git reset HEAD game/index.html
```

Undo the last commit but keep the changes:

```bash
git reset --soft HEAD~1
```

---

## 10. Quick Reference Table

| What you want to do | Command |
|---------------------|---------|
| Clone your fork | `git clone https://github.com/you/learn-git-spec-driven-gaming.git` |
| Create a branch | `git checkout -b name/description` |
| See what changed | `git status` |
| Stage everything | `git add .` |
| Commit | `git commit -m "message"` |
| Push | `git push origin name/description` |
| Switch to main | `git checkout main` |
| Update main | `git pull origin main` |
| Check out someone's branch | `git fetch origin && git checkout their-branch` |
| Open a PR | `gh pr create` |
| Delete a local branch | `git branch -d name/description` |
