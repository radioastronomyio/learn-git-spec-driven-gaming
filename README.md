<!--
---
title: "Learn Git: Spec-Driven Gaming"
description: "Learn Git and spec-driven development by building a Breakout game with AI"
author: "radioastronomyio"
date: "2026-05-17"
version: "2.0"
status: "Active"
tags:
  - type: project-root
  - domain: [game, git-workflow]
  - tech: [javascript, html, css, canvas]
related_documents:
  - "[radioastronomyio Organization](https://github.com/radioastronomyio)"
  - "[Repository](https://github.com/radioastronomyio/learn-git-spec-driven-gaming)"
---
-->

# Learn Git: Spec-Driven Gaming

> Learn Git and spec-driven development by building a Breakout game. You write the specs. An AI writes the code. You play the game to decide if it's right.

Two or more people. One game. Nobody writes code. An AI builds the game from specs. The participants play it, review it, and decide if it's good. Git tracks the whole thing: specs, code, reviews, and history. By the end, everyone knows how to fork, clone, branch, commit, PR, and merge because they did it while building something real.

---

## How It Works

You describe what the game should do in game terms: "when the ball hits a brick, the brick disappears and the ball bounces." An AI assistant translates that into JavaScript. You open `game/index.html` in your browser and play. If the physics feel wrong, if a sound is missing, if a feature doesn't work, you refine the spec and the AI tries again.

The spec is the artifact you own. The playtest is your validation. You don't need to read code to know if the game works. A gamer knows when the ball is bouncing wrong.

Git becomes incidental to the work. Nobody studies branching in the abstract. They branch because they're adding sticky paddles and need to keep that separate from the power-up system someone else is building. Pull requests aren't an exercise; they're how you share your game with your teammate for playtesting.

---

## Getting Started

**Prerequisites:** A GitHub account, Git installed on your machine, a modern web browser, and an AI assistant that can read your project files.

**Quick start:**

1. **Fork** this repository into your account (or your organization)
2. **Clone** your fork locally
3. **Read through the repository** before connecting your AI (see [docs/getting-started.md](docs/getting-started.md))
4. **Connect your AI** to the project (see [docs/ai-setup.md](docs/ai-setup.md))
5. **Branch, build, playtest, commit, PR, review, merge**

The full walkthrough is in [docs/getting-started.md](docs/getting-started.md). It covers every step from fork to first pull request, introducing Git concepts through use rather than lecture.

---

## The Three Rounds

### Round 1: Build the Foundation

The first participant builds the baseline Breakout game from `spec/baseline.md`, then picks 3 to 5 features from `spec/round-1-features.md`. These are visually rewarding additions: sound effects, particle effects, ball trails, music, speed ramps. The result is a complete, playable game. They open a PR for review.

### Round 2: Extend the Gameplay

The second participant playtests the Round 1 game, merges it, then picks features from `spec/round-2-features.md`. These are gameplay-focused: power-up drops, multi-hit bricks, sticky paddle, combo scoring. They build on the foundation and interact with Round 1 features. Another PR, another review.

### Round 3: Polish (Teams of 3+)

A third participant picks from `SUGGESTIONS.md` or invents new features. Their PR requires approval from everyone who built before them. The dynamic shifts: the polisher proposes, the builders judge.

Each round teaches more Git naturally. Round 1 covers the basic flow. Round 2 introduces building on someone else's work. Round 3 adds multi-reviewer PRs and potential merge conflicts.

---

## The Game

Breakout. HTML, CSS, and vanilla JavaScript. No frameworks, no build tools, no server required. Open `game/index.html` in a browser and play.

The game uses pixel art sprites from the included Pixeltier Breakout Asset Pack: paddles, balls, blocks (with damage states), power-up icons (with animations), and a star sky background. Pixel fonts and music loops are also included. All assets are free-licensed for personal and commercial use.

---

## Repository Structure

```
learn-git-spec-driven-gaming/
├── assets/                       # Asset packs (sprites, fonts, music, reference)
│   ├── pixeltiers-breakout-asset-pack/
│   ├── cosmic-breakout-html-game-template-free/
│   ├── fonts/
│   ├── music/
│   └── README.md
├── docs/                         # Documentation
│   ├── documentation-standards/  # Template library and guidelines
│   ├── ai-setup.md               # How to connect your AI assistant
│   ├── game-design-document.md   # Learning experience design
│   └── getting-started.md        # Step-by-step walkthrough
├── game/                         # The Breakout game
│   ├── index.html                # Game source (starts as placeholder)
│   └── assets/                   # Sprites, fonts, audio used by the game
├── internal-files/               # Source materials (gitignored)
├── recycle/                      # Removed files (gitignored)
├── spec/                         # Specs for AI execution
│   ├── baseline.md               # Minimum viable Breakout
│   ├── round-1-features.md       # Foundation features
│   └── round-2-features.md       # Gameplay features
├── tests/                        # Test suites
├── work-logs/                    # Development history
├── .gitignore
├── AGENTS.md                     # AI assistant context
├── CLAUDE.md                     # Pointer to AGENTS.md
├── CONTRIBUTING.md               # Branch naming, PR process
├── GIT-REFERENCE.md              # Git command cheat sheet
├── README.md                     # This file
└── SUGGESTIONS.md                # Feature backlog for Round 3+
```

---

## Architecture

No servers, no deployment, no build step. The game runs locally in a browser.

| Component | Implementation |
|-----------|----------------|
| Game engine | HTML5 Canvas + vanilla JavaScript |
| Assets | Pixel art sprites loaded from `game/assets/` |
| Audio (SFX) | Web Audio API, synthesized at runtime |
| Audio (music) | .ogg loop files from `game/assets/audio/` |
| Collaboration | Git + GitHub (fork, branch, PR, merge) |
| AI assistant | Any model that can read project files and produce code |

---

## Project Status

| Area | Status |
|------|--------|
| Repository scaffolding | Complete |
| Asset packs | Complete (Pixeltier sprites, fonts, music) |
| Baseline spec | Complete |
| Round 1 feature menu | Complete |
| Round 2 feature menu | Complete |
| Suggestion backlog | Complete |
| Documentation | Complete |
| Game (Round 1) | Not started |
| Game (Round 2) | Not started |
| Game (Round 3) | Not started |

---

## Further Reading

| Document | Purpose |
|----------|---------|
| [Getting Started](docs/getting-started.md) | Full walkthrough from fork to first PR |
| [AI Setup](docs/ai-setup.md) | How to connect your AI assistant |
| [Game Design Document](docs/game-design-document.md) | Why the learning experience works |
| [Baseline Spec](spec/baseline.md) | What the minimum viable game must do |
| [Contributing](CONTRIBUTING.md) | Branch naming, commits, PR process |
| [Git Reference](GIT-REFERENCE.md) | Command cheat sheet |
| [Suggestions](SUGGESTIONS.md) | 50+ feature ideas for future rounds |
