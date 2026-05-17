<!--
---
title: "Getting Started"
description: "Step-by-step walkthrough from fork to first PR"
author: "radioastronomyio"
date: "2026-05-17"
version: "1.0"
status: "Active"
tags:
  - type: guide
  - domain: [git-workflow, onboarding]
---
-->

# Getting Started

This guide walks you through the full process: forking the repository, cloning it, orienting yourself, connecting an AI assistant, and starting your first round of development. Each step introduces a Git concept through use, not lecture. By the time you open your first pull request, you'll have practiced every core Git operation.

Prerequisites: a GitHub account, Git installed on your machine, a modern web browser, and access to an AI assistant (see `ai-setup.md` for options).

---

## 1. Fork the Repository

A fork is your personal copy of the entire repository. It lives on your GitHub account (or your organization's account), separate from the original. You can change anything in your fork without affecting the source. This is how open-source collaboration works: everyone works on their own copy, then proposes changes back.

**To fork into your personal account:**

1. Go to the repository page on GitHub
2. Click the "Fork" button in the top right
3. GitHub creates a copy under `github.com/your-username/learn-git-spec-driven-gaming`

**To fork into an organization:**

1. Click the "Fork" button
2. In the "Owner" dropdown, select your organization instead of your personal account
3. GitHub creates the copy under `github.com/your-org/learn-git-spec-driven-gaming`

Forking into an org is useful when the project is a team exercise within a company or class. Everyone on the team works in the org's fork. The upstream repository stays untouched.

After forking, your fork is an independent repository. It has its own branches, its own issues, and its own settings. GitHub remembers where it came from, which lets you pull updates from the original later if needed.

---

## 2. Clone Your Fork

Cloning downloads your fork to your local machine. This is where you'll do all your work.

```bash
git clone https://github.com/your-username/learn-git-spec-driven-gaming.git
cd learn-git-spec-driven-gaming
```

Replace `your-username` with your GitHub username (or org name if you forked into an org).

After cloning, you have the complete repository on your machine: all the specs, all the assets, the game directory, the documentation. Everything is local. You don't need an internet connection to work on the game, only to push your changes back to GitHub.

---

## 3. Orient Yourself

Before you touch anything, read through the repository. Open folders. Read the README. Skim the specs. Look at the assets.

This matters for two reasons.

First, you're about to hand this repository's contents to an AI assistant. The AI will read whatever you give it and follow the instructions it finds. If someone put something malicious or misleading in a repo you cloned, and you handed it to an AI without reading it, you'd have a problem. Treat repository contents the way you'd treat any code you downloaded from the internet: review before you trust.

Second, understanding the project structure saves time. You'll know where specs live, where assets are, what the game directory looks like, and what's expected of you in each round. Fifteen minutes of reading now prevents confusion later.

**Key files to read:**

| File | What it tells you |
|------|-------------------|
| `README.md` | Project overview, what you're building, how the rounds work |
| `AGENTS.md` | Context for your AI assistant (read this yourself first) |
| `spec/baseline.md` | What the minimum viable game must do |
| `spec/round-1-features.md` | Feature menu for Round 1 |
| `CONTRIBUTING.md` | Branch naming, commit messages, PR process |
| `assets/README.md` | What's in the asset packs and their licenses |

**Key directories to browse:**

| Directory | Contents |
|-----------|----------|
| `game/` | The game itself (starts as a placeholder) |
| `assets/` | Sprite sheets, fonts, music, reference materials |
| `spec/` | Baseline spec and feature menus for each round |
| `docs/` | Design document, this guide, AI setup, standards |

---

## 4. Set Up Your AI Assistant

The game is built by an AI from your specs. You describe what you want in game terms; the AI writes the code. You playtest by opening `game/index.html` in your browser.

See [ai-setup.md](ai-setup.md) for how to connect your AI assistant to the project. The short version: give your AI the `AGENTS.md` file as its starting context, along with whatever spec you're working from.

---

## 5. Create a Branch

A branch is a separate line of work. You create one before making any changes so your work stays isolated from everyone else's. When you're done, you'll propose merging your branch into `main` through a pull request.

```bash
git checkout -b your-name/baseline-breakout
```

This creates a new branch and switches to it. The naming convention is `your-name/short-description`. See `CONTRIBUTING.md` for details.

From this point on, every change you make is on your branch. The `main` branch stays exactly as it was when you cloned.

---

## 6. Build the Game

This is the core loop. You'll repeat it for the baseline and for each feature you add.

### Write a spec

Open a conversation with your AI assistant. Describe what you want the game to do. Start with the baseline spec (`spec/baseline.md`), which defines the minimum viable breakout game. Your AI has the AGENTS.md context, so it knows the project structure, the assets available, and the conventions to follow.

A good spec describes behavior in game terms: "when the ball hits a brick, the brick disappears and the ball bounces." You're telling the AI what the game should do, not how to code it. The spec is the artifact you own.

### AI builds

The AI produces code (or modifies existing code) based on your spec. It writes to `game/index.html` and may copy assets into `game/assets/`. Review what it produced before moving on.

### Playtest

Open `game/index.html` in your browser. Play the game. Does it match the spec? Does the ball bounce correctly? Do bricks break? Is the score updating?

This is your validation. You don't need to read JavaScript to know if the game feels right. A gamer knows when physics are wrong, when a sound is missing, when a feature doesn't work as described. That domain judgment is the human-in-the-loop review.

### Iterate

If something is off, tell the AI what's wrong in game terms: "the ball clips through the paddle on the left edge" or "bricks in the top row aren't breaking." The AI adjusts. You playtest again. Repeat until satisfied.

### Commit

When a feature works correctly, save your progress:

```bash
git add .
git commit -m "add baseline breakout with paddle, ball, and bricks"
```

The commit message describes what changed, present tense, imperative mood. See `CONTRIBUTING.md` for conventions.

### Push

Send your branch to GitHub:

```bash
git push origin your-name/baseline-breakout
```

The first time you push a new branch, Git may ask you to set the upstream. Follow the suggestion it prints, or use:

```bash
git push -u origin your-name/baseline-breakout
```

After the first push, `git push` alone works for subsequent commits on the same branch.

---

## 7. Open a Pull Request

A pull request (PR) is a proposal to merge your branch into `main`. It's how your teammates see your work and how the review process starts.

**On GitHub:**

1. Go to your fork's page on GitHub
2. GitHub usually shows a banner offering to create a PR for your recently pushed branch. Click it.
3. Write a title and description. The description should say what you built and what to look for when playtesting.
4. Assign your teammate(s) as reviewers
5. Submit the PR

**What happens next:**

Your reviewer pulls your branch, opens `game/index.html`, and plays the game. They don't read your code. They play the game and report what they find: "the speed ramp feels too aggressive after level 3" or "sound effects work great, the brick-break sound is satisfying."

If they find issues, they leave comments on the PR. You fix the issues (back to the loop: tell the AI, playtest, commit, push). The PR updates automatically with your new commits.

If the game plays well, they approve the PR.

---

## 8. Merge

Once approved, merge the PR on GitHub. The "Merge pull request" button does this. Your work is now in `main`.

Delete the branch after merging (GitHub offers a button). The branch served its purpose; the work lives in main now.

---

## 9. Next Round

The next participant pulls `main`, creates their own branch, and starts building from the new feature menu. The game grows with each round.

```bash
git pull origin main
git checkout -b next-person/power-ups
```

Round 2 builds on Round 1. Round 3 builds on Round 2. Each round introduces more Git complexity naturally: working with someone else's code, handling merge conflicts if they arise, multi-reviewer PRs in later rounds.

The loop stays the same throughout: spec, build, playtest, iterate, commit, push, PR, review, merge.

---

## Quick Reference

| What you want to do | Command |
|---------------------|---------|
| Clone your fork | `git clone https://github.com/you/learn-git-spec-driven-gaming.git` |
| Create a branch | `git checkout -b your-name/feature` |
| See what's changed | `git status` |
| Stage everything | `git add .` |
| Commit | `git commit -m "your message"` |
| Push | `git push origin your-name/feature` |
| Pull latest main | `git pull origin main` |
| Switch branches | `git checkout branch-name` |

See `GIT-REFERENCE.md` for the full cheat sheet.
