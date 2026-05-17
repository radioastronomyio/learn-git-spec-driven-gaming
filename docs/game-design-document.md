<!--
---
title: "Game Design Document"
description: "How the learning experience works: thesis, rounds, workflow, outcomes"
author: "radioastronomyio"
date: "2026-05-17"
version: "2.0"
status: "Active"
tags:
  - type: guide
  - domain: [game, git-workflow, specs]
  - tech: [javascript, html, css, canvas]
related_documents:
  - "[Repository Root](../README.md)"
  - "[Baseline Spec](../spec/baseline.md)"
  - "[Round 1 Features](../spec/round-1-features.md)"
  - "[Round 2 Features](../spec/round-2-features.md)"
  - "[Suggestions](../SUGGESTIONS.md)"
  - "[Contributing](../CONTRIBUTING.md)"
---
-->

# Game Design Document

This document describes the design of the learning experience, not the game. The game is Breakout. The learning experience is Git workflow, spec-driven development, and domain validation. The game is the vehicle; the skills are the destination.

---

## 1. Core Thesis

The traditional code review falls apart when the reviewer can't read the code. That's not a failure of the reviewer; it's a failure of the process. The question isn't "can you review this JavaScript?" It's "does this game work the way the spec says it should?"

Domain expertise is the validation layer. A gamer knows when physics feel wrong, when a power-up is overpowered, when the ball clips through a wall. That judgment doesn't require reading a single line of code. The spec describes what the game should do. The playtest reveals whether it does. The pull request captures the discussion. Git tracks the whole history.

This project makes that thesis concrete. Participants write specs describing what the game should do in game terms. An AI builds it. They play it. If something is off, they refine the spec and the AI tries again. The code is abstracted away. The spec, source-controlled alongside the code, is the artifact the human owns.

Git becomes incidental to the work. Nobody studies branching in the abstract. They branch because they're adding a feature and need to keep it separate from what someone else is building. Pull requests aren't an exercise; they're how you share your game with your teammate for playtesting. The tool becomes obvious through use.

---

## 2. The Team

This project works with two or more participants. The round structure scales to the team size.

| Team Size | Round Structure |
|-----------|----------------|
| 2 | Participant A builds (Round 1), Participant B extends (Round 2). Each reviews the other's PR. |
| 3 | A builds, B extends, C polishes. C's PR requires approval from both A and B. |
| 4+ | Add rounds or split a round between parallel participants. Parallel work on the same codebase introduces merge conflicts naturally. |

Roles rotate through rounds. The person who builds in Round 1 reviews in Round 2. The person who extends in Round 2 reviews in Round 3. Everyone experiences both sides of the PR process: proposing changes and evaluating someone else's work.

If participants have different levels of experience, the more experienced one should take Round 1. The baseline requires more comfort with iterating on AI output and debugging specs. By Round 2, the second participant has seen the process work through reviewing the Round 1 PR and is ready to drive.

---

## 3. The Game

Breakout. HTML, CSS, and vanilla JavaScript. No frameworks, no build tools, no server required. Open `game/index.html` in a browser and play.

Breakout is the right choice for several reasons. It's simple enough that a single prompt to an AI produces a working game. The feature space is large: visual effects, physics, power-up systems, level design, scoring, sound, UI. Every feature is a self-contained unit of work that maps to a branch and a PR. The quality bar is intuitive. Everyone knows what Breakout should feel like. You don't need to read code to know if the ball is bouncing wrong.

The game uses pixel art sprites from the included asset pack (see `assets/`). The pack provides paddles, balls, blocks (with damage states), power-up icons (with animations), and a star sky background. Fonts and music loops are also included. All assets are free-licensed for commercial use.

---

## 4. The Three Rounds

### Round 1: Build the Foundation

The first participant receives two documents: the baseline spec (`spec/baseline.md`) and a curated feature menu (`spec/round-1-features.md`).

The baseline defines minimum viable Breakout: canvas, paddle, ball, bricks, bounce physics, score, lives, win/lose, pause, restart. This is non-negotiable. The AI builds all of it using the included sprite assets and star background.

The feature menu offers options that are visually rewarding and self-contained: sound effects, particle effects, ball trails, speed ramps, level progression. The participant picks 3 to 5 features, writes specs for each with their AI assistant, has the AI build them, and playtests until satisfied.

**Workflow:**

1. Read the baseline spec and the Round 1 feature menu
2. Create a branch (`your-name/baseline-breakout`)
3. Work with the AI to build the baseline game
4. Playtest by opening `game/index.html` in the browser
5. Iterate until the baseline is solid
6. Add chosen features one at a time, playtesting after each
7. Commit, push, and open a PR requesting review from the next participant

**What gets learned:** Fork, clone, branch, commit, push, open a PR. How to write a spec that an AI can execute. How to iterate when the output is wrong (refine the spec, not the code). The discipline of reading a repository before working in it.

### Round 2: Extend the Gameplay

The second participant receives the Round 1 PR. Their first job is to playtest, not read code.

They pull the branch, open `game/index.html`, and play the game. If it works, they approve and merge. If something is off, they leave a review comment describing the gameplay issue ("ball clips through the paddle on the left edge") and the first participant fixes it.

After merge, the second participant gets their own feature menu (`spec/round-2-features.md`). These features are gameplay-focused and build on the existing foundation: power-up drops (using the sprites from the asset pack), multi-hit bricks (using the damage-state sprites), sticky paddle, combo scoring, indestructible bricks. They interact with Round 1 features, so playtesting for side effects matters.

**Workflow mirrors Round 1:** branch, spec, AI builds, playtest, iterate, commit, PR. The PR goes back to the first participant, who playtests the additions.

**What gets learned:** Everything from Round 1, plus: reviewing a PR through playtesting, leaving constructive review comments in game terms, pulling someone else's branch, testing for feature interactions, and the experience of building on top of existing code.

### Round 3: Polish (Teams of 3+)

The third participant receives the game after two rounds. The foundation is solid, the gameplay is engaging. They pick from any feature in `SUGGESTIONS.md` or invent new ones: gravity, procedural levels, a level editor, weather effects, achievements, mobile touch controls.

Their PR requires approval from the previous participants. They built this game. They know what it should feel like. All must agree that the additions improve it.

**What gets learned:** Multi-reviewer PRs. The experience of reviewing changes to something you built and have ownership over. The dynamic shifts: the polisher proposes, the builders judge.

---

## 5. The Workflow Loop

Every feature, in every round, follows the same loop:

```
Write spec  →  AI builds  →  Playtest  →  Iterate  →  Commit  →  PR  →  Review  →  Merge
     ↑                                         |
     └──────────── refine spec ────────────────┘
```

The spec is written in game terms. "Bricks that take multiple hits and change appearance as they weaken." The AI translates that into JavaScript. The participant plays the game and decides if it's right. If the bricks don't change appearance, or the change is too subtle, or the ball bounces wrong off a damaged brick, the spec gets refined. The AI gets another pass. The loop continues until the participant is satisfied.

The participant never needs to understand the code. The spec is their artifact. The playtest is their validation. The Git history records the whole journey.

---

## 6. What Gets Learned (Without Being Taught)

The design deliberately avoids tutorials. Nobody reads a chapter on branching and then does an exercise. They branch because the work requires it. The learning is a side effect of doing real work.

| Skill | How it's learned |
|-------|------------------|
| `fork` | First thing you do to get your own copy |
| `git clone` | How you get the fork onto your machine |
| `git checkout -b` | You need a branch before you can change anything |
| `git add` / `git commit` | You finished a feature and want to save it |
| `git push` | You need your teammate to see your work |
| Pull requests | The only way to get code into main |
| PR review | You have to play the game to approve it |
| Review comments | "The paddle is too fast" is a review comment |
| Merge | Your PR was approved, now it's in main |
| Merge conflicts | You and your teammate both edited index.html |
| Branch protection | Main requires approval; you can't skip the review |
| Multi-reviewer PRs | Round 3 requires all builders to approve |
| Spec writing | The AI needs clear instructions to build the right thing |
| Iteration | The first build is rarely right; refine and retry |
| Domain validation | You know it's right because you played it, not because you read the code |

---

## 7. The Asset Pack

The game is built with pixel art sprites from the Pixeltier Breakout Asset Pack (included in `assets/pixeltiers-breakout-asset-pack/`). The pack provides:

| Category | Contents |
|----------|----------|
| Paddles | 4 styles, 3 sizes (small, mid, large), 5 metallic colors. 60 sprites total. |
| Blocks | 5 intact types + 3 damage states, 2 sizes (standard, mid), 12 colors. 168 sprites total. Plus 3-frame gloss animation overlay. |
| Balls | 4 designs (some animated), 12 colors. 120 sprites total. |
| Power-ups | 7 types (extra ball, grow, power ball, reverse, shield, split, twin balls), each with 4-frame animation. |
| Background | Star sky, two resolutions. |

The pack's damage states (broken_1, broken_2, broken_3) give multi-hit bricks visual feedback without any custom art. The three paddle sizes support the grow power-up visually. The seven power-up types with animations are ready to wire into gameplay.

Additional assets included: free pixel fonts (OPF family, Pixbob family) and royalty-free music loops (Torone loop pack, .ogg format) for background music and stingers.

All assets are free-licensed for personal and commercial use. See `assets/README.md` for license details per pack.

---

## 8. The Suggestion Backlog

`SUGGESTIONS.md` contains 50+ feature ideas organized by game design complexity: visual polish, gameplay mechanics, power-ups, physics, level design, system features, and ambitious multi-PR projects.

Any future participant can clone (or fork) this repo, pick a feature from the backlog, and go through the same loop. The repo teaches itself. The game grows with each person who touches it.

---

## 9. Generalizing Beyond Breakout

This document describes a breakout game, but the structure generalizes cleanly:

- The three-round framework (Build, Extend, Polish) works with any team of two or more
- The feature menus can be rebalanced for different skill levels
- The game could be anything with a large feature space and intuitive quality signals: a tower defense game, a platformer, a puzzle game, a roguelite
- The thesis holds regardless of the game: specs are the artifact participants own, domain expertise is the validation, and Git is learned through use

---

## Document Info

| | |
|---|---|
| Author | radioastronomyio |
| Created | 2026-05-17 |
| Version | 2.0 |
